---
title: Render HTML sebagai PNG di .NET dengan Aspose.HTML
linktitle: Render HTML sebagai PNG di .NET
second_title: Aspose.HTML .NET API manipulasi HTML
description: Belajar bekerja dengan Aspose.HTML untuk .NET. Memanipulasi HTML, mengonversi ke berbagai format, dan banyak lagi. Selami tutorial komprehensif ini!
type: docs
weight: 10
url: /id/net/rendering-html-documents/render-html-as-png/
---

Dalam tutorial ini, kita akan mempelajari dunia Aspose.HTML untuk .NET, alat canggih untuk bekerja dengan dokumen HTML secara terprogram. Baik Anda seorang pengembang berpengalaman atau baru memulai perjalanan Anda di dunia pemrograman .NET, tutorial ini akan memandu Anda memahami esensi Aspose.HTML, mulai dari mengimpor namespace hingga menguraikan contoh praktis.

## Perkenalan

Aspose.HTML untuk .NET adalah perpustakaan serbaguna yang memungkinkan pengembang memanipulasi dokumen HTML dengan mudah. Apakah Anda perlu mengonversi HTML ke format lain, mengekstrak data dari dokumen HTML, atau membuat konten HTML dinamis, Aspose.HTML siap membantu Anda. Dalam tutorial ini, kita akan mengeksplorasi kemampuannya langkah demi langkah.

## Prasyarat

Sebelum kita mendalami contoh kode, Anda memerlukan beberapa prasyarat:

1. Visual Studio: Pastikan Anda telah menginstal Visual Studio, karena kami akan menulis kode .NET.

2.  Aspose.HTML untuk .NET: Unduh dan instal perpustakaan Aspose.HTML untuk .NET dari[Link ini](https://releases.aspose.com/html/net/) . Anda dapat memilih antara uji coba gratis atau membeli lisensi[Di Sini](https://purchase.aspose.com/buy).

3. .NET Framework atau .NET Core: Pastikan Anda telah menginstal .NET Framework atau .NET Core di mesin pengembangan Anda, bergantung pada kebutuhan proyek Anda.

4. Editor Kode: Anda dapat menggunakan Visual Studio atau editor kode lain pilihan Anda.

## Mengimpor Namespace

Untuk memulai Aspose.HTML untuk .NET, pertama-tama kita perlu mengimpor namespace yang diperlukan. Buka proyek Anda di Visual Studio, buat kelas C# baru, dan impor namespace berikut:

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;
```

Namespace ini menyediakan akses ke berbagai kelas dan metode yang diperlukan untuk bekerja dengan dokumen HTML secara terprogram.

## Render HTML sebagai Contoh PNG

Mari kita lihat lebih dekat contoh kode yang Anda berikan dan bagi menjadi beberapa langkah:

```csharp
// Render HTML sebagai PNG di .NET dengan Aspose.HTML
string dataDir = "Your Data Directory";

// Langkah 1: Buat objek dokumen HTML
using (var document = new Aspose.Html.HTMLDocument("<style>p { color: green; }</style><p>my first paragraph</p>", @"c:\work\"))
{
    // Langkah 2: Buat penyaji HTML
    using (HtmlRenderer renderer = new HtmlRenderer())
    using (ImageDevice device = new ImageDevice(dataDir + @"document_out.png"))
    {
        // Langkah 3: Render dokumen HTML ke PNG
        renderer.Render(device, document);
    }
}
```

### Langkah 1: Buat Objek Dokumen HTML

 Pada langkah ini, kami membuat`HTMLDocument` objek, yang mewakili dokumen HTML. Anda dapat meneruskan konten HTML sebagai string ke konstruktor, dan Anda juga dapat menentukan jalur dasar untuk menyelesaikan jalur relatif.

### Langkah 2: Buat Perender HTML

 Di sini, kami membuat`HtmlRenderer` obyek. Ini adalah komponen inti yang bertanggung jawab untuk merender konten HTML. 

### Langkah 3: Render Dokumen HTML ke PNG

 Terakhir, kami merender dokumen HTML menjadi gambar PNG menggunakan`HtmlRenderer` dan sebuah`ImageDevice` . Gambar PNG yang dihasilkan akan disimpan di tempat yang ditentukan`dataDir`.

## Kesimpulan

Dalam tutorial ini, kami telah memperkenalkan Anda ke Aspose.HTML untuk .NET dan memberikan rincian kode contoh. Ini hanyalah permulaan dari apa yang dapat Anda capai dengan perpustakaan canggih ini. Anda dapat menjelajahi dokumentasinya yang ekstensif[Di Sini](https://reference.aspose.com/html/net/) dan mengakses sumber daya dan dukungan tambahan di[Asumsikan forum](https://forum.aspose.com/).

Jika Anda memiliki pertanyaan atau memerlukan bantuan dengan Aspose.HTML untuk .NET, jangan ragu untuk menghubungi komunitas Aspose atau lihat dokumentasi untuk panduan lebih lanjut.

## Pertanyaan yang Sering Diajukan (FAQ)

### Apa itu Aspose.HTML untuk .NET?
   Aspose.HTML untuk .NET adalah perpustakaan yang memungkinkan pengembang memanipulasi dan mengonversi dokumen HTML secara terprogram dalam aplikasi .NET.

### Bagaimana saya bisa mendapatkan lisensi sementara Aspose.HTML untuk .NET?
    Anda bisa mendapatkan lisensi sementara untuk Aspose.HTML untuk .NET[Di Sini](https://purchase.aspose.com/temporary-license/).

### Bisakah saya mengonversi HTML ke format lain menggunakan Aspose.HTML untuk .NET?
   Ya, Aspose.HTML untuk .NET menyediakan berbagai konverter untuk mengonversi HTML ke format seperti PDF, XPS, dan gambar.

### Apakah ada uji coba gratis yang tersedia untuk Aspose.HTML untuk .NET?
    Ya, Anda dapat mengunduh uji coba gratis Aspose.HTML untuk .NET[Di Sini](https://releases.aspose.com/).

### Di mana saya dapat menemukan tutorial dan dokumentasi lainnya?
   Anda dapat menjelajahi dokumentasi dan tutorial komprehensif di[Aspose.HTML untuk halaman dokumentasi .NET](https://reference.aspose.com/html/net/).