---
category: general
date: 2025-12-29
description: Buat dokumen HTML dalam C# dan pelajari cara mengatur keluarga font,
  mengatur ukuran font, lalu menyimpan HTML sebagai PDF atau mengonversi HTML ke PDF
  menggunakan Aspose.HTML.
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: id
og_description: Buat dokumen HTML dalam C# dan langsung lihat cara mengatur jenis
  font, mengatur ukuran font, kemudian menyimpan HTML sebagai PDF atau mengonversi
  HTML ke PDF dengan Aspose.HTML.
og_title: Buat Dokumen HTML – Teks Bergaya & Ekspor PDF
tags:
- aspnet
- csharp
- pdf-generation
title: Buat Dokumen HTML dengan Teks Bergaya dan Ekspor ke PDF – Panduan Lengkap
url: /id/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Dokumen HTML dengan Teks Bergaya dan Ekspor ke PDF

Pernahkah Anda perlu **create HTML document** secara cepat dan mengubahnya menjadi PDF tanpa meninggalkan kode C# Anda? Mungkin Anda sedang membangun mesin pelaporan, generator faktur, atau sekadar preview cepat untuk pengguna. Kabar baiknya, Anda dapat melakukannya dalam beberapa baris kode menggunakan Aspose.HTML, dan Anda akan mendapatkan kontrol penuh atas font family, font size, bahkan gaya bold‑italic.

Dalam tutorial ini kami akan membimbing Anda melalui seluruh proses—dari membuat dokumen HTML di memori hingga menyimpannya sebagai file PDF. Pada akhir tutorial Anda akan tahu persis cara **set font family**, **set font size**, dan **save HTML as PDF** (atau **convert HTML to PDF**) dengan contoh kode yang bersih dan siap produksi.

## Apa yang Anda Butuhkan

- .NET 6+ (API ini bekerja dengan .NET Core dan .NET Framework)  
- Paket NuGet Aspose.HTML for .NET (`Aspose.Html`) – instal via `dotnet add package Aspose.Html`  
- Sebuah folder di disk tempat PDF yang dihasilkan dapat ditulis  

Tidak ada template HTML tambahan, tidak ada konverter eksternal, hanya C# murni.

![create html document illustration](/images/create-html-document.png){alt="contoh pembuatan dokumen html"}

## Langkah 1: Buat Dokumen HTML

Pertama, kita memerlukan objek dokumen HTML kosong. Anggap saja ini sebagai kanvas bersih yang nanti akan Anda isi dengan paragraf bergaya.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**Mengapa ini penting:** `HTMLDocument` memberi Anda struktur mirip DOM yang dapat dimanipulasi secara programatik. Tidak perlu menyentuh string mentah atau I/O file sampai tahap akhir.

## Langkah 2: Tambahkan Paragraf dan Atur Font Family & Font Size

Sekarang kita akan membuat elemen `<p>`, menyisipkan teks, dan secara eksplisit menentukan font family serta ukuran font. Di sinilah kata kunci **set font family** dan **set font size** berperan.

```csharp
// Step 2 – create a <p> element with some sample text
HtmlElement paragraph = htmlDocument.CreateElement("p");
paragraph.InnerHtml = "Bold & Italic text";

// Define the base font style
paragraph.Style.FontFamily = "Arial";   // set font family
paragraph.Style.FontSize = "18px";      // set font size

// Attach the paragraph to the document body
body.AppendChild(paragraph);
```

**Tips Pro:** Jika Anda memerlukan fallback web‑safe, Anda dapat memberikan daftar dipisahkan koma seperti `"Arial, Helvetica, sans-serif"`; browser (atau Aspose) akan memilih font pertama yang tersedia.

## Langkah 3: Terapkan Gaya Bold dan Italic dengan Flag WebFontStyle

Aspose.HTML menyediakan enum yang berguna `WebFontStyle` yang memungkinkan Anda menggabungkan gaya dengan operasi OR bitwise. Mari buat teks menjadi **bold** **dan** italic.

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**Apa yang terjadi di balik layar?** Properti `FontStyle` diterjemahkan menjadi deklarasi CSS `font-weight` dan `font-style`. Dengan meng‑OR flag‑flag tersebut kita menghindari penulisan dua baris CSS terpisah.

## Langkah 4: Konversi HTML ke PDF (Simpan HTML sebagai PDF)

Langkah terakhir adalah konversi sebenarnya. Dengan satu panggilan ke `Save`, Aspose.HTML merender DOM dan menulis file PDF ke disk. Ini memenuhi kebutuhan **save html as pdf** dan **convert html to pdf**.

```csharp
// Step 4 – save the HTML document as a PDF file
string outputPath = @"C:\Temp\styled.pdf";
htmlDocument.Save(outputPath, new PDFSaveOptions());

// Optional: open the PDF automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Hasil yang diharapkan:** Buka `styled.pdf` dan Anda akan melihat satu paragraf berisi “Bold & Italic text” dengan ukuran 18‑px Arial, ditampilkan bold dan italic. Dimensi PDF sesuai halaman A4 standar, dan teks dapat dipilih—berkat rendering vektor.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang siap dijalankan:

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new HTML document
        HTMLDocument htmlDocument = new HTMLDocument();
        HTMLBodyElement body = htmlDocument.Body;

        // 2️⃣ Add a styled paragraph
        HtmlElement paragraph = htmlDocument.CreateElement("p");
        paragraph.InnerHtml = "Bold & Italic text";

        // Set font family and size
        paragraph.Style.FontFamily = "Arial";
        paragraph.Style.FontSize = "18px";

        // 3️⃣ Apply bold + italic
        paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // Append to body
        body.AppendChild(paragraph);

        // 4️⃣ Save as PDF (convert HTML to PDF)
        string outputFile = @"C:\Temp\styled.pdf";
        htmlDocument.Save(outputFile, new PDFSaveOptions());

        Console.WriteLine($"PDF generated at: {outputFile}");
    }
}
```

### Menjalankan kode

1. Instal paket NuGet Aspose.HTML:  
   ```bash
   dotnet add package Aspose.Html
   ```
2. Ganti `C:\Temp\styled.pdf` dengan folder yang Anda miliki hak tulisnya.  
3. Build dan jalankan: `dotnet run`.  

Anda akan melihat pesan konsol yang mengonfirmasi lokasi file, dan PDF akan berisi paragraf bergaya.

## Pertanyaan Umum & Kasus Tepi

- **Bagaimana jika saya membutuhkan font web khusus?**  
  Muat font dengan `HTMLFontFaceRule` atau referensikan file CSS `@font-face` remote sebelum membuat paragraf.

- **Bisakah saya menambahkan gambar sebelum konversi?**  
  Tentu saja. Gunakan `HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");` dan set `img.Source` ke path lokal atau data URI.

- **Bagaimana dengan PDF multi‑halaman?**  
  Tambahkan lebih banyak elemen (tabel, div, dll.) dan Aspose.HTML akan otomatis mem-paginate ketika konten melebihi tinggi halaman.

- **Apakah ada cara mengontrol metadata PDF?**  
  Berikan instance `PdfSaveOptions` dan set properti seperti `Author`, `Title`, atau `PdfAConformanceLevel`.

## Ringkasan

Kami telah membahas cara **create HTML document** di C#, **set font family**, **set font size**, menerapkan gaya bold‑italic, dan akhirnya **save HTML as PDF**—secara efektif **convert HTML to PDF** dengan Aspose.HTML. Potongan kode ini cukup singkat untuk disisipkan ke proyek .NET apa pun, namun cukup lengkap untuk menjadi fondasi yang solid bagi skenario pelaporan yang lebih kompleks.

## Langkah Selanjutnya

- Bereksperimen dengan kelas CSS untuk styling yang dapat digunakan kembali.  
- Gabungkan beberapa paragraf, tabel, dan gambar untuk membangun PDF yang lebih kaya.  
- Jelajahi kepatuhan PDF/A jika Anda memerlukan dokumen tingkat arsip.  

Silakan ubah font, ukuran, atau warna—tidak ada batasan apa yang dapat Anda hasilkan secara programatis. Selamat coding, dan semoga PDF Anda selalu ter‑render persis seperti yang Anda bayangkan!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}