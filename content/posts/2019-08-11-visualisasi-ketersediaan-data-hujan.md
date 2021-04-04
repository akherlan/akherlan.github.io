---
title: "Visualisasi Ketersediaan Data Hujan"
date: '2019-08-11'
tags: rstats
categories: belajar
---

## Objective

Tutorial ini merupakan catatan pengingat bagi saya. Kan, syukur kalau bisa dibagi ke teman-teman semua. Tujuan tutorialnya adalah untuk membuat visualisasi "kekosongan" data hujan yang saya miliki. Atau dengan kata lain untuk mengetahui berapa persen *sih* kelengkapannya?

Harapannya: agar tahu mana yang masih harus dilegkapi. Juga bisa memilih data hujan mana, serta data hujan kapan yang bisa saya gunakan untuk tahap analisis berikutnya.

## Preparation

Yang kita butuhkan untuk melakukan ini semua tentu saja **data** hujan. Saya menyimpannya dalam format `.Rda`. Sebenarnya juga bisa dari `.csv` atau `.xls`, tapi kalau dalam format data R tentu lebih rapi. Jadi saya pakai itu. Data hujan yang saya gunakan ini juga sudah bisa teman-teman akses [dari tadi](#) sebenarnya. Resolusi datanya hujan harian.

Selain data, kita juga butuh beberapa paket *library* untuk manipulasi. Makna manipulasi di sini bukan "memalsukan", tetapi "ngotak-ngatik".

```r
# library yang dibutuhkan
library(dplyr)         # manipulasi data
library(lubridate)     # manipulasi tanggal
library(ggplot2)       # plot grafik

# memuat data, sesuaikan lokasi file
load(file = "~/R/repo/hujan/data/prc/Raingauge/Precip.Rda")

# menghilangkan hari yang kosong (aneh, ya?)
Precip <- Precip[!is.na(Precip$tgl),]

# kategorisasi nama stasiun
Precip$NamaStasiun <- as.factor(Precip$NamaStasiun)

summary(Precip)
```

Data ini sudah saya rapikan sebelumnya. Agar teman-teman bisa mengakses data ini dari RStudio di komputer masing-masing, silakan sesuaikan nilai `"~/R/repo/hujan/data/precip.Rda"` dengan direktori yang tepat sesuai lokasi teman-teman menyimpannya.

Simpan dalam hati? Oh, jangan.

Kembali ke laptop!

Kalau diperhatikan dari hasil `summary` data, kolom tanggal (**tgl**) dan kolom curah hujan (**prc**) sudah tidak ada data kosong (*NA*) seperti pada **(LONx, LATy)**. Tetapi, sebenarnya ada beberapa tanggal yang data hujannya memang kosong. Hanya saja saya hilangkan.

Maka berikutnya, kita akan menghitung jumlah stasiun yang punya rekaman data pada hari X. *Check it out!*

## Counting Data

```r
p.mod <- Precip %>%
  group_by(tgl) %>%
  summarise(count = sum(as.numeric(ifelse(!is.na(prc), yes = 1, no = 0)))) %>%
  mutate(persen = (count / nlevels(Precip$NamaStasiun))*100)
```

Baris kode di atas akan membuat tabel baru bernama **p.mod**, yang merupakan ringkasan dari tabel **Precip** dengan nilai-nilai yang kita butuhkan untuk membuat visualisasi.

1. Bagian `count = ...` bertujuan untuk membuat kolom baru yang berisi hasil hitungan jumlah data. Jika pada hari X stasiun hujan Q memiliki rekaman data, maka dihitung satu. Termasuk data nol (0 bukan NA).
2. Bagian `persen = ...` adalah untuk membuat kolom baru yang berisi perhitungan persentase data hujan harian yang tersedia dari ke-19 stasiun hujan yang digunakan datanya. Jumlah stasiun yang punya data harian (nilai dalam masing-masing cell pada kolom **count**) dibagi dengan jumlah stasiun (`nlevels(Precip$NamaStasiun)`) kemudian dikali 100 persen.

Kalau kita lihat struktur tabel **p.mod** itu seperti berikut.
```r
str(p.mod)   # struktur data
```

Kalau dilihat dalam bentuk tabel, seperti di bawah ini.
```r
head(p.mod)   # menampilkan 6 rekaman data teratas
```

## Plotting

Tiba saatnya untuk *plotting* grafik. Waktu yang ditunggu-tunggu. Berikut baris data yang digunakan.

```r
p.mod %>%
mutate(bulan = month(tgl, label = TRUE, abbr = TRUE),
      tahun  = year(tgl),
      hari   = wday(tgl,label=TRUE),
      pekan  = ceiling(day(tgl)/7)) %>%
      group_by(bulan, tahun, hari, pekan) %>%
  
  ggplot() + aes( hari, pekan, fill = persen) + 
    geom_tile(colour = "white") + 
    facet_grid(tahun~bulan) + 
    scale_fill_gradient2(low="blue", mid="yellow", high="red",
                         na.value = "grey70", midpoint=50) +
    theme(axis.title=element_blank(),
          axis.text=element_blank(),
          axis.ticks=element_blank(),
          strip.text=element_text(angle=0),
          strip.text.y=element_text(angle=0),
          panel.spacing = unit(0, "lines"))
```

Taraaaaa, jadi.

<script async src="https://telegram.org/js/telegram-widget.js?14" data-telegram-post="teknologimasagitu/11" data-width="100%" data-userpic="false"></script>

## Conclution

Hhmmm... Data paling lengkap sepertinya pada 2009. Sepakat? Atau kita eliminasi saja stasiun hujannya. Hahaha... Pada 2013 terjadi ke-ompong-an. Kita pakai 2004-2009 saja, bagaimana?

Terima kasih. Semoga bermanfaat.

-----

## Reference
- Manuel Gimond's note [here](https://mgimond.github.io/meteo_waterville/)
