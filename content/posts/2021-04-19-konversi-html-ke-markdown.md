---
title: "Konversi HTML Ke Markdown"
date: 2021-04-19T10:27:32+07:00
---

{{< toc >}}

>  **TL;DR** : untuk konversi HTML ke markdown, saya menggunakan pandoc tapi lewat R, bukan langsung dengan bash, karena saya terlalu cupu.

Beberapa tahun belakangan ini saya tidak pernah menyimpan catatan-catatan yang saya buat dengan baik dan rapi, sehingga berserakan di mana-mana. Tapi sekarang mudah-mudahan tidak lagi. Saya sedang menggunakan aplikasi ketik yang sedang naik daun (juga), yaitu [Obsidian](https://obsidian.md/). Dengannya saya bisa sekaligus memanajemen pikiran saya dan juga (mudah-mudahan) hidup saya dengan menggunakannya untuk mengetik kegiatan sehari-hari.

Obsidian memungkinkan saya untuk membuat semacam Wikipedia atau dokumentasi tentang kehidupan saya dan arsip pikirkan juga perasaan saya dalam bentuk tulisan. Sebetulnya saya malas sekali mengakui bahwa saya termasuk orang yang suka *journaling*, sedikit, maksudnya tidak terlalu rutin. Tapi nggak apa-apa. Kita coba saja.

Sistem yang digunakan Obsidian sama dengan beberapa aplikasi *note-taking* lain (selain [Notion](https://notion.so)) yang disebut [Zettelkasten](https://en.wikipedia.org/wiki/Zettelkasten) (bahasa Jerman untuk *card index box*). Biasa orang-orang membandingkannya dengan [Roam Research](https://roamresearch.com/) atau Notion.

## Bukan Notion

Sebetulnya saya suka dengan Notion karena fiturnya yang disebut "database". Keren. Karena memungkinkan saya untuk bisa membuat kanban yang langsung terintegrasi dengan daftar pengarsipan tulisan. Namun karena Notion tidak menggunakan [enkripsi e2e](https://protonmail.com/blog/wp-content/uploads/2015/05/bob-alice.jpg), rasanya tulisan-tulisan yang bersifat pribadi jadi *gimanaa gitu* kalau disimpan di situ. Jadi, saya ingin coba pakai alternatif lain. Kebetulan Obsidian.

## Evernote ke Obsidian

Nah, ceritanya, saya sedang memindahkan berbagai macam catatan yang dulu pernah saya buat untuk bisa saya sunting lagi dan rapikan ulang menggunakan format markdown dari dalam Obsidian. Obsidian juga menggunakan metode *formatting* ini untuk mengetik.

Saya menemukan tulisan lamaaa sekali yang merupakan hasil konversi dari [Evernote](https://evernote.com/). Mungkin, tulisan itu saya buat ketika saya masih menggunakan sistem operasi Windows dulu, saya juga tidak yakin. Sudah lupa karena sudah lama.

Dulu memang saya sempat pakai Evernote sebentar. Berkas yang terekspor dari Evernote ini menggunakan format HTML. Maka saya harus konversi agar bisa disunting kembali menggunakan Obsidian.

## HTML ke Markdown

Sebetulnya saya sudah menginstal **pandoc** di sistem komputer saya, bisa diakses menggunakan perintah bash dari terminal. Namun karena saya sangat cupu dalam menggunakan bash, makan saya pakai R saja. Saya sudah punya paket **rmarkdown** di R yang juga merupakan "kepanjangan tangan" dari pandoc.

Kode yang saya gunakan seperti berikut:

```R
library("rmarkdown")
path <- "/home/andi/Documents/Notes/Evernote/"
files <- dir(path, pattern = "html")
path <- paste0(path, files)

for (i in path) {
  out <- gsub("html", "md", i)
  pandoc_convert(i, to = "markdown_strict", output = out)
}
```

Variabel `path` merupakan path ke berkas-berkas tulisan saya dalam format HTML, yang kemudian dikonversi menggunakan fungsi `pandoc_convert()`. Iya, saya pakai for loop karena berkasnya banyak, tapi tidak terlalu banyak. Variabel `out` digunakan untuk mengubah nama yang semula berakhiran `*.html` menjadi `*.md`.

Tapi hasilnya masih sedikit "cacat" karena ada masalah pada encoding berkas. Entahlah. Saya juga nggak ngerti. Setidaknya ini meringankan pekerjaan saya agar tidak copas-copas dari HTML ke markdown bolak-balik secara manual. Nanti kita coba akalin lagi mulai dari sini.