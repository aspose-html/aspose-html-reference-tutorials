---
category: general
date: 2026-04-05
description: Tutorial multithreading Java yang menunjukkan cara menjalankan tugas
  secara paralel menggunakan fixed thread pool di Java dan menghentikan ExecutorService
  dengan aman.
draft: false
keywords:
- java multithreading tutorial
- fixed thread pool java
- shutdown executorservice
- print thread name
- run tasks parallel
language: id
og_description: Tutorial multithreading Java yang memandu Anda menjalankan tugas secara
  paralel, membuat fixed thread pool Java, mencetak nama thread, dan menutup ExecutorService
  dengan bersih.
og_title: tutorial multithreading java – Eksekusi Paralel dengan Fixed Thread Pool
tags:
- Java
- Concurrency
- ExecutorService
title: 'Tutorial multithreading Java: Jalankan Tugas Secara Paralel dengan Fixed Thread
  Pool'
url: /id/java/advanced-usage/java-multithreading-tutorial-run-tasks-parallel-with-fixed-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial multithreading java – Eksekusi Paralel yang Sederhana

Pernah bertanya-tanya bagaimana cara **run tasks parallel** di Java tanpa tenggelam dalam manajemen thread tingkat rendah? Dalam **java multithreading tutorial** ini kami akan memandu Anda langkah demi langkah: menggunakan **fixed thread pool java**, mencetak nama setiap thread, dan dengan bersih **shutdown executorservice** ketika pekerjaan selesai.  

Jika Anda pernah menulis loop yang memblokir pada I/O jaringan atau Anda perlu meng-scrape beberapa halaman web sekaligus, pola yang kami bahas di bawah ini akan menghemat waktu dan mengurangi sakit kepala Anda.  

Kami akan membahas semua yang Anda butuhkan—tanpa dokumentasi eksternal, hanya kode Java murni yang dapat Anda salin‑tempel, jalankan, dan lihat hasilnya. Pada akhir tutorial Anda akan memahami mengapa fixed thread pool sering menjadi pilihan tepat untuk paralelisme terbatas, cara menghentikannya dengan aman, dan cara membuat log Anda lebih mudah dibaca dengan mencetak nama thread.  

> **Prerequisites**: Java 8+ (paket `java.util.concurrent` telah stabil selama bertahun‑tahun), sebuah IDE atau baris perintah sederhana `javac`/`java`, dan pemahaman dasar tentang OOP. Tidak ada pustaka tambahan yang diperlukan selain jar Aspose HTML for Java yang sudah Anda miliki.

---

![diagram tutorial multithreading java yang menunjukkan sebuah thread pool memberi tugas](https://example.com/images/java-multithreading-tutorial.png "diagram tutorial multithreading java")

## tutorial multithreading java – Menyiapkan Fixed Thread Pool

Sebuah **fixed thread pool** membatasi jumlah thread yang berjalan secara bersamaan, mencegah aplikasi Anda membuat terlalu banyak thread OS dan menghabiskan sumber daya. Di sini kami membuat pool dengan empat pekerja:

```java
import java.util.concurrent.*;

public class ParallelProcessingTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Mengapa empat?* Itu sesuai dengan jumlah URL yang akan kami ambil, tetapi Anda dapat menyesuaikan angka ini berdasarkan inti CPU, intensitas I/O, atau batas memori. Factory `Executors` melindungi Anda dari konstruktor `Thread` tingkat‑rendah dan memberi Anda referensi `ExecutorService` yang bersih yang nanti akan Anda **shutdown executorservice**.

## Siapkan URL dan Definisikan Tugas Paralel

Selanjutnya, kami mencantumkan halaman yang ingin diproses. Dalam scraper nyata Anda mungkin akan membaca ini dari file atau basis data, tetapi array statis menjaga contoh tetap mandiri:

```java
        // Step 2: List the web pages to process
        String[] pageUrls = {
            "https://example.com/a.html",
            "https://example.com/b.html",
            "https://example.com/c.html",
            "https://example.com/d.html"
        };
```

Sekarang datang bagian **run tasks parallel**. Untuk setiap URL kami mengirimkan lambda yang memuat dokumen dan mencetak judulnya. Perhatikan penggunaan `Thread.currentThread().getName()` – itu adalah trik **print thread name** kami yang membuat debugging jauh lebih mudah:

```java
        // Step 3: Submit a task for each URL that loads the document and prints its title
        for (String url : pageUrls) {
            executor.submit(() -> {
                try (HTMLDocument doc = new HTMLDocument(url)) {
                    String title = doc.getTitle();
                    // Print the thread name alongside the title
                    System.out.println(Thread.currentThread().getName() + " – " + title);
                } catch (Exception e) {
                    System.err.println(Thread.currentThread().getName() + " failed: " + e.getMessage());
                }
            });
        }
```

> **Pro tip**: Membungkus `HTMLDocument` dalam blok try‑with‑resources menjamin aliran dasar ditutup, bahkan jika halaman gagal dimuat.

## Menutup ExecutorService dengan Elegan

Meninggalkan thread pool tetap hidup setelah pekerjaannya selesai dapat membuat JVM Anda menggantung. Cara yang tepat adalah **shutdown executorservice**, kemudian menunggu terminasi:

```java
        // Step 4: Shut down the pool and wait for all tasks to finish
        executor.shutdown();                         // No new tasks will be accepted
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            // Force shutdown if tasks exceed the timeout
            executor.shutdownNow();
        }
    }
}
```

*Mengapa ada batas waktu?* Ini melindungi Anda dari tugas nakal yang tidak pernah kembali (mis., panggilan jaringan yang menggantung). Jika pool tidak selesai dalam satu menit kami memanggil `shutdownNow()` untuk menginterupsi thread yang masih tertinggal.

### Output yang Diharapkan

Menjalankan program mencetak sesuatu yang mirip dengan:

```
pool-1-thread-1 – Example A
pool-1-thread-3 – Example C
pool-1-thread-2 – Example B
pool-1-thread-4 – Example D
```

Urutan tepatnya dapat bervariasi—karena tugas memang paralel. Yang tetap konstan adalah awalan **print thread name**, yang memberi tahu Anda secara tepat thread mana yang menangani setiap URL.

---

## Variasi Umum & Kasus Tepi

| Situasi | Apa yang Diubah | Alasan |
|-----------|----------------|--------|
| **Lebih banyak URL daripada thread** | Pertahankan ukuran pool yang sama; tugas tambahan akan otomatis masuk antrian. | Fixed pool menangani back‑pressure untuk Anda. |
| **Pekerjaan CPU‑bound** | Set ukuran pool ke `Runtime.getRuntime().availableProcessors()` alih‑alih angka 4 yang ditetapkan secara keras. | Maksimalkan pemanfaatan CPU tanpa oversubscribing. |
| **Perlu membatalkan tugas tertentu** | Simpan referensi `Future<?>` dari `executor.submit()` dan panggil `future.cancel(true)`. | Memberikan kontrol detail atas pekerjaan individual. |
| **Memproses file besar** | Tingkatkan ukuran pool secara moderat *atau* beralih ke `newCachedThreadPool()` jika Anda mengharapkan lonjakan. | Pool cached membuat thread sesuai permintaan, tetapi hati-hati dengan pertumbuhan tak terbatas. |

---

## Kesimpulan

Anda kini memiliki **java multithreading tutorial** yang solid yang menunjukkan cara **run tasks parallel** menggunakan **fixed thread pool java**, **print thread name** untuk logging yang jelas, dan **shutdown executorservice** dengan bersih. Kode lengkap yang dapat dijalankan berada dalam satu kelas, sehingga Anda dapat menambahkannya ke proyek mana pun dan langsung mulai menskalakan pekerjaan I/O‑bound Anda.

Apa selanjutnya? Cobalah mengganti `HTMLDocument` dengan klien HTTP Anda sendiri, bereksperimen dengan ukuran pool yang berbeda, atau mengintegrasikan `CompletionService` untuk mengumpulkan hasil saat selesai. Anda juga dapat menjelajahi `java.util.concurrent.Flow` untuk aliran reaktif jika Anda membutuhkan penanganan back‑pressure di luar antrian sederhana.

Selamat coding, dan ingat: dengan strategi thread‑pool yang tepat, concurrency menjadi *piece of cake*, bukan sumber bug. Jika Anda memiliki pertanyaan, jangan ragu meninggalkan komentar—saya selalu siap mengobrol tentang concurrency Java!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}