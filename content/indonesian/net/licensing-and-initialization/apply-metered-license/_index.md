---
title: Terapkan Lisensi Terukur di .NET dengan Aspose.HTML
linktitle: Terapkan Lisensi Terukur di .NET
second_title: Aspose.HTML .NET API manipulasi HTML
description: Pelajari cara menerapkan lisensi terukur di Aspose.HTML untuk .NET. Kelola kebutuhan manipulasi HTML Anda secara efisien. Mulai sekarang!
type: docs
weight: 10
url: /id/net/licensing-and-initialization/apply-metered-license/
---
Dalam tutorial ini, kami akan memandu Anda melalui proses penerapan lisensi terukur di aplikasi .NET Anda menggunakan Aspose.HTML. Lisensi terukur adalah cara mudah untuk mengelola lisensi untuk kebutuhan manipulasi HTML Anda. Dengan mengikuti langkah-langkah di bawah ini, Anda akan dapat menerapkan lisensi terukur ke proyek Aspose.HTML untuk .NET Anda.

## Prasyarat

Sebelum melanjutkan, pastikan Anda memiliki prasyarat berikut:

-  Lisensi Aspose.HTML untuk .NET yang valid. Anda bisa mendapatkannya dari[Asumsikan Pembelian](https://purchase.aspose.com/buy).
-  Pustaka Aspose.HTML untuk .NET, tempat Anda dapat mengunduh[Di Sini](https://releases.aspose.com/html/net/).
- Jalur direktori data tempat Anda menyimpan file HTML masukan Anda.

Sekarang, mari kita uraikan kode contoh dan jelaskan setiap langkah secara detail:

## Impor Namespace

Dalam proyek .NET Anda, Anda perlu menyertakan namespace yang diperlukan. Tambahkan pernyataan penggunaan berikut di bagian atas file C# Anda:

```csharp
using Aspose.Html;
```

## Panduan Langkah demi Langkah

Di sini, kami akan memecah kode contoh menjadi beberapa langkah dan menjelaskan setiap langkah secara detail.

### Tetapkan Jalur Direktori Data:

   Pertama, Anda harus mengatur jalur ke direktori data tempat file HTML masukan Anda berada. Anda harus menggantinya`"Your Data Directory"` dengan jalur sebenarnya.

   ```csharp
   string dataDir = "Your Data Directory";
   ```

### Tetapkan Kunci Publik dan Pribadi Terukur:

    Untuk menerapkan lisensi terukur, Anda perlu memberikan kunci publik dan pribadi Anda. Anda bisa mendapatkan kunci ini saat membeli lisensi terukur dari Aspose. Mengganti`"*****"` dengan kunci publik dan pribadi Anda yang sebenarnya.

   ```csharp
   Aspose.Html.Metered metered = new Aspose.Html.Metered();
   metered.SetMeteredKey("YOUR_PUBLIC_KEY", "YOUR_PRIVATE_KEY");
   ```

### Muat Dokumen HTML:

    Muat dokumen HTML dari direktori data Anda menggunakan kelas HTMLDocument. Pastikan untuk mengganti`"input.html"` dengan nama file sebenarnya.

   ```csharp
   HTMLDocument document = new HTMLDocument(dataDir + "input.html");
   ```

### Cetak HTML Dalam:

   Setelah memuat dokumen HTML, Anda dapat mengakses dan mencetak HTML bagian dalam file tersebut ke konsol untuk verifikasi.

   ```csharp
   Console.WriteLine(document.Body.InnerHTML);
   ```

Itu dia! Anda telah berhasil menerapkan lisensi terukur ke proyek .NET dan memuat dokumen HTML.

## Kesimpulan

Dalam tutorial ini, kami telah menunjukkan cara menerapkan lisensi terukur menggunakan Aspose.HTML untuk .NET. Dengan mengikuti langkah-langkah ini, Anda dapat mengintegrasikan Aspose.HTML dengan lancar ke dalam aplikasi .NET Anda untuk manipulasi HTML.

---

## Pertanyaan yang Sering Diajukan (FAQ)

### Apa yang dimaksud dengan lisensi terukur di Aspose.HTML untuk .NET?
Lisensi terukur memungkinkan Anda membayar Aspose.HTML dengan sistem bayar sesuai penggunaan, bergantung pada penggunaan Anda. Ini adalah opsi lisensi yang fleksibel.

### Di mana saya bisa mendapatkan lisensi terukur untuk Aspose.HTML untuk .NET?
 Anda dapat membeli lisensi terukur dari[Asumsikan Pembelian](https://purchase.aspose.com/buy).

### Bagaimana cara mengunduh perpustakaan Aspose.HTML untuk .NET?
 Anda dapat mengunduh perpustakaan dari[Di Sini](https://releases.aspose.com/html/net/).

### Apakah ada opsi uji coba gratis yang tersedia untuk Aspose.HTML untuk .NET?
 Ya, Anda dapat mengakses uji coba gratis dari[Di Sini](https://releases.aspose.com/).

### Di mana saya bisa mendapatkan dukungan atau mengajukan pertanyaan tentang Aspose.HTML untuk .NET?
 Anda dapat bergabung dengan komunitas dan mencari dukungan di[Asumsikan Forum](https://forum.aspose.com/).