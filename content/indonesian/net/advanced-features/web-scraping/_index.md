---
title: Pengikisan Web di .NET dengan Aspose.HTML
linktitle: Pengikisan Web di .NET
second_title: Aspose.HTML .NET API manipulasi HTML
description: Pelajari cara memanipulasi dokumen HTML di .NET dengan Aspose.HTML. Navigasi, filter, kueri, dan pilih elemen secara efektif untuk pengembangan web yang lebih baik.
type: docs
weight: 13
url: /id/net/advanced-features/web-scraping/
---

Di era digital saat ini, memanipulasi dan mengekstrak informasi dari dokumen HTML adalah tugas umum bagi pengembang. Aspose.HTML untuk .NET adalah alat canggih yang menyederhanakan pemrosesan dan manipulasi HTML dalam aplikasi .NET. Dalam tutorial ini, kita akan menjelajahi berbagai aspek Aspose.HTML untuk .NET, termasuk prasyarat, namespace, dan contoh langkah demi langkah untuk membantu Anda memanfaatkan potensi penuhnya.

## Prasyarat

Sebelum mendalami dunia Aspose.HTML untuk .NET, Anda memerlukan beberapa prasyarat:

1. Lingkungan Pengembangan: Pastikan Anda memiliki lingkungan pengembangan yang berfungsi dengan Visual Studio atau IDE lain yang kompatibel untuk pengembangan .NET.

2.  Aspose.HTML untuk .NET: Unduh dan instal perpustakaan Aspose.HTML untuk .NET dari[tautan unduhan](https://releases.aspose.com/html/net/). Anda dapat memilih antara versi uji coba gratis atau versi berlisensi berdasarkan kebutuhan Anda.

3. Pengetahuan Dasar tentang HTML: Keakraban dengan struktur dan elemen HTML sangat penting untuk menggunakan Aspose.HTML untuk .NET secara efektif.

## Mengimpor Namespace

Untuk memulai, Anda perlu mengimpor namespace yang diperlukan dalam proyek C# Anda. Namespace berikut menyediakan akses ke kelas dan fungsi Aspose.HTML untuk .NET:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

Dengan prasyarat yang ada dan namespace yang diimpor, mari kita uraikan beberapa contoh penting langkah demi langkah untuk mengilustrasikan cara menggunakan Aspose.HTML untuk .NET secara efektif.

## Menavigasi Melalui HTML

Dalam contoh ini, kita akan menavigasi dokumen HTML dan mengakses elemennya langkah demi langkah.

```csharp
public static void NavigateThroughHTML()
{
    // Siapkan kode HTML
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    // Inisialisasi dokumen dari kode yang telah disiapkan
    using (var document = new HTMLDocument(html_code, "."))
    {
        // Dapatkan referensi ke anak pertama (SPAN pertama) dari BODY
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // Keluaran: Halo

        // Dapatkan referensi spasi antar elemen HTML
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Keluaran: ''

        // Dapatkan referensi ke elemen SPAN kedua
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Keluaran: Dunia!
    }
}
```

 Dalam contoh ini, kita membuat dokumen HTML, mengakses anak pertamanya (a`SPAN` elemen), spasi antar elemen, dan yang kedua`SPAN` elemen, menunjukkan navigasi dasar.

## Menggunakan Filter Node

Filter node memungkinkan Anda memproses elemen tertentu secara selektif dalam dokumen HTML.

```csharp
public static void NodeFilterUsageExample()
{
    // Siapkan kode HTML
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    // Inisialisasi dokumen berdasarkan kode yang disiapkan
    using (var document = new HTMLDocument(code, "."))
    {
        // Buat TreeWalker dengan filter khusus untuk elemen gambar
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                // Keluaran: gambar1.png
                // Keluaran: gambar2.png
            }
        }
    }
}
```

 Contoh ini menunjukkan cara menggunakan filter simpul khusus untuk mengekstrak elemen tertentu (dalam hal ini,`IMG` elemen) dari dokumen HTML.

## Pertanyaan XPath

Kueri XPath memungkinkan Anda mencari elemen dalam dokumen HTML berdasarkan kriteria tertentu.

```csharp
public static void XPathQueryUsageExample()
{
    // Siapkan kode HTML
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello!</span>
            </div>
        </div>
        <p class='happy'>
            <span>World</span>
        </p>
    ";
    
    // Inisialisasi dokumen berdasarkan kode yang disiapkan
    using (var document = new HTMLDocument(code, "."))
    {
        // Evaluasi ekspresi XPath untuk memilih elemen tertentu
        var result = document.Evaluate("//*[@kelas='bahagia']//span",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // Ulangi node yang dihasilkan
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // Keluaran: Halo
            // Keluaran: Dunia!
        }
    }
}
```

Contoh ini menunjukkan penggunaan kueri XPath untuk menemukan elemen dalam dokumen HTML berdasarkan atribut dan strukturnya.

## Pemilih CSS

Pemilih CSS memberikan cara alternatif untuk memilih elemen dalam dokumen HTML, mirip dengan bagaimana stylesheet CSS menargetkan elemen.

```csharp
public static void CSSSelectorUsageExample()
{
    // Siapkan kode HTML
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello</span>
            </div>
        </div>
        <p class='happy'>
            <span>World!</span>
        </p>
    ";
    
    // Inisialisasi dokumen berdasarkan kode yang disiapkan
    using (var document = new HTMLDocument(code, "."))
    {
        //Gunakan pemilih CSS untuk mengekstrak elemen berdasarkan kelas dan hierarki
        var elements = document.QuerySelectorAll(".happy span");
        
        // Ulangi daftar elemen yang dihasilkan
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // Keluaran: Halo
            // Keluaran: Dunia!
        }
    }
}
```

Di sini, kami mendemonstrasikan cara menggunakan pemilih CSS untuk menargetkan elemen tertentu dalam dokumen HTML.

Dengan contoh ini, Anda telah memperoleh pemahaman dasar tentang cara menavigasi, memfilter, mengkueri, dan memilih elemen dalam dokumen HTML menggunakan Aspose.HTML untuk .NET.

## Kesimpulan

 Aspose.HTML untuk .NET adalah perpustakaan serbaguna yang memberdayakan pengembang .NET untuk bekerja secara efisien dengan dokumen HTML. Dengan fitur canggihnya untuk navigasi, pemfilteran, kueri, dan pemilihan elemen, Anda dapat menangani berbagai tugas pemrosesan HTML dengan lancar. Dengan mengikuti tutorial ini dan menjelajahi dokumentasi di[Aspose.HTML untuk Dokumentasi .NET](https://reference.aspose.com/html/net/), Anda dapat membuka potensi penuh alat ini untuk aplikasi .NET Anda.

## FAQ

### Q1. Apakah Aspose.HTML untuk .NET gratis untuk digunakan?

A1: Aspose.HTML untuk .NET menawarkan versi uji coba gratis, namun untuk penggunaan produksi, Anda harus membeli lisensi. Anda dapat menemukan detail dan opsi lisensi di[Pembelian Aspose.HTML](https://purchase.aspose.com/buy).

### Q2. Bagaimana saya bisa mendapatkan lisensi sementara Aspose.HTML untuk .NET?

 A2: Anda bisa mendapatkan lisensi sementara untuk tujuan pengujian dari[Lisensi Sementara Aspose.HTML](https://purchase.aspose.com/temporary-license/).

### Q3. Di mana saya dapat mencari bantuan atau dukungan untuk Aspose.HTML untuk .NET?

 A3: Jika Anda mengalami masalah atau memiliki pertanyaan, Anda dapat mengunjungi[Forum Aspose.HTML](https://forum.aspose.com/) untuk bantuan dan dukungan masyarakat.

### Q4. Apakah ada sumber daya tambahan untuk mempelajari Aspose.HTML untuk .NET?

 A4: Bersamaan dengan tutorial ini, Anda dapat menjelajahi lebih banyak tutorial dan dokumentasi di[Aspose.HTML untuk halaman dokumentasi .NET](https://reference.aspose.com/html/net/).

### Q5. Apakah Aspose.HTML untuk .NET kompatibel dengan versi .NET terbaru?

A5: Aspose.HTML untuk .NET diperbarui secara berkala untuk memastikan kompatibilitas dengan versi dan teknologi .NET terbaru.