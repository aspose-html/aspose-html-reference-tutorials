---
category: general
date: 2026-02-10
description: Pelajari cara menggunakan fixed thread pool Java untuk menghitung gambar
  dalam file HTML, menjalankan tugas secara bersamaan di Java, dan mematikan executor
  service dengan benar.
draft: false
keywords:
- java fixed thread pool
- how to count images
- shutdown executor service
- java parallel file processing
- run tasks concurrently java
language: id
og_description: Menguasai penggunaan fixed thread pool Java untuk menghitung gambar,
  memproses file secara paralel, dan mematikan layanan executor dengan aman.
og_title: 'java fixed thread pool: Hitung Gambar pada File Paralel'
tags:
- Java
- Concurrency
- Aspose.HTML
title: 'java fixed thread pool: Hitung Gambar dalam File Paralel'
url: /id/java/data-handling-stream-management/java-fixed-thread-pool-count-images-in-parallel-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java fixed thread pool – Tutorial Penghitungan Gambar Paralel

Pernah bertanya-tanya bagaimana cara **java fixed thread pool** melalui puluhan file HTML dan mendapatkan hitungan gambar dengan cepat? Mungkin Anda telah menatap sebuah direktori halaman, berpikir “Saya perlu tahu berapa banyak tag `<img>` yang dimiliki setiap file”, dan kemudian menyadari bahwa loop satu‑thread akan memakan waktu lama.  

Kabar baiknya, Anda tidak perlu menulis manajer thread khusus atau berjuang dengan objek `Thread` tingkat‑rendah. Dalam panduan ini kami akan menunjukkan secara tepat **how to count images** menggunakan *java fixed thread pool*, menjalankan tugas secara bersamaan java, dan dengan elegan **shutdown executor service** ketika pekerjaan selesai.  

Kami akan membahas semuanya mulai dari menyiapkan pool, menyiapkan daftar file, mengirimkan tugas paralel, menangani kasus tepi, hingga memverifikasi output. Pada akhir tutorial, Anda akan memiliki program siap‑jalankan yang mendemonstrasikan **java parallel file processing** dengan cara yang bersih dan mudah dipelihara.  

## Prasyarat

- Java 17 atau lebih baru (kode menggunakan keyword `var` untuk singkat, tetapi Anda dapat menurunkannya jika diperlukan).
- Aspose.HTML for Java di classpath Anda – Anda dapat mengambilnya dari Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- Sekelompok file HTML yang ingin Anda analisis (tutorial mengasumsikan mereka berada di `YOUR_DIRECTORY/`).
- IDE atau alat build yang Anda nyaman gunakan – IntelliJ IDEA, VS Code, atau `javac` biasa sudah cukup.

## Langkah 1: Buat java fixed thread pool

Sebuah *java fixed thread pool* memberikan Anda sekumpulan thread pekerja terbatas yang dapat digunakan kembali untuk setiap tugas yang dikirimkan. Ini mencegah overhead pembuatan thread baru secara terus‑menerus dan membatasi tingkat konkruensi, yang penting saat Anda membaca file dari disk.

```java
import java.util.concurrent.*;

public class ParallelImageCounter {
    // A pool of 4 threads – adjust based on your CPU cores and I/O profile
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);
}
```

**Why 4?** Jika Anda memiliki laptop quad‑core, empat thread akan menjaga setiap core tetap sibuk tanpa oversubscribing. Pada server dengan lebih banyak core Anda dapat meningkatkan jumlahnya, tetapi ingat bahwa setiap thread akan membuka handle file, sehingga terlalu banyak dapat menghabiskan batas OS.

## Langkah 2: Daftar file HTML yang ingin Anda analisis

Bagian selanjutnya dari **java parallel file processing** hanyalah membangun sebuah array (atau `List`) dari jalur file. Dalam proyek nyata Anda mungkin menelusuri direktori secara rekursif, menyaring berdasarkan ekstensi, atau membaca jalur dari basis data. Berikut pendekatan yang sederhana:

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/a.html",
    "YOUR_DIRECTORY/b.html",
    "YOUR_DIRECTORY/c.html",
    "YOUR_DIRECTORY/d.html"
};
```

Jika Anda perlu menangani kumpulan dinamis, ganti array statis dengan sesuatu seperti:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
String[] htmlFiles = Files.list(dir)
                         .filter(p -> p.toString().endsWith(".html"))
                         .map(Path::toString)
                         .toArray(String[]::new);
```

Potongan kode tersebut mendemonstrasikan **java parallel file processing** untuk jumlah file berapa pun tanpa mengubah bagian kode lainnya.

## Langkah 3: Kirim tugas ke **run tasks concurrently java**

Sekarang masuk ke inti tutorial – kami akan **run tasks concurrently java** dengan mengirimkan lambda untuk setiap file. Setiap tugas memuat dokumen HTML dengan Aspose.HTML, menanyakan semua elemen `<img>`, dan mencetak hitungannya.

```java
import com.aspose.html.HTMLDocument;

public static void main(String[] args) throws InterruptedException {
    for (String filePath : htmlFiles) {
        executor.submit(() -> {
            // Load the document – Aspose.HTML does the heavy lifting
            HTMLDocument document = new HTMLDocument(filePath);
            // querySelectorAll returns a NodeList; its length is the image count
            int imageCount = document.querySelectorAll("img").length;
            System.out.println(filePath + " contains " + imageCount + " images.");
        });
    }

    // Step 4 is next – gracefully shut down the pool
    shutdownAndAwaitTermination();
}
```

**Why use a lambda?** Ini membuat kode tetap singkat dan menghindari pembuatan kelas `Runnable` terpisah. Lambda secara otomatis menangkap `filePath`, sehingga setiap tugas bekerja pada file masing‑masing.

### Cara **count images** secara efisien

Aspose.HTML mem-parsing file sekali, membangun DOM, dan kemudian `querySelectorAll("img")` berjalan dalam O(n) dimana *n* adalah jumlah node. Untuk kebanyakan halaman HTML ini dapat diabaikan. Jika Anda membutuhkan pendekatan yang lebih cepat, hanya streaming (misalnya, untuk file berukuran gigabyte), Anda dapat beralih ke parser SAX, tetapi itu akan mengorbankan kesederhanaan yang kami inginkan.

## Langkah 4: Secara tepat **shutdown executor service**

Jangan pernah lupa menutup pool, atau JVM Anda akan terus berjalan selamanya. Pola di bawah ini adalah cara yang direkomendasikan untuk **shutdown executor service** sambil menunggu semua tugas selesai:

```java
private static void shutdownAndAwaitTermination() {
    executor.shutdown(); // Disable new tasks from being submitted
    try {
        // Wait a while for existing tasks to terminate
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            executor.shutdownNow(); // Cancel currently executing tasks
            // Wait a second for tasks to respond to being cancelled
            if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                System.err.println("Pool did not terminate");
        }
    } catch (InterruptedException ie) {
        // (Re-)Cancel if current thread also interrupted
        executor.shutdownNow();
        // Preserve interrupt status
        Thread.currentThread().interrupt();
    }
}
```

**What if a task hangs?** Pemanggilan `shutdownNow()` berusaha menginterupsi thread yang sedang berjalan. Jika logika penghitungan gambar Anda menghormati interupsi (yang Aspose.HTML tidak memblokir pada I/O), pool akan berakhir dengan bersih. Pola ini adalah standar emas untuk penggunaan **java fixed thread pool** apa pun.

## Langkah 5: Verifikasi output

Jalankan program dari IDE Anda atau melalui command line:

```bash
javac -cp "path/to/aspose-html.jar" ParallelImageCounter.java
java -cp ".:path/to/aspose-html.jar" ParallelImageCounter
```

Output tipikal terlihat seperti:

```
YOUR_DIRECTORY/a.html contains 5 images.
YOUR_DIRECTORY/b.html contains 0 images.
YOUR_DIRECTORY/c.html contains 12 images.
YOUR_DIRECTORY/d.html contains 3 images.
```

Jika Anda melihat hitungan dicetak dalam urutan apa pun, itu diharapkan – thread selesai pada waktu yang berbeda. Hal pentingnya adalah setiap file terhitung dan program keluar dengan bersih setelah urutan shutdown.

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelImageCounter {
    // 1️⃣ Fixed thread pool – change size based on your hardware
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);

    public static void main(String[] args) throws InterruptedException {
        // 2️⃣ List of HTML files – replace with your own directory
        String[] htmlFiles = {
            "YOUR_DIRECTORY/a.html",
            "YOUR_DIRECTORY/b.html",
            "YOUR_DIRECTORY/c.html",
            "YOUR_DIRECTORY/d.html"
        };

        // 3️⃣ Submit a counting task for each file
        for (String filePath : htmlFiles) {
            executor.submit(() -> {
                HTMLDocument document = new HTMLDocument(filePath);
                int imageCount = document.querySelectorAll("img").length;
                System.out.println(filePath + " contains " + imageCount + " images.");
            });
        }

        // 4️⃣ Gracefully shut down the pool
        shutdownAndAwaitTermination();
    }

    // 5️⃣ Helper method to cleanly stop the executor
    private static void shutdownAndAwaitTermination() {
        executor.shutdown(); // Disable new tasks
        try {
            if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
                executor.shutdownNow(); // Cancel currently executing tasks
                if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                    System.err.println("Pool did not terminate");
            }
        } catch (InterruptedException ie) {
            executor.shutdownNow();
            Thread.currentThread().interrupt();
        }
    }
}
```

### Hasil yang Diharapkan

Menjalankan potongan kode mencetak setiap jalur file diikuti oleh jumlah tag `<img>` yang terkandung, kemudian JVM keluar. Tidak ada thread yang tersisa, tidak ada kebocoran memori.

## Kesalahan Umum & Tips Pro

- **Pitfall:** Menggunakan `newCachedThreadPool()` alih‑alih *fixed* pool. Itu membuat thread tak terbatas, yang dapat menghabiskan descriptor file pada batch besar. Tetap gunakan `newFixedThreadPool`.
- **Pro tip:** Jika file HTML Anda sangat besar, pertimbangkan meningkatkan heap (`-Xmx2g`) atau beralih ke parser streaming. Untuk kebanyakan halaman pemasaran, heap default sudah cukup.
- **Pitfall:** Lupa memanggil `shutdown()` – aplikasi Anda akan hang setelah mencetak hasil. Metode `shutdownAndAwaitTermination` di atas menangani ini dengan kuat.
- **Pro tip:** Catat waktu mulai dan selesai setiap tugas jika Anda membutuhkan metrik performa. `System.nanoTime()` sederhana sebelum dan sesudah konstruk `HTMLDocument` memberi tahu berapa lama parsing berlangsung.
- **Pitfall:** Menetapkan jumlah thread secara keras. Gunakan `Runtime.getRuntime().availableProcessors()` untuk memilih nilai default yang masuk akal:

```java
int cores = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(cores);
```

## Topik Terkait yang Mungkin Anda Jelajahi Selanjutnya

- **run tasks concurrently java** dengan `CompletableFuture` untuk pipeline yang lebih ekspresif.
- Menyimpan hitungan gambar ke basis data untuk dasbor analitik.
- Menggunakan **java parallel file processing** dengan API `java.nio.file.Files.walk` yang digabungkan dengan streams.
- Mengimplementasikan `ThreadFactory` khusus untuk memberi thread nama yang bermakna (membantu debugging).

## Kesimpulan

Kami baru saja melewati contoh lengkap dan mandiri yang menunjukkan bagaimana **java fixed thread pool** dapat dimanfaatkan untuk **how to count images** pada banyak file HTML, sekaligus mendemonstrasikan cara yang tepat untuk **shutdown executor service**. Pola ini skalabel dengan baik—ganti array file dengan daftar dinamis, tingkatkan ukuran pool, dan Anda memiliki solusi kuat untuk beban kerja **java parallel file processing** apa pun.  

Cobalah, ubah jumlah thread, dan mungkin tambahkan ekspor CSV dari hasilnya. Langit adalah batasnya ketika Anda menggabungkan fondasi konkruensi yang solid dengan pustaka praktis seperti Aspose.HTML. Selamat coding!  

![java fixed thread pool diagram](image.png){alt="java fixed thread pool diagram"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}