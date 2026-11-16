---
category: general
date: 2026-05-22
description: Atur lebar dan tinggi gambar saat mengonversi dokumen Word ke PNG. Pelajari
  cara mengekspor docx sebagai gambar dengan rendering berkualitas tinggi dalam tutorial
  langkah demi langkah.
draft: false
keywords:
- set image width height
- convert word to png
- save docx as png
- export docx as image
- how to render word
language: id
og_description: Atur lebar dan tinggi gambar saat mengonversi dokumen Word ke PNG.
  Tutorial ini menunjukkan cara mengekspor docx sebagai gambar dengan pengaturan kualitas
  tinggi.
og_title: Atur Lebar Tinggi Gambar Saat Mengonversi Word ke PNG – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-22'
  description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  headline: Set Image Width Height When Converting Word to PNG – Full Guide
  type: TechArticle
- description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  name: Set Image Width Height When Converting Word to PNG – Full Guide
  steps:
  - name: 1. Preserve Transparent Backgrounds
    text: 'If your Word document contains shapes with transparent backgrounds and
      you want to keep that transparency, set the `BackgroundColor` to `Color.Transparent`:'
  - name: 2. Render Only a Specific Range
    text: Sometimes you only need a paragraph or a table, not the whole page. Use
      `DocumentVisitor` to extract the node and render it separately. That’s a more
      advanced scenario, but it shows **how to render word** content at a granular
      level.
  - name: 3. Adjust DPI Dynamically
    text: 'If you need different DPI per page (e.g., high‑resolution for the cover
      page), modify `Resolution` inside the loop:'
  - name: 4. Batch Processing
    text: When converting dozens of documents, wrap the whole flow in a method and
      reuse the same `ImageRenderingOptions` instance. Re‑using the options object
      reduces allocation overhead.
  type: HowTo
tags:
- Aspose.Words
- C#
- Image Rendering
title: Atur Lebar dan Tinggi Gambar Saat Mengonversi Word ke PNG – Panduan Lengkap
url: /id/net/generate-jpg-and-png-images/set-image-width-height-when-converting-word-to-png-full-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Atur Lebar Tinggi Gambar Saat Mengonversi Word ke PNG – Panduan Lengkap

Pernah bertanya‑tanya bagaimana cara **set image width height** saat Anda **convert Word to PNG**? Anda bukan satu‑satunya. Banyak pengembang mengalami kebuntuan ketika ekspor default menghasilkan gambar yang buram atau dimensi yang salah, dan kemudian mereka menghabiskan berjam‑jam mencari solusi yang benar‑benar bekerja.

Dalam tutorial ini kami akan membahas solusi bersih, end‑to‑end yang menunjukkan **how to render word** dokumen sebagai gambar PNG, memungkinkan Anda **save docx as PNG** dengan kontrol lebar‑tinggi yang tepat dan antialiasing berkualitas tinggi. Pada akhir tutorial Anda akan memiliki cuplikan kode siap‑jalankan, pemahaman yang kuat tentang opsi API, dan beberapa tips profesional untuk menghindari jebakan umum.

## Apa yang Akan Anda Pelajari

- Muat file `.docx` menggunakan Aspose.Words for .NET.
- **Set image width height** dengan `ImageRenderingOptions`.
- **Export docx as image** (PNG) dengan antialiasing diaktifkan.
- Cara **convert word to png** untuk satu halaman atau seluruh dokumen.
- Tips untuk menangani dokumen besar, pertimbangan DPI, dan jalur sistem‑file.

Tanpa alat eksternal, tanpa kerumitan baris perintah—hanya kode C# murni yang dapat Anda sisipkan ke dalam proyek .NET apa pun.

## Prerequisites

Sebelum kita mulai, pastikan Anda memiliki hal‑hal berikut:

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| **.NET 6.0+** (atau .NET Framework 4.7.2) | Aspose.Words mendukung keduanya, tetapi runtime yang lebih baru memberikan kinerja yang lebih baik. |
| **Aspose.Words for .NET** paket NuGet (`Install-Package Aspose.Words`) | Menyediakan kelas `Document` dan mesin rendering. |
| Sebuah **Word document** (`.docx`) yang ingin Anda ubah menjadi PNG. | Sumber yang akan Anda konversi. |
| Pengetahuan dasar C# – Anda akan memahami pernyataan `using` dan inisialisasi objek. | Menjaga kurva pembelajaran tetap ringan. |

Jika Anda belum memiliki paket NuGet, jalankan perintah berikut di Package Manager Console:

```powershell
Install-Package Aspose.Words
```

Itu saja—setelah paket terpasang, Anda siap mulai menulis kode.

## Step 1: Load the Source Document

Hal pertama yang perlu Anda lakukan adalah menunjuk perpustakaan ke file Word yang ingin Anda transformasi.

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Load the .docx file from disk
Document doc = new Document(@"C:\MyFiles\input.docx");
```

**Mengapa ini penting:** Kelas `Document` membaca seluruh paket Word ke memori, memberi Anda akses ke halaman, gaya, dan semua hal lainnya. Jika jalur salah, Anda akan mendapatkan `FileNotFoundException`, jadi periksa kembali bahwa file ada dan jalur menggunakan backslash yang di‑escape (`\\`) atau string verbatim (`@`).

> **Pro tip:** Bungkus pemanggilan load dalam blok `try/catch` jika Anda mengharapkan file mungkin tidak ada saat runtime.

## Step 2: Configure Image Rendering Options (Set Image Width Height)

Sekarang masuk ke inti tutorial: **how to set image width height** agar PNG yang dihasilkan tidak terdistorsi atau berbintik. Kelas `ImageRenderingOptions` memberi Anda kontrol halus atas dimensi, DPI, dan smoothing.

```csharp
// Create rendering options and explicitly set width and height
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Desired output size in pixels
    Width = 1024,          // Set image width height: 1024px wide
    Height = 768,          // Set image width height: 768px tall

    // High‑quality antialiasing works on Windows, Linux, and macOS
    UseAntialiasing = true,

    // Optional: increase DPI for sharper output (default is 96)
    Resolution = 300
};
```

**Explanation of the key properties:**

- `Width` dan `Height` – Ini adalah dimensi piksel tepat yang Anda inginkan. Dengan mengaturnya, Anda **set image width height** secara langsung, menggantikan ukuran halaman default.
- `UseAntialiasing` – Mengaktifkan smoothing berkualitas tinggi untuk teks dan grafik vektor, yang penting ketika Anda **convert word to png** dan menginginkan tepi yang tajam.
- `Resolution` – DPI yang lebih tinggi menghasilkan lebih banyak detail, terutama untuk tata letak kompleks. Perhatikan penggunaan memori; gambar 300 DPI dapat menjadi besar.

> **Mengapa tidak hanya mengandalkan ukuran default?** Default menggunakan dimensi fisik halaman (mis., A4 pada 96 DPI). Itu sering menghasilkan gambar 794 × 1123 piksel—cukup untuk beberapa kasus tetapi tidak ketika Anda membutuhkan thumbnail UI tertentu atau pratinjau berukuran tetap.

## Step 3: Render and Save as PNG (Export Docx as Image)

Dengan dokumen dimuat dan opsi dikonfigurasi, Anda akhirnya dapat **export docx as image**. Metode `RenderToImage` melakukan pekerjaan berat.

```csharp
// Render the first page (page index 0) to a PNG file
doc.RenderToImage(@"C:\MyFiles\output.png", imageOptions);
```

Jika Anda ingin merender **the whole document** (semua halaman) ke dalam file PNG terpisah, lakukan perulangan atas koleksi halaman:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string outPath = $@"C:\MyFiles\page_{i + 1}.png";
    doc.RenderToImage(outPath, imageOptions, i);
}
```

**Apa yang terjadi di balik layar?** Renderer meraster setiap halaman menggunakan dimensi yang Anda berikan, menerapkan antialiasing, dan menulis aliran byte PNG ke disk. Karena PNG bersifat lossless, Anda mempertahankan fidelitas penuh tata letak Word asli.

**Output yang diharapkan:** File PNG yang tajam dengan tepat 1024 × 768 piksel (atau ukuran apa pun yang Anda tetapkan). Buka di penampil gambar apa pun dan Anda akan melihat konten Word dirender persis seperti yang muncul di dokumen asli, tetapi kini sebagai gambar bitmap.

## Advanced Tips & Variations

### 1. Preserve Transparent Backgrounds

Jika dokumen Word Anda berisi bentuk dengan latar belakang transparan dan Anda ingin mempertahankan transparansi tersebut, setel `BackgroundColor` ke `Color.Transparent`:

```csharp
imageOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### 2. Render Only a Specific Range

Kadang‑kadang Anda hanya membutuhkan sebuah paragraf atau tabel, bukan seluruh halaman. Gunakan `DocumentVisitor` untuk mengekstrak node dan merendernya secara terpisah. Itu adalah skenario yang lebih maju, tetapi menunjukkan **how to render word** konten pada tingkat granular.

### 3. Adjust DPI Dynamically

Jika Anda memerlukan DPI yang berbeda per halaman (mis., resolusi tinggi untuk halaman sampul), ubah `Resolution` di dalam perulangan:

```csharp
if (i == 0) imageOptions.Resolution = 600; // cover page
else imageOptions.Resolution = 300;
```

### 4. Batch Processing

Saat mengonversi puluhan dokumen, bungkus seluruh alur dalam sebuah metode dan gunakan kembali instance `ImageRenderingOptions` yang sama. Menggunakan kembali objek opsi mengurangi beban alokasi.

## Common Pitfalls & How to Avoid Them

| Gejala | Penyebab Kemungkinan | Solusi |
|--------|----------------------|--------|
| PNG buram meskipun DPI tinggi | `UseAntialiasing` dibiarkan `false` | Set `UseAntialiasing = true`. |
| Ukuran output tidak cocok dengan `Width`/`Height` | DPI tidak dipertimbangkan | Kalikan ukuran yang diinginkan dengan `Resolution / 96` atau sesuaikan `Resolution`. |
| Exception out‑of‑memory pada dokumen besar | Merender seluruh dokumen pada 300 DPI | Render satu halaman pada satu waktu, buang setiap gambar setelah disimpan. |
| PNG menampilkan latar putih pada gambar transparan | `BackgroundColor` tidak diatur | Set `imageOptions.BackgroundColor = Color.Transparent`. |

## Complete Working Example

Berikut adalah program mandiri yang dapat Anda salin‑tempel ke aplikasi console. Program ini mendemonstrasikan **convert word to png**, **save docx as png**, dan tentu saja **set image width height**.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;
using System.Drawing; // For Color

namespace WordToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            string inputPath = @"C:\MyFiles\input.docx";
            Document doc = new Document(inputPath);

            // 2️⃣ Configure rendering options (set image width height)
            ImageRenderingOptions options = new ImageRenderingOptions
            {
                Width = 1024,          // Desired pixel width
                Height = 768,          // Desired pixel height
                UseAntialiasing = true,
                Resolution = 300,
                BackgroundColor = Color.Transparent // Keep transparency if needed
            };

            // 3️⃣ Render the first page to PNG (export docx as image)
            string outputPath = @"C:\MyFiles\output.png";
            doc.RenderToImage(outputPath, options);

            Console.WriteLine($"✅ Document rendered successfully to {outputPath}");
            // Optional: render all pages
            //RenderAllPages(doc, options);
        }

        // Helper method for batch rendering (uncomment if needed)
        static void RenderAllPages(Document doc, ImageRenderingOptions options)
        {
            for (int i = 0; i < doc.PageCount; i++)
            {
                string pagePath = $@"C:\MyFiles\page_{i + 1}.png";
                doc.RenderToImage(pagePath, options, i);
                Console.WriteLine($"Page {i + 1} saved to {pagePath}");
            }
        }
    }
}
```

**Jalankan:** Bangun proyek, letakkan `input.docx` yang valid pada jalur yang Anda tentukan, dan jalankan. Anda akan melihat `output.png` tepat **1024 × 768** piksel, dirender dengan tepi yang halus.

## Related Tutorials

- [Cara Mengaktifkan Antialiasing Saat Mengonversi DOCX ke PNG/JPG](/html/english/net/generate-jpg-and-png-images/how-to-enable-antialiasing-when-converting-docx-to-png-jpg/)
- [convert docx to png – buat arsip zip tutorial c#](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)
- [Cara Menggunakan Aspose untuk Merender HTML ke PNG – Panduan Langkah‑per‑Langkah](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}