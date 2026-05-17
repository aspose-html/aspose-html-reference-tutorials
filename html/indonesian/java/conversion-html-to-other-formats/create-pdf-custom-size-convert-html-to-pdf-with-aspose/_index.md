---
category: general
date: 2026-03-26
description: Buat PDF ukuran khusus dari HTML menggunakan Aspose.HTML untuk Java.
  Pelajari cara mengonversi HTML ke PDF dan mengatur ukuran halaman PDF dalam beberapa
  langkah saja.
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- change pdf page size
- generate pdf from html
- set pdf page size
language: id
og_description: Buat PDF ukuran kustom dari HTML dengan Aspose. Panduan ini menunjukkan
  cara mengonversi HTML ke PDF, mengubah ukuran halaman PDF, dan mengatur ukuran halaman
  PDF dengan mudah.
og_title: Buat PDF Ukuran Kustom – Panduan Cepat Mengonversi HTML ke PDF
tags:
- aspose
- java
- pdf
- html
title: Buat PDF Ukuran Kustom – Konversi HTML ke PDF dengan Aspose
url: /id/java/conversion-html-to-other-formats/create-pdf-custom-size-convert-html-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF Ukuran Kustom – Konversi HTML ke PDF dengan Aspose

Pernah membutuhkan untuk **membuat PDF ukuran kustom** dari file HTML? Dalam tutorial ini kami akan menunjukkan cara **mengonversi HTML ke PDF** dan mengatur ukuran halaman PDF menggunakan Aspose.HTML untuk Java.  

Jika Anda membuat faktur, laporan, atau e‑book, mendapatkan dimensi halaman yang tepat sangat penting—jika tidak, tata letak Anda akan tampak tidak berpusat atau terpotong.  

Kami akan membimbing Anda melalui setiap langkah, mulai dari memuat HTML sumber hingga menyesuaikan margin, dan selesai dengan PDF siap pakai. Tanpa referensi yang samar, hanya contoh lengkap yang dapat dijalankan yang dapat Anda salin‑tempel hari ini.

## Apa yang Anda Butuhkan

- **Java 17** (atau JDK terbaru apa pun).  
- **Aspose.HTML for Java** JARs – Anda dapat mengambil versi terbaru dari repositori Maven atau situs web Aspose.  
- File `input.html` sederhana yang ditempatkan di folder yang Anda kontrol.  
- IDE atau editor teks pilihan Anda; saya biasanya menulis kode di IntelliJ IDEA, tetapi Eclipse juga berfungsi dengan baik.

Memiliki prasyarat ini berarti Anda tidak akan mengalami error “class not found” di tengah proses.  

Sekarang, mari kita mulai.

![Contoh PDF ukuran kustom](/images/create-pdf-custom-size.png "Tangkapan layar yang menunjukkan PDF yang dihasilkan dengan ukuran halaman dan margin kustom – buat pdf ukuran kustom")

## Buat PDF Ukuran Kustom – Langkah-Langkah Inti

Berikut adalah program Java lengkap yang akan Anda dapatkan. Silakan salin ke dalam file bernama `ConvertHtmlToPdfCustomPage.java` dan jalankan setelah Anda menambahkan dependensi Aspose ke proyek Anda.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfConversionOptions;
import com.aspose.html.saving.PageSize;
import com.aspose.html.saving.Margin;

public class ConvertHtmlToPdfCustomPage {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Set up PDF conversion options
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(PageSize.A4); // Choose page size (A4, Letter, etc.)
        pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Portrait); // Portrait or Landscape
        pdfOptions.setMargins(new Margin(20, 20, 20, 20)); // Margins: left, top, right, bottom (points)

        // Step 3: Convert the HTML document to a PDF file with the custom settings
        Converter.convertHTML(htmlDoc, "YOUR_DIRECTORY/custom_page.pdf", pdfOptions);

        // Step 4: Inform the user that the PDF has been created
        System.out.println("PDF generated with custom page size and margins.");
    }
}
```

### Langkah 1 – Mengonversi HTML ke PDF: Memuat Dokumen

Hal pertama yang kami lakukan adalah **memuat HTML** yang ingin diubah menjadi PDF.  
`HTMLDocument` membaca file, menyelesaikan tautan relatif, dan membangun DOM yang dapat dirender oleh Aspose.  

> **Mengapa ini penting:** Jika HTML merujuk ke CSS atau gambar, Aspose akan mengambilnya relatif terhadap jalur file. Menggunakan jalur absolut (`YOUR_DIRECTORY/input.html`) menghindari kejutan “file not found”.

### Langkah 2 – Mengubah Ukuran Halaman PDF: Mengonfigurasi Opsi

Di sini kami membuat objek `PdfConversionOptions`.  
- `setPageSize(PageSize.A4)` memberi tahu Aspose untuk menggunakan dimensi standar A4 (210 × 297 mm).  
- `setPageOrientation(...)` memutar halaman jika Anda membutuhkan orientasi lanskap.  
- `setMargins(new Margin(20, 20, 20, 20))` memberikan margin 20‑point di setiap sisi.

Anda dapat mengganti `PageSize.A4` dengan `PageSize.LETTER` atau bahkan **ukuran kustom** dengan melewatkan objek `SizeF`, misalnya:

```java
pdfOptions.setPageSize(new SizeF(500, 800)); // width, height in points
```

> **Tips pro:** Satu point sama dengan 1/72 inci. Jika Anda berpikir dalam milimeter, kalikan dengan 2.83465 untuk mendapatkan point.

### Langkah 3 – Menghasilkan PDF dari HTML: Menjalankan Konversi

`Converter.convertHTML` melakukan pekerjaan berat. Ia mengambil `HTMLDocument` yang telah dimuat, jalur output, dan opsi yang baru saja kami konfigurasikan.  

Jika Anda ingin **mengatur ukuran halaman PDF** secara dinamis berdasarkan konten, Anda dapat menghitung dimensi yang diperlukan sebelum langkah ini dan menyesuaikan `pdfOptions` sesuai.

### Langkah 4 – Memverifikasi Hasil

Baris `System.out.println` bersifat opsional, tetapi memberikan umpan balik cepat saat Anda menjalankan program dari konsol. Setelah eksekusi, buka `custom_page.pdf` – Anda akan melihat PDF portrait A4 dengan margin 20‑point seragam, persis seperti yang kami tentukan.

## Konversi HTML ke PDF – Variasi Umum

### Menggunakan Stream Alih-alih Jalur File

Kadang-kadang Anda tidak memiliki file fisik; mungkin HTML berasal dari basis data atau API. Dalam kasus itu, bungkus string dalam `ByteArrayInputStream`:

```java
String htmlContent = "<html><body><h1>Hello, PDF!</h1></body></html>";
HTMLDocument htmlDoc = new HTMLDocument(
        new ByteArrayInputStream(htmlContent.getBytes(StandardCharsets.UTF_8)),
        "http://example.com/");
```

Argumen kedua adalah URL dasar untuk menyelesaikan sumber daya relatif.

### Mengubah Orientasi Halaman

Jika laporan Anda lebar, beralih ke lanskap:

```java
pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Landscape);
```

### Menyetel Margin Secara Halus

Margin menerima nilai floating‑point, sehingga Anda dapat mengatur 0.5 pt untuk batas yang sangat tipis:

```java
pdfOptions.setMargins(new Margin(5.5, 10.2, 5.5, 10.2));
```

### Menangani File HTML Besar

Untuk dokumen yang sangat besar, pertimbangkan mengaktifkan **streaming efisien memori**:

```java
pdfOptions.setUseMemoryCache(true);
```

Ini memberi tahu Aspose untuk menulis data menengah ke file sementara alih-alih menyimpan semuanya di RAM.

## Atur Ukuran Halaman PDF – Kasus Tepi & Jebakan

- **Missing Fonts:** Jika HTML Anda menggunakan font khusus yang tidak terpasang di server, PDF akan kembali ke font default. Sematkan font dengan `pdfOptions.getFontEmbeddingMode().setEmbeddingMode(EmbeddingMode.Always);`.  
- **Image Scaling:** Gambar beresolusi tinggi dapat memperbesar ukuran PDF. Gunakan `pdfOptions.setImageResolution(150);` untuk menurunkan resolusi sambil mempertahankan kualitas.  
- **CSS Compatibility:** Tidak semua properti CSS didukung sepenuhnya. Gunakan teknik tata letak standar (flexbox berfungsi, tetapi grid mungkin memiliki keanehan).  
- **Path Permissions:** Pastikan proses memiliki akses menulis ke `YOUR_DIRECTORY`. Jika tidak, `IOException` akan dilempar.

## Output yang Diharapkan

Menjalankan program menghasilkan PDF yang terlihat seperti ini (ilustrasi konseptual):

```
+---------------------------------------------------+
|                     Header                        |
|                                                   |
|   (HTML rendered content goes here)               |
|                                                   |
|                     Footer                        |
+---------------------------------------------------+
```

- Ukuran halaman: **A4** (210 × 297 mm).  
- Orientasi: **Portrait**.  
- Margin: **20 pt** pada setiap sisi.  

Buka file dengan penampil PDF apa pun (Adobe Reader, Chrome, dll.) untuk mengonfirmasi.

## Kesimpulan

Anda sekarang tahu cara **membuat PDF ukuran kustom** dari sumber HTML menggunakan Aspose.HTML untuk Java. Tutorial ini mencakup seluruh alur: **mengonversi HTML ke PDF**, **mengubah ukuran halaman PDF**, **mengatur ukuran halaman PDF**, dan **menghasilkan PDF dari HTML** dengan margin kustom.  

Silakan bereksperimen—ganti `PageSize.LETTER` dengan ukuran legal, ubah margin, atau sematkan font Anda sendiri. Selanjutnya, Anda mungkin ingin menjelajahi **menambahkan watermark**, **mengenkripsi PDF**, atau **memproses batch beberapa file HTML**. Semua topik tersebut dibangun di atas konsep inti yang baru saja kami bahas.

Ada pertanyaan tentang kasus tepi tertentu? Tinggalkan komentar di bawah, dan saya akan membantu Anda memecahkan masalah. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}