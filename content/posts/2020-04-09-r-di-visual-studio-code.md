---
title: "R Di Visual Studio Code"
date: '2020-04-09'
categories: [tutorial]
tags: [rstats, tool]
---
{{< toc >}}

OK! Saya akui saya terlena dengan perbincangan tentang menggunakan editor VS Code dari Microsoft untuk bekerja dengan R, [di twitter](https://twitter.com/jozefhajnala/status/1204496900461912068).

Berangkat dari tweet tersebut, saya melakukan beberapa langkah instalasi di mesin linux saya untuk bisa ikutan dalam keseruan ini. Berikut...

## 1. Siapkan VS Code

Saya [unduh](https://code.visualstudio.com/Download) dan instal VS Code dulu tentunya. Instalasi di linux Ubuntu semudah mengerjakan skripsi: _copas ini saja!_ (ups)

Ganti bagian `~/Downloads/code_x.xx.x-xxxxxx_amd64.deb` dengan direktori tempat teman-teman menyimpan berkas `deb`-nya VS Code.

```bash
$ sudo dpkg -i ~/Downloads/code_x.xx.x-xxxxxx_amd64.deb
```

Lalu, pergi ke menu, cari Visual Studio Code. Atau di terminal ketikkan `code`, enter.

## 2. Instal Ekstensi R LSP Client

Cara instal:

- pergi ke bagian extension (nomor 1), 
- ketik "r lsp" di pencarian, 
- pilih **R LSP Client** yang dari REditorSupport (nomor 2), 
- lalu klik "Install".

{{< figure src="https://telegra.ph/file/e95a671d8754cf7a1049a.png" caption="Instal ekstensi R LSP" alt="R in visual studio code" >}}

Ketika menginstal ternyata ada pesan error yang muncul:

{{< figure src="https://telegra.ph/file/8cf9f5a5ebaaf7bbdd9b2.png" caption="Galat terjadi karena harus terinstal languageserver di R" alt="R in visual studio code" >}}

Ini terjadi karena saya belum instal library `languageserver` untuk R. Itulah mengapa saya juga harus melakukan...

## 3. Instal library languageserver

Instalasinya bisa dari terminal linux, console R di terminal, console R di RStudio, atau terminal yang masuk ke console R dari VS Code.

Pilihan terakhir adalah yang saya pilih, biar gak kemana-mana lagi.

Di bagian bawah, ada TERMINAL, ketik R (tentu saja R sudah terinstal), kemudian ketikkan:

```r
install.packages("languageserver")
```

Tunggu sampai selesai instal, ada beberapa dependensinya juga yang diperlukan. Cas-cis-cus...

{{< figure src="https://telegra.ph/file/fce2613a545270b736a7e.png" caption="Instal paket languageserver" alt="R in visual studio code" >}}

Terakhir, tutup dan buka kembali (restart) VS Code, biar afdhol.

## 4. Taraaa....

_Autocompletion_ di VS Code untuk bahasa R.

{{< figure src="https://telegra.ph/file/1027c969895e737d1ec6d.gif" caption="Berhasil. Autocompletion bahasa R di VS Code" alt="R autocompletion in visual studio code" >}}

Sekian dulu.
