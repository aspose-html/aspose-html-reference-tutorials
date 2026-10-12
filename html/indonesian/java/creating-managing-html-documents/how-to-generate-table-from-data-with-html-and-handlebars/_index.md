---
category: general
date: 2026-10-12
description: Pelajari cara membuat tabel dari data dan mengisi tabel dari JSON menggunakan
  Handlebars. Panduan langkah demi langkah untuk mengulang baris tabel dalam tabel
  HTML dinamis.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: id
lastmod: 2026-10-12
og_description: Buat tabel dari data dan isi tabel dari JSON menggunakan Handlebars.
  Ikuti tutorial ini untuk membuat tabel HTML dinamis dengan baris tabel yang berulang.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Buat tabel dari data dengan Handlebars – panduan lengkap
schemas:
- author: Aspose
  dateModified: '2026-10-12'
  description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  headline: How to generate table from data with HTML and Handlebars
  type: TechArticle
- description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  name: How to generate table from data with HTML and Handlebars
  steps:
  - name: 1. Empty data sets
    text: 'If the JSON array is empty, Handlebars will still render the header row
      but no data rows. To display a friendly message, wrap the table in a conditional
      block:'
  - name: 2. Nested loops (e.g., multiple addresses per person)
    text: 'When a person can have several addresses, you can nest another `{{#foreach}}`
      inside the row:'
  - name: 3. Using a real API
    text: 'Replace the static `<script id="people-data">` with a fetch call:'
  - name: 4. Accessibility considerations
    text: '* Add `scope="col"` to `<th>` elements. * Use `<caption>` to describe the
      table purpose. * Ensure sufficient color contrast if you apply custom CSS.'
  type: HowTo
tags:
- HTML
- Handlebars
- JSON
- templating
title: Cara membuat tabel dari data dengan HTML dan Handlebars
url: /id/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menghasilkan tabel dari data dengan HTML dan Handlebars

Jika Anda perlu **menghasilkan tabel dari data** di sebuah halaman web, tutorial ini akan menunjukkan caranya secara tepat. Dengan menggunakan loop Handlebars sederhana, Anda dapat **mengisi tabel dari JSON**, membuat **pengulangan baris tabel**, dan menghasilkan **tabel HTML dinamis** yang memperbarui diri setiap kali sumber data berubah.

Dalam beberapa menit ke depan Anda akan melihat contoh lengkap yang dapat dijalankan, memahami mengapa setiap bagian penting, dan belajar cara menyesuaikan pola ini untuk skenario yang lebih kompleks seperti kolom bersyarat atau objek bersarang.

## Apa yang akan Anda buat

Kami akan membuat tabel HTML yang:

* Membaca payload JSON yang berisi daftar orang.
* Mengulangi satu baris tabel untuk setiap orang (`repeat table rows`).
* Menyisipkan nama depan, nama belakang, dan alamat masing‑masing orang ke dalam sel yang sesuai.
* Berfungsi tanpa rendering sisi server – seluruh proses terjadi di browser.

**Prasyarat**

* Pengetahuan dasar tentang HTML dan JavaScript.
* Browser modern (Chrome, Edge, Firefox, atau Safari).
* Handlebars.js – kami akan memuatnya dari CDN, jadi tidak diperlukan alat build.

---

## Langkah 1: Siapkan sumber data JSON

Langkah pertama adalah mendefinisikan objek JavaScript yang meniru JSON yang akan Anda terima dari sebuah API. Handlebars bekerja dengan objek biasa, jadi Anda dapat menyematkan data langsung dalam tag `<script>` untuk tujuan demonstrasi.

```html
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>
```

**Mengapa ini penting** – Dengan menempatkan data dalam elemen `<script>` terpisah, Anda dapat dengan mudah menggantinya dengan panggilan AJAX nyata di kemudian hari. Struktur (`Persons.Person`) cocok dengan jalur yang digunakan dalam blok Handlebars `{{#foreach Persons.Person}}`, yang esensial untuk **populate table from JSON**.

---

## Langkah 2: Tulis template Handlebars yang mengulang baris

Selanjutnya, buat blok `<script type="text/x-handlebars-template">` yang berisi markup tabel. Handlebars akan menggantikan placeholder dengan nilai sebenarnya dan mengulang `<tr>` untuk setiap orang.

```html
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <!-- Header row describing the columns -->
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <!-- Data row – this block is repeated for each Person -->
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>
```

**Penjelasan bagian‑bagian penting**

* `{{#foreach Persons.Person}}` memberi tahu Handlebars untuk **repeat table rows** untuk setiap entri dalam array `Persons.Person`.
* Ekspresi `{{FirstName}} {{LastName}}` dan `{{Address.*}}` mengambil nilai dari elemen array saat ini.
* Membungkus seluruh tabel dalam atribut `data_merge` bersifat opsional; dapat berguna untuk pemrosesan lanjutan atau selector CSS.

---

## Langkah 3: Muat Handlebars dan kompilasi template

Kami akan mengambil Handlebars dari CDN, mengurai JSON, mengompilasi template, dan menyuntikkan HTML akhir ke dalam halaman.

```html
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  // Parse the JSON stored in the <script id="people-data">
  const rawData = document.getElementById('people-data').textContent;
  const context = JSON.parse(rawData);

  // Grab the template markup and compile it
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);

  // Generate the final HTML by applying the context
  const html = template(context);

  // Insert the generated table into the DOM
  document.getElementById('output').innerHTML = html;
</script>
```

**Mengapa mengompilasi pada runtime?** – Mengompilasi template sekali dan menggunakannya kembali membuat halaman tetap cepat, terutama ketika data sering berubah. Pola ini juga memudahkan **populate table from JSON** berkali‑kali tanpa memuat ulang halaman.

---

## Langkah 4: Sediakan kontainer untuk tabel yang dihasilkan

Tambahkan placeholder `<div>` tempat tabel dinamis akan muncul. Ini menjaga markup tetap bersih dan memisahkan kepentingan antara tata letak statis dan konten yang dihasilkan.

```html
<div id="output"></div>
```

Saat skrip pada Langkah 3 dijalankan, `<div id="output">` akan berisi elemen `<table>` yang sudah lengkap, siap untuk styling atau manipulasi lebih lanjut.

---

## Langkah 5: Verifikasi output dan beri gaya pada tabel (opsional)

Buka halaman di browser dan Anda akan melihat tabel seperti contoh di bawah ini:

![Tangkapan layar menampilkan tabel yang dihasilkan dari data](image.png "Tangkapan layar menampilkan tabel yang dihasilkan dari data")

```html
<table border="1" data_merge="true">
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <tr>
    <td>Alice Anderson</td>
    <td>Maple 123, Springfield</td>
  </tr>
  <tr>
    <td>Bob Baker</td>
    <td>Oak 456, Rivertown</td>
  </tr>
</table>
```

**Styling opsional** – Jika Anda menginginkan tampilan yang lebih bersih, tambahkan beberapa aturan CSS berikut:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## Menangani kasus tepi dan variasi umum

### 1. Set data kosong

Jika array JSON kosong, Handlebars tetap akan merender baris header tetapi tidak ada baris data. Untuk menampilkan pesan yang ramah, bungkus tabel dalam blok bersyarat:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. Loop bersarang (misalnya, beberapa alamat per orang)

Ketika seorang orang dapat memiliki beberapa alamat, Anda dapat menempatkan `{{#foreach}}` lain di dalam baris:

```handlebars
{{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>
      {{#foreach Address}}
        {{Street}} {{Number}}, {{City}}<br>
      {{/foreach}}
    </td>
  </tr>
{{/foreach}}
```

### 3. Menggunakan API nyata

Ganti `<script id="people-data">` statis dengan panggilan `fetch`:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

Ini memperlihatkan teknik **dynamic table rows** yang sama sambil menarik data secara langsung.

### 4. Pertimbangan aksesibilitas

* Tambahkan `scope="col"` pada elemen `<th>`.
* Gunakan `<caption>` untuk menjelaskan tujuan tabel.
* Pastikan kontras warna cukup jika Anda menerapkan CSS khusus.

---

## Contoh lengkap yang dapat dijalankan

Salin blok berikut ke dalam file `index.html` dan buka di browser. Halaman akan **generate table from data**, **populate table from JSON**, dan mengulang baris secara otomatis.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dynamic table from JSON</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { padding: 8px; text-align: left; border: 1px solid #ddd; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

<!-- Step 1: JSON data source -->
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>

<!-- Step 2: Handlebars template -->
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <tr>
    <th scope="col">Person</th>
    <th scope="col">Address</th>
  </tr>
  {{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
  {{/foreach}}
</table>
</script>

<!-- Step 4: Container for the generated table -->
<div id="output"></div>

<!-- Step 3: Load Handlebars, compile, and render -->
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  const raw = document.getElementById('people-data').textContent;
  const context = JSON.parse(raw);
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);
  document.getElementById('output').innerHTML = template(context);
</script>

</body>
</html>
```

**Hasil yang diharapkan**

Sebuah tabel dua baris (plus header) yang menampilkan “Alice Anderson” dan “Bob Baker” beserta alamat masing‑masing. Halaman berfungsi secara offline, membuktikan bahwa Anda dapat **generate table from data** tanpa komponen server apa pun.

---

## Kesimpulan

Anda kini tahu cara **generate table from data** menggunakan template Handlebars, **populate table from JSON**, dan membuat **repeat table rows** yang membentuk **dynamic HTML table**. Pola ini dapat diskalakan ke set data yang lebih besar, struktur bersarang, dan panggilan API real‑time, memberikan fondasi yang kuat untuk pelaporan sisi klien atau UI admin apa pun.

**Langkah selanjutnya**

* Jelajahi helper Handlebars untuk memformat tanggal atau angka.
* Gabungkan pendekatan ini dengan CSS Grid atau Flexbox untuk tata letak tabel yang responsif.
* Integrasikan pustaka pagination atau sorting untuk menangani set data yang sangat besar.

Silakan bereksperimen dengan bentuk JSON yang berbeda, tambahkan kolom bersyarat, atau ganti Handlebars dengan mesin templating lain—keterampilan baru Anda akan memungkinkan pembuatan antarmuka berbasis data yang fleksibel dengan cepat dan andal.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Create HTML Document with Java – Fetch JSON and Generate Content](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)
- [How to Load HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}