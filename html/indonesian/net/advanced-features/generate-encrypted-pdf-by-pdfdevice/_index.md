---
title: Hasilkan PDF Terenkripsi oleh PdfDevice dalam .NET dengan Aspose.HTML
linktitle: Hasilkan PDF Terenkripsi oleh PdfDevice dalam .NET
second_title: Aspose.HTML .NET API manipulasi HTML
description: Konversi HTML ke PDF secara dinamis dengan Aspose.HTML untuk .NET. Integrasi yang mudah, opsi yang dapat disesuaikan, dan kinerja yang tangguh.
weight: 15
url: /id/net/advanced-features/generate-encrypted-pdf-by-pdfdevice/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hasilkan PDF Terenkripsi oleh PdfDevice dalam .NET dengan Aspose.HTML


Dalam dunia pengembangan web yang serba cepat, kebutuhan untuk mengonversi HTML ke PDF secara dinamis telah menjadi persyaratan umum. Apakah Anda ingin membuat laporan, faktur, atau sekadar mengarsipkan konten web, Aspose.HTML untuk .NET adalah alat canggih yang dapat menyederhanakan proses ini. Dalam tutorial ini, kami akan memandu Anda melalui langkah-langkah untuk mencapai konversi HTML dinamis ke PDF menggunakan Aspose.HTML untuk .NET.

## Prasyarat

Sebelum kita masuk ke kode, mari pastikan Anda memiliki semua yang Anda butuhkan:

### 1. Instalasi

 Pertama, Anda perlu mengunduh dan menginstal Aspose.HTML untuk .NET. Anda dapat menemukan tautan unduhannya[Di Sini](https://releases.aspose.com/html/net/).

### 2. Impor Ruang Nama

Untuk memulai, sertakan namespace yang diperlukan di awal kode Anda. Namespace ini penting untuk mengakses fungsionalitas Aspose.HTML untuk .NET.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Pdf.Paging;
using Aspose.Html.Saving;
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using System;
using System.Drawing;
```

Sekarang, mari kita uraikan contoh kode yang Anda berikan menjadi beberapa langkah dan jelaskan setiap langkahnya.

## Perincian

### Langkah 1: Inisialisasi Dokumen HTML

```csharp
using (var document = new Aspose.Html.HTMLDocument("<style>p { color: green; }</style><p>my first paragraph</p>", @"c:\work\"))
```

 Pada langkah ini, kita membuat sebuah instance dari`HTMLDocument` class, yang mewakili konten HTML yang ingin Anda konversi. Anda dapat meneruskan konten HTML sebagai string. Pastikan Anda menentukan jalur yang benar untuk direktori kerja Anda.

### Langkah 2: Konfigurasikan Opsi Rendering PDF

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(new Size(500, 500), new Margin(50, 50, 50, 50))
    },
    Encryption = new PdfEncryptionInfo("user", "p@wd", PdfPermissions.PrintDocument, PdfEncryptionAlgorithm.RC4_128)
};
```

 Pada langkah ini, kita membuat sebuah instance dari`PdfRenderingOptions`. Ini memungkinkan Anda mengonfigurasi berbagai pengaturan untuk konversi PDF. Dalam contoh ini, kami mengatur ukuran halaman dan margin serta menentukan pengaturan enkripsi untuk PDF keluaran.

### Langkah 3: Render HTML ke PDF

```csharp
using (PdfDevice device = new PdfDevice(options, dataDir + @"document_out.pdf"))
{
    document.RenderTo(device);
}
```

 Pada langkah terakhir ini, kami menggunakan`RenderTo` metode untuk mengubah dokumen HTML menjadi PDF. Kami meneruskan`PdfDevice` contoh dan jalur file keluaran yang diinginkan. Konten HTML akan diubah menjadi dokumen PDF dengan pengaturan yang ditentukan.

Selamat! Anda telah berhasil mengonversi HTML ke PDF secara dinamis menggunakan Aspose.HTML untuk .NET. Kini Anda dapat mengintegrasikan kode ini ke aplikasi web atau proyek sesuai kebutuhan.

## Kesimpulan

Aspose.HTML untuk .NET menyederhanakan proses konversi HTML ke PDF secara dinamis, menjadikannya alat yang berharga bagi pengembang web. Dengan mengikuti langkah-langkah yang diuraikan dalam tutorial ini, Anda dapat dengan mudah membuat dokumen PDF dari konten HTML sambil menyesuaikan output untuk memenuhi persyaratan khusus Anda.

## Pertanyaan yang Sering Diajukan

### Q1. Apakah Aspose.HTML untuk .NET kompatibel dengan versi HTML yang berbeda?

A1: Ya, Aspose.HTML untuk .NET dirancang untuk menangani berbagai versi HTML, memastikan kompatibilitas dengan berbagai konten web.

### Q2. Bisakah saya menyesuaikan hasil keluaran PDF lebih lanjut?

A2: Tentu saja! Anda dapat menyesuaikan opsi rendering untuk menyesuaikan ukuran halaman, margin, enkripsi, dan pengaturan khusus PDF lainnya sesuai kebutuhan Anda.

### Q3. Apakah Aspose.HTML untuk .NET mendukung format output lain?

A3: Ya, selain PDF, Aspose.HTML untuk .NET mendukung berbagai format keluaran lainnya, termasuk format gambar seperti PNG dan JPEG.

### Q4. Apakah ada uji coba gratis yang tersedia?

A4: Ya, Anda dapat menjelajahi Aspose.HTML untuk .NET dengan uji coba gratis. Mari mulai[Di Sini](https://releases.aspose.com/).

### Q5. Di mana saya bisa mendapatkan bantuan dan dukungan?

 A5: Untuk pertanyaan atau masalah apa pun, Anda dapat mengunjungi forum Aspose untuk dukungan dan diskusi:[Mendukung](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
