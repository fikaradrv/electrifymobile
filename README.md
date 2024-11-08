# Electrify Mobile
- Nama : Fikar Hilmi Adhrevi
- NPM : 2306203873
- Kelas : PBP C
<details>
  <summary style="font-size: 30px; font-family: Arial, sans-serif;"><b>Tugas 7</b></summary>

### Cara saya mengimplementasikan checklist

**1. Membuat sebuah program Flutter baru dengan tema E-Commerce yang sesuai dengan tugas-tugas sebelumnya.**
- Membuat proyek Flutter baru dengan nama "electrifymobile" menggunakan perintah `flutter create electrifymobile`
- Masuk ke direktori proyek dan membersihkan template bawaan Flutter
- Membuat file baru `menu.dart` untuk menampung widget halaman utama

**2. Membuat tiga tombol sederhana dengan ikon dan teks untuk:**
- Mengimplementasikan tiga tombol menggunakan `ItemCard` yang dibungkus dalam `GridView.count`
- Membuat class `ItemHomepage` untuk menyimpan properti setiap tombol (nama, ikon, dan warna)
- Menginisialisasi daftar item dalam `List<ItemHomepage>`:
  ```dart
  final List<ItemHomepage> items = [
    ItemHomepage("Lihat Daftar Produk", Icons.list, Colors.blue),
    ItemHomepage("Tambah Produk", Icons.add, Colors.amber),
    ItemHomepage("Logout", Icons.logout, Colors.red),
  ];
  ```

**3. Mengimplementasikan warna-warna yang berbeda untuk setiap tombol:**
- Lihat Daftar Produk: Menggunakan `Colors.blue`
- Tambah Produk: Menggunakan `Colors.amber`
- Logout: Menggunakan `Colors.red`
- Warna diimplementasikan melalui parameter `color` dalam konstruktor `ItemHomepage`

**4. Memunculkan Snackbar dengan tulisan:**
- Mengimplementasikan `onTap` pada widget `InkWell` dalam `ItemCard`
- Menggunakan `ScaffoldMessenger.of(context)` untuk menampilkan SnackBar
- Pesan SnackBar disesuaikan dengan nama tombol yang ditekan:
  ```dart
  ScaffoldMessenger.of(context)
    ..hideCurrentSnackBar()
    ..showSnackBar(
      SnackBar(content: Text("Kamu telah menekan tombol ${item.name}!"))
    );
  ```

### Jelaskan apa yang dimaksud dengan stateless widget dan stateful widget, dan jelaskan perbedaan dari keduanya.

**Stateless Widget:**
- Widget yang bersifat statis/tidak berubah (immutable)
- Tidak memiliki state internal yang bisa berubah selama widget hidup
- Cocok untuk UI yang tidak perlu update berdasarkan interaksi atau perubahan data
- Lebih ringan dan efisien karena tidak perlu mekanisme untuk mengatur state
- Contoh: Text, Icon, IconButton

**Stateful Widget:**
- Widget yang bersifat dinamis dan dapat berubah (mutable)
- Memiliki state internal yang bisa diperbarui selama widget hidup
- Dapat memperbarui tampilan ketika ada interaksi pengguna atau perubahan data
- Menggunakan setState() untuk memicu rebuild widget
- Contoh: Checkbox, TextField, Form

### Sebutkan widget apa saja yang kamu gunakan pada proyek ini dan jelaskan fungsinya.

1. **Structural Widgets:**
   - `MaterialApp`: Widget root untuk implementasi Material Design
   - `Scaffold`: Menyediakan struktur dasar layout Material Design
   - `AppBar`: Bar di bagian atas aplikasi
   - `Column` & `Row`: Mengatur widget secara vertikal dan horizontal

2. **Layout Widgets:**
   - `Container`: Membungkus widget lain dengan kemampuan styling
   - `Padding`: Memberikan padding pada widget
   - `Center`: Menempatkan widget di tengah
   - `GridView`: Menampilkan widget dalam bentuk grid
   - `SizedBox`: Memberikan space kosong dengan ukuran tertentu

3. **Content Widgets:**
   - `Text`: Menampilkan text
   - `Icon`: Menampilkan icon
   - `Card`: Menampilkan content dalam bentuk card
   - `InkWell`: Memberikan efek ripple saat ditekan

### Apa fungsi dari setState()? Jelaskan variabel apa saja yang dapat terdampak dengan fungsi tersebut.

`setState()` adalah method yang digunakan untuk memberitahu framework Flutter bahwa ada perubahan state internal yang memerlukan update UI. 

Variabel yang dapat terdampak:
- Semua variabel yang dideklarasikan sebagai state dalam class StatefulWidget
- Variabel yang digunakan dalam build method yang nilainya berubah
- Variabel yang mempengaruhi tampilan UI

Contoh penggunaan:
```dart
setState(() {
  _counter++; // Variable yang berubah
});
```

### Jelaskan perbedaan antara const dengan final.

**const:**
- Variabel harus diinisialisasi pada saat kompilasi
- Nilai harus sudah diketahui sebelum runtime
- Membuat objek menjadi deeply immutable
- Lebih efisien untuk nilai yang diketahui saat compile time

```dart
const pi = 3.14;
const list = [1, 2, 3]; // List juga immutable
```

**final:**
- Variabel hanya bisa diassign sekali
- Nilai bisa diinisialisasi saat runtime
- Hanya membuat reference immutable, bukan value-nya
- Cocok untuk nilai yang ditentukan saat runtime

```dart
final currentTime = DateTime.now(); // Nilai ditentukan saat runtime
final list = [1, 2, 3]; // List masih bisa dimodifikasi
```

</details>

<details>
  <summary style="font-size: 30px; font-family: Arial, sans-serif;"><b>Tugas 8</b></summary>

### Cara saya mengimplementasikan checklist

**1. Membuat halaman formulir tambah item baru:**

- Membuat file baru `productentry_form.dart` dalam folder `lib/screens` yang nantinya akan berisi form untuk mengisi attribut dari produk
- Mengimplementasikan form dengan 5 elemen input:
  ```dart
  String _name = "";         // Input nama produk
  int _amount = 0;          // Input harga produk
  String _description = ""; // Input deskripsi produk
  int _stock = 0;          // Input stok produk
  int _rating = 0;         // Input rating produk
  ```
  Setiap elemen input ini akan diimplementasikan dengan membuat child pada column yang di wrap dengan padding seperti contoh ini
  ```dart
  Padding(
    padding: const EdgeInsets.all(8.0),
    child: TextFormField(
      decoration: InputDecoration(
        hintText: "Amount",
        labelText: "Amount",
        border: OutlineInputBorder(
          borderRadius: BorderRadius.circular(5.0),
        ),
      ),
      onChanged: (String? value) {
        setState(() {
          _amount = int.tryParse(value!) ?? 0;
        });
      },
      validator: (String? value) {
        if (value == null || value.isEmpty) {
          return "Amount tidak boleh kosong!";
        }
        if (int.tryParse(value) == null) {
          return "Amount harus berupa angka!";
        }
        return null;
      },
    ),
  ),
  ```
- Validasi untuk String (Name & Description):
  ```dart
  validator: (String? value) {
    if (value == null || value.isEmpty) {
      return "Field tidak boleh kosong!";
    }
    return null;
  }
  ```
- Validasi untuk Integer (Amount, Stock & Rating):
  ```dart
  validator: (String? value) {
    if (value == null || value.isEmpty) {
      return "Field tidak boleh kosong!";
    }
    if (int.tryParse(value) == null) {
      return "Field harus berupa angka!";
    }
    return null;
  }
  ```
- Setiap input menggunakan TextFormField dengan validasi:
  - Name & Description: tidak boleh kosong
  - Amount, Stock & Rating: harus berupa angka dan tidak boleh kosong
- Menambahkan tombol Save yang akan memunculkan pop-up data dengan implementasi seperti ini
  ```dart
  child: const Text(
    "Save",
    style: TextStyle(color: Colors.white),
  ),
  ```


**2. Mengarahkan ke halaman form tambah item:**

- Mengimplementasikan navigasi di `product_card.dart` untuk button tambah produk:
  ```dart
  if (item.name == "Tambah Produk") {
    Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => const ProductEntryFormPage()),
    );
  }
  ```
- Mengimplementasikan navigasi di left_drawer.dart untuk drawer:
```dart
ListTile(
  leading: const Icon(Icons.add),
  title: const Text('Tambah Produk'),
  // Bagian redirection ke ProductEntryFormPage
  onTap: () {
    Navigator.push(
      context,
      MaterialPageRoute(
        builder: (context) => const ProductEntryFormPage(),
      ));
  },
),
```
**3. Memunculkan pop-up data form:**

- Menggunakan AlertDialog dalam onPressed tombol Save:
  ```dart
  showDialog(
    context: context,
    builder: (context) {
      return AlertDialog(
        title: const Text('Product berhasil tersimpan'),
        content: SingleChildScrollView(
          child: Column(
            children: [
              Text('Name: $_name'),
              Text('Amount: $_amount'),
              // ... data lainnya
            ],
          ),
        ),
        // ... 
      );
    },
  );
  ```

**4. Membuat drawer aplikasi:**

- Membuat file `left_drawer.dart` dalam folder `lib/widgets`

- Mengimplementasikan Drawer dengan:
  - Header berisi nama aplikasi dan tagline
  ```dart
  DrawerHeader(
      decoration: BoxDecoration(
      color: Theme.of(context).colorScheme.primary,
    ),
    child: const Column(
      children: [
        Text(
          'Electrify',
          textAlign: TextAlign.center,
          style: TextStyle(
            fontSize: 24,
            fontWeight: FontWeight.bold,
            color: Colors.white,
          ),
        ),
        Padding(padding: EdgeInsets.all(8)),
        Text(
          "Ayo beli produk kami!",
          textAlign: TextAlign.center,
          style: TextStyle(
            fontSize: 15,
            color: Colors.white,
            fontWeight: FontWeight.normal,
          ),
        ),
      ],
    ),
  ),
  ```
  - Menu Halaman Utama dengan navigasi ke MyHomePage
  ```dart
  ListTile(
    leading: const Icon(Icons.home_outlined),
    title: const Text('Halaman Utama'),
    // Bagian redirection ke MyHomePage
    onTap: () {
      Navigator.pushReplacement(
          context,
          MaterialPageRoute(
            builder: (context) => MyHomePage(),
          ));
    },
  ),
  ```
  - Menu Tambah Produk dengan navigasi ke ProductEntryFormPage
  ```dart
  ListTile(
    leading: const Icon(Icons.add),
    title: const Text('Tambah Produk'),
    // Bagian redirection ke ProductEntryFormPage
    onTap: () {
      Navigator.push(
        context,
        MaterialPageRoute(
          builder: (context) => const ProductEntryFormPage(),
        ));
    },
  ),
  ```
- Menambahkan drawer ke Scaffold di setiap halaman:
  ```dart
  drawer: const LeftDrawer(),
  ```


### Apa kegunaan `const` di Flutter? Jelaskan apa keuntungan ketika menggunakan `const` pada kode Flutter. Kapan sebaiknya kita menggunakan `const`, dan kapan sebaiknya tidak digunakan?

#### Kegunaan `const` di Flutter
`const` digunakan untuk membuat nilai atau objek menjadi konstan, nilai tersebut tidak dapat diubah setelah didefinisikan. Di Flutter, `const` memastikan bahwa objek yang dibuat akan disimpan di memori hanya sekali. Hal ini bermanfaat dalam pengelolaan memori, terutama untuk widget yang statis atau tidak berubah.

#### Keuntungan Menggunakan `const`
1. **Efisiensi Memori**: Dengan menggunakan `const`, Flutter dapat menghemat memori dengan hanya menyimpan satu instance objek yang sama, sehingga mempercepat rendering UI.
2. **Peningkatan Kinerja**: `const` memungkinkan Flutter untuk mengetahui objek yang tidak akan berubah, sehingga tidak perlu di-render ulang setiap kali aplikasi di-rebuild.
3. **Menghindari Pembuatan Ulang Objek**: Menggunakan `const` pada objek yang tidak berubah mencegah objek tersebut dibuat ulang saat build widget, yang akan mempercepat waktu eksekusi.

#### Kapan Sebaiknya Menggunakan `const`
- Saat membuat widget atau elemen UI yang tidak akan berubah selama siklus hidup aplikasi.
- Pada nilai statis atau string yang tidak perlu diubah, misalnya pada `Text` yang bersifat tetap.
- Jika objek tidak menerima parameter yang bersifat dinamis atau variabel.

#### Kapan Sebaiknya Tidak Menggunakan `const`
- Jika widget atau nilai dapat berubah berdasarkan interaksi pengguna atau kondisi lainnya.
- Saat widget memerlukan data dinamis, seperti data dari API atau input pengguna, karena nilai `const` tidak bisa diubah setelah inisialisasi.

### Jelaskan dan bandingkan penggunaan `Column` dan `Row` pada Flutter. Berikan contoh implementasi dari masing-masing layout widget ini!

#### Penggunaan dan Perbedaan `Column` dan `Row`
- `Column`: Digunakan untuk menyusun widget secara vertikal (top-to-bottom). Biasanya digunakan ketika ingin membuat layout bertingkat ke bawah.
- `Row`: Digunakan untuk menyusun widget secara horizontal (left-to-right). Cocok untuk mengatur layout yang sejajar ke samping.

#### Contoh Implementasi `Column`
```dart
Column(
  children: <Widget>[
    Text('Title'),
    SizedBox(height: 10),
    Text('Subtitle'),
    ElevatedButton(
      onPressed: () {},
      child: Text('Press Me'),
    ),
  ],
)
```

#### Contoh Implementasi `Row`
```dart
Row(
  mainAxisAlignment: MainAxisAlignment.spaceBetween,
  children: <Widget>[
    Icon(Icons.home),
    Text('Home'),
    Icon(Icons.settings),
  ],
)
```


### Sebutkan apa saja elemen input yang kamu gunakan pada halaman form yang kamu buat pada tugas kali ini. Apakah terdapat elemen input Flutter lain yang tidak kamu gunakan pada tugas ini? Jelaskan!

#### Elemen Input yang Digunakan
Pada file `productentry_form.dart`, elemen input yang digunakan adalah sebagai berikut:
- `TextFormField`: Untuk menerima input teks dari pengguna, misalnya nama produk atau deskripsi produk.
- `ElevatedButton`: Untuk tindakan, seperti submit atau menyimpan data.

#### Elemen Input Lain yang Tidak Digunakan
Beberapa elemen input Flutter lain yang tidak digunakan dalam form ini antara lain:
- `Checkbox`: Untuk pilihan ganda yang bisa diaktifkan atau dinonaktifkan.
- `Radio`: Untuk memilih satu opsi dari beberapa pilihan.
- `Slider`: Untuk memilih nilai dalam rentang tertentu.
- `Switch`: Untuk mengaktifkan atau menonaktifkan fitur tertentu.


### Bagaimana cara kamu mengatur tema (theme) dalam aplikasi Flutter agar aplikasi yang dibuat konsisten? Apakah kamu mengimplementasikan tema pada aplikasi yang kamu buat?

Di Flutter, tema dapat diatur menggunakan `ThemeData` di dalam properti `theme` dari `MaterialApp`. Dengan mengatur tema, gaya visual aplikasi, seperti warna utama, warna teks, dan tampilan elemen UI lainnya dapat diterapkan secara konsisten di seluruh aplikasi.

Untuk mengimplementasikan tema dalam aplikasi, kita bisa mendefinisikan `ThemeData` di level aplikasi:
```dart
MaterialApp(
  theme: ThemeData(
    primaryColor: Colors.blue,
    accentColor: Colors.amber,
    textTheme: TextTheme(
      headline1: TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
      bodyText1: TextStyle(fontSize: 14),
    ),
  ),
  home: HomeScreen(),
);
```


### Bagaimana cara kamu menangani navigasi dalam aplikasi dengan banyak halaman pada Flutter?

Navigasi dalam aplikasi Flutter dapat diatur dengan menggunakan `Navigator` dan `Routes`. Dengan navigator, kita bisa mendorong halaman baru ke dalam stack atau kembali ke halaman sebelumnya.

#### Implementasi Navigasi
Misalnya, dalam aplikasi dengan banyak halaman, kita bisa menggunakan kode berikut:
```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => SecondScreen()),
);
```

Untuk navigasi dengan `Drawer`, seperti dalam `left_drawer.dart`, kita dapat menambahkan item drawer yang memanggil halaman lain:
```dart
ListTile(
  title: Text('Home'),
  onTap: () {
    Navigator.pushNamed(context, '/home');
  },
),
```
