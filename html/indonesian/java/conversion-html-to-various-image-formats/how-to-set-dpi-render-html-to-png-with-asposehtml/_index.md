---
category: general
date: 2026-01-14
description: cara mengatur dpi saat mengonversi URL ke PNG. Pelajari cara merender
  HTML ke PNG, mengatur ukuran viewport, dan menyimpan HTML sebagai PNG menggunakan
  Aspose.HTML di Java.
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: id
og_description: cara mengatur dpi saat mengonversi URL ke PNG. Panduan langkah demi
  langkah untuk merender HTML ke PNG, mengontrol ukuran viewport, dan menyimpan HTML
  sebagai PNG menggunakan Aspose.HTML.
og_title: cara mengatur dpi – Render HTML ke PNG dengan AsposeHTML
tags:
- AsposeHTML
- Java
- image rendering
title: Cara mengatur DPI – Render HTML ke PNG dengan AsposeHTML
url: /id/java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara mengatur dpi – Render HTML ke PNG dengan AsposeHTML

Pernah bertanya-tanya **cara mengatur dpi** untuk gambar mirip screenshot yang dihasilkan dari halaman web? Mungkin Anda membutuhkan PNG 300 DPI untuk cetak, atau thumbnail beresolusi rendah untuk aplikasi seluler. Dalam kedua kasus, triknya adalah memberi tahu mesin render DPI logis yang Anda inginkan, lalu biarkan ia melakukan pekerjaan berat.  

Dalam tutorial ini kami akan mengambil URL langsung, merendernya ke file PNG, **mengatur ukuran viewport**, menyesuaikan DPI, dan akhirnya **menyimpan HTML sebagai PNG**—semua dengan Aspose.HTML untuk Java. Tanpa browser eksternal, tanpa alat baris perintah yang berantakan—hanya kode Java bersih yang dapat Anda masukkan ke proyek Maven atau Gradle apa pun.

> **Pro tip:** Jika hanya menginginkan thumbnail cepat, Anda dapat mempertahankan DPI pada 96 DPI (default untuk kebanyakan layar). Untuk aset siap cetak, naikkan ke 300 DPI atau lebih tinggi.

![contoh cara mengatur dpi](https://example.com/images/how-to-set-dpi.png "contoh cara mengatur dpi")

## Apa yang Anda Butuhkan

- **Java 17** (atau JDK terbaru lainnya).  
- **Aspose.HTML for Java** 24.10 atau lebih baru. Anda dapat mengambilnya dari Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- Koneksi internet untuk mengambil halaman target (contoh menggunakan `https://example.com/sample.html`).  
- Izin menulis ke folder output.

Itu saja—tanpa Selenium, tanpa Chrome headless. Aspose.HTML melakukan rendering di dalam proses, yang berarti Anda tetap berada di dalam JVM dan menghindari beban meluncurkan browser.

## Langkah 1 – Muat Dokumen HTML dari URL

Pertama kami membuat instance `HTMLDocument` yang menunjuk ke halaman yang ingin kami tangkap. Konstruktor secara otomatis mengunduh HTML, mem-parsenya, dan menyiapkan DOM.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*Mengapa ini penting:* Dengan memuat dokumen secara langsung, Anda melewatkan kebutuhan akan klien HTTP terpisah. Aspose.HTML menghormati pengalihan, cookie, dan bahkan otentikasi dasar jika Anda menyematkan kredensial dalam URL.

## Langkah 2 – Bangun Sandbox dengan DPI dan Viewport yang Diinginkan

Sebuah **sandbox** adalah cara Aspose.HTML meniru lingkungan browser. Di sini kami memberitahunya untuk berpura-pura menjadi layar 1280 × 720 dan, yang paling penting, kami mengatur **DPI perangkat**. Mengubah DPI mengubah kepadatan piksel gambar yang dirender tanpa mengubah ukuran logis.

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*Mengapa Anda mungkin menyesuaikan nilai-nilai ini:*  
- **Ukuran viewport** mengontrol bagaimana media query CSS (`@media (max-width: …)`) berperilaku.  
- **DPI perangkat** memengaruhi ukuran fisik gambar saat dicetak. Gambar 96 DPI terlihat baik di layar; gambar 300 DPI tetap tajam di kertas.  

Jika Anda membutuhkan thumbnail berbentuk kotak, cukup ubah `setViewportSize(500, 500)` dan pertahankan DPI rendah.

## Langkah 3 – Pilih PNG sebagai Format Output

Aspose.HTML mendukung beberapa format raster (PNG, JPEG, BMP, GIF). PNG bersifat loss‑less, sehingga cocok untuk screenshot di mana Anda menginginkan setiap piksel dipertahankan.

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

Anda juga dapat menyesuaikan tingkat kompresi (`pngOptions.setCompressionLevel(9)`) jika Anda khawatir tentang ukuran file.

## Langkah 4 – Render dan Simpan Gambar

Sekarang kami memberi tahu dokumen untuk **menyimpan** dirinya sebagai gambar. Metode `save` menerima jalur file dan opsi yang telah dikonfigurasi sebelumnya.

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

Saat program selesai, Anda akan menemukan file PNG di `YOUR_DIRECTORY/sandboxed.png`. Buka file tersebut—jika Anda mengatur DPI ke 300, metadata gambar akan mencerminkan hal itu, meskipun dimensi piksel tetap 1280 × 720.

## Langkah 5 – Verifikasi DPI (Opsional tapi Berguna)

Jika Anda ingin memeriksa kembali bahwa DPI benar-benar diterapkan, Anda dapat membaca metadata PNG dengan pustaka ringan seperti **metadata‑extractor**:

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

Anda akan melihat `300` (atau nilai yang Anda tetapkan) tercetak di konsol. Langkah ini tidak diperlukan untuk rendering, tetapi merupakan pemeriksaan cepat, terutama saat Anda menghasilkan aset untuk alur kerja cetak.

## Pertanyaan Umum & Kasus Tepi

### “Bagaimana jika halaman menggunakan JavaScript untuk memuat konten?”

Aspose.HTML mengeksekusi **subset terbatas** dari JavaScript. Untuk kebanyakan situs statis, ini berfungsi langsung. Jika halaman sangat bergantung pada kerangka kerja sisi klien (React, Angular, Vue), Anda mungkin perlu melakukan pre‑render halaman atau menggunakan browser headless sebagai gantinya. Namun, pengaturan DPI tetap bekerja dengan cara yang sama setelah DOM siap.

### “Bisakah saya merender PDF alih-alih PNG?”

Tentu saja. Ganti `ImageSaveOptions` dengan `PdfSaveOptions` dan ubah ekstensi output menjadi `.pdf`. Pengaturan DPI tetap memengaruhi tampilan raster dari gambar yang disematkan.

### “Bagaimana dengan screenshot resolusi tinggi untuk tampilan retina?”

Cukup gandakan dimensi viewport sambil mempertahankan DPI pada 96 DPI, atau pertahankan viewport dan naikkan DPI ke 192. PNG yang dihasilkan akan berisi dua kali lebih banyak piksel, memberikan kesan retina yang tajam.

### “Apakah saya perlu membersihkan sumber daya?”

`HTMLDocument` mengimplementasikan `AutoCloseable`. Dalam aplikasi produksi, bungkuslah dalam blok try‑with‑resources:

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

Hal ini memastikan sumber daya native dilepaskan dengan cepat.

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah program lengkap yang siap dijalankan. Ganti `YOUR_DIRECTORY` dengan folder sebenarnya di mesin Anda.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

Jalankan kelas tersebut, dan Anda akan mendapatkan PNG yang menghormati pengaturan **cara mengatur dpi** yang Anda tentukan.

## Kesimpulan

Kami telah membahas **cara mengatur dpi** ketika Anda **merender HTML ke PNG**, mencakup langkah **mengatur ukuran viewport**, dan menunjukkan cara **menyimpan HTML sebagai PNG** menggunakan Aspose.HTML untuk Java. Poin pentingnya adalah:

- Gunakan **sandbox** untuk mengontrol DPI dan viewport.  
- Pilih **ImageSaveOptions** yang tepat untuk output lossless.  
- Verifikasi metadata DPI jika Anda perlu menjamin kualitas cetak.  

Dari sini Anda dapat bereksperimen dengan nilai DPI yang berbeda, viewport yang lebih besar, atau bahkan memproses batch daftar URL. Ingin mengonversi seluruh situs web menjadi thumbnail PNG? Cukup loop melalui array URL dan gunakan kembali konfigurasi sandbox yang sama.

Selamat merender, semoga screenshot Anda selalu pixel‑perfect!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}