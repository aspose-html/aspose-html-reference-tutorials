---
title: Menyempurnakan Konverter di .NET dengan Aspose.HTML
linktitle: Menyempurnakan Konverter di .NET
second_title: Aspose.HTML .NET API manipulasi HTML
description: Pelajari cara mengonversi HTML ke PDF, XPS, dan gambar dengan Aspose.HTML untuk .NET. Tutorial langkah demi langkah dengan contoh kode dan FAQ.
type: docs
weight: 16
url: /id/net/advanced-features/fine-tuning-converters/
---

## Perkenalan

Aspose.HTML untuk .NET adalah perpustakaan canggih yang memungkinkan pengembang memanipulasi dan mengonversi dokumen HTML dalam berbagai format. Baik Anda perlu mengonversi HTML ke PDF, XPS, atau gambar, atau melakukan tugas terkait HTML lainnya, Aspose.HTML menyediakan seperangkat alat canggih untuk membantu Anda menyelesaikan pekerjaan.

Dalam tutorial ini, kita akan menjelajahi beberapa fitur penting Aspose.HTML untuk .NET dan memberikan penjelasan langkah demi langkah untuk setiap contoh. Di akhir tutorial ini, Anda akan memiliki pemahaman yang kuat tentang cara menggunakan Aspose.HTML untuk .NET di aplikasi .NET Anda.

## Prasyarat

Sebelum kita mendalami contohnya, pastikan Anda memiliki prasyarat berikut:

-  Aspose.HTML untuk .NET: Anda harus menginstal pustaka Aspose.HTML untuk .NET. Anda dapat mengunduhnya dari[tautan unduhan](https://releases.aspose.com/html/net/).

- Lisensi Sementara (Opsional): Jika Anda tidak memiliki lisensi yang valid, Anda dapat memperoleh lisensi sementara dari[Di Sini](https://purchase.aspose.com/temporary-license/).

Sekarang, mari jelajahi beberapa kasus penggunaan umum dengan Aspose.HTML untuk .NET.

## Impor Namespace

Dalam kode C# Anda, mulailah dengan mengimpor namespace yang diperlukan:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## Konversi HTML ke PDF

### Langkah 1: Siapkan Kode HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Langkah 2: Inisialisasi Dokumen HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Langkah 3: Buat Perangkat PDF dan Tentukan File Output

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Langkah 4: Render HTML ke PDF

```csharp
document.RenderTo(device);
```

Contoh ini mengubah cuplikan HTML menjadi dokumen PDF. Anda dapat menyesuaikan kode HTML dan file keluaran sesuai kebutuhan.

## Tetapkan Ukuran Halaman Kustom

### Langkah 1: Siapkan Kode HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Langkah 2: Inisialisasi Dokumen HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Langkah 3: Buat Opsi Rendering PDF

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### Langkah 4: Buat Perangkat PDF dan Tentukan Opsi dan File Output

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Langkah 5: Render HTML ke PDF

```csharp
document.RenderTo(device);
```

Contoh ini menunjukkan cara mengatur ukuran halaman khusus untuk dokumen PDF yang dihasilkan.

## Sesuaikan Resolusi

### Langkah 1: Siapkan Kode HTML dan Simpan ke File

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Langkah 2: Inisialisasi Dokumen HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Langkah 3: Buat Opsi Rendering PDF untuk Resolusi Rendah

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### Langkah 4: Buat Perangkat PDF dan Tentukan Opsi dan File Output untuk Resolusi Rendah

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Langkah 5: Render HTML ke PDF untuk Resolusi Rendah

```csharp
document.RenderTo(device);
```

### Langkah 6: Buat Opsi Rendering PDF untuk Resolusi Tinggi

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### Langkah 7: Buat Perangkat PDF dan Tentukan Opsi dan File Output untuk Resolusi Tinggi

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Langkah 8: Render HTML ke PDF untuk Resolusi Tinggi

```csharp
document.RenderTo(device);
```

Contoh ini mengilustrasikan cara menyesuaikan resolusi saat merender HTML ke PDF, dengan mempertimbangkan layar beresolusi rendah dan tinggi.

## Tentukan Warna Latar Belakang

### Langkah 1: Siapkan Kode HTML dan Simpan ke File

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Langkah 2: Inisialisasi Dokumen HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Langkah 3: Inisialisasi Opsi Rendering PDF dengan Warna Latar Belakang

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### Langkah 4: Buat Perangkat PDF dan Tentukan Opsi dan File Output

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Langkah 5: Render HTML ke PDF

```csharp
document.RenderTo(device);
```

Contoh ini menunjukkan cara menentukan warna latar belakang saat mengonversi HTML ke PDF.

## Atur Ukuran Halaman Kiri dan Kanan

### Langkah 1: Siapkan Kode HTML

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### Langkah 2: Inisialisasi Dokumen HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Langkah 3: Buat Opsi Rendering PDF dengan Ukuran Halaman Kiri dan Kanan

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### Langkah 4: Buat Perangkat PDF dan Tentukan Opsi dan File Output

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Langkah 5: Render HTML ke PDF

```csharp
document.RenderTo(device);
```

Contoh ini menunjukkan cara mengatur ukuran halaman berbeda untuk halaman kiri dan kanan saat mengonversi HTML ke PDF.

## Sesuaikan Ukuran Halaman dengan Konten

### Langkah 1: Siapkan Kode HTML

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### Langkah 2: Inisialisasi Dokumen HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Langkah 3: Buat Opsi Rendering PDF

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Langkah 4: Buat Perangkat PDF dan Tentukan Opsi dan File Output

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Langkah 5: Render HTML ke PDF

```csharp
document.RenderTo(device);
```

Contoh ini menunjukkan cara menyesuaikan ukuran halaman ke konten terluas saat mengonversi HTML ke PDF.

## Tentukan Izin PDF

### Langkah 1: Siapkan Kode HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### Langkah 2: Inisialisasi Dokumen HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Langkah 3: Buat Opsi Rendering PDF dengan Izin

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### Langkah 4: Buat Perangkat PDF dan Tentukan Opsi dan File Output

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Langkah 5: Render HTML ke PDF

```csharp
document.RenderTo(device);
```

Contoh ini menunjukkan cara menentukan izin dan enkripsi saat mengonversi HTML ke PDF yang dilindungi.

## Tentukan Opsi Khusus Gambar

### Langkah 1: Siapkan Kode HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### Langkah 2: Inisialisasi Dokumen HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Langkah 3: Buat Opsi Rendering Gambar

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Langkah 4: Buat Perangkat Gambar dan Tentukan Opsi dan File Output

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Langkah 5: Render HTML ke Gambar

```csharp
document.RenderTo(device);
```

Contoh ini menunjukkan cara mengonversi HTML menjadi gambar dengan opsi rendering tertentu, seperti format, resolusi, dan mode penghalusan.

## Tentukan Opsi Rendering XPS

### Langkah 1: Siapkan Kode HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Langkah 2: Inisialisasi Dokumen HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Langkah 3: Buat Opsi Rendering XPS dengan Ukuran Halaman

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### Langkah 4: Buat Perangkat XPS dan Tentukan Opsi dan File Output

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### Langkah 5: Render HTML ke XPS

```csharp
document.RenderTo(device);
```

Contoh ini menunjukkan cara mengonversi HTML ke XPS dengan ukuran halaman khusus dan opsi rendering.

## Gabungkan Beberapa Dokumen HTML menjadi PDF

### Langkah 1: Siapkan Kode HTML untuk Banyak Dokumen

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### Langkah 2: Buat Dokumen HTML untuk Digabung

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### Langkah 3: Inisialisasi HTML Renderer

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Langkah 4: Buat Perangkat PDF untuk Output Gabungan

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Langkah 5: Gabungkan Dokumen HTML menjadi PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

Contoh ini menunjukkan cara menggabungkan beberapa dokumen HTML menjadi satu file PDF menggunakan Aspose.HTML untuk .NET.

## Setel Batas Waktu Rendering

### Langkah 1: Siapkan Kode HTML dengan JavaScript

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### Langkah 2: Inisialisasi Dokumen HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Langkah 3: Inisialisasi HTML Renderer

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Langkah 4: Buat Perangkat PDF dan Atur Batas Waktu Rendering

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Langkah 5: Render HTML ke PDF dengan Timeout

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

Contoh ini menunjukkan cara menyetel batas waktu rendering saat mengonversi HTML ke PDF, yang dapat berguna saat menangani konten dinamis atau skrip yang sudah berjalan lama.

## Kesimpulan

Aspose.HTML untuk .NET adalah perpustakaan serbaguna yang memberdayakan pengembang untuk bekerja dengan dokumen HTML secara efisien. Dalam tutorial ini, kami membahas berbagai contoh, mulai dari konversi HTML dasar ke PDF hingga fitur lebih lanjut seperti ukuran halaman khusus, resolusi, dan izin. Dengan mengikuti contoh berikut, Anda dapat memanfaatkan potensi penuh Aspose.HTML untuk .NET dalam aplikasi .NET Anda.

 Jika Anda memiliki pertanyaan atau memerlukan bantuan lebih lanjut, jangan ragu untuk mengunjungi[Forum Aspose.HTML](https://forum.aspose.com/) untuk dukungan dan bimbingan.

## FAQ

### Q1. Apa itu Aspose.HTML untuk .NET?
   
A1: Aspose.HTML untuk .NET adalah pustaka .NET yang memungkinkan pengembang memanipulasi dan mengonversi dokumen HTML secara terprogram. Ia menawarkan berbagai fitur untuk bekerja dengan konten HTML, termasuk HTML ke PDF, XPS, dan konversi gambar, serta opsi rendering tingkat lanjut.

### Q2. Di mana saya dapat mengunduh Aspose.HTML untuk .NET?

 A2: Anda dapat mengunduh Aspose.HTML untuk .NET dari[tautan unduhan](https://releases.aspose.com/html/net/).

### Q3. Apakah saya memerlukan lisensi untuk menggunakan Aspose.HTML untuk .NET?

A3: Meskipun Anda dapat menggunakan Aspose.HTML untuk .NET tanpa lisensi, disarankan untuk mendapatkan lisensi penggunaan produksi guna membuka kunci semua fitur dan menghapus tanda air atau batasan apa pun.

### Q4. Bagaimana cara melindungi file PDF saya yang dihasilkan dengan Aspose.HTML untuk .NET?

A4: Anda dapat menentukan izin PDF dan pengaturan enkripsi saat merender HTML ke PDF menggunakan Aspose.HTML untuk .NET. Ini memungkinkan Anda mengontrol siapa yang dapat mengakses dan memodifikasi file PDF yang dihasilkan.

### Q5. Bisakah saya mengonversi HTML ke format lain seperti XPS atau gambar?

A5: Ya, Aspose.HTML untuk .NET mendukung konversi HTML ke berbagai format, termasuk PDF, XPS, dan gambar (misalnya JPEG). Anda dapat menyesuaikan pengaturan konversi untuk memenuhi kebutuhan spesifik Anda.