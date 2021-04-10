---
title: PostgreSQL dan RStudio
date: '2020-04-16'
categories: [belajar, tutorial]
tags: [basisdata, postgresql, rstats]
---
{{< toc >}}

Saya sedang belajar mengelola data dalam sebuah basisdata. Sebab ketertarikan saya dengan bidang geospasial, saya coba untuk mempelajari DBMS terkenal untuk ini, yaitu PostgreSQL dengan ekstensi PostGIS.

Singkat cerita, saya sudah melakukan instalasi dan pengaturan basis data postgres + postgis di komputer saya. Selanjutnya saya ingin coba membuat koneksi untuk akses basisdata melalui RStudio. Saya merasa agak sedikit sombong karena sebelumnya sudah sukses dengan koneksi PostgreSQL lewat QGIS.

Ada [dua cara](https://db.rstudio.com/databases/postgresql/) membuat koneksi dari R untuk mengakses basis data:

- menggunakan paket `odbc` dengan `DBI`
- menggunakan paket `RPostgres`

Untuk saat ini saya menggunakan cara yang pertama. Langkah yang saya lakukan adalah:

### 1. Instal odbc drivers di komputer linux

Memasang odbc di Ubuntu dengan mengetikkan perintah berikut:

```bash
$ sudo apt update 
$ sudo apt install unixodbc unixodbc-dev odbc-postgresql
```

Setelah itu ...

### 2. Periksa hasil instalasi kita

Beberapa berkas yang perlu kita tahu dan butuhkan untuk menunjang pengaturan dan kerja paket `odbc` di R diantaranya berkas `odbcinst.ini` dan `odbc.ini`. Di mana mereka?

Kita bisa gunakan perintah berikut di terminal:

```bash
$ odbcinst -j
```

{{< figure src="https://telegra.ph/file/74d5055f0bc6505dec8e1.png" title="Gambar 1" caption="Keluaran perintah `odbcinst_j`" alt="terminal command output" >}}

Atau dengan cara lain, misalnya:

```bash
$ locate odbcinst.ini
$ locate odbc.ini
```

{{< figure src="https://telegra.ph/file/ab7612fe9f5b20325647e.png" title="Gambar 2" caption="Lokasi berkas konfigurasi odbc" alt="terminal command output" >}}

Akan ditampilkan tempat berkas-berkas itu tersimpan.

Kemudian coba kita cek apa isi dari berkas `odbcinst.ini`. Berikut isinya:

{{< figure src="https://telegra.ph/file/a57cc39e019779844a954.png" title="Gambar 3" caption="Print odbcinst.ini" alt="terminal command output" >}}

Sedangkan untuk berkas `.odbc.ini`, sepengalaman saya saat _fresh-install_ tidak ada isinya alias masih kosong. Berikutnya kita perlu isi itu.

### 3. Konfigurasi / sunting berkas odbc.ini

Berkas ini ada di dua tempat, seperti sudah kita periksa sebelumnya.

`/etc/odbc.ini` menyimpan pengaturan yang bisa digunakan secara global. Artinya bisa diakses oleh semua user di komputer terinstal, tetapi untuk pengaturannya kita membutuhkan akses root.

Sedangkan `~/.odbc.ini` hanya untuk user tertentu (sesuai lokasi home punya user mana). Kita tidak perlu root untuk ini. Berkasnya disembunyikan di direktori home.

Sunting berkas `.odbc.ini` milik user menggunakan text editor `nano` dengan perintah di terminal:

```bash
$ nano ~/.odbc.ini
```

Isikan detail seperti berikut:

```
[PostgreSQL]
Driver              = PostgreSQL Driver
Database            = namaDbKamu
Servername          = localhost
UserName            = usernamekamu
Password            = passwordSayaKamuGabolehTau
Port                = 5432
```

{{< figure src="https://telegra.ph/file/6dcbc3daf6344722708d3.png" title="Gambar 4" caption="Isi konfigurasi" alt="terminal text nano" >}}

Ganti nilai pada bagian `Database` dan `UserName`, juga pada bagian `Password`, sesuai dengan pengaturan basis data PostgreSQL milik teman-teman.

### 4. Menginstal paket odbc dan DBI di R

```r
install.packages("odbc")
install.packages("DBI")
```

Kemudian restart R session.

Koneksi sudah bisa digunakan...

{{< youtube z5tZ1C9SVyo >}}

Sekian.

-----

**Referensi:** https://db.rstudio.com/best-practices/drivers/#linux-debian-ubuntu
