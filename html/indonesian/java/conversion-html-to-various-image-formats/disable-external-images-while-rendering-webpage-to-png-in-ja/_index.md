---
category: general
date: 2026-05-31
description: Nonaktifkan gambar eksternal saat Anda merender halaman web ke PNG di
  Java menggunakan Aspose HTML. Pelajari cara memuat halaman web di sandbox dengan
  aman dan menyimpan dokumen HTML sebagai PNG.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: id
og_description: Nonaktifkan gambar eksternal saat merender halaman web menjadi PNG
  di Java. Panduan langkah demi langkah ini menunjukkan cara memuat halaman web dalam
  sandbox dan menyimpan dokumen HTML sebagai PNG.
og_title: Menonaktifkan Gambar Eksternal Saat Merender Halaman Web ke PNG di Java
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: Nonaktifkan Gambar Eksternal Saat Merender Halaman Web ke PNG di Java
url: /id/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nonaktifkan Gambar Eksternal Saat Merender Halaman Web ke PNG dalam Java

Pernah perlu **menonaktifkan gambar eksternal** saat Anda merender halaman web ke PNG dalam Java? Mungkin Anda sedang membangun layanan thumbnail yang harus tetap terisolasi dari internet publik, atau Anda hanya ingin memastikan tidak ada gambar pihak ketiga yang bocor selama konversi. Bagaimanapun, Anda berada di tempat yang tepat.

Dalam tutorial ini kami akan membahas cara memuat halaman web dalam sandbox, mematikan pengambilan gambar eksternal, dan akhirnya menyimpan dokumen HTML sebagai file PNG—semua dengan Aspose.HTML untuk Java. Pada akhir tutorial Anda akan memiliki contoh yang siap dijalankan, serta beberapa tips praktis untuk menghindari jebakan umum.

## Apa yang Akan Anda Pelajari

- **Cara merender HTML ke gambar Java** menggunakan `Converter` Aspose.HTML.
- Langkah‑langkah tepat untuk **memuat halaman web dalam sandbox** dengan viewport dan DPI khusus.
- Konfigurasi yang diperlukan untuk **menonaktifkan gambar eksternal** sambil tetap merender halaman.
- Cara **menyimpan dokumen HTML sebagai PNG** (atau format lain yang didukung) ke disk.
- Penanganan kasus tepi, petunjuk kinerja, dan saran pemecahan masalah.

### Prasyarat

- Java 8 atau lebih baru terpasang (kode ini juga bekerja dengan JDK 11+).
- Maven atau Gradle untuk mengambil pustaka Aspose.HTML for Java.
- Familiaritas dasar dengan sintaks Java dan penanganan pengecualian.
- Koneksi internet untuk pemuatan halaman awal (kecuali Anda menyajikan HTML secara lokal).

> **Pro tip:** Jika Anda bekerja di belakang proxy perusahaan, atur properti JVM `http.proxyHost` dan `http.proxyPort` sebelum menjalankan contoh.

---

## Langkah 1: Siapkan Proyek Anda dan Tambahkan Aspose.HTML

Pertama-tama—tambahkan dependensi Aspose.HTML. Jika Anda menggunakan Maven, letakkan ini ke dalam `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Untuk Gradle, setaraannya adalah:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Setelah pustaka berada di classpath, Anda siap mulai menulis kode.

---

## Langkah 2: **Nonaktifkan Gambar Eksternal** dengan Lingkungan Sandbox

Inti solusi terletak pada `DocumentSandbox`. Dengan memberikan nilai `false` untuk flag *allowExternalImages*, kami memberi tahu Aspose.HTML untuk mengabaikan semua tag `<img>` yang mengarah ke URL di luar sandbox. Inilah mekanisme tepat yang **menonaktifkan gambar eksternal**.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **Mengapa ini penting:** Tanpa sandbox, renderer akan mencoba mengunduh setiap gambar yang direferensikan oleh halaman, yang dapat menjadi lambat, tidak dapat diandalkan, atau bahkan menjadi risiko keamanan. Menetapkan flag ke `false` menjamin proses rendering yang bersih dan mandiri.

---

## Langkah 3: **Muat Halaman Web dalam Sandbox**  

Sekarang kami mengarahkan Aspose.HTML ke URL yang ingin kami tangkap. Konstruktor `HTMLDocument` menerima instance sandbox, secara otomatis menerapkan pembatasan yang baru saja kami definisikan.

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

Jika halaman sangat bergantung pada skrip eksternal untuk tata letak, Anda mungkin melihat konten yang hilang karena kami juga menonaktifkan skrip. Dalam kasus itu, ubah flag `allowExternalScripts` menjadi `true` sambil tetap menjaga `allowExternalImages` tetap `false`.

---

## Langkah 4: **Render Halaman Web ke PNG**  

Dengan dokumen sudah dimuat, mengonversinya menjadi gambar cukup satu baris kode menggunakan `Converter.convert`. Objek `ImageSaveOptions` memungkinkan Anda memilih format output; di sini kami memilih PNG.

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

File yang dihasilkan, `sandboxed.png`, berisi snapshot halaman **tanpa gambar eksternal**—hanya SVG inline atau grafik yang di‑encode base64 yang tetap ada, jika ada.

---

## Langkah 5: Verifikasi Output dan Debug Masalah Umum

Setelah menjalankan program, buka `sandboxed.png` dengan penampil gambar apa pun. Anda harus melihat tata letak halaman, teks, dan styling CSS, tetapi semua elemen `<img src="http://…">` akan kosong (sering kali dirender sebagai persegi putih atau dihilangkan sepenuhnya).

### Masalah Umum dan Cara Memperbaikinya

| Gejala | Penyebab kemungkinan | Perbaikan |
|---|---|---|
| Halaman kosong | URL target memblokir permintaan (misalnya Cloudflare) | Tambahkan header yang tepat ke user‑agent sandbox atau gunakan proxy. |
| Font tidak ditemukan | File font disimpan secara eksternal | Instal font secara lokal atau sematkan sebagai `@font-face` dengan data URI. |
| Perubahan tata letak | CSS merujuk ke stylesheet eksternal yang diblokir | Atur `allowExternalScripts` ke `true` *hanya* untuk pemuatan CSS, lalu jalankan kembali. |
| `java.lang.OutOfMemoryError` | Merender halaman sangat besar dengan DPI tinggi | Kurangi ukuran viewport atau DPI, atau tingkatkan heap JVM (`-Xmx2g`). |

---

## Langkah 6: Memperluas Contoh – Simpan dalam Format Lain

Kode yang sama bekerja untuk JPEG, BMP, atau bahkan PDF. Cukup ubah enum `SaveFormat`:

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

Jika Anda memerlukan PDF, gantilah `ImageSaveOptions` dengan `PdfSaveOptions` dan sesuaikan ekstensi file yang dihasilkan.

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah **program lengkap yang dapat dijalankan**. Buat kelas Java baru, tempelkan kode, pastikan direktori `output` ada, lalu jalankan.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**Output yang diharapkan** (console):

```
PNG image saved to: output/sandboxed.png
```

Buka `sandboxed.png` – Anda akan melihat halaman dirender **tanpa gambar eksternal**.

---

## Pertanyaan yang Sering Diajukan

**Q: Apakah saya masih dapat menampilkan gambar yang dibundel di dalam HTML?**  
A: Ya. URI `data:` inline atau gambar yang di‑encode base64 dianggap bagian dari dokumen dan akan muncul di PNG.

**Q: Bagaimana jika saya perlu mempertahankan beberapa gambar eksternal tetapi memblokir yang lain?**  
A: Sandbox berfungsi sebagai saklar semua‑atau‑tidak sama sekali. Untuk kontrol yang lebih halus, unduh gambar yang diizinkan secara manual, sematkan sebagai data URI, lalu render.

**Q: Apakah pendekatan ini bekerja di server tanpa tampilan (headless)?**  
A: Tentu saja. Aspose.HTML adalah pustaka murni Java; tidak memerlukan server tampilan atau mesin browser.

**Q: Bagaimana ini berbeda dari menggunakan Selenium atau Puppeteer?**  
A: Selenium mengendalikan browser nyata, yang berat dan lebih sulit disandbox. Aspose.HTML merender HTML langsung di memori, memberikan kinerja yang deterministik dan kontrol keamanan yang lebih mudah seperti **menonaktifkan gambar eksternal**.

---

## Kesimpulan

Anda kini memiliki resep lengkap, ujung‑ke‑ujung untuk **menonaktifkan gambar eksternal saat merender halaman web ke PNG dalam Java**. Dengan memanfaatkan `DocumentSandbox`, Anda memperoleh kontrol ketat atas sumber daya eksternal yang diizinkan, memastikan keamanan dan reproduktifitas. Dari sini Anda dapat bereksperimen dengan ukuran viewport berbeda, pengaturan DPI, atau format output—setiap penyesuaian membuka peluang baru untuk menghasilkan thumbnail, pratinjau, atau snapshot arsip.

Siap untuk tantangan berikutnya? Cobalah merender batch URL secara paralel, atau integrasikan logika ini ke dalam microservice Spring Boot yang mengembalikan PNG sesuai permintaan. Langit adalah batasnya ketika Anda menggabungkan fleksibilitas Aspose.HTML dengan alat konkuren Java.

Selamat coding, dan jangan lupa bagikan kisah sukses Anda di kolom komentar!

## Apa yang Harus Anda Pelajari Selanjutnya?

- [Cara Menggunakan Aspose untuk Merender HTML ke PNG – Panduan Langkah‑per‑Langkah](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [Cara Merender HTML ke PNG dengan Aspose – Panduan Lengkap](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [Cara Mengedit CSS - Pengeditan CSS Eksternal Lanjutan dengan Aspose.HTML untuk Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}