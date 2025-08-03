# Flutter: Using onSubmitted to show input text after submit

Di Flutter, **`onSubmitted`** digunakan untuk menangani tindakan ketika pengguna mengirimkan input melalui **`TextField`** (misalnya, menekan tombol "Enter" pada keyboard). Setelah pengguna mengklik tombol submit atau mengetikkan "Enter", kita bisa menampilkan teks yang dimasukkan.

#### Contoh Kode: Menggunakan `onSubmitted` untuk Menampilkan Teks Setelah Submit

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

  // Fungsi untuk memperbarui teks input setelah submit
  void _submitText(String text) {
    setState(() {
      _inputText = text; // Memperbarui teks input
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Demo onSubmitted'),
      ),
      body: Padding(
        padding: EdgeInsets.all(16.0),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            TextField(
              onSubmitted: _submitText, // Menggunakan onSubmitted untuk mendengarkan submit
              decoration: InputDecoration(
                labelText: 'Masukkan teks',
                border: OutlineInputBorder(),
              ),
            ),
            SizedBox(height: 20),
            Text(
              'Teks Input: $_inputText', // Menampilkan teks yang dimasukkan setelah submit
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
   * **`onSubmitted`**: Callback ini dipanggil ketika pengguna menekan tombol "Enter" atau tombol submit pada keyboard. Fungsi yang diberikan (dalam contoh ini adalah `_submitText`) akan menerima teks yang dimasukkan dan memperbarui state.
2. **State Management**:
   * Kita menggunakan **StatefulWidget** (`InputTextDemo`) karena kita ingin memperbarui tampilan ketika teks diubah oleh pengguna dan kemudian dikirim (submit).
   * **`setState()`** digunakan untuk memperbarui state `_inputText` dan menyebabkan tampilan diperbarui.
3. **Menampilkan Input**:
   * Setelah teks diperbarui dalam **state**, kita menampilkan teks tersebut di bawah **TextField** menggunakan widget **Text**.

#### Fungsi `onSubmitted`:

* **`onSubmitted`** digunakan ketika kita ingin melakukan aksi setelah pengguna menyelesaikan pengeditan dan menekan tombol "Enter" pada keyboard.
* Biasanya digunakan untuk pengumpulan data atau pengiriman formulir.

Dengan contoh di atas, ketika pengguna mengetik teks dan menekan tombol "Enter", teks yang dimasukkan akan langsung ditampilkan di bawah **TextField**, memberikan pengalaman pengguna yang lebih interaktif.
