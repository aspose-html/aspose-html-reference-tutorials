---
category: general
date: 2025-12-27
description: Buat memory stream C# dengan cepat menggunakan panduan langkah demi langkah.
  Pelajari cara membuat stream, mengelola sumber daya, dan mengimplementasikan pembuatan
  stream khusus di .NET.
draft: false
keywords:
- create memory stream c#
- how to create stream
- how to handle resources
- custom stream creation
language: id
og_description: Buat memory stream C# dalam hitungan detik. Tutorial ini menunjukkan
  cara membuat stream, mengelola sumber daya, dan membangun pembuatan stream khusus
  dengan API .NET modern.
og_title: Buat memory stream C# – Panduan Lengkap Stream Kustom
tags:
- stream
- csharp
- .net
- resource-handling
title: Buat memory stream C# – Panduan pembuatan stream khusus
url: /id/net/advanced-features/create-memory-stream-c-custom-stream-creation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat memory stream c# – Panduan pembuatan stream khusus

Pernah membutuhkan untuk **create memory stream c#** tetapi tidak yakin API mana yang harus dipilih? Anda tidak sendirian. Di banyak proyek legacy Anda akan menemukan `IOutputStorage`, sementara basis kode yang lebih baru lebih menyukai `ResourceHandler`. Bagaimanapun, tujuannya sama: menghasilkan sebuah `Stream` yang dapat dikonsumsi oleh kerangka kerja Anda.

Dalam tutorial ini Anda akan belajar **how to create stream** objek, **how to handle resources** dengan aman, dan menguasai **custom stream creation** untuk versi perpustakaan pre‑24.2 dan 24.2+. Pada akhir tutorial Anda akan memiliki contoh yang dapat langsung digunakan dalam solusi .NET apa pun—tanpa referensi misterius, hanya C# murni.

## Apa yang akan Anda dapatkan

- Perbandingan jelas antara pola legacy `IOutputStorage` dengan pendekatan modern `ResourceHandler`.  
- Kode lengkap, siap salin‑tempel yang dapat dikompilasi pada .NET 6+ (atau versi lebih lama, jika Anda membutuhkannya).  
- Tips untuk kasus tepi seperti membuang (dispose) stream, menangani payload besar, dan menguji stream khusus Anda.

> **Pro tip:** Jika Anda menargetkan .NET 8, `ResourceHandler` yang lebih baru memberikan dukungan async bawaan, yang dapat mengurangi beberapa milidetik pada skenario throughput tinggi.

## Buat memory stream c# – Pendekatan Legacy (pre‑24.2)

Ketika Anda terjebak pada versi perpustakaan yang lebih lama, kontrak yang harus Anda penuhi adalah `IOutputStorage`. Antarmuka hanya meminta sebuah metode yang mengembalikan `Stream` untuk nama sumber daya tertentu.

```csharp
using System;
using System.IO;

// Step 1: Implement the old IOutputStorage contract.
public class MyStorage : IOutputStorage
{
    /// <summary>
    /// Returns a stream for the requested resource name.
    /// In a real app you might open a file, a network socket,
    /// or generate data on the fly.
    /// </summary>
    /// <param name="name">Logical name of the resource.</param>
    /// <returns>A writable Stream instance.</returns>
    public Stream CreateStream(string name)
    {
        // Custom stream creation logic.
        // Here we simply return an in‑memory stream.
        // You could also wrap a FileStream if you prefer.
        return new MemoryStream();
    }
}
```

### Mengapa ini berhasil

- **Interface contract** – Kerangka kerja akan memanggil `CreateStream` setiap kali perlu menulis output.  
- **Flexibility** – Karena Anda mengembalikan `Stream`, Anda dapat mengganti `MemoryStream` dengan `FileStream` atau bahkan stream berbuffer khusus nanti tanpa mengubah kode lainnya.  
- **Resource safety** – Pemanggil bertanggung jawab untuk membuang (dispose) stream yang dikembalikan, itulah mengapa kami tidak memanggil `Dispose` di dalam metode.

### Kesalahan umum

| Masalah | Apa yang terjadi | Perbaikan |
|---------|------------------|-----------|
| Mengembalikan stream yang tertutup | Konsumen akan mendapatkan `ObjectDisposedException` saat menulis. | Pastikan stream **terbuka** saat Anda menyerahkannya. |
| Lupa mengatur `Position = 0` setelah menulis | Data terlihat kosong saat dibaca nanti. | Panggil `stream.Seek(0, SeekOrigin.Begin)` sebelum mengembalikan jika Anda telah mengisi sebelumnya. |
| Menggunakan `MemoryStream` yang sangat besar untuk file besar | Kegagalan karena kehabisan memori. | Beralih ke `FileStream` sementara atau stream berbuffer khusus. |

## Buat memory stream c# – Pendekatan Modern (24.2+)

Mulai dari versi 24.2 perpustakaan memperkenalkan `ResourceHandler`. Alih-alih antarmuka, Anda kini mewarisi dari kelas dasar dan menimpa satu metode. Ini memberi Anda titik masuk yang lebih bersih dan ramah async.

```csharp
using System;
using System.IO;

// Step 2: Inherit from the new ResourceHandler base class.
public class MyHandler : ResourceHandler
{
    /// <summary>
    /// Called by the framework to obtain a stream for a resource.
    /// </summary>
    /// <param name="name">The logical name of the resource.</param>
    /// <returns>A writable Stream instance.</returns>
    public override Stream HandleResource(string name)
    {
        // Your custom stream creation logic goes here.
        // For demonstration we use a MemoryStream.
        return new MemoryStream();
    }

    // Optional async version (available in 24.2+)
    public override async Task<Stream> HandleResourceAsync(string name, CancellationToken ct = default)
    {
        // Simulate async work, e.g., fetching data from a service.
        await Task.Delay(10, ct);
        return new MemoryStream();
    }
}
```

### Mengapa memilih `ResourceHandler`

- **Async support** – Metode `HandleResourceAsync` memungkinkan Anda melakukan I/O tanpa memblokir thread.  
- **Built‑in error handling** – Kelas dasar menangkap pengecualian dan mengubahnya menjadi kode error spesifik kerangka kerja.  
- **Future‑proof** – Rilis terbaru menambahkan hook (mis., logging, telemetry) yang hanya berfungsi dengan pola handler.

### Penanganan kasus tepi

1. **Disposal** – Kerangka kerja membuang (dispose) stream setelah selesai, tetapi jika Anda membungkus disposable lain (seperti `FileStream`) Anda harus mengimplementasikan blok `using` di dalam metode dan mengembalikan pembungkus yang meneruskan `Dispose`.  
2. **Large payloads** – Jika Anda memperkirakan payload > 100 MB, gantilah `MemoryStream` dengan `FileStream` yang menunjuk ke file sementara. Contoh:  

   ```csharp
   return new FileStream(Path.GetTempFileName(),
                         FileMode.Create,
                         FileAccess.ReadWrite,
                         FileShare.None,
                         bufferSize: 81920,
                         useAsync: true);
   ```
3. **Testing** – Uji unit handler Anda dengan menyuntikkan mock `IServiceProvider` jika kelas dasar mengambil layanan dari DI. Verifikasi bahwa `HandleResource` mengembalikan stream yang dapat ditulis dan dibaca.

## Cara membuat stream – Panduan cepat

| Skenario | API yang Disarankan | Contoh Kode |
|----------|---------------------|-------------|
| Data sederhana dalam memori | `MemoryStream` | `new MemoryStream()` |
| File sementara besar | `FileStream` (temp) | `new FileStream(Path.GetTempFileName(), FileMode.Create, FileAccess.ReadWrite, FileShare.None, 81920, true)` |
| Sumber berbasis jaringan | `NetworkStream` | `new NetworkStream(socket)` |
| Buffering khusus | Derive from `Stream` | Lihat [Microsoft docs] untuk implementasi stream khusus |

> **Catatan:** Selalu atur `stream.Position = 0` sebelum mengembalikan jika Anda mengisi stream sebelumnya; jika tidak, pembaca hilir akan menganggap stream kosong.

## Ilustrasi Gambar

![Diagram yang menunjukkan proses create memory stream c# process](https://example.com/images/create-memory-stream-diagram.png)

*Alt text:* diagram yang menunjukkan proses create memory stream c# process

## Contoh lengkap yang dapat dijalankan

Berikut adalah aplikasi console minimal yang menunjukkan kedua pendekatan legacy dan modern. Anda dapat menyalin‑tempelnya ke dalam proyek console .NET 6 baru dan menjalankannya apa adanya.

```csharp
using System;
using System.IO;
using System.Threading;
using System.Threading.Tasks;

// -------------------------------------------------
// Legacy implementation (pre‑24.2)
// -------------------------------------------------
public class MyStorage : IOutputStorage
{
    public Stream CreateStream(string name) => new MemoryStream();
}

// -------------------------------------------------
// Modern implementation (24.2+)
// -------------------------------------------------
public class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string name) => new MemoryStream();

    public override async Task<Stream> HandleResourceAsync(string name, CancellationToken ct = default)
    {
        await Task.Delay(10, ct); // simulate async work
        return new MemoryStream();
    }
}

// -------------------------------------------------
// Demo program
// -------------------------------------------------
class Program
{
    static async Task Main()
    {
        // Legacy usage
        IOutputStorage legacy = new MyStorage();
        using (var legacyStream = legacy.CreateStream("legacy"))
        using (var writer = new StreamWriter(legacyStream))
        {
            writer.Write("Hello from legacy API!");
            writer.Flush();
            legacyStream.Seek(0, SeekOrigin.Begin);
            Console.WriteLine(new StreamReader(legacyStream).ReadToEnd());
        }

        // Modern sync usage
        var handler = new MyHandler();
        using (var modernStream = handler.HandleResource("modern"))
        using (var writer = new StreamWriter(modernStream))
        {
            writer.Write("Hello from modern API!");
            writer.Flush();
            modernStream.Seek(0, SeekOrigin.Begin);
            Console.WriteLine(new StreamReader(modernStream).ReadToEnd());
        }

        // Modern async usage
        using (var asyncStream = await handler.HandleResourceAsync("async"))
        using (var writer = new StreamWriter(asyncStream))
        {
            await writer.WriteAsync("Hello from async API!");
            await writer.FlushAsync();
            asyncStream.Seek(0, SeekOrigin.Begin);
            Console.WriteLine(await new StreamReader(asyncStream).ReadToEndAsync());
        }
    }
}
```

**Output yang diharapkan**

```
Hello from legacy API!
Hello from modern API!
Hello from async API!
```

Program ini menunjukkan tiga cara untuk **how to create stream**: `IOutputStorage` lama, `HandleResource` sinkron baru, dan `HandleResourceAsync` async. Ketiga cara tersebut mengembalikan `MemoryStream`, membuktikan bahwa pembuatan stream khusus berfungsi terlepas dari versi mana yang Anda targetkan.

## Pertanyaan yang sering diajukan (FAQ)

**Q: Apakah saya perlu memanggil `Dispose` pada stream yang saya terima?**  
A: Kerangka kerja (atau kode pemanggil Anda) bertanggung jawab atas pembuangan. Jika Anda membungkus disposable lain di dalam stream yang dikembalikan, pastikan ia meneruskan panggilan `Dispose`.

**Q: Bisakah saya mengembalikan stream hanya-baca?**  
A: Ya, tetapi kontrak biasanya mengharapkan stream yang dapat ditulis. Jika Anda hanya perlu membaca, implementasikan `CanWrite => false` dan dokumentasikan keterbatasannya.

**Q: Bagaimana jika data saya lebih besar dari RAM yang tersedia?**  
A: Beralih ke `FileStream` yang didukung oleh file sementara, atau implementasikan stream berbuffer khusus yang menulis ke disk dalam potongan.

**Q: Apakah ada perbedaan kinerja antara kedua pendekatan?**  
A: `ResourceHandler` modern menambahkan overhead kecil karena logika kelas dasar tambahan, tetapi versi async dapat secara dramatis meningkatkan throughput pada tingkat konkruensi tinggi.

## Kesimpulan

Kami baru saja membahas **create memory stream c#** dari semua sudut yang mungkin Anda temui di lapangan. Sekarang Anda tahu **how to create stream** menggunakan pola legacy `IOutputStorage` dan kelas `ResourceHandler` yang lebih baru, serta telah melihat tips praktis untuk **how to handle resources** secara bertanggung jawab dan memperluas pola dengan **custom stream creation** untuk file besar atau skenario async.

Ready for

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}