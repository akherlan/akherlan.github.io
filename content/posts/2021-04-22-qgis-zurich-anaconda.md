---
title: "QGIS Zürich versi Anaconda"
date: 2021-04-22T15:54:19+07:00
tags: ["GIS"]
---

Sore ini saya iseng-iseng cek laman QGIS di channel [conda-forge](https://anaconda.org/conda-forge/qgis). Lama sudah tidak cek update aplikasi ini karena sekarang juga malah sudah jarang pakai. Saat tulisan ini diketik, bertepatan dengan 3 hari (2 hari 21 jam) QGIS versi 3.18.2 Zürich (non-LTR) rilis versi conda. Masih sangat segar. Tapi sudah ada total unduh sebanyak 341.369 kali waktu saya mulai ikutan unduh juga.

Karena saya sudah punya environment conda (Miniconda) dengan nama `qgis3` yang khusus saya peruntukkan bagi QGIS agar berjalan lancar tanpa gangguan, maka saya tinggal mutakhirkan saja yang lama ke versi terbaru 3.18.

```bash
$ conda activate qgis3
$ conda update -c conda-forge qgis
```

Muncul detail semua dependensi yang akan terunduh, yang baru akan diinstal, yang akan dihapus, dst. Lalu saya tekan `y` dan `Enter`. Tanda setuju melakukan update.

Mengapa saya menggunakan QGIS keluaran Anaconda dan tidak menggunakan versi official dengan pasang repository QGIS resmi di komputer saya? Jawabannya, karena dependensi QGIS yang saya instal pernah konflik dengan dependensi [#Rspatial](https://twitter.com/hashtag/rspatial). 

Malaaaaas sekali kalau sudah kacau begitu. Lebih baik saya pisahkan lingkungan kerjanya saja. Mana QGIS ini banyak versinya pula, ada yang nightly lah, ada yang stable, ada yang cuma versi LTR, dan lain-lain. Dan versi dependensinya tentu saja berbeda-beda juga. Nanti beda lagi dengan yang dipakai di R.

Sebetulnya saya ingin pasang dan perbarui setiap ada versi LTR rilis saja. Tapi sistem yang terisolasi lebih penting sekarang ketimbang masalah up to date. Sekarang, tinggal jalankan aplikasi QGIS lewat terminal.

```bash
$ qgis # dalam environment conda yang terinstal QGIS
```

Tampilan splash QGIS 3.18 di destop saya:

{{< figure src="https://telegra.ph/file/b49f3914333fffce6fc7b.png" caption="QGIS 3.18 Zürich di Xubuntu" alt="Running QGIS 3.18 Zürich on Ubuntu" >}}

Sekian curhatan saya.
