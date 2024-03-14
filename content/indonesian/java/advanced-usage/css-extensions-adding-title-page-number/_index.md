---
title: Sesuaikan Margin Halaman HTML dengan Aspose.HTML
linktitle: Ekstensi CSS - Menambahkan Judul dan Nomor Halaman
second_title: Pemrosesan Java HTML dengan Aspose.HTML
description: Pelajari cara menyesuaikan margin halaman, menambahkan nomor halaman, dan judul ke dokumen HTML menggunakan Aspose.HTML untuk Java.
type: docs
weight: 10
url: /id/java/advanced-usage/css-extensions-adding-title-page-number/
---
Aspose.HTML untuk Java adalah perpustakaan yang kuat untuk memproses dokumen HTML dalam aplikasi Java. Dalam tutorial ini, kita akan mempelajari cara membuat margin halaman khusus dan menambahkan nomor halaman serta judul ke dokumen HTML Anda menggunakan Aspose.HTML untuk Java. Panduan langkah demi langkah ini akan memecah proses menjadi langkah-langkah yang dapat dikelola untuk membantu Anda mengintegrasikan fitur-fitur ini dengan mudah ke dalam dokumen HTML Anda.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki prasyarat berikut:

1. Lingkungan Pengembangan Java: Pastikan Anda telah menyiapkan lingkungan pengembangan Java di komputer Anda.

2.  Aspose.HTML untuk Java: Unduh dan instal pustaka Aspose.HTML untuk Java dari[Di Sini](https://releases.aspose.com/html/java/).

## Paket Impor

Untuk memulai, Anda perlu mengimpor paket yang diperlukan dari Aspose.HTML untuk Java. Tambahkan pernyataan import berikut ke kode Java Anda:

```java
// Impor paket Aspose.HTML
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

Sekarang, mari kita uraikan proses penambahan margin halaman khusus, nomor halaman, dan judul ke dalam langkah-langkah yang dapat dikelola:

## Langkah 1: Inisialisasi Konfigurasi dan Margin Halaman

```java
// Inisialisasi objek konfigurasi dan atur margin halaman untuk dokumen
Configuration configuration = new Configuration();
try {
    // Dapatkan layanan Agen Pengguna
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Atur gaya margin khusus dan buat tanda di atasnya
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

Pada langkah ini, kita menginisialisasi objek konfigurasi dan mengatur margin halaman khusus, termasuk posisi penghitung halaman dan judul halaman.

## Langkah 2: Inisialisasi Dokumen HTML

```java
// Inisialisasi dokumen HTML
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Di sini, kita membuat dokumen HTML dengan contoh konten (dalam hal ini, pesan "Halo Dunia") dan menerapkan konfigurasi dari Langkah 1.

## Langkah 3: Inisialisasi Perangkat Output dan Render Dokumen

```java
// Inisialisasi perangkat keluaran
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    //Kirim dokumen ke perangkat keluaran
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Pada langkah ini, kami menyiapkan perangkat keluaran dan merender dokumen HTML. Dokumen akan diproses dan disimpan sebagai file XPS dengan margin halaman, nomor halaman, dan judul yang ditentukan.

## Kesimpulan

Selamat! Anda telah berhasil mempelajari cara membuat margin halaman khusus dan menambahkan nomor halaman serta judul ke dokumen HTML Anda menggunakan Aspose.HTML untuk Java. Penyesuaian ini memungkinkan Anda membuat dokumen yang lebih profesional dan menarik secara visual.

 Jika Anda memiliki pertanyaan atau menghadapi masalah apa pun, silakan kunjungi[Aspose.HTML untuk dokumentasi Java](https://reference.aspose.com/html/java/) atau mencari bantuan di[Asumsikan forum dukungan](https://forum.aspose.com/).

## FAQ

### Q1: Apa itu Aspose.HTML untuk Java?

A1: Aspose.HTML untuk Java adalah pustaka Java yang menyediakan alat canggih untuk bekerja dengan dokumen HTML dalam aplikasi Java.

### Q2: Dapatkah saya menyesuaikan margin halaman lebih lanjut?

A2: Ya, Anda dapat mengubah gaya CSS pada Langkah 1 untuk menyesuaikan margin halaman sesuai kebutuhan Anda.

### Q3: Bagaimana cara menambahkan lebih banyak konten ke dokumen HTML?

A3: Anda dapat mengubah konten HTML pada Langkah 2 dengan mengganti konten sampel dengan milik Anda sendiri.

### Q4: Apakah Aspose.HTML untuk Java kompatibel dengan format dokumen lain?

A4: Ya, Aspose.HTML untuk Java dapat digunakan untuk mengkonversi dokumen HTML ke berbagai format, termasuk PDF, XPS, dan gambar.

### Q5: Apakah saya memerlukan lisensi untuk menggunakan Aspose.HTML untuk Java?

 A5: Ya, Anda bisa mendapatkan lisensi atau uji coba gratis dari[Di Sini](https://purchase.aspose.com/buy) atau[Di Sini](https://releases.aspose.com/).