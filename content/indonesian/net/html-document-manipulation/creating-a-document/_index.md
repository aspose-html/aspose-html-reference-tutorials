---
title: Membuat Dokumen di .NET dengan Aspose.HTML
linktitle: Membuat Dokumen di .NET
second_title: Aspose.HTML .NET API manipulasi HTML
description: Bebaskan Kekuatan Aspose.HTML untuk .NET. Belajar Membuat, Memanipulasi, dan Mengoptimalkan Dokumen HTML dan SVG dengan Mudah. Jelajahi Contoh Langkah-demi-Langkah dan FAQ.
type: docs
weight: 14
url: /id/net/html-document-manipulation/creating-a-document/
---

Dalam dunia pengembangan web yang terus berkembang, menjadi yang terdepan sangatlah penting. Aspose.HTML untuk .NET memberi pengembang perangkat yang tangguh untuk bekerja dengan dokumen HTML. Baik Anda memulai dari awal, memuat dari file, mengambil dari URL, atau menangani dokumen SVG, perpustakaan ini menawarkan keserbagunaan yang Anda perlukan.

Dalam panduan langkah demi langkah ini, kami akan mempelajari dasar-dasar penggunaan Aspose.HTML untuk .NET, memastikan Anda siap menggunakan alat canggih ini dalam proyek pengembangan web Anda. Sebelum kita mendalami detailnya, mari kita bahas prasyarat dan namespace yang diperlukan untuk memulai perjalanan Anda.

## Prasyarat

Agar berhasil mengikuti tutorial ini dan memanfaatkan kekuatan Aspose.HTML untuk .NET, Anda memerlukan prasyarat berikut:

- Mesin Windows dengan .NET Framework atau .NET Core terinstal.
- Editor kode seperti Visual Studio.
- Pengetahuan dasar tentang pemrograman C#.

Sekarang setelah Anda memiliki prasyarat, mari kita mulai.

## Mengimpor Namespace

Sebelum Anda mulai menggunakan Aspose.HTML untuk .NET, Anda perlu mengimpor namespace yang diperlukan. Namespace ini berisi kelas dan metode yang penting untuk bekerja dengan dokumen HTML. Di bawah ini adalah daftar namespace yang harus Anda impor:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Dengan mengimpor namespace ini, Anda sekarang siap untuk mendalami contoh langkah demi langkah.

## Membuat Dokumen HTML dari Awal

### Langkah 1: Inisialisasi Dokumen HTML Kosong

```csharp
// Inisialisasi Dokumen HTML kosong.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Buat elemen teks dan tambahkan ke dokumen
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Simpan dokumen ke disk.
    document.Save("document.html");
}
```

Dalam contoh ini, kita mulai dengan membuat dokumen HTML kosong dan menambahkan teks "Hello World!" teks ke sana. Kami kemudian menyimpan dokumen ke file.

## Membuat Dokumen HTML dari File

### Langkah 1: Siapkan file 'document.html'

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### Langkah 2: Muat dari file 'document.html'

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Tulis konten dokumen ke aliran keluaran.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Di sini, kami menyiapkan file dengan "Hello World!" konten dan kemudian memuatnya sebagai dokumen HTML. Kami mencetak konten dokumen ke konsol.

## Membuat Dokumen HTML dari URL

### Langkah 1: Muat dokumen dari halaman web

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // Tulis konten dokumen ke aliran keluaran.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Dalam contoh ini, kita memuat dokumen HTML langsung dari halaman web dan menampilkan kontennya.

## Membuat Dokumen HTML dari String

### Langkah 1: Siapkan kode HTML

```csharp
var html_code = "<p>Hello World!</p>";
```

### Langkah 2: Inisialisasi dokumen dari variabel string

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Simpan dokumen ke disk.
    document.Save("document.html");
}
```

Di sini, kita membuat dokumen HTML dari variabel string dan menyimpannya ke file.

## Membuat Dokumen HTML dari MemoryStream

### Langkah 1: Buat objek aliran memori

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // Tulis Kode HTML ke dalam objek memori
    sw.Write("<p>Hello World!</p>");
    // Atur posisinya ke awal
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // Inisialisasi dokumen dari aliran memori
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // Simpan dokumen ke disk.
        document.Save("document.html");
    }
}
```

Dalam contoh ini, kita membuat dokumen HTML dari aliran memori dan menyimpannya ke file.

## Bekerja dengan Dokumen SVG

### Langkah 1: Inisialisasi Dokumen SVG dari sebuah string

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // Tulis konten dokumen ke aliran keluaran.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Di sini, kami membuat dan menampilkan dokumen SVG dari sebuah string.

## Memuat Dokumen HTML Secara Asinkron

### Langkah 1: Buat instance Dokumen HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Langkah 2: Berlangganan acara 'ReadyStateChange'

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    //Periksa nilai properti 'ReadyState'.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Langkah 3: Menavigasi secara asinkron pada Uri yang ditentukan

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Dalam contoh ini, kita memuat dokumen HTML secara asinkron dan menangani event 'ReadyStateChange' untuk menampilkan konten saat pemuatan selesai.

## Menangani Acara 'OnLoad'

### Langkah 1: Buat instance Dokumen HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Langkah 2: Berlangganan acara 'OnLoad'

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### Langkah 3: Menavigasi secara asinkron pada Uri yang ditentukan

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Contoh ini menunjukkan pemuatan dokumen HTML secara asinkron dan menangani peristiwa 'OnLoad' untuk menampilkan konten setelah selesai.

## Kesimpulannya

Dalam dunia pengembangan web yang dinamis, memiliki alat yang tepat sangatlah penting. Aspose.HTML untuk .NET membekali Anda dengan sarana untuk membuat, memanipulasi, dan memproses dokumen HTML dan SVG secara efisien. Panduan komprehensif ini telah memandu Anda memahami hal-hal penting, memastikan bahwa Anda dapat memanfaatkan kekuatan Aspose.HTML untuk .NET dalam proyek Anda.

## FAQ

### Q1: Apa itu Aspose.HTML untuk .NET?

A1: Aspose.HTML untuk .NET adalah pustaka .NET canggih yang memungkinkan pengembang bekerja dengan dokumen HTML dan SVG. Ini menyediakan berbagai fitur, mulai dari membuat dokumen dari awal hingga menguraikan dan memanipulasi file HTML dan SVG yang ada.

### Q2: Bisakah saya menggunakan Aspose.HTML untuk .NET dengan .NET Core?

A2: Ya, Aspose.HTML untuk .NET kompatibel dengan .NET Framework dan .NET Core, menjadikannya pilihan serbaguna untuk aplikasi .NET modern.

### Q3: Apakah Aspose.HTML untuk .NET cocok untuk pengikisan dan penguraian web?

A3: Tentu saja! Aspose.HTML untuk .NET adalah pilihan yang sangat baik untuk tugas pengikisan dan penguraian web, berkat kemampuannya memuat dokumen HTML dari URL dan string. Anda dapat mengekstrak data, melakukan analisis, dan banyak lagi.

### Q4: Bagaimana cara mengakses dukungan Aspose.HTML untuk .NET?

 A4: Jika Anda mengalami masalah atau memiliki pertanyaan saat menggunakan Aspose.HTML untuk .NET, Anda dapat mengunjungi[Asumsikan Forum](https://forum.aspose.com/) atas dukungan dan bantuan dari masyarakat dan para ahli Aspose.

### A5: Di mana saya dapat menemukan dokumentasi terperinci dan opsi pengunduhan?

A5: Untuk dokumentasi komprehensif dan akses ke opsi pengunduhan, Anda dapat merujuk ke tautan berikut:

- [Dokumentasi](https://reference.aspose.com/html/net/)
- [Unduh](https://releases.aspose.com/html/net/)
- [Membeli](https://purchase.aspose.com/buy)
- [Uji Coba Gratis](https://releases.aspose.com/)
- [Lisensi Sementara](https://purchase.aspose.com/temporary-license/)