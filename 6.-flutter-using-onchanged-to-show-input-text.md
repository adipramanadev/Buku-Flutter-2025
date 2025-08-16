# Flutter: Using onChanged to show input text

#### Contoh Kode: Menggunakan `onChanged` untuk Menampilkan Teks Input

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: InputTextDemo(),
    );
  }
}

class InputTextDemo extends StatefulWidget {
  @override
  _InputTextDemoState createState() => _InputTextDemoState();
}

class _InputTextDemoState extends State<InputTextDemo> {
  String _inputText = ''; // Variabel untuk menyimpan teks input

  // Fungsi untuk memperbarui teks input
  void _updateText(String text) {
    setState(() {
      _inputText = text; // Memperbarui teks input
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Demo onChanged'),
      ),
      body: Padding(
        padding: EdgeInsets.all(16.0),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            TextField(
              onChanged: _updateText, // Menggunakan onChanged untuk mendengarkan perubahan teks
              decoration: InputDecoration(
                labelText: 'Masukkan teks',
                border: OutlineInputBorder(),
              ),
            ),
            SizedBox(height: 20),
            Text(
              'Teks Input: $_inputText', // Menampilkan teks yang dimasukkan
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

1. **`TextField` Widget**:
   * **`onChanged`**: Callback ini dipanggil setiap kali teks yang dimasukkan oleh pengguna berubah. Fungsi yang diberikan (dalam contoh ini adalah `_updateText`) akan menerima teks yang dimasukkan dan memperbarui state.
2. **State Management**:
   * Kita menggunakan **StatefulWidget** (`InputTextDemo`) karena kita perlu memperbarui tampilan saat ada perubahan data (teks yang dimasukkan).
   * **`setState()`** digunakan untuk memperbarui state `_inputText` agar UI bisa diperbarui secara otomatis ketika teks berubah.
3. **Menampilkan Input**:
   * Setelah teks diperbarui dalam **state**, kita menampilkan teks tersebut di bawah **TextField** menggunakan widget **Text**.

#### Fungsi `onChanged`:

* **`onChanged`** berguna untuk mendeteksi dan merespons setiap perubahan teks yang dimasukkan oleh pengguna secara langsung.
* Dengan cara ini, teks yang dimasukkan langsung ditampilkan di layar tanpa perlu melakukan tindakan tambahan, seperti menekan tombol.

Dengan contoh di atas, setiap perubahan teks yang dimasukkan oleh pengguna langsung terlihat di bawah kolom input, memberikan pengalaman pengguna yang lebih interaktif dan responsif.
