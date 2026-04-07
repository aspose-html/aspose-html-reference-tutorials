---
category: general
date: 2026-04-06
description: Pelajari cara mengaktifkan antialiasing, mengatur lebar dan tinggi gambar,
  serta menyimpan dokumen sebagai PNG di C# – panduan singkat untuk mengekspor dokumen
  ke gambar.
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: id
og_description: Cara mengaktifkan antialiasing saat mengekspor dokumen ke gambar.
  Panduan ini menunjukkan cara mengatur lebar gambar, mengatur tinggi gambar, dan
  menyimpan dokumen sebagai PNG.
og_title: Cara Mengaktifkan Antialiasing – Ekspor Dokumen ke Gambar
tags:
- C#
- ImageRendering
- Antialiasing
title: Cara Mengaktifkan Antialiasing – Mengekspor Dokumen ke Gambar dengan C#
url: /id/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengaktifkan Antialiasing – Mengekspor Dokumen ke Gambar dalam C#

Pernah bertanya-tanya **bagaimana cara mengaktifkan antialiasing** saat mengubah dokumen menjadi gambar? Mungkin Anda mencoba pemanggilan cepat `Save` dan hasilnya terlihat bergerigi, terutama pada garis diagonal. Kabar baiknya, Anda tidak memerlukan ahli grafis—hanya beberapa baris C# dan opsi yang tepat.

Dalam tutorial ini kami akan menjelaskan cara mengatur lebar gambar, mengatur tinggi gambar, dan akhirnya **menyimpan dokumen sebagai PNG** sehingga Anda dapat **mengekspor dokumen ke gambar** dengan tepi yang halus. Pada akhir tutorial Anda akan memiliki potongan kode siap‑jalankan yang menghasilkan PNG 800 × 600 yang tajam dengan antialiasing diaktifkan.

## Prasyarat

- .NET 6.0 atau yang lebih baru (kode ini juga bekerja pada .NET Framework 4.7+)
- Referensi ke perpustakaan rendering yang mendukung `ImageRenderingOptions` (misalnya, Aspose.Words, Syncfusion, atau API apa pun yang menyediakan properti serupa)
- Pemahaman dasar tentang sintaks C#

Tidak ada pengaturan berat—cukup tambahkan paket NuGet dan Anda siap melanjutkan.

## Langkah 1: Instal Perpustakaan Rendering

Pertama, tarik paket ke dalam proyek Anda. Jika Anda menggunakan Aspose.Words, jalankan:

```bash
dotnet add package Aspose.Words
```

> **Pro tip:** Jaga versi perpustakaan tetap terbaru; rilis terbaru (per April 2026) menambahkan penyesuaian kinerja untuk antialiasing.

## Langkah 2: Buat Objek Document

Muat atau buat dokumen yang ingin Anda render. Berikut contoh minimal yang membuat dokumen satu halaman dengan paragraf sederhana:

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

Kelas `Document` adalah titik masuk; semua yang Anda render berasal darinya. Pada proyek nyata Anda mungkin akan memuat .docx yang sudah ada:

```csharp
// Document doc = new Document("input.docx");
```

## Langkah 3: Tentukan Opsi Rendering (Lebar, Tinggi, Antialiasing)

Sekarang kami menjawab pertanyaan utama: **bagaimana cara mengaktifkan antialiasing**. Objek `ImageRenderingOptions` memungkinkan Anda mengaktifkan smoothing dan mengontrol dimensi.

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

Perhatikan komentar: mereka secara eksplisit menyebutkan **set image width**, **set image height**, dan **UseAntialiasing**—tiga pengaturan yang paling penting ketika Anda menginginkan PNG yang halus.

### Mengapa Antialiasing Penting

Tanpa antialiasing, garis diagonal dan kurva muncul berbentuk tangga karena renderer memperlakukan setiap piksel sebagai hidup atau mati. Mengaktifkannya mencampur piksel tepi, menghasilkan pelembutan visual yang meniru apa yang Anda lihat di editor foto. Trade‑off-nya adalah peningkatan waktu pemrosesan yang sangat kecil, namun untuk kebanyakan ekspor berorientasi UI hal ini dapat diabaikan.

## Langkah 4: Simpan Dokumen sebagai PNG (Ekspor Dokumen ke Gambar)

Dengan opsi yang siap, akhirnya kami **menyimpan dokumen sebagai PNG**. Metode `Save` menerima jalur file dan opsi yang baru saja kami konfigurasikan.

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

Itu saja—dokumen Anda kini menjadi PNG 800 × 600 dengan antialiasing diterapkan. Jika Anda membuka `output.png`, Anda akan melihat teks bersih, garis halus, dan tidak ada artefak bergerigi.

### Memverifikasi Hasil

Anda dapat dengan cepat memeriksa file di penampil gambar apa pun. Perhatikan:

- Dimensi yang tepat (800 × 600)
- Tidak ada tepi berbentuk tangga yang terlihat pada teks atau bentuk apa pun
- Latar belakang transparan jika dokumen Anda tidak memiliki warna latar (sebagian besar perpustakaan default ke putih)

Jika gambar terlihat bergerigi, periksa kembali bahwa `UseAntialiasing = true` tidak ditimpa di tempat lain.

## Langkah 5: Kasus Tepi & Variasi

### Mengubah Format Output

Ingin JPEG alih-alih PNG? Cukup ubah ekstensi file dan, bila perlu, sesuaikan kompresi:

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### Mengekspor Beberapa Halaman

Ketika dokumen sumber memiliki beberapa halaman, renderer secara default membuat file gambar terpisah per halaman. Anda dapat melakukan loop melalui halaman:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### Menyimpan ke Stream (mis., respons HTTP)

Jika Anda membangun API web, Anda mungkin ingin mengembalikan PNG secara langsung:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap disalin‑tempel yang menggabungkan setiap langkah yang dibahas:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

Menjalankan program ini menghasilkan `output.png` di folder executable. Buka file tersebut, dan Anda akan melihat PNG 800 × 600 yang halus—tepat seperti yang kami targetkan.

## Pertanyaan Umum & Pemecahan Masalah

- **Bagaimana jika gambar terlihat buram?**  
  Buram dapat terjadi ketika Anda memperbesar halaman sumber yang kecil. Jaga ukuran halaman sumber mendekati dimensi target, atau tingkatkan DPI melalui `imageOptions.Resolution` (misalnya, `Resolution = 300`).

- **Apakah ini bekerja pada .NET Framework?**  
  Ya. API yang sama tersedia di framework klasik; cukup referensikan DLL yang sesuai.

- **Bisakah saya mengontrol warna latar belakang?**  
  Tentu saja. Atur `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` sebelum menyimpan.

- **Apakah antialiasing dipercepat oleh hardware?**  
  Kebanyakan perpustakaan melakukan antialiasing secara perangkat lunak. Jika Anda memerlukan akselerasi GPU, cari mesin rendering yang secara eksplisit mendukungnya.

## Kesimpulan

Kami telah membahas **bagaimana cara mengaktifkan antialiasing** saat Anda **mengekspor dokumen ke gambar**, menjelaskan **set image width** dan **set image height**, serta menunjukkan langkah‑langkah tepat untuk **menyimpan dokumen sebagai PNG**. Potongan kode di atas siap untuk produksi, dan Anda kini dapat menyesuaikannya ke JPEG, PDF multi‑halaman, atau bahkan mengalirkan gambar langsung ke klien.

Selanjutnya, Anda mungkin ingin menjelajahi penambahan watermark, menyesuaikan DPI untuk output kualitas cetak, atau mengintegrasikan logika ini ke dalam endpoint ASP.NET Core. Prinsip yang sama berlaku—cukup ganti jalur file dengan stream respons.

Selamat coding, dan nikmati gambar yang tajam dan antialias!

![PNG yang Dirender dengan antialiasing diaktifkan](output.png "PNG yang Dirender dengan antialiasing diaktifkan")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}