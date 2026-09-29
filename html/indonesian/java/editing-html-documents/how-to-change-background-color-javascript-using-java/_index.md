---
category: general
date: 2026-09-29
description: Ubah warna latar belakang dengan JavaScript dalam file HTML menggunakan
  Java. Pelajari cara memuat HTML di Java, menjalankan JS di HTML, dan memodifikasi
  HTML dengan Java untuk latar belakang halaman baru.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change background color javascript
- load html in java
- run js in html
- modify html with java
- set page background
language: id
lastmod: 2026-09-29
og_description: Ubah warna latar belakang dengan JavaScript pada halaman HTML menggunakan
  Java. Tutorial ini menunjukkan cara memuat HTML di Java, menjalankan JS di HTML,
  dan mengatur latar belakang halaman secara programatis.
og_image_alt: Screenshot of Java code that changes the page background color
og_title: Ubah warna latar belakang JavaScript dengan Java – panduan langkah demi
  langkah
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Change background color javascript in an HTML file using Java. Learn
    to load html in java, run js in html, and modify html with java for a new page
    background.
  headline: How to change background color javascript using Java
  type: TechArticle
tags:
- Java
- HTMLUnit
- JavaScript
- HTML manipulation
title: Cara mengubah warna latar belakang javascript menggunakan Java
url: /id/java/editing-html-documents/how-to-change-background-color-javascript-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengubah warna latar belakang javascript menggunakan Java

Jika Anda perlu **change background color javascript** dalam file HTML yang ada, Anda dapat melakukannya sepenuhnya dari Java tanpa membuka peramban. Tutorial ini menunjukkan cara **load html in java**, mengeksekusi potongan JavaScript kecil, dan kemudian **modify html with java** sehingga latar belakang halaman diperbarui.  

Solusi ini bekerja dengan pustaka sumber terbuka **HTMLUnit**, yang menyediakan peramban headless yang dapat mengevaluasi JavaScript persis seperti peramban nyata. Pada akhir panduan ini Anda akan memiliki metode yang dapat digunakan kembali yang **sets page background** ke warna apa pun yang Anda pilih.

## Prasyarat

| Apa yang Anda butuhkan | Mengapa penting |
|---------------|----------------|
| Java 8 atau lebih baru | HTMLUnit memerlukan setidaknya Java 8. |
| Alat build Maven atau Gradle | Untuk menarik dependensi HTMLUnit secara otomatis. |
| File HTML yang ingin Anda edit (mis., `input.html`) | Dokumen sumber yang akan dimuat dan diubah. |

Tambahkan HTMLUnit ke proyek Anda:

*Maven*  

```xml
<dependency>
    <groupId>net.sourceforge.htmlunit</groupId>
    <artifactId>htmlunit</artifactId>
    <version>2.71.0</version>
</dependency>
```

*Gradle*  

```gradle
implementation 'net.sourceforge.htmlunit:htmlunit:2.71.0'
```

> **Pro tip:** Gunakan versi stabil terbaru dari HTMLUnit untuk mendapatkan mesin JavaScript yang paling akurat.

## Mengubah warna latar belakang javascript – memuat HTML di Java

Langkah pertama adalah memuat dokumen HTML ke dalam objek `HTMLPage`. Ini memberi Anda API mirip DOM dan konteks eksekusi JavaScript.

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;

public class BackgroundColorChanger {

    /**
     * Loads an HTML file from the given path.
     *
     * @param htmlPath absolute or relative path to the source HTML file
     * @return HtmlPage representing the loaded document
     * @throws IOException if the file cannot be read
     */
    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        // WebClient acts as a headless browser; disabling CSS speeds up loading.
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);

        // Convert the file path to a URL that HTMLUnit can understand.
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }
}
```

*Mengapa ini penting*: `WebClient` membuat lingkungan sandbox tempat JavaScript dapat dijalankan, sehingga Anda dapat **run js in html** persis seperti peramban pengguna.

## Menjalankan js di html untuk mengatur latar belakang halaman

Setelah halaman dimuat, Anda dapat mengevaluasi ekspresi JavaScript apa pun. Potongan kode di bawah mengubah gaya `backgroundColor` dari elemen `<body>`.

```java
/**
 * Executes JavaScript that changes the page background color.
 *
 * @param page   the HtmlPage loaded earlier
 * @param color  any valid CSS color string, e.g., "lightblue" or "#ffcc00"
 */
private static void changeBackground(HtmlPage page, String color) {
    // The eval method runs JavaScript in the page's context.
    String script = "document.body.style.backgroundColor = '" + color + "';";
    page.getEnclosingWindow().getScriptableObject().eval(script);
}
```

*Penjelasan*:  
- `document.body.style.backgroundColor` adalah properti DOM standar untuk latar belakang halaman.  
- Dengan memanggil `eval`, kami **run js in html** tanpa memerlukan jendela peramban nyata.  
- Metode ini dapat digunakan kembali untuk warna apa pun, memenuhi kebutuhan **set page background**.

## Memodifikasi html dengan java dan menyimpan hasilnya

Setelah skrip dijalankan, DOM mencerminkan gaya baru. Anda sekarang dapat menulis HTML yang diperbarui kembali ke disk.

```java
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Saves the modified HTML content to a new file.
 *
 * @param page          the HtmlPage that has been altered
 * @param outputPath    destination file path
 * @throws IOException  if writing fails
 */
private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
    // page.asXml() returns the current HTML markup, including the changed style.
    String updatedHtml = page.asXml();
    Files.write(Paths.get(outputPath), updatedHtml.getBytes());
}
```

Menggabungkan semuanya memberikan Anda satu program yang dapat dijalankan:

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class BackgroundColorChanger {

    public static void main(String[] args) {
        // Adjust these paths for your environment.
        String inputFile = "YOUR_DIRECTORY/input.html";
        String outputFile = "YOUR_DIRECTORY/js_modified.html";
        String newColor = "lightblue"; // Change to any CSS color you need.

        try {
            HtmlPage page = loadHtml(inputFile);
            changeBackground(page, newColor);
            saveModifiedHtml(page, outputFile);
            System.out.println("Background color changed to '" + newColor + "' and saved to " + outputFile);
        } catch (IOException e) {
            System.err.println("Error processing HTML file: " + e.getMessage());
        }
    }

    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }

    private static void changeBackground(HtmlPage page, String color) {
        String script = "document.body.style.backgroundColor = '" + color + "';";
        page.getEnclosingWindow().getScriptableObject().eval(script);
    }

    private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
        String updatedHtml = page.asXml();
        Files.write(Paths.get(outputPath), updatedHtml.getBytes());
    }
}
```

### Output yang Diharapkan

Menjalankan program mencetak:

```
Background color changed to 'lightblue' and saved to YOUR_DIRECTORY/js_modified.html
```

Membuka `js_modified.html` di peramban apa pun menampilkan halaman dengan latar belakang biru muda, mengonfirmasi bahwa operasi **change background color javascript** berhasil.

## Variasi umum dan kasus tepi

| Situasi | Cara menanganinya |
|-----------|------------------|
| **Berbagai format warna** | Berikan nilai yang kompatibel dengan CSS apa pun (`"red"`, `"#ff0000"`, `"rgb(255,0,0)"`). |
| **Tag `<body>` hilang** | Skrip akan gagal secara diam-diam; Anda dapat terlebih dahulu memastikan `<body>` ada dengan `page.getFirstByXPath("//body")`. |
| **File HTML besar** | Nonaktifkan CSS (`setCssEnabled(false)`) dan aktifkan hanya fitur JavaScript yang Anda butuhkan untuk mengurangi penggunaan memori. |
| **Menjalankan beberapa skrip** | Panggil `changeBackground` berulang kali atau buat metode utilitas yang menerima daftar perintah JavaScript. |

## Kesimpulan

Anda sekarang tahu cara **change background color javascript** dengan memuat file HTML di Java, **run js in html**, dan **modify html with java** untuk **set page background** ke warna apa pun yang Anda pilih. Contoh lengkap di atas bekerja dengan pustaka HTMLUnit terbaru dan dapat diintegrasikan ke dalam pipeline otomatisasi yang lebih besar, seperti pemrosesan batch laporan HTML atau menyiapkan templat email.

**Langkah selanjutnya**  
- Jelajahi manipulasi DOM lainnya (mis., menyisipkan elemen, menghapus skrip).  
- Gabungkan pendekatan ini dengan renderer PDF untuk menghasilkan PDF dari halaman yang bergaya.  
- Coba gunakan mesin headless lain seperti Selenium WebDriver jika Anda memerlukan kesetiaan peramban penuh.

Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Get Computed Style Java – Extract Background Color from HTML](/html/english/java/css-html-form-editing/get-computed-style-java-extract-background-color-from-html/)
- [How to Load HTML, Set Device DPI & Read Background Color](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Generate HTML from JavaScript in Java – Complete Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/generate-html-from-javascript-in-java-complete-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}