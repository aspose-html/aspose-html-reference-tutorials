---
category: general
date: 2026-10-09
description: Buat instance ImageRenderingOptions untuk mengaktifkan antialiasing dan
  meningkatkan kualitas rendering grafis dalam aplikasi .NET.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create imagerenderingoptions instance
- ImageRenderingOptions
- antialiasing
- SmoothingMode
- graphics rendering
language: id
lastmod: 2026-10-09
og_description: Buat instance imagerenderingoptions untuk mengaktifkan antialiasing
  dan menghasilkan rendering grafis yang lebih halus di .NET. Ikuti panduan langkah
  demi langkah.
og_image_alt: Screenshot showing smooth edges after enabling antialiasing with ImageRenderingOptions
og_title: Buat instance ImageRenderingOptions – tingkatkan kualitas grafis di .NET
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  headline: Create imagerenderingoptions instance for high‑quality graphics rendering
  type: TechArticle
- description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  name: Create imagerenderingoptions instance for high‑quality graphics rendering
  steps:
  - name: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
    text: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
  - name: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
    text: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
  - name: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
    text: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
  type: HowTo
tags:
- .NET
- C#
- rendering
title: Buat instance ImageRenderingOptions untuk rendering grafis berkualitas tinggi
url: /id/net/canvas-and-image-manipulation/create-imagerenderingoptions-instance-for-high-quality-graph/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat instance imagerenderingoptions untuk rendering grafis berkualitas tinggi

Jika Anda perlu **membuat instance imagerenderingoptions** untuk menghasilkan grafis yang lebih halus, panduan ini menunjukkan cara melakukannya secara tepat. Dengan mengonfigurasi antialiasing Anda menghilangkan tepi bergerigi dan memperoleh output kelas profesional tanpa perpustakaan tambahan.

Anda akan belajar cara menginstansiasi `ImageRenderingOptions`, mengaktifkan antialiasing, dan melampirkan opsi tersebut ke mesin rendering seperti Aspose.Slides atau System.Drawing. Tutorial ini mengasumsikan Anda sudah familiar dengan sintaks dasar C# dan memiliki lingkungan pengembangan .NET yang siap.

## Prasyarat

- .NET 6.0 atau lebih baru (API tersedia di .NET Standard 2.0+)
- Referensi ke assembly yang berisi `ImageRenderingOptions` (misalnya, `Aspose.Slides.NET`)
- IDE seperti Visual Studio 2022 atau VS Code dengan ekstensi C#
- Pemahaman dasar tentang pipeline rendering grafis

## Langkah 1: Buat instance imagerenderingoptions

Operasi pertama adalah mengalokasikan objek `ImageRenderingOptions` baru. Objek ini berfungsi sebagai wadah untuk semua flag yang terkait dengan rendering.

```csharp
using Aspose.Slides;          // Replace with the appropriate namespace
using Aspose.Slides.Export;   // Needed for ImageRenderingOptions

// Step 1: Create the ImageRenderingOptions instance
ImageRenderingOptions imgOptions = new ImageRenderingOptions();
```

Membuat instance memberi Anda kontrol penuh atas cara vektor grafis di rasterisasi. Anda kemudian dapat mengaktifkan atau menonaktifkan fitur tertentu seperti antialiasing, mode rendering teks, atau kompresi gambar.

## Langkah 2: Aktifkan antialiasing untuk meningkatkan rendering grafis

Antialiasing memperhalus transisi antara warna piksel, mengurangi efek tangga pada garis diagonal atau melengkung. Properti `SmoothingMode` yang lebih lama sudah tidak direkomendasikan; `UseAntialiasing` adalah pendekatan modern yang disarankan.

```csharp
// Step 2: Turn on antialiasing for smoother output
imgOptions.UseAntialiasing = true;
```

Menetapkan `UseAntialiasing` ke `true` memberi tahu mesin rendering untuk menerapkan filter berkualitas tinggi selama rasterisasi. Flag ini bekerja untuk bentuk vektor maupun teks, memastikan konsistensi fidelitas visual di seluruh slide.

### Mengapa tidak menggunakan SmoothingMode?

`SmoothingMode` milik `System.Drawing.Graphics` dan hanya memengaruhi gambar GDI+. Saat Anda merender slide atau PDF melalui Aspose.Slides, `ImageRenderingOptions.UseAntialiasing` adalah satu‑satunya flag yang dihormati oleh pustaka. Menggunakan properti yang lebih baru menjamin kompatibilitas ke depan dan menghilangkan perilaku tak terduga pada platform non‑Windows.

## Langkah 3: Terapkan opsi ke operasi rendering

Setelah instance `ImageRenderingOptions` dikonfigurasi, berikan ke metode yang melakukan rendering sebenarnya. Di bawah ini contoh lengkap yang dapat dijalankan yang memuat presentasi, merender slide pertama sebagai PNG, dan menyimpan gambar dengan antialiasing diaktifkan.

```csharp
using System;
using Aspose.Slides;
using Aspose.Slides.Export;

class Program
{
    static void Main()
    {
        // Load a sample presentation
        using Presentation pres = new Presentation("sample.pptx");

        // Create and configure ImageRenderingOptions
        ImageRenderingOptions imgOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true   // Enable antialiasing
        };

        // Render the first slide to a PNG file
        Slide slide = pres.Slides[0];
        slide.GetThumbnail(2f, 2f, imgOptions)   // 2x scale for higher resolution
            .Save("slide1_antialiased.png", Export.SaveFormat.Png);

        Console.WriteLine("Slide rendered with antialiasing.");
    }
}
```

**Penjelasan baris kunci**

- `new Presentation("sample.pptx")` memuat file sumber.  
- `GetThumbnail(2f, 2f, imgOptions)` membuat bitmap slide dengan DPI dua kali lipat dari default sambil menerapkan opsi rendering yang Anda konfigurasikan.  
- PNG yang dihasilkan (`slide1_antialiased.png`) menampilkan kurva dan teks yang halus berkat `UseAntialiasing = true`.

### Output yang Diharapkan

Open `slide1_antialiased.png` di penampil gambar apa pun. Dibandingkan dengan rendering yang tidak menggunakan antialiasing, Anda akan memperhatikan:

- Sudut bulat pada bentuk muncul tanpa langkah bergerigi.  
- Tepi teks tajam namun lembut, menghilangkan artefak piksel.  
- Kualitas visual keseluruhan cocok dengan apa yang Anda lihat di tampilan PowerPoint asli.

## Langkah 4: Penyesuaian opsional untuk rendering grafis lanjutan

Walaupun antialiasing adalah flag yang paling umum, `ImageRenderingOptions` menawarkan kontrol tambahan:

| Property | Tujuan | Nilai tipikal |
|----------|--------|---------------|
| `UseHighQualityRendering` | Enables sub‑pixel rendering for text | `true` |
| `PixelFormat` | Determines color depth of the output bitmap | `PixelFormat.Format32bppArgb` |
| `ImageFormat` | Sets the target image format (PNG, JPEG, etc.) | `Export.SaveFormat.Png` |

Anda dapat menggabungkan pengaturan ini:

```csharp
imgOptions.UseHighQualityRendering = true;
imgOptions.PixelFormat = System.Drawing.Imaging.PixelFormat.Format32bppArgb;
```

**Pro tip:** Saat menghasilkan PDF skala besar atau PNG resolusi tinggi, tetap aktifkan `UseAntialiasing` tetapi pantau penggunaan memori. Antialiasing menambah beban pemrosesan ekstra, yang dapat terlihat pada mesin dengan spesifikasi rendah.

## Kesalahan umum dan cara menghindarinya

1. **Lupa mengirimkan opsi** – Metode rendering yang menerima `ImageRenderingOptions` akan mengabaikan antialiasing jika Anda memanggil overload tanpa parameter opsi. Selalu gunakan `GetThumbnail` tiga‑parameter atau metode setara.  
2. **Mencampur SmoothingMode dengan ImageRenderingOptions** – Menetapkan `Graphics.SmoothingMode` tidak berpengaruh pada rendering Aspose.Slides. Hanya mengandalkan `UseAntialiasing`.  
3. **Menggunakan versi pustaka yang usang** – `ImageRenderingOptions` diperkenalkan pada Aspose.Slides 20.5. Pastikan paket NuGet Anda terbaru; jika tidak, kelas tersebut mungkin tidak ada atau tidak memiliki properti `UseAntialiasing`.

## Kesimpulan

Anda kini tahu cara **membuat instance imagerenderingoptions**, mengaktifkan antialiasing, dan mengintegrasikan opsi ke dalam alur kerja rendering. Pendekatan ini menjamin rendering grafis yang lebih halus, menggantikan pengaturan `SmoothingMode` lama, dan bekerja secara konsisten di seluruh platform .NET.

Dari sini Anda dapat menjelajahi flag rendering tambahan, bereksperimen dengan skala DPI yang berbeda, atau menggabungkan teknik ini dengan ekspor PDF untuk aset kualitas cetak. Menguasai `ImageRenderingOptions` adalah fondasi pemrograman grafis .NET dengan fidelitas tinggi.

---


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat PNG dari HTML – Panduan Rendering C# Lengkap](/html/english/net/rendering-html-documents/create-png-from-html-full-c-rendering-guide/)
- [Buat gambar dari HTML di C# – Panduan Langkah‑per‑Langkah Lengkap](/html/english/net/rendering-html-documents/create-image-from-html-in-c-complete-step-by-step-guide/)
- [Buat teks kanvas – Panduan Lengkap Rendering Teks pada Gambar](/html/english/net/canvas-and-image-manipulation/create-canvas-text-full-guide-to-rendering-text-on-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}