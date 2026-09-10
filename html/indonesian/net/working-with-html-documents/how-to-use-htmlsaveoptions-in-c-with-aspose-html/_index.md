---
category: general
date: 2026-09-10
description: Pelajari cara menggunakan HtmlSaveOptions dalam C# untuk mengontrol gaya
  web‑font dan menyimpan file HTML dengan Aspose.HTML. Contoh kode lengkap serta tips
  praktis disertakan.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use htmlsaveoptions
- Aspose HTML library
- WebFontStyle flags
- HTMLDocument conversion
- C# save HTML
- Aspose.Html SaveOptions
language: id
lastmod: 2026-09-10
og_description: Cara menggunakan HtmlSaveOptions di C# untuk mengaktifkan gaya huruf
  tebal dan miring pada web‑font saat menyimpan HTML dengan Aspose.HTML. Ikuti contoh
  lengkap dan tips praktik terbaik.
og_image_alt: Screenshot showing how to use HtmlSaveOptions to save an HTML file in
  C#
og_title: Cara menggunakan HtmlSaveOptions di C# dengan Aspose.HTML – panduan langkah
  demi langkah
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  headline: How to use HtmlSaveOptions in C# with Aspose.HTML
  type: TechArticle
- description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  name: How to use HtmlSaveOptions in C# with Aspose.HTML
  steps:
  - name: Why configure WebFontStyle?
    text: 'When you export an HTML document, Aspose.HTML can embed web fonts that
      match the original styling. By setting `WebFontStyle`, you tell the exporter
      which font variants to include. This reduces the final file size when you only
      need specific styles and guarantees that the rendered output matches the '
  - name: 5.1 Controlling CSS embedding
    text: 'You can decide whether to embed CSS inline, keep external links, or embed
      everything:'
  - name: 5.2 Saving to a specific encoding
    text: '```csharp saveOptions.Encoding = Encoding.UTF8; ```'
  - name: 5.3 Handling large documents
    text: 'For very large HTML files, consider streaming the output to avoid high
      memory consumption:'
  - name: 5.4 Error handling best practice
    text: 'Wrap the entire workflow in a try‑catch block and log the exception details.
      This ensures that any I/O or parsing errors are captured:'
  - name: Expected console output
    text: '``` HTML saved successfully to ''YOUR_DIRECTORY/output.html''. ```'
  type: HowTo
tags:
- Aspose.HTML
- C#
- HTML processing
title: Cara menggunakan HtmlSaveOptions di C# dengan Aspose.HTML
url: /id/net/working-with-html-documents/how-to-use-htmlsaveoptions-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan HtmlSaveOptions di C# dengan Aspose.HTML

Jika Anda perlu mengontrol cara Aspose.HTML menyimpan dokumen HTML, **memahami cara menggunakan HtmlSaveOptions sangat penting**. Tutorial ini menunjukkan langkah‑demi‑langkah cara menggunakan HtmlSaveOptions untuk mengaktifkan gaya web‑font tebal dan miring saat menyimpan dokumen.

Pustaka Aspose HTML menyediakan API yang kaya untuk memuat, memanipulasi, dan mengekspor konten HTML. Pada akhir panduan ini Anda akan dapat:

* Memuat file HTML yang ada ke dalam sebuah `HTMLDocument`.
* Mengonfigurasi `HtmlSaveOptions` untuk menerapkan flag `WebFontStyle` tertentu.
* Menyimpan dokumen yang telah dimodifikasi ke lokasi baru atau ke stream.
* Memperluas solusi untuk gaya font lain, CSS khusus, dan penanganan error.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* .NET 6.0 atau yang lebih baru terpasang.
* Lisensi yang valid untuk **Aspose.HTML for .NET** (versi trial gratis dapat digunakan untuk contoh ini).
* Visual Studio 2022 (atau IDE C# lain) untuk mengkompilasi dan menjalankan kode.

Tidak ada paket NuGet tambahan yang diperlukan selain `Aspose.HTML`.

## Langkah 1: Siapkan proyek dan impor namespace

Buat proyek **Console App** baru dan tambahkan paket NuGet Aspose.HTML:

```bash
dotnet add package Aspose.HTML
```

Kemudian, di bagian atas `Program.cs`, impor namespace yang diperlukan:

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

Namespace ini menyediakan tipe `HTMLDocument`, `HtmlSaveOptions`, dan `WebFontStyle` yang akan Anda gunakan sepanjang tutorial.

## Langkah 2: Muat dokumen HTML sumber

Operasi pertama adalah membaca HTML yang ingin Anda proses. Ganti `"YOUR_DIRECTORY/input.html"` dengan jalur sebenarnya ke file Anda.

```csharp
// Load the source HTML document from disk
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

`HTMLDocument` mem-parsing markup, membangun pohon DOM, dan menyiapkannya untuk manipulasi. Jika file tidak ada, akan dilemparkan exception, sehingga Anda mungkin ingin membungkus pemanggilan ini dalam blok try‑catch untuk kode produksi.

## Langkah 3: Buat dan konfigurasikan HtmlSaveOptions

`HtmlSaveOptions` memungkinkan Anda menyesuaikan proses penyimpanan. Untuk mengaktifkan gaya web‑font tebal dan mirik, gabungkan flag `WebFontStyle` yang bersesuaian menggunakan operator bitwise OR (`|`).

```csharp
// Create a new HtmlSaveOptions instance
HtmlSaveOptions saveOptions = new HtmlSaveOptions();

// Enable bold and italic web‑font styles (equivalent to the old FontStyle flags)
saveOptions.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

### Mengapa mengonfigurasi WebFontStyle?

Saat Anda mengekspor dokumen HTML, Aspose.HTML dapat menyematkan web font yang cocok dengan gaya asli. Dengan mengatur `WebFontStyle`, Anda memberi tahu exporter varian font mana yang harus disertakan. Ini mengurangi ukuran file akhir ketika Anda hanya membutuhkan gaya tertentu dan memastikan bahwa output yang di‑render cocok dengan sumber.

#### Variasi umum

| Gaya yang diinginkan | Flag `WebFontStyle` yang bersesuaian |
|----------------------|--------------------------------------|
| Normal (regular)    | `WebFontStyle.Regular` |
| Bold                 | `WebFontStyle.Bold` |
| Italic               | `WebFontStyle.Italic` |
| Bold + Italic        | `WebFontStyle.Bold | WebFontStyle.Italic` |
| Semua varian         | `WebFontStyle.All` |

Anda dapat menggabungkan kombinasi apa pun yang sesuai dengan skenario Anda.

## Langkah 4: Simpan dokumen dengan opsi yang telah dikonfigurasi

Sekarang tulis dokumen ke file baru. Metode `Save` menerima jalur target dan instance `HtmlSaveOptions` yang telah Anda siapkan.

```csharp
// Save the processed HTML using the configured options
document.Save("YOUR_DIRECTORY/output.html", saveOptions);
```

Jika Anda perlu menulis ke memory stream (misalnya, untuk mengirim file melalui HTTP), gunakan overload yang menerima objek `Stream`:

```csharp
using (var stream = new MemoryStream())
{
    document.Save(stream, saveOptions);
    // Reset the position to read the content later
    stream.Position = 0;
    // Example: return the stream from a Web API endpoint
}
```

## Langkah 5: Verifikasi hasilnya

Buka `output.html` di browser atau periksa file dengan editor teks. Anda akan melihat bahwa blok `<style>` kini berisi aturan `@font-face` untuk varian tebal dan miring dari semua web font yang direferensikan dalam dokumen asli.

**Potongan output yang diharapkan:**

```html
<link rel="stylesheet" href="fonts/Roboto-Bold.woff2" type="font/woff2">
<link rel="stylesheet" href="fonts/Roboto-Italic.woff2" type="font/woff2">
```

Jika HTML asli mereferensikan keluarga font yang hanya memiliki berat regular, Aspose.HTML hanya akan menyertakan file tersebut, sesuai dengan konfigurasi `WebFontStyle`.

## Lanjutan: Menggunakan HtmlSaveOptions dengan fitur tambahan

### 5.1 Mengontrol penyematan CSS

Anda dapat memutuskan apakah akan menyematkan CSS secara inline, mempertahankan tautan eksternal, atau menyematkan semuanya:

```csharp
saveOptions.CssSavingMode = CssSavingMode.EmbedAllCss;
```

### 5.2 Menyimpan dengan encoding tertentu

```csharp
saveOptions.Encoding = Encoding.UTF8;
```

### 5.3 Menangani dokumen besar

Untuk file HTML yang sangat besar, pertimbangkan streaming output untuk menghindari konsumsi memori yang tinggi:

```csharp
using (FileStream fs = new FileStream("large_output.html", FileMode.Create, FileAccess.Write))
{
    document.Save(fs, saveOptions);
}
```

### 5.4 Praktik terbaik penanganan error

Bungkus seluruh alur kerja dalam blok try‑catch dan log detail exception. Ini memastikan setiap error I/O atau parsing tertangkap:

```csharp
try
{
    // Load, configure, and save as shown earlier
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error processing HTML: {ex.Message}");
}
```

## Tips pro: Menggunakan kembali HtmlSaveOptions untuk banyak penyimpanan

Jika Anda perlu menyimpan beberapa dokumen dengan konfigurasi gaya‑font yang sama, buat satu instance `HtmlSaveOptions` dan gunakan kembali. Ini mengurangi overhead alokasi objek dan menjamin output yang konsisten.

```csharp
HtmlSaveOptions sharedOptions = new HtmlSaveOptions
{
    WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
    CssSavingMode = CssSavingMode.EmbedAllCss
};

foreach (var file in Directory.GetFiles("input_folder", "*.html"))
{
    HTMLDocument doc = new HTMLDocument(file);
    string outputPath = Path.Combine("output_folder", Path.GetFileName(file));
    doc.Save(outputPath, sharedOptions);
}
```

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang menggabungkan semua langkah yang dibahas. Salin ke `Program.cs` dan jalankan setelah menyesuaikan jalur file.

```csharp
using System;
using System.IO;
using System.Text;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath = "YOUR_DIRECTORY/input.html";
        string outputPath = "YOUR_DIRECTORY/output.html";

        try
        {
            // Step 1: Load the source HTML document
            HTMLDocument document = new HTMLDocument(inputPath);

            // Step 2: Create HtmlSaveOptions and enable bold + italic web‑font styles
            HtmlSaveOptions saveOptions = new HtmlSaveOptions
            {
                WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
                // Optional: embed all CSS and use UTF‑8 encoding
                CssSavingMode = CssSavingMode.EmbedAllCss,
                Encoding = Encoding.UTF8
            };

            // Step 3: Save the document with the configured options
            document.Save(outputPath, saveOptions);

            Console.WriteLine($"HTML saved successfully to '{outputPath}'.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### Output konsol yang diharapkan

```
HTML saved successfully to 'YOUR_DIRECTORY/output.html'.
```

Buka `output.html` yang dihasilkan untuk memastikan bahwa gaya web‑font tebal dan miring sudah ada.

## Kesimpulan

Anda kini mengetahui **cara menggunakan HtmlSaveOptions** untuk mengontrol penyematan web‑font, penanganan CSS, dan encoding saat menyimpan HTML dengan pustaka Aspose HTML di C#. Dengan mengonfigurasi flag `WebFontStyle` Anda dapat menyesuaikan output agar hanya menyertakan varian font yang diperlukan, yang meningkatkan kinerja dan mengurangi ukuran file.

Selanjutnya Anda dapat menjelajahi properti `HtmlSaveOptions` lainnya seperti `ImageSavingMode`, `JavaScriptSavingMode`, atau menggabungkan beberapa opsi untuk pipeline konversi yang kompleks. Bereksperimenlah dengan penyimpanan ke stream untuk API web, atau integrasikan alur kerja ini ke dalam sistem generasi dokumen yang lebih besar.

---


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang berhubungan erat dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Save HTML with Aspose.Html – Complete C# Guide](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [How to Use Aspose to Render HTML to PNG in C#](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-in-c/)
- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}