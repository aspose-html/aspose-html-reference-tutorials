---
title: Konversi EPUB ke PDF di .NET dengan Aspose.HTML
linktitle: Konversi EPUB ke PDF di .NET
second_title: Aspose.HTML .NET API manipulasi HTML
description: Pelajari cara mengonversi EPUB ke PDF menggunakan Aspose.HTML untuk .NET. Panduan langkah demi langkah ini mencakup opsi penyesuaian, FAQ, dan lainnya untuk konversi dokumen yang lancar.
type: docs
weight: 12
url: /id/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

Dalam tutorial ini, kita akan mempelajari cara menggunakan Aspose.HTML untuk .NET untuk mengonversi file EPUB ke PDF. Aspose.HTML adalah perpustakaan .NET yang kuat yang menyediakan berbagai fungsi untuk bekerja dengan dokumen HTML dan EPUB. Kami akan membahas prasyarat, mengimpor namespace yang diperlukan, dan menguraikan beberapa contoh, menjelaskan setiap langkah secara detail.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki prasyarat berikut:

1. Aspose.HTML untuk .NET: Pastikan Anda telah menginstal Aspose.HTML untuk .NET di proyek .NET Anda. Anda dapat mengunduhnya dari[Di Sini](https://releases.aspose.com/html/net/).

2. Direktori Data Anda: Anda memerlukan direktori data tempat file EPUB Anda disimpan.

Sekarang, mari selami proses langkah demi langkah mengonversi EPUB ke PDF menggunakan Aspose.HTML untuk .NET.

## Konversi EPUB ke PDF

### Langkah 1: Inisialisasi Proyek Anda

Pastikan Anda telah menyiapkan proyek .NET, dan Aspose.HTML untuk .NET telah diinstal.

### Langkah 2: Impor Namespace yang Diperlukan

Dalam file kode C# Anda, impor namespace yang diperlukan:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### Langkah 3: Buka File EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Lanjutkan ke langkah berikutnya...
}
```

-  Mengganti`"Your Data Directory"` dengan direktori sebenarnya tempat file EPUB Anda berada.
- Kode ini membuka file EPUB untuk dibaca.

### Langkah 4: Tetapkan Opsi PDF dan Lakukan Konversi

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Buat sebuah contoh dari`PdfSaveOptions` untuk menentukan pengaturan konversi PDF.
-  Menggunakan`Converter.ConvertEPUB` metode untuk mengonversi EPUB ke PDF dengan opsi yang diberikan.
- Simpan PDF yang dihasilkan sebagai "output.pdf".

## Tentukan Opsi Penyimpanan PDF

### Langkah 1: Inisialisasi Proyek Anda

Pastikan Anda telah menyiapkan proyek .NET dan Aspose.HTML untuk .NET diinstal.

### Langkah 2: Impor Namespace yang Diperlukan

Impor namespace yang diperlukan dalam kode C# Anda:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### Langkah 3: Buka File EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Lanjutkan ke langkah berikutnya...
}
```

-  Mengganti`"Your Data Directory"` dengan direktori sebenarnya dari file EPUB Anda.
- Buka file EPUB untuk dibaca.

### Langkah 4: Sesuaikan Opsi PDF

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  Buat sebuah contoh dari`PdfSaveOptions` dan sesuaikan sesuai kebutuhan Anda.
- Dalam contoh ini, kami mengatur ukuran halaman menjadi lebar 3000 piksel dan tinggi 1000 piksel, dan warna latar belakang menjadi Alice Blue.

### Langkah 5: Lakukan Konversi

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Menggunakan`Converter.ConvertEPUB` metode untuk mengonversi EPUB ke PDF dengan opsi khusus.
- Simpan PDF yang dihasilkan sebagai "output.pdf".

## Gunakan Penyedia Aliran Khusus

### Langkah 1: Inisialisasi Proyek Anda

Siapkan proyek .NET dan instal Aspose.HTML untuk .NET.

### Langkah 2: Impor Namespace yang Diperlukan

Dalam kode C# Anda, impor namespace yang diperlukan:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### Langkah 3: Buka File EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Lanjutkan ke langkah berikutnya...
}
```

-  Mengganti`"Your Data Directory"` dengan direktori sebenarnya dari file EPUB Anda.
- Buka file EPUB untuk dibaca.

### Langkah 4: Gunakan Penyedia Aliran Khusus

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // Lanjutkan ke langkah berikutnya...
}
```

-  Membuat`MemoryStreamProvider` untuk mengelola hasil konversi sebagai aliran memori.
-  Menggunakan`Converter.ConvertEPUB` metode dengan penyedia aliran khusus.

### Langkah 5: Simpan Hasilnya

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- Akses aliran memori yang berisi data yang dikonversi.
- Atur posisi streaming ke awal.
- Buat file PDF keluaran dan salin konten dari aliran memori ke dalamnya.

### Kode sumber Kelas MemoryStreamProvider. 

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Daftar objek MemoryStream yang dibuat selama rendering dokumen
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Metode ini dipanggil ketika hanya satu aliran keluaran yang diperlukan, misalnya untuk format XPS, PDF, atau TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Metode ini dipanggil ketika pembuatan beberapa aliran keluaran diperlukan. Misalnya selama rendering HTML ke daftar file gambar (JPG, PNG, dll.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Di sini Anda dapat melepaskan aliran yang berisi data dan, misalnya, mengalirkannya ke hard-drive
            }
            public void Dispose()
            {
                // Melepaskan sumber daya
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Sekarang, Anda telah mempelajari cara mengonversi file EPUB ke PDF menggunakan Aspose.HTML untuk .NET dengan berbagai opsi dan kemungkinan penyesuaian. Aspose.HTML menyederhanakan proses, memberikan fleksibilitas dan kontrol atas konversi dokumen Anda.

## Kesimpulan

Aspose.HTML untuk .NET adalah alat serbaguna untuk mengonversi file EPUB ke PDF, menawarkan opsi penyesuaian untuk menyesuaikan dokumen PDF yang dihasilkan dengan kebutuhan Anda. Apakah Anda memerlukan konversi sederhana atau penyesuaian tingkat lanjut, Aspose.HTML siap membantu Anda.

 Jika Anda belum melakukannya, Anda dapat mengunduh Aspose.HTML untuk .NET dari[situs web](https://releases.aspose.com/html/net/) dan mulai menggunakannya di aplikasi .NET Anda hari ini.

---

## FAQ

### Apakah Aspose.HTML untuk .NET gratis untuk digunakan?
    Aspose.HTML untuk .NET adalah produk komersial, tetapi tersedia uji coba gratis[Di Sini](https://releases.aspose.com/).

### Bisakah saya menyesuaikan tampilan PDF yang dikonversi?
   Ya, Anda dapat menyesuaikan tampilan PDF dengan menyesuaikan opsi seperti ukuran halaman dan warna latar belakang, seperti yang ditunjukkan pada Contoh 2.

### Bagaimana saya bisa mendapatkan dukungan untuk Aspose.HTML untuk .NET?
    Anda dapat menemukan dukungan dan sumber daya di[Forum Aspose.HTML](https://forum.aspose.com/).

### Apakah ada format lain yang dapat saya konversi dengan Aspose.HTML untuk .NET?
   Ya, Aspose.HTML untuk .NET mendukung berbagai format dokumen, termasuk HTML, EPUB, dan lainnya.

### Apakah Aspose.HTML untuk ..NET cocok untuk konversi dokumen skala besar?
   Aspose.HTML untuk .NET dirancang untuk menangani konversi dokumen skala besar secara efisien, sehingga cocok untuk berbagai aplikasi.

