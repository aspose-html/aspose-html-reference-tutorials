---
category: general
date: 2026-03-02
description: Pelajari cara mengompres HTML menggunakan Aspose HTML, penangan sumber
  daya khusus, dan .NET ZipArchive. Panduan langkah demi langkah tentang cara membuat
  zip dan menyematkan sumber daya.
draft: false
keywords:
- how to zip html
- custom resource handler
- aspose html save
- how to create zip
- how to embed resources
language: id
og_description: Pelajari cara mengompres HTML menggunakan Aspose HTML, penangani sumber
  daya khusus, dan .NET ZipArchive. Ikuti langkah-langkah untuk membuat zip dan menyematkan
  sumber daya.
og_title: Cara Mengompres HTML dengan Aspose HTML – Panduan Lengkap
tags:
- Aspose.HTML
- C#
- ZIP archive
title: Cara Mengompres HTML dengan Aspose HTML – Panduan Lengkap
url: /id/net/advanced-features/how-to-zip-html-with-aspose-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Meng‑zip HTML dengan Aspose HTML – Panduan Lengkap

Pernah perlu **meng‑zip HTML** bersama semua gambar, file CSS, dan skrip yang direferensikannya? Mungkin Anda sedang membuat paket unduhan untuk sistem bantuan offline, atau hanya ingin mengirim situs statis sebagai satu file. Bagaimanapun, mempelajari **cara meng‑zip HTML** adalah keterampilan berguna dalam kotak peralatan pengembang .NET.

Dalam tutorial ini kita akan melangkah melalui solusi praktis yang menggunakan **Aspose.HTML**, **custom resource handler**, dan kelas bawaan `System.IO.Compression.ZipArchive`. Pada akhir tutorial Anda akan tahu persis cara **menyimpan** dokumen HTML ke dalam ZIP, **menyematkan sumber daya**, dan bahkan menyesuaikan proses jika Anda perlu mendukung URI yang tidak biasa.

> **Pro tip:** Pola yang sama bekerja untuk PDF, SVG, atau format berat sumber daya web lainnya—cukup ganti kelas Aspose.

---

## Apa yang Anda Butuhkan

- .NET 6 atau yang lebih baru (kode juga dapat dikompilasi dengan .NET Framework)
- Paket NuGet **Aspose.HTML for .NET** (`Aspose.Html`)
- Pemahaman dasar tentang aliran C# dan I/O file
- Halaman HTML yang mereferensikan sumber daya eksternal (gambar, CSS, JS)

Tidak diperlukan pustaka ZIP pihak ketiga tambahan; namespace standar `System.IO.Compression` melakukan semua pekerjaan berat.

---

## Langkah 1: Buat Custom ResourceHandler (custom resource handler)

Aspose.HTML memanggil sebuah `ResourceHandler` setiap kali menemukan referensi eksternal saat menyimpan. Secara default ia mencoba mengunduh sumber daya dari web, tetapi kita ingin **menyematkan** file yang tepat yang berada di disk. Di sinilah **custom resource handler** berperan.

```csharp
using System;
using System.IO;
using Aspose.Html;

// Step 1 – custom handler that copies local files into the output stream
class MyResourceHandler : ResourceHandler
{
    public override void HandleResource(string uri, Stream outputStream)
    {
        // Assume uri is a local file path; adjust logic for URLs if needed
        using (var source = new FileStream(uri, FileMode.Open, FileAccess.Read))
        {
            source.CopyTo(outputStream);
        }
    }
}
```

**Mengapa ini penting:**  
Jika Anda melewatkan langkah ini, Aspose akan melakukan permintaan HTTP untuk setiap `src` atau `href`. Hal itu menambah latensi, dapat gagal di balik firewall, dan menghilangkan tujuan ZIP yang mandiri. Handler kami menjamin bahwa file tepat yang ada di disk masuk ke dalam arsip.

---

## Langkah 2: Muat Dokumen HTML (aspose html save)

Aspose.HTML dapat menerima URL, jalur file, atau string HTML mentah. Untuk demo ini kita akan memuat halaman remote, tetapi kode yang sama bekerja dengan file lokal.

```csharp
using Aspose.Html;

// Step 2 – load the HTML document (URL, file path, or raw string)
var htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

**Apa yang terjadi di balik layar?**  
Kelas `HTMLDocument` mem-parsing markup, membangun DOM, dan menyelesaikan URL relatif. Ketika Anda kemudian memanggil `Save`, Aspose menelusuri DOM, meminta `ResourceHandler` Anda untuk setiap file eksternal, dan menulis semuanya ke aliran target.

---

## Langkah 3: Siapkan Arsip ZIP In‑Memory (how to create zip)

Alih‑alih menulis file sementara ke disk, kita akan menyimpan semuanya di memori menggunakan `MemoryStream`. Pendekatan ini lebih cepat dan menghindari kekacauan pada sistem file.

```csharp
using System.IO;
using System.IO.Compression;

// Step 3 – create a memory‑backed ZIP archive
using var archiveStream = new MemoryStream();
using var archive = new ZipArchive(archiveStream, ZipArchiveMode.Create, true);
```

**Catatan kasus tepi:**  
Jika HTML Anda mereferensikan aset yang sangat besar (misalnya gambar resolusi tinggi), aliran in‑memory dapat mengonsumsi banyak RAM. Pada skenario tersebut, beralihlah ke ZIP berbasis `FileStream` (`new FileStream("temp.zip", FileMode.Create)`).

---

## Langkah 4: Simpan Dokumen HTML ke dalam ZIP (aspose html save)

Sekarang kita gabungkan semuanya: dokumen, `MyResourceHandler` kita, dan arsip ZIP.

```csharp
// Step 4 – save HTML + resources into the ZIP
var resourceHandler = new MyResourceHandler();
htmlDoc.Save(archive, resourceHandler);
```

Di balik layar, Aspose membuat entri untuk file HTML utama (biasanya `index.html`) dan entri tambahan untuk setiap sumber daya (misalnya `images/logo.png`). `resourceHandler` menulis data biner langsung ke dalam entri‑entri tersebut.

---

## Langkah 5: Tulis ZIP ke Disk (how to embed resources)

Akhirnya, kita menyimpan arsip in‑memory ke sebuah file. Anda dapat memilih folder mana saja; cukup ganti `YOUR_DIRECTORY` dengan jalur aktual Anda.

```csharp
using System.IO;

// Step 5 – persist the ZIP file
File.WriteAllBytes(@"YOUR_DIRECTORY\sample.zip", archiveStream.ToArray());

// Optional: verify the archive size
Console.WriteLine($"ZIP created: {new FileInfo(@"YOUR_DIRECTORY\sample.zip").Length} bytes");
```

**Tips verifikasi:**  
Buka `sample.zip` yang dihasilkan dengan penjelajah arsip OS Anda. Anda harus melihat `index.html` plus hierarki folder yang mencerminkan lokasi sumber daya asli. Klik ganda `index.html`—halaman harus ditampilkan secara offline tanpa gambar atau gaya yang hilang.

---

## Contoh Lengkap yang Berfungsi (All Steps Combined)

Berikut adalah program lengkap yang siap dijalankan. Salin‑tempel ke proyek Console App baru, pulihkan paket NuGet `Aspose.Html`, dan tekan **F5**.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

// Step 1: Custom ResourceHandler that copies each external resource into the ZIP entry.
class MyResourceHandler : ResourceHandler
{
    public override void HandleResource(string uri, Stream outputStream)
    {
        // Handle both absolute file paths and relative URLs.
        if (File.Exists(uri))
        {
            using var source = new FileStream(uri, FileMode.Open, FileAccess.Read);
            source.CopyTo(outputStream);
        }
        else
        {
            // Fallback: try to download from the web (rarely needed for offline ZIPs).
            using var client = new System.Net.WebClient();
            var data = client.DownloadData(uri);
            outputStream.Write(data, 0, data.Length);
        }
    }
}

class Program
{
    static void Main()
    {
        // Step 2: Load the HTML document (URL, file path, or raw HTML string).
        var htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // Step 3: Prepare an in‑memory ZIP archive.
        using var archiveStream = new MemoryStream();
        using var archive = new ZipArchive(archiveStream, ZipArchiveMode.Create, true);

        // Step 4: Save the HTML + its resources into the ZIP.
        var resourceHandler = new MyResourceHandler();
        htmlDoc.Save(archive, resourceHandler);

        // Step 5: Persist the ZIP to disk.
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "sample.zip");
        File.WriteAllBytes(outputPath, archiveStream.ToArray());

        Console.WriteLine($"✅ ZIP created at: {outputPath}");
    }
}
```

**Hasil yang diharapkan:**  
File `sample.zip` muncul di Desktop Anda. Ekstrak dan buka `index.html`—halaman harus terlihat persis seperti versi daring, tetapi kini berfungsi sepenuhnya offline.

---

## Pertanyaan yang Sering Diajukan (FAQs)

### Apakah ini bekerja dengan file HTML lokal?
Tentu saja. Ganti URL pada `HTMLDocument` dengan jalur file, misalnya `new HTMLDocument(@"C:\site\index.html")`. `MyResourceHandler` yang sama akan menyalin sumber daya lokal.

### Bagaimana jika sebuah sumber daya berupa data‑URI (base64‑encoded)?
Aspose memperlakukan data‑URI sebagai sudah disematkan, sehingga handler tidak dipanggil. Tidak ada pekerjaan tambahan yang diperlukan.

### Bisakah saya mengontrol struktur folder di dalam ZIP?
Ya. Sebelum memanggil `htmlDoc.Save`, Anda dapat mengatur `htmlDoc.SaveOptions` dan menentukan base path. Atau, modifikasi `MyResourceHandler` untuk menambahkan nama folder saat membuat entri.

### Bagaimana cara menambahkan file README ke arsip?
Cukup buat entri baru secara manual:

```csharp
var readme = archive.CreateEntry("README.txt");
using var writer = new StreamWriter(readme.Open());
writer.WriteLine("This ZIP contains an offline HTML site.");
```

---

## Langkah Selanjutnya & Topik Terkait

- **Cara menyematkan sumber daya** dalam format lain (PDF, SVG) menggunakan API Aspose yang serupa.  
- **Menyesuaikan level kompresi**: `new ZipArchive(stream, ZipArchiveMode.Create, true, Encoding.UTF8)` memungkinkan Anda mengatur `ZipArchiveEntry.CompressionLevel` untuk arsip yang lebih cepat atau lebih kecil.  
- **Menyajikan ZIP via ASP.NET Core**: Kembalikan `MemoryStream` sebagai hasil file (`File(archiveStream, "application/zip", "site.zip")`).  

Cobalah variasi tersebut agar sesuai dengan kebutuhan proyek Anda. Pola yang kami bahas cukup fleksibel untuk menangani sebagian besar skenario “bundel‑semua‑ke‑satu”.

---

## Kesimpulan

Kami baru saja mendemonstrasikan **cara meng‑zip HTML** menggunakan Aspose.HTML, **custom resource handler**, dan kelas .NET `ZipArchive`. Dengan membuat handler yang men-stream file lokal, memuat dokumen, mengemas semuanya di memori, dan akhirnya menyimpan ZIP, Anda mendapatkan arsip mandiri yang siap didistribusikan.

Sekarang Anda dapat dengan percaya diri membuat paket zip untuk situs statis, mengekspor bundel dokumentasi, atau bahkan mengotomatisasi backup offline—semua dengan beberapa baris kode C#.

Ada trik lain yang ingin Anda bagikan? Tinggalkan komentar, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}