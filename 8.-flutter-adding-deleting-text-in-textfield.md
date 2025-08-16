# Flutter: Adding-Deleting text in TextField

Di Flutter, kita bisa menambahkan atau menghapus teks di **`TextField`** dengan menggunakan **`TextEditingController`**. **`TextEditingController`** memungkinkan kita untuk mengelola teks yang dimasukkan di **`TextField`**, termasuk menambah, menghapus, atau memodifikasi teks secara langsung.

#### Contoh Kode: Menambah dan Menghapus Teks di **`TextField`**

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: TextFieldDemo(),
    );
  }
}

class TextFieldDemo extends StatefulWidget {
  @override
  _TextFieldDemoState createState() => _TextFieldDemoState();
}

class _TextFieldDemoState extends State<TextFieldDemo> {
  // Membuat TextEditingController untuk mengelola teks
  TextEditingController _controller = TextEditingController();

  // Fungsi untuk menambah teks
  void _addText(String text) {
    setState(() {
      _controller.text = _controller.text + text; // Menambahkan teks
    });
  }

  // Fungsi untuk menghapus teks
  void _clearText() {
    setState(() {
      _controller.clear(); // Menghapus teks di TextField
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Tambah dan Hapus Teks di TextField'),
      ),
      body: Padding(
        padding: EdgeInsets.all(16.0),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            TextField(
              controller: _controller, // Menghubungkan TextField dengan controller
              decoration: InputDecoration(
                labelText: 'Masukkan teks',
                border: OutlineInputBorder(),
              ),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                _addText('Flutter'); // Menambahkan teks "Flutter"
              },
              child: Text('Tambah Teks "Flutter"'),
            ),
            SizedBox(height: 10),
            ElevatedButton(
              onPressed: _clearText, // Menghapus teks
              child: Text('Hapus Teks'),
            ),
            SizedBox(height: 20),
            Text(
              'Teks Saat Ini: ${_controller.text}', // Menampilkan teks yang ada saat ini
              style: TextStyle(fontSize: 20),
            ),
          ],
        ),
      ),
    );
  }
}
```

#### Penjelasan Kode:

1. **`TextEditingController`**:
   * Kita menggunakan **`TextEditingController`** untuk mengontrol teks yang ada di **`TextField`**. Dengan **`TextEditingController`**, kita bisa menambah teks, menghapus teks, atau memodifikasi teks secara langsung.
   * **`_controller`** adalah variabel **`TextEditingController`** yang kita gunakan untuk mengelola teks dalam **`TextField`**.
2.  **Menambah Teks**:

    * Fungsi **`_addText`** digunakan untuk menambahkan teks ke dalam **`TextField`**. Di sini, kita menambahkan string `'Flutter'` ke teks yang sudah ada dengan cara menggabungkan teks lama dengan teks baru menggunakan operator `+`.

    ```dart
    _controller.text = _controller.text + text;
    ```
3.  **Menghapus Teks**:

    * Fungsi **`_clearText`** digunakan untuk menghapus seluruh teks dalam **`TextField`** dengan menggunakan metode **`clear()`** pada **`TextEditingController`**.

    ```dart
    _controller.clear();
    ```
4. **Menampilkan Teks**:
   * Di bagian bawah, kita menampilkan teks yang ada dalam **`TextField`** saat ini dengan **`_controller.text`**.

#### Fungsi `TextEditingController`:

* **Menambah Teks**: Kita bisa menambah teks baru ke **`TextField`** dengan menggabungkan **`_controller.text`** dengan teks baru.
* **Menghapus Teks**: Untuk menghapus teks di **`TextField`**, kita cukup memanggil metode **`clear()`** pada **`TextEditingController`**.

Dengan contoh ini, kamu bisa melihat cara untuk menambah dan menghapus teks dalam **`TextField`** di Flutter secara dinamis dengan memanfaatkan **`TextEditingController`**.
