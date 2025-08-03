# Tab Navigation

**Tab Navigation** adalah teknik yang digunakan untuk membagi aplikasi menjadi beberapa layar atau halaman yang berbeda, yang dapat diakses melalui tab di bagian atas atau bawah aplikasi. Flutter menyediakan berbagai cara untuk mengimplementasikan **Tab Navigation**, salah satunya menggunakan **`TabBar`** dan **`TabController`**.

#### Contoh Implementasi Tab Navigation di Flutter

Berikut adalah contoh bagaimana membuat aplikasi dengan **Tab Navigation** menggunakan **`TabBar`** dan **`TabBarView`**.

#### Contoh Kode: Tab Navigation di Flutter

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Tab Navigation Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: TabNavigationDemo(), // Halaman utama dengan Tab Navigation
    );
  }
}

class TabNavigationDemo extends StatefulWidget {
  @override
  _TabNavigationDemoState createState() => _TabNavigationDemoState();
}

class _TabNavigationDemoState extends State<TabNavigationDemo> with SingleTickerProviderStateMixin {
  // Deklarasi TabController untuk mengontrol tab
  late TabController _tabController;

  @override
  void initState() {
    super.initState();
    // Membuat TabController dengan jumlah tab (3 tab)
    _tabController = TabController(length: 3, vsync: this);
  }

  @override
  void dispose() {
    // Jangan lupa untuk menutup controller saat tidak digunakan
    _tabController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Tab Navigation'),
        bottom: TabBar(
          controller: _tabController,
          tabs: [
            Tab(text: 'Tab 1'),
            Tab(text: 'Tab 2'),
            Tab(text: 'Tab 3'),
          ],
        ),
      ),
      body: TabBarView(
        controller: _tabController,
        children: [
          Center(child: Text('Konten Tab 1')),
          Center(child: Text('Konten Tab 2')),
          Center(child: Text('Konten Tab 3')),
        ],
      ),
    );
  }
}
```

#### Penjelasan Kode:

1. **`TabController`**:
   * Kita menggunakan **`TabController`** untuk mengontrol tab yang aktif. `TabController` mengelola animasi tab dan transisi antar tab.
   * Pada **`initState()`**, kita menginisialisasi **`TabController`** dengan panjang jumlah tab (dalam hal ini 3 tab) dan menyediakan **`vsync`** yang digunakan untuk animasi.
2. **`TabBar`**:
   * **`TabBar`** adalah widget yang menampilkan tab-tab di bagian atas aplikasi.
   * Setiap tab didefinisikan menggunakan widget **`Tab`** di dalam daftar **`tabs`**. Di sini kita menggunakan **`Text`** untuk menampilkan label tab.
3. **`TabBarView`**:
   * **`TabBarView`** adalah widget yang menampilkan konten untuk masing-masing tab.
   * Setiap tab akan menampilkan widget yang berbeda. Dalam contoh ini, kita hanya menampilkan teks sebagai konten untuk setiap tab.
4. **`SingleTickerProviderStateMixin`**:
   * Mixin ini digunakan untuk memberikan **`vsync`** pada **`TabController`**. **`vsync`** digunakan untuk mengoptimalkan animasi dengan memastikan animasi hanya dijalankan ketika widget sedang aktif di layar.

#### Alur Kerja:

1. **TabBar**: Menampilkan tab dengan label "Tab 1", "Tab 2", dan "Tab 3".
2. **TabBarView**: Menampilkan konten sesuai dengan tab yang dipilih. Misalnya, ketika tab pertama dipilih, konten untuk "Tab 1" akan ditampilkan.
3. Pengguna dapat beralih antara tab dengan cara mengklik tab yang diinginkan, dan tampilan akan berubah sesuai dengan konten yang sesuai dengan tab tersebut.

#### Tambahan Fitur:

*   **Tab dengan Ikon**: Kamu bisa menggunakan ikon selain teks pada tab. Contoh:

    ```dart
    Tab(icon: Icon(Icons.home))
    ```
* **TabBar di Bottom**: Jika kamu ingin meletakkan tab di bagian bawah layar, kamu bisa menambahkan `bottom` di **`Scaffold`** dan menggunakan **`BottomAppBar`**.

Dengan pendekatan **Tab Navigation** ini, kamu bisa dengan mudah menavigasi antar halaman atau fitur di dalam aplikasi yang memiliki banyak bagian, sehingga memberikan pengalaman pengguna yang lebih baik.
