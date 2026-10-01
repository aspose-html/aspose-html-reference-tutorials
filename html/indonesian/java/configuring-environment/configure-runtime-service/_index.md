---
date: 2026-02-10
description: Pelajari cara mengatur batas waktu di Aspose.HTML untuk Java, mengonfigurasi
  Runtime Service untuk mengonversi HTML ke PNG, mencegah loop tak terbatas, dan meningkatkan
  kinerja.
linktitle: Configure Runtime Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Cara Mengatur Timeout pada Layanan Runtime Aspose.HTML untuk Java
url: /id/java/configuring-environment/configure-runtime-service/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengatur Timeout di Aspose.HTML untuk Layanan Runtime Java

## Pendahuluan
Jika Anda mencari **how to set timeout** untuk skrip saat bekerja dengan Aspose.HTML untuk Java, Anda berada di tempat yang tepat. Mengontrol eksekusi skrip tidak hanya mencegah loop tak berujung tetapi juga membantu Anda **convert html to png** lebih cepat dan menjaga aplikasi tetap responsif. Dalam tutorial ini kami akan menjelaskan langkah‑langkah tepat untuk mengonfigurasi Runtime Service, membatasi eksekusi skrip, dan akhirnya menghasilkan gambar PNG dari HTML tanpa membuat program Anda macet.

## Cara mengatur timeout di Aspose.HTML Runtime Service
Memahami tujuan Runtime Service memudahkan melihat mengapa timeout penting. Layanan ini berfungsi sebagai sandbox untuk kode sisi‑klien, memberi Anda kemampuan untuk menghentikan JavaScript yang tak terkendali sebelum mengonsumsi semua siklus CPU. Dengan mengatur timeout Anda melindungi server dari skenario penolakan layanan (denial‑of‑service) dan memastikan bahwa **html to png conversion** selesai dalam waktu yang dapat diprediksi.

## Jawaban Cepat
- **What does the Runtime Service do?** Ini memungkinkan Anda mengontrol waktu eksekusi skrip dan mengelola sumber daya saat memproses HTML.  
- **How to set timeout for JavaScript?** Gunakan `runtimeService.setJavaScriptTimeout(TimeSpan.fromSeconds(...))`.  
- **Can I prevent infinite loops?** Ya – timeout menghentikan loop yang melebihi batas yang ditentukan.  
- **Does this affect HTML‑to‑PNG conversion?** Tidak, konversi tetap berlangsung setelah skrip selesai atau dihentikan oleh timeout.  
- **Which Aspose.HTML version is required?** Versi terbaru dari halaman unduhan Aspose.  

## Prasyarat
Sebelum kita masuk ke detail teknis, pastikan Anda memiliki hal‑hal berikut:

1. **Java Development Kit (JDK)** – instal dari [Oracle's website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java Library** – dapatkan build terbaru dari [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse, atau NetBeans akan bekerja dengan baik.  
4. **Basic Java & HTML knowledge** – penting untuk mengikuti potongan kode.  

## Impor Paket
Pertama, impor kelas yang Anda perlukan. Impor `java.io.IOException` diperlukan untuk penanganan file.

```java
import java.io.IOException;
```

## Langkah 1: Buat File HTML dengan Kode JavaScript
Kami akan memulai dengan membuat file HTML sederhana yang berisi loop JavaScript. Loop ini akan berjalan selamanya jika tidak ada timeout, menjadikannya demo yang sempurna untuk Runtime Service.

```java
String code = "<h1>Runtime Service</h1>\r\n" +
        "<script> while(true) {} </script>\r\n" +
        "<p>The Runtime Service optimizes your system by helping it start apps and programs faster.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("runtime-service.html")) {
    fileWriter.write(code);
}
```

- Skrip `while(true) {}` mewakili potensi loop tak berujung.  
- `FileWriter` menulis konten HTML ke **runtime-service.html**.

## Langkah 2: Siapkan Objek Konfigurasi
Selanjutnya, buat instance `Configuration`. Objek ini merupakan tulang punggung semua layanan Aspose.HTML, termasuk Runtime Service.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Langkah 3: Konfigurasikan Runtime Service
Di sinilah kita benar‑benarnya **how to set timeout**. Dengan mengambil `IRuntimeService` dari konfigurasi, kita dapat menentukan batas eksekusi JavaScript.

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

- `setJavaScriptTimeout` membatasi eksekusi skrip pada **5 detik**, secara efektif **preventing infinite loops**.  
- Ini juga **limits script execution** untuk kode sisi‑klien yang berat.

## Langkah 4: Muat Dokumen HTML dengan Konfigurasi
Sekarang muat file HTML menggunakan konfigurasi yang berisi aturan timeout kami.

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

- Dokumen menghormati timeout yang ditetapkan sebelumnya, sehingga loop tak berujung akan dihentikan setelah 5 detik.

## Langkah 5: Konversi HTML ke PNG
Dengan dokumen yang sudah dimuat dengan aman, kita dapat **convert html to png**. Konversi terjadi hanya setelah skrip selesai atau dihentikan oleh timeout.

```java
    com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.ImageSaveOptions(),
        "runtime-service_out.png"
    );
```

- `ImageSaveOptions` memberi tahu Aspose.HTML untuk menghasilkan gambar PNG.  
- File yang dihasilkan, **runtime-service_out.png**, menampilkan HTML yang dirender tanpa macet.

## Langkah 6: Bersihkan Sumber Daya
Terakhir, buang (dispose) objek-objek untuk membebaskan memori dan menghindari kebocoran.

```java
} finally {
    if (document != null) {
        document.dispose();
    }
    if (configuration != null) {
        configuration.dispose();
    }
}
```

- Pembuangan yang tepat sangat penting untuk aplikasi yang berjalan lama.

## Mengapa ini penting
Mengatur timeout bukan hanya jaring pengaman; itu secara langsung meningkatkan keandalan pipeline **html to png conversion**. Ketika Anda mengintegrasikan Aspose.HTML ke dalam layanan web yang memproses HTML buatan pengguna, skrip berbahaya dapat mengunci thread secara tak terbatas. Timeout yang wajar (misalnya, 5 detik) memberi skrip sah cukup waktu untuk berjalan sambil memutus perilaku penyalahgunaan.

## Kesalahan Umum & Pemecahan Masalah
- **Timeout too short** – Halaman kompleks dengan banyak sumber daya mungkin memerlukan batas yang lebih lama. Tingkatkan nilai `TimeSpan` jika Anda melihat terminasi prematur.  
- **Missing disposal** – Lupa memanggil `dispose()` dapat menyebabkan kebocoran memori native, terutama saat memproses banyak dokumen dalam loop.  
- **Incorrect configuration object** – Selalu ambil `IRuntimeService` dari instance `Configuration` yang sama yang Anda gunakan untuk memuat dokumen; jika tidak, timeout tidak akan diterapkan.

## Pertanyaan yang Sering Diajukan

**Q: Apa tujuan Runtime Service dalam Aspose.HTML untuk Java?**  
A: Ini memungkinkan Anda mengontrol waktu eksekusi skrip, membantu **prevent infinite loops** dan menjaga konversi tetap responsif.

**Q: Bagaimana cara mengunduh Aspose.HTML untuk Java?**  
A: Dapatkan versi terbaru dari [releases page](https://releases.aspose.com/html/java/).

**Q: Apakah perlu membuang (dispose) objek `document` dan `configuration`?**  
A: Ya, pembuangan melepaskan sumber daya native dan mencegah kebocoran memori.

**Q: Bisakah saya mengatur timeout JavaScript ke nilai selain 5 detik?**  
A: Tentu – ubah argumen `TimeSpan.fromSeconds()` ke batas yang sesuai dengan skenario Anda.

**Q: Di mana saya dapat menemukan bantuan jika mengalami masalah?**  
A: Kunjungi [Aspose.HTML forum](https://forum.aspose.com/c/html/29) untuk bantuan komunitas dan staf.

---

**Terakhir Diperbarui:** 2026-02-10  
**Diuji Dengan:** Aspose.HTML for Java 24.11 (latest)  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}