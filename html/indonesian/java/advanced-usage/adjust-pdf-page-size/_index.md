---
title: Sesuaikan Ukuran Halaman PDF dengan Aspose.HTML untuk Java
linktitle: Menyesuaikan Ukuran Halaman PDF
second_title: Pemrosesan HTML Java dengan Aspose.HTML
description: Pelajari cara menyesuaikan ukuran halaman PDF dengan Aspose.HTML untuk Java. Buat PDF berkualitas tinggi dari HTML dengan mudah. Kontrol dimensi halaman secara efektif.
weight: 15
url: /id/java/advanced-usage/adjust-pdf-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sesuaikan Ukuran Halaman PDF dengan Aspose.HTML untuk Java


Di era digital saat ini, kebutuhan untuk menghasilkan PDF berkualitas tinggi dari konten HTML semakin meningkat. Aspose.HTML untuk Java adalah pustaka Java yang canggih yang memungkinkan Anda mengonversi dokumen HTML ke format PDF dengan mudah. Dalam tutorial ini, kami akan fokus pada penyesuaian ukuran halaman saat mengonversi HTML ke PDF menggunakan Aspose.HTML untuk Java.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki prasyarat berikut:

- Lingkungan Pengembangan Java: Pastikan Anda telah menginstal Java Development Kit (JDK) di sistem Anda.
-  Aspose.HTML untuk Java: Anda perlu mengunduh dan menginstal Aspose.HTML untuk Java dari situs web[Di Sini](https://releases.aspose.com/html/java/).
- Dokumen HTML: Anda harus memiliki dokumen HTML yang siap dikonversi. Jika belum, buatlah satu atau gunakan berkas HTML yang sudah ada.

## Paket Impor

Untuk memulai, Anda perlu mengimpor paket yang diperlukan untuk bekerja dengan Aspose.HTML untuk Java. Cuplikan kode berikut menunjukkan cara melakukannya:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

Sekarang Anda telah menyiapkan prasyarat dan mengimpor paket yang diperlukan, mari kita uraikan proses penyesuaian ukuran halaman PDF menjadi beberapa langkah:

## Langkah 1: Membaca Konten HTML

Pertama, Anda perlu membaca konten HTML yang ingin Anda ubah ke PDF. Dalam contoh ini, kita akan membaca HTML dari file bernama "FirstFile.html."

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Langkah 2: Menulis Konten HTML

Berikutnya, Anda akan menulis konten HTML ke file bernama "FirstFileOut.html."

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Tambahkan gaya HTML atau konten khusus di sini
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## Langkah 3: Merender HTML ke PDF

Sekarang, Anda akan merender konten HTML ke dalam berkas PDF. Kami akan membahas dua skenario: satu di mana ukuran halaman tidak disesuaikan dengan lebar konten, dan yang lainnya di mana ukuran halaman disesuaikan.

### Ukuran Halaman Tidak Disesuaikan

Dalam skenario ini, ukuran halaman ditetapkan pada lebar dan tinggi tetap, yang dapat memotong konten jika melebihi dimensi ini.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Buat instance HTMLDocument dari file HTML
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Tetapkan opsi rendering PDF
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Render outputnya
pdf_renderer.render(device, html_document);
```

### Ukuran Halaman Disesuaikan dengan Lebar Konten

Dalam skenario ini, ukuran halaman disesuaikan menurut lebar konten.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Render outputnya
pdf_renderer.render(device, html_document);
```

## Kesimpulan

Dalam tutorial ini, kami telah mempelajari cara menyesuaikan ukuran halaman PDF saat mengonversi HTML ke PDF menggunakan Aspose.HTML untuk Java. Anda telah mempelajari prasyarat, mengimpor paket yang diperlukan, dan mengikuti panduan langkah demi langkah untuk mencapai tugas ini. Dengan Aspose.HTML untuk Java, Anda dapat dengan mudah mengontrol ukuran halaman PDF yang Anda hasilkan, memastikan bahwa konten Anda ditampilkan sebagaimana mestinya.

 Jangan ragu untuk bereksperimen dengan berbagai ukuran dan pengaturan halaman untuk memenuhi kebutuhan spesifik Anda. Jika Anda mengalami masalah atau memiliki pertanyaan lebih lanjut, jangan ragu untuk meminta bantuan dari[Dokumentasi Aspose.HTML untuk Java](https://reference.aspose.com/html/java/) atau[Forum dukungan Aspose](https://forum.aspose.com/).

## Pertanyaan yang Sering Diajukan

### Q1: Apa itu Aspose.HTML untuk Java?

A1: Aspose.HTML untuk Java adalah pustaka Java yang memungkinkan Anda bekerja dengan dokumen HTML, memanipulasi, mengonversi, dan merendernya ke berbagai format, termasuk PDF.

### Q2: Bagaimana cara menyesuaikan ukuran halaman PDF saat mengonversi HTML ke PDF dengan Aspose.HTML untuk Java?

 A2: Anda dapat menyesuaikan ukuran halaman PDF dengan menggunakan`PageSetup` kelas dan pengaturan`AdjustToWidestPage` properti untuk`true` atau `salah, tergantung pada kebutuhan Anda.

### Q3: Dapatkah saya menyesuaikan gaya konten HTML sebelum mengonversinya ke PDF?

A3: Ya, Anda dapat menyesuaikan gaya dengan menambahkan elemen CSS dan HTML ke konten HTML Anda sebelum mengonversinya ke PDF, seperti yang ditunjukkan dalam tutorial.

### Q4: Di mana saya dapat menemukan dokumentasi untuk Aspose.HTML untuk Java?

 A4: Anda dapat merujuk ke dokumentasi[Di Sini](https://reference.aspose.com/html/java/) untuk informasi dan contoh yang lengkap.

### Q5: Apakah ada uji coba gratis yang tersedia untuk Aspose.HTML untuk Java?

 A5: Ya, Anda dapat mengakses uji coba gratis Aspose.HTML untuk Java dari[tautan ini](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
