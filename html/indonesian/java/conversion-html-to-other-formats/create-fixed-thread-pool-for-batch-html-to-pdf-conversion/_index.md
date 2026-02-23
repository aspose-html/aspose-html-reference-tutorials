---
category: general
date: 2026-02-22
description: Buat fixed thread pool untuk mengonversi HTML ke PDF secara batch secara
  efisien di Java. Pelajari contoh thread pool Java yang menyimpan HTML sebagai PDF
  dengan cepat.
draft: false
keywords:
- create fixed thread pool
- convert html to pdf
- batch html to pdf
- thread pool java example
- save html as pdf
language: id
og_description: Buat pool thread tetap untuk mengonversi HTML ke PDF secara batch.
  Panduan ini memandu Anda melalui contoh pool thread Java yang menyimpan HTML sebagai
  PDF secara efisien.
og_title: Buat Fixed Thread Pool untuk Konversi Batch HTML ke PDF
tags:
- Java
- Concurrency
- PDF Generation
title: Buat Fixed Thread Pool untuk Konversi Batch HTML ke PDF
url: /id/java/conversion-html-to-other-formats/create-fixed-thread-pool-for-batch-html-to-pdf-conversion/
---

{{< /blocks/products/pf/tutorial-page-section >}} etc. Keep.

Also there is a back button shortcode at end.

Now produce final output with all translated content, preserving shortcodes and placeholders.

Let's assemble.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Fixed Thread Pool untuk Konversi Batch HTML ke PDF

Pernah bertanya-tanya bagaimana cara **create fixed thread pool** yang mengubah sekumpulan file HTML menjadi PDF tanpa membebani CPU Anda? Anda bukan satu-satunya. Ketika Anda memiliki puluhan—atau bahkan ratusan—halaman untuk diproses, menjalankannya satu per satu sangat lambat, tetapi memulai thread pool tak terbatas dapat dengan cepat menghabiskan memori.  

Dalam tutorial ini kami akan menyelesaikan dilema tersebut dengan menunjukkan **thread pool Java example** yang **batch HTML to PDF**, menyimpan setiap hasil, dan mematikan dengan bersih. Pada akhir Anda akan dapat **convert HTML to PDF** secara paralel, dan Anda akan memahami mengapa fixed thread pool adalah pilihan tepat untuk kebanyakan pekerjaan batch.

## Apa yang Akan Anda Dapatkan

- Program Java lengkap yang dapat dijalankan yang membuat fixed thread pool.
- Penjelasan langkah‑demi‑langkah setiap baris, sehingga Anda tahu **why** kami melakukan apa yang kami lakukan.
- Panduan memilih library PDF (sehingga Anda dapat **save HTML as PDF** tanpa mencari potongan kode).
- Tips untuk menangani error, menyesuaikan ukuran pool, dan memperluas solusi ke batch yang lebih besar.

**Prerequisites** – Java 8+ terpasang, IDE dasar (IntelliJ, Eclipse, atau VS Code), dan library konversi PDF pada classpath Anda (kami akan menggunakan *OpenHTMLtoPDF* dalam contoh). Tidak diperlukan framework lain.

---

## Buat Fixed Thread Pool – Mengapa Ini Penting

Saat Anda **create fixed thread pool**, Anda memberi tahu JVM berapa banyak thread pekerja yang diizinkan berjalan secara bersamaan. Ini mencegah lonjakan pembuatan thread, menjaga penggunaan memori tetap dapat diprediksi, dan memungkinkan OS menjadwalkan pekerjaan secara efisien.  

Bayangkan seperti jalur kasir di toko kelontong: Anda membuka sejumlah jalur, membiarkan pelanggan mengantri, dan menutup jalur ketika antrean hilang. `FixedThreadPool` bekerja dengan cara yang sama—tugas menunggu gilirannya, tetapi tidak ada thread tambahan yang dibuat secara dinamis.

```java
// Step 1: Build a fixed‑size thread pool with 4 workers
ExecutorService threadPool = Executors.newFixedThreadPool(4);
```

Angka `4` adalah titik awal yang baik pada laptop quad‑core; Anda dapat menyesuaikannya berdasarkan inti CPU dan karakteristik I/O Anda.

## Batch HTML ke PDF: Mengonversi Setiap Halaman

Sekarang pool sudah ada, kita perlu memberi tugas yang **convert HTML to PDF**. Setiap tugas akan:

1. Muat dokumen HTML dari disk.
2. Serahkan ke library PDF.
3. Tuliskan PDF yang dihasilkan kembali ke direktori yang sama.

Karena pekerjaan ini berat pada I/O (membaca file, menulis PDF), pool kecil sering mengungguli pool yang lebih besar yang hanya menganggur menunggu disk.

```java
// Step 2: Submit a conversion job for every HTML file you have
for (int i = 0; i < 4; i++) {
    final int pageIndex = i;               // capture loop variable for the lambda
    threadPool.submit(() -> {
        // Load the HTML file
        Path htmlPath = Paths.get("YOUR_DIRECTORY/page" + pageIndex + ".html");
        String html = Files.readString(htmlPath, StandardCharsets.UTF_8);

        // Convert and save as PDF
        Path pdfPath = Paths.get("YOUR_DIRECTORY/page" + pageIndex + ".pdf");
        convertHtmlToPdf(html, pdfPath);
    });
}
```

> **Pro tip:** Jika Anda memiliki lebih dari empat halaman, cukup tingkatkan batas loop atau baca daftar file secara dinamis—`Files.list(Paths.get("YOUR_DIRECTORY")).filter(p -> p.toString().endsWith(".html"))` membuatnya mudah.

## Penjelasan Contoh Thread Pool Java

Mari kita uraikan **thread pool Java example** baris per baris sehingga Anda tidak hanya menyalin kode, tetapi benar‑benar memahami alurnya.

| Baris | Apa yang Dilakukan | Mengapa Penting |
|------|--------------------|-----------------|
| `ExecutorService threadPool = Executors.newFixedThreadPool(4);` | Membuat instance pool dengan tepat empat thread. | Menjamin jumlah konversi bersamaan yang terbatas, menghindari error out‑of‑memory. |
| `for (int i = 0; i < 4; i++) { … }` | Mengiterasi halaman yang ingin Anda proses. | Loop menggerakkan pembuatan tugas; Anda dapat mengganti batas statis dengan daftar dinamis. |
| `final int pageIndex = i;` | Menangkap indeks loop untuk digunakan di dalam lambda. | Tanpa `final` (atau secara efektif final) lambda akan melihat variabel yang berubah, yang menyebabkan nama file salah. |
| `threadPool.submit(() -> { … });` | Memberikan `Runnable` ke pool untuk eksekusi asynchronous. | Pool menjadwalkan runnable pada thread pekerja yang idle, membebaskan thread utama untuk terus mengantre pekerjaan. |
| `Files.readString(htmlPath, …);` | Membaca file HTML ke dalam `String`. | Diperlukan karena kebanyakan library PDF menerima HTML sebagai string atau stream. |
| `convertHtmlToPdf(html, pdfPath);` | Memanggil metode helper yang melakukan konversi sebenarnya. | Menjaga lambda tetap rapi dan memisahkan kode khusus library. |

Berikut adalah metode helper lengkap menggunakan **OpenHTMLtoPDF**, library ringan yang **save HTML as PDF** dengan satu panggilan.

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

private static void convertHtmlToPdf(String html, Path outputPdf) throws IOException {
    try (OutputStream os = Files.newOutputStream(outputPdf)) {
        PdfRendererBuilder builder = new PdfRendererBuilder();
        builder.withHtmlContent(html, null);     // base URI is null because we use absolute paths
        builder.toStream(os);
        builder.run();                           // blocks until PDF is written
    } catch (Exception e) {
        // Wrap any checked exception as an unchecked one so the lambda can compile
        throw new RuntimeException("Failed to convert HTML to PDF for " + outputPdf, e);
    }
}
```

> **Why OpenHTMLtoPDF?** Ini murni Java, tanpa dependensi native, dan menghormati CSS, yang membuat PDF yang dihasilkan tampak mirip dengan halaman web asli. Jika Anda lebih suka iText atau Flying Saucer, cukup ganti implementasi di dalam `convertHtmlToPdf`.

## Save HTML as PDF – Memilih Library

Anda mungkin bertanya, “Library mana yang harus saya **convert HTML to PDF** dengan?” Berikut perbandingan singkat:

| Library | Maven Coordinates | Kelebihan | Kekurangan |
|---------|-------------------|-----------|------------|
| OpenHTMLtoPDF | `com.openhtmltopdf:openhtmltopdf-pdfbox:1.0.10` | Pure Java, dukungan CSS baik, ringan | Fitur PDF lanjutan terbatas (misalnya enkripsi) |
| iText 7 + html2pdf | `com.itextpdf:html2pdf:3.0.6` | Set fitur lengkap, dukungan komersial | Membutuhkan lisensi berbayar untuk banyak kasus penggunaan |
| Flying Saucer | `org.xhtmlrenderer:flying-saucer-pdf:9.1.22` | Matang, bekerja dengan versi Java lama | Lebih lambat pada dokumen besar, cakupan CSS lebih sedikit |

Pilih yang sesuai dengan kebutuhan proyek Anda. Untuk pekerjaan **batch HTML to PDF**, OpenHTMLtoPDF biasanya menjadi pilihan tepat: cepat, sederhana, dan gratis.

## Shutdown yang Elegan dan Penanganan Error

Meninggalkan executor berjalan dapat mencegah JVM Anda keluar, dan exception yang tidak tertangkap di dalam thread dapat sulit dideteksi. Pola berikut memastikan shutdown yang rapi:

```java
// Step 5: Initiate an orderly shutdown after all tasks are queued
threadPool.shutdown();                     // No new tasks accepted
try {
    // Wait up to 60 seconds for existing tasks to finish
    if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
        threadPool.shutdownNow();          // Force shutdown if tasks linger
    }
} catch (InterruptedException ex) {
    threadPool.shutdownNow();              // Preserve interrupt status
    Thread.currentThread().interrupt();
}
```

- `shutdown()` memberi tahu pool untuk menyelesaikan apa yang sedang dikerjakan tetapi menolak pekerjaan baru.
- `awaitTermination` memblokir hingga semua selesai atau batas waktu habis.
- `shutdownNow()` mencoba membatalkan tugas yang sedang berjalan—berguna untuk penghentian paksa.

Jika ada konversi yang gagal, `RuntimeException` yang kami lempar akan naik ke executor, yang secara default mencatatnya ke konsol. Dalam produksi Anda dapat menambahkan `ThreadPoolExecutor` khusus dengan metode `afterExecute` yang dioverride untuk mencatat ke file atau sistem pemantauan.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut kelas Java mandiri yang dapat Anda copy‑paste ke `src/main/java/com/example/BatchPdfConverter.java`. Pastikan dependensi OpenHTMLtoPDF ada di classpath Anda.

```java
package com.example;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;
import java.util.concurrent.*;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;

/**
 * Demonstrates how to create a fixed thread pool to batch HTML to PDF conversion.
 * Adjust POOL_SIZE and DIRECTORY constants to fit your environment.
 */
public class BatchPdfConverter {

    private static final int POOL_SIZE = 4;                     // Number of parallel workers
    private static final Path DIRECTORY = Paths.get("YOUR_DIRECTORY"); // Change to your folder

    public static void main(String[] args) {
        ExecutorService threadPool = Executors.newFixedThreadPool(POOL_SIZE);

        // Discover all *.html files in the target directory
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(DIRECTORY, "*.html")) {
            for (Path htmlPath : stream) {
                threadPool.submit(() -> processFile(htmlPath));
            }
        } catch (IOException e) {
            System.err.println("Failed to list HTML files: " + e.getMessage());
        }

        // Graceful shutdown
        thread

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}