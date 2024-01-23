---
title: Hasilkan PDF Terenkripsi oleh PdfDevice di .NET dengan Aspose.HTML
linktitle: Hasilkan PDF Terenkripsi dengan PdfDevice di .NET
second_title: Aspose.HTML .NET API manipulasi HTML
description: Konversi HTML ke PDF secara dinamis dengan Aspose.HTML untuk .NET. Integrasi yang mudah, opsi yang dapat disesuaikan, dan kinerja yang tangguh.
type: docs
weight: 15
url: /id/net/advanced-features/generate-encrypted-pdf-by-pdfdevice/
---

Dalam dunia pengembangan web yang serba cepat, kebutuhan untuk mengkonversi HTML ke PDF secara dinamis telah menjadi kebutuhan umum. Baik Anda ingin membuat laporan, faktur, atau sekadar mengarsipkan konten web, Aspose.HTML untuk .NET adalah alat canggih yang dapat menyederhanakan proses ini. Dalam tutorial ini, kami akan memandu Anda melalui langkah-langkah untuk mencapai konversi HTML ke PDF dinamis menggunakan Aspose.HTML untuk .NET.

## Prasyarat

Sebelum kita mendalami kodenya, pastikan Anda memiliki semua yang Anda perlukan:

### 1. Instalasi

 Pertama, Anda perlu mengunduh dan menginstal Aspose.HTML untuk .NET. Anda dapat menemukan tautan unduhan[Di Sini](https://releases.aspose.com/html/net/).

### 2. Impor Namespace

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

Sekarang, mari kita bagi contoh kode yang Anda berikan menjadi beberapa langkah dan jelaskan setiap langkahnya.

## Perincian

### Langkah 1: Inisialisasi Dokumen HTML

```csharp
using (var document = new Aspose.Html.HTMLDocument("<style>p { color: green; }</style><p>my first paragraph</p>", @"c:\work\"))
```

 Pada langkah ini, kita membuat sebuah instance dari`HTMLDocument`kelas, yang mewakili konten HTML yang ingin Anda konversi. Anda dapat meneruskan konten HTML Anda sebagai string. Pastikan Anda menentukan jalur yang benar untuk direktori kerja Anda.

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

 Pada langkah ini, kita membuat sebuah instance dari`PdfRenderingOptions`. Ini memungkinkan Anda mengonfigurasi berbagai pengaturan untuk konversi PDF. Dalam contoh ini, kami mengatur ukuran halaman dan margin serta menentukan pengaturan enkripsi untuk output PDF.

### Langkah 3: Render HTML ke PDF

```csharp
using (PdfDevice device = new PdfDevice(options, dataDir + @"document_out.pdf"))
{
    document.RenderTo(device);
}
```

 Pada langkah terakhir ini, kami menggunakan`RenderTo` metode untuk mengkonversi dokumen HTML ke PDF. Kami melewati`PdfDevice` contoh dan jalur file keluaran yang diinginkan. Konten HTML akan diubah menjadi dokumen PDF dengan pengaturan yang ditentukan.

Selamat! Anda telah berhasil mengonversi HTML ke PDF secara dinamis menggunakan Aspose.HTML untuk .NET. Anda sekarang dapat mengintegrasikan kode ini ke dalam aplikasi web atau proyek Anda sesuai kebutuhan.

## Kesimpulan

Aspose.HTML untuk .NET menyederhanakan proses konversi HTML ke PDF secara dinamis, menjadikannya alat yang berharga bagi pengembang web. Dengan mengikuti langkah-langkah yang diuraikan dalam tutorial ini, Anda dapat dengan mudah membuat dokumen PDF dari konten HTML sambil menyesuaikan hasilnya untuk memenuhi kebutuhan spesifik Anda.

## FAQ

### Q1. Apakah Aspose.HTML untuk .NET kompatibel dengan versi HTML yang berbeda?

A1: Ya, Aspose.HTML untuk .NET dirancang untuk menangani berbagai versi HTML, memastikan kompatibilitas dengan berbagai konten web.

### Q2. Bisakah saya menyesuaikan keluaran PDF lebih lanjut?

A2: Tentu saja! Anda dapat menyesuaikan opsi rendering untuk menyesuaikan ukuran halaman, margin, enkripsi, dan pengaturan khusus PDF lainnya agar sesuai dengan kebutuhan Anda.

### Q3. Apakah Aspose.HTML untuk .NET mendukung format keluaran lainnya?

A3: Ya, selain PDF, Aspose.HTML untuk .NET mendukung berbagai format output lainnya, termasuk format gambar seperti PNG dan JPEG.

### Q4. Apakah ada uji coba gratis yang tersedia?

A4: Ya, Anda dapat menjelajahi Aspose.HTML untuk .NET dengan uji coba gratis. Memulai[Di Sini](https://releases.aspose.com/).

### Q5. Di mana saya bisa mendapatkan bantuan dan dukungan?

 A5: Untuk pertanyaan atau masalah apa pun, Anda dapat mengunjungi forum Aspose untuk mendapatkan dukungan dan diskusi:[Mendukung](https://forum.aspose.com/).