---
category: general
date: 2026-10-21
description: Pelajari cara menyimpan HTML sebagai ZIP menggunakan Aspose.HTML, mengonversi
  HTML ke ZIP, dan menghapus sumber daya untuk paket yang bersih.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save html as zip
- convert html to zip
- how to omit resources
- how to strip resources
- create html zip
language: id
lastmod: 2026-10-21
og_description: Simpan HTML sebagai ZIP dengan Aspose.HTML, pelajari cara mengonversi
  HTML ke ZIP dan menghapus sumber daya untuk arsip yang ringan.
og_image_alt: Screenshot showing the save html as zip process with resources omitted
og_title: Simpan HTML sebagai ZIP dengan Aspose.HTML – abaikan sumber daya dalam satu
  langkah
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to save HTML as ZIP using Aspose.HTML, convert HTML to ZIP,
    and strip resources for a clean package.
  headline: How to save HTML as ZIP with Aspose.HTML and omit resources
  type: TechArticle
tags:
- Aspose.HTML
- C#
- ZIP archive
- HTML conversion
- Resource handling
title: Cara menyimpan HTML sebagai ZIP dengan Aspose.HTML dan mengabaikan sumber daya
url: /id/net/html-extensions-and-conversions/how-to-save-html-as-zip-with-aspose-html-and-omit-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyimpan HTML sebagai ZIP dengan Aspose.HTML dan menghilangkan sumber daya

Jika Anda perlu **menyimpan HTML sebagai ZIP** sambil menghapus file eksternal, panduan ini menunjukkan solusi lengkap yang siap dijalankan. Pada akhir tutorial Anda akan dapat **mengonversi HTML ke ZIP**, mengontrol sumber daya mana yang disimpan, dan menghasilkan arsip bersih yang hanya berisi markup inti.

Banyak skenario otomasi web memerlukan pengemasan halaman untuk penggunaan offline, lampiran email, atau penyimpanan arsip. Menyertakan gambar, font, atau skrip sering kali membuat arsip menjadi terlalu besar. Langkah‑langkah di bawah ini menjelaskan **cara menghilangkan sumber daya** dan **cara menghapus sumber daya** dari output, sehingga ZIP yang dihasilkan tetap ringan.

## Prasyarat

- .NET 6.0 atau yang lebih baru terinstal  
- Lisensi Aspose.HTML untuk .NET (atau evaluasi gratis)  
- Lingkungan pengembangan C# dasar (Visual Studio, VS Code, atau Rider)  

Tidak ada paket NuGet tambahan yang diperlukan selain `Aspose.Html`.

## Langkah 1: Buat handler sumber daya khusus

Inti dari **cara menghilangkan sumber daya** terletak pada subclass `ResourceHandler`. Aspose.HTML memanggil handler ini untuk setiap aset eksternal (gambar, CSS, skrip). Dengan mengembalikan stream kosong, Anda secara efektif memberi tahu konverter untuk melewatkan aset tersebut.

```csharp
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Prevents external resources from being written to the output package.
/// </summary>
class CustomResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Returning an empty MemoryStream strips the resource from the ZIP.
        return new MemoryStream();
    }
}
```

**Mengapa ini penting:** Perilaku default menyalin setiap file yang terhubung ke dalam ZIP, yang dapat menggandakan atau melipatgandakan ukuran file. Menimpa `HandleResource` memberi Anda kontrol yang halus tanpa mengubah HTML asli.

## Langkah 2: Muat dokumen HTML

Muat file sumber dengan `HTMLDocument`. Konstruktor menerima jalur file, URL, atau stream. Pada contoh ini kami membaca file lokal bernama `input.html`.

```csharp
// Load the source HTML file from the local file system.
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

Jika HTML Anda berada di memori atau berasal dari permintaan web, Anda dapat memberikan `MemoryStream` atau string URL sebagai gantinya. API berfungsi dengan cara yang sama.

## Langkah 3: Konfigurasikan opsi penyimpanan

Buat instance `HtmlSaveOptions` dan tetapkan handler khusus yang dibuat pada Langkah 1. Ini memberi tahu Aspose.HTML untuk menggunakan handler setiap kali menemukan sumber daya.

```csharp
// Prepare save options and attach the custom resource handler.
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // The ResourceHandler property is what enables resource stripping.
    ResourceHandler = new CustomResourceHandler()
};
```

Anda juga dapat menyesuaikan opsi lain di sini, seperti `CompressImages = false` jika ingin menyimpan data gambar tetapi tetap menghilangkan aset lainnya. Contoh ini mempertahankan pengaturan kompresi default.

## Langkah 4: Simpan dokumen sebagai arsip ZIP

Akhirnya, panggil `Save` dengan jalur target dan opsi yang telah dikonfigurasi. File output akan menjadi `.zip` yang berisi `index.html` (atau nama file asli) dan **tidak ada sumber daya eksternal**.

```csharp
// Save the HTML document as a ZIP file. The archive will contain only the HTML markup.
document.Save("YOUR_DIRECTORY/output.zip", saveOptions);
```

### Hasil yang diharapkan

- `output.zip` → berisi satu file `index.html`.  
- Semua gambar, file CSS, dan referensi JavaScript dihilangkan, karena handler khusus mengembalikan stream kosong untuk masing‑masing.

Anda dapat memverifikasi arsip dengan membukanya menggunakan penampil ZIP apa pun. Halaman HTML masih akan merujuk ke URL asli, tetapi file‑file tersebut tidak ada dalam arsip, sehingga paket tetap minimal.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin, tempel, dan jalankan. Ganti `YOUR_DIRECTORY` dengan jalur folder yang sebenarnya di mesin Anda.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

class Program
{
    static void Main()
    {
        // Step 1: Define a custom resource handler to control how external resources are saved.
        class CustomResourceHandler : ResourceHandler
        {
            public override Stream HandleResource(ResourceInfo info)
            {
                // Returning an empty stream strips the resource from the ZIP output.
                return new MemoryStream();
            }
        }

        // Step 2: Load an HTML document from a file.
        string inputPath = "YOUR_DIRECTORY/input.html";
        HTMLDocument document = new HTMLDocument(inputPath);

        // Step 3: Create HTML save options and assign the custom handler.
        HtmlSaveOptions saveOptions = new HtmlSaveOptions
        {
            ResourceHandler = new CustomResourceHandler()
        };

        // Step 4: Save the document as a ZIP archive containing the HTML and (now omitted) resources.
        string outputPath = "YOUR_DIRECTORY/output.zip";
        document.Save(outputPath, saveOptions);

        Console.WriteLine($"HTML has been saved as ZIP at: {outputPath}");
    }
}
```

Menjalankan program ini menghasilkan file ZIP yang dijelaskan sebelumnya. Sekarang Anda dapat mendistribusikan halaman HTML tanpa menyertakan aset yang tidak diperlukan.

## Variasi umum dan kasus tepi

| Scenario | Adjustment |
|----------|------------|
| **Simpan gambar tetapi hapus CSS/JS** | Di `CustomResourceHandler`, periksa `info.MimeType`. Kembalikan `MemoryStream` hanya untuk `text/css` dan `application/javascript`. |
| **Pertahankan font eksternal** | Kembalikan stream asli untuk tipe MIME `font/woff2`, jika tidak kembalikan stream kosong. |
| **Buat ZIP dengan nama entri khusus** | Gunakan overload `HtmlSaveOptions` `Save(string path, SaveOptions options, string entryName)` untuk menentukan nama file root yang berbeda. |
| **Konversi beberapa file HTML menjadi satu ZIP** | Lakukan loop pada setiap file, buat `HTMLDocument` terpisah, dan tambahkan masing‑masing ke `ZipArchive` yang sama secara manual menggunakan `System.IO.Compression`. |

## Tips profesional

- **Validasi hasil**: Setelah menyimpan, buka ZIP dan muat `index.html` di browser. Sumber daya yang hilang akan muncul sebagai tautan rusak, menegaskan bahwa handler berfungsi.  
- **Kinerja**: Mengembalikan `MemoryStream` kosong murah, tetapi jika Anda memiliki ribuan aset, pertimbangkan untuk menyimpan keputusan dalam cache (misalnya, `HashSet<string>` tipe MIME yang akan dilewati).  
- **Lisensi**: Versi evaluasi gratis Aspose.HTML menambahkan komentar watermark di dalam HTML. Gunakan versi berlisensi untuk menghapusnya pada penggunaan produksi.  

## Kesimpulan

Anda sekarang tahu cara **menyimpan HTML sebagai ZIP**, **mengonversi HTML ke ZIP**, dan **menghapus sumber daya** menggunakan Aspose.HTML untuk .NET. Dengan mengimplementasikan `ResourceHandler` khusus, Anda dapat menghilangkan file yang tidak diinginkan dan menjaga arsip tetap ringan. Bereksperimenlah dengan logika handler untuk menyimpan hanya sumber daya yang benar‑benar Anda perlukan, dan integrasikan pola ini ke dalam pipeline otomasi yang lebih besar.

---

**Langkah selanjutnya**

- Jelajahi fitur lain `HtmlSaveOptions` seperti `EmbedImages` untuk menyematkan gambar langsung ke dalam HTML.  
- Gabungkan pendekatan ini dengan `Aspose.PDF` untuk mengonversi HTML yang sama menjadi PDF setelah membuat ZIP.  
- Pelajari skenario sisi‑server di mana Anda menghasilkan ZIP sesuai permintaan dan mengalirkannya ke klien tanpa menulis ke disk.  

Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menggunakan ZipArchive – Simpan HTML dan Sumber Daya ke File ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [Cara Menyimpan HTML di C# – Handler Sumber Daya Kustom & ZIP](/html/english/net/working-with-html-documents/how-to-save-html-in-c-custom-resource-handlers-zip/)
- [Cara Menyimpan HTML sebagai ZIP di C# – Panduan Lengkap Aspose.HTML](/html/english/net/html-extensions-and-conversions/how-to-save-html-as-zip-in-c-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}