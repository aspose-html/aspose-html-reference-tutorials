---
category: general
date: 2026-06-29
description: Pelajari cara mengatur DPI dan resolusi gambar saat mengonversi HTML
  ke PNG dengan Aspose HTML Converter. Contoh Java langkah demi langkah disertakan.
draft: false
keywords:
- how to set dpi
- convert html to png
- set image resolution
- convert html page
- aspose html converter
language: id
og_description: Cara mengatur DPI dalam konversi HTML Aspose. Panduan ini menunjukkan
  cara mengonversi halaman HTML menjadi gambar PNG beresolusi tinggi di Java.
og_title: Cara Mengatur DPI Saat Mengonversi HTML ke PNG – Tutorial HTML Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Learn how to set DPI and image resolution while converting HTML to
    PNG with Aspose HTML Converter. Step‑by‑step Java example included.
  headline: How to Set DPI When Converting HTML to PNG – Complete Aspose HTML Guide
  type: TechArticle
- description: Learn how to set DPI and image resolution while converting HTML to
    PNG with Aspose HTML Converter. Step‑by‑step Java example included.
  name: How to Set DPI When Converting HTML to PNG – Complete Aspose HTML Guide
  steps:
  - name: 1. Different Output Formats
    text: Aspose.HTML isn’t limited to PNG. Swap the file extension and use a matching
      options class, e.g., `JpegConversionOptions` for JPEGs. The DPI logic stays
      identical.
  - name: 2. Dynamically Determining Screen Size
    text: 'If you need the sandbox to mimic a mobile device, read the dimensions from
      a config file:'
  - name: 3. Batch Conversion
    text: Wrap the conversion call inside a loop that iterates over a directory of
      HTML files. Remember to reuse the same `Sandbox` and `ImageConversionOptions`
      objects to avoid unnecessary allocations.
  type: HowTo
tags:
- Java
- Aspose.HTML
- Image Processing
title: Cara Mengatur DPI Saat Mengonversi HTML ke PNG – Panduan Lengkap Aspose HTML
url: /id/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-html-to-png-complete-aspose-h/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengatur DPI Saat Mengonversi HTML ke PNG – Panduan Lengkap Aspose HTML

Pernah bertanya-tanya **bagaimana cara mengatur DPI** untuk PNG yang Anda hasilkan dari halaman HTML? Dalam banyak skenario pelaporan atau otomatisasi screenshot, DPI default 96 dpi tidak cukup tajam. Kabar baiknya, Aspose.HTML for Java memberi Anda kontrol penuh atas simulasi layar dan resolusi gambar, sehingga Anda dapat meningkatkan DPI hingga 300 atau bahkan 600 hanya dengan beberapa baris kode.

Di tutorial ini kami akan membahas contoh Java dunia nyata yang **mengonversi halaman HTML ke PNG** sambil secara eksplisit **mengatur DPI** dan **resolusi gambar**. Pada akhir tutorial Anda akan memiliki kelas yang siap dijalankan, memahami mengapa setiap pengaturan penting, dan tahu cara menyesuaikannya untuk berbagai kasus penggunaan seperti cetakan beresolusi tinggi atau thumbnail web.

> **Pratinjau cepat:** Langkah inti adalah (1) membuat `Sandbox` yang meniru layar, (2) mengatur DPI-nya, (3) mengonfigurasi `ImageConversionOptions` dengan resolusi yang diinginkan, dan (4) memanggil `Converter.convert`. Tanpa alat eksternal, tanpa trik baris perintah—hanya Java murni.

## Prasyarat

- **Java 17** (atau JDK terbaru) yang terpasang dan dikonfigurasi di IDE Anda.
- **Aspose.HTML for Java** library (artifact Maven `com.aspose:aspose-html`). Anda dapat mengambil versi terbaru dari [Aspose Maven repository](https://repo.aspose.com/repo) atau mengunduh JAR secara langsung.
- File HTML sederhana (`page.html`) yang ingin Anda ubah menjadi PNG. Letakkan di lokasi yang dapat dijangkau, misalnya `C:/temp/page.html`.
- Familiaritas dasar dengan penanganan exception di Java—tidak ada yang rumit.

Jika ada yang belum familiar, jeda sejenak dan instal komponen yang belum ada. Sisanya panduan mengasumsikan Anda nyaman membuka proyek Java dan menambahkan JAR eksternal.

## Langkah 1: Siapkan Proyek Maven Anda (atau Tambahkan JAR Secara Manual)

Jika Anda menggunakan Maven, tambahkan dependensi ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.11</version> <!-- Check for the newest version -->
</dependency>
```

Jika tidak, letakkan `aspose-html-*.jar` ke folder `libs` proyek Anda dan tambahkan ke build path. Langkah ini tidak secara langsung tentang **cara mengatur DPI**, tetapi tanpa library Anda tidak dapat mengakses kelas `Sandbox` yang memungkinkan kontrol DPI.

## Langkah 2: Buat Sandbox yang Mensimulasikan Layar Nyata

*Sandbox* adalah cara Aspose mereproduksi lingkungan peramban. Anggaplah sebagai monitor virtual di mana Anda menentukan lebar, tinggi, dan yang paling penting **DPI**. Berikut cuplikan kode yang membuat layar 1024 × 768 dengan 96 dpi—hanya baseline sebelum kami meningkatkan resolusi:

```java
// Step 2.1: Initialise the sandbox
Sandbox sandbox = new Sandbox();

// Step 2.2: Define virtual screen dimensions (pixels)
sandbox.setScreenWidth(1024);
sandbox.setScreenHeight(768);

// Step 2.3: Set the DPI – this is the key to controlling image sharpness
sandbox.setDpi(96); // Change this value to 300, 600, etc., later
```

> **Mengapa sandbox?** Tanpa itu, Aspose akan kembali ke pengaturan layar mesin host, menghasilkan hasil yang tidak konsisten di antara mesin pengembangan. Dengan mengunci DPI, Anda menjamin setiap konversi terlihat sama, baik dijalankan di laptop maupun server CI.

## Langkah 3: Konfigurasikan Opsi Konversi Gambar – Atur Resolusi Gambar

Sekarang sandbox siap, kami memberi tahu konverter resolusi **gambar** yang diinginkan. Kelas `ImageConversionOptions` memungkinkan Anda mengatur DPI PNG output secara terpisah dari DPI sandbox, memberi Anda dua tuas untuk diatur.

```java
// Step 3.1: Prepare conversion options
ImageConversionOptions conversionOptions = new ImageConversionOptions();

// Step 3.2: Desired output DPI – this directly influences PNG quality
conversionOptions.setResolution(300); // 300 dpi is print‑quality; increase for sharper prints

// Step 3.3: Bind the sandbox to the options so the layout engine respects our virtual screen
conversionOptions.setSandbox(sandbox);
```

**Tip:** Jika Anda menginginkan PNG 600 dpi untuk brosur berkualitas tinggi, cukup ubah `setResolution(300)` menjadi `setResolution(600)`. Ingat bahwa nilai DPI yang lebih besar meningkatkan konsumsi memori dan waktu pemrosesan, jadi uji dulu dengan halaman kecil.

## Langkah 4: Konversi Halaman HTML ke PNG

Dengan sandbox dan opsi yang sudah disiapkan, langkah **convert html to png** sebenarnya hanya satu baris:

```java
// Step 4: Perform the conversion
Converter.convert(
        "C:/temp/page.html",   // Source HTML file (convert html page)
        "C:/temp/page.png",    // Destination PNG file
        conversionOptions);    // Options that include DPI and sandbox
```

Jika semuanya berjalan lancar, Anda akan melihat pesan konsol pada langkah berikutnya.

## Langkah 5: Verifikasi Hasil dan Cetak Konfirmasi

`System.out.println` singkat memberi tahu Anda bahwa pekerjaan selesai. Pada proyek nyata Anda mungkin ingin memeriksa ukuran file, dimensi, atau bahkan membuka PNG secara programatik untuk memvalidasi DPI.

```java
System.out.println("PNG generated with sandboxed layout at 300 dpi.");
```

Menjalankan kelas akan membuat `page.png` di folder yang sama dengan file HTML Anda. Buka dengan penampil gambar yang menampilkan DPI (mis., Windows Photo Viewer → Properties → Details) dan pastikan tertulis **300 dpi**.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut kelas Java mandiri yang dapat Anda salin‑tempel ke IDE:

```java
import com.aspose.html.conversions.Converter;
import com.aspose.html.conversions.options.ImageConversionOptions;
import com.aspose.html.sandbox.Sandbox;

public class HtmlToPngWithSandbox {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox that simulates a 1024×768 screen with 96 dpi.
        Sandbox sandbox = new Sandbox();
        sandbox.setScreenWidth(1024);
        sandbox.setScreenHeight(768);
        sandbox.setDpi(96); // <-- This is where you learn how to set dpi

        // Step 2: Configure image conversion options – 300 dpi PNG using the sandbox.
        ImageConversionOptions conversionOptions = new ImageConversionOptions();
        conversionOptions.setResolution(300); // Set image resolution (dpi)
        conversionOptions.setSandbox(sandbox);

        // Step 3: Convert the HTML page to a PNG image using the defined options.
        Converter.convert(
                "C:/temp/page.html",   // convert html page
                "C:/temp/page.png",    // output PNG
                conversionOptions);    // includes dpi and resolution settings

        // Step 4: Indicate that the conversion has completed.
        System.out.println("PNG generated with sandboxed layout at 300 dpi.");
    }
}
```

> **Ingat:** Baris `sandbox.setDpi(96);` adalah bagian *cara mengatur dpi*. Sesuaikan dengan kepadatan layar yang Anda butuhkan; `conversionOptions.setResolution(300);` mengontrol DPI akhir gambar.

## Menangani Kendala Umum

| Situasi | Hal yang Perlu Diperhatikan | Solusi yang Disarankan |
|-----------|-------------------|---------------|
| **Out‑of‑Memory errors** saat menggunakan 600 dpi | DPI tinggi secara dramatis meningkatkan ukuran raster (mis., 1024 × 768 @ 600 dpi ≈ 4 MP). | Kurangi dimensi layar, atau alirkan konversi menggunakan callback `ConversionProgress`. |
| **HTML menggunakan CSS/JS eksternal yang tidak dimuat** | Sandbox berjalan secara terisolasi; sumber daya remote harus dapat dijangkau. | Berikan URL absolut atau sematkan CSS langsung dalam HTML. |
| **DPI tidak tepat pada output** | Anda mengubah `sandbox.setDpi` tetapi lupa menyesuaikan `conversionOptions.setResolution`. | Pastikan kedua nilai selaras dengan output target Anda. |
| **FileNotFoundException** | Kesalahan penulisan path atau izin file yang hilang. | Gunakan `Paths.get(...).toAbsolutePath()` dan verifikasi hak baca/tulis. |

## Variasi Lanjutan

### 1. Format Output Berbeda

Aspose.HTML tidak terbatas pada PNG. Ganti ekstensi file dan gunakan kelas opsi yang sesuai, mis., `JpegConversionOptions` untuk JPEG. Logika DPI tetap sama.

```java
import com.aspose.html.conversions.options.JpegConversionOptions;

// ...

JpegConversionOptions jpegOpts = new JpegConversionOptions();
jpegOpts.setResolution(300);
jpegOpts.setSandbox(sandbox);

Converter.convert("page.html", "page.jpg", jpegOpts);
```

### 2. Menentukan Ukuran Layar Secara Dinamis

Jika Anda perlu sandbox meniru perangkat seluler, baca dimensi dari file konfigurasi:

```java
sandbox.setScreenWidth(Integer.parseInt(System.getProperty("screen.width", "375")));
sandbox.setScreenHeight(Integer.parseInt(System.getProperty("screen.height", "667")));
sandbox.setDpi(Integer.parseInt(System.getProperty("screen.dpi", "96")));
```

Jalankan dengan `-Dscreen.width=375 -Dscreen.height=667 -Dscreen.dpi=326` untuk meniru tampilan iPhone Retina.

### 3. Konversi Batch

Balut pemanggilan konversi dalam loop yang mengiterasi direktori file HTML. Ingat untuk menggunakan kembali objek `Sandbox` dan `ImageConversionOptions` yang sama agar tidak membuat alokasi yang tidak perlu.

```java
Files.list(Paths.get("C:/temp/html"))
     .filter(p -> p.toString().endsWith(".html"))
     .forEach(htmlPath -> {
         String pngPath = htmlPath.toString().replace(".html", ".png");
         Converter.convert(htmlPath.toString(), pngPath, conversionOptions);
     });
```

## Output yang Diharapkan

Menjalankan kelas dengan pengaturan default menghasilkan file PNG kira‑kira **1024 × 768 pixel** pada **300 dpi**. Di kebanyakan editor gambar, dimensi akan muncul sebagai 1024 × 768, sementara metadata DPI menunjukkan 300. Jika Anda mencetak gambar dengan lebar 1 inci, Anda akan mendapatkan garis 300 pixel yang tajam—sempurna untuk flyer berkualitas tinggi.

## Ringkasan Visual

![cara mengatur dpi dalam konversi Aspose HTML](/images/aspose-dpi-example.png "cara mengatur dpi – contoh sandbox Aspose HTML")

*Tangkapan layar menunjukkan metadata DPI PNG yang dihasilkan (300 dpi).*

## Kesimpulan

Kami telah membahas **cara mengatur DPI** saat Anda **mengonversi HTML ke PNG** menggunakan **Aspose HTML Converter** di Java. Dengan membuat sandbox, mengonfigurasi `ImageConversionOptions`, dan memanggil `Converter.convert`, Anda memperoleh kontrol pixel‑perfect atas simulasi layar dan resolusi gambar akhir. Baik Anda menghasilkan faktur yang dapat dicetak, aset web beresolusi tinggi, atau thumbnail otomatis, pola yang sama berlaku—cukup sesuaikan DPI dan ukuran layar sesuai kebutuhan Anda

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menggunakan Aspose untuk Merender HTML ke PNG – Panduan Langkah‑per‑Langkah](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [Cara Mengonversi HTML ke JPEG Menggunakan Aspose.HTML untuk Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)
- [Cara Mengonversi HTML ke BMP dengan Aspose.HTML untuk Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-bmp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}