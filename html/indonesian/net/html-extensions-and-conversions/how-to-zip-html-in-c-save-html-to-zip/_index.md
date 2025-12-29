---
category: general
date: 2025-12-29
description: Cara Mengompres HTML menjadi ZIP di C# dengan cepat menggunakan Aspose.HTML
  – simpan HTML ke dalam zip dengan ZipResourceHandler khusus. Pelajari langkah demi
  langkah.
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: id
og_description: Cara Mengompres HTML menjadi ZIP di C# dengan cepat menggunakan Aspose.HTML.
  Ikuti panduan ini untuk menyimpan HTML ke dalam zip dan membuat arsip zip dengan
  penanganan sumber daya khusus.
og_title: Cara Mengompres HTML menjadi Zip di C# – Simpan HTML ke Zip
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: Cara Mengompres HTML menjadi Zip di C# – Simpan HTML ke Zip
url: /id/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengompres HTML menjadi Zip di C# – Menyimpan HTML ke Zip

Mengompres HTML menjadi Zip di C# adalah kebutuhan umum ketika Anda ingin mengemas halaman web untuk penggunaan offline. Baik Anda menggabungkan satu halaman beserta gambarnya atau mengekspor seluruh situs, **menyimpan HTML ke zip** membuat semuanya rapi dan dapat dipindahkan. Dalam tutorial ini kami akan membimbing Anda melalui solusi lengkap yang siap dijalankan, yang tidak hanya mengompres markup HTML tetapi juga menyalurkan setiap sumber daya yang direferensikan langsung ke dalam arsip.

Anda akan belajar cara:

* Membuat arsip zip secara programatis dengan `System.IO.Compression` milik .NET.
* Menyisipkan `ResourceHandler` kustom ke Aspose.HTML sehingga sumber daya mengalir langsung ke zip.
* Menangani kasus khusus seperti file zip yang sudah ada dan aset biner berukuran besar.

Tidak memerlukan alat eksternal—hanya C#, Aspose.HTML, dan beberapa baris kode.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki:

* **.NET 6+** (kode ini juga berfungsi pada .NET Framework 4.6.2 dan yang lebih baru).
* **Aspose.HTML for .NET** – Anda dapat mengunduh trial gratis dari situs Aspose atau menggunakan salinan berlisensi.
* Lingkungan pengembangan (Visual Studio, VS Code, Rider—sesuai pilihan Anda).

Itu saja. Tidak ada paket NuGet tambahan selain `System.IO.Compression` (sudah termasuk dalam .NET) dan `Aspose.HTML`.

## Langkah 1: Siapkan Proyek dan Import

Buat proyek konsol baru (atau letakkan kode ke dalam proyek yang sudah ada). Tambahkan direktif `using` yang diperlukan di bagian atas file Anda:

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **Tips pro:** Jika Anda menggunakan Visual Studio, IDE akan menyarankan penambahan paket NuGet yang hilang untuk `Aspose.Html`. Setujui, dan Anda siap melanjutkan.

## Langkah 2: Implementasikan ZipResourceHandler Kustom

Aspose.HTML memanggil sebuah `ResourceHandler` setiap kali ia perlu menulis sebuah sumber daya (seperti gambar, file CSS, atau skrip). Dengan menimpa `HandleResource`, kita dapat menentukan secara tepat ke mana setiap sumber daya disimpan. Handler di bawah ini membuat entri zip yang mencerminkan jalur logis sumber daya, kemudian mengembalikan stream yang dapat ditulis langsung ke entri tersebut.

```csharp
/// <summary>
/// Streams each HTML resource straight into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Ensure the entry's directory structure exists inside the zip.
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        // The returned stream writes directly into the zip entry.
        return entry.Open();
    }
}
```

**Mengapa ini penting:**  
Alih‑alih menulis sumber daya ke folder sementara lalu mengompres folder tersebut, handler ini menyalurkan data secara langsung, mengurangi I/O disk dan menjaga penggunaan memori tetap rendah. Ia juga memastikan bahwa hierarki folder internal zip cocok dengan jalur relatif HTML, yang diharapkan browser saat Anda mengekstrak dan membuka halaman.

## Langkah 3: Siapkan Arsip Zip

Sekarang kita akan membuka (atau membuat) file zip target. Flag `FileMode.Create` akan menimpa file yang sudah ada—sempurna untuk build yang dapat diulang. Jika Anda lebih suka mempertahankan arsip yang sudah ada, ubah menjadi `FileMode.OpenOrCreate` dan tangani entri duplikat sesuai kebutuhan.

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **Kasus khusus:** Jika proses crash sebelum blok `using` membuang arsip, Anda mungkin akan mendapatkan zip yang korup. Menjalankan kode di dalam `try/catch` dan menghapus file yang hanya sebagian dibuat saat terjadi kegagalan adalah langkah pencegahan sederhana.

## Langkah 4: Bangun Dokumen HTML dengan Sumber Daya Tersemat

Untuk demonstrasi, kita akan membuat halaman HTML kecil yang mereferensikan gambar bernama `image.png`. Pada skenario dunia nyata Anda akan memuat HTML dari file atau string yang berasal dari basis data.

```csharp
// Sample HTML containing an <img> tag.
// Aspose.HTML will ask the ResourceHandler for "image.png".
string htmlContent = @"
<html>
<head><title>Sample Zip</title></head>
<body>
    <h1>Hello, zipped world!</h1>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

// Create the document from the string.
var html = new HTMLDocument(htmlContent);
```

Jika Anda memiliki file gambar nyata di disk, Anda dapat menambahkannya ke zip secara manual sebelum menyimpan HTML, atau membiarkan Aspose.HTML mengambilnya melalui handler (misalnya, dari URL). Handler yang kami buat berfungsi untuk jalur lokal maupun URL remote.

## Langkah 5: Konfigurasikan Opsi Penyimpanan untuk Menggunakan ZipResourceHandler

Sekarang kita beri tahu Aspose.HTML untuk menggunakan handler kustom kami saat menulis sumber daya. Kelas `HTMLSaveOptions` juga memungkinkan Anda menentukan nama file output di dalam zip (secara default adalah `index.html`).

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## Langkah 6: Simpan Dokumen – Semua Mengalir ke Zip

Akhirnya, panggil `Save`. Aspose.HTML akan mem-parsing markup, menemukan tag `<img>`, memanggil `HandleResource` untuk `image.png`, dan menulis baik file HTML maupun gambar ke dalam arsip zip yang sama.

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

Saat blok `using` selesai, `ZipArchive` akan memfinalisasi file, menjadikannya siap didistribusikan.

### Contoh Lengkap yang Berfungsi

Berikut adalah seluruh program yang telah digabungkan. Salin‑tempel ke `Program.cs` dan jalankan—tidak perlu modifikasi lebih lanjut.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare the zip file.
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);
        using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);

        // 2️⃣ Build a simple HTML document with an image reference.
        string htmlContent = @"
        <html>
        <head><title>Sample Zip</title></head>
        <body>
            <h1>Hello, zipped world!</h1>
            <img src='image.png' alt='Demo image'>
        </body>
        </html>";
        var html = new HTMLDocument(htmlContent);

        // 3️⃣ Set save options to stream resources into the zip.
        var saveOptions = new HTMLSaveOptions
        {
            OutputFileName = "index.html",
            OutputStorage = new ZipResourceHandler(zip)
        };

        // 4️⃣ Save – everything ends up in output.zip.
        html.Save(saveOptions);
        Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
    }
}
```

**Hasil yang diharapkan:** Setelah eksekusi, `output.zip` berisi dua entri:

```
index.html
image.png
```

Jika Anda mengekstrak file tersebut dan membuka `index.html` di browser, gambar akan tampil dengan benar karena jalur relatifnya tetap terjaga.

## Pertanyaan yang Sering Diajukan

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}