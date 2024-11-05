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

