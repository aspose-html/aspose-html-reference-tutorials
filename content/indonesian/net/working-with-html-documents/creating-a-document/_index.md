---
title: Membuat Dokumen HTML di .NET dengan Aspose.HTML
linktitle: Membuat Dokumen HTML di .NET
second_title: Aspose.HTML .NET API manipulasi HTML
description: Pelajari cara membuat dokumen HTML di .NET menggunakan Aspose.HTML, dari awal atau dari URL. Tutorial komprehensif untuk pengembang web.
type: docs
weight: 10
url: /id/net/working-with-html-documents/creating-a-document/
---

Dalam bidang pengembangan web dan manipulasi data, memiliki alat yang ampuh untuk membuat, memodifikasi, dan bekerja dengan dokumen HTML sangat diperlukan. Aspose.HTML untuk .NET adalah salah satu alat yang dapat menyederhanakan tugas-tugas Anda yang berhubungan dengan HTML. Dalam tutorial komprehensif ini, kita akan mempelajari cara membuat dokumen HTML menggunakan Aspose.HTML untuk .NET langkah demi langkah. Sebelum kita mendalami contohnya, mari kita bahas beberapa prasyarat.

## Prasyarat

Sebelum Anda memulai perjalanan ini, pastikan Anda memiliki prasyarat berikut:

1. Visual Studio: Pastikan Anda telah menginstal Visual Studio di sistem Anda.

2.  Aspose.HTML untuk .NET: Unduh dan instal perpustakaan Aspose.HTML untuk .NET. Anda dapat menemukan tautan unduhan[Di Sini](https://releases.aspose.com/html/net/).

3. Pengetahuan Dasar C#: Biasakan diri Anda dengan dasar-dasar bahasa pemrograman C#.

Sekarang kita telah memenuhi prasyaratnya, mari kita mulai membuat dokumen HTML.

## Mengimpor Namespace

Pertama, Anda perlu mengimpor namespace yang diperlukan untuk menggunakan Aspose.HTML di proyek C# Anda. Tambahkan arahan penggunaan berikut ke file kode Anda:

```csharp
using Aspose.Html.Dom.Svg;
using Aspose.Html;
```

## Membuat Dokumen SVG

```csharp
static void CreateSVG()
{
    using (var document = new SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "about:blank"))
    {
        // Lakukan tindakan pada dokumen SVG di sini...
    }
}
```

 Dalam contoh ini, kami membuat dokumen SVG dengan menyediakan konten SVG dan URL dasar. Itu`SVGDocument`kelas dari Aspose.HTML untuk .NET memungkinkan Anda memanipulasi dokumen SVG dengan mudah.

## Membuat Dokumen HTML dari Awal

```csharp
static void FromScratch()
{
    using (var document = new HTMLDocument())
    {
        // Lakukan tindakan pada dokumen HTML di sini...
    }
}
```

 Contoh ini menunjukkan cara membuat dokumen HTML dari awal. Itu`HTMLDocument` kelas menyediakan kanvas kosong untuk konten HTML Anda.

## Membuat Dokumen HTML dari File Lokal

```csharp
static void FromLocalFile()
{
    string dataDir = "Your Data Directory";
    using (var document = new HTMLDocument(dataDir + "input.html"))
    {
        // Lakukan tindakan pada dokumen HTML di sini...
    }
}
```

 Jika Anda memiliki file HTML di sistem lokal Anda, Anda dapat memuatnya menggunakan`HTMLDocument` kelas, seperti yang ditunjukkan dalam contoh ini.

## Membuat Dokumen HTML dari URL Jarak Jauh

```csharp
static void FromRemoteURL()
{
    using (var document = new HTMLDocument("http://situs.com/"))
    {
        // Lakukan tindakan pada dokumen HTML di sini...
    }
}
```

Terkadang, Anda mungkin perlu bekerja dengan konten HTML yang dihosting di server jarak jauh. Contoh ini menunjukkan cara membuat dokumen HTML dari URL jarak jauh.

## Membuat Dokumen HTML dari URL Jarak Jauh (Alternatif)

```csharp
static void FromRemoteURL1()
{
    using (var document = new HTMLDocument(new Url("http://situs.com/")))
    {
        // Lakukan tindakan pada dokumen HTML di sini...
    }
}
```

Pendekatan alternatif ini juga menunjukkan cara membuat dokumen HTML dari URL jarak jauh menggunakan konstruktor berbeda.

## Membuat Dokumen HTML dari Konten HTML

```csharp
static void FromHTML()
{
    using (var document = new HTMLDocument("<p>my first paragraph</p>", "."))
    {
        // Lakukan tindakan pada dokumen HTML di sini...
    }
}
```

Jika Anda memiliki konten HTML dalam format string, Anda dapat membuat dokumen HTML dengannya, seperti yang ditunjukkan dalam contoh ini.

## Membuat Dokumen HTML dari Aliran

```csharp
static void FromStream()
{
    using (MemoryStream mem = new MemoryStream())
    using (StreamWriter sw = new StreamWriter(mem))
    {
        sw.Write("<p>my first paragraph</p>");
        sw.Flush();
        mem.Seek(0, SeekOrigin.Begin);
        using (var document = new HTMLDocument(mem, "about:blank"))
        {
            // Lakukan tindakan pada dokumen HTML di sini...
        }
    }
}
```

Dalam contoh ini, kami menunjukkan cara membuat dokumen HTML dari data dalam aliran memori. Ini dapat berguna ketika Anda memiliki konten HTML dalam aliran dan ingin memanipulasinya.

## Kesimpulan

Aspose.HTML untuk .NET menyediakan seperangkat alat canggih untuk membuat dan bekerja dengan dokumen HTML di aplikasi .NET Anda. Dengan contoh yang diberikan dalam tutorial ini, Anda dapat dengan mudah memulai pembuatan dokumen HTML, baik dari awal, file lokal, URL jarak jauh, atau konten HTML yang sudah ada.

 Ada pertanyaan atau butuh bantuan? Kunjungi forum komunitas Aspose.HTML untuk mendapatkan dukungan di[https://forum.aspose.com/](https://forum.aspose.com/).

## FAQ

### Q1: Apakah Aspose.HTML untuk .NET gratis untuk digunakan?
 A1: Aspose.HTML untuk .NET menawarkan uji coba gratis, namun untuk penggunaan penuh, Anda perlu membeli lisensi. Anda dapat menemukan rincian lebih lanjut di[https://purchase.aspose.com/buy](https://purchase.aspose.com/buy).

### Q2: Bagaimana saya bisa mendapatkan lisensi sementara Aspose.HTML untuk .NET?
A2: Jika Anda memerlukan lisensi sementara, Anda dapat memperolehnya di[https://purchase.aspose.com/temporary-license/](https://purchase.aspose.com/temporary-license/).

### Q3: Di mana saya dapat menemukan dokumentasi Aspose.HTML untuk .NET?
 A3: Dokumentasinya dapat ditemukan di[https://reference.aspose.com/html/net/](https://reference.aspose.com/html/net/).

### Q4: Apakah ada perpustakaan Aspose lain untuk pengembangan .NET?
 A4: Ya, Aspose menyediakan serangkaian perpustakaan untuk berbagai format file dan tugas manipulasi dokumen. Lihat penawaran mereka di[https://products.aspose.com/](https://products.aspose.com/).

### Q5: Bisakah saya menggunakan Aspose.HTML untuk .NET di aplikasi web saya?
A5: Ya, Aspose.HTML untuk .NET kompatibel dengan aplikasi web, menjadikannya pilihan serbaguna untuk proyek desktop dan berbasis web.
