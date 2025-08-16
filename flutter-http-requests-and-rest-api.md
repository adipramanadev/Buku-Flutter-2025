# Flutter: HTTP Requests & REST API

Materi ini dirancang agar pemula bisa memahami cara berkomunikasi dengan server menggunakan **HTTP** dan **REST API** di Flutter.

***

### 1. Apa itu REST API?

* **API (Application Programming Interface)**: jembatan antara aplikasi kita dan server.
* **REST API**: standar pertukaran data menggunakan protokol HTTP (GET, POST, PUT, DELETE).
* **Format data**: biasanya JSON.

Contoh: Aplikasi cuaca → meminta data suhu dari server → server mengembalikan data JSON.

***

### 2. Paket yang Digunakan

Untuk HTTP request di Flutter, gunakan paket **http**:

```yaml
dependencies:
  http: ^1.2.0
```

Lalu jalankan:

```bash
flutter pub get
```

Import di file Dart:

```dart
import 'package:http/http.dart' as http;
import 'dart:convert';
```

***

### 3. HTTP GET Request

**Tujuan**: mengambil data dari server.

Contoh API: [https://jsonplaceholder.typicode.com/posts](https://jsonplaceholder.typicode.com/posts)

```dart
Future<void> getPosts() async {
  final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts'));

  if (response.statusCode == 200) {
    List data = jsonDecode(response.body);
    print(data[0]); // tampilkan post pertama
  } else {
    print('Request gagal: ${response.statusCode}');
  }
}
```

**Penjelasan**:

* `http.get` → ambil data dari URL
* `response.statusCode` → status (200 = OK)
* `jsonDecode` → ubah JSON ke List/Map Dart

***

### 4. HTTP POST Request

**Tujuan**: mengirim data ke server.

```dart
Future<void> createPost() async {
  final response = await http.post(
    Uri.parse('https://jsonplaceholder.typicode.com/posts'),
    headers: {'Content-Type': 'application/json'},
    body: jsonEncode({
      'title': 'Belajar Flutter',
      'body': 'Ini postingan baru',
      'userId': 1,
    }),
  );

  if (response.statusCode == 201) {
    print('Post berhasil dibuat: ${response.body}');
  } else {
    print('Gagal membuat post');
  }
}
```

**Penjelasan**:

* `http.post` → kirim data
* `headers` → memberi tahu server format data (JSON)
* `body` → isi data yang dikirim

***

### 5. HTTP PUT & DELETE

#### Update Data (PUT)

```dart
Future<void> updatePost() async {
  final response = await http.put(
    Uri.parse('https://jsonplaceholder.typicode.com/posts/1'),
    headers: {'Content-Type': 'application/json'},
    body: jsonEncode({
      'id': 1,
      'title': 'Update Judul',
      'body': 'Konten diperbarui',
      'userId': 1,
    }),
  );

  print('Response: ${response.body}');
}
```

#### Hapus Data (DELETE)

```dart
Future<void> deletePost() async {
  final response = await http.delete(
    Uri.parse('https://jsonplaceholder.typicode.com/posts/1'),
  );

  print('Status: ${response.statusCode}');
}
```

***

### 6. Tampilkan Data di Flutter

Contoh menampilkan daftar post:

```dart
class PostListPage extends StatelessWidget {
  Future<List> fetchPosts() async {
    final res = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/posts'));
    return jsonDecode(res.body);
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Daftar Post')),
      body: FutureBuilder(
        future: fetchPosts(),
        builder: (context, snapshot) {
          if (snapshot.connectionState == ConnectionState.waiting) {
            return Center(child: CircularProgressIndicator());
          }
          if (snapshot.hasError) {
            return Center(child: Text('Error: ${snapshot.error}'));
          }
          final posts = snapshot.data as List;
          return ListView.builder(
            itemCount: posts.length,
            itemBuilder: (context, index) {
              return ListTile(
                title: Text(posts[index]['title']),
                subtitle: Text(posts[index]['body']),
              );
            },
          );
        },
      ),
    );
  }
}
```

***

### 7. Best Practice

* Gunakan **Model Class** agar data rapi.
* Pisahkan **Service/API Helper** dari UI.
* Tangani error (timeout, koneksi gagal).
* Jangan simpan API key di kode → gunakan `.env`.
* Jika data banyak, gunakan **pagination**.

***

### 8. Latihan

1. Buat aplikasi sederhana menampilkan daftar **users** dari endpoint `https://jsonplaceholder.typicode.com/users`.
2. Tambahkan fitur **detail user** saat item diklik.
3. Buat form input untuk menambahkan data baru (POST).

***

### 9. Proyek Mini

**Aplikasi Catatan Online**

* Fitur: tampilkan daftar catatan (GET), tambah catatan (POST), edit (PUT), hapus (DELETE).
* Gunakan **ListView** untuk menampilkan catatan.
* Tambahkan notifikasi snackbar untuk feedback.

***

### 10. Referensi

* [Flutter HTTP package](https://pub.dev/packages/http)
* [JSONPlaceholder (API gratis)](https://jsonplaceholder.typicode.com/)

***

