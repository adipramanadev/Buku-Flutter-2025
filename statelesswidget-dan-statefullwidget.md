# StatelessWidget Dan StateFullWidget

Dalam **Flutter**, ada dua jenis widget utama yang digunakan untuk membangun antarmuka pengguna, yaitu **StatelessWidget** dan **StatefulWidget**. Keduanya digunakan untuk membangun tampilan antarmuka, tetapi berbeda dalam hal bagaimana mereka menangani perubahan data dan pembaruan tampilan.

#### 1. **StatelessWidget**

**StatelessWidget** adalah widget yang tidak memiliki keadaan yang dapat berubah. Artinya, setelah widget ini dibangun, tampilannya tidak akan berubah lagi selama aplikasi berjalan, kecuali ada perubahan dari luar (misalnya, melalui parameter atau data dari widget induk).

* **Ciri-ciri:**
  * Tidak memiliki **state** yang dapat berubah.
  * Setelah pertama kali dibangun, widget ini tetap statis.
  * Umumnya digunakan untuk elemen UI yang tidak perlu diubah setelah ditampilkan, seperti ikon, teks statis, tombol, dsb.
*   **Contoh:**

    ```dart
    class MyStatelessWidget extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        return Scaffold(
          appBar: AppBar(
            title: Text('Stateless Widget Example'),
          ),
          body: Center(
            child: Text('Hello, Flutter!'),
          ),
        );
      }
    }
    ```

#### 2. **StatefulWidget**

**StatefulWidget** adalah widget yang memiliki **state** atau keadaan yang dapat berubah seiring waktu. Ketika state berubah, widget ini akan di-rebuild (dibangun ulang) untuk mencerminkan perubahan tersebut di UI.

* **Ciri-ciri:**
  * Memiliki state yang dapat berubah.
  * Ketika state berubah, widget ini akan memperbarui tampilan dengan memanggil metode **setState()**.
  * Digunakan ketika kamu perlu memperbarui UI berdasarkan interaksi pengguna atau perubahan data, seperti form input, animasi, atau widget dinamis lainnya.
*   **Contoh:**

    ```dart
    class MyStatefulWidget extends StatefulWidget {
      @override
      _MyStatefulWidgetState createState() => _MyStatefulWidgetState();
    }

    class _MyStatefulWidgetState extends State<MyStatefulWidget> {
      int _counter = 0;

      void _incrementCounter() {
        setState(() {
          _counter++;
        });
      }

      @override
      Widget build(BuildContext context) {
        return Scaffold(
          appBar: AppBar(
            title: Text('Stateful Widget Example'),
          ),
          body: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                Text('You have pressed the button this many times:'),
                Text('$_counter', style: Theme.of(context).textTheme.headline4),
              ],
            ),
          ),
          floatingActionButton: FloatingActionButton(
            onPressed: _incrementCounter,
            tooltip: 'Increment',
            child: Icon(Icons.add),
          ),
        );
      }
    }
    ```

#### Perbedaan utama:

* **StatelessWidget**: Tidak memiliki state yang berubah, hanya digunakan untuk tampilan statis.
* **StatefulWidget**: Memiliki state yang dapat berubah dan menyebabkan tampilan di-rebuild saat state berubah.

Secara umum, gunakan **StatelessWidget** untuk elemen UI yang tidak perlu diperbarui setelah ditampilkan, dan gunakan **StatefulWidget** ketika ada interaksi atau perubahan data yang perlu diperbarui di UI.
