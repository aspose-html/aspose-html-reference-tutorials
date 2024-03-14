---
title: Sesuaikan Ukuran Halaman XPS dengan Aspose.HTML untuk Java
linktitle: Menyesuaikan Ukuran Halaman XPS
second_title: Pemrosesan Java HTML dengan Aspose.HTML
description: Pelajari cara menyesuaikan ukuran halaman XPS dengan Aspose.HTML untuk Java. Kontrol dimensi keluaran dokumen XPS Anda dengan mudah.
type: docs
weight: 16
url: /id/java/advanced-usage/adjust-xps-page-size/
---

Dalam tutorial ini, kami akan memandu Anda melalui proses penyesuaian ukuran halaman XPS menggunakan Aspose.HTML untuk Java. Pustaka canggih ini memungkinkan Anda memanipulasi dokumen HTML dan merendernya ke dalam berbagai format, termasuk XPS. Menyesuaikan ukuran halaman sangat penting ketika Anda perlu mengontrol dimensi keluaran dokumen XPS Anda.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut:

1. Lingkungan Pengembangan Java: Pastikan Anda telah menginstal Java Development Kit (JDK) di sistem Anda.

2.  Aspose.HTML untuk Perpustakaan Java: Anda perlu mengunduh dan menyertakan perpustakaan Aspose.HTML untuk Java di proyek Java Anda. Anda dapat menemukan perpustakaan[Di Sini](https://releases.aspose.com/html/java/).

3. Masukkan File HTML: Siapkan file HTML yang ingin Anda render dan sesuaikan ukuran halaman XPS. Anda dapat menggunakan file HTML Anda sendiri untuk tutorial ini.

## Paket Impor

Pertama, Anda perlu mengimpor paket yang diperlukan agar dapat bekerja dengan Aspose.HTML untuk Java. Sertakan paket-paket ini di awal kelas Java Anda:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Langkah 1: Tetapkan Nama File Masukan

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 Pada langkah ini, kami membaca file input HTML Anda menggunakan a`FileInputStream`.

## Langkah 2: Buat Dokumen HTML dan Atur Gaya

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 Langkah ini melibatkan pembuatan`HTMLDocument` dan menambahkan gaya ke dalamnya.

## Langkah 3: Buat Opsi Rendering XPS

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Di sini, kami membuat opsi rendering XPS untuk mengonfigurasi proses rendering.

## Langkah 4: Sesuaikan Ukuran Halaman

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

Langkah ini melibatkan pengaturan ukuran halaman dan menentukan apakah akan menyesuaikannya ke halaman terluas.

## Langkah 5: Render Outputnya

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

Pada langkah terakhir, kami merender output XPS menggunakan opsi yang dikonfigurasi.

## Kesimpulan

Dalam tutorial ini, kami telah menunjukkan kepada Anda cara menyesuaikan ukuran halaman XPS menggunakan Aspose.HTML untuk Java. Anda dapat mengontrol dimensi keluaran dokumen XPS Anda, memastikannya memenuhi kebutuhan spesifik Anda. Dengan kode dan langkah-langkah yang disediakan, Anda dapat dengan mudah mengimplementasikan fitur ini di aplikasi Java Anda.

 Jika Anda memiliki pertanyaan atau memerlukan bantuan lebih lanjut, silakan kunjungi[Aspose.HTML untuk dokumentasi Java](https://reference.aspose.com/html/java/) atau meminta bantuan di[Asumsikan Forum](https://forum.aspose.com/).

## FAQ

### Q1: Apa itu Aspose.HTML untuk Java?

A1: Aspose.HTML untuk Java adalah pustaka Java yang memungkinkan pengembang memanipulasi dan mengonversi dokumen HTML ke berbagai format, seperti XPS, PDF, dan gambar.

### Q2: Di mana saya dapat mengunduh Aspose.HTML untuk Java?

 A2: Anda dapat mengunduh perpustakaan Aspose.HTML untuk Java dari[Link ini](https://releases.aspose.com/html/java/).

### Q3: Apakah tersedia uji coba gratis untuk Aspose.HTML untuk Java?

 A3: Ya, Anda bisa mendapatkan uji coba gratis Aspose.HTML untuk Java dari[Di Sini](https://releases.aspose.com/).

### Q4: Bagaimana cara mendapatkan lisensi sementara Aspose.HTML untuk Java?

 A4: Untuk mendapatkan lisensi sementara Aspose.HTML untuk Java, kunjungi[halaman ini](https://purchase.aspose.com/temporary-license/).

### Q5: Bisakah saya mendapatkan dukungan untuk Aspose.HTML untuk Java?

 A5: Ya, Anda dapat mencari bantuan dan dukungan dari komunitas Aspose di[Asumsikan Forum](https://forum.aspose.com/).