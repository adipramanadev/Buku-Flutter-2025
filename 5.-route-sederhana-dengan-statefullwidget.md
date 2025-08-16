# Route Sederhana Dengan Statefullwidget

#### Langkah-langkah Membuat Route dengan StatefulWidget:

1. **StatefulWidget** digunakan untuk membuat halaman yang bisa berubah, misalnya menampilkan data yang dapat diubah oleh pengguna.
2. Menggunakan **Navigator** untuk melakukan navigasi antar halaman.
3. Menyediakan aksi untuk berpindah halaman menggunakan tombol atau elemen lainnya.

#### Contoh Kode:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Route Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: FirstPage(), // Halaman pertama yang ditampilkan
    );
  }
}

class FirstPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Halaman Pertama'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // Navigasi ke SecondPage
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => SecondPage()),
            );
          },
          child: Text('Ke Halaman Kedua'),
        ),
      ),
    );
  }
}

class SecondPage extends StatefulWidget {
  @override
  _SecondPageState createState() => _SecondPageState();
}

class _SecondPageState extends State<SecondPage> {
  int _counter = 0; // Variabel yang akan berubah (state)

  void _incrementCounter() {
    setState(() {
      _counter++; // Mengubah state dan memperbarui tampilan
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Halaman Kedua'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'Counter: $_counter',
              style: TextStyle(fontSize: 24),
            ),
            ElevatedButton(
              onPressed: _incrementCounter,
              child: Text('Tambah Counter'),
            ),
            ElevatedButton(
              onPressed: () {
                // Navigasi kembali ke FirstPage
                Navigator.pop(context);
              },
              child: Text('Kembali ke Halaman Pertama'),
            ),
          ],
        ),
      ),
    );
  }
}
```

#### Penjelasan Kode:

1. **`MyApp`**: Ini adalah widget utama yang menjalankan aplikasi. Di sini, kita menggunakan **MaterialApp** yang menyertakan tema dan halaman utama **FirstPage**.
2. **`FirstPage`**: Halaman pertama yang menampilkan tombol. Ketika tombol ditekan, aplikasi akan melakukan navigasi ke **SecondPage** menggunakan **Navigator.push**.
   * **Navigator.push**: Digunakan untuk berpindah ke halaman baru. Di sini, kita membuat **MaterialPageRoute** yang menerima builder dan mengarahkan ke **SecondPage**.
3. **`SecondPage`**: Ini adalah **StatefulWidget** yang memiliki sebuah state (\_counter) yang bisa berubah.
   * **State** digunakan untuk menjaga nilai counter (\_counter) dan memperbarui tampilan setiap kali tombol ditekan.
   * Fungsi **\_incrementCounter()** menggunakan **setState** untuk memperbarui nilai counter dan mengubah tampilan.
   * **Navigator.pop(context)** digunakan untuk kembali ke halaman sebelumnya (FirstPage).
4. **Hot Reload**: Ketika kita mengubah nilai counter di **SecondPage**, aplikasi akan memperbarui tampilan secara otomatis tanpa perlu memuat ulang aplikasi.

#### Alur Navigasi:

1. **FirstPage** muncul pertama kali, dengan tombol yang mengarah ke **SecondPage**.
2. Di **SecondPage**, kita dapat menambah nilai counter menggunakan tombol, dan kita dapat kembali ke **FirstPage** menggunakan tombol "Kembali ke Halaman Pertama".

Dengan menggunakan **StatefulWidget**, kita bisa membuat halaman yang interaktif, yang memungkinkan perubahan data atau tampilan ketika pengguna berinteraksi dengan elemen UI.
