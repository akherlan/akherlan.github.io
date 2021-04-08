---
title: "Personal Access Token Github"
date: '2020-04-16'
categories: [tutorial]
tags: [git, github, rstats]
---
{{< toc >}}

Personal access token (PAT) berguna untuk interaksi antara suatu program dengan akun Github milik kita melalui "pintu belakang yang disepakati".

Pada kasus ini, saya ingin agar saya bisa berinteraksi dengan kumpulan dataset saya yang tersimpan di repositori Github melalui RStudio (maupun konsol R melalui terminal).

Repositori ini tentu tidak boleh diotak-atik sembarangan oleh siapapun, dan hanya pemilik akun (atau komunitas/grup) yang berwenang menyuntingnya, maka dibutuhkan token. Pemilik token-lah yang memegang kendali.

Ada beberapa cara untuk membuat dan menyimpan Github PAT ke komputer linux (saya pakai Xubuntu). Seharusnya, di Windows tidak akan jauh berbeda.

## 1. Menggunakan paket usethis

Cara pertama ini adalah yang saya gunakan. Lebih mudah jika dilakukan lewat RStudio. Yang wajib disediakan adalah tentu saja paket `usethis`. Jika belum punya, bisa instal dulu dari konsol:

```r
install.packages("usethis")
```

Log in dulu ke akun Github di browser default, agar nanti ketika direct dari RStudio langsung terbuka halaman yang tinggal OK-OK saja. Gunakan perintah ini untuk menuju laman pembuatan token.

```r
usethis::browse_github_pat()
```

Kita akan diarahkan ke [laman pembuatan PAT](https://github.com/settings/tokens/new) dan otomatis terisi default yang dibutuhkan. Ini bisa di _custom_ dulu kalau kita perlukan. Kalau saya sementara biarkan yang sudah terpilih saja. Lalu tekan "Generate token" yang di paling bawah.

**INI PENTING!** Jangan lupa copas seluruh 40 karakter acak yang muncul.

Berikutnya kita kembali ke jendela RStudio lagi, lalu gunakan perintah berikut untuk menampilkan berkas `.Renviron` yang tersimpan di komputer:

```r
usethis::edit_r_environ()
```

{{< figure src="https://telegra.ph/file/2ff4dbf4ba62c842cf3e6.gif" caption="Membuka berkas .Renviron" alt="R environment" >}}

Akan terbuka berkas `.Renviron` yang berada di direktori home. Jika tidak punya, berarti `usethis` akan membuatkan berkas ini untukmu. Ketikkan teks berikut di editor skrip yang terbuka:

```r
GITHUB_PAT=xxxxxxxxxxxxxx
# ganti xxxxxxxxxxxxxx dengan token yang tadi di copas dari Github
```

{{< figure src="https://telegra.ph/file/51c0b4e6546f51392d9ff.gif" caption="Memasukkan token" alt="Personal Access Token Github" >}}

Tanpa tanda kutip ya...

Pastikan satu baris terakhir tersisa kosong (mereka bilang ini _new line_). Jangan lupa di simpan. Kalau nggak, percuma tadi capek-capek bikin.

Cek, apakah sudah ada?

```r
nchar(Sys.getenv("GITHUB_PAT"))
## [1] 40
```

Betul, ada 40 karakter. Berikutnya, kita sudah bisa menggunakan berbagai fungsi dari paket R macam-macam yang membutuhkan akses token Github.

Misalnya saya mau koneksikan RStudio dengan [repositori dataset](https://github.com/akherlan/dataset/) yang saya punya.

```r
library("pins")

board_register(
  board = "github", 
  name = "databoard", 
  repo = "akherlan/dataset"
)

gempa <- pin_get("gempa", "databoard")

head(gempa)
```

Keluaran:

```r
## # A tibble: 6 x 13
##   tanggal    waktu   lat   lon kdlm.KM mag.SR typemag  smaj    smin    az
##   <date>     <chr> <dbl> <dbl>   <dbl>  <dbl> <fct>   <dbl>   <dbl> <int>
## 1 2009-01-01 01:2…  3.73  127.      67    4.6 MLv     10317 1.80e+3   147
## 2 2009-01-01 03:4… -6.84  130.     103    5.2 mb      22841 2.78e+3    48
## 3 2009-01-01 05:2…  1.45  121.      10    5.1 MLv     10432 1.54e+0   121
## 4 2009-01-01 08:4…  1.52  122.      10    4.5 MLv      7557 1.04e+3   136
## 5 2009-01-01 08:5… -8.44  116.      91    3.4 MLv      2699 1.93e-1   261
## 6 2009-01-01 10:3…  1.41  122       34    5   Mw(mB)  84783 9.33e-1    46
## # … with 3 more variables: rms <dbl>, cphase <int>, region <chr>
```

## 2. Tanpa menggunakan usethis

Cara ini adalah cara manual. Mengapa saya bilang manual? Karena semua dilakukan sendiri langkah-langkahnya dan kita menentukan sendiri letak-letak berkasnya, juga akses halamannya cari sendiri. Kasian yah?

Tapi dengan cara ini kita nggak perlu instal `usethis`.

1. Login ke Github dengan akun sendiri
2. Pergi ke laman Setting > Developer settings > Personal access tokens
3. Atau kasian lah, saya titip aja [link](https://github.com/settings/tokens/)-nya
4. Klik tombol "Generate new token"
5. Beri nama PAT-nya pada kolom "note"
6. Ceklis akses apa saja yang dibutuhkan
7. "Generate token" yang warna hijau
8. Copy/copas token
9. Buat berkas baru di direktori home di komputer dengan nama `.Renviron` (tanpa _extension_), kalau sudah ada, pakai yang ada
10. Buka `.Renviron` menggunakan text editor
11. unting/edit isinya dengan menambahkan baris `GITHUB_PAT=xxxxxxxxxxxxxx` seperti penjelasan sebelumnya
12. Simpan

Bahkan dengan cara ini, kita nggak perlu berinteraksi dengan konsol R atau buka-buka program RStudio!

Sekian dulu.

-----

**Referensi:** https://happygitwithr.com/github-pat.html
