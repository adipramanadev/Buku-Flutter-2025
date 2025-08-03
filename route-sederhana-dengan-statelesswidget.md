# Route Sederhana Dengan Statelesswidget

#### Langkah-langkah Membuat Route dengan StatelessWidget:

1. **StatelessWidget** digunakan untuk membuat halaman yang tidak memiliki state atau perubahan data. Halaman ini biasanya digunakan untuk menampilkan UI yang bersifat statis, seperti halaman informasi, pengaturan, dan lainnya.
2. Menggunakan **Navigator** untuk melakukan navigasi antar halaman.
3. Menggunakan tombol untuk berpindah halaman.

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
      title: 'Flutter Stateless Route Example',
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

class SecondPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Halaman Kedua'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // Navigasi kembali ke FirstPage
            Navigator.pop(context);
          },
          child: Text('Kembali ke Halaman Pertama'),
        ),
      ),
    );
  }
}
```

#### Penjelasan Kode:

1. **`MyApp`**:
   * Ini adalah widget utama yang menjalankan aplikasi. Di dalamnya, kita menggunakan **MaterialApp** untuk menyetel tema aplikasi dan menetapkan halaman utama (home) ke **FirstPage**.
   * **MaterialApp** juga memungkinkan kita menggunakan komponen Material Design di aplikasi.
2. **`FirstPage`**:
   * **FirstPage** adalah widget berbasis **StatelessWidget**, yang berarti tidak memiliki **state** yang berubah. Di halaman ini, terdapat sebuah tombol yang ketika ditekan akan menavigasikan pengguna ke **SecondPage**.
   * **Navigator.push** digunakan untuk berpindah ke halaman baru. Kita menggunakan **MaterialPageRoute** untuk mendefinisikan rute dan halaman tujuan.
3. **`SecondPage`**:
   * **SecondPage** juga merupakan widget berbasis **StatelessWidget**. Halaman ini juga hanya menampilkan sebuah tombol, yang ketika ditekan, akan membawa pengguna kembali ke **FirstPage** menggunakan **Navigator.pop**.
   * **Navigator.pop(context)** digunakan untuk kembali ke halaman sebelumnya, dalam hal ini **FirstPage**.

#### Alur Navigasi:

1. **FirstPage** muncul pertama kali, dengan tombol yang mengarah ke **SecondPage**.
2. Di **SecondPage**, ada tombol yang memungkinkan pengguna untuk kembali ke **FirstPage**.

#### Perbedaan dengan StatefulWidget:

* **StatelessWidget** digunakan ketika halaman tersebut tidak perlu merespons perubahan data atau interaksi pengguna yang mengubah UI.
* **StatefulWidget**, di sisi lain, digunakan ketika ada data atau status yang perlu diperbarui berdasarkan interaksi pengguna, misalnya ketika mengubah nilai atau menampilkan informasi dinamis.

#### Kesimpulan:

Penggunaan **StatelessWidget** sangat cocok untuk aplikasi yang memiliki tampilan statis atau halaman-halaman yang tidak memerlukan pembaruan UI setelah pertama kali dibangun. Navigasi antar halaman menggunakan **Navigator.push** dan **Navigator.pop** untuk berpindah dan kembali antar halaman.
