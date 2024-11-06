# toko_jam_bobert


1. **Jelaskan apa yang dimaksud dengan stateless widget dan stateful widget, dan jelaskan perbedaan dari keduanya.**<br>
    Stateless widget adalah widget statis dimana setiap konfigurasi di dalamnya sudah di initialize dari awal, 
    sehingga setelah widget dirender maka tidak akan berubah selama aplikasinya berjalan. Stateful widget adalah widget 
    yang dinamis dan interaktif, sehingga widget ini bisa diperbaharui kapanpun berdasarkan user actions atau ketika terjadi 
    perubahan data. Contoh kegunaan dari stateless widget yaitu untuk menampilkan data statis seperti text biasa. Lalu, contoh 
    kegunaan untuk stateful widget yaitu untuk terpakai untuk setiap tombol yang bisa diklik, untuk form input, atau untuk sebuah animation. 
    Jadi stateless widget terpakai jika UInya bergantung pada external input dan data tidak berubah, lalu stateful widget terpakai
     ketika kita perlu melacak data yang dapat berubah seperti counter begitu.
    Contoh stateless yaitu:
    ```python
    class MyApp extends StatelessWidget {
        const MyApp({super.key});

        // This widget is the root of your application.
        @override
        Widget build(BuildContext context) {
            return MaterialApp(
                title: 'Flutter Demo',
                theme: ThemeData(
                    colorScheme: ColorScheme.fromSwatch(
                    primarySwatch: Colors.deepPurple,
                    ).copyWith(secondary: Colors.deepPurple[400]),
                    useMaterial3: true,
                    ),
                    home: MyHomePage(),
                );
            }
        }
    ```

2. **Sebutkan widget apa saja yang kamu gunakan pada proyek ini dan jelaskan fungsinya.**<br>
    Widget-widget yang saya pakai pada proyek ini yaitu:<br>
    MaterialApp, Scaffold, AppBar, Column, Row, GridView.count, Card, Container, SizedBox, Icon, InkWell, SnackBar, Text, dan Material.
    <br><br>
    Berikut penjelasan singkat masing-masing:
    - Scaffold: berfungsi sebagai struktur dasar untuk layout halaman, termasuk AppBar, body, dan lainnya.
    - AppBar: untuk membantu navigasi pengguna di dalam aplikasi, mungkin bisa dibilang mirip navBar.
    - Text: Digunakan untuk menampilkan judul, informasi, dan teks apapun lainnya.
    - Column: Untuk penyusunan secara vertikal.
    - Row: untuk penyusunan secara horizontal.
    - SizedBox: Memberikan jarak vertikal atau horizontal antar elemen di dalam layout.
    - InfoCard: Widget custom yang menampilkan informasi dalam bentuk kartu dengan title dan content.
    - GridView.count: Widget untuk menampilkan grid dengan kolom tertentu, di mana item dalam grid bisa disesuaikan.
    - Card: Widget yang digunakan untuk membuat kartu dengan shadow dan isi di dalamnya.
    - Container: Widget dasar yang digunakan untuk menyusun widget lainnya dan memberi padding, margin, atau pengaturan ukuran.
    - Material: Widget untuk mengimplementasikan desain material (misalnya, sprti background color).
    - MaterialApp: widget utama yang membungkus aplikasi dan mengonfigurasi tema, navigasi, routing, dan berbagai pengaturan aplikasi lainnya.
    - InkWell: Widget yang menangani interaksi sentuhan, memberikan efek ripple saat ditekan.
    - Icon: Menampilkan ikon, digunakan untuk menampilkan gambar berbentuk ikon.
    - SnackBar: widget untuk menampilkan text singkat yang muncul di bawah screen abis ada interaction dgn user.

3. **Apa fungsi dari setState()? Jelaskan variabel apa saja yang dapat terdampak dengan fungsi tersebut.**<br>
    Fungsi setState() berfungsi untuk memberi tahu framework kalau ada perubahan yang terjadi pada state sebuah widget yang stateful, 
    perubahan ini perlu diperbaharui pada user interface. Ketika fungsi ini dipanggil, maka flutter akan menjalankan ulang build() dari 
    widgetnya sehingga ada UI yang sudah diperbaharui.

    Variabel yang akan terdampak dari pemanggilan fungsi setState() tentunya adalah semua variabel state lokal yang ada di dalam build().<br> 
    Variabel-variabel yang mempengaruhi UI juga akan ikut terdampak oleh setState(). Contoh variabel yang tidak terdampak adalah variabel-variabel
     yang ada di luar dari build(), variabel global atau static, dan variabel yang didefine sebagai const atau final.

4. **Jelaskan perbedaan antara const dengan final**<br>
    Dalam dart, keyword const merupakan compile-time constant, sedangkan keyword final adalah run-time constant. Compile-time constant 
    artinya nilai harus sudah didefinisikan saat kompilasi, sedangkan kalau run-time constant artinya bisa bergantung pada nilai lain yang 
    detailnya mungkin hanya bisa diketahui saat program berjalan (saat runtime baru bisa dihitung). Dengan begitu, final akan cocok digunakan 
    untuk objek yang valuenya didapatkan ketika runtime dan const cocok digunakan untuk objek yang statis karena const harus diinisialisasi di 
    compile-time. Contoh pemakaian const yaitu `const a = 1`, lalu contoh pemakaian final yaitu `final DateTime tanggal = DateTime.now()`.

5. **Jelaskan bagaimana cara kamu mengimplementasikan checklist-checklist di atas**
    1. Pertama-tama, buat terlebih dahulu project flutter bernama toko-jam-bobert dengan melakukan `flutter create toko-jam-bobert`.
    2. Ciptakan menu.dart, pindahkan class MyhomePage dan MyHomePageState ke menu.dart, dan ubah setiap stateful jadi stateless widget.
    3. Membuat widget ItemHomePage dan juga ItemCard. Pada ItemHomePage, definisikan:<br>
    ```dart
        final String npm = '2306214990'; // NPM
        final String name = 'Henry Aditya Kosasi'; // Nama
        final String className = 'PBP F'; // Kelas
    ```
    Lalu pada InfoCard definisikan:
    ```dart
        final String title;  // Judul kartu.
        final String content;  // Isi kartu.

        const InfoCard({super.key, required this.title, required this.content});
    ```
    4. Selanjutnya, buat button card sederhana yang akan memakai widget icon untuk gambarnya. Pada MyHomePage, tambahkan tombol:
    ```dart
        final List<ItemHomepage> items = [
            ItemHomepage("Lihat Daftar Produk", Icons.mood, Colors.green),
            ItemHomepage("Tambah Produk", Icons.add, Colors.lightGreen),
            ItemHomepage("Logout", Icons.logout, const Color.fromARGB(255, 25, 255, 17)),
        ];
    ```
    Lalu pada ItemHomepage:
    ```dart
        final String name;
        final IconData icon;
        final Color color; // Tambahin color agar warnanya beda beda
        ItemHomepage(this.name, this.icon, this.color);
    ```
    5. Buat ItemCard yang ketika dipencet akan menampilkan snackbar.
    ```dart
    class ItemCard extends StatelessWidget {
        // Menampilkan kartu dengan ikon dan nama.

        final ItemHomepage item; 
        
        const ItemCard(this.item, {super.key}); 

        @override
        Widget build(BuildContext context) {
            return Material(
            // Menentukan warna latar belakang dari tema aplikasi.
            color: Theme.of(context).colorScheme.secondary,
            // Membuat sudut kartu melengkung.
            borderRadius: BorderRadius.circular(12),
            
            child: InkWell(
                // Aksi ketika kartu ditekan.
                onTap: () {
                // Menampilkan pesan SnackBar saat kartu ditekan.
                ScaffoldMessenger.of(context)
                    ..hideCurrentSnackBar()
                    ..showSnackBar(
                    SnackBar(content: Text("Kamu telah menekan tombol ${item.name}!"))
                    );
                },
            ...
    ```
