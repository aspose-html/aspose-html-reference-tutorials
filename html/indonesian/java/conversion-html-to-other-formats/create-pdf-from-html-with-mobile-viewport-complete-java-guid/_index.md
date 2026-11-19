---
category: general
date: 2026-03-18
description: Buat PDF dari HTML di Java dengan cepat. Pelajari cara mengonversi HTML
  ke PDF, mensimulasikan layar iPhone, dan mengatur ukuran layar untuk PDF responsif.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- simulate iphone screen
- how to set screen
- how to convert html
language: id
og_description: Buat PDF dari HTML di Java. Panduan ini menunjukkan cara mengonversi
  HTML ke PDF, mensimulasikan layar iPhone, dan mengatur dimensi layar untuk PDF responsif
  yang sempurna.
og_title: Buat PDF dari HTML dengan Viewport Seluler – Tutorial Java
tags:
- Java
- Aspose.HTML
- PDF
- Responsive Design
- Mobile Viewport
title: Buat PDF dari HTML dengan Mobile Viewport – Panduan Java Lengkap
url: /id/java/conversion-html-to-other-formats/create-pdf-from-html-with-mobile-viewport-complete-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF dari HTML dengan Mobile Viewport – Panduan Java Lengkap

Pernah perlu **create PDF from HTML** tetapi outputnya terlihat seperti halaman desktop pada layar ponsel yang kecil? Anda bukan satu-satunya. Saat Anda mengonversi situs web responsif ke PDF, viewport default sering mengabaikan breakpoint mobile, meninggalkan hasil yang sempit.  

Berita baiknya? Anda dapat **convert HTML to PDF** sambil **simulating an iPhone screen**, semuanya dengan kode Java biasa. Dalam tutorial ini kami akan membahas setiap langkah—cara mengatur ukuran layar, cara menyesuaikan device‑scale factor, dan mengapa pengaturan tersebut penting untuk PDF yang pixel‑perfect.

> **Pro tip:** Jika Anda sudah pernah menggunakan Aspose.HTML untuk konversi sederhana, Anda akan menemukan penyesuaian viewport hanya beberapa baris tambahan.

---

## Apa yang Akan Anda Pelajari

* Bagaimana cara **create PDF from HTML** menggunakan Aspose.HTML untuk Java.  
* Kode tepat untuk **simulate iPhone screen** dengan dimensi (375 × 667 px @ 2× density).  
* Di mana menempatkan opsi **how to set screen** dalam pipeline konversi.  
* Jebakan umum saat mengonversi halaman responsif dan cara menghindarinya.  
* Contoh Java lengkap, siap‑jalankan yang dapat Anda copy‑paste ke IDE.

### Prasyarat

* Java 17 atau lebih baru (kode dapat dikompilasi dengan versi lebih lama, tetapi 17 disarankan).  
* Aspose.HTML untuk Java – Anda dapat mengunduh JAR terbaru dari [Aspose website](https://products.aspose.com/html/java).  
* File HTML sederhana (`input.html`) yang ingin Anda ubah menjadi PDF.  
* Pemahaman dasar tentang Maven atau Gradle (kami akan menunjukkan contoh Maven).

## Langkah 1 – Tambahkan Aspose.HTML ke Proyek Anda

Pertama-tama, Anda memerlukan perpustakaan ini di classpath Anda. Jika Anda menggunakan Maven, tambahkan dependensi ini ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **Why this matters:** Aspose.HTML menangani pekerjaan berat—parsing HTML, menerapkan CSS, dan meraster layout. Tanpanya, Anda harus menulis mesin browser lengkap sendiri, yang merupakan *banyak* pekerjaan.

Jika Anda lebih suka Gradle, setaraannya adalah:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

---

## Langkah 2 – Siapkan Load Options dan Simulasikan Viewport iPhone

Sekarang kami akan mengonfigurasi parameter **how to set screen**. Kelas `HtmlLoadOptions` memungkinkan Anda memberi tahu Aspose ukuran dan kepadatan piksel yang harus dipalsukan oleh browser.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;

public class ViewportDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create load options for the HTML document
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();

        // 2️⃣ Simulate a mobile viewport (iPhone 6/7/8) – 375 × 667 pixels with retina density
        loadOptions.setScreenSize(new Size(375, 667));
        loadOptions.setDeviceScaleFactor(2.0);

        // 3️⃣ Convert the HTML file to PDF using the configured viewport
        Converter.convertDocument(
                "YOUR_DIRECTORY/input.html",          // source HTML
                "YOUR_DIRECTORY/output.pdf",          // destination PDF
                new PdfSaveOptions(),
                loadOptions);

        // 4️⃣ Notify that the conversion is complete
        System.out.println("Responsive conversion using mobile viewport.");
    }
}
```

### Mengapa Angka‑Angka Ini?

* **375 × 667** cocok dengan dimensi piksel CSS logis iPhone 6/7/8 dalam mode potret.  
* **DeviceScaleFactor = 2.0** memberi tahu renderer bahwa setiap piksel CSS berkorespondensi dengan dua piksel fisik, meniru tampilan Retina.  

Jika Anda memerlukan perangkat lain—misalnya iPhone 12 Pro Max—Anda dapat mengubah ukuran menjadi `428 × 926` dan mempertahankan scale factor pada `3.0`.

## Langkah 3 – Jalankan Konversi dan Verifikasi Output

Compile and run the class:

```bash
mvn compile exec:java -Dexec.mainClass=ViewportDemo
```

Setelah program selesai, buka `output.pdf`. Anda akan melihat:

* Semua media query yang menargetkan `max-width: 375px` diterapkan dengan benar.  
* Gambar dirender tajam berkat scale factor 2×.  
* Teks yang menghormati hierarki ukuran font mobile yang Anda definisikan di CSS.

Jika PDF masih terlihat seperti halaman desktop, periksa kembali bahwa HTML Anda menggunakan meta tag responsif:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Tanpa tag tersebut, bahkan pengaturan viewport yang sempurna tidak akan memicu stylesheet mobile.

## Langkah 4 – Menangani Sumber Daya Eksternal (Gambar, Font, CSS)

Saat Anda **convert HTML to PDF**, Aspose.HTML berusaha mengambil setiap sumber daya yang terhubung. Jika Anda mengonversi halaman yang berada di sistem file lokal, URL absolut (`file:///…`) berfungsi baik. Untuk aset remote Anda mungkin menemui:

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **404 errors for images** | HTML mengarah ke URL yang memerlukan autentikasi. | Gunakan `HtmlLoadOptions.setBaseUrl("file:///C:/myproject/")` untuk menyelesaikan path relatif, atau sematkan gambar sebagai Base64. |
| **Missing web fonts** | Mesin PDF tidak dapat mengunduh file font. | Unduh file `.woff`/`.ttf` secara lokal dan referensikan dengan path relatif. |
| **CSS not applied** | File CSS diblokir oleh CORS. | Host CSS pada server yang mengizinkan permintaan cross‑origin, atau inline CSS di dalam HTML. |

Cara cepat untuk menguji pemuatan sumber daya adalah membungkus pemanggilan konversi dalam blok try‑catch dan mencetak pesan `Exception`. Aspose.HTML menyediakan log detail yang menunjukkan URL tepat yang gagal.

```java
try {
    Converter.convertDocument(...);
} catch (Exception ex) {
    System.err.println("Conversion failed: " + ex.getMessage());
}
```

## Langkah 5 – Penyesuaian Lanjutan (Opsional)

### a) Ubah Ukuran Halaman PDF

Secara default Aspose.HTML membuat halaman PDF yang sesuai dengan ukuran viewport. Jika Anda menginginkan A4 atau Letter, tambahkan konfigurasi `PdfSaveOptions`:

```java
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setPageSize(PageSize.A4);
Converter.convertDocument("input.html", "output.pdf", pdfOptions, loadOptions);
```

### b) Tambahkan Header/Footer secara Programatis

Anda dapat menyisipkan header/footer sederhana setelah konversi menggunakan Aspose.PDF (perpustakaan terpisah). Alur kerjanya:

1. Konversi HTML → PDF (seperti ditunjukkan).  
2. Buka PDF yang dihasilkan dengan Aspose.PDF.  
3. Tambahkan objek `HeaderFooter` ke setiap halaman.

```java
import com.aspose.pdf.*;

Document pdfDoc = new Document("output.pdf");
for (Page page : pdfDoc.getPages()) {
    page.addHeaderFooter(new HeaderFooter("Generated on " + LocalDate.now()));
}
pdfDoc.save("output-with-header.pdf");
```

### c) Konversi Batch

Jika Anda memiliki folder berisi file HTML, lakukan loop pada mereka:

```java
Files.list(Paths.get("html_folder"))
     .filter(p -> p.toString().endsWith(".html"))
     .forEach(p -> {
         String pdfPath = p.toString().replace(".html", ".pdf");
         Converter.convertDocument(p.toString(), pdfPath, new PdfSaveOptions(), loadOptions);
     });
```

## Pertanyaan yang Sering Diajukan (FAQs)

**Q: Apakah ini bekerja dengan halaman yang berat JavaScript?**  
A: Aspose.HTML mendukung subset JavaScript. Manipulasi DOM sederhana dan perubahan CSS biasanya berfungsi, tetapi kerangka kerja kompleks (React, Angular) mungkin memerlukan snapshot HTML statis yang telah diprerender.

**Q: Bagaimana jika saya perlu mengonversi halaman yang menggunakan aturan `@media print`?**  
A: Perpustakaan secara otomatis menghormati `@media print`. Namun, jika Anda juga mengatur viewport mobile, stylesheet `print` dapat menimpa beberapa gaya mobile. Uji kedua skenario.

**Q: Bisakah saya mengatur DPI khusus untuk PDF?**  
A: Ya. Gunakan `PdfSaveOptions.setDpi(300)` sebelum konversi. DPI yang lebih tinggi menghasilkan file lebih besar tetapi gambar lebih tajam.

## Screenshot Hasil yang Diharapkan

Berikut ilustrasi halaman PDF akhir (viewport mobile disimulasikan).  
![Tangkapan layar PDF yang dihasilkan oleh demo create pdf from html menampilkan tata letak berukuran iPhone]  

*Teks alt gambar mencakup kata kunci utama untuk SEO.*

## Kesimpulan

Anda kini memiliki alur kerja **create pdf from html** yang solid, menghormati breakpoint mobile, mensimulasikan layar iPhone, dan memberi Anda kontrol penuh atas dimensi halaman. Dengan menyesuaikan `HtmlLoadOptions` Anda dapat menjawab “**how to set screen**” untuk perangkat apa pun, dan dengan menggunakan `Converter.convertDocument` Anda telah menguasai **how to convert html** dalam Java.

Siap untuk tantangan berikutnya? Cobalah menggabungkan pendekatan ini dengan Aspose.PDF untuk menambahkan watermark, menggabungkan beberapa PDF, atau melindungi dokumen dengan kata sandi. Dan jangan lupa bereksperimen dengan perangkat lain—cukup ubah nilai `Size` dan `DeviceScaleFactor` agar sesuai dengan kepadatan piksel yang Anda butuhkan.

Selamat coding, semoga PDF Anda selalu tampak tajam di kertas seperti di layar ponsel!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}