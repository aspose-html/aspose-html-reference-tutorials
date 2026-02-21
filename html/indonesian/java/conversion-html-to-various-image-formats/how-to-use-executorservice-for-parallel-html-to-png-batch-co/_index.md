---
category: general
date: 2026-02-21
description: Cara menggunakan ExecutorService untuk mengonversi HTML ke PNG dengan
  cepat. Pelajari cara mengonversi batch file HTML dengan tugas paralel di Java.
draft: false
keywords:
- how to use executorservice
- convert html to png
- how to run parallel tasks
- how to convert html to png
- batch convert html files
language: id
og_description: Cara menggunakan ExecutorService untuk mengonversi batch file HTML
  menjadi PNG. Panduan langkah demi langkah dengan contoh Java lengkap.
og_title: Cara Menggunakan ExecutorService untuk Konversi HTML ke PNG Secara Paralel
tags:
- Java
- concurrency
- Aspose.HTML
- image‑conversion
title: Cara Menggunakan ExecutorService untuk Konversi Batch HTML ke PNG secara Paralel
url: /id/java/conversion-html-to-various-image-formats/how-to-use-executorservice-for-parallel-html-to-png-batch-co/
---

placeholders.

Now produce final output with all content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan ExecutorService untuk Konversi Batch HTML‑ke‑PNG Paralel

Pernah bertanya-tanya **bagaimana cara menggunakan ExecutorService** ketika Anda memiliki folder penuh halaman HTML yang harus diubah menjadi gambar PNG? Anda bukan satu-satunya—banyak pengembang mengalami hal ini ketika pipeline pelaporan web mereka terhenti pada loop konversi satu‑thread.  

Berita baik? Dengan beberapa baris Java dan Aspose.HTML `Converter` yang kuat, Anda dapat membuat pool thread pekerja, memberi setiap file HTML ke konverter, dan melihat gambar muncul secara paralel. Dalam tutorial ini kami juga akan membahas dasar‑dasar **convert html to png**, menunjukkan cara **run parallel tasks**, dan memberi Anda skrip **batch convert html files** yang siap dijalankan.

## Prasyarat

- Java 17 atau lebih baru (kode menggunakan API modern `java.nio.file`).  
- Pustaka Aspose.HTML untuk Java di classpath Anda. Anda dapat mengunduhnya dari Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

- Sebuah direktori yang berisi file `.html` sumber dan folder output kosong.  
- Jumlah RAM yang cukup—setiap konversi berjalan di thread masing‑masing, jadi ukuran pool harus sesuai dengan jumlah core CPU yang Anda miliki.

> **Pro tip:** Jika Anda menggunakan mesin dengan hyper‑threading, `Runtime.getRuntime().availableProcessors()` biasanya mengembalikan jumlah core yang optimal.

## Langkah 1 – Tentukan Jalur Input dan Output

Pertama kita perlu memberi tahu Java di mana HTML berada dan ke mana PNG harus disimpan. Menggunakan objek `Path` membuat kode tetap independen platform.

```java
import java.nio.file.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Input folder containing .html files
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        // Output folder for the generated .png files
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");

        // Ensure the output folder exists
        Files.createDirectories(outputDir);
```

> **Why this matters:** Membuat direktori output terlebih dahulu mencegah `FileNotFoundException` ketika thread pekerja pertama mencoba menulis file.

## Langkah 2 – Bangun Thread Pool dengan Ukuran Tetap

Inti dari **how to use ExecutorService** terletak pada pembuatan pool yang sesuai dengan perangkat keras Anda. Pool *fixed* menjamin kami tidak akan membuat lebih banyak thread daripada yang dapat dijalankan.

```java
        // Create a thread pool sized to the number of available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());
```

> **Explanation:** `ExecutorService` menyembunyikan manajemen thread tingkat rendah. Dengan menggunakan `newFixedThreadPool`, kami membiarkan JVM menggunakan kembali thread, yang mengurangi beban membuat dan menghancurkan thread secara terus‑menerus.

## Langkah 3 – Kirim Satu Tugas Konversi per File HTML

Sekarang kami menelusuri direktori input, memilih setiap file `*.html`, dan menyerahkannya ke pool. Setiap tugas adalah lambda kecil yang memanggil `Converter.convert`.

```java
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        // Build the output filename by swapping .html for .png
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();

                        // Perform the actual conversion
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }
```

### Apa yang terjadi di balik layar?

1. **DirectoryStream** membaca nama file secara malas, sehingga penggunaan memori tetap rendah bahkan dengan ribuan file.  
2. Lambda menangkap `htmlFile` dan `outputDir`—tidak perlu kelas `Runnable` terpisah.  
3. `Converter.convert` adalah panggilan blocking yang membaca HTML, merendernya, dan menulis PNG. Karena setiap panggilan berjalan di thread masing‑masing, beberapa file diproses secara bersamaan—tepat seperti yang Anda harapkan saat **run parallel tasks**.

## Langkah 4 – Matikan Pool dengan Anggun

Setelah semua tugas dimasukkan ke antrian, kami memberi tahu pool untuk berhenti menerima pekerjaan baru dan menunggu semuanya selesai. Jika ada yang macet, batas waktu akan menghentikan setelah satu jam, yang cukup longgar untuk kebanyakan pekerjaan batch.

```java
        // No more tasks will be submitted
        pool.shutdown();

        // Wait up to 1 hour for all conversions to complete
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }

        System.out.println("All conversions completed.");
    }
}
```

> **Edge case:** Jika Anda memiliki file HTML yang sangat besar, Anda mungkin ingin meningkatkan batas waktu atau memantau penggunaan memori. Menambahkan `pool.setRejectedExecutionHandler(new ThreadPoolExecutor.CallerRunsPolicy())` memaksa thread pemanggil menjalankan tugas berlebih, mencegah `RejectedExecutionException`.

## Contoh Lengkap yang Siap Dijalan

Berikut adalah seluruh program, dapat disalin‑tempel ke dalam satu file `ParallelBatchConversion.java`.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.*;
import java.util.concurrent.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Step 1: Define source and destination folders
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");
        Files.createDirectories(outputDir);

        // Step 2: Create a thread pool sized to the available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());

        // Step 3: Submit a conversion task for each HTML file found
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }

        // Step 4: Shut down the pool and wait for all conversions to finish
        pool.shutdown();
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }
        System.out.println("All conversions completed.");
    }
}
```

### Output yang Diharapkan

Menjalankan program mencetak satu baris untuk setiap konversi yang berhasil:

```
Converted: report1.html
Converted: dashboard.html
Converted: summary.html
All conversions completed.
```

Jika sebuah file gagal, Anda akan melihat baris error dengan pesan pengecualian, sehingga debugging menjadi sederhana.

## Cara Memperluas Pola Ini

- **Berbagai format gambar:** Ganti ekstensi `.png` dengan `.jpg` atau `.bmp` dan sesuaikan opsi konversi Aspose yang bersangkutan.  
- **Jumlah thread dinamis:** Untuk beban kerja I/O‑bound Anda mungkin meningkatkan ukuran pool (`availableProcessors() * 2`).  
- **Pemantauan progres:** Ganti `System.out.println` dengan pustaka progress bar yang thread‑safe seperti `jline` atau log ke file.  
- **Penanganan error:** Kumpulkan path yang gagal ke dalam `List<Path>` dan coba lagi setelah loop utama selesai.

## Pertanyaan yang Sering Diajukan

**Q: Apakah ini bekerja di Windows dan Linux?**  
A: Ya. `java.nio.file` menyembunyikan sistem file yang mendasarinya, sehingga kode yang sama berjalan tanpa perubahan pada OS apa pun yang mendukung Java.

**Q: Bagaimana jika saya memiliki lebih dari 10 000 file HTML?**  
A: Iterator `DirectoryStream` membaca entri secara malas, sehingga memori tetap rendah. Pastikan saja disk Anda memiliki ruang kosong yang cukup untuk output PNG.

**Q: Bisakah saya membatasi memori yang digunakan setiap konversi?**  
A: Aspose.HTML memungkinkan Anda mengonfigurasi mesin rendering melalui `HtmlLoadOptions` dan `ImageSaveOptions`. Anda dapat menetapkan ukuran bitmap maksimum atau mengaktifkan rendering kualitas rendah untuk menjaga konsumsi RAM tetap terkendali.

## Kesimpulan

Kami telah menjelaskan **how to use ExecutorService** untuk **batch convert html files** menjadi gambar PNG, menjelaskan mengapa pool ukuran tetap adalah titik optimal untuk rendering CPU‑bound, dan memberi Anda program Java lengkap yang dapat disalin‑tempel. Dengan mengikuti langkah‑langkah di atas, Anda akan mengubah loop satu‑thread yang lambat menjadi pipeline cepat dan skalabel yang dapat menangani ribuan file dengan satu perintah.

Siap untuk tantangan berikutnya? Coba ganti `Converter.convert` dengan ekspor PDF Aspose untuk **convert html to pdf**, atau integrasikan logika ini ke dalam microservice Spring Boot yang menerima permintaan upload‑and‑convert. Ide utama—menggunakan `ExecutorService` untuk **run parallel tasks**—tetap sama, dan Anda akan menemukan kegunaannya di banyak skenario pemrosesan batch.

Selamat coding, dan semoga thread Anda selalu hidup! 

![diagram cara menggunakan executorservice](placeholder.png "Diagram yang menggambarkan alur kerja thread pool untuk konversi HTML‑ke‑PNG paralel")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}