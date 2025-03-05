---
title: Konversi HTML ke JPG dengan Aspose.HTML untuk Java
linktitle: Mengonversi HTML ke JPG
second_title: Pemrosesan HTML Java dengan Aspose.HTML
description: Pelajari cara mengonversi HTML ke JPG menggunakan Aspose.HTML untuk Java. Ikuti panduan langkah demi langkah kami untuk konversi HTML ke JPG yang lancar.
type: docs
weight: 12
url: /id/java/converting-html-to-various-image-formats/convert-html-to-jpg/
---

Di era digital, mengubah konten HTML ke berbagai format merupakan kebutuhan umum. Aspose.HTML untuk Java adalah pustaka canggih yang menyederhanakan proses konversi HTML ke JPG. Dalam panduan lengkap ini, kami akan memandu Anda melalui proses tersebut langkah demi langkah. Anda akan mempelajari prasyarat, cara mengimpor paket, dan membagi setiap contoh menjadi beberapa langkah untuk menguasai konversi HTML ke JPG dengan Aspose.HTML untuk Java.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki prasyarat berikut:

1. Java Development Environment: Pastikan Anda telah menginstal Java di sistem Anda. Anda dapat mengunduh dan menginstalnya dari situs web Java.

2.  Pustaka Aspose.HTML untuk Java: Anda perlu memasang pustaka Aspose.HTML untuk Java. Jika Anda belum melakukannya, Anda dapat mengunduhnya dari[Di Sini](https://releases.aspose.com/html/java/).

## Paket Impor

Untuk memulai, Anda perlu mengimpor paket Aspose.HTML yang diperlukan ke dalam proyek Java Anda. Anda dapat melakukannya dengan menggunakan kode berikut:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.image.ImageFormat;
import com.aspose.html.converters.Converter;
import java.io.FileWriter;
```

Sekarang, mari kita uraikan proses konversi HTML ke JPG menjadi beberapa langkah:

## Siapkan Kode HTML

Pertama, siapkan kode HTML yang ingin Anda ubah menjadi gambar JPG. Anda dapat melakukannya dengan membuat file HTML atau string yang berisi kode HTML.

```java
String code = "<span>Hello</span> <span>World!!</span>";
try (FileWriter fileWriter = new FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Inisialisasi Dokumen HTML

Selanjutnya, Anda perlu menginisialisasi dokumen HTML dari berkas HTML yang baru saja Anda buat. Ini dilakukan dengan menggunakan pustaka Aspose.HTML.

```java
HTMLDocument document = new HTMLDocument("document.html");
```

## Konfigurasikan ImageSaveOptions

 Sekarang, konfigurasikan`ImageSaveOptions` untuk menentukan format penyimpanan gambar. Dalam kasus ini, kita akan mengonversinya ke JPEG.

```java
ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Jpeg);
```

## Konversi HTML ke JPG

Langkah terakhir adalah mengonversi dokumen HTML menjadi gambar JPG menggunakan opsi yang ditentukan.

```java
Converter.convertHTML(document, options, "output.jpg");
```

## Pembersihan

Jangan lupa untuk melepaskan sumber daya setelah Anda selesai melakukan konversi.

```java
if (document != null) {
    document.dispose();
}
```

Selamat! Anda berhasil mengonversi HTML ke JPG menggunakan Aspose.HTML untuk Java.

## Kesimpulan

Aspose.HTML untuk Java menyederhanakan proses konversi HTML ke JPG, menjadikannya alat penting bagi para pengembang. Dengan panduan langkah demi langkah ini, Anda telah mempelajari cara menyiapkan HTML, menginisialisasi dokumen, mengonfigurasi opsi, dan melakukan konversi. Sekarang, Anda dapat dengan mudah mengintegrasikan fitur ini ke dalam aplikasi Java Anda.

 Jika Anda memiliki pertanyaan lebih lanjut atau memerlukan dukungan, jangan ragu untuk mengunjungi[Dokumentasi Aspose.HTML untuk Java](https://reference.aspose.com/html/java/) atau hubungi[Forum dukungan Aspose](https://forum.aspose.com/).

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.HTML untuk Java?
Aspose.HTML untuk Java adalah pustaka Java yang memungkinkan pengembang untuk bekerja dengan dokumen HTML dan melakukan berbagai operasi, termasuk konversi HTML ke JPG.

### Di mana saya dapat mengunduh Aspose.HTML untuk Java?
 Anda dapat mengunduh Aspose.HTML untuk Java dari halaman rilis[Di Sini](https://releases.aspose.com/html/java/).

### Apakah ada uji coba gratis yang tersedia?
 Ya, Anda bisa mendapatkan uji coba gratis Aspose.HTML untuk Java dari[Di Sini](https://releases.aspose.com/).

### Apakah saya memerlukan lisensi untuk penggunaan komersial?
 Ya, untuk penggunaan komersial, Anda dapat membeli lisensi dari[tautan ini](https://purchase.aspose.com/buy).

### Bagaimana saya bisa mendapatkan lisensi sementara?
Jika Anda memerlukan lisensi sementara, Anda dapat memperolehnya dari[tautan ini](https://purchase.aspose.com/temporary-license/).