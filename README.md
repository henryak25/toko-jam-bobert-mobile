# toko_jam_bobert

**<h1>Tugas 9</h1>**
**<h1>1. Jelaskan mengapa kita perlu membuat model untuk melakukan pengambilan ataupun pengiriman data JSON? Apakah akan terjadi error jika kita tidak membuat model terlebih dahulu?</h1>**
Membuat model penting untuk mengatur data JSON karena model membantu memetakan struktur data secara terorganisir dan konsisten. Tanpa model, data yang diambil dari API hanya berupa map atau struktur mentah yang sulit digunakan, terutama jika data tersebut memiliki banyak atribut atau relasi. Model memungkinkan kita mengubah data JSON menjadi objek yang mudah diakses, dengan tipe data yang jelas untuk setiap atribut. Hal ini juga membantu saat kita perlu memvalidasi atau memanipulasi data, karena model menyediakan metode dan fungsi yang mempermudah pengelolaan data tersebut.
Jika tidak membuat model, kemungkinan besar akan muncul error, terutama saat ada perubahan struktur data di backend. Flutter tidak akan langsung mengenali atribut atau tipe data yang diharapkan, sehingga bisa terjadi kesalahan runtime saat mengakses data yang tidak sesuai dengan ekspektasi. Selain itu, tanpa model, kode akan lebih sulit dibaca dan rentan terhadap bug karena pengolahan data dilakukan secara manual. 

**<h1>2. Jelaskan fungsi dari library http yang sudah kamu implementasikan pada tugas ini</h1>**
Library http pada Flutter berfungsi sebagai alat untuk melakukan komunikasi antara aplikasi Flutter dengan server backend, dalam hal ini Django. Library ini menyediakan fungsi-fungsi untuk mengirimkan permintaan HTTP, seperti GET, POST, PUT, dan DELETE, serta menerima respons dari server. Dengan menggunakan http, aplikasi Flutter dapat mengambil data JSON dari Django (fetch data), mengirimkan data yang diisi user ke server (submit data), atau memperbarui dan menghapus data pada backend sesuai kebutuhan.
Pada tugas 9 ini, library http digunakan untuk menghubungkan aplikasi Flutter dengan API Django. Misalnya, ketika user mau melihat daftar produk, nanti app akan mengirimkan permintaan GET ke endpoint Django yang menyediakan data produk dalam format JSON. Respons dari server tersebut kemudian diolah menjadi model Dart agar mudah digunakan di Flutter. Dengan begitu, library http berfungsi sebagai jembatan utama yang memungkinkan integrasi antara backend Django dan frontend Flutter, sehingga data dapat ditampilkan atau dimanipulasi dalam aplikasi secara real-time.

**<h1>3. Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.</h1>**
CookieRequest berfungsi untuk menyimpan cookie yang diterima dari server setelah pengguna berhasil login, sehingga setiap permintaan HTTP berikutnya yang membutuhkan authentication dapat menyertakan cookie tersebut. hal tersebut penting untuk menjaga sesi pengguna tetap aktif tanpa perlu mengirim ulang kredensial pada setiap permintaan.

Instance CookieRequest perlu dibagikan ke semua komponen dalam aplikasi Flutter agar semua bagian aplikasi yang membutuhkan akses ke data yang dilindungi atau memerlukan authentication dapat menggunakan cookie yang sama. Dengan cara ini, sesi pengguna dapat dikelola dengan konsisten di seluruh aplikasi, seperti untuk fitur login, atau akses ke halaman yang butuh authentication. Penggunaan shared instance juga menghindari duplikasi atau konflik dalam pengelolaan cookie, sehingga memastikan komunikasi antara aplikasi Flutter dan server Django berjalan dengan lancar dan aman.

**<h1>4. Jelaskan mekanisme pengiriman data mulai dari input hingga dapat ditampilkan pada Flutter.</h1>**
Mekanisme pengiriman data dari input di web Django hingga dapat ditampilkan di aplikasi Flutter melalui metode GET melibatkan beberapa langkah berikut:

    1. Input Data di Web Django
    Data dimasukkan oleh user di website Django. Setelah form diisi dan disubmit, Django memproses input tersebut dan menyimpannya di database. Proses ini dilakukan oleh views Django yang berinteraksi dengan model untuk menyimpan data.<br>

    2. Penyediaan API Endpoint di Django
    Django menyediakan endpoint REST API yang memungkinkan aplikasi eksternal, seperti Flutter, untuk mengakses data dari database.  Saat diakses dengan metode GET, endpoint akan mengembalikan data dalam format JSON.<br>

    3. Pengambilan Data di Flutter
    Di sisi Flutter, library seperti http digunakan untuk mengirim permintaan GET ke endpoint Django tersebut. Permintaan ini dilakukan melalui URL yang mengarah ke endpoint API Django.<br>

    4. Deserialisasi Data JSON
    Data yang diterima dari Django dalam format JSON perlu diubah menjadi objek yang dapat digunakan di Flutter. Ini dilakukan dengan membuat model data di Flutter yang sesuai dengan struktur JSON yang dikirim Django. Model ini biasanya didefinisikan menggunakan kelas dan fungsi untuk parsing JSON.<br>

    5. Menampilkan Data di Flutter
    Setelah data diubah menjadi objek Dart melalui proses deserialisasi, data tersebut kemudian ditampilkan di aplikasi Flutter.<br>


**<h1>5. Jelaskan mekanisme autentikasi dari login, register, hingga logout. Mulai dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.</h1>**
bikin view login di authentication views urlsnya juga set trus register jg sama. di flutter bikin login.dart sama register.dart, cocokin aja isinya nanti. jangan lupa authentication masukkin di settings.py pada django. lalu logout juga sama bikin aja viewsnya sm set urls juga. kalo register kita perlu send ke si django pnya server. yah intinya gitu sih

**<h1>6. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step! (bukan hanya sekadar mengikuti tutorial)</h1>**
bikin view register login logout ya pokoknya gitu. page .dart buatkan, lalu sebenarnya mirip sama tutorial tapi perlu menyesuaikan model, untuk bagian login logout register mah tetap sama seperti tutorial, yang berbeda itu pas mau insert data dari flutter harus send juga ke website, dan itu perlu csrf exempt. Kita perlu kasih cookies juga buat usernya tambahkan biar kita gak usah login tiap kali pergantian page dll. Lalu jangan lupa tambahin logic buat onclick add product view product dan juga logout. Jika kita pencet view product nanti akan redirect ke list_productentry.dart, lalu dalam list itu bisa lihat produk saya implementasi dengan cara masukkinnya box dulu beserta nama produknya, nanti kalau dipencet akan redirect detail_product.dart. di detail_product.dart baru kita tampilin data-datanya si produk. perlu juga untuk mengubah modelsnya tapi gak ubah banyak juga, untungnya cuman perlu ganti mood jadi name lalu feelings jadi description dan juga quantity jadi price. Singkatnya seperti itu.

berikut file detail_product.dart:
```dart
    import 'package:flutter/material.dart';
    import 'package:toko_jam_bobert/models/mood_entry.dart';
    import 'package:toko_jam_bobert/widgets/left_drawer.dart';

    class DetailProductPage extends StatelessWidget {
    final Product product;

    const DetailProductPage({Key? key, required this.product}) : super(key: key);

    @override
    Widget build(BuildContext context) {
        return Scaffold(
        appBar: AppBar(
            title: Text(product.fields.name),
        ),
        drawer: const LeftDrawer(),
        body: Padding(
            padding: const EdgeInsets.all(16.0),
            child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
                Text(
                product.fields.name,
                style: const TextStyle(
                    fontSize: 24.0,
                    fontWeight: FontWeight.bold,
                ),
                ),
                const SizedBox(height: 16),
                Text(
                "Price: ${product.fields.price}",
                style: const TextStyle(fontSize: 18.0),
                ),
                const SizedBox(height: 16),
                Text(
                "Time: ${product.fields.time}",
                style: const TextStyle(fontSize: 18.0),
                ),
                const SizedBox(height: 16),
                Text(
                product.fields.description,
                style: const TextStyle(fontSize: 16.0),
                ),
            ],
            ),
        ),
        );
    }
    }

```
**<h1>Tugas 8</h1>**

**<h1>Apa kegunaan const di Flutter? Jelaskan apa keuntungan ketika menggunakan const pada kode Flutter. Kapan sebaiknya kita menggunakan const, dan kapan sebaiknya tidak digunakan?</h1>**
Dalam flutter, const digunakan untuk mendefinisikan objek atau widget yang bersifat konstan (immutable) dan tidak akan berubah selama aplikasi 
berjalan. const memungkinkan Dart untuk mengalokasikan objek tersebut pada saat kompilasi (compile-time), bukan saat aplikasi berjalan (runtime). 
Keuntungan pakai const:
- Penghematan memori: Dengan menggunakan const, objek dibuat hanya sekali di memori, dan instance yang sama dapat digunakan kembali 
setiap kali dibutuhkan.
- Performa rendering yang lebih baik: Karena const widget tidak akan berubah, Flutter tidak perlu me-render ulang widget tersebut, 
yang membantu menjaga aplikasi tetap responsif.
- Pendeteksian kesalahan lebih awal: Karena nilai const harus tetap, kesalahan akan terdeteksi pada saat kompilasi 
jika ada kode yang mencoba mengubah nilai const. 
Ini membantu menangkap error lebih cepat.

Sebaiknya kita memakai const ketika ada widget yang statis dan pada nilai konstan seperti int atau string begitu, dan Jika ada widget 
yang di dalamnya hanya berisi widget konstan lainnya, maka gunakan const pada widget induk untuk memanfaatkan compile-time constant sepenuhnya.
Lalu kita sebaiknya tidak memakai const untuk widget yang dinamis dan widget yang menerima input user seperti TextField atau Slider. 
Hal ini karena const itu bersifat konstan (immutable) dan tidak akan berubah selama aplikasi berjalan.


**<h1>Jelaskan dan bandingkan penggunaan Column dan Row pada Flutter. Berikan contoh implementasi dari masing-masing layout widget ini!</h1>**
Sesuai namanya, Column akan terpakai untuk layout secara kolom atau vertikal, sedangkan Row akan terpakai untuk layout secara baris atau horizontal.

Contoh pemakaian Row
```dart
Row(
    mainAxisAlignment: MainAxisAlignment.spaceEvenly,
    children: [
    InfoCard(title: 'NPM', content: npm),
    InfoCard(title: 'Name', content: name),
    InfoCard(title: 'Class', content: className),
    ],
),
```
Contoh pemakaian Column
```dart
child: Column(
          children: [
            Text(
              title,
              style: const TextStyle(fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 8.0),
            Text(content),
          ],
        ),
```

**<h1>Sebutkan apa saja elemen input yang kamu gunakan pada halaman form yang kamu buat pada tugas kali ini. Apakah terdapat elemen input Flutter lain yang tidak kamu gunakan pada tugas ini? Jelaskan!</h1>**
Elemen input yang saya gunakan pada halaman form saya adalah TextFormField. TextFormField ini terpakai untuk input Name, Description, dan Amount.
Beberapa elemen input lain yang tidak digunakan dalam form ini, seperti:
- Checkbox - Untuk input boolean (true/false)
- Radio - Untuk memilih satu opsi dari beberapa pilihan
- DropdownButton - Untuk memilih satu item dari daftar dropdown

**<h1>Bagaimana cara kamu mengatur tema (theme) dalam aplikasi Flutter agar aplikasi yang dibuat konsisten? Apakah kamu mengimplementasikan tema pada aplikasi yang kamu buat?</h1>**
Dengan mengimplementasikan ThemeData pada MaterialApp seperti ThemeData.dark(), sehingga kita pakai itu di widget tertentu agar bisa konsisten dengan tema utama. <br>
ini di main.dart
```dart
theme: ThemeData(
        colorScheme: ColorScheme.fromSwatch(
        primarySwatch: Colors.deepPurple,
        ).copyWith(secondary: Colors.deepPurple[400]),
        useMaterial3: true,
      ),
```
ini contoh pemakaiannya:
```dart
backgroundColor: Theme.of(context).colorScheme.secondary,
color: Theme.of(context).colorScheme.secondary,
backgroundColor: WidgetStateProperty.all(
    Theme.of(context).colorScheme.primary),
)
```

**<h1>Bagaimana cara kamu menangani navigasi dalam aplikasi dengan banyak halaman pada Flutter?</h1>**
Yaitu dengan cara menggunakan widget Navigator yang menampilkan halaman-halaman sebagai tumpukan (stack). Untuk membuka halaman baru atau berpindah antar halaman, kita dapat memanfaatkan Navigator melalui BuildContext. Beberapa fungsi utama yang sering digunakan dalam Navigator adalah:
- push() – Menambahkan halaman baru ke atas stack, sehingga halaman baru tersebut tampil di layar.
- pop() – Menghapus halaman yang sedang aktif dari stack, sehingga kembali ke halaman sebelumnya.
- pushReplacement() – Mengganti halaman saat ini dengan halaman baru tanpa menambahkannya ke dalam stack, cocok untuk skenario seperti login atau onboarding.<br>
Berikut contoh pemakaian dari push(), pop(), dan juga pushReplacement():
```dart
// push()
if (item.name == "Tambah Mood") {
        Navigator.push(context,
            MaterialPageRoute(builder: (context) => const MoodEntryFormPage()));
    }
// pop()
onPressed: () {
        Navigator.pop(context);
    },
// pushReplacement()
onTap: () {
        Navigator.pushReplacement(
        context,
        MaterialPageRoute(
            builder: (context) => MyHomePage(),
        ));
    },
```
Sebagai info tambahan, terdapat juga beberapa method lain yang dapat memudahkan routing dalam pengembangan aplikasi, seperti popUntil(), canPop(), dan maybePop().
**<h1>Tugas 7</h1>**

1. **Jelaskan apa yang dimaksud dengan stateless widget dan stateful widget, dan jelaskan perbedaan dari keduanya.**<br>
    Stateless widget adalah widget statis dimana setiap konfigurasi di dalamnya sudah di initialize dari awal, 
    sehingga setelah widget dirender maka tidak akan berubah selama aplikasinya berjalan. Stateful widget adalah widget 
    yang dinamis dan interaktif, sehingga widget ini bisa diperbaharui kapanpun berdasarkan user actions atau ketika terjadi 
    perubahan data. Contoh kegunaan dari stateless widget yaitu untuk menampilkan data statis seperti text biasa. Lalu, contoh 
    kegunaan untuk stateful widget yaitu untuk terpakai untuk setiap tombol yang bisa diklik, untuk form input, atau untuk sebuah animation. 
    Jadi stateless widget terpakai jika UInya bergantung pada external input dan data tidak berubah, lalu stateful widget terpakai
     ketika kita perlu melacak data yang dapat berubah seperti counter begitu.
    Contoh stateless yaitu:
    ```dart
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
