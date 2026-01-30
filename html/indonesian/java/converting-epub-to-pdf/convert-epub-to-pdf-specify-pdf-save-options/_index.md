---
date: 2026-01-02
description: Pelajari cara mengonversi EPUB ke PDF dalam Java dengan Aspose.HTML sambil
  mengatur ukuran halaman PDF khusus dan opsi penyimpanan PDF lainnya.
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 'Ukuran Halaman PDF Kustom: Menentukan Opsi Penyimpanan PDF untuk EPUB ke PDF'
url: /id/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ukuran Halaman PDF Kustom: Menentukan Opsi Penyimpanan PDF untuk EPUB ke PDF

## Pendahuluan

Aspose.HTML for Java memudahkan **konversi EPUB ke PDF** dan memberi Anda kontrol penuh atas output, termasuk mengatur **ukuran halaman PDF kustom**. Dalam panduan langkah‑demi‑langkah ini kami akan membahas semua yang Anda perlukan—dari menyiapkan lingkungan hingga menyesuaikan `PdfSaveOptions` sehingga PDF yang dihasilkan memiliki dimensi halaman yang tepat sesuai kebutuhan Anda. Baik Anda membangun pipeline penerbitan, platform e‑learning, atau sekadar mengotomatisasi konversi dokumen, teknik‑teknik di sini akan sangat berguna.

## Jawaban Cepat
- **Apa tujuan utama tutorial ini?** Mengonversi file EPUB ke PDF sambil menerapkan ukuran halaman PDF kustom.  
- **Perpustakaan apa yang digunakan?** Aspose.HTML for Java.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis tersedia; lisensi komersial diperlukan untuk produksi.  
- **Bisakah saya mengubah warna latar belakang?** Ya, menggunakan `PdfSaveOptions`.  
- **Apakah Java 8+ didukung?** Tentu saja—semua runtime Java modern dapat digunakan.

## Apa itu ukuran halaman PDF kustom?

Ukuran halaman PDF kustom memungkinkan Anda menentukan lebar dan tinggi tepat setiap halaman dalam PDF output, alih‑alih mengandalkan ukuran standar seperti A4 atau Letter. Ini sangat berguna untuk e‑book, selebaran, atau skenario apa pun di mana tata letak visual harus cocok dengan desain tertentu.

## Mengapa menggunakan Aspose.HTML untuk konversi EPUB ke PDF?

- **Fidelity tinggi:** Mempertahankan tata letak kompleks, font, dan gambar.  
- **Kontrol detail:** Mengatur ukuran halaman, latar belakang, margin, dan lainnya melalui `PdfSaveOptions`.  
- **Cross‑platform:** Berfungsi di Windows, Linux, dan macOS dengan kode Java yang sama.  
- **Performa:** Mesin rendering yang dioptimalkan untuk konversi cepat.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

- **Lingkungan Pengembangan Java:** JDK 8 atau yang lebih baru terpasang dan terkonfigurasi.  
- **Aspose.HTML for Java:** Unduh JAR terbaru dari [situs web](https://releases.aspose.com/html/java/).  
- **File EPUB:** Dokumen `.epub` yang ingin Anda konversi.  

Setelah semua siap, mari kita masuk ke langkah‑langkah konversi yang sebenarnya.

## Langkah 1: Buka File EPUB

Pertama, kita perlu membuka file EPUB menggunakan `FileInputStream`. Stream ini akan diteruskan ke konverter nanti.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## Langkah 2: Tentukan Opsi Penyimpanan PDF

Di sinilah kita mengatur **ukuran halaman PDF kustom** dan warna latar belakang opsional. Sesuaikan nilai piksel agar cocok dengan dimensi yang Anda inginkan.

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

### Tips profesional:
- **Pixel vs. Point:** `Length.fromPixels` mengonversi piksel layar ke poin PDF (1 poin = 1/72 inci). Pilih nilai yang mencerminkan ukuran cetak akhir yang Anda butuhkan.

## Langkah 3: Konversi EPUB ke PDF

Dengan stream input dan opsi kustom siap, panggil konverter. PDF output akan disimpan ke lokasi yang Anda tentukan.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## Kode Sumber Lengkap

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## Masalah Umum dan Solusinya

| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| **Halaman PDF kosong** | Stream input ditutup sebelum konversi | Pertahankan blok `try‑with‑resources` tetap terbuka hingga setelah `convertEPUB`. |
| **Dimensi halaman tidak tepat** | Menggunakan piksel yang tidak sesuai dengan ukuran cetak yang diinginkan | Konversikan ukuran inci yang diinginkan ke poin (`1 inch = 72 points`) lalu ke piksel menggunakan `Length.fromPixels`. |
| **Font hilang** | Font tidak ter-embed dalam EPUB | Pastikan font dipaketkan di dalam EPUB atau instal font tersebut di mesin host. |

## Pertanyaan yang Sering Diajukan (FAQ)

### Apakah Aspose.HTML for Java merupakan perpustakaan gratis?
Aspose.HTML for Java adalah perpustakaan komersial, tetapi Anda dapat memperoleh versi percobaan gratis dari [situs web](https://releases.aspose.com/).

### Format EPUB apa saja yang didukung untuk konversi?
Aspose.HTML for Java mendukung konversi berbagai format EPUB, memastikan kompatibilitas dengan sebagian besar dokumen EPUB.

### Bisakah saya menyesuaikan output PDF lebih lanjut?
Ya, Anda dapat menyesuaikan output PDF dengan mengatur pengaturan halaman, warna latar belakang, dan pengaturan lain dalam `PdfSaveOptions`.

### Apakah ada batasan pada versi percobaan Aspose.HTML for Java?
Versi percobaan mungkin memiliki beberapa batasan, jadi disarankan untuk memeriksa dokumentasi untuk detailnya.

### Di mana saya dapat mendapatkan dukungan untuk Aspose.HTML for Java?
Anda dapat menemukan jawaban atas pertanyaan Anda dan mencari dukungan di [forum Aspose.HTML](https://forum.aspose.com/).

---

**Terakhir Diperbarui:** 2026-01-02  
**Diuji Dengan:** Aspose.HTML for Java 24.11 (terbaru pada saat penulisan)  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}