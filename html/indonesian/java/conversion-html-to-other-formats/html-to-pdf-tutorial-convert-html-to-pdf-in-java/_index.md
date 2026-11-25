---
category: general
date: 2026-06-19
description: Pelajari cara menghasilkan PDF dari HTML menggunakan contoh Java sederhana.
  Tutorial HTML ke PDF ini menunjukkan cara mengonversi file HTML menjadi PDF dengan
  OpenHTMLtoPDF.
draft: false
keywords:
- html to pdf tutorial
- generate pdf from html
- convert html file pdf
- create pdf from html
- convert webpage to pdf
language: id
og_description: Tutorial html ke pdf menunjukkan cara menghasilkan PDF dari HTML menggunakan
  Java. Ikuti langkah-langkah untuk mengonversi file HTML ke PDF dengan cepat.
og_title: 'tutorial html ke pdf: panduan konversi Java'
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  headline: 'html to pdf tutorial: Convert HTML to PDF in Java'
  type: TechArticle
- description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  name: 'html to pdf tutorial: Convert HTML to PDF in Java'
  steps:
  - name: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
    text: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
  - name: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
    text: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
  - name: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
    text: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: 'Tutorial html ke pdf: Mengonversi HTML ke PDF dengan Java'
url: /id/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial html ke pdf – Mengubah halaman HTML menjadi PDF dengan Java

Pernah bertanya-tanya bagaimana cara mengubah halaman HTML statis menjadi dokumen PDF yang rapi tanpa meninggalkan IDE Anda? Anda tidak sendirian. Dalam **html to pdf tutorial** ini kami akan membahas contoh Java lengkap yang siap dijalankan yang **generate pdf from html** dalam beberapa menit saja.

Kami akan membahas semua yang Anda butuhkan—penyiapan proyek, menambahkan pustaka yang tepat, menulis kode konversi, dan bahkan tip cepat untuk mengonversi halaman web langsung ke PDF. Pada akhir tutorial Anda akan dapat **convert html file pdf** di mesin Anda sendiri, dan Anda akan memahami cara **create pdf from html** untuk proyek masa depan mana pun.

## Apa yang Anda butuhkan

- Java 17 atau lebih baru (kode ini bekerja dengan JDK terbaru apa pun)
- Maven atau Gradle (kami akan menunjukkan cuplikan Maven)
- File HTML kecil yang ingin Anda ubah menjadi PDF (kami akan membuatnya secara langsung)
- IDE atau editor teks sederhana—pilihan Anda

Itu saja. Tanpa server berat, tanpa SDK berbayar, hanya Java murni dan pustaka open‑source gratis.

## Langkah 1: html to pdf tutorial – Menyiapkan proyek Maven

Pertama-tama. Buat proyek Maven baru (atau tambahkan ke proyek yang sudah ada). Satu-satunya dependensi yang benar‑benar Anda butuhkan adalah **OpenHTMLtoPDF**, yang melakukan pekerjaan berat dalam merender HTML dan CSS menjadi PDF.

```xml
<!-- pom.xml snippet -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>html-to-pdf-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- OpenHTMLtoPDF core -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-pdfbox</artifactId>
            <version>1.0.10</version>
        </dependency>
        <!-- Optional: support for SVG, if your HTML uses it -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-svg-support</artifactId>
            <version>1.0.10</version>
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Jika Anda menggunakan Gradle, dependensi yang sama dapat ditambahkan di bawah `implementation` dalam `build.gradle`.  

Mengapa langkah ini penting: tanpa pustaka tersebut JVM tidak tahu cara menerjemahkan tag HTML menjadi perintah gambar PDF. OpenHTMLtoPDF ringan, aktif dipelihara, dan bekerja dengan CSS‑2.1, sehingga gaya Anda tetap utuh.

## Langkah 2: generate pdf from html – Menyiapkan file HTML contoh

Mari buat `input.html` kecil tepat di sebelah sumber Java kami. Ini membuat contoh menjadi mandiri dan memperlihatkan alur kerja **create pdf from html**.

```html
<!-- src/main/resources/input.html -->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Sample Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        h1 { color: #2E86C1; }
        p { line-height: 1.5; }
    </style>
</head>
<body>
    <h1>Monthly Sales Report</h1>
    <p>This PDF was generated directly from an HTML file using Java.</p>
    <p>All you need is a few lines of code.</p>
</body>
</html>
```

Anda dapat mengganti kontennya dengan apa saja—tabel, gambar, bahkan JavaScript (meskipun perender mengabaikan skrip). Bagian pentingnya adalah file tersebut berada di classpath sehingga konverter dapat menemukannya.

## Langkah 3: convert html file pdf – Menulis utilitas konversi

Sekarang inti dari **html to pdf tutorial**: kelas kecil `HtmlToPdfConverter` yang membaca HTML dan menulis PDF. Kode di bawah ini adalah contoh lengkap yang dapat dijalankan; salin‑tempel ke `src/main/java/com/example/HtmlToPdfConverter.java`.

```java
package com.example;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;

/**
 * Simple utility that converts an HTML file to PDF.
 * It demonstrates the "convert html file pdf" use‑case.
 */
public class HtmlToPdfConverter {

    /**
     * Converts the given HTML file to a PDF file.
     *
     * @param htmlPath path to the source HTML file (can be absolute or classpath)
     * @param pdfPath  destination path for the generated PDF
     * @throws IOException if reading or writing fails
     */
    public static void convert(String htmlPath, String pdfPath) throws IOException {
        // Resolve the HTML file – support both absolute paths and classpath resources
        InputStream htmlStream = Files.exists(Path.of(htmlPath))
                ? Files.newInputStream(Path.of(htmlPath))
                : HtmlToPdfConverter.class.getResourceAsStream(htmlPath);

        if (htmlStream == null) {
            throw new FileNotFoundException("HTML source not found: " + htmlPath);
        }

        // Ensure the output directory exists
        Path pdfFile = Path.of(pdfPath);
        Files.createDirectories(pdfFile.getParent());

        try (OutputStream os = Files.newOutputStream(pdfFile);
             InputStream is = htmlStream) {

            // Builder does the heavy lifting – it parses HTML + CSS and writes PDF bytes
            new PdfRendererBuilder()
                    .withHtmlContent(new String(is.readAllBytes()), null) // base URI null = no external resources
                    .toStream(os)
                    .run();
        }
    }

    // Demo entry point – feel free to run this class directly
    public static void main(String[] args) {
        // Step 1: Specify the input HTML file location
        String htmlPath = "src/main/resources/input.html";

        // Step 2: Specify the desired output PDF file location
        String pdfPath = "target/output.pdf";

        // Step 3: Convert the HTML document to PDF using default conversion settings
        try {
            convert(htmlPath, pdfPath);
            System.out.println("✅ PDF successfully created at " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Mengapa kode ini berhasil

1. **Resource flexibility** – metode pertama memeriksa apakah jalur yang diberikan mengarah ke file nyata; jika tidak, ia beralih ke sumber daya classpath. Itu berarti Anda dapat **convert webpage to pdf** nanti dengan memberikan string URL (cukup ganti panggilan `withHtmlContent` dengan `withUri`).

2. **Automatic directory creation** – `Files.createDirectories` memastikan folder `target/` ada, sehingga Anda tidak akan mendapatkan error “No such file or directory”.

3. **Single‑line conversion** – `PdfRendererBuilder` menangani CSS, font, dan tata letak halaman secara internal. Tidak perlu mengelola halaman PDF secara manual; pustaka melakukannya untuk Anda, menjadikan contoh singkat dan terfokus pada konsep **convert html file pdf**.

## Langkah 4: create pdf from html – Menjalankan program dan memverifikasi

Buka terminal di root proyek dan jalankan:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HtmlToPdfConverter
```

Jika semuanya telah disiapkan dengan benar Anda akan melihat:

```
✅ PDF successfully created at target/output.pdf
```

Buka `target/output.pdf` dengan penampil PDF apa pun. Anda seharusnya melihat header “Monthly Sales Report” yang bergaya, teks paragraf, dan margin yang sama seperti yang Anda definisikan dalam blok `<style>` HTML.

> **Bagaimana jika Anda tidak melihat gaya?**  
> Pastikan CSS berada inline atau berada di folder yang sama dengan HTML. OpenHTMLtoPDF menyelesaikan URL relatif berdasarkan base URI yang Anda berikan ke `withHtmlContent`. Pada cuplikan di atas kami memberikan `null`, yang berfungsi untuk CSS inline sederhana. Untuk stylesheet eksternal, berikan path direktori sebagai argumen kedua.

## Langkah 5: convert webpage to pdf – Menangani URL remote (opsional)

Kadang-kadang Anda perlu **convert webpage to pdf** langsung dari internet—misalnya mengarsipkan kwitansi online. Pustaka mendukung ini melalui `withUri`. Berikut adaptasi cepat:

```java
public static void convertUrl(String url, String pdfPath) throws IOException {
    Path pdfFile = Path.of(pdfPath);
    Files.createDirectories(pdfFile.getParent());

    try (OutputStream os = Files.newOutputStream(pdfFile)) {
        new PdfRendererBuilder()
                .withUri(url)          // Load HTML from the web
                .toStream(os)
                .run();
    }
}
```

Call it like:



## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF Java – Configuring Environment in Aspose.HTML](/html/english/java/configuring-environment/)
- [Convert HTML to PDF in Java – Step‑by‑Step Guide with Page Size Settings](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}