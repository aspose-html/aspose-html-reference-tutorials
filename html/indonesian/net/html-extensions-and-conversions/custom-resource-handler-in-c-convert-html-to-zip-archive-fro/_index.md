---
category: general
date: 2026-02-13
description: Pelajari cara membuat penangan sumber daya khusus di C# untuk mengonversi
  HTML menjadi arsip ZIP, membuat zip dari memori dengan Aspose.HTML – panduan langkah
  demi langkah.
draft: false
keywords:
- custom resource handler
- convert html zip archive
- create zip from memory
- Aspose HTML
- in‑memory streaming
- C# zip compression
language: id
og_description: Temukan solusi lengkap C# untuk menggunakan penangan sumber daya khusus
  yang mengonversi HTML menjadi arsip ZIP langsung di memori.
og_title: Penangani Sumber Daya Kustom – Mengonversi HTML ke ZIP dari Memori
tags:
- C#
- Aspose.HTML
- ZipArchive
- MemoryStream
title: Penangan Sumber Daya Kustom di C# – Mengonversi HTML ke Arsip ZIP dari Memori
url: /id/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-archive-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Penangan Sumber Daya Kustom – Mengonversi HTML ke Arsip ZIP dari Memori

Pernah membutuhkan **custom resource handler** untuk mengambil setiap gambar, file CSS, atau skrip yang dimuat oleh halaman HTML, dan kemudian mengompres semuanya tanpa menyentuh disk? Anda tidak sendirian. Dalam banyak skenario otomasi web atau templating email, Anda ingin seluruh halaman dibundel sebagai satu paket portabel, dan Anda lebih suka menyimpan semuanya di RAM untuk kecepatan dan keamanan.

Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang menunjukkan secara tepat cara **convert HTML zip archive** menggunakan **custom resource handler** dan kemudian **create zip from memory** dengan .NET `System.IO.Compression`. Pada akhir tutorial Anda akan memiliki metode mandiri yang dapat Anda sisipkan ke proyek C# mana pun yang menggunakan Aspose.HTML.

## Apa yang Anda Butuhkan

- .NET 6+ (atau .NET Framework 4.7.2+)  
- Aspose.HTML untuk .NET (paket NuGet `Aspose.HTML`)  
- Familiaritas dasar dengan stream dan kelas `ZipArchive`

Tanpa alat eksternal, tanpa file sementara, hanya pemrosesan murni dalam memori.

## Langkah 1: Definisikan Custom Resource Handler

Inti dari solusi ini adalah kelas yang mewarisi dari `Aspose.Html.ResourceHandler`. Tugasnya adalah menyediakan `Stream` baru untuk setiap sumber daya eksternal yang diminta oleh mesin HTML. Dengan mengembalikan `MemoryStream` baru setiap kali, kami menjaga data terisolasi dan siap untuk dikemas nanti.

```csharp
using System.IO;
using Aspose.Html;

// Step 1 – Custom handler that stores resources in memory
class MemoryResourceHandler : ResourceHandler
{
    // The framework calls this method for every external resource (images, CSS, etc.)
    public override Stream HandleResource(Resource resource)
    {
        // We give the engine an empty stream; later we’ll fill it with the actual bytes.
        // Using MemoryStream means everything stays in RAM.
        return new MemoryStream();
    }
}
```

**Mengapa ini penting:**  
Jika Anda membiarkan Aspose.HTML menulis sumber daya ke disk, Anda harus membersihkannya kemudian. Penangan dalam memori menghilangkan overhead I/O dan membuat kode aman untuk lingkungan sandbox (mis., Azure Functions).

## Langkah 2: Muat Dokumen HTML Anda

Selanjutnya, arahkan Aspose.HTML ke file HTML yang ingin Anda paketkan. Dokumen dapat berada di disk, URL, atau bahkan string mentah. Di sini kami menggunakan jalur file untuk kesederhanaan.

```csharp
using Aspose.Html;

// Step 2 – Load the source HTML
HtmlDocument document = new HtmlDocument("YOUR_DIRECTORY/input.html");
```

> **Pro tip:** Jika HTML Anda merujuk ke sumber daya relatif, pastikan `input.html` berada di folder yang sama dengan aset‑aset tersebut, jika tidak penangan tidak akan dapat menemukannya.

## Langkah 3: Hubungkan Penangan dan Simpan ke MemoryStream

Sekarang kami menginstansiasi penangan dan memberi tahu Aspose.HTML untuk menggunakannya melalui `HtmlSaveOptions.OutputStorage`. HTML yang dihasilkan (termasuk URL sumber daya yang ditulis ulang) disimpan dalam `MemoryStream`.

```csharp
using Aspose.Html.Saving;
using System.IO;

// Step 3 – Prepare the handler and an in‑memory buffer for the final HTML
var resourceHandler = new MemoryResourceHandler();

using (MemoryStream htmlMemoryStream = new MemoryStream())
{
    document.Save(htmlMemoryStream, new HtmlSaveOptions
    {
        OutputStorage = resourceHandler // redirects all resources to the handler
    });

    // At this point htmlMemoryStream contains the full HTML file,
    // while each external resource resides in the streams returned by the handler.
```

**Apa yang terjadi di balik layar?**  
Ketika `document.Save` dijalankan, Aspose.HTML meminta `MemoryResourceHandler` untuk stream setiap sumber daya. Karena kami mengembalikan `MemoryStream` kosong, mesin menulis byte mentah langsung ke memori. Tidak ada file sementara yang dibuat.

## Langkah 4: Susun Arsip ZIP Sepenuhnya dalam Memori

Sekarang bagian yang menyenangkan: kami akan membuat `ZipArchive` yang berada di dalam `MemoryStream` lain. Ini memungkinkan kita **create zip from memory** tanpa pernah menyentuh sistem file.

```csharp
    // Step 4 – Build the ZIP archive in memory
    using (MemoryStream zipMemoryStream = new MemoryStream())
    using (var zipArchive = new ZipArchive(zipMemoryStream, ZipArchiveMode.Create, leaveOpen: true))
    {
        // 4a – Add the main HTML file
        var htmlEntry = zipArchive.CreateEntry("index.html");
        using (var entryStream = htmlEntry.Open())
        {
            // Reset the position of the HTML stream before copying
            htmlMemoryStream.Position = 0;
            htmlMemoryStream.CopyTo(entryStream);
        }

        // 4b – Add each resource that the handler captured
        // The handler stored each resource in a fresh MemoryStream, which we can enumerate.
        // For demonstration, assume we kept a list of those streams (you could store them in a dictionary).
        // Example placeholder – replace with your actual collection:
        // foreach (var kvp in capturedResources)
        // {
        //     var resourceEntry = zipArchive.CreateEntry(kvp.Key); // kvp.Key = relative path
        //     using var entry = resourceEntry.Open();
        //     kvp.Value.Position = 0;
        //     kvp.Value.CopyTo(entry);
        // }

        // When we’re done, flush everything
        zipArchive.Dispose(); // optional because of using, but makes intent clear
    }

    // At this stage zipMemoryStream holds the complete ZIP file.
    // You can return it, write it to a response stream, or save it to disk if you wish.
}
```

> **Catatan:** Bagian yang dikomentari menunjukkan cara Anda dapat mengumpulkan stream di dalam `MemoryResourceHandler`. Dalam skenario produksi, Anda akan menyimpan setiap `MemoryStream` dalam kamus yang diindeks oleh URL sumber daya asli, lalu iterasi di sini untuk menambahkannya ke arsip.

**Mengapa menyimpan ZIP di memori?**  
Menyimpan arsip dalam `MemoryStream` memudahkan untuk mengirim langsung ke klien HTTP (`FileResult` di ASP.NET Core) atau mengunggah ke penyimpanan cloud tanpa file perantara.

## Langkah 5: (Opsional) Simpan ZIP ke Disk

Jika Anda masih membutuhkan file fisik—mungkin untuk debugging—cukup tulis `zipMemoryStream` ke disk:

```csharp
// Optional: write the in‑memory ZIP to a file for inspection
File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipMemoryStream.ToArray());
```

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program tunggal yang siap disalin‑tempel yang **converts HTML to a ZIP archive** sepenuhnya dalam memori.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class MemoryResourceHandler : ResourceHandler
{
    // Capture each resource in a dictionary for later retrieval
    public static readonly System.Collections.Generic.Dictionary<string, MemoryStream> Captured = new();

    public override Stream HandleResource(Resource resource)
    {
        var ms = new MemoryStream();
        // Store the stream using the resource's absolute URL as the key
        Captured[resource.Uri.AbsoluteUri] = ms;
        return ms;
    }
}

class Program
{
    static void Main()
    {
        // Load the HTML file
        HtmlDocument doc = new HtmlDocument("YOUR_DIRECTORY/input.html");

        // Attach the custom handler
        var handler = new MemoryResourceHandler();

        // Save HTML + resources to memory
        using var htmlStream = new MemoryStream();
        doc.Save(htmlStream, new HtmlSaveOptions { OutputStorage = handler });

        // Create the ZIP archive in memory
        using var zipStream = new MemoryStream();
        using (var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            // Add the HTML file
            var htmlEntry = zip.CreateEntry("index.html");
            using (var entry = htmlEntry.Open())
            {
                htmlStream.Position = 0;
                htmlStream.CopyTo(entry);
            }

            // Add each captured resource
            foreach (var kvp in MemoryResourceHandler.Captured)
            {
                // Derive a sane relative path from the URL
                var uri = new Uri(kvp.Key);
                var relativePath = uri.AbsolutePath.TrimStart('/');
                var resEntry = zip.CreateEntry(relativePath);
                using var entry = resEntry.Open();
                kvp.Value.Position = 0;
                kvp.Value.CopyTo(entry);
            }
        }

        // The ZIP is ready – write it out or return it from a web API
        File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipStream.ToArray());

        Console.WriteLine("HTML successfully packaged into output.zip");
    }
}
```

### Hasil yang Diharapkan

Menjalankan program membuat `output.zip` yang berisi:

- `index.html` – HTML yang ditulis ulang yang mengarah ke sumber daya yang dibundel.  
- Semua gambar, CSS, dan file JavaScript yang direferensikan oleh halaman asli, disimpan menggunakan jalur relatif aslinya.

Buka `index.html` dari ZIP di browser apa pun dan Anda akan melihat halaman ditampilkan persis seperti saat berada di sistem file.

## Pertanyaan Umum & Kasus Tepi

| Pertanyaan | Jawaban |
|------------|---------|
| **Bagaimana jika sebuah sumber daya sangat besar (mis., video)?** | Karena semuanya berada di memori, file yang sangat besar dapat menyebabkan `OutOfMemoryException`. Dalam kasus tersebut, alirkan langsung ke file sementara atau batasi ukuran yang Anda terima. |
| **Apakah saya perlu menangani URL sumber daya yang duplikat?** | Kamus pada penangan akan menimpa duplikat. Jika Anda ingin menyimpan hanya satu salinan, periksa `Captured.ContainsKey` sebelum menambahkannya. |
| **Bisakah saya menggunakan ini di controller ASP.NET Core?** | Tentu saja. Kembalikan `File(zipStream.ToArray(), "application/zip", "page.zip")` dari metode aksi. |
| **Bagaimana dengan sumber daya HTTPS?** | Aspose.HTML akan mengunduhnya secara otomatis selama runtime mempercayai sertifikat SSL. Untuk sertifikat self‑signed, konfigurasikan `ServicePointManager.ServerCertificateValidationCallback`. |
| **Apakah penangan kustom thread‑safe?** | Contoh ini menggunakan kamus statis, yang *tidak* thread‑safe. Bungkus akses dengan lock atau gunakan `ConcurrentDictionary` jika Anda berencana memproses banyak dokumen secara bersamaan. |

## Tips Pro untuk Penggunaan Produksi

- **Gunakan kembali penangan** hanya untuk satu dokumen; buat instance baru per permintaan untuk menghindari cross‑talk antar pengguna.  
- **Buang stream** segera. Meskipun blok `using` menangani sebagian besar kasus, setiap stream yang disimpan dalam kamus harus dibuang setelah ZIP selesai dibangun.  
- **Validasi HTML** sebelum diproses untuk menangkap markup yang rusak yang dapat menyebabkan penangan meminta sumber daya tak terduga.  
- **Kompres secara agresif** dengan mengatur `ZipArchiveEntry.CompressionLevel = CompressionLevel.Optimal` jika ukuran file penting.  

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **custom resource handler** melalui halaman HTML, menangkap setiap aset yang terhubung, dan **create zip from memory** tanpa pernah menyentuh disk. Pola yang ditunjukkan di sini cukup fleksibel untuk skenario layanan web, pekerjaan latar belakang, atau bahkan utilitas desktop yang perlu mengirimkan bundel HTML mandiri.

Cobalah—ganti `YOUR_DIRECTORY/input.html` dengan halaman apa pun yang Anda suka, sesuaikan penangan untuk menyimpan sumber daya dalam `ConcurrentDictionary`, dan Anda akan memiliki pipeline HTML‑to‑ZIP dalam memori yang kuat siap untuk produksi.

---

*Siap untuk naik level?* Selanjutnya, jelajahi cara **convert HTML to PDF** menggunakan Aspose.HTML, atau bereksperimen dengan mengenkripsi ZIP untuk keamanan tambahan. Langit adalah batasnya ketika Anda menguasai streaming dalam memori di C#. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}