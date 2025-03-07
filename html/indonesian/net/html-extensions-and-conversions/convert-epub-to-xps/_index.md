---
title: Konversi EPUB ke XPS dalam .NET dengan Aspose.HTML
linktitle: Konversi EPUB ke XPS dalam .NET
second_title: Aspose.HTML .NET API manipulasi HTML
description: Pelajari cara mengonversi EPUB ke XPS dalam format .NET menggunakan Aspose.HTML untuk .NET. Ikuti panduan langkah demi langkah kami untuk konversi yang mudah.
weight: 13
url: /id/net/html-extensions-and-conversions/convert-epub-to-xps/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konversi EPUB ke XPS dalam .NET dengan Aspose.HTML


Apakah Anda mencari cara mudah untuk mengonversi file EPUB ke format XPS di aplikasi .NET Anda? Aspose.HTML untuk .NET menyediakan solusi hebat untuk mencapainya dengan mudah. Dalam panduan langkah demi langkah ini, kami akan memandu Anda melalui proses mengonversi EPUB ke XPS menggunakan Aspose.HTML. Mari kita mulai!

## Prasyarat

Sebelum Anda memulai proses konversi EPUB ke XPS, Anda harus memastikan bahwa Anda memiliki prasyarat berikut:

### 1. Pustaka Aspose.HTML untuk .NET

 Pastikan Anda telah menginstal pustaka Aspose.HTML for .NET di proyek Anda. Jika Anda belum melakukannya, Anda dapat memperolehnya dari[Aspose.HTML untuk halaman unduhan .NET](https://releases.aspose.com/html/net/).

### 2. Masukkan berkas EPUB

Anda memerlukan file EPUB yang ingin dikonversi ke XPS. Pastikan Anda memiliki file EPUB yang tersedia untuk konversi.

### 3. Lingkungan Pengembangan .NET

Panduan ini mengasumsikan Anda telah memiliki lingkungan pengembangan .NET yang berfungsi pada komputer Anda.

## Impor Ruang Nama

Untuk memulai, Anda harus mengimpor namespace yang diperlukan untuk Aspose.HTML:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## Konversi EPUB ke XPS

Mari kita uraikan proses mengonversi berkas EPUB ke format XPS menjadi beberapa langkah.

### Langkah 1.1: Buka File EPUB

Pertama, buka file EPUB yang ada untuk dibaca menggunakan FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Lanjutkan proses konversi
}
```

### Langkah 1.2: Buat XpsSaveOptions

Buat contoh XpsSaveOptions. Langkah ini penting untuk mengonfigurasi keluaran XPS:

```csharp
var options = new XpsSaveOptions();
```

### Langkah 1.3: Konversi EPUB ke XPS

Sekarang, mari panggil metode ConvertEPUB untuk mengonversi EPUB ke XPS:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Tentukan Opsi XPS Kustom

Anda dapat menyesuaikan keluaran XPS lebih lanjut dengan menentukan opsi khusus seperti ukuran halaman dan warna latar belakang.

### Langkah 2.1: Ukuran Halaman Kustom dan Warna Latar Belakang

Buat contoh XpsSaveOptions dengan ukuran halaman dan warna latar belakang khusus:

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### Langkah 2.2: Konversi EPUB ke XPS dengan Opsi Kustom

Sekarang, panggil metode ConvertEPUB untuk mengonversi EPUB ke XPS dengan opsi khusus:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Gunakan Penyedia Aliran Kustom

Pada langkah ini, kami akan mengonversi EPUB ke XPS menggunakan penyedia aliran khusus, yang memungkinkan Anda memanipulasi data yang dihasilkan.

### Langkah 3.1: Buat MemoryStreamProvider

Buat contoh MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Lanjutkan proses konversi
}
```

### Langkah 3.2: Konversi EPUB ke XPS dengan Penyedia Streaming

Konversi EPUB ke XPS dengan menggunakan MemoryStreamProvider:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Langkah 3.3: Akses dan Simpan Hasil

Ambil aliran memori yang berisi data yang dikonversi dan simpan ke file keluaran:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Kode Sumber Kelas MemoryStreamProvider

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
                // Metode ini dipanggil saat diperlukan pembuatan beberapa aliran output. Misalnya saat merender HTML ke daftar file gambar (JPG, PNG, dll.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Di sini Anda dapat melepaskan aliran yang diisi dengan data dan, misalnya, membuangnya ke hard-drive
            }
            public void Dispose()
            {
                // Melepaskan sumber daya
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Selamat! Anda berhasil mengonversi file EPUB ke format XPS menggunakan Aspose.HTML untuk .NET.

## Kesimpulan

Dalam tutorial komprehensif ini, kami menjajaki cara memanfaatkan Aspose.HTML untuk .NET guna mengonversi file EPUB ke format XPS dengan berbagai opsi penyesuaian. Baik Anda pengembang berpengalaman atau baru memulai, Aspose.HTML menyederhanakan proses, sehingga Anda dapat menangani konversi EPUB ke XPS dengan mudah.

 Punya pertanyaan atau mengalami masalah? Lihat[Dokumentasi Aspose.HTML](https://reference.aspose.com/html/net/) untuk wawasan lebih lanjut atau mencari bantuan dari[Forum Komunitas Aspose.HTML](https://forum.aspose.com/).

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.HTML untuk .NET?
Aspose.HTML untuk .NET adalah pustaka hebat yang memungkinkan pengembang untuk bekerja dengan dokumen HTML, EPUB, dan XPS dalam aplikasi .NET.

### Di mana saya dapat mengunduh Aspose.HTML untuk .NET?
 Anda dapat mengunduh Aspose.HTML untuk .NET dari[halaman unduhan](https://releases.aspose.com/html/net/).

### Apakah ada uji coba gratis yang tersedia untuk Aspose.HTML untuk .NET?
 Ya, Anda bisa mendapatkan uji coba gratis dari[Di Sini](https://releases.aspose.com/).

### Bagaimana cara memperoleh lisensi sementara untuk Aspose.HTML untuk .NET?
 Untuk mendapatkan lisensi sementara, kunjungi[halaman lisensi sementara](https://purchase.aspose.com/temporary-license/).

### Di mana saya dapat menemukan lebih banyak tutorial dan dokumentasi untuk Aspose.HTML for .NET?
 Jelajahi berbagai tutorial dan dokumentasi terperinci tentang[Dokumentasi Aspose.HTML](https://reference.aspose.com/html/net/) halaman.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
