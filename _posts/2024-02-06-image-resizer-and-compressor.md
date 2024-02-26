---
layout: post
title: Script Ruby untuk Resize dan Compress Gambar
published_at: 6 Februari 2024
short_description: Melakukan bulk resize dan compress image secara bulk via script Ruby. 
tags: ruby
featured_image_url: /assets/images/2024/02/06/image-resize-and-compress.jpeg
permalink: /posts/image-resize-and-compressor/
---

Saya punya satu side hustle yang sudah berjalan selama kurang lebih 2 tahun: bikin undangan digital. Lumayan banget buat nambah-nambah uang jajan atau buat tambahan dana di tanggal tua 🤣

Salah satu tantangan ketika ada pesanan baru adalah melakukan resize dan compress gambar yang dikirimkan oleh client. 

Awal-awal merintis, saya masih melakukannya secara manual, satu per satu. Sampai akhirnya di satu titik, dapat orderan yang foto pre-wedding nya banyak banget. Tangan saya pegel ngedit manual.

Akhirnya saya termenung, dan kepikiran: pekerjaan ini repetitif, dan ada polanya juga, kenapa nggak dibuat program untuk resize dan compress gambar sekaligus ya?

Setelah riset sana-sini, ternyata bisa. Saya bikin program-nya pakai bahasa Ruby: bahasa favorit saya.

Script ini punya dependensi ke 2 library: `mini_magick` untuk resize foto, dan `image_optimizer` untuk compress foto. Saat ini programnya masih dibuat dalam 1 file. Rencananya mau dibuat sebagai Ruby gem aja, supaya nanti tinggal install via `gem install`.

Repo-nya bisa dicek di sini: <a href="https://github.com/adiprnm/image-resizer" target="_blank">https://github.com/adiprnm/image-resizer</a>
