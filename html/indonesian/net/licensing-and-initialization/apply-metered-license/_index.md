---
title: Terapkan Lisensi Terukur di .NET dengan Aspose.HTML
linktitle: Terapkan Lisensi Terukur di .NET
second_title: Aspose.HTML .NET API manipulasi HTML
description: Pelajari cara menerapkan lisensi terukur di Aspose.HTML untuk .NET. Kelola kebutuhan manipulasi HTML Anda secara efisien. Mulailah sekarang!
weight: 10
url: /id/net/licensing-and-initialization/apply-metered-license/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Terapkan Lisensi Terukur di .NET dengan Aspose.HTML

Dalam tutorial ini, kami akan memandu Anda melalui proses penerapan lisensi terukur dalam aplikasi .NET Anda menggunakan Aspose.HTML. Lisensi terukur adalah cara mudah untuk mengelola lisensi untuk kebutuhan manipulasi HTML Anda. Dengan mengikuti langkah-langkah di bawah ini, Anda akan dapat menerapkan lisensi terukur ke proyek Aspose.HTML for .NET Anda.

## Prasyarat

Sebelum melanjutkan, pastikan Anda memiliki prasyarat berikut:

-  Lisensi Aspose.HTML yang valid untuk .NET. Anda dapat memperolehnya dari[Aspose Pembelian](https://purchase.aspose.com/buy).
-  Pustaka Aspose.HTML untuk .NET, yang dapat Anda unduh dari[Di Sini](https://releases.aspose.com/html/net/).
- Jalur direktori data tempat Anda menyimpan berkas HTML masukan.

Sekarang, mari kita uraikan kode contoh dan jelaskan setiap langkah secara terperinci:

## Mengimpor Ruang Nama

Dalam proyek .NET Anda, Anda perlu menyertakan namespace yang diperlukan. Tambahkan pernyataan using berikut di bagian atas file C# Anda:

```csharp
using Aspose.Html;
```

## Panduan Langkah demi Langkah

Di sini, kami akan membagi kode contoh menjadi beberapa langkah dan menjelaskan setiap langkah secara rinci.

### Tetapkan Jalur Direktori Data:

   Pertama, Anda harus mengatur jalur ke direktori data tempat file HTML input Anda berada. Anda perlu mengganti`"Your Data Directory"` dengan jalur sebenarnya.

   ```csharp
   string dataDir = "Your Data Directory";
   ```

### Tetapkan Kunci Publik dan Pribadi yang Terukur:

    Untuk menerapkan lisensi terukur, Anda perlu memberikan kunci publik dan pribadi Anda. Anda dapat memperoleh kunci ini saat membeli lisensi terukur dari Aspose. Ganti`"*****"` dengan kunci publik dan pribadi Anda yang sebenarnya.

   ```csharp
   Aspose.Html.Metered metered = new Aspose.Html.Metered();
   metered.SetMeteredKey("YOUR_PUBLIC_KEY", "YOUR_PRIVATE_KEY");
   ```

### Muat Dokumen HTML:

    Muat dokumen HTML dari direktori data Anda menggunakan kelas HTMLDocument. Pastikan untuk mengganti`"input.html"` dengan nama berkas sebenarnya.

   ```csharp
   HTMLDocument document = new HTMLDocument(dataDir + "input.html");
   ```

### Cetak HTML Dalam:

   Setelah memuat dokumen HTML, Anda dapat mengakses dan mencetak HTML bagian dalam file ke konsol untuk verifikasi.

   ```csharp
   Console.WriteLine(document.Body.InnerHTML);
   ```

Selesai! Anda telah berhasil menerapkan lisensi terukur ke proyek .NET Anda dan memuat dokumen HTML.

## Kesimpulan

Dalam tutorial ini, kami telah menunjukkan cara menerapkan lisensi terukur menggunakan Aspose.HTML untuk .NET. Dengan mengikuti langkah-langkah ini, Anda dapat mengintegrasikan Aspose.HTML dengan lancar ke dalam aplikasi .NET Anda untuk manipulasi HTML.

---

## Pertanyaan yang Sering Diajukan (FAQ)

### Apa itu lisensi terukur dalam Aspose.HTML untuk .NET?
Lisensi berbayar memungkinkan Anda membayar Aspose.HTML berdasarkan pemakaian, tergantung pada penggunaan Anda. Ini adalah opsi lisensi yang fleksibel.

### Di mana saya bisa mendapatkan lisensi terukur untuk Aspose.HTML for .NET?
 Anda dapat membeli lisensi terukur dari[Aspose Pembelian](https://purchase.aspose.com/buy).

### Bagaimana cara mengunduh pustaka Aspose.HTML untuk .NET?
 Anda dapat mengunduh perpustakaan dari[Di Sini](https://releases.aspose.com/html/net/).

### Apakah ada pilihan uji coba gratis yang tersedia untuk Aspose.HTML for .NET?
 Ya, Anda dapat mengakses uji coba gratis dari[Di Sini](https://releases.aspose.com/).

### Di mana saya bisa mendapatkan dukungan atau mengajukan pertanyaan tentang Aspose.HTML untuk .NET?
 Anda dapat bergabung dengan komunitas dan mencari dukungan di[Forum Aspose](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
