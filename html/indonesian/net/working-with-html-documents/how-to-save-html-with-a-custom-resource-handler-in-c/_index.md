---
category: general
date: 2026-11-20
description: Pelajari cara menyimpan HTML menggunakan ResourceHandler khusus di C#
  dan juga menyimpan HTML ke arsip zip dengan kode yang ringkas dan siap produksi.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: id
lastmod: 2026-11-20
og_description: Cara menyimpan HTML menggunakan ResourceHandler kustom di C# dan secara
  opsional menyimpan HTML ke file zip—panduan lengkap dan dapat dijalankan untuk pengembang
  .NET.
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: Cara menyimpan HTML dengan penangan sumber daya khusus di C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  headline: How to save HTML with a custom resource handler in C#
  type: TechArticle
- description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  name: How to save HTML with a custom resource handler in C#
  steps:
  - name: What if I need multiple HTML files in the same zip?
    text: 'Create a new entry for each call to `HandleResource`. The `resourceName`
      argument typically contains the filename, so you can use it directly:'
  - name: How to handle large documents without exhausting memory?
    text: Replace `MemoryStream` with a `FileStream` that points to a temporary file.
      The handler then returns the file stream, and you can later delete the file
      after the zip is created.
  - name: Does this approach work with .NET Core on Linux?
    text: Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are
      cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.
  - name: Can I encrypt the zip archive?
    text: '`ZipArchive` supports password‑based encryption only through third‑party
      libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output
      bytes with a library that provides AES encryption before sending them to the
      client.'
  type: HowTo
tags:
- C#
- HTML
- file I/O
title: Cara menyimpan HTML dengan handler sumber daya khusus di C#
url: /id/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyimpan HTML dengan penangan sumber daya khusus di C#

Jika Anda perlu mengetahui **cara menyimpan HTML** dari string dalam memori atau dokumen yang diurai, panduan ini menunjukkan solusi lengkap. Menggunakan `ResourceHandler` khusus memungkinkan Anda mengontrol aliran tujuan, yang berarti Anda dapat **menyimpan HTML ke zip** arsip tanpa menulis file sementara.

Anda akan melihat mengapa `ResourceHandler` lebih disukai dibandingkan pendekatan `IOutputStorage` yang lebih lama, cara menyiapkannya, dan cara memperluasnya untuk kompresi zip. Pada akhir tutorial ini Anda dapat menyematkan kode dalam proyek .NET 6+ apa pun dan menyesuaikannya dengan kebutuhan penyimpanan Anda.

## Apa yang akan Anda bangun

* Sebuah `ResourceHandler` minimal yang mengembalikan `MemoryStream`.
* Sebuah `HtmlDocument` yang dibuat dengan **HtmlAgilityPack**.
* Sebuah panggilan ke `doc.Save` yang menulis HTML ke aliran yang disediakan oleh handler.
* Sebuah pembungkus opsional yang mengompres HTML yang dihasilkan ke dalam file zip.

Prasyarat:

* .NET 6 SDK atau yang lebih baru.
* Paket NuGet `HtmlAgilityPack` (`dotnet add package HtmlAgilityPack`).
* Familiaritas dasar dengan aliran C#.

## Langkah 1: Buat penangan sumber daya khusus (cara utama untuk **cara menyimpan html**)

Kelas dasar `ResourceHandler` (tersedia sejak versi 24.2 dari viewer SDK) mendefinisikan satu metode abstrak, `HandleResource`. Mengimplementasikan metode ini memberi Anda kontrol penuh atas tempat HTML ditulis.

```csharp
using System.IO;

/// <summary>
/// Handles the output stream for each HTML resource.
/// Returning a MemoryStream keeps everything in memory, which is ideal for further processing
/// such as zipping or sending over a network.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string resourceName)
    {
        // You could inspect resourceName to decide between file, memory, or zip entry.
        return new MemoryStream();
    }
}
```

**Mengapa ini penting:** Dengan mengembalikan `MemoryStream`, Anda menghindari I/O disk, mengurangi latensi, dan menjaga kode deterministik untuk unit test. Handler dipanggil secara otomatis oleh metode `Save`, sehingga Anda tidak pernah perlu mengirimkan aliran secara eksplisit.

## Langkah 2: Muat atau bangun dokumen HTML

`HtmlAgilityPack` menyediakan kelas `HtmlDocument` yang nyaman yang dapat mengurai string, file, atau aliran. Untuk contoh ini kami memuat literal sederhana, tetapi kode yang sama bekerja dengan sumber HTML apa pun.

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**Mengapa ini penting:** Menjaga dokumen di memori selaras dengan pendekatan berbasis aliran dari handler khusus. Ini juga memungkinkan Anda memanipulasi DOM sebelum menyimpan, seperti menyisipkan skrip atau memperbaiki tag yang rusak.

## Langkah 3: Simpan dokumen menggunakan handler khusus

Memanggil `doc.Save` dengan instance `MyHandler` memicu metode `HandleResource`. HTML ditulis langsung ke aliran yang Anda kembalikan.

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

Setelah `Save` selesai, `MemoryStream` di dalam `MyHandler` berisi HTML yang diserialisasi. Anda dapat mengambilnya seperti ini:

```csharp
// Cast the handler back to access the stream (if you kept a reference)
MyHandler handler = new MyHandler();
doc.Save(handler);

// Reset position to read from the beginning.
handler.HandleResource("").Seek(0, SeekOrigin.Begin);
using var reader = new StreamReader(handler.HandleResource(""));
string htmlOutput = reader.ReadToEnd();
System.Console.WriteLine(htmlOutput);
```

**Hasil:** Konsol mencetak HTML persis yang Anda berikan ke `LoadHtml`. Ini membuktikan bahwa Anda kini memahami **cara menyimpan HTML** dengan handler khusus.

## Langkah 4: Memperluas handler untuk **menyimpan HTML ke zip**

Jika Anda ingin mengarsipkan HTML, ubah `MyHandler` untuk menulis ke `ZipArchiveEntry`. Namespace .NET `System.IO.Compression` membuat ini sederhana.

```csharp
using System.IO.Compression;

/// <summary>
/// Writes the HTML into a zip entry named "document.html".
/// The zip archive is created in memory and can be saved to a file or sent over HTTP.
/// </summary>
class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        // Initialise the zip archive in create mode.
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        // Create a zip entry for the HTML file.
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open(); // Returns a stream that writes directly into the zip entry.
    }

    /// <summary>
    /// Finalises the zip archive and returns the raw bytes.
    /// </summary>
    public byte[] GetZipBytes()
    {
        // Ensure all entries are flushed.
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}
```

Sekarang gunakan handler baru:

```csharp
// Instantiate the zip‑aware handler.
using var zipHandler = new ZipHtmlHandler();

// Save HTML; it ends up inside the zip archive.
doc.Save(zipHandler);

// Retrieve the zip file as a byte array.
byte[] zipBytes = zipHandler.GetZipBytes();

// Optionally write the zip to disk for verification.
File.WriteAllBytes("output.zip", zipBytes);
System.Console.WriteLine("ZIP file created with size: " + zipBytes.Length);
```

**Mengapa ini berhasil:** Metode `HandleResource` membuat entri zip bernama `document.html`. Ketika `doc.Save` menulis ke aliran yang dikembalikan, data secara otomatis dikompresi. Karena zip dibangun di memori, Anda dapat mengembalikannya dari web API, melampirkannya ke email, atau menyimpannya di basis data tanpa menyentuh sistem file.

## Pertanyaan umum dan kasus tepi

### Bagaimana jika saya membutuhkan beberapa file HTML dalam zip yang sama?

Buat entri baru untuk setiap panggilan ke `HandleResource`. Argumen `resourceName` biasanya berisi nama file, sehingga Anda dapat menggunakannya langsung:

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### Bagaimana menangani dokumen besar tanpa menghabiskan memori?

Ganti `MemoryStream` dengan `FileStream` yang menunjuk ke file sementara. Handler kemudian mengembalikan aliran file, dan Anda dapat menghapus file tersebut setelah zip dibuat.

### Apakah pendekatan ini bekerja dengan .NET Core di Linux?

Ya. Semua API yang digunakan (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) bersifat lintas‑platform. Pastikan kerangka target setidaknya .NET 6 untuk kompatibilitas terbaik.

### Bisakah saya mengenkripsi arsip zip?

`ZipArchive` mendukung enkripsi berbasis kata sandi hanya melalui pustaka pihak ketiga (mis., `SharpZipLib`). Jika enkripsi diperlukan, bungkus byte output dengan pustaka yang menyediakan enkripsi AES sebelum mengirimkannya ke klien.

## Tips profesional

* **Gunakan kembali handler** saat memproses banyak dokumen dalam satu batch; membuat `ZipArchive` baru untuk setiap file menambah beban yang tidak perlu.
* **Setel `LeaveOpen: true`** pada konstruktor `ZipArchive` jika Anda perlu membaca byte zip sementara arsip masih terbuka.
* **Validasi HTML** sebelum menyimpan dengan memanggil `doc.OptionCheckSyntax = true;` – ini menangkap tag yang rusak lebih awal.
* **Catat ukuran** zip yang dihasilkan; output yang tidak biasa besar sering menunjukkan sumber daya duplikat atau kompresi yang hilang.

## Contoh lengkap yang berfungsi

Berikut adalah satu file yang dapat Anda tempel ke proyek konsol (`dotnet new console`) dan jalankan. Ini mendemonstrasikan penyimpanan HTML biasa dan kompresi zip.



## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menyimpan HTML di C# dengan Penangan Sumber Daya Khusus](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [Cara Menggunakan ZipArchive – Menyimpan HTML dan Sumber Daya ke File ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [simpan html sebagai zip dengan penangan sumber daya khusus – panduan langkah‑demi‑langkah](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}