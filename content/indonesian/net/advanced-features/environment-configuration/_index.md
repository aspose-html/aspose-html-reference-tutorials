---
title: Konfigurasi Lingkungan di .NET dengan Aspose.HTML
linktitle: Konfigurasi Lingkungan di .NET
second_title: Aspose.HTML .NET API manipulasi HTML
description: Pelajari cara bekerja dengan dokumen HTML dalam .NET menggunakan Aspose.HTML untuk tugas-tugas seperti manajemen skrip, gaya kustom, kontrol eksekusi JavaScript, dan banyak lagi. Tutorial komprehensif ini menyediakan contoh langkah demi langkah dan Tanya Jawab Umum untuk membantu Anda memulai.
type: docs
weight: 10
url: /id/net/advanced-features/environment-configuration/
---

Di dunia digital saat ini, membuat dan memanipulasi dokumen HTML merupakan tugas mendasar bagi banyak pengembang. Baik Anda sedang membangun aplikasi web atau perlu mengonversi HTML ke format lain seperti PDF atau gambar, Aspose.HTML for .NET merupakan alat yang hebat untuk dimiliki dalam perangkat Anda. Dalam tutorial ini, kita akan menjelajahi berbagai aspek Aspose.HTML for .NET, termasuk prasyarat, mengimpor namespace, dan contoh langkah demi langkah dengan penjelasan terperinci.

## Prasyarat

Sebelum kita mulai menggunakan Aspose.HTML untuk .NET, Anda harus memastikan bahwa Anda memiliki prasyarat berikut:

1. Visual Studio: Pastikan Anda telah menginstal Visual Studio di komputer pengembangan Anda. Aspose.HTML untuk .NET dirancang agar dapat bekerja dengan lancar dengan Visual Studio.

2.  Aspose.HTML untuk .NET: Anda dapat mengunduh pustaka Aspose.HTML untuk .NET dari situs web. Gunakan tautan berikut untuk mengakses halaman unduhan:[Unduh Aspose.HTML untuk .NET](https://releases.aspose.com/html/net/).

3.  Instalasi dan Lisensi: Setelah mengunduh pustaka, ikuti petunjuk instalasi yang tersedia dalam dokumentasi. Anda mungkin juga memerlukan lisensi yang valid untuk menggunakan beberapa fitur lanjutan. Anda dapat memperoleh lisensi dari situs web Aspose:[Beli Lisensi Aspose.HTML](https://purchase.aspose.com/buy).

4.  Uji Coba Gratis: Jika Anda ingin mencoba Aspose.HTML sebelum membeli lisensi, Anda bisa mendapatkan versi uji coba gratis dari tautan ini:[Uji Coba Gratis Aspose.HTML](https://releases.aspose.com/).

Sekarang setelah Anda memiliki prasyarat yang diperlukan, mari lanjutkan ke bagian berikutnya di mana kita akan mengimpor namespace yang diperlukan.

## Mengimpor Ruang Nama

Agar dapat bekerja dengan Aspose.HTML for .NET secara efektif, Anda perlu mengimpor namespace yang sesuai ke dalam proyek Anda. Di bawah ini, kami akan mencantumkan namespace yang Anda perlukan untuk contoh yang akan kami bahas:

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

Dengan namespace yang diimpor, Anda dapat mengakses fungsionalitas yang disediakan oleh Aspose.HTML untuk .NET.

## Nonaktifkan Eksekusi Skrip

Mari kita mulai dengan contoh dasar menonaktifkan eksekusi skrip dalam dokumen HTML dan mengonversinya ke PDF. Ikuti langkah-langkah berikut:

1. Buat potongan kode HTML dan simpan ke file bernama "document.html."

```csharp
var code = "<span>Hello World!!</span> " +
           "<script>document.write('Have a nice day!');</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Inisialisasi konfigurasi Aspose.HTML, tandai 'skrip' sebagai sumber daya yang tidak tepercaya.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    configuration.Security |= Aspose.Html.Sandbox.Scripts;
    
    // Inisialisasi dokumen HTML dengan konfigurasi yang ditentukan
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Konversi HTML ke PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

Dalam contoh ini, kami telah mencegah eksekusi skrip dalam dokumen HTML, memastikan keamanan saat mengonversinya ke PDF. Sekarang, mari kita beralih ke contoh berikutnya.

## Tentukan Stylesheet Pengguna

Terkadang, Anda mungkin ingin menerapkan gaya khusus ke elemen dalam dokumen HTML. Berikut cara melakukannya menggunakan Aspose.HTML untuk .NET:

1. Buat potongan kode HTML dan simpan ke file bernama "document.html."

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2.  Tetapkan warna khusus untuk`<span>` elemen menggunakan lembar gaya pengguna.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var userAgent = configuration.GetService<Aspose.Html.Services.IUserAgentService>();
    userAgent.UserStyleSheet = "span { color: green; }";
    
    // Inisialisasi dokumen HTML dengan konfigurasi yang ditentukan
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Konversi HTML ke PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

 Dalam contoh ini, kami telah menerapkan gaya khusus ke`<span>` elemen, mengatur warna teksnya menjadi hijau. Aspose.HTML untuk .NET memungkinkan Anda memanipulasi gaya dengan mudah.

## Batas Waktu Eksekusi JavaScript

Saat menangani kode JavaScript yang berpotensi memakan waktu, penting untuk menetapkan batas waktu guna mencegah eksekusi tanpa batas. Berikut cara melakukannya:

1. Buat potongan kode HTML dengan loop tak berujung dan simpan ke file bernama "document.html."

```csharp
var code = @"<script>while(true){}</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Tetapkan batas waktu eksekusi JavaScript menjadi 10 detik.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var runtime = configuration.GetService<Aspose.Html.Services.IRuntimeService>();
    runtime.JavaScriptTimeout = TimeSpan.FromSeconds(10);
    
    // Inisialisasi dokumen HTML dengan konfigurasi yang ditentukan
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Tunggu sampai semua skrip selesai/dibatalkan dan ubah HTML ke PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

Dalam contoh ini, kami membatasi waktu eksekusi JavaScript hingga 10 detik, memastikan skrip tidak berjalan tanpa batas, yang berpotensi menyebabkan masalah kinerja.

## Penanganan Pesan Kustom

Terkadang, Anda mungkin perlu menangani pesan kesalahan atau sumber daya yang hilang saat memuat dokumen HTML. Berikut ini contoh cara membuat penangan pesan kustom:

1. Buat potongan kode HTML dengan referensi file gambar yang hilang dan simpan ke file bernama "document.html."

```csharp
var code = @"<img src='missing.jpg'>";
System.IO.File.WriteAllText("document.html", code);
```

2. Tambahkan penanganan pesan kesalahan ke layanan jaringan untuk mencatat permintaan yang gagal.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var network = configuration.GetService<Aspose.Html.Services.INetworkService>();
    network.MessageHandlers.Add(new LogMessageHandler());
    
    // Inisialisasi dokumen HTML dengan konfigurasi yang ditentukan
    // Selama pemuatan dokumen, aplikasi akan mencoba memuat gambar, dan kita akan melihat hasil operasi ini di konsol.
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Konversi HTML ke PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

Dalam contoh ini, kami telah menambahkan penangan pesan khusus (`LogMessageHandler`) untuk mencatat informasi tentang permintaan yang gagal. Hal ini dapat sangat berguna untuk men-debug dan menangani sumber daya yang hilang dengan baik.

## Kesimpulan

Aspose.HTML untuk .NET adalah pustaka serbaguna yang memungkinkan pengembang bekerja dengan dokumen HTML secara efisien. Dalam tutorial ini, kami telah membahas konsep-konsep penting dan memberikan contoh langkah demi langkah untuk tugas-tugas umum, termasuk manajemen skrip, kustomisasi stylesheet, kontrol eksekusi JavaScript, dan penanganan pesan kustom.

Dengan mengikuti langkah-langkah yang diuraikan dalam tutorial ini, Anda dapat memanfaatkan kekuatan Aspose.HTML untuk .NET untuk membuat, memanipulasi, dan mengonversi dokumen HTML di aplikasi .NET Anda dengan percaya diri.

## Pertanyaan yang Sering Diajukan

### Q1: Dapatkah saya menggunakan Aspose.HTML untuk .NET tanpa membeli lisensi?

A1: Ya, Anda dapat mencoba Aspose.HTML untuk .NET dengan versi uji coba gratis, tetapi beberapa fitur lanjutan mungkin memerlukan lisensi yang valid.

### Q2: Bagaimana cara memperoleh lisensi Aspose.HTML untuk .NET?

 A2: Anda dapat membeli lisensi dari situs web Aspose:[Beli Lisensi Aspose.HTML](https://purchase.aspose.com/buy).

### Q3: Format apa yang dapat saya ubah ke dokumen HTML menggunakan Aspose.HTML untuk .NET?

A3: Aspose.HTML untuk .NET mendukung konversi ke berbagai format, termasuk PDF, gambar, dan banyak lagi.

### Q4: Apakah ada komunitas atau forum dukungan untuk Aspose.HTML for .NET?

 A4: Ya, Anda dapat menemukan bantuan dan dukungan di forum Aspose:[Forum Dukungan Aspose.HTML](https://forum.aspose.com/).

### Q5: Apakah Aspose.HTML untuk .NET menyediakan dokumentasi dan tutorial?

 A5: Ya, Anda dapat mengakses dokumentasinya di sini:[Dokumentasi Aspose.HTML untuk .NET](https://reference.aspose.com/html/net/).