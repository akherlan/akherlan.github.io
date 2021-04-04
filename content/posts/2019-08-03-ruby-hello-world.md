---
title: 'Ruby: "Hello World!"'
date: '2019-08-03'
tags: ruby
categories: belajar
---

## Latar Belakang

Saya dapat kerjaan bantu-bantu ngurusin web. Nggak ngoding-ngoding banget, sih. Enak jadinya, cenderung lebih santai. Tapi saya masih belum puas dengan metode yang saat ini sedang dipakai. Berbekal rasa penasaran saya cari tahu teknologi apa yang kiranya cocok digunakan seandainya ganti metode *develop*-nya.

Ceritanya, ini adalah website yang diharapkan bisa punya fitur ruang kumpul komunitas dan proses pesan jasa. Saya cari tahu *framework* yang dipakai oleh kompetitor terbesar saat ini. Wah, **Ruby on Rails**. Kecurigaan saya terjawab. Sejak awal saya selalu berpikir tentang kerangka kerja yang satu ini.

Konon, bahasa Ruby dipakai untuk membangun website Bukalapak. Juga AirBnB, GitHub, Shopify, itu memang yang terkenal. Saya tertarik dengan Ruby ketika mengetahui Bukalapak dan Shopify menggunakannya. Saya pikir, kayaknya web yang sekarang lagi dibangun ini tipe-tipenya cocok, nih, dibikin pakai ginian. Tapi, tentu saja nggak akan keburu. Sebentar lagi target peluncurannya. Apalagi yang sekarang memang sudah cukup matang. Senggaknya untuk tahap awal. Kata saya.

Ketika beberapa kali main-main ke artikel orang yang membicarakan tentang Ruby, memang bahasa ini banyak digunakan oleh perusahaan rintisan (nggak semuanya tentunya). Alasannya, karena lebih murah untuk kegiatan membangun, seperti pada umumnya sumber terbuka (*open source*) memang murah bahkan gratis. Juga karena, katanya, mudah dipelajari. Ah, ini banyak katanya-katanya.

Tapi saya jadi pingin belajar, lho!

## Antarmuka Ruby: irb

Ruby di Ubuntu saya menggunakan **irb** atau katakanlah *"Interface Ruby"* lewat terminal emulator. Tandanya sudah jalan, begini:

```ruby
irb(main):001:0>
```

Cara masuk ke antarmuka ini tinggal ketikkan `irb` di terminal kesayanganmu.

## Hello World!

Yang pertama saya pelajari tentu saja `"Hello world!"`. Bagaimana?

```ruby
puts "Hello world!"
```

Hasilnya?

```ruby
irb(main):001:0> puts "Hello world!"
Hello world!
=> nil
```

Tentu saja saya langsung lanjut ke materi berikutnya karena langsung bisa. Selanjutnya belajar aritmatika sederhana.

## Operasi Aritmatika

Operasi yang mirip dengan bahasa pemrograman lainnya seperti `+`, `-`, `*`, `/`, `**`, `%`, tapi untuk akar dipakai `Math.sqrt()`. Kenapa begitu? Nanti saya belajar lagi. Dijelaskan oleh tutorial. Tapi saya kurang perhatikan. Hehe... Nanti saja di-*update* artikel ini.

```ruby
2 + 2
```

Hasilnya:

```ruby
irb(main):002:0> 2 + 2
=> 4
```

Nah, lo! Tadi ada `==> nil` begitu. Sekarang nggak. Coba lagi:

```ruby
6 / 3
```

Hasilnya seperti ini:

```ruby
irb(main):003:0> 6 / 3
=> 2
```

Coba kita balik lagi ke yang string tadi.

```ruby
puts "saya siapa"
```

Hasilnya:

```ruby
irb(main):004:0> puts "saya siapa"
saya siapa
=> nil
```

Baiklah, tapi kalau begini:

```ruby
print "saya andi"
```

Maka hasilnya menjadi:

```ruby
irb(main):005:0> print "saya andi"
saya andi=> nil
```

Oke. Lanjut nulis nanti lagi. Sudah malam dan lelah.

Bye!
