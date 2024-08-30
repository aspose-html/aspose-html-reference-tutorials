---
title: Konversi EPUB ke Gambar dalam .NET dengan Aspose.HTML
linktitle: Konversi EPUB ke Gambar dalam .NET
second_title: Aspose.HTML .NET API manipulasi HTML
description: Pelajari cara mengonversi EPUB ke gambar menggunakan Aspose.HTML untuk .NET. Tutorial langkah demi langkah dengan contoh kode dan opsi yang dapat disesuaikan.
type: docs
weight: 11
url: /id/net/html-extensions-and-conversions/convert-epub-to-image/
---

Di era digital saat ini, kemampuan untuk memanipulasi dan mengonversi berbagai format dokumen merupakan keterampilan yang berharga. Aspose.HTML untuk .NET adalah alat canggih yang memungkinkan pengembang untuk bekerja dengan dokumen HTML dan EPUB dengan mudah. Dalam tutorial ini, kita akan mempelajari dunia Aspose.HTML untuk .NET dan memandu Anda melalui proses mengonversi dokumen EPUB ke berbagai format gambar. Kami akan menguraikan setiap contoh menjadi beberapa langkah, menjelaskan setiap langkah di sepanjang prosesnya.

## Prasyarat

Sebelum kita menyelami dunia Aspose.HTML untuk .NET, Anda harus memastikan Anda memiliki prasyarat berikut:

1. Visual Studio: Pastikan Anda telah menginstal Visual Studio di sistem Anda. Anda dapat mengunduhnya dari situs web.

2.  Aspose.HTML untuk .NET: Anda dapat memperoleh pustaka dari situs web Aspose[Di Sini](https://releases.aspose.com/html/net/).

3. Direktori Data Anda: Siapkan direktori tempat Anda menyimpan file EPUB dan tempat gambar keluaran akan disimpan.

4. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# sangat penting untuk memahami dan menerapkan contoh kode yang disediakan dalam tutorial ini.

## Mengimpor Ruang Nama yang Diperlukan

Sebelum kita mulai bekerja dengan Aspose.HTML untuk .NET, Anda perlu mengimpor namespace yang diperlukan ke dalam kode C# Anda. Namespace ini menyediakan akses ke fitur-fitur Aspose.HTML untuk .NET.

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

Sekarang setelah kita memiliki prasyarat dan namespace yang dibutuhkan, mari beralih ke contoh langkah demi langkah.

## Mengonversi EPUB ke JPEG

```csharp
    string dataDir = "Your Data Directory";
    // Buka berkas EPUB yang ada untuk dibaca.
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // Panggil metode ConvertEPUB untuk mengonversi berkas EPUB menjadi gambar.
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### Tangga

1. Berikan jalur ke file EPUB Anda dalam variabel dataDir.
2. Buka berkas EPUB untuk dibaca menggunakan FileStream.
3. Panggil metode ConvertEPUB, lewati aliran EPUB, ImageSaveOptions yang menentukan format keluaran (JPEG), dan nama berkas keluaran ("output.jpg").
5. Berkas EPUB diubah menjadi gambar JPEG.

Dalam contoh ini, kami membuka berkas EPUB, membaca isinya, dan mengubahnya menjadi format gambar JPEG. Gambar keluaran disimpan sebagai "output.jpg."

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
### Tangga
1. Buka berkas EPUB untuk dibaca menggunakan FileStream.
2. Inisialisasi objek ImageSaveOptions dengan format keluaran yang diinginkan (dalam hal ini, PNG).
3. Panggil metode ConvertEPUB, lewati aliran EPUB, opsi penyimpanan gambar, dan nama berkas keluaran.
4. Berkas EPUB dikonversi ke format gambar yang ditentukan.

## Tentukan Opsi Penyimpanan Gambar

Anda dapat menyesuaikan hasil keluaran gambar dengan menentukan opsi seperti ukuran halaman dan warna latar belakang. Berikut contohnya:

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
### Tangga

1.  Berikan jalur ke file EPUB Anda di`dataDir` variabel.
2.  Buka file EPUB untuk membaca menggunakan`FileStream`.
3.  Membuat sebuah`ImageSaveOptions` objek dan tentukan format keluaran yang diinginkan (JPEG).
4. Sesuaikan ukuran halaman dan warna latar belakang, jika diperlukan.
5.  Telepon`ConvertEPUB`metode, meneruskan aliran EPUB, opsi penyimpanan gambar, dan nama berkas keluaran.
6. Berkas EPUB diubah menjadi gambar dengan opsi yang ditentukan.

## Tentukan Penyedia Aliran Kustom

Jika Anda perlu memanipulasi aliran output, Anda dapat menggunakan penyedia aliran kustom. Berikut contohnya:

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

### Tangga
1.  Berikan jalur ke file EPUB Anda di`dataDir` variabel.
2.  Buka file EPUB untuk membaca menggunakan`FileStream`.
3.  Membuat sebuah`MemoryStreamProvider` untuk menangani aliran keluaran khusus.
4.  Telepon`ConvertEPUB` metode, meneruskan aliran EPUB, opsi penyimpanan gambar (JPEG), dan penyedia aliran kustom.
5. Ulangi aliran memori di penyedia khusus, simpan ke dalam berkas individual.
6. Contoh ini memungkinkan Anda untuk memanipulasi dan menyimpan beberapa aliran keluaran sesuai kebutuhan.

## Kesimpulan

Aspose.HTML untuk .NET adalah pustaka serbaguna yang menyederhanakan pekerjaan dengan dokumen EPUB dan HTML. Dengan kemampuan mengonversi dokumen EPUB ke berbagai format gambar dan opsi yang dapat disesuaikan, pustaka ini menawarkan berbagai aplikasi untuk pengembang.

---

## Pertanyaan yang Sering Diajukan

### 1. Di mana saya dapat mengunduh Aspose.HTML untuk .NET?

 Anda dapat mengunduh Aspose.HTML untuk .NET dari halaman rilis[Di Sini](https://releases.aspose.com/html/net/).

### 2. Bagaimana cara mendapatkan lisensi sementara untuk Aspose.HTML untuk .NET?

 Untuk mendapatkan lisensi sementara, kunjungi halaman lisensi sementara[Di Sini](https://purchase.aspose.com/temporary-license/).

### 3. Di mana saya dapat menemukan dukungan tambahan untuk Aspose.HTML for .NET?

 Untuk pertanyaan atau masalah apa pun, Anda dapat mencari bantuan dari komunitas Aspose di forum dukungan[Di Sini](https://forum.aspose.com/).

### 4. Dapatkah saya mengonversi dokumen EPUB ke format lain seperti PDF atau XPS?

Ya, Anda dapat menggunakan Aspose.HTML untuk .NET untuk mengonversi dokumen EPUB ke berbagai format, termasuk PDF dan XPS.

### 5. Apakah Aspose.HTML untuk .NET cocok untuk proyek skala kecil dan besar?

Tentu saja! Aspose.HTML untuk .NET dirancang agar dapat diskalakan, sehingga menjadi pilihan yang tepat untuk proyek dengan berbagai ukuran.
