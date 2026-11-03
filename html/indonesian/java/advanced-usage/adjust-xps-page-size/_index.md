---
date: 2026-08-28
description: Sesuaikan ukuran halaman XPS saat mengonversi HTML ke XPS di Java menggunakan
  Aspose.HTML. Render HTML ke XPS dengan dimensi yang tepat.
keywords:
- adjust xps page size
- render html to xps
- aspose.html java
- xps conversion java
- html to xps
lastmod: 2026-08-28
linktitle: Menyesuaikan Ukuran Halaman XPS
og_description: Sesuaikan ukuran halaman XPS saat mengonversi HTML ke XPS di Java
  menggunakan Aspose.HTML. Pelajari cara merender HTML ke XPS dengan dimensi yang
  tepat dalam hitungan detik.
og_image_alt: Tutorial showing how to adjust XPS page size during HTML to XPS conversion
  with Aspose.HTML for Java
og_title: Sesuaikan ukuran halaman XPS saat mengonversi HTML ke XPS di Java
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  headline: Adjust XPS page size when converting HTML to XPS in Java
  type: TechArticle
- description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  name: Adjust XPS page size when converting HTML to XPS in Java
  steps:
  - name: set the input file name
    text: The `FileInputStream` class reads raw bytes from a file, providing the HTML
      source to the renderer.
  - name: create an HTML document and set styles
    text: The `HTMLDocument` class represents an in‑memory HTML DOM used by Aspose.HTML
      for rendering.
  - name: create XPS rendering options
    text: The `XpsRenderingOptions` class holds settings that control how HTML is
      rendered to XPS, such as page size and image quality.
  - name: adjust the page size
    text: '**How to set XPS page size** – Define a custom page size (width × height
      in points) and tell the renderer whether it should automatically expand to the
      widest page. Setting `adjustToWidestPage` to `false` preserves the exact dimensions
      you specify. The `PageSetup` class defines page size, margins, a'
  - name: render the output
    text: The `XpsDevice` class is the rendering target that writes the processed
      content to an XPS file.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a Java library that allows developers to manipulate
      and convert HTML documents into various formats, such as XPS, PDF, and images.
      You can download the library from [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).
    question: What is Aspose.HTML for Java?
  - answer: You can download the Aspose.HTML for Java library from [Aspose product
      releases page](https://releases.aspose.com/).
    question: Where can I download Aspose.HTML for Java?
  - answer: Yes, you can get a free trial of Aspose.HTML for Java from the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: Is there a free trial available for Aspose.HTML for Java?
  - answer: To get a temporary license for Aspose.HTML for Java, visit the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: How can I obtain a temporary license for Aspose.HTML for Java?
  - answer: Yes, you can seek help and support from the Aspose community on the [Aspose
      Forum](https://forum.aspose.com/).
    question: Can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
tags:
- adjust xps page size
- Aspose.HTML
- Java XPS conversion
- HTML to XPS
- document rendering
title: Sesuaikan ukuran halaman XPS saat mengonversi HTML ke XPS di Java
url: /id/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sesuaikan ukuran halaman XPS saat mengonversi HTML ke XPS di Java

Dalam tutorial ini Anda akan belajar **cara menyesuaikan ukuran halaman XPS** saat mengonversi HTML ke XPS dengan Aspose.HTML untuk Java. Baik Anda membutuhkan faktur yang dapat dicetak, laporan arsip, atau label berukuran khusus, mengendalikan dimensi halaman menjamin bahwa XPS akhir terlihat persis seperti yang diinginkan. Kami akan membahas penyiapan lingkungan, opsi rendering, dan pembuatan XPS akhir sehingga Anda dapat menyematkan kemampuan ini langsung ke dalam aplikasi Java Anda.

## Jawaban Cepat
- **Apa arti “convert HTML to XPS”?** Itu merender dokumen HTML menjadi file XPS, mempertahankan tata letak dan gaya.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Versi Java mana yang didukung?** Java 8 atau lebih tinggi (JDK 11+ disarankan).  
- **Bisakah saya mengubah ukuran halaman?** Ya – Aspose.HTML memungkinkan Anda menentukan dimensi khusus sebelum rendering.  
- **Berapa lama proses konversi?** Biasanya kurang dari satu detik untuk halaman standar; dokumen yang lebih besar mungkin memerlukan waktu lebih lama.

## Apa itu mengonversi HTML ke XPS?
Mengonversi HTML ke XPS berarti mengambil file markup berbasis web dan menghasilkan dokumen XPS (XML Paper Specification) — format tata letak tetap, siap cetak yang mirip dengan PDF. Ini berguna ketika Anda memerlukan dokumen dengan fidelitas tinggi, independen perangkat untuk pengarsipan atau pencetakan dari aplikasi Java.

## Mengapa menyesuaikan ukuran halaman XPS?
Menyesuaikan ukuran halaman XPS memberi Anda kontrol atas dimensi fisik dokumen akhir (misalnya, A4, Letter, label khusus). Ini mencegah skala yang tidak diinginkan, memastikan konten pas sempurna, dan dapat mengurangi ukuran file dengan menghilangkan ruang putih yang tidak diperlukan.

## Cara merender HTML ke XPS dengan ukuran halaman khusus?
Muat HTML Anda, konfigurasikan `XpsRenderingOptions` dengan `PageSetup` yang menentukan lebar dan tinggi tepat yang Anda butuhkan, lalu render ke `XpsDevice`. Alur dua langkah ini memungkinkan Anda menjaga tata letak tetap sambil menerapkan dimensi yang Anda tentukan, semuanya dalam satu panggilan API.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut:

1. **Lingkungan Pengembangan Java** – Java Development Kit (JDK) terpasang di sistem Anda.  
2. **Perpustakaan Aspose.HTML untuk Java** – Unduh dan sertakan perpustakaan Aspose.HTML untuk Java dalam proyek Anda. Anda dapat menemukan perpustakaan di [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).  
3. **File HTML Input** – Siapkan file HTML yang ingin Anda render dan sesuaikan ukuran halaman XPS-nya. Anda dapat menggunakan file HTML Anda sendiri untuk tutorial ini.

## Impor paket

Kelas `Page` mewakili dimensi halaman dan pengaturan untuk output XPS. Kelas `HtmlRenderer` melakukan konversi dari HTML ke XPS.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Panduan langkah demi langkah

Berikut adalah panduan singkat berurutan yang mencerminkan langkah-langkah asli sambil menambahkan konteks tambahan untuk kejelasan.

### Langkah 1: tetapkan nama file input

Kelas `FileInputStream` membaca byte mentah dari sebuah file, menyediakan sumber HTML ke renderer.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### Langkah 2: buat dokumen HTML dan atur gaya

Kelas `HTMLDocument` mewakili DOM HTML dalam memori yang digunakan oleh Aspose.HTML untuk rendering.

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### Langkah 3: buat opsi rendering XPS

Kelas `XpsRenderingOptions` menyimpan pengaturan yang mengontrol bagaimana HTML dirender ke XPS, seperti ukuran halaman dan kualitas gambar.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### Langkah 4: sesuaikan ukuran halaman  

**Cara mengatur ukuran halaman XPS** – Tentukan ukuran halaman khusus (lebar × tinggi dalam poin) dan beri tahu renderer apakah harus secara otomatis memperluas ke halaman terlebar. Menetapkan `adjustToWidestPage` ke `false` mempertahankan dimensi tepat yang Anda tentukan.

Kelas `PageSetup` mendefinisikan ukuran halaman, margin, dan orientasi untuk output XPS.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### Langkah 5: render output

Kelas `XpsDevice` adalah target rendering yang menulis konten yang diproses ke file XPS.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Masalah umum dan solusi

| Masalah | Mengapa terjadi | Solusi |
|-------|----------------|-----|
| **Output XPS kosong** | Aliran input tidak ditutup atau HTMLDocument mengarah ke file yang salah. | Pastikan `FileInputStream` dibungkus dengan benar dalam blok try‑with‑resources dan jalur file akurat. |
| **Ukuran halaman tidak diterapkan** | `adjustToWidestPage` dibiarkan `true`. | Setel `pageSetup.setAdjustToWidestPage(false);` seperti yang ditunjukkan pada Langkah 4. |
| **CSS tidak didukung** | Aspose.HTML mendukung sebagian subset CSS. | Gunakan tata letak dasar, font, dan warna; hindari selector lanjutan atau CSS Grid. |
| **LicenseException** | Menjalankan tanpa lisensi yang valid di produksi. | Terapkan lisensi sementara atau lisensi yang dibeli sebelum rendering (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Pertanyaan yang sering diajukan

**T: Apa itu Aspose.HTML untuk Java?**  
J: Aspose.HTML untuk Java adalah perpustakaan Java yang memungkinkan pengembang memanipulasi dan mengonversi dokumen HTML ke berbagai format, seperti XPS, PDF, dan gambar. Anda dapat mengunduh perpustakaan dari [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).

**T: Di mana saya dapat mengunduh Aspose.HTML untuk Java?**  
J: Anda dapat mengunduh perpustakaan Aspose.HTML untuk Java dari [Aspose product releases page](https://releases.aspose.com/).

**T: Apakah ada percobaan gratis untuk Aspose.HTML untuk Java?**  
J: Ya, Anda dapat memperoleh percobaan gratis Aspose.HTML untuk Java dari [temporary license request page](https://purchase.aspose.com/temporary-license/).

**T: Bagaimana cara mendapatkan lisensi sementara untuk Aspose.HTML untuk Java?**  
J: Untuk mendapatkan lisensi sementara untuk Aspose.HTML untuk Java, kunjungi [temporary license request page](https://purchase.aspose.com/temporary-license/).

**T: Bisakah saya mendapatkan dukungan untuk Aspose.HTML untuk Java?**  
J: Ya, Anda dapat mencari bantuan dan dukungan dari komunitas Aspose di [Aspose Forum](https://forum.aspose.com/).

**T: Bisakah saya mengonversi HTML ke XPS di server tanpa tampilan (headless)?**  
J: Tentu saja. Aspose.HTML berfungsi di lingkungan tanpa GUI; pastikan runtime Java terkonfigurasi dengan benar.

**T: Apakah perpustakaan mendukung margin halaman khusus?**  
J: Ya. Gunakan `PageSetup.setMarginTop()`, `setMarginBottom()`, dll., sebelum menetapkan `PageSetup` ke opsi rendering.

## Kesimpulan

Kami telah membahas proses lengkap **mengonversi HTML ke XPS** dan **menyesuaikan ukuran halaman XPS** dengan Aspose.HTML untuk Java. Dengan mengikuti langkah‑langkah ini Anda dapat menghasilkan dokumen XPS siap cetak yang sesuai dengan persyaratan tata letak Anda. Jangan ragu bereksperimen dengan dimensi halaman yang berbeda, gaya, atau bahkan menambahkan header dan footer untuk memenuhi kebutuhan proyek Anda.

Jika Anda memiliki pertanyaan atau membutuhkan bantuan lebih lanjut, jelajahi [dokumentasi Aspose.HTML untuk Java](https://reference.aspose.com/html/java/) atau bergabung dalam diskusi di [Aspose Forum](https://forum.aspose.com/).

---

**Terakhir Diperbarui:** 2026-08-28  
**Diuji Dengan:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Penulis:** Aspose

## Tutorial Terkait

- [Konversi HTML ke XPS dengan Aspose.HTML untuk Java](/html/java/conversion-html-to-other-formats/convert-html-to-xps/)
- [Sesuaikan Ukuran Halaman PDF dengan Aspose.HTML untuk Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Konversi EPUB ke XPS dengan Aspose.HTML untuk Java](/html/java/converting-epub-to-xps/convert-epub-to-xps/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}