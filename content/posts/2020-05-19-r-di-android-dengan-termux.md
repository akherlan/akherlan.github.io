---
title: "R di Android dengan Termux"
date: '2020-05-19'
categories: [tutorial]
tags: [android, rstats, termux]
---
{{< toc >}}

Apakah mungkin menjalankan R di ponsel pintar Android? Bisa.

Kita bisa menginstal dan menjalankan beberapa aplikasi yang tersedia di linux melalui termux. Salah satunya bahasa R.

Termux merupakan terminal emulator di Android. Berjalan tanpa harus dalam mode root. Tersedia di [PlayStore](https://play.google.com/store/apps/details?id=com.termux) dan juga [F-Droid](https://f-droid.org/repository/browse/?fdid=com.termux).

Karena saya kadang-kadang pakai R dan sedang belajar juga, jadi saya ingin instal R di Android.

## Paket manajemen termux

Tidak semua paket di simpan dalam satu repositori termux, melainkan dibagi menjadi repo default (lebih stabil), dan selainnya ada repo untuk aplikasi root, unstable (dalam pengembangan), dan X11 (antarmuka grafis).

Repositori termux yang menyimpan aplikasi R ada "di luar" atau mereka menyebutnya dengan "repositori komunitas", bernama `its-pointless`. Cara menambahkannya ke daftar agak berbeda dengan repo termux yang _official_.

Akhir tahun 2019 sampai awal-awal 2020 lalu akses ke repositori ini sempat hilang atau dicabut atau entahlah. Sedang dikembangkan mungkin? Namun sesaat sebelum saya menulis ini, repo itu sudah aktif kembali.

Oh ya, termux ini pakai basis Debian/Ubuntu, jadi pakai manajemen paket APT dan DPKG. Tapi punya perintah bawaan sendiri, sih: `pkg <command>`. Bisa dilihat dengan `pkg help`. Gak tau deh, untuk hal itu [baca wiki](https://wiki.termux.com/wiki/Main_Page)-nya saja ya...

## Menambah repositori its-pointless

Pertama, kita perlu `curl` untuk unduh skrip bash yang sudah dibuatkan untuk kita. Jadi kita bisa menambah repo ini dengan mudah. Enak sekali jadi kita ini.

Periksa apakah `curl` sudah terinstal.

```bash
$ dpkg -l | grep curl
```

Kalau sudah didahului **ii** berarti sudah. Kalau belum, instal dengan cara berikut (kita tidak usah pakai mode root di termux):

```bash
$ pkg install curl
```

Kalau sudah punya, kita akan unduh skrip dan menjalankannya dengan perintah:

```bash
$ curl -LO https://its-pointless.github.io/setup-pointless-repo.sh
$ bash setup-pointless-repo.sh
$ rm setup-pointless-repo.sh
```

Repositori its-pointless selesai ditambahkan.

## Instal R di Android

Biasanya setelah menambahkan alamat repo baru, kita harus update daftar paketnya. Tapi tadi sudah dilakukan ketika menjalankan skrip. Jadi, daftar paket sudah diperbarui. Berikutnya tinggal instal R.

```bash
$ pkg install r-base
```

Tunggu sampai selesai. Kemudian tes, apakah sudah berhasil.

```bash
$ R
```

Kita juga bisa menginstal pustaka `tidyverse` di Android. Tapi saya belum tes untuk yang itu. Karena sayang ruang penyimpanannya. Bahkan mungkin di ponsel saya tidak cukup, karena termux menggunakan ruang penyimpanan internal untuk aplikasi.

Selain `r-base`, its-pointless juga menyediakan `gcc-7`, `gfortran`, `octave`, `rustc`, `scipy`, dan beberapa _games_!

Sampai di sini, selamat menggunakan R di Android.

## Video demo

Bisa saksikan di laman [Youtube Channel](https://youtu.be/kDrc8-2K2DI "youtube") saya.

## Tips

Izinkan termux mengakses penyimpanan: 

```bash
$ termux-setup-storage
```

[lebih lanjut...](https://wiki.termux.com/wiki/Termux-setup-storage)

Tampilkan tombol-tombol keyboard yang biasanya ada di komputer, tapi di ponsel tidak ada:

```bash
$ pkg install nano
$ nano ~/.termux/termux.properties
```

Copas teks berikut:

```
extra-keys = [ \
 ['ESC','|','/','HOME','UP','END','PGUP','DEL'], \
 ['TAB','CTRL','ALT','LEFT','DOWN','RIGHT','PGDN','BKSP'] \
]
```

Kemudian `Ctrl + S` dan `Ctrl + X` lalu restart sesi termux-nya.

[lebih lanjut...](https://wiki.termux.com/wiki/Touch_Keyboard)

**Referensi:** [Manajemen Paket Termux](https://wiki.termux.com/wiki/Package_Management)
