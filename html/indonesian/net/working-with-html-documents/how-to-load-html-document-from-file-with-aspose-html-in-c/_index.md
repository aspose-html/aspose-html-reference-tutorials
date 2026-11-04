---
category: general
date: 2026-09-10
description: Pelajari cara memuat dokumen HTML dari file menggunakan Aspose.HTML di
  C#. Termasuk opsi rendering gambar, opsi rendering teks, dan penangan sumber daya
  khusus.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- load html document from file
- Aspose.HTML rendering
- HTML to image conversion
- custom resource handler
- image rendering options
- text rendering options
language: id
lastmod: 2026-09-10
og_description: Muat dokumen HTML dari file menggunakan Aspose.HTML di C#. Panduan
  ini mencakup opsi rendering, penangan sumber daya khusus, dan kode lengkap yang
  dapat Anda jalankan hari ini.
og_image_alt: Code editor displaying how to load HTML document from file with Aspose.HTML
og_title: Muat dokumen HTML dari file dengan Aspose.HTML – panduan langkah demi langkah
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: Learn to load HTML document from file using Aspose.HTML in C#. Includes
    image rendering options, text rendering options, and a custom resource handler.
  headline: How to load HTML document from file with Aspose.HTML in C#
  type: TechArticle
tags:
- Aspose.HTML
- C#
- HTML rendering
title: Cara memuat dokumen HTML dari file dengan Aspose.HTML di C#
url: /id/net/working-with-html-documents/how-to-load-html-document-from-file-with-aspose-html-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara memuat dokumen HTML dari file dengan Aspose.HTML di C#

Jika Anda perlu **memuat dokumen HTML dari file** dan mengontrol proses rendering‑nya, tutorial ini menunjukkan solusi lengkap yang siap dijalankan. Anda akan melihat cara mengonfigurasi rendering gambar, mengaktifkan text hinting, dan menyediakan custom resource handler yang mengembalikan stream kosong untuk aset eksternal. Pada akhir panduan Anda dapat menyimpan HTML yang telah diproses ke dalam memory stream atau tujuan lain yang Anda inginkan.

Contoh ini menggunakan Aspose.HTML untuk .NET, sebuah pustaka yang menyederhanakan pemrosesan HTML, CSS, dan SVG tanpa mesin peramban. Tidak diperlukan alat eksternal, dan kode ini bekerja dengan .NET 6 atau yang lebih baru. Pastikan paket NuGet Aspose.HTML sudah terpasang sebelum memulai.

## Prasyarat

- .NET 6 SDK (atau versi .NET lain yang didukung oleh Aspose.HTML)
- Visual Studio 2022 atau IDE C# lainnya
- Paket NuGet Aspose.HTML untuk .NET (`Install-Package Aspose.HTML`)
- Sebuah file HTML bernama `input.html` yang ditempatkan di folder yang dapat direferensikan dari kode

## Langkah 1: Muat dokumen HTML dari file

Operasi pertama adalah membuat instance `HTMLDocument` yang membaca file sumber. Objek ini mewakili seluruh pohon DOM dan menyediakan metode untuk manipulasi lebih lanjut.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;
using System.IO;

// Load the HTML document from a file
var htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

**Mengapa ini penting:** Memuat file ke dalam `HTMLDocument` memberi Anda akses penuh ke struktur dokumen, gaya, dan sumber daya, yang kemudian dapat Anda render atau transformasi.

## Langkah 2: Siapkan opsi rendering gambar (Aspose.HTML rendering)

Jika Anda berencana meraster halaman nanti, mengonfigurasi rendering gambar meningkatkan kualitas visual. Antialiasing melicinkan tepi dan mengurangi artefak bergerigi.

```csharp
// Configure image rendering options
var imageOptions = new ImageRenderingOptions
{
    UseAntialiasing = true   // Enables smoother graphics
};
```

**Tip:** `UseAntialiasing` sangat berguna untuk grafik vektor dan teks yang akan diraster menjadi PNG atau JPEG.

## Langkah 3: Aktifkan text hinting (text rendering options)

Text hinting memengaruhi cara glyph disejajarkan dengan grid piksel, yang dapat membuat font berukuran kecil tampak lebih tajam.

```csharp
// Configure text rendering options
var textOptions = new TextOptions
{
    UseHinting = true   // Improves readability of rendered text
};
```

**Mengapa penting:** Saat Anda mengekspor HTML ke gambar, hinting mengurangi karakter yang blur dan memastikan tipografi konsisten di berbagai platform.

## Langkah 4: Buat custom resource handler (custom resource handler)

Sumber daya eksternal seperti font, gambar, atau skrip dapat direferensikan dalam HTML. `ResourceHandler` memungkinkan Anda mengontrol cara sumber daya tersebut diambil. Pada contoh ini handler mengembalikan `MemoryStream` kosong untuk setiap permintaan, sehingga secara efektif menghapus aset eksternal.

```csharp
// Custom resource handler that supplies empty streams
class MemoryResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info) => new MemoryStream();
}

// Instantiate the handler
var resourceHandler = new MemoryResourceHandler();
```

**Kapan digunakan:** Pola ini berguna untuk lingkungan dengan batasan keamanan, pengujian unit, atau ketika Anda hanya membutuhkan markup tanpa file eksternal.

## Langkah 5: Susun opsi penyimpanan HTML (HTML to image conversion)

Semua komponen—resource handler, pengaturan rendering, dan gaya font—dilekatkan pada objek `HtmlSaveOptions`. Objek ini memberi tahu Aspose.HTML cara men-serialize dokumen.

```csharp
var saveOptions = new HtmlSaveOptions
{
    ResourceHandler = resourceHandler,   // Use the custom handler
    WebFontStyle = WebFontStyle.Bold,    // Example of a font style override
    ImageRenderingOptions = imageOptions,
    TextOptions = textOptions
};
```

**Penjelasan:** `WebFontStyle` dapat memaksa gaya tertentu (misalnya, bold) untuk web font yang mungkin tidak tersedia. `ImageRenderingOptions` dan `TextOptions` yang kami konfigurasikan sebelumnya disuntikkan di sini, memastikan mereka memengaruhi rasterisasi apa pun yang terjadi kemudian.

## Langkah 6: Simpan dokumen ke memory stream (solusi lengkap)

Akhirnya, tulis HTML yang telah diproses ke dalam `MemoryStream`. Dari sini Anda dapat menulis stream ke file, mengirimnya melalui jaringan, atau meneruskannya ke API lain.

```csharp
using (var outputStream = new MemoryStream())
{
    // Save the HTML with all configured options
    htmlDoc.Save(outputStream, saveOptions);

    // At this point outputStream contains the HTML markup,
    // its (empty) resources, and the applied rendering settings.
    // Example: write the stream to a file for verification
    File.WriteAllBytes("output.html", outputStream.ToArray());
}
```

**Hasil:** `output.html` kini berisi markup yang sama dengan `input.html` tetapi semua sumber daya eksternal telah diganti dengan stream kosong, dan preferensi rendering telah disematkan ke dalam opsi penyimpanan.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua langkah menghasilkan program mandiri yang dapat Anda salin, tempel, dan jalankan.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // Step 1: Load the HTML document from a file
        var htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Image rendering options
        var imageOptions = new ImageRenderingOptions { UseAntialiasing = true };

        // Step 3: Text rendering options
        var textOptions = new TextOptions { UseHinting = true };

        // Step 4: Custom resource handler
        var resourceHandler = new MemoryResourceHandler();

        // Step 5: Save options with all settings
        var saveOptions = new HtmlSaveOptions
        {
            ResourceHandler = resourceHandler,
            WebFontStyle = WebFontStyle.Bold,
            ImageRenderingOptions = imageOptions,
            TextOptions = textOptions
        };

        // Step 6: Save to a memory stream and write to disk
        using (var outputStream = new MemoryStream())
        {
            htmlDoc.Save(outputStream, saveOptions);
            File.WriteAllBytes("output.html", outputStream.ToArray());
        }
    }
}

// Custom handler that returns empty streams for any resource request
class MemoryResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info) => new MemoryStream();
}
```

Menjalankan program ini menghasilkan `output.html` di direktori saat ini. Buka file tersebut di peramban untuk memastikan markup asli dimuat, tetapi gambar, font, atau skrip yang terhubung tidak ada (karena telah diganti dengan stream kosong).

## Pertanyaan umum dan kasus tepi

| Pertanyaan | Jawaban |
|----------|--------|
| **Bagaimana jika saya membutuhkan sumber daya asli alih‑alih stream kosong?** | Ganti `MemoryResourceHandler` dengan handler yang membaca file dari disk atau mengunduhnya melalui HTTP. |
| **Bisakah saya merender HTML langsung ke PNG atau JPEG?** | Ya. Gunakan `ImageRenderer` dengan `ImageRenderingOptions` dan `TextOptions` yang sama, lalu panggil `renderer.Render(page, outputStream, ImageFormat.Png)`. |
| **Apakah `WebFontStyle.Bold` wajib?** | Tidak. Itu hanya contoh cara mengganti gaya font. Hapus atau ubah menjadi `WebFontStyle.Normal` jika tidak memerlukan gaya paksa. |
| **Apakah ini bekerja pada .NET Core?** | Aspose.HTML mendukung .NET 5/6/7, sehingga kode yang sama dapat dijalankan pada proyek .NET Core. |
| **Bagaimana cara menangani file HTML besar secara efisien?** | Stream file ke `HTMLDocument` menggunakan konstruktor `FileStream` untuk menghindari memuat seluruh file ke memori sekaligus. |

## Kesimpulan

Anda kini tahu cara **memuat dokumen HTML dari file** menggunakan Aspose.HTML, mengonfigurasi **opsi rendering gambar** dan **opsi rendering teks**, serta menerapkan **custom resource handler** untuk mengontrol aset eksternal. Contoh lengkap menunjukkan cara menyimpan HTML yang telah diproses ke dalam memory stream, yang dapat Anda persist atau kirim sesuai kebutuhan.

Selanjutnya, Anda dapat menjelajahi **konversi HTML ke gambar** dengan mengganti `HtmlSaveOptions` menjadi `ImageRenderer`, atau bereksperimen dengan fitur **Aspose.HTML rendering** seperti media query CSS, dukungan SVG, dan ekspor PDF. Ekstensi‑ekstensi ini memungkinkan Anda membangun pipeline pemrosesan dokumen yang kaya sepenuhnya dalam C#.

Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Load HTML Using a Remote Server in .NET with Aspose.HTML](/html/english/net/html-document-manipulation/load-html-using-remote-server/)
- [Load HTML Using URL in .NET with Aspose.HTML](/html/english/net/html-document-manipulation/load-html-using-url/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}