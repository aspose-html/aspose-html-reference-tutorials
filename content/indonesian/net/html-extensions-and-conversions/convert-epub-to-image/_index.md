---
title: Konversikan EPUB ke Gambar di .NET dengan Aspose.HTML
linktitle: Konversikan EPUB ke Gambar di .NET
second_title: Aspose.HTML .NET API manipulasi HTML
description: Pelajari cara mengonversi EPUB menjadi gambar menggunakan Aspose.HTML untuk .NET. Tutorial langkah demi langkah dengan contoh kode dan opsi yang dapat disesuaikan.
type: docs
weight: 11
url: /id/net/html-extensions-and-conversions/convert-epub-to-image/
---

Di era digital saat ini, kemampuan memanipulasi dan mengubah berbagai format dokumen merupakan keterampilan yang berharga. Aspose.HTML untuk .NET adalah alat canggih yang memungkinkan pengembang bekerja dengan dokumen HTML dan EPUB dengan mudah. Dalam tutorial ini, kami akan mempelajari dunia Aspose.HTML untuk .NET dan memandu Anda melalui proses konversi dokumen EPUB ke berbagai format gambar. Kami akan membagi setiap contoh menjadi beberapa langkah, menjelaskan setiap langkahnya.

## Prasyarat

Sebelum kita mendalami dunia Aspose.HTML untuk .NET, Anda harus memastikan bahwa Anda memiliki prasyarat berikut:

1. Visual Studio: Pastikan Anda telah menginstal Visual Studio di sistem Anda. Anda dapat mengunduhnya dari situs web.

2.  Aspose.HTML untuk .NET: Anda dapat memperoleh perpustakaan dari situs web Aspose[Di Sini](https://releases.aspose.com/html/net/).

3. Direktori Data Anda: Siapkan direktori tempat Anda menyimpan file EPUB dan tempat gambar keluaran akan disimpan.

4. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# sangat penting untuk memahami dan mengimplementasikan contoh kode yang disediakan dalam tutorial ini.

## Mengimpor Namespace yang Diperlukan

Sebelum kita mulai bekerja dengan Aspose.HTML untuk .NET, Anda perlu mengimpor namespace yang diperlukan ke dalam kode C# Anda. Namespace ini menyediakan akses ke fitur Aspose.HTML untuk .NET.

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using Aspose.Html.Rendering.Image;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
using System.IO;
using System.Drawing;
using System.Collections.Generic;
```

Sekarang kita sudah memiliki prasyarat dan namespace, mari beralih ke contoh langkah demi langkah.

## Mengonversi EPUB ke JPEG

```csharp
    string dataDir = "Your Data Directory";
    // Buka file EPUB yang ada untuk dibaca.
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // Panggil metode ConvertEPUB untuk mengonversi file EPUB menjadi gambar.
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### Langkah

1. Berikan jalur ke file EPUB Anda di variabel dataDir.
2. Buka file EPUB untuk dibaca menggunakan FileStream.
3. Panggil metode ConvertEPUB, meneruskan aliran EPUB, ImageSaveOptions yang menentukan format keluaran (JPEG), dan nama file keluaran ("output.jpg").
5. File EPUB dikonversi ke gambar JPEG.

Dalam contoh ini, kita membuka file EPUB, membaca kontennya, dan mengubahnya menjadi format gambar JPEG. Gambar keluaran disimpan sebagai "output.jpg."

## Mengonversi EPUB ke PNG

Anda dapat dengan mudah mengonversi file EPUB ke berbagai format gambar seperti PNG, BMP, GIF, dan TIFF menggunakan struktur kode yang serupa. Berikut ini contoh untuk mengonversi ke PNG:

```csharp

    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Png);
        Converter.ConvertEPUB(stream, options, "output.png");
    }

```
### Langkah
1. Buka file EPUB untuk dibaca menggunakan FileStream.
2. Inisialisasi objek ImageSaveOptions dengan format output yang diinginkan (dalam hal ini, PNG).
3. Panggil metode ConvertEPUB, meneruskan aliran EPUB, opsi penyimpanan gambar, dan nama file keluaran.
4. File EPUB dikonversi ke format gambar yang ditentukan.

## Tentukan Opsi Penyimpanan Gambar

Anda dapat menyesuaikan keluaran gambar dengan menentukan opsi seperti ukuran halaman dan warna latar belakang. Berikut ini contohnya:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Jpeg)
        {
            PageSetup =
            {
                AnyPage = new Page()
                {
                    Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
                }
            },
            BackgroundColor = Color.AliceBlue,
        };
        Converter.ConvertEPUB(stream, options, "output.jpg");
    }
```
### Langkah

1.  Berikan jalur ke file EPUB Anda di`dataDir` variabel.
2.  Buka file EPUB untuk dibaca menggunakan a`FileStream`.
3.  Buat sebuah`ImageSaveOptions` objek dan tentukan format output yang diinginkan (JPEG).
4. Sesuaikan ukuran halaman dan warna latar belakang, jika diperlukan.
5.  Hubungi`ConvertEPUB`metode, meneruskan aliran EPUB, opsi penyimpanan gambar, dan nama file keluaran.
6. File EPUB dikonversi menjadi gambar dengan opsi yang ditentukan.

## Tentukan Penyedia Streaming Kustom

Jika Anda perlu memanipulasi aliran keluaran, Anda dapat menggunakan penyedia aliran khusus. Berikut ini contohnya:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        using (var streamProvider = new MemoryStreamProvider())
        {
            Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), streamProvider);
            
            for (int i = 0; i < streamProvider.Streams.Count; i++)
            {
                var memory = streamProvider.Streams[i];
                memory.Seek(0, SeekOrigin.Begin);
                
                using (FileStream fs = File.Create($"page_{i + 1}.jpg"))
                {
                    memory.CopyTo(fs);
                }
            }
        }
    }

```
Kode Sumber Kelas MemoryStreamProvider.

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

### Langkah
1.  Berikan jalur ke file EPUB Anda di`dataDir` variabel.
2.  Buka file EPUB untuk dibaca menggunakan a`FileStream`.
3.  Membuat`MemoryStreamProvider` untuk menangani aliran keluaran khusus.
4.  Hubungi`ConvertEPUB` metode, meneruskan aliran EPUB, opsi penyimpanan gambar (JPEG), dan penyedia aliran khusus.
5. Iterasi melalui aliran memori di penyedia khusus, simpan ke file individual.
6. Contoh ini memungkinkan Anda memanipulasi dan menyimpan beberapa aliran keluaran sesuai kebutuhan.

## Kesimpulan

Aspose.HTML untuk .NET adalah perpustakaan serbaguna yang menyederhanakan pekerjaan dengan dokumen EPUB dan HTML. Dengan kemampuan untuk mengonversi dokumen EPUB ke berbagai format gambar dan opsi yang dapat disesuaikan, ia menawarkan beragam aplikasi untuk pengembang.

---

## Pertanyaan yang Sering Diajukan

### 1. Di mana saya dapat mengunduh Aspose.HTML untuk .NET?

 Anda dapat mengunduh Aspose.HTML untuk .NET dari halaman rilis[Di Sini](https://releases.aspose.com/html/net/).

### 2. Bagaimana saya bisa mendapatkan lisensi sementara Aspose.HTML untuk .NET?

 Untuk mendapatkan lisensi sementara, kunjungi halaman lisensi sementara[Di Sini](https://purchase.aspose.com/temporary-license/).

### 3. Di mana saya dapat menemukan dukungan tambahan untuk Aspose.HTML untuk .NET?

 Untuk pertanyaan atau masalah apa pun, Anda dapat mencari bantuan dari komunitas Aspose di forum dukungan[Di Sini](https://forum.aspose.com/).

### 4. Bisakah saya mengonversi dokumen EPUB ke format lain seperti PDF atau XPS?

Ya, Anda dapat menggunakan Aspose.HTML untuk .NET untuk mengonversi dokumen EPUB ke berbagai format, termasuk PDF dan XPS.

### 5. Apakah Aspose.HTML untuk .NET cocok untuk proyek skala kecil dan besar?

Sangat! Aspose.HTML untuk .NET dirancang agar dapat diskalakan, menjadikannya pilihan tepat untuk proyek dengan segala ukuran.
