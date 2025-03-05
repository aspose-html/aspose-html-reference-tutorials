---
title: Menentukan Opsi Penyimpanan PDF untuk EPUB ke PDF
linktitle: Menentukan Opsi Penyimpanan PDF untuk EPUB ke PDF
second_title: Pemrosesan HTML Java dengan Aspose.HTML
description: Pelajari cara mengonversi EPUB ke PDF di Java menggunakan Aspose.HTML, pustaka manipulasi HTML yang canggih.
type: docs
weight: 12
url: /id/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
---

## Perkenalan

Aspose.HTML untuk Java adalah alat yang hebat untuk bekerja dengan dokumen HTML dan EPUB. Dalam panduan langkah demi langkah ini, kami akan memandu Anda melalui proses mengonversi file EPUB ke PDF menggunakan Aspose.HTML untuk Java. Apakah Anda seorang pengembang berpengalaman atau baru memulai, tutorial ini akan memberi Anda pengetahuan dan keterampilan yang diperlukan untuk melakukan tugas ini secara efisien.

## Prasyarat

Sebelum kita memulai, pastikan Anda memiliki prasyarat berikut:

- Lingkungan Pengembangan Java: Anda harus menyiapkan lingkungan pengembangan Java di sistem Anda.

-  Aspose.HTML untuk Java: Unduh dan instal pustaka Aspose.HTML untuk Java. Anda dapat menemukan pustaka dan dokumentasi terkait di[situs web](https://releases.aspose.com/html/java/).

- Berkas EPUB: Anda memerlukan berkas EPUB yang ingin diubah ke PDF.

Sekarang, mari selami panduan langkah demi langkah untuk mengonversi EPUB ke PDF menggunakan Aspose.HTML untuk Java.

## Langkah 1: Buka File EPUB

 Untuk memulai, buka file EPUB yang sudah ada untuk dibaca. Anda dapat menggunakan`FileInputStream` untuk mencapai hal ini. Berikut kode untuk langkah ini:

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Kode Anda untuk langkah berikutnya akan diletakkan di sini.
}
```

## Langkah 2: Tentukan Opsi Penyimpanan PDF

 Buat contoh dari`PdfSaveOptions` dengan ukuran halaman dan warna latar belakang yang dapat disesuaikan. Anda dapat mengonfigurasi pengaturan halaman sesuai dengan kebutuhan Anda. Berikut cara melakukannya:

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

## Langkah 3: Konversi EPUB ke PDF

 Sekarang, hubungi`ConvertEPUB` metode untuk mengonversi file EPUB ke PDF. Tentukan aliran input, opsi penyimpanan PDF, dan lokasi output. Berikut cara melakukannya:

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

Selamat! Anda telah berhasil mengonversi file EPUB ke PDF menggunakan Aspose.HTML untuk Java. Anda sekarang dapat mengakses file PDF yang dikonversi di lokasi keluaran yang ditentukan.

## Kode Sumber Lengkap
```java
Specifying PDF Save Options for EPUB to PDF
        // Buka berkas EPUB yang ada untuk dibaca.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Buat contoh PdfSaveOptions dengan ukuran halaman dan warna latar belakang khusus.
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
            // Panggil metode ConvertEPUB untuk mengonversi EPUB ke PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```


## Kesimpulan

Dalam tutorial ini, kita telah mempelajari cara menggunakan Aspose.HTML untuk Java guna mengonversi file EPUB ke format PDF. Pustaka serbaguna ini menyediakan alat yang hebat bagi pengembang untuk memanipulasi dokumen. Dengan mengikuti langkah-langkah yang diuraikan dalam panduan ini, Anda dapat mengintegrasikan konversi EPUB ke PDF ke dalam aplikasi Java Anda dengan lancar.

## Pertanyaan yang Sering Diajukan (FAQ)

### Apakah Aspose.HTML untuk Java merupakan pustaka gratis?
 Aspose.HTML untuk Java adalah pustaka komersial, tetapi Anda bisa mendapatkan versi uji coba gratis dari mereka[situs web](https://releases.aspose.com/).

### Format EPUB apa yang didukung untuk konversi?
Aspose.HTML untuk Java mendukung konversi berbagai format EPUB, memastikan kompatibilitas dengan sebagian besar dokumen EPUB.

### Bisakah saya menyesuaikan keluaran PDF lebih lanjut?
 Ya, Anda dapat menyesuaikan keluaran PDF dengan menyesuaikan pengaturan halaman, warna latar belakang, dan pengaturan lainnya di`PdfSaveOptions`.

### Apakah ada batasan pada versi uji coba Aspose.HTML untuk Java?
Versi uji coba mungkin memiliki beberapa keterbatasan, jadi sebaiknya periksa dokumentasi untuk mengetahui detailnya.

### Di mana saya bisa mendapatkan dukungan untuk Aspose.HTML untuk Java?
Anda dapat menemukan jawaban atas pertanyaan Anda dan mencari dukungan di[Forum Aspose.HTML](https://forum.aspose.com/).
