---
date: 2025-12-05
description: Pelajari cara mengatur margin halaman HTML di Java menggunakan Aspose.HTML,
  serta menambahkan nomor halaman dan judul ke dokumen Anda.
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: Cara Mengatur Margin Halaman HTML dengan Java menggunakan Aspose.HTML
url: /id/java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengatur Margin Halaman HTML Java dengan Aspose.HTML

Dalam tutorial ini Anda akan menemukan **cara mengatur margin halaman HTML Java**‑style menggunakan Aspose.HTML untuk Java. Kami akan membahas cara membuat margin halaman khusus, menyisipkan nomor halaman, dan menambahkan judul dokumen—semua dengan kode langkah‑demi‑langkah yang jelas yang dapat Anda salin ke proyek Anda.

## Jawaban Cepat
- **Perpustakaan apa yang dibutuhkan?** Aspose.HTML for Java  
- **Apakah saya dapat mengontrol margin secara programatis?** Ya, via aturan CSS `@page` di user‑style sheet  
- **Format output mana yang mendukung margin?** XPS, PDF, dan format raster lainnya  
- **Apakah saya memerlukan lisensi untuk produksi?** Lisensi Aspose.HTML yang valid diperlukan untuk penggunaan non‑trial  
- **Apakah ini kompatibel dengan Java 11+?** Tentu – perpustakaan ini bekerja dengan versi Java modern  

## Apa Itu “Mengatur Margin Halaman HTML Java”?
Mengatur margin halaman HTML di Java berarti mengonfigurasi mesin rendering (disediakan oleh Aspose.HTML) untuk menerapkan properti CSS page‑box sebelum dokumen dikonversi ke format yang dapat dicetak seperti XPS atau PDF. Dengan mendefinisikan aturan `@page` khusus, Anda mengontrol area yang dapat dicetak, nomor halaman, serta konten header/footer.

## Mengapa Menggunakan Aspose.HTML untuk Kontrol Margin?
- **Tata letak presisi** – CSS `@page` memberi Anda kontrol pixel‑perfect atas margin, header, dan footer.  
- **Konsistensi lintas format** – Definisi margin yang sama bekerja untuk XPS, PDF, dan output gambar.  
- **Tanpa ketergantungan browser** – Rendering terjadi di sisi server, jadi Anda tidak memerlukan browser headless.  

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut:

1. **Lingkungan Pengembangan Java** – JDK 11 atau yang lebih baru terpasang.  
2. **Aspose.HTML untuk Java** – Unduh dan instal perpustakaan dari [here](https://releases.aspose.com/html/java/).  

## Impor Paket

Untuk memulai, impor kelas Aspose.HTML yang diperlukan:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## Cara Mengatur Margin Halaman HTML Java – Panduan Langkah‑demi‑Langkah

### Langkah 1: Inisialisasi Konfigurasi dan Definisikan Margin Halaman Kustom

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

Dalam blok ini kami membuat objek `Configuration`, memperoleh `IUserAgentService`, dan menyuntikkan aturan CSS `@page` yang mendefinisikan margin, penghitung halaman kanan‑bawah, serta judul dokumen di tengah‑atas.

### Langkah 2: Buat Dokumen HTML

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Di sini kami menginstansiasi `HTMLDocument` dengan potongan sederhana “Hello World”. Konfigurasi yang sama dari Langkah 1 diterapkan, sehingga margin khusus dihormati saat dokumen dirender.

### Langkah 3: Render ke File XPS (atau output lain yang didukung)

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Langkah ini membuat `XpsDevice` yang menulis halaman yang dirender ke `output.xps`. Margin, nomor halaman, dan judul yang Anda definisikan sebelumnya akan muncul di file akhir.

## Masalah Umum & Tips

- **Margin tidak berubah** – Pastikan aturan `@page` tidak ditimpa oleh stylesheet lain. Pemanggilan `setUserStyleSheet` memaksanya menjadi prioritas tertinggi.  
- **Nomor halaman menampilkan “NaN”** – Pastikan Anda menggunakan Aspose.HTML versi 23.10 atau lebih baru; versi lama tidak memiliki fungsi `currentPageNumber()`.  
- **File output kosong** – Pastikan jalur `Resources.output` terresolusi dengan benar dan Anda memiliki izin menulis.  

## Pertanyaan yang Sering Diajukan

### Q1: Apa itu Aspose.HTML untuk Java?

**A:** Aspose.HTML untuk Java adalah perpustakaan Java yang menyediakan alat kuat untuk bekerja dengan dokumen HTML dalam aplikasi Java, termasuk konversi, rendering, dan manipulasi.

### Q2: Bisakah saya menyesuaikan margin halaman lebih lanjut?

**A:** Ya, cukup edit CSS di dalam `setUserStyleSheet`. Anda dapat mengubah nilai `margin-*` apa pun atau menambahkan kotak `@top-*` / `@bottom-*` tambahan.

### Q3: Bagaimana saya dapat menambahkan lebih banyak konten ke dokumen HTML?

**A:** Ganti string dalam `new HTMLDocument("<div>Hello World!!!</div>", …)` dengan markup HTML Anda sendiri, atau muat file eksternal menggunakan konstruktor `HTMLDocument(String url, …)`.

### Q4: Apakah Aspose.HTML untuk Java kompatibel dengan format dokumen lain?

**A:** Tentu saja. `HTMLDocument` yang sama dapat dirender ke PDF, XPS, gambar, atau bahkan EPUB dengan mengganti perangkat output (misalnya, `PdfDevice`, `PngDevice`).

### Q5: Apakah saya memerlukan lisensi untuk menggunakan Aspose.HTML untuk Java?

**A:** Ya, lisensi diperlukan untuk penggunaan produksi. Anda dapat memperoleh percobaan atau membeli lisensi dari [here](https://purchase.aspose.com/buy) atau [here](https://releases.aspose.com/).

### Q6: Bagaimana cara mengatur margin berbeda untuk halaman ganjil dan genap?

**A:** Gunakan pseudo‑class `@page :left` dan `@page :right` di dalam stylesheet Anda untuk mendefinisikan margin yang berbeda untuk halaman kiri (genap) dan kanan (ganjil).

### Q7: Bisakah saya menyematkan font khusus dalam dokumen yang dirender?

**A:** Ya. Tambahkan aturan `@font-face` ke stylesheet pengguna dan referensikan font tersebut dalam konten HTML Anda.

## Kesimpulan

Anda kini telah menguasai **cara mengatur margin halaman HTML Java** menggunakan Aspose.HTML, dan Anda tahu cara menambahkan nomor halaman serta judul untuk membuat dokumen Anda terlihat profesional. Jangan ragu untuk bereksperimen dengan kotak `@page` tambahan, font khusus, atau format output berbeda sesuai kebutuhan proyek Anda.

Jika Anda menghadapi tantangan, dokumentasi resmi [Aspose.HTML for Java documentation](https://reference.aspose.com/html/java/) dan [Aspose support forum](https://forum.aspose.com/) adalah tempat yang sangat baik untuk mendapatkan bantuan.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-05  
**Tested With:** Aspose.HTML for Java 23.12  
**Author:** Aspose