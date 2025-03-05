---
title: Sesuaikan Margin Halaman HTML dengan Aspose.HTML
linktitle: Ekstensi CSS - Menambahkan Judul dan Nomor Halaman
second_title: Pemrosesan HTML Java dengan Aspose.HTML
description: Pelajari cara menyesuaikan margin halaman, menambahkan nomor halaman, dan judul ke dokumen HTML menggunakan Aspose.HTML untuk Java.
type: docs
weight: 10
url: /id/java/advanced-usage/css-extensions-adding-title-page-number/
---
Aspose.HTML untuk Java adalah pustaka yang hebat untuk memproses dokumen HTML dalam aplikasi Java. Dalam tutorial ini, kita akan menjelajahi cara membuat margin halaman khusus dan menambahkan nomor halaman dan judul ke dokumen HTML Anda menggunakan Aspose.HTML untuk Java. Panduan langkah demi langkah ini akan menguraikan proses menjadi langkah-langkah yang mudah dikelola untuk membantu Anda mengintegrasikan fitur-fitur ini ke dalam dokumen HTML Anda dengan mudah.

## Prasyarat

Sebelum kita memulai, pastikan Anda memiliki prasyarat berikut:

1. Lingkungan Pengembangan Java: Pastikan Anda telah menyiapkan lingkungan pengembangan Java di komputer Anda.

2.  Aspose.HTML untuk Java: Unduh dan instal pustaka Aspose.HTML untuk Java dari[Di Sini](https://releases.aspose.com/html/java/).

## Paket Impor

Untuk memulai, Anda perlu mengimpor paket yang diperlukan dari Aspose.HTML untuk Java. Tambahkan pernyataan impor berikut ke kode Java Anda:

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
    // Mengatur gaya margin kustom dan membuat tanda di atasnya
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

Pada langkah ini, kami menginisialisasi objek konfigurasi dan mengatur margin halaman khusus, termasuk posisi penghitung halaman dan judul halaman.

## Langkah 2: Inisialisasi Dokumen HTML

```java
// Inisialisasi dokumen HTML
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Di sini, kami membuat dokumen HTML dengan contoh konten (dalam hal ini, pesan "Halo Dunia") dan menerapkan konfigurasi dari Langkah 1.

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

Pada langkah ini, kita menyiapkan perangkat keluaran dan merender dokumen HTML. Dokumen akan diproses dan disimpan sebagai file XPS dengan margin halaman, nomor halaman, dan judul yang ditentukan.

## Kesimpulan

Selamat! Anda telah berhasil mempelajari cara membuat margin halaman khusus dan menambahkan nomor halaman serta judul ke dokumen HTML Anda menggunakan Aspose.HTML untuk Java. Kustomisasi ini memungkinkan Anda membuat dokumen yang lebih profesional dan menarik secara visual.

 Jika Anda memiliki pertanyaan atau menghadapi masalah, jangan ragu untuk mengunjungi[Dokumentasi Aspose.HTML untuk Java](https://reference.aspose.com/html/java/) atau mencari bantuan di[Forum dukungan Aspose](https://forum.aspose.com/).

## Pertanyaan yang Sering Diajukan

### Q1: Apa itu Aspose.HTML untuk Java?

A1: Aspose.HTML untuk Java adalah pustaka Java yang menyediakan alat hebat untuk bekerja dengan dokumen HTML dalam aplikasi Java.

### Q2: Dapatkah saya menyesuaikan margin halaman lebih lanjut?

A2: Ya, Anda dapat mengubah gaya CSS di Langkah 1 untuk menyesuaikan margin halaman sesuai kebutuhan Anda.

### Q3: Bagaimana saya dapat menambahkan lebih banyak konten ke dokumen HTML?

A3: Anda dapat mengubah konten HTML pada Langkah 2 dengan mengganti konten contoh dengan konten Anda sendiri.

### Q4: Apakah Aspose.HTML untuk Java kompatibel dengan format dokumen lain?

A4: Ya, Aspose.HTML untuk Java dapat digunakan untuk mengonversi dokumen HTML ke berbagai format, termasuk PDF, XPS, dan gambar.

### Q5: Apakah saya memerlukan lisensi untuk menggunakan Aspose.HTML untuk Java?

 A5: Ya, Anda bisa mendapatkan lisensi atau uji coba gratis dari[Di Sini](https://purchase.aspose.com/buy) atau[Di Sini](https://releases.aspose.com/).