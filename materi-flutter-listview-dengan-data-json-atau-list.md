# Materi Flutter: ListView dengan Data JSON atau List

Tujuan: Memahami cara menampilkan daftar data di Flutter menggunakan `ListView` dari dua sumber: **List statis** dan **JSON** (lokal/hardcode maupun dari API).

***

### 1) Konsep Dasar `ListView`

* `ListView(children: [...])` → cocok untuk jumlah item sedikit.
* `ListView.builder(itemCount, itemBuilder)` → efisien untuk list panjang, render sesuai kebutuhan (lazy).
* `ListView.separated` → ada pemisah antar item.
* `ListTile` → widget praktis untuk baris daftar (leading, title, subtitle, trailing).

```dart
ListView.builder(
  itemCount: items.length,
  itemBuilder: (context, index) {
    final item = items[index];
    return ListTile(title: Text(item));
  },
)
```

***

### 2) Sumber Data: List Statis (Hardcoded)

Contoh sederhana memakai list string.

```dart
class CitiesPage extends StatelessWidget {
  final cities = const ['Jakarta', 'Bandung', 'Surabaya', 'Medan', 'Makassar'];

  const CitiesPage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Kota')),
      body: ListView.separated(
        itemCount: cities.length,
        separatorBuilder: (_, __) => const Divider(height: 1),
        itemBuilder: (context, i) => ListTile(
          leading: CircleAvatar(child: Text('${i+1}')),
          title: Text(cities[i]),
          trailing: const Icon(Icons.chevron_right),
          onTap: () {},
        ),
      ),
    );
  }
}
```

> Gunakan `const` di mana mungkin agar performa lebih baik.

***

### 3) Sumber Data: JSON Lokal (Hardcode Map/List)

* Cocok untuk belajar struktur JSON tanpa koneksi internet.

```dart
final List<Map<String, dynamic>> products = [
  {"id": 1, "name": "Mouse", "price": 120000},
  {"id": 2, "name": "Keyboard", "price": 250000},
];

class ProductList extends StatelessWidget {
  const ProductList({super.key});
  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: products.length,
      itemBuilder: (context, index) {
        final p = products[index];
        return ListTile(
          title: Text(p['name']),
          subtitle: Text('Rp ${p['price']}'),
        );
      },
    );
  }
}
```

***

### 4) Sumber Data: JSON → Model Class

Membuat model mempermudah parsing & maintenance.

```dart
class Product {
  final int id;
  final String name;
  final int price;

  Product({required this.id, required this.name, required this.price});

  factory Product.fromJson(Map<String, dynamic> json) => Product(
    id: json['id'] as int,
    name: json['name'] as String,
    price: json['price'] as int,
  );
}

final jsonList = [
  {"id": 1, "name": "Mouse", "price": 120000},
  {"id": 2, "name": "Keyboard", "price": 250000},
];

final productsModel = jsonList.map((e) => Product.fromJson(e)).toList();
```

Penggunaan di `ListView`:

```dart
ListView.builder(
  itemCount: productsModel.length,
  itemBuilder: (context, i) {
    final p = productsModel[i];
    return ListTile(
      title: Text(p.name),
      subtitle: Text('Rp ${p.price}'),
    );
  },
)
```

***

### 5) Sumber Data: JSON dari API (HTTP)

* Pakai paket `http` dan `FutureBuilder` untuk menunggu jaringan.

```dart
import 'package:http/http.dart' as http;
import 'dart:convert';

class Post {
  final int id; final String title; final String body;
  Post({required this.id, required this.title, required this.body});
  factory Post.fromJson(Map<String, dynamic> j) => Post(
    id: j['id'], title: j['title'], body: j['body'],
  );
}

Future<List<Post>> fetchPosts() async {
  final res = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts'));
  if (res.statusCode != 200) throw Exception('Gagal memuat');
  final data = jsonDecode(res.body) as List;
  return data.map((e) => Post.fromJson(e)).toList();
}

class PostListPage extends StatelessWidget {
  const PostListPage({super.key});
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Posts')),
      body: FutureBuilder<List<Post>>(
        future: fetchPosts(),
        builder: (context, snap) {
          if (snap.connectionState == ConnectionState.waiting) {
            return const Center(child: CircularProgressIndicator());
          }
          if (snap.hasError) {
            return Center(child: Text('Error: ${snap.error}'));
          }
          final posts = snap.data!;
          if (posts.isEmpty) return const Center(child: Text('Kosong'));
          return ListView.separated(
            itemCount: posts.length,
            separatorBuilder: (_, __) => const Divider(height: 1),
            itemBuilder: (context, i) {
              final p = posts[i];
              return ListTile(
                title: Text(p.title),
                subtitle: Text(p.body),
                onTap: () {
                  Navigator.push(
                    context,
                    MaterialPageRoute(
                      builder: (_) => DetailPage(post: p),
                    ),
                  );
                },
              );
            },
          );
        },
      ),
    );
  }
}

class DetailPage extends StatelessWidget {
  final Post post; const DetailPage({super.key, required this.post});
  @override
  Widget build(BuildContext context) => Scaffold(
    appBar: AppBar(title: Text('Post #${post.id}')),
    body: Padding(
      padding: const EdgeInsets.all(16),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          Text(post.title, style: Theme.of(context).textTheme.titleLarge),
          const SizedBox(height: 12),
          Text(post.body),
        ],
      ),
    ),
  );
}
```

***

### 6) Custom Item Widget

Pisahkan tampilan item agar rapi dan mudah di-test.

```dart
class ProductTile extends StatelessWidget {
  final Product p; final VoidCallback? onTap;
  const ProductTile({super.key, required this.p, this.onTap});
  @override
  Widget build(BuildContext context) {
    return ListTile(
      leading: CircleAvatar(child: Text(p.name[0].toUpperCase())),
      title: Text(p.name),
      subtitle: Text('Rp ${p.price}'),
      trailing: const Icon(Icons.chevron_right),
      onTap: onTap,
    );
  }
}
```

Penggunaan:

```dart
ListView.builder(
  itemCount: productsModel.length,
  itemBuilder: (_, i) => ProductTile(p: productsModel[i], onTap: () {}),
)
```

***

### 7) Refresh & Pagination Sederhana

#### Pull-to-Refresh

```dart
RefreshIndicator(
  onRefresh: () async { /* fetch ulang */ },
  child: ListView.builder(
    itemCount: items.length,
    itemBuilder: (_, i) => ListTile(title: Text(items[i].toString())),
  ),
)
```

#### Infinite Scroll (ScrollController)

```dart
class InfiniteList extends StatefulWidget { const InfiniteList({super.key});
  @override State<InfiniteList> createState() => _InfiniteListState(); }

class _InfiniteListState extends State<InfiniteList> {
  final _c = ScrollController();
  final _items = <int>[]; bool _loading = false; int _page = 1; final _pageSize = 20;

  @override void initState() { super.initState(); _load(); _c.addListener(_onScroll); }
  void _onScroll() {
    if (_c.position.pixels >= _c.position.maxScrollExtent - 200 && !_loading) _load();
  }

  Future<void> _load() async {
    setState(() => _loading = true);
    await Future.delayed(const Duration(milliseconds: 800)); // simulasi API
    final start = (_page - 1) * _pageSize;
    _items.addAll(List.generate(_pageSize, (i) => start + i));
    _page++; setState(() => _loading = false);
  }

  @override Widget build(BuildContext context) {
    return ListView.builder(
      controller: _c,
      itemCount: _items.length + 1,
      itemBuilder: (_, i) {
        if (i == _items.length) {
          return _loading ? const Padding(
            padding: EdgeInsets.all(16), child: Center(child: CircularProgressIndicator()),
          ) : const SizedBox.shrink();
        }
        return ListTile(title: Text('Item ${_items[i]}'));
      },
    );
  }

  @override void dispose() { _c.dispose(); super.dispose(); }
}
```

***

### 8) Error & Empty State

* Saat gagal fetch, tampilkan pesan & tombol coba lagi.
* Jika list kosong, tampilkan ilustrasi/teks “Data kosong”.

```dart
Widget buildBody(AsyncSnapshot<List<Post>> snap) {
  if (snap.connectionState == ConnectionState.waiting) {
    return const Center(child: CircularProgressIndicator());
  }
  if (snap.hasError) {
    return Center(
      child: Column(
        mainAxisSize: MainAxisSize.min,
        children: [
          Text('Terjadi kesalahan'),
          const SizedBox(height: 8),
          ElevatedButton(onPressed: () { /* panggil setState/fetch ulang */ }, child: const Text('Coba Lagi')),
        ],
      ),
    );
  }
  final data = snap.data ?? [];
  if (data.isEmpty) return const Center(child: Text('Belum ada data'));
  return ListView.builder(
    itemCount: data.length,
    itemBuilder: (_, i) => ListTile(title: Text(data[i].title)),
  );
}
```

***

### 9) Tips Performa & Aksesibilitas

* Gunakan `ListView.builder` untuk list besar.
* Tambahkan `key` unik pada item jika data dinamis.
* Gunakan `const` pada widget statis.
* Batasi pekerjaan berat di `itemBuilder`.
* Pastikan kontras teks, ukuran font, dan tap target memadai.

***

### 10) Latihan Praktik

1. **List Statis**: tampilkan daftar 20 nama buah dengan `ListView.separated`.
2. **JSON Lokal → Model**: render katalog produk dengan `ProductTile` kustom.
3. **API**: ambil `https://jsonplaceholder.typicode.com/users`, tampilkan `name`, `email`, `phone`. Klik item → halaman detail.
4. **Refresh**: tambah `RefreshIndicator` pada daftar users.
5. **Pagination**: implementasi infinite scroll (bisa dengan simulasi data).

***

### 11) Struktur Folder Sederhana (Saran)

```
lib/
  main.dart
  features/
    users/
      data/
        user_api.dart      // http request
        user_model.dart    // fromJson/toJson
      presentation/
        users_page.dart    // ListView + FutureBuilder
        user_detail_page.dart
```

***

### 12) Tantangan Mini-Project

**Directory App**

* Ambil daftar kontak dari API, tampilkan dengan `ListView.separated` & avatar.
* Fitur: pencarian sederhana (filter list), pull-to-refresh, halaman detail.
* Bonus: simpan favorit ke lokal (SharedPreferences) dan tambahkan badge pada item favorit.

***

Dengan materi ini, kamu siap membangun tampilan daftar yang efisien dari berbagai sumber data di Flutter.
