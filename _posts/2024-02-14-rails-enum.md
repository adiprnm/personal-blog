---
layout: post
title: Tips ActiveRecord enum di Ruby on Rails
published_at: 14 Februari 2024
short_description: Beberapa tips yang bisa diimplementasikan di kode Ruby on Rails kamu supaya semakin clean.
tags: ruby, ruby on rails
featured_image_url: /assets/images/2024/02/enum-1.png
permalink: /posts/tips-rails-enum/
---

Saya sebenarnya pernah seputar ActiveRecord enum di akun X saya. Saya coba share di sini juga, mudah-mudahan bermanfaat.

# Jadi, apa itu enum?

Enum itu bisa dibilang sebuah nilai yang sudah kita tentukan nila-nilai pastinya, atau istilahnya *pre-defined*. Sehingga, jika user mencoba untuk memasukkan nilai lain selain dari nilai-nilai yang sudah ditentukan, secara definisi seharusnya tidak diperkenankan.

Di Ruby on Rails, ada 2 cara buat deklarasi enum. Cara pertama yaitu pakai array biasa macam gambar di bawah ini:

<img src="/assets/images/2024/02/enum-1.png" alt="Deklarasi enum array">

Cara kedua yaitu pakai hash (struktur data key-value) macam gambar berikut:

<img src="/assets/images/2024/02/enum-2.png" alt="Deklarasi enum hash">

Bedanya, kalau pakai cara pertama, kolom `state` harus berupa integer, karena yang disimpan ke database adalah indeks dari enum. Cara kedua harus berupa string.

# Cara pakenya gimana aja tuh?

Kurang lebih begini:

### 1. Instansiasi dan Create Record Baru

Misal kita mau membuat sebuah record author baru dengan state `active`, kita bisa pakai `Author.active.new` untuk instansiasi, atau `Author.active.create` untuk langsung create record baru.

<img src="/assets/images/2024/02/instantiation.jpeg" alt="Instansiasi menggunakan enum">

### 2. Query Database

Proses query ke database bisa dilakukan lebih sederhana. `Author.where(state: "active")` hasilnya akan sama dengan `Author.active`. Enum ini bisa digabungkan dengan scope model.

Misal, kita punya scope `published_at_least_five_books` untuk melakukan query author mana saja yang sudah menerbitkan setidaknya lima buku.

Kita bisa langsung panggil `Author.active.published_at_least_five_books` untuk melakukan query author mana saja yang masih aktif **dan** sudah menerbitkan setidaknya lima buku.

<img src="/assets/images/2024/02/querying.jpeg" alt="Query menggunakan enum">


### 3. Kondisi dan Update Data

Hasil `author.state == "active"` akan sama dengan `author.active?`. Hasil `author.update(state: "retired")` hasilnya akan sama dengan `author.retired!`.

<img src="/assets/images/2024/02/enum-condition.png" alt="Cek kondisi status author menggunakan enum">

<img src="/assets/images/2024/02/enum-update.jpeg" alt="Update state via enum">

### 4. Relasi

Katakanlah penulis punya banyak buku. Buku ini ada yang masih draft, dan ada yang sudah dipublikasikan. Jika dikonversi menjadi model, kurang lebih begini:

<img src="/assets/images/2024/02/relationship-1.png" alt="Model books">

Di model author, kita bisa definisikan bahwa *author has many published books* secara sederhana macam gambar di bawah ini:

<img src="/assets/images/2024/02/relationship-1.1.png" alt="Penulis mempunyai banyak buku yang telah dipublikasikan">

<img src="/assets/images/2024/02/relationship-2.jpeg" alt="Penulis mempunyai banyak buku yang telah dipublikasikan">


### 5. Kondisi Join Query

Misal ada requirement begini: kita perlu menampilkan penulis siapa aja yang punya buku yang masih draft. Kita nggak bisa pakai scope `published_books`, sehingga kita perlu buat scope baru yang lebih general, katakanlah `has_many :books`.

<img src="/assets/images/2024/02/join-1.png" alt="Author punya banyak buku">

Kombinasi antara `joins` dan `merge` akan me-return hasil yang diharapkan.

<img src="/assets/images/2024/02/join-2.jpeg" alt="Mendapatkan author yang punya buku masih draft.">

Yaa kurang lebih itu adalah cara menggunakan enum di Ruby on Rails. Hope it helps!
