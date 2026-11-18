---
category: general
date: 2026-09-07
description: cara mengikat data dalam tabel HTML dinamis – pelajari cara menghasilkan
  baris tabel dan mengisi bidang nama depan serta nama belakang secara efisien
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: id
lastmod: 2026-09-07
og_description: cara mengikat data dalam tabel HTML dinamis. tutorial ini menunjukkan
  cara menghasilkan baris tabel, menampilkan nama depan dan nama belakang, serta mengisi
  baris tabel dengan JavaScript.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: Cara mengikat data ke tabel HTML dinamis – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-09-07'
  description: how to bind data in a dynamic HTML table – learn how to generate table
    rows and populate first and last name fields efficiently
  headline: How to bind data to a dynamic HTML table with first and last name columns
  type: TechArticle
tags:
- data binding
- html table
- templating
title: Cara mengikat data ke tabel HTML dinamis dengan kolom nama depan dan nama belakang
url: /id/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengikat data ke tabel HTML dinamis dengan kolom nama depan dan nama belakang

Jika Anda perlu **mengikat data** ke dalam tabel yang bertambah dengan setiap catatan, panduan ini menunjukkan solusi lengkap. Anda akan melihat cara menghasilkan tabel HTML dinamis, mengisi baris tabel, dan menampilkan nama depan serta nama belakang setiap orang tanpa menulis markup berulang.

Contoh ini menggunakan sintaks templating ringan yang bekerja di semua browser modern, tetapi konsepnya berlaku untuk Handlebars, Mustache, atau mesin sisi‑server lainnya. Pada akhir tutorial Anda dapat menyalin kode ke dalam proyek Anda dan mulai mengikat data secara instan.

## Apa yang dibahas dalam tutorial ini

* Cara menyusun sumber data yang berisi beberapa orang  
* Cara membuat templat tabel yang dapat digunakan kembali dan diulang untuk setiap entri  
* Cara mengikat data dan menghasilkan markup HTML akhir  
* Kesulitan umum saat mengisi baris tabel dan cara menghindarinya  

Tidak ada pustaka eksternal yang diperlukan, meskipun pola yang sama dapat bekerja dengan kerangka kerja templating populer. Prasyarat satu‑satunya adalah pengetahuan dasar HTML dan JavaScript.

## Prasyarat

* Browser modern (Chrome, Edge, Firefox, atau Safari)  
* Editor untuk file HTML/JavaScript  
* Opsional: file JSON atau objek JavaScript yang mewakili koleksi orang  

## Langkah 1: Tentukan sumber data

Pertama, buat objek JavaScript yang mencerminkan struktur yang digunakan dalam templat. Setiap orang memiliki nama depan, nama belakang, dan objek alamat.

```html
<script>
  // Data source – an array of person objects
  const data = {
    Persons: {
      Person: [
        {
          FirstName: "Alice",
          LastName: "Johnson",
          Address: {
            Street: "Maple",
            Number: "12A",
            City: "Springfield"
          }
        },
        {
          FirstName: "Bob",
          LastName: "Smith",
          Address: {
            Street: "Oak",
            Number: "34B",
            City: "Riverdale"
          }
        }
        // Add more person objects as needed
      ]
    }
  };
</script>
```

**Mengapa ini penting:** Hierarki objek (`Persons.Person`) cocok dengan loop `{{#foreach Persons.Person}}` dalam templat, memungkinkan mesin untuk mengulangi setiap entri secara otomatis.

## Langkah 2: Tulis templat tabel dengan blok pengulangan

Templat di bawah ini menggunakan sintaks gaya Mustache sederhana (`{{#foreach}}`) untuk mengulang `<tr>` bagi setiap orang. Letakkan templat di dalam tag `<script type="text/template">` sehingga browser mengabaikannya sampai Anda memprosesnya.

```html
<script type="text/template" id="table-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <!-- Table header -->
  <tr>
    <th>Person</th><th>Address</th>
  </tr>
  <!-- Row populated with each person's data -->
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>
```

**Mengapa ini penting:** Direktif `{{#foreach Persons.Person}}` memberi tahu mesin untuk mengulangi semua di antara tag pembuka dan penutup untuk setiap objek orang. Di dalam baris Anda dapat merujuk ke properti apa pun (`{{FirstName}}`, `{{LastName}}`, dll.) untuk **mengisi baris tabel** secara dinamis.

## Langkah 3: Implementasikan fungsi rendering kecil

Karena tutorial harus berdiri sendiri, kami akan menulis renderer minimal yang menggantikan placeholder gaya Mustache dengan nilai sebenarnya. Fungsi ini menelusuri objek data, memperluas blok pengulangan, dan menyuntikkan HTML akhir ke halaman.

```html
<script>
  /**
   * Renders a template that contains a single {{#foreach}} block.
   * This implementation is intentionally simple and works for the
   * specific structure used in this tutorial.
   *
   * @param {string} tmpl   The raw template string.
   * @param {object} ctx    The data context (e.g., the `data` object).
   * @returns {string}      The rendered HTML.
   */
  function renderTemplate(tmpl, ctx) {
    // Extract the foreach expression and the block to repeat
    const foreachRegex = /{{#foreach\s+([^}]+)}}([\s\S]*?){{\/foreach}}/;
    const match = tmpl.match(foreachRegex);
    if (!match) return tmpl; // No foreach found

    const path = match[1].trim(); // e.g., "Persons.Person"
    const block = match[2];       // HTML that repeats

    // Resolve the array from the context (supports dot notation)
    const items = path.split('.').reduce((obj, key) => obj && obj[key], ctx);
    if (!Array.isArray(items)) return tmpl;

    // Render each item
    const renderedBlocks = items.map(item => {
      // Replace each {{property}} with the corresponding value
      return block.replace(/{{([^}]+)}}/g, (_, prop) => {
        const value = prop.trim().split('.').reduce((obj, key) => obj && obj[key], item);
        return value !== undefined ? value : '';
      });
    });

    // Replace the whole foreach section with the concatenated rows
    return tmpl.replace(foreachRegex, renderedBlocks.join(''));
  }

  // When the DOM is ready, render the table
  document.addEventListener('DOMContentLoaded', () => {
    const tmpl = document.getElementById('table-template').innerHTML;
    const html = renderTemplate(tmpl, data);
    document.getElementById('output').innerHTML = html;
  });
</script>
```

**Mengapa ini penting:** Renderer menunjukkan **cara menghasilkan tabel** markup secara programatis tanpa harus memasukkan seluruh pustaka. Ini juga memperjelas transformasi dari templat ke HTML akhir, yang membantu Anda menyesuaikan kode ke mesin templating lain di kemudian hari.

## Langkah 4: Tambahkan placeholder di mana tabel yang dihasilkan akan muncul

Buat `<div>` kosong yang akan diisi skrip setelah rendering.

```html
<div id="output"></div>
```

Saat halaman dimuat, skrip menggantikan isi `<div>` ini dengan tabel yang sepenuhnya terisi.

## Langkah 5: Verifikasi hasil

Buka file HTML di browser. Anda harus melihat tabel yang menampilkan nama lengkap dan alamat setiap orang:

| Person          | Address                         |
|-----------------|---------------------------------|
| Alice Johnson   | Maple 12A, Springfield          |
| Bob Smith       | Oak 34B, Riverdale              |

Jika Anda menambahkan lebih banyak objek ke array `data.Persons.Person`, tabel akan otomatis bertambah—memenuhi kebutuhan **mengisi baris tabel**.

## Tips pro: menangani koleksi kosong

Ketika array data kosong, renderer saat ini menghasilkan header tabel kosong. Untuk memberikan pengalaman pengguna yang lebih jelas, tambahkan penjagaan:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

Perubahan kecil ini mencegah tabel kosong muncul dan memberi pengguna umpan balik langsung.

## Variasi umum dan kasus tepi

| Situasi                               | Penyesuaian                                                                 |
|----------------------------------------|----------------------------------------------------------------------------|
| Menggunakan mesin sisi‑server (mis., Handlebars) | Ganti `renderTemplate` khusus dengan `Handlebars.compile` dan berikan objek data yang sama. |
| Perlu mengurutkan baris secara alfabet       | Urutkan `data.Persons.Person` sebelum memanggil `renderTemplate`.               |
| Menambahkan kolom untuk nomor telepon       | Perluas `<tr>` dengan `<td>{{Phone}}</td>` dan sertakan `Phone` di setiap objek orang. |
| Set data besar (ratusan baris)     | Render baris dalam potongan atau gunakan scrolling virtual agar UI tetap responsif. |

## Contoh lengkap yang berfungsi

Berikut adalah file HTML lengkap yang dapat Anda salin‑tempel ke `index.html`. File ini berisi semua bagian yang dibahas di atas.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to bind data to a dynamic HTML table</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { padding: 8px; text-align: left; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

<h1>Dynamic HTML table bound to JavaScript data</h1>

<!-- Step 2: Table template -->
<script type="text/template" id="table-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <tr>
    <th>Person</th><th>Address</th>
  </tr>
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>

<!-- Step 1: Data source -->
<script>
  const data = {
    Persons: {
      Person: [
        {
          FirstName: "Alice",
          LastName: "Johnson",
          Address: { Street: "Maple", Number: "12A", City: "Springfield" }
        },
        {
          FirstName: "Bob",
          LastName: "Smith",
          Address: { Street: "Oak", Number: "34B", City: "Riverdale" }
        }
        // Add more entries as needed
      ]
    }
  };
</script>

<!-- Step 4: Output container -->
<div id="output"></div>

<!-- Step 3: Rendering logic -->
<script>
  function renderTemplate(tmpl, ctx) {
    const foreachRegex = /{{#foreach\s+([^}]+)}}([\s\S]*?){{\/foreach}}/;
    const match = tmpl.match(foreachRegex);
    if (!match) return tmpl;
    const path = match[1].trim();
    const block = match[2];
    const items = path.split('.').reduce((obj, key) => obj && obj[key], ctx);
    if (!Array.isArray(items) || items.length === 0) {
      return '<p>No records found.</p>';
    }
    const renderedBlocks = items.map(item => {
      return block.replace(/{{([^}]+)}}/g, (_, prop) => {
        const value = prop.trim().split('.').reduce((obj, key) => obj && obj[key], item);
        return value !== undefined ? value : '';
      });
    });
    return tmpl.replace(foreachRegex, renderedBlocks.join(''));
  }

  document.addEventListener('DOMContentLoaded', () => {
    const tmpl = document.getElementById('table-template').innerHTML;
    const html = renderTemplate(tmpl, data);
    document.getElementById('output').innerHTML = html;
  });
</script>

</body>
</html>
```

**Output yang diharapkan**

Halaman menampilkan tabel dengan dua baris, masing‑masing menampilkan nama lengkap dan alamat terformat seorang orang. Menambahkan lebih banyak objek ke array `Person` secara otomatis menambah baris baru—menunjukkan **cara menghasilkan tabel** elemen dari data.

## Kesimpulan

Anda kini tahu **cara mengikat data** ke **tabel HTML dinamis**, menghasilkan baris untuk setiap catatan, dan menampilkan nilai nama depan serta nama belakang bersama alamat.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menambahkan CSS – CSS Inline ke Dokumen HTML di Aspose.HTML untuk Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Cara Mengedit Pohon Dokumen HTML di Aspose.HTML untuk Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Cara Mengaktifkan JavaScript di Aspose HTML – Memuat HTML & Mendapatkan Teks](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}