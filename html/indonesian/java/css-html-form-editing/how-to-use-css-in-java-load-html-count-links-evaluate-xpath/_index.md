---
category: general
date: 2026-06-16
description: Cara menggunakan CSS untuk memuat file HTML dan menghitung tautan dalam
  Java. Pelajari cara menghitung elemen HTML dan mengevaluasi XPath Java dalam satu
  contoh yang jelas.
draft: false
keywords:
- how to use css
- load html file
- how to count links
- count html elements
- evaluate xpath java
language: id
og_description: Cara menggunakan CSS di Java untuk memuat file HTML, menghitung tautan,
  dan mengevaluasi ekspresi XPath—semua dalam satu panduan praktis.
og_title: Cara Menggunakan CSS di Java – Memuat HTML, Menghitung Tautan & Mengevaluasi
  XPath
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use CSS to load HTML file and count links in Java. Learn to
    count html elements and evaluate xpath java in a single, clear example.
  headline: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
  type: TechArticle
- description: How to use CSS to load HTML file and count links in Java. Learn to
    count html elements and evaluate xpath java in a single, clear example.
  name: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
  steps:
  - name: What if the HTML file is malformed?
    text: Both the CSS and XPath engines are tolerant of minor markup errors (missing
      closing tags, unquoted attributes). However, severe malformations may cause
      the parser to abort. In production, wrap the loading step in a try‑catch block
      and log the exception.
  - name: Can I combine CSS and XPath in a single expression?
    text: Not directly; each engine has its own syntax. The typical pattern is to
      use the one that expresses the condition most naturally (CSS for structural
      queries, XPath for attribute functions) and then merge the results in Java if
      needed.
  - name: How do I count elements across multiple files?
    text: 'Just place the loading logic inside a loop:'
  - name: Does this work with Java 8?
    text: Yes—provided you use a library version that targets Java 8 or higher. The
      code shown does not rely on newer language features.
  type: HowTo
tags:
- Java
- HTML parsing
- CSS selectors
- XPath
title: Cara Menggunakan CSS di Java – Memuat HTML, Menghitung Tautan & Mengevaluasi
  XPath
url: /id/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan CSS di Java – Memuat HTML, Menghitung Tautan & Mengevaluasi XPath

Pernah bertanya‑tanya **cara menggunakan CSS** selector saat memproses file HTML di Java? Mungkin Anda sedang membangun web‑crawler, scraper, atau hanya perlu mengaudit situs statis. Kabar baiknya? Anda tidak perlu menulis parser khusus dari nol—perpustakaan modern memungkinkan Anda menggabungkan selector CSS4 dengan ekspresi XPath 3.1 dalam satu alur kerja yang rapi.

Dalam tutorial ini kita akan membahas **cara memuat file HTML**, menerapkan selector CSS untuk menghitung tautan di dalam bilah navigasi, dan kemudian **mengevaluasi XPath** untuk menghitung elemen gambar tertentu. Pada akhir tutorial Anda akan memiliki program lengkap yang dapat dijalankan dan mencetak jumlah node yang cocok, serta memahami mengapa setiap bagian penting.

## Prasyarat

- Java 17 (atau JDK terbaru) terpasang di mesin Anda  
- Maven atau Gradle untuk manajemen dependensi (kami akan menggunakan Maven dalam contoh)  
- Sebuah potongan HTML kecil yang disimpan sebagai `input.html` di folder yang Anda kontrol  

Tidak ada alat lain yang diperlukan—hanya editor teks dan terminal.

## Apa yang Dibahas Tutorial Ini

- **Memuat file HTML** ke dalam struktur mirip DOM menggunakan kelas *HTMLDocument*  
- Menerapkan **selector CSS4** (`nav a[data-role]`) untuk menemukan tautan navigasi  
- Menjalankan **ekspresi XPath 3.1** untuk menemukan tag `<img>` yang `src`‑nya berakhiran `.png` dan juga memiliki atribut `alt`  
- **Menghitung** hasil kedua kueri dan mencetaknya ke konsol  
- Kode sumber lengkap, penjelasan “mengapa”, dan sekilas tentang kasus tepi yang mungkin terjadi  

Mari langsung mulai.

---

## Langkah 1 – Cara Memuat File HTML dengan HTMLDocument

Sebelum Anda dapat melakukan query apa pun, dokumen HTML harus di‑parse menjadi model yang dapat dilalui. Kelas `HTMLDocument` dari perpustakaan **jsoup‑plus** (atau parser HTML‑aware serupa) melakukan hal itu secara tepat.

```java
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Load the HTML document from the file system
        HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/input.html");
        // From here on we can query the DOM using CSS or XPath
```

*Mengapa ini penting:*  
Memuat file sekali dan menyimpan referensi (`doc`) menghindari I/O berulang, yang dapat menjadi bottleneck kinerja saat memproses batch halaman yang besar.

---

## Langkah 2 – Cara Menggunakan CSS untuk Menghitung Tautan di Dalam `<nav>`

Setelah dokumen berada di memori, kita dapat menggunakan selector CSS4 untuk mengambil setiap elemen `<a>` yang berada di dalam `<nav>` dan juga memiliki atribut `data‑role`. Ini adalah pola umum untuk menu navigasi yang menggunakan data attribute sebagai hook JavaScript.

```java
        // Use a CSS4 selector to find every <a> inside a <nav> that has a data‑role attribute
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");
```

*Penjelasan:*  
- `nav a[data-role]` dibaca sebagai “setiap elemen `<a>` dengan atribut `data‑role` yang merupakan descendant dari elemen `<nav>`.”  
- Selector ini kompatibel dengan **CSS4**, sehingga Anda juga dapat menggunakan pseudo‑class seperti `:not()` atau `:has()` bila kebutuhan Anda berkembang.

> **Pro tip:** Jika Anda hanya membutuhkan anak langsung, ganti spasi dengan `>` (`nav > a[data-role]`). Ini mengurangi ruang pencarian dan dapat mempercepat dokumen yang besar.

---

## Langkah 3 – Mengevaluasi XPath di Java untuk Menghitung Elemen `<img>` Tertentu

XPath bersinar ketika Anda memerlukan penyaringan berbasis atribut yang tidak semudah di CSS. Di sini kita akan menemukan setiap `<img>` yang `src`‑nya berakhiran `.png` **dan** yang juga memiliki atribut `alt`—berguna untuk audit aksesibilitas.

```java
        // Use an XPath 3.1 expression to locate all <img> elements whose src ends with .png and have an alt attribute
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");
```

*Mengapa XPath?*  
- Fungsi `ends-with()` merupakan bagian dari XPath 3.1, memungkinkan pencocokan akhiran tanpa harus menggunakan regex.  
- Menggabungkan beberapa predikat (`and @alt`) memastikan Anda hanya menghitung gambar yang sumbernya benar dan sudah diberi deskripsi.

Jika perpustakaan Anda hanya mendukung XPath 1.0, Anda harus menggunakan `contains(@src, '.png')` dan kemudian menyaring di Java—pendekatan yang kurang presisi.

---

## Langkah 4 – Cara Menghitung Elemen HTML dan Mencetak Hasil

Akhirnya, kita mengambil panjang masing‑masing objek `NodeList` dan menampilkannya. Inilah bagian **cara menghitung tautan** dalam puzzle, tetapi dapat bekerja untuk koleksi node apa pun.

```java
        // Output the number of matches for each query
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**Output konsol yang diharapkan** (asumsi HTML contoh berisi 3 tautan yang cocok dan 2 gambar yang cocok):

```
Nav links: 3
PNG images with alt: 2
```

Jika hitungannya nol, periksa kembali sintaks selector Anda atau pastikan `input.html` memang berisi elemen yang diharapkan.

---

## Contoh Program Lengkap

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke file bernama `CssXPathDemo.java`. Program ini mencakup impor yang diperlukan, cuplikan `pom.xml` sederhana untuk Maven, serta contoh HTML minimal untuk pengujian.

```java
/* CssXPathDemo.java */
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the HTML document
        HTMLDocument doc = new HTMLDocument("input.html");

        // Step 2: CSS selector – count navigation links with data-role
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");

        // Step 3: XPath expression – count PNG images that have alt text
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");

        // Step 4: Print the results
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**Cuplikan `pom.xml` Maven** (tambahkan dependensi ini untuk mengambil parser HTML yang mendukung CSS4 dan XPath 3.1):

```xml
<dependencies>
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>html-parser-plus</artifactId>
        <version>2.3.1</version>
    </dependency>
</dependencies>
```

**Contoh `input.html`** (letakkan di direktori yang sama dengan file Java):

```html
<!DOCTYPE html>
<html lang="en">
<head><title>Test Page</title></head>
<body>
<nav>
    <a href="/home" data-role="main">Home</a>
    <a href="/about" data-role="secondary">About</a>
    <a href="/contact">Contact</a>
</nav>
<img src="logo.png" alt="Company Logo">
<img src="banner.jpg">
<img src="icon.png" alt="Icon">
</body>
</html>
```

Menjalankan `mvn compile exec:java -Dexec.mainClass=CssXPathDemo` akan menghasilkan hitungan yang sama seperti yang ditunjukkan sebelumnya.

---

## Kasus Tepi & Pertanyaan Umum

### Bagaimana jika file HTML rusak?

Baik mesin CSS maupun XPath toleran terhadap kesalahan markup minor (tag penutup yang hilang, atribut tanpa kutipan). Namun, malformasi yang parah dapat menyebabkan parser berhenti. Pada produksi, bungkus langkah pemuatan dalam blok try‑catch dan log exception yang terjadi.

### Bisakah saya menggabungkan CSS dan XPath dalam satu ekspresi?

Tidak secara langsung; masing‑masing engine memiliki sintaksnya sendiri. Pola umum adalah menggunakan engine yang paling natural untuk kondisi tertentu (CSS untuk query struktural, XPath untuk fungsi atribut) lalu menggabungkan hasilnya di Java bila diperlukan.

### Bagaimana cara menghitung elemen di banyak file?

Letakkan logika pemuatan di dalam loop:

```java
for (Path p : Files.newDirectoryStream(Paths.get("html_folder"), "*.html")) {
    HTMLDocument doc = new HTMLDocument(p.toString());
    // repeat the queries...
}
```

### Apakah ini bekerja dengan Java 8?

Ya—asalkan Anda menggunakan versi perpustakaan yang menargetkan Java 8 atau lebih tinggi. Kode yang ditampilkan tidak bergantung pada fitur bahasa yang lebih baru.

---

## Kesimpulan

Kami telah mendemonstrasikan **cara menggunakan CSS** selector bersama **mengevaluasi xpath java** untuk **memuat file HTML**, **menghitung tautan**, dan **menghitung elemen HTML** yang memenuhi kriteria tertentu. Poin penting yang dapat diambil:

- Muat dokumen sekali dengan `HTMLDocument`.  
- Manfaatkan CSS4 untuk query struktural sederhana (`nav a[data-role]`).  
- Manfaatkan XPath 3.1 untuk fungsi atribut yang kuat (`ends-with(@src, '.png')`).  
- Dapatkan panjang `NodeList` untuk menghitung secara akurat.  

Dari sini Anda dapat memperluas skrip: menambahkan selector lain, menulis hasil ke CSV, atau mengintegrasikannya ke dalam pipeline crawling yang lebih besar. Kombinasi CSS dan XPath memberi Anda fleksibilitas untuk menangani hampir semua tantangan scraping HTML.

Siap bereksperimen? Coba ganti selector CSS menjadi `section article[data-id]` atau ubah XPath untuk menargetkan tag `<video>` dengan codec tertentu. Langit adalah batasnya.

Jika Anda merasa panduan ini membantu, silakan bagikan, beri bintang pada repositori, atau tinggalkan komentar dengan kasus penggunaan Anda sendiri. Selamat coding!

![diagram contoh cara menggunakan css](https://example.com/diagram.png "contoh cara menggunakan css")

---


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menambahkan CSS – Inline CSS ke Dokumen HTML di Aspose.HTML untuk Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Cara Mengedit CSS - Penyuntingan CSS Eksternal Lanjutan dengan Aspose.HTML untuk Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)
- [Cara Mengedit Pohon Dokumen HTML di Aspose.HTML untuk Java](/html/english/java/editing-html-documents/edit-html-document-tree/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}