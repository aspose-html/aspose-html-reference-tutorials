---
category: general
date: 2026-08-15
description: Buat penangan sumber daya khusus di C# untuk mengelola sumber daya HTML
  seperti gambar dan CSS. Pelajari HTMLLoadOptions, aliran memori, dan pemuatan HTMLDocument.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: id
lastmod: 2026-08-15
og_description: Buat penangan sumber daya khusus di C# untuk mengontrol cara aliran
  sumber daya HTML. Tutorial ini menunjukkan pengaturan HTMLLoadOptions, penanganan
  memory stream, dan pemuatan HTMLDocument dengan logika khusus.
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: Buat penangan sumber daya khusus di C# – panduan lengkap untuk manajemen
  sumber daya HTML
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: Buat penangan sumber daya khusus di C# untuk memuat HTML
url: /id/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat custom resource handler di C# untuk pemuatan HTML

Jika Anda perlu **create custom resource handler** untuk file HTML, panduan ini menunjukkan secara tepat caranya. Anda akan belajar cara menyela gambar, CSS, dan aset lainnya saat memuat dokumen HTML, menggunakan `HTMLLoadOptions` dan aliran berbasis memori.

Tutorial ini mencakup semua yang diperlukan untuk mengimplementasikan handler yang dapat digunakan kembali, mengonfigurasi opsi pemuatan, dan memverifikasi bahwa sumber daya ditangkap dengan benar. Tidak diperlukan dokumentasi eksternal—hanya kode di bawah ini dan penjelasannya.

## Prasyarat

- .NET 6.0 atau yang lebih baru
- Familiaritas dasar dengan C#
- Referensi ke pustaka pemrosesan HTML yang menyediakan `HTMLDocument`, `HtmlLoadOptions`, dan `ResourceHandler` (misalnya GroupDocs.Viewer untuk .NET)

## Gambaran solusi

Kita akan:

1. **Create a custom resource handler** dengan membuat subclass `ResourceHandler`.
2. Mengonfigurasi `HTMLLoadOptions` untuk menggunakan handler.
3. Memuat file HTML dengan `HTMLDocument` sementara handler menyediakan aliran untuk setiap sumber daya.
4. (Opsional) Menyimpan sumber daya yang diterima ke disk untuk verifikasi.

Setiap langkah menyertakan kode sumber lengkap dan penjelasan di baliknya.

## Langkah 1: Definisikan kelas custom resource handler

Membuat handler khusus berarti menimpa `HandleResource` sehingga pustaka dapat menulis byte sumber daya ke aliran yang Anda kontrol. Menggunakan `MemoryStream` menjaga data tetap di memori, yang ideal untuk pengujian atau pemrosesan lebih lanjut.

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**Mengapa ini penting:**  
Menimpa `HandleResource` memberi Anda kontrol penuh atas tempat data sumber daya disimpan. Jika nanti Anda perlu menyimpan cache gambar, mengubah CSS, atau mencatat penggunaan sumber daya, Anda dapat mengganti `MemoryStream` dengan implementasi aliran khusus apa pun.

## Langkah 2: Konfigurasikan `HTMLLoadOptions` untuk menggunakan handler

`HTMLLoadOptions` memungkinkan Anda menyambungkan handler ke pipeline pemuatan. Menetapkan properti `ResourceHandler` memberi tahu viewer untuk memanggil `MyHandler` untuk setiap aset eksternal.

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**Mengapa ini penting:**  
Tanpa menetapkan `ResourceHandler`, viewer akan menulis sumber daya ke lokasi defaultnya (seringkali folder sementara). Dengan menentukan handler Anda sendiri, Anda **create custom resource handler** yang selaras dengan strategi penyimpanan aplikasi Anda.

## Langkah 3: Muat dokumen HTML dengan opsi yang telah dikonfigurasi

Sekarang muat file HTML. Viewer akan memanggil `MyHandler.HandleResource` untuk setiap sumber daya yang ditemukannya.

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

Pada titik ini konten HTML telah diparse, dan semua sumber daya eksternal telah dialirkan ke buffer memori yang disediakan oleh `MyHandler`.

## Langkah 4 (opsional): Akses sumber daya yang ditangkap

Jika Anda perlu memeriksa atau menyimpan sumber daya, Anda dapat memodifikasi `MyHandler` untuk menyimpan setiap `MemoryStream` dalam kamus yang diindeks dengan nama sumber daya.

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

Setelah pemuatan, Anda dapat mengiterasi `handler.Resources` dan menulis masing‑masing ke disk:

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**Mengapa ini penting:**  
Menyimpan sumber daya memungkinkan pemrosesan lanjutan seperti optimasi gambar, minifikasi CSS, atau pengarsipan. Ini juga memberikan verifikasi nyata bahwa logika **create custom resource handler** berfungsi sebagaimana mestinya.

## Langkah 5: Bersihkan

Baik `HTMLDocument` maupun aliran apa pun harus dibuang untuk membebaskan sumber daya yang tidak dikelola.

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## Contoh lengkap yang dapat dijalankan

Berikut adalah program mandiri yang mendemonstrasikan semua langkah mulai dari definisi kelas hingga ekstraksi sumber daya.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**Output yang diharapkan**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

Konsol akan menampilkan setiap sumber daya yang dialirkan viewer melalui handler khusus Anda, mengonfirmasi bahwa alur kerja **create custom resource handler** berhasil.

## Pertanyaan umum dan kasus tepi

| Pertanyaan | Jawaban |
|------------|---------|
| *Bagaimana jika sebuah sumber daya berukuran besar (misalnya gambar resolusi tinggi)?* | Ganti `MemoryStream` dengan `FileStream` yang mengarah ke folder sementara. Ini mencegah konsumsi memori yang berlebihan. |
| *Bisakah saya memfilter sumber daya berdasarkan tipe?* | Di dalam `HandleResource`, periksa `info.MimeType` atau `info.Extension` dan kembalikan `null` untuk tipe yang tidak diinginkan. Mengembalikan `null` memberi tahu viewer untuk melewatkan sumber daya tersebut. |
| *Apakah diperlukan keamanan thread?* | Jika instance handler yang sama digunakan pada beberapa pemuatan bersamaan, lindungi kamus `Resources` dengan lock atau gunakan koleksi bersamaan. |
| *Bagaimana cara mendukung URL relatif?* | `ResourceInfo` berisi URL asli; Anda dapat menggabungkannya dengan jalur dasar file HTML untuk menyelesaikan referensi relatif sebelum menyimpan. |

## Kesimpulan

Anda kini tahu cara **create custom resource handler** di C# untuk pemuatan HTML, mengonfigurasi `HTMLLoadOptions`, menangkap aset yang dialirkan, dan membersihkan secara bertanggung jawab. Pola ini memberi Anda kontrol penuh atas manajemen sumber daya, memungkinkan skenario seperti pemrosesan gambar secara langsung, penulisan ulang CSS, atau penyimpanan aman.

Selanjutnya, jelajahi topik terkait seperti **HTMLDocument loading** dengan opsi rendering yang berbeda, atau perpanjang handler menjadi implementasi **C# resource handler** yang menulis langsung ke penyimpanan cloud. Bereksperimenlah dengan metode `HandleResource` handler untuk menyesuaikannya dengan alur kerja sumber daya spesifik proyek Anda.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Custom Resource Handler in C# – Convert HTML to ZIP Tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}