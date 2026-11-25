---
category: general
date: 2026-03-05
description: Cara melakukan query HTML di Java untuk membaca file HTML dan mengekstrak
  gambar. Pelajari cara membaca file HTML dengan Java, mendapatkan URL gambar dengan
  Java, dan mengiterasi NodeList di Java.
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: id
og_description: Cara men-query HTML di Java dan mengambil URL gambar. Panduan ini
  menunjukkan cara membaca file HTML di Java, menemukan gambar, dan mengiterasi NodeList
  di Java.
og_title: Cara Mengquery HTML di Java – Ekstrak URL Gambar
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: Cara Mengkueri HTML di Java – Ekstrak URL Gambar
url: /id/java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menanyakan HTML di Java – Ekstrak URL Gambar

Pernah bertanya-tanya **cara menanyakan HTML** di Java untuk mengambil setiap gambar pada sebuah halaman? Anda tidak sendirian—para pengembang terus-menerus perlu membaca file HTML, meng-scrape gambar, dan kemudian melakukan sesuatu yang berguna dengan URL‑nya. Dalam tutorial ini kami akan membahas contoh praktis yang menunjukkan secara tepat **cara menanyakan HTML**, membaca file HTML gaya Java, dan mendapatkan URL gambar secara Java‑wise.

Kami akan menggunakan Aspose.HTML untuk Java, tetapi konsep—XPath, selector CSS, dan iterasi atas `NodeList`—berlaku untuk perpustakaan DOM apa pun. Pada akhir panduan ini Anda akan merasa nyaman dengan **cara mengekstrak gambar**, mengetahui cara **mengiterasi NodeList Java**, dan memiliki potongan kode siap‑jalankan yang dapat Anda masukkan ke dalam proyek Anda.

![Contoh cara menanyakan HTML di Java](https://example.com/placeholder.png "Cara menanyakan HTML di Java")

---

## Apa yang Akan Anda Pelajari

- Memuat dokumen HTML dari disk (read HTML file Java)
- Menemukan tag `<img>` menggunakan baik XPath maupun selector CSS (how to extract images)
- Mengulang `NodeList` yang dihasilkan (iterate over NodeList Java)
- Mencetak atribut `src` setiap gambar (get image URLs Java)

Tanpa layanan eksternal, tanpa alat build yang rumit—hanya Java biasa dan satu dependensi Maven.

---

## Prasyarat

- Java 8 atau lebih baru terpasang
- Maven atau Gradle untuk manajemen dependensi
- Familiaritas dasar dengan struktur HTML
- Opsional namun membantu: sebuah file HTML sederhana (`sample.html`) yang berisi beberapa elemen `<figure><img …></figure>`

Jika Anda sudah memiliki semua itu, kita bisa langsung melompat.

---

## Langkah 1: Read HTML File Java – Muat Dokumen

Hal pertama yang harus dilakukan: kita perlu membawa HTML ke memori. Kelas `HTMLDocument` milik Aspose.HTML melakukan pekerjaan berat tersebut. Anggap saja seperti membuka buku sehingga Anda dapat membuka ke halaman mana pun.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.NodeList;
import com.aspose.html.dom.Element;

/**
 * Demonstrates how to query HTML in Java and extract image URLs.
 */
public class QueryExample {
    public static void main(String[] args) throws Exception {

        // ① Load the HTML document from a local file.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

**Mengapa ini penting:** Memuat file memberi Anda pohon DOM yang dapat Anda tanyakan. Jika jalurnya salah, Anda akan mendapatkan `FileNotFoundException`, jadi periksa kembali lokasi sebelum menjalankan.

---

## Langkah 2: Temukan Gambar dengan XPath – Cara Mengekstrak Gambar

XPath adalah bahasa kueri yang kuat yang memungkinkan Anda menargetkan node dengan presisi laser. Di sini kami meminta setiap `<img>` di dalam `<figure>` yang juga memiliki atribut `alt`.

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**Mengapa XPath?** Ia singkat dan tetap bekerja meski HTML berantakan. Ekspresi `//figure/img[@alt]` diterjemahkan menjadi: “setiap `<img>` di bawah `<figure>` yang memiliki atribut `alt`.” Jika Anda perlu memfilter berdasarkan atribut lain, cukup ubah bagian dalam kurung siku.

---

## Langkah 3: Temukan Gambar dengan Selector CSS – Cara Alternatif Mengekstrak Gambar

Kadang‑kadang Anda lebih suka sintaks CSS karena mencerminkan apa yang Anda tulis di stylesheet. `querySelectorAll` menerima selector yang sama seperti yang Anda gunakan di browser.

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**Mengapa keduanya?** Menunjukkan kedua cara memberi Anda kebebasan memilih alat yang paling nyaman. Dalam praktiknya Anda akan tetap pada satu cara, tetapi memiliki kedua contoh membuat tutorial ini lebih lengkap.

---

## Langkah 4: Iterate Over NodeList Java – Dapatkan URL Gambar Java

Sekarang kita memiliki koleksi, kita perlu melaluinya satu per satu. Di sinilah **iterate over NodeList Java** berperan. Kami akan mengambil atribut `src` setiap gambar dan mencetaknya.

```java
        // ④ Loop through the NodeList returned by the CSS query.
        for (int i = 0; i < cssImages.getLength(); i++) {
            Element imageElement = (Element) cssImages.item(i);
            // Extract the "src" attribute – that’s the image URL.
            System.out.println("Image src: " + imageElement.getAttribute("src"));
        }
    }
}
```

**Mengapa menggunakan loop `for` klasik?** `NodeList` milik Aspose tidak mengimplementasikan `Iterable`, sehingga sintaks `for‑each` yang disingkat tidak akan terkompilasi. Menggunakan loop indeks adalah cara yang dapat diandalkan untuk **iterate over NodeList Java**.

---

## Output yang Diharapkan

Menjalankan program terhadap HTML contoh seperti:

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

Akan menghasilkan sesuatu yang mirip dengan:

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

Jika file Anda berisi lebih banyak tag `<img>` yang memenuhi kriteria, jumlahnya akan bertambah sesuai.

---

## Kesalahan Umum & Tips Pro

- **Masalah jalur file:** Gunakan jalur absolut atau letakkan `sample.html` relatif terhadap direktori kerja proyek Anda.  
- **Atribut `alt` tidak ada:** Kuery XPath/CSS kami memfilter pada `[@alt]`. Jika Anda membutuhkan *semua* gambar, hapus filter atribut (`//figure/img` atau `figure img`).  
- **Kinerja:** Untuk dokumen yang sangat besar, pertimbangkan parser streaming, tetapi untuk kebanyakan tugas web‑scraping pendekatan DOM sudah cukup.  
- **Masalah enkoding:** Aspose.HTML menghormati charset yang dideklarasikan dalam HTML. Jika Anda melihat karakter yang rusak, pastikan file disimpan sebagai UTF‑8.  

---

## Memperluas Contoh

Sekarang Anda dapat **get image URLs Java**, Anda mungkin ingin:

1. **Mengunduh gambar** menggunakan `java.net.URL` dan `Files.copy`.  
2. **Menyimpan URL ke basis data** untuk pemrosesan selanjutnya.  
3. **Memfilter berdasarkan ekstensi file** (`src.endsWith(".png")`).  

Semua hal ini merupakan ekstensi sederhana dari loop yang ditunjukkan pada Langkah 4.

---

## Kesimpulan

Dalam panduan ini kami membahas **cara menanyakan HTML** di Java dari awal hingga akhir: memuat file, menemukan gambar dengan baik XPath maupun selector CSS, dan **mengiterasi NodeList Java** untuk mencetak `src` setiap gambar. Anda kini memiliki dasar yang kuat untuk **cara mengekstrak gambar**, dan Anda tahu persis **cara membaca file HTML Java** menggunakan Aspose.HTML.

Silakan sesuaikan kode ini sesuai kebutuhan scraping Anda—baik itu mengambil atribut lain, menangani tag `<a>`, atau mengirim URL ke downloader. Polanya tetap sama: muat, tanyakan, iterasi, dan aksi.

Punya pertanyaan atau ingin berbagi kasus penggunaan menarik? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}