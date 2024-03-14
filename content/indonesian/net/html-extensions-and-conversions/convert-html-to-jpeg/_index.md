---
title: Konversi HTML ke JPEG di .NET dengan Aspose.HTML
linktitle: Konversi HTML ke JPEG di .NET
second_title: Aspose.HTML .NET API manipulasi HTML
description: Pelajari cara mengonversi HTML ke JPEG di .NET dengan Aspose.HTML untuk .NET. Panduan langkah demi langkah untuk memanfaatkan kekuatan Aspose.HTML untuk .NET.
type: docs
weight: 17
url: /id/net/html-extensions-and-conversions/convert-html-to-jpeg/
---

Dalam dunia pengembangan web, Aspose.HTML untuk .NET adalah alat canggih dan serbaguna yang memungkinkan pengembang memanipulasi dokumen HTML dengan mudah. Panduan komprehensif ini akan membawa Anda melalui proses mengimpor namespace dan memecah contoh menjadi beberapa langkah menggunakan Aspose.HTML untuk .NET. Baik Anda seorang pengembang berpengalaman atau pemula, tutorial ini akan membantu Anda memanfaatkan potensi perpustakaan ini.

## Perkenalan

Aspose.HTML untuk .NET adalah perpustakaan kaya fitur yang memungkinkan pengembang bekerja dengan dokumen HTML dengan lancar. Dengan perpustakaan ini, Anda dapat melakukan berbagai operasi pada file HTML, termasuk konversi ke format berbeda, manipulasi elemen dokumen, dan banyak lagi. Dalam panduan langkah demi langkah ini, kita akan mempelajari proses mengonversi HTML ke JPEG di lingkungan .NET. Mari kita mulai!

## Prasyarat

Sebelum masuk ke tutorial, ada beberapa prasyarat yang perlu Anda pastikan:

### 1. Visual Studio Terpasang
 Pastikan Anda telah menginstal Visual Studio di sistem Anda. Anda dapat mengunduhnya[Di Sini](https://visualstudio.microsoft.com/downloads/).

### 2. Aspose.HTML untuk Perpustakaan .NET
 Anda harus memiliki perpustakaan Aspose.HTML untuk .NET. Kamu bisa mendapatkannya[Di Sini](https://releases.aspose.com/html/net/).

### 3. .NET Kerangka
Pastikan Anda telah menginstal .NET Framework. Aspose.HTML untuk .NET memerlukan .NET Framework 2.0 atau lebih tinggi.

### 4. Pemahaman Dasar C#
Keakraban dengan bahasa pemrograman C# akan bermanfaat karena kita akan menulis kode dalam C#.

Sekarang setelah Anda memiliki prasyaratnya, mari mulai bekerja dengan Aspose.HTML untuk .NET.

## Impor Ruang Nama

Untuk mulai menggunakan Aspose.HTML untuk .NET, Anda perlu mengimpor namespace yang diperlukan. Ikuti langkah ini:

### Buka Proyek Visual Studio Anda

Luncurkan Visual Studio dan buka proyek Anda yang sudah ada atau buat yang baru.

### Tambahkan Referensi ke Aspose.HTML untuk .NET

Untuk menyertakan Aspose.HTML untuk .NET dalam proyek Anda, klik kanan pada "Referensi" di penjelajah solusi Anda, dan pilih "Tambahkan Referensi."

### Telusuri Aspose.HTML.dll

Klik "Jelajahi" dan arahkan ke lokasi tempat Anda menyimpan file Aspose.HTML.dll. Setelah memilihnya, klik "OK."

### Impor Namespace

Dalam file kode Anda, impor namespace yang diperlukan dengan menyertakan kode berikut di bagian atas:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;
```

Sekarang Anda siap bekerja dengan Aspose.HTML untuk .NET.

## Konversi HTML ke JPEG di .NET dengan Aspose.HTML

Selanjutnya, mari kita lihat proses mengonversi dokumen HTML menjadi gambar JPEG menggunakan Aspose.HTML untuk .NET.

### Inisialisasi Jalur dan Muat Dokumen HTML

Pada langkah ini, Anda akan menyiapkan jalur dan memuat dokumen HTML.

```csharp
// Jalur ke direktori dokumen
string dataDir = "Your Data Directory";

// Dokumen HTML sumber
HTMLDocument htmlDocument = new HTMLDocument(dataDir + "input.html");
```

Pastikan untuk mengganti "Direktori Data Anda" dengan jalur sebenarnya ke file HTML Anda.

### Inisialisasi ImageSaveOptions

Buat ImageSaveOptions untuk menentukan format keluaran, dalam hal ini, JPEG.

```csharp
// Inisialisasi ImageSaveOptions
ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Jpeg);
```

### Atur Jalur File Keluaran

Tentukan jalur untuk file JPEG keluaran.

```csharp
// Jalur file keluaran
string outputFile = dataDir + "HTMLtoJPEG_Output.jpeg";
```

### Konversi HTML ke JPEG

Sekarang saatnya mengubah dokumen HTML menjadi gambar JPEG.

```csharp
// Konversi HTML ke JPEG
Converter.ConvertHTML(htmlDocument, options, outputFile);
```

Dan itu saja! Anda telah berhasil mengonversi dokumen HTML menjadi gambar JPEG menggunakan Aspose.HTML untuk .NET.

## Kesimpulan

Aspose.HTML untuk .NET adalah alat yang berharga bagi pengembang, membuat manipulasi HTML dan tugas konversi menjadi lebih mudah. Dalam panduan ini, kami mempelajari proses mengimpor namespace dan mengonversi HTML ke JPEG di lingkungan .NET. Dengan Aspose.HTML untuk .NET, Anda memiliki kekuatan untuk menangani berbagai tugas terkait HTML dengan mudah.

 Jika Anda mengalami masalah atau memiliki pertanyaan, jangan ragu untuk mencari dukungan dari komunitas Aspose[Di Sini](https://forum.aspose.com/).

## FAQ

### Apakah Aspose.HTML untuk .NET gratis?
    Aspose.HTML untuk .NET adalah perpustakaan berbayar, tetapi Anda dapat menjelajahinya dengan uji coba gratis. Untuk membeli lisensi, kunjungi[Di Sini](https://purchase.aspose.com/buy).

### Bisakah saya menggunakan Aspose.HTML untuk .NET dengan .NET Core?
   Ya, Aspose.HTML untuk .NET kompatibel dengan .NET Core, sehingga Anda dapat menggunakannya dalam proyek .NET Core Anda.

### Format lain apa yang dapat saya ubah menjadi HTML dengan Aspose.HTML untuk .NET?
   Aspose.HTML untuk .NET mendukung berbagai format keluaran, termasuk PDF, PNG, dan XPS, selain JPEG.

### Apakah ada batasan pada versi uji coba gratis?
   Versi uji coba gratis memiliki beberapa keterbatasan, seperti memberi watermark pada dokumen keluaran. Untuk menghilangkan batasan ini, Anda perlu membeli lisensi.

### Apakah Aspose.HTML untuk .NET cocok untuk web scraping?
   Meskipun Aspose.HTML untuk .NET terutama untuk manipulasi dokumen, Aspose.HTML untuk .NET dapat digunakan untuk pengikisan web dengan mengekstraksi data dari dokumen HTML.