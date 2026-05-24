---
category: general
date: 2026-02-16
description: Cara melakukan query HTML menggunakan Aspose.HTML untuk Java. Pelajari
  cara memilih elemen HTML, menyaring elemen berdasarkan atribut, mengiterasi NodeList,
  dan mendapatkan konten teks dalam beberapa langkah.
draft: false
keywords:
- how to query html
- select html elements
- get text content
- iterate over nodelist
- filter elements by attribute
language: id
og_description: Cara mengquery HTML dengan Aspose.HTML untuk Java. Tutorial ini menunjukkan
  cara memilih elemen HTML, memfilter berdasarkan atribut, mengiterasi NodeList, dan
  mendapatkan konten teks.
og_title: Cara Menquery HTML di Java – Panduan Lengkap
tags:
- Java
- Aspose.HTML
- DOM manipulation
title: Cara melakukan query HTML di Java – Pilih elemen, filter berdasarkan atribut,
  dan dapatkan konten teks
url: /id/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/
---

kept same number of #.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara melakukan query HTML di Java – Panduan Lengkap

Pernah bertanya-tanya **bagaimana cara melakukan query HTML** ketika Anda perlu mengambil data dari halaman statis? Mungkin Anda sedang membangun alat pemantauan harga atau meng-scrape daftar produk untuk sebuah katalog. Dalam kedua kasus, Anda akan segera menyadari bahwa memilih node yang tepat dan mengekstrak teksnya adalah inti dari pekerjaan.  

Dalam tutorial ini kami akan membahas contoh dunia nyata yang **memilih elemen HTML**, **menyaring elemen berdasarkan atribut**, **mengiterasi NodeList**, dan akhirnya **mengambil konten teks** dari setiap kecocokan. Pada akhir tutorial Anda akan memiliki program Java siap‑jalankan yang mencetak setiap judul produk dengan harga lebih dari 100 USD.

> **Tip pro:** Aspose.HTML for Java membuat selector bergaya CSS terasa alami, sehingga Anda tidak memerlukan pustaka parsing terpisah.

---

## Apa yang Anda Butuhkan

- **Java 17** (atau JDK terbaru) – API bekerja dengan Java 8+ tetapi versi yang lebih baru memberikan kinerja yang lebih baik.
- **Aspose.HTML for Java** JARs – Anda dapat mengunduh trial gratis dari situs web Aspose atau menambahkan dependensi Maven.
- File **catalog.html** sederhana yang berisi kartu produk dengan atribut `data-price` (kami akan menampilkan cuplikan di bawah).

Tidak ada kerangka kerja lain yang diperlukan; kode dijalankan sebagai aplikasi Java biasa.

---

## Langkah 1: Muat dokumen HTML dari disk  

Hal pertama yang harus Anda lakukan adalah memberi tahu Aspose.HTML di mana file sumber Anda berada. Kelas `Document` mewakili seluruh pohon DOM, seperti yang dibangun oleh browser.

```java
import com.aspose.html.dom.*;
import com.aspose.html.load.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document from a local file
        Document htmlDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **Mengapa ini penting:** Memuat dokumen membuat DOM yang hidup, yang memungkinkan Anda menjalankan selector CSS nanti. Jika file tidak ditemukan, Aspose melempar `FileNotFoundException` yang jelas, sehingga Anda tahu persis apa yang harus diperbaiki.

---

## Langkah 2: Menyaring elemen berdasarkan atribut – pilih kartu produk dengan harga tinggi  

Sekarang kami hanya menginginkan elemen `.product‑card` yang atribut `data-price`‑nya melebihi 100. Selector `.product-card[data-price>100]` melakukan hal itu dengan tepat.

```java
        // Select product cards where data-price > 100
        NodeList highPricedCards = htmlDoc.querySelectorAll(".product-card[data-price>100]");
```

> **Cara kerjanya:**  
> - `.product-card` mencocokkan setiap elemen dengan kelas tersebut.  
> - `[data-price>100]` adalah filter atribut yang hanya menyimpan node yang nilai numerik `data-price`‑nya lebih besar dari 100.  
> Ini adalah sintaks yang sama seperti yang Anda gunakan di konsol DevTools browser, membuatnya intuitif bagi pengembang front‑end.

---

## Langkah 3: Iterasi NodeList dan ambil konten teks  

Sebuah `NodeList` berperilaku seperti koleksi berbentuk array, tetapi Anda tetap memerlukan loop untuk melintasi setiap elemen. Di dalam loop kami akan **memilih elemen anak** (`.title`) dan membaca teksnya, kemudian mengambil harga dari atribut.

```java
        // Loop through each matching card
        for (Node node : highPricedCards) {
            Element cardElement = (Element) node; // cast to Element for convenience

            // Get the product title text
            String productTitle = cardElement.querySelector(".title").getTextContent();

            // Retrieve the raw price from the attribute
            String productPrice = cardElement.getAttribute("data-price");

            // Output the result
            System.out.println(productTitle + " – $" + productPrice);
        }
    }
}
```

**Output yang diharapkan** (asumsi HTML berisi dua kartu yang memenuhi syarat):

```
Deluxe Coffee Maker – $149
Smart LED TV – $799
```

> **Kesalahan umum:** Jika sebuah kartu tidak mengandung elemen `.title`, `querySelector` mengembalikan `null` dan memanggil `getTextContent()` akan melempar `NullPointerException`. Pemeriksaan defensif (`if (titleElement != null)`) disarankan untuk kode produksi.

---

## Langkah 4: Contoh lengkap yang dapat dijalankan  

Menggabungkan semuanya, berikut program lengkap yang dapat Anda salin‑tempel ke IDE Anda. Ingat untuk mengganti `YOUR_DIRECTORY/catalog.html` dengan jalur sebenarnya ke file HTML Anda.

```java
import com.aspose.html.dom.*;
import com.aspose.html.load.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document from a file
        Document htmlDoc = new Document("YOUR_DIRECTORY/catalog.html");

        // Step 2: Select product cards whose data-price attribute is greater than 100
        NodeList highPricedCards = htmlDoc.querySelectorAll(".product-card[data-price>100]");

        // Step 3: Iterate over the matching elements and extract title and price
        for (Node node : highPricedCards) {
            Element cardElement = (Element) node;
            String productTitle = cardElement.querySelector(".title").getTextContent();
            String productPrice = cardElement.getAttribute("data-price");

            // Step 4: Output the product information
            System.out.println(productTitle + " – $" + productPrice);
        }
    }
}
```

Simpan file sebagai `CssSelectorDemo.java`, kompilasi dengan `javac`, dan jalankan `java CssSelectorDemo`. Jika semuanya sudah diatur dengan benar, Anda akan melihat produk berharga tinggi dicetak ke konsol.

---

## Langkah 5: Memahami konsep dasar  

### Memilih elemen HTML  

Metode `querySelectorAll` menerima selector CSS yang valid apa pun. Itu berarti Anda dapat menggabungkan nama kelas, ID, filter atribut, pseudo‑class, dan bahkan selector keturunan. Misalnya, `".category[data-active=true] a[href]"` akan mengambil semua tautan di dalam kategori yang aktif.

### Mengambil konten teks  

`Element.getTextContent()` mengembalikan teks yang digabungkan dari elemen dan keturunannya, menghilangkan tag HTML. Ini adalah cara paling andal untuk mengambil teks yang terlihat, tidak seperti `innerHTML` yang menyertakan markup.

### Mengiterasi NodeList  

Sebuah `NodeList` mengimplementasikan `Iterable<Node>`, sehingga Anda dapat menggunakan loop `for‑each` yang ditingkatkan seperti yang ditunjukkan di atas. Jika Anda memerlukan akses berbasis indeks, Anda dapat memanggil `item(int index)` atau mengubahnya menjadi `List<Node>`.

### Menyaring elemen berdasarkan atribut  

Selector atribut mendukung operator seperti `=`, `~=`, `|=`, `^=`, `$=`, `*=` dan operator perbandingan numerik (`>`, `<`, `>=`, `<=`). Ini memberi Anda kontrol detail tanpa menulis kode Java tambahan.

---

## Langkah 6: Kasus tepi dan variasi  

- **Perbandingan numerik vs. string:** Selector `[data-price>100]` berfungsi karena nilai atribut dapat diparse sebagai angka. Jika atribut Anda berisi karakter non‑numerik (mis., `"100USD"`), perbandingan akan gagal. Hapus satuan terlebih dahulu atau gunakan filter khusus di Java.
- **Nama kelas sensitif huruf:** Selector CSS sensitif huruf dalam mode XML. Pastikan nama kelas di HTML Anda cocok persis.
- **Beberapa kecocokan per kartu:** Jika sebuah kartu berisi beberapa elemen `.title`, `querySelector` mengembalikan yang pertama. Gunakan `querySelectorAll(".title")` dan loop jika Anda memerlukan semua judul.

---

## Langkah 7: Langkah selanjutnya – apa lagi yang dapat Anda lakukan?  

Sekarang Anda telah menguasai **cara melakukan query HTML**, pertimbangkan untuk memperluas skrip:

1. **Tuliskan hasil ke CSV** – berguna untuk memasukkan data ke spreadsheet.
2. **Gabungkan dengan klien HTTP** – ambil halaman remote secara langsung menggunakan `java.net.http.HttpClient`.
3. **Terapkan filter yang lebih kompleks** – mis., pilih item yang sedang diskon (`[data-discount>0]`) atau urutkan berdasarkan harga menggunakan stream Java.
4. **Integrasikan dengan basis data** – simpan produk yang diekstrak di SQLite atau MySQL untuk analisis selanjutnya.

Semua ide ini menggunakan kembali konsep inti yang sama: **memilih elemen HTML**, **menyaring elemen berdasarkan atribut**, **mengiterasi NodeList**, dan **mengambil konten teks**.

---

## Kesimpulan  

Kami telah membahas **cara melakukan query HTML** dengan Aspose.HTML untuk Java dari awal hingga akhir. Dengan memuat dokumen, menggunakan selector CSS yang menyaring pada `data-price`, melakukan loop melalui `NodeList` yang dihasilkan, dan mengekstrak baik judul maupun harga, Anda kini memiliki pola yang solid yang dapat Anda sesuaikan untuk tugas scraping atau ekstraksi data apa pun.

Jalankan kode tersebut, sesuaikan selector agar cocok dengan markup Anda, dan saksikan data mengalir keluar dari halaman ke aplikasi Java Anda. Selamat coding!

![contoh cara query html](/images/query-html-example.png "contoh cara query html")

*Gambar menunjukkan output konsol dari program, menggambarkan judul produk dan harga yang diekstrak.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}