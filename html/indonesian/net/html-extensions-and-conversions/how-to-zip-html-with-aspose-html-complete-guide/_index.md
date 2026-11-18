---
category: general
date: 2026-03-21
description: Pelajari cara mengompres file HTML beserta gambar menggunakan Aspose.HTML.
  Panduan ini mencakup penangan sumber daya khusus, menyimpan HTML sebagai zip, dan
  opsi penyimpanan Aspose HTML.
draft: false
keywords:
- how to zip html
- save html with images
- custom resource handler
- save html as zip
- aspose html save options
language: id
og_description: Pelajari cara mengompres HTML dengan gambar menggunakan Aspose.HTML.
  Tutorial ini menunjukkan penangan sumber daya khusus, menyimpan HTML sebagai zip,
  dan opsi penyimpanan Aspose HTML terbaik.
og_title: Cara Mengompres HTML dengan Aspose.HTML – Panduan Lengkap
tags:
- Aspose.HTML
- C#
- ZIP
- HTML processing
title: Cara Mengompres HTML dengan Aspose.HTML – Panduan Lengkap
url: /id/net/html-extensions-and-conversions/how-to-zip-html-with-aspose-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengompres HTML dengan Aspose.HTML – Panduan Lengkap

Pernah bertanya-tanya **cara mengompres HTML** yang berisi sumber daya eksternal seperti gambar, CSS, atau JavaScript? Anda bukan satu-satunya. Dalam banyak proyek kami perlu mengirimkan satu paket yang mempertahankan tata letak halaman, dan mengompres HTML bersama aset‑asetsnya adalah solusi paling rapi.  

Dalam tutorial ini kami akan menunjukkan **cara mengompres HTML** menggunakan pustaka kuat Aspose.HTML, dan kami akan menelusuri setiap langkah—dari membuat custom resource handler hingga mengonfigurasi `ZipArchiveSaveOptions`. Pada akhir tutorial Anda akan dapat *menyimpan HTML dengan gambar* di dalam arsip ZIP, dan Anda akan memahami pola **custom resource handler** yang membuat semuanya mungkin.

Kami juga akan menyentuh topik terkait seperti **save HTML as zip**, menjelajahi **Aspose HTML save options** yang relevan, dan memberi Anda tip untuk menangani kasus tepi. Tidak memerlukan dokumentasi eksternal—semua yang Anda butuhkan ada di sini.

---

## Apa yang Anda Butuhkan

- **.NET 6+** (atau runtime .NET terbaru yang mendukung Aspose.HTML)
- **Aspose.HTML for .NET** paket NuGet (versi 23.9 atau lebih baru)
- Lingkungan pengembangan C# dasar (Visual Studio, Rider, atau VS Code)
- File gambar (`image.png`) yang ditempatkan di folder yang sama dengan kode sumber (atau sumber daya eksternal lain yang ingin Anda bundel)

Itu saja—tidak ada alat tambahan, tidak ada langkah build yang rumit. Siap? Mari kita mulai.

---

## Langkah 1: Instal Aspose.HTML melalui NuGet

Pertama, tambahkan pustaka Aspose.HTML ke proyek Anda. Buka terminal di folder proyek dan jalankan:

```bash
dotnet add package Aspose.HTML
```

*Tip pro:* Jika Anda menggunakan Visual Studio, Anda juga dapat klik kanan proyek → **Manage NuGet Packages** → cari **Aspose.HTML** dan instal dari sana.

---

## Langkah 2: Buat Custom Resource Handler (save html with images)

Saat Anda memanggil `document.Save` dengan opsi ZIP, Aspose.HTML membutuhkan cara untuk menulis setiap sumber daya eksternal (seperti `image.png`) ke arsip. Di sinilah **custom resource handler** berperan. Handler menerima nama sumber daya dan mengembalikan `Stream` yang dapat ditulisi.

```csharp
using Aspose.Html;
using Aspose.Html.Saving;
using System.IO;

/// <summary>
/// Writes each external resource (images, CSS, etc.) to a folder on disk.
/// The folder path is supplied when the handler is instantiated.
/// </summary>
class MyResourceHandler : ResourceHandler
{
    private readonly string _outputFolder;

    public MyResourceHandler(string outputFolder) => _outputFolder = outputFolder;

    public override Stream HandleResource(string resourceName)
    {
        // Build the full path for the resource inside the output folder
        string path = Path.Combine(_outputFolder, resourceName);
        Directory.CreateDirectory(Path.GetDirectoryName(path)!);
        // Return a stream that Aspose.HTML will write the resource to
        return File.OpenWrite(path);
    }
}
```

**Mengapa ini penting:** Tanpa handler, Aspose.HTML akan mencoba menyematkan sumber daya langsung ke dalam ZIP, yang dapat menyebabkan gambar hilang jika jalurnya relatif. Handler kami menjamin setiap file yang direferensikan berakhir di tempat yang diharapkan oleh HTML.

---

## Langkah 3: Definisikan Konten HTML (save html as zip)

Untuk demonstrasi, kami akan menggunakan potongan HTML kecil yang mereferensikan gambar eksternal. Silakan ganti string tersebut dengan markup Anda sendiri.

```csharp
string html = @"<html>
<head>
    <title>Sample Page</title>
</head>
<body>
    <h1>Welcome!</h1>
    <p>This page includes an external image.</p>
    <img src='image.png' alt='Sample image'>
</body>
</html>";
```

Perhatikan atribut `alt`—baik untuk aksesibilitas dan juga berfungsi sebagai fallback yang berguna jika gambar gagal dimuat.

---

## Langkah 4: Muat HTML ke dalam Aspose.HTML Document

Sekarang kami memasukkan string ke dalam Aspose.HTML. Pustaka ini mem-parsing markup dan membangun DOM yang dapat kami simpan nanti.

```csharp
HTMLDocument document = new HTMLDocument(html);
```

Itu saja—tidak ada I/O file, tidak ada file sementara. Objek `HTMLDocument` kini memegang seluruh struktur halaman.

---

## Langkah 5: Konfigurasikan ZipArchiveSaveOptions (aspose html save options)

Selanjutnya, kami menyiapkan **Aspose HTML save options** yang memberi tahu pustaka untuk menghasilkan arsip ZIP. Kami juga melampirkan custom resource handler yang dibuat sebelumnya.

```csharp
using (var zipStream = new MemoryStream())
{
    // Prepare ZIP save options
    var zipOptions = new ZipArchiveSaveOptions
    {
        // Attach the custom handler so resources are written to the folder
        ResourceHandler = new MyResourceHandler("output/Resources")
    };

    // Save the document (HTML + all referenced resources) into the ZIP stream
    document.Save(zipStream, zipOptions);

    // Optional: write the ZIP to disk for inspection
    File.WriteAllBytes("output/output.zip", zipStream.ToArray());
}
```

**Poin penting:**
- `ZipArchiveSaveOptions` adalah kelas yang mengenkapsulasi **aspose html save options** untuk output ZIP.
- `ResourceHandler` memastikan setiap file eksternal—seperti `image.png`—disimpan bersamaan dengan HTML.
- `MemoryStream` memungkinkan kami menyimpan semuanya di memori sampai kami memutuskan ke mana menuliskannya.

---

## Langkah 6: Verifikasi Hasil

Setelah menjalankan program, Anda harus melihat dua hal di folder `output` Anda:

1. **output.zip** – arsip ZIP yang berisi `index.html` dan subfolder `Resources`.
2. **Resources/image.png** – file gambar sebenarnya yang direferensikan dalam HTML.

Ekstrak ZIP dan buka `index.html` di browser. Gambar harus tampil dengan benar, membuktikan bahwa Anda telah berhasil mempelajari **cara mengompres HTML** dengan aset‑asetsnya.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika HTML mereferensikan file CSS atau JavaScript?

`MyResourceHandler` yang sama akan menangkap jenis sumber daya apa pun—CSS, JS, font, dll.—selama HTML menunjuk ke mereka dengan URL relatif. Handler tidak peduli dengan ekstensi file.

### Bagaimana saya mengontrol struktur folder di dalam ZIP?

Anda dapat memodifikasi `resourceName` di dalam `HandleResource`. Misalnya, tambahkan awalan `"assets/"` untuk menempatkan semuanya di bawah direktori `assets`:

```csharp
string path = Path.Combine(_outputFolder, "assets", resourceName);
```

### Bisakah saya streaming ZIP langsung ke respons web?

Tentu saja. Alih‑alih menulis ke disk, Anda dapat mengembalikan `zipStream` dari controller ASP.NET. Cukup reset posisi stream:

```csharp
zipStream.Position = 0;
return File(zipStream, "application/zip", "page.zip");
```

### Bagaimana dengan gambar besar yang dapat menghabiskan memori?

Karena handler menulis setiap sumber daya langsung ke file stream, konsumsi memori tetap rendah. Hanya DOM HTML yang berada di memori, yang biasanya cukup kecil.

---

## Contoh Lengkap yang Berjalan (Save HTML with Images as a ZIP)

Berikut adalah program lengkap yang siap dijalankan. Salin‑tempel ke aplikasi console dan tekan **F5**.

```csharp
using Aspose.Html;
using Aspose.Html.Saving;
using System.IO;

class MyResourceHandler : ResourceHandler
{
    private readonly string _outputFolder;
    public MyResourceHandler(string outputFolder) => _outputFolder = outputFolder;

    public override Stream HandleResource(string resourceName)
    {
        string path = Path.Combine(_outputFolder, resourceName);
        Directory.CreateDirectory(Path.GetDirectoryName(path)!);
        return File.OpenWrite(path);
    }
}

class Program
{
    static void Main()
    {
        // HTML that references an external image
        string html = @"<html>
<head><title>Sample</title></head>
<body>
    <h2>How to Zip HTML Demo</h2>
    <p>Image below is loaded from an external file.</p>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

        // Load HTML into Aspose.HTML document
        HTMLDocument document = new HTMLDocument(html);

        // Prepare ZIP options and attach custom handler
        using var zipStream = new MemoryStream();
        var zipOptions = new ZipArchiveSaveOptions
        {
            ResourceHandler = new MyResourceHandler("output/Resources")
        };

        // Save HTML + resources into ZIP
        document.Save(zipStream, zipOptions);

        // Write ZIP to disk (optional)
        File.WriteAllBytes("output/output.zip", zipStream.ToArray());

        System.Console.WriteLine("ZIP created successfully! Check the 'output' folder.");
    }
}
```

**Output yang diharapkan:** Konsol mencetak *“ZIP created successfully! Check the 'output' folder.”* dan direktori `output` berisi `output.zip` serta file `Resources/image.png`.

---

## Kesimpulan

Anda kini tahu **cara mengompres HTML** yang mereferensikan aset eksternal menggunakan Aspose.HTML. Dengan membuat **custom resource handler**, mengonfigurasi **aspose html save options** yang tepat, dan memanfaatkan `ZipArchiveSaveOptions`, Anda dapat dengan andal **menyimpan HTML dengan gambar** (atau sumber daya lain) ke dalam satu file ZIP yang portabel.  

Dari sini Anda dapat mengeksplorasi:

- **Saving HTML as zip** di endpoint API web untuk unduhan on‑the‑fly.
- Menggunakan pola yang sama untuk menyematkan file **CSS** dan **JavaScript**.
- Menyesuaikan **custom resource handler** untuk mengompres gambar secara langsung.

Cobalah, sesuaikan handler agar cocok dengan tata letak folder Anda, dan biarkan paket ZIP melakukan pekerjaan berat. Selamat coding!  

---  

![contoh cara mengompres html](/images/how-to-zip-html.png "Ilustrasi yang menunjukkan cara mengompres html dengan Aspose.HTML")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}