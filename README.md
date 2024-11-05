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