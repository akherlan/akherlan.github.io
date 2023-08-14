---
title: "Travel with Gojek"
date: 2021-08-28T01:12:29+07:00
lastmod: 2021-08-29T04:28:00+07:00
tags: [data, rstats, gojek]
---

Data yang saya gunakan merupakan hasil mengumpulkan invoice dari Gojek yang dikirimkan melalui surel setiap kali selesai melakukan pemesanan jasa transportasi lewat aplikasi. Data diimpor dari Gmail ke Google Sheets melalui Google Apps Script, kemudian diekspor ke format csv untuk diolah menggunakan R. Referensi lebih lanjut tentang kode yang saya gunakan silakan mengunjungi [repositori gojek](https://github.com/akherlan/gojek) di Github saya.

### Waktu

![time with gojek](https://raw.githubusercontent.com/akherlan/gojek/main/figs/clock.png)

Saya tidak terlalu rutin menggunakan moda transporasi ini. Namun total {{< annotate underline "lama waktu perjalanan" >}} saya sudah hampir {{< annotate underline "dua harian" >}} terhitung sejak 2018 hingga saat tulisan ini ditulis.

Waktu perjalanan {{< annotate underline "paling sering" >}} adalah ketika {{< annotate underline "malam hari" >}} antara pukul sembilanan hingga pukul sepuluhan, juga saat {{< annotate underline "pagi menjelang siang" >}}.

### Jarak

![movement with gojek](https://raw.githubusercontent.com/akherlan/gojek/main/figs/distance_map.png)

Dengan Gojek saya sudah melaju seolah-olah mulai dari ujung Barat pulau Jawa hingga ke ujung Timurnya. Saya paling sering melakukan {{< annotate underline "perjalanan dengan jarak yang bisa dicapai dalam 5-10 menitan" >}}.

Ada saatnya beberapa kali saya menempuh perjalanan yang cukup jauh yaitu ketika terlambat mengejar jadwal kereta terakhir dari Sudirman menuju Depok, juga ketika pindah kosan dari Srengseng Jakarta Barat kembali ke Depok.

Namun ada beberapa data yang "aneh" dan tidak masuk akal karena durasi perjalanan hanya dalam 3-6 detik saja dalam jarak antara 3-5 kilometer.

### Kebutuhan

![effort with gojek](https://raw.githubusercontent.com/akherlan/gojek/main/figs/needs.png)

Perjalanan terbanyak ketika ng-Gojek adalah {{< annotate underline "dari stasiun (atau halte) untuk pulang," >}} disusul oleh perjalanan pulang selepas beraktivitas di luar selain kerja.

Ada hubungan yang erat antara kantor dengan aktivitas transit, dihubungkan dengan aktivitas ng-Gojek.

Jika saya harus menggunakan uang tunai kemungkinan karena saya kehabisan GoPay saat berada di luar rumah.

Pertanyaan berikutnya adalah kenapa ada perjalanan dari rumah ke rumah? Punya rumah lebih dari satu! Hahahaha... Saya pindah-pindah kost sebetulnya.

### Biaya

![expenses with gojek](https://raw.githubusercontent.com/akherlan/gojek/main/figs/cost.png)

Biaya dalam tampilan grafik ini {{< annotate underline "belum termasuk dengan penggunaan GoBills" >}} untuk BPJS, pulsa, dll. apalagi dengan GoFood. Belum. Jika saya harus menggunakan uang tunai saat bepergian kemungkinan karena saya kehabisan GoPay saat berada di luar rumah, bisa diperhatikan melalui grafik sebelumnya.

Setelah ini apalagi yang bisa dieksplorasi?

-----

*Proyek personal ini terinspirasi dari Mas [Rasyid Ridha](http://rasyidridha.com/datague/data-gojek/) yang pernah mengolah data Gojek miliknya pribadi.*
