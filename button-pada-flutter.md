# Button Pada Flutter

Di Flutter, **Button** adalah widget interaktif yang digunakan untuk menangani input dari pengguna. Flutter menyediakan berbagai jenis tombol, yang dapat disesuaikan sesuai dengan kebutuhan aplikasi. Berikut adalah beberapa jenis tombol yang paling umum digunakan di Flutter beserta penjelasan dan contoh penggunaannya.

#### 1. **ElevatedButton**

**ElevatedButton** adalah tombol yang muncul dengan latar belakang berwarna solid dan memiliki efek bayangan untuk memberikan kesan "diangkat" (elevated). Tombol ini digunakan ketika kamu ingin tombol terlihat lebih menonjol dan mudah terlihat.

*   **Contoh Penggunaan:**

    ```dart
    ElevatedButton(
      onPressed: () {
        // Aksi yang dilakukan saat tombol ditekan
        print("ElevatedButton pressed");
      },
      child: Text("Klik Saya"),
    );
    ```

#### 2. **TextButton**

**TextButton** adalah tombol dengan tampilan minimalis, tanpa latar belakang atau bayangan. Tombol ini cocok digunakan untuk tombol yang tidak membutuhkan efek visual yang mencolok, seperti tombol di dalam dialog atau tombol di bagian bawah aplikasi.

*   **Contoh Penggunaan:**

    ```dart
    TextButton(
      onPressed: () {
        // Aksi yang dilakukan saat tombol ditekan
        print("TextButton pressed");
      },
      child: Text("Klik Saya"),
    );
    ```

#### 3. **OutlinedButton**

**OutlinedButton** adalah tombol yang memiliki border tipis di sekelilingnya, tanpa latar belakang. Tombol ini memberikan tampilan lebih ringan dibandingkan **ElevatedButton**, tetapi masih memberikan interaktivitas dengan menampilkan border saat dihover atau ditekan.

*   **Contoh Penggunaan:**

    ```dart
    OutlinedButton(
      onPressed: () {
        // Aksi yang dilakukan saat tombol ditekan
        print("OutlinedButton pressed");
      },
      child: Text("Klik Saya"),
    );
    ```

#### 4. **FloatingActionButton**

**FloatingActionButton** (FAB) adalah tombol yang mengapung di atas konten aplikasi, biasanya digunakan untuk aksi utama yang sering dilakukan, seperti membuat entri baru atau mengirim data. Biasanya, FAB diletakkan di sudut bawah kanan layar.

*   **Contoh Penggunaan:**

    ```dart
    FloatingActionButton(
      onPressed: () {
        // Aksi yang dilakukan saat FAB ditekan
        print("FloatingActionButton pressed");
      },
      child: Icon(Icons.add),
    );
    ```

#### 5. **IconButton**

**IconButton** adalah tombol yang hanya berisi ikon, biasanya digunakan untuk menambahkan tombol dengan ikon di dalam toolbar atau bagian lain dari antarmuka pengguna.

*   **Contoh Penggunaan:**

    ```dart
    IconButton(
      icon: Icon(Icons.favorite),
      onPressed: () {
        // Aksi yang dilakukan saat ikon ditekan
        print("IconButton pressed");
      },
    );
    ```

#### 6. **Custom Button**

Selain tombol standar yang sudah disediakan Flutter, kamu juga bisa membuat tombol kustom dengan menggunakan **GestureDetector** atau **InkWell**, yang memungkinkan kamu untuk membuat tombol dengan lebih banyak kustomisasi, seperti menambahkan animasi atau efek interaktif lainnya.

*   **Contoh Penggunaan (Custom Button dengan InkWell):**

    ```dart
    InkWell(
      onTap: () {
        // Aksi yang dilakukan saat tombol ditekan
        print("Custom InkWell pressed");
      },
      child: Container(
        padding: EdgeInsets.all(16),
        decoration: BoxDecoration(
          color: Colors.blue,
          borderRadius: BorderRadius.circular(8),
        ),
        child: Text(
          "Custom Button",
          style: TextStyle(color: Colors.white),
        ),
      ),
    );
    ```

#### Kesimpulan:

Flutter menawarkan berbagai jenis tombol, seperti **ElevatedButton**, **TextButton**, **OutlinedButton**, **FloatingActionButton**, dan **IconButton**, yang memungkinkan pengembang untuk memilih tombol yang sesuai dengan gaya dan fungsionalitas aplikasi. Selain itu, tombol juga bisa dikustomisasi lebih lanjut dengan menggunakan widget lain seperti **GestureDetector** atau **InkWell**.
