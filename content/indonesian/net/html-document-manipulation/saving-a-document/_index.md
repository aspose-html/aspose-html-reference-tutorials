---
title: Menyimpan Dokumen di .NET dengan Aspose.HTML
linktitle: Menyimpan Dokumen di .NET
second_title: Aspose.HTML .NET API manipulasi HTML
description: Buka kekuatan Aspose.HTML untuk .NET dengan panduan langkah demi langkah kami. Pelajari cara membuat, memanipulasi, dan mengonversi dokumen HTML dan SVG
type: docs
weight: 16
url: /id/net/html-document-manipulation/saving-a-document/
---

Di era digital saat ini, membuat dan memanipulasi dokumen HTML dan SVG sangat penting bagi banyak pengembang perangkat lunak dan bisnis. Aspose.HTML untuk .NET adalah perpustakaan canggih yang menyederhanakan tugas-tugas ini, menawarkan berbagai fungsi untuk bekerja dengan HTML, SVG, dan banyak lagi. Dalam panduan komprehensif ini, kami akan mendalami esensi Aspose.HTML untuk .NET, dan mengelompokkan setiap contoh menjadi langkah-langkah yang mudah diikuti. Baik Anda seorang pengembang berpengalaman atau baru memulai, Anda akan menemukan panduan ini sangat berharga untuk memanfaatkan kemampuan Aspose.HTML.

## Prasyarat

Sebelum kita memulai perjalanan ini, pastikan Anda memiliki semua yang Anda butuhkan:

- Lingkungan Pengembangan: Pastikan Anda memiliki Visual Studio atau lingkungan pengembangan .NET lainnya yang terinstal di komputer Anda.

- Aspose.HTML untuk .NET: Anda perlu mendapatkan perpustakaan Aspose.HTML untuk .NET. Anda dapat mengunduhnya dari[Di Sini](https://releases.aspose.com/html/net/).

- Pengetahuan tentang C#: Keakraban dengan bahasa pemrograman C# bermanfaat tetapi tidak wajib. Panduan ini dirancang agar ramah bagi pemula.

## Impor Ruang Nama

Untuk mulai menggunakan Aspose.HTML untuk .NET, Anda harus mengimpor namespace yang diperlukan ke dalam proyek Anda. Dalam kode C# Anda, sertakan namespace berikut:

### Langkah 1: Impor Namespace Aspose.HTML
```csharp
using Aspose.Html;
```

Namespace ini akan memberi Anda akses ke berbagai kemampuan manipulasi HTML dan SVG.

## HTML ke File

### Langkah 1: Inisialisasi Dokumen HTML Kosong
```csharp
// Inisialisasi Dokumen HTML kosong.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Buat elemen teks dan tambahkan ke dokumen
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Simpan HTML ke file di disk.
    document.Save("document.html");
}
```

Dalam contoh ini, kita membuat dokumen HTML dan menambahkan kalimat sederhana "Hello World!" teks ke sana. Kami kemudian menyimpan HTML ke file di disk.

## HTML Tanpa File Tertaut

### Langkah 1: Siapkan File HTML Sederhana
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Di sini, kita membuat file HTML dasar dengan link jangkar ke file lain.

### Langkah 2: Muat 'document.html' ke dalam Memori
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Buat contoh Simpan Opsi
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //Atur kedalaman penanganan maksimum ke 0 untuk memotong file HTML yang tertaut.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // Simpan dokumennya
    document.Save(@".\html-to-file-example\document.html", options);
}
```

Dalam contoh ini, kita memuat dokumen HTML ke dalam memori, mengatur kedalaman penanganan maksimum untuk memotong file tertaut, dan menyimpan dokumen. 

## HTML ke MHTML

### Langkah 1: Siapkan File HTML Sederhana
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Sama seperti pada Contoh 2, kita membuat file HTML dasar dengan link jangkar ke file lain.

### Langkah 2: Muat 'document.html' ke dalam Memori dan Simpan sebagai MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Simpan dokumen sebagai MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

Di sini, kami memuat dokumen HTML ke dalam memori dan menyimpannya dalam format MHTML.

## HTML ke Penurunan Harga

### Langkah 1: Siapkan Kode HTML
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 Pada langkah ini, kita mendefinisikan cuplikan kode HTML yang berisi`<H2>` elemen.

### Langkah 2: Inisialisasi Dokumen dari Kode HTML dan Simpan sebagai Penurunan Harga
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Simpan dokumen sebagai file penurunan harga.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

Kami membuat dokumen HTML dari cuplikan kode dan menyimpannya sebagai file Markdown.

## SVG ke File

### Langkah 1: Siapkan Kode SVG
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' height='80' width='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

Di sini, kami membuat kode SVG yang menggambar grafik sederhana dan penuh warna.

### Langkah 2: Inisialisasi Dokumen SVG dari Kode dan Simpan ke Disk
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // Simpan file SVG ke disk
    document.Save("document.svg");
}
```

Pada langkah ini, kita membuat dokumen SVG dari kode dan menyimpannya sebagai file SVG.

## Kesimpulan

Aspose.HTML untuk .NET adalah perpustakaan serbaguna yang menyederhanakan penanganan dokumen HTML dan SVG dalam aplikasi .NET Anda. Dalam panduan ini, kami telah membahas lima contoh penting, dan mengelompokkannya menjadi petunjuk langkah demi langkah. Baik Anda membuat, memanipulasi, atau mengonversi dokumen, Aspose.HTML siap membantu Anda. Dengan mengikuti langkah-langkah ini, Anda sudah siap untuk menguasai alat canggih ini.

## FAQ

### Q1: Apa itu Aspose.HTML untuk .NET?

A1: Aspose.HTML untuk .NET adalah pustaka .NET yang menyediakan berbagai fitur untuk bekerja dengan dokumen HTML dan SVG, termasuk pembuatan, manipulasi, dan konversi.

### Q2: Di mana saya dapat mengunduh Aspose.HTML untuk .NET?

 A2: Anda dapat mengunduh Aspose.HTML untuk .NET dari[Di Sini](https://releases.aspose.com/html/net/).

### Q3: Apakah Aspose.HTML untuk .NET cocok untuk pemula?

A3: Ya, Aspose.HTML untuk .NET dapat digunakan oleh pemula dan pengembang berpengalaman. Contoh dalam panduan ini dirancang agar ramah bagi pemula.

### Q4: Dapatkah saya mengonversi HTML ke format lain menggunakan Aspose.HTML untuk .NET?

A4: Ya, Aspose.HTML untuk .NET mendukung konversi ke berbagai format, termasuk MHTML dan Markdown, seperti yang ditunjukkan dalam contoh.

### Q5: Di mana saya bisa mendapatkan dukungan Aspose.HTML untuk .NET?

 A5: Anda dapat menemukan dukungan dan jawaban atas pertanyaan Anda di forum komunitas Aspose.HTML[Di Sini](https://forum.aspose.com/).