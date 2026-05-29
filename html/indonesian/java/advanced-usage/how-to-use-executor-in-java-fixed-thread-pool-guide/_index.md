---
category: general
date: 2026-05-28
description: cara menggunakan executor di Java dengan fixed thread pool, mengekstrak
  teks dari HTML, dan mempercepat pemrosesan – contoh lengkap thread pool Java.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: id
og_description: Cara menggunakan executor di Java dengan fixed thread pool. Pelajari
  contoh lengkap thread pool Java yang mengekstrak teks dari file HTML secara efisien.
og_title: Cara Menggunakan Executor di Java – Panduan Fixed Thread Pool
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: how to use executor in Java with a fixed thread pool, extract text
    from HTML and speed up processing – a complete java thread pool example.
  headline: How to Use Executor in Java – Fixed Thread Pool Guide
  type: TechArticle
tags:
- Java
- Concurrency
- HTML Parsing
title: Cara Menggunakan Executor di Java – Panduan Fixed Thread Pool
url: /id/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Executor di Java – Panduan Fixed Thread Pool

Pernah bertanya-tanya **bagaimana cara menggunakan executor** untuk menjalankan banyak tugas sekaligus tanpa menghabiskan memori Anda? Anda tidak sendirian. Dalam banyak aplikasi dunia nyata Anda perlu merayapi sebuah folder berisi file HTML, mengambil teks body, dan melakukannya dengan cepat—tepat skenario yang diselesaikan tutorial ini.

Kami akan membahas implementasi **fixed thread pool java** yang mengekstrak teks dari HTML, mencetak jumlah karakter tiap file, dan menutup dengan bersih. Pada akhir tutorial Anda akan memiliki **java thread pool example** yang berdiri sendiri dan dapat dimasukkan ke proyek apa pun, serta beberapa tips tentang menyesuaikan ukuran pool dan menangani kasus pinggiran.

> **Apa yang Anda butuhkan**  
> * Java 17 (atau JDK terbaru apa pun)  
> * Sebuah perpustakaan parsing HTML kecil – kami akan memakai *jsoup* karena sudah teruji dan tanpa konfigurasi.  
> * Beberapa file *.html* contoh di direktori pilihan Anda.

---

## Cara Menggunakan Executor dengan Fixed Thread Pool

Inti dari setiap program Java yang berat pada concurrency adalah `ExecutorService`. Dengan membuat **fixed thread pool** kita memberi tahu JVM untuk mempertahankan tepat N thread pekerja tetap hidup, yang mencegah overhead pembuatan thread dan membatasi penggunaan sumber daya.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Mengapa ini penting:*  
Jika Anda meluncurkan `Thread` baru untuk setiap file HTML, OS harus menjadwalkan puluhan thread pada laptop yang biasa, yang menyebabkan thrashing pada context‑switch. Pool tetap menggunakan kembali empat thread yang sama, memberi Anda penggunaan CPU yang dapat diprediksi.

---

## Menentukan File HTML yang Akan Diproses – Fixed Thread Pool Java

Selanjutnya kami mencantumkan file‑file yang ingin kami masukkan ke dalam pool. Pada aplikasi nyata Anda mungkin akan menelusuri pohon direktori; di sini kami menyederhanakannya.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Tip:* `List.of` mengembalikan daftar yang tidak dapat diubah, yang aman untuk dibagikan antar thread tanpa sinkronisasi tambahan.

---

## Mengirimkan Tugas Terpisah untuk Setiap File HTML

Sekarang kami menyerahkan setiap path ke executor. Lambda yang kami kirimkan akan berjalan **secara paralel** pada salah satu dari empat thread pekerja.

```java
// Step 3: Dispatch a parsing job for every file
for (String htmlFilePath : htmlFilePaths) {
    executor.submit(() -> {
        // Each lambda runs on a thread from the pool
        try {
            // Step 4: Open the document, extract its text, and display the length
            String text = extractBodyText(htmlFilePath);
            System.out.println(htmlFilePath + " → " + text.length() + " chars");
        } catch (IOException e) {
            System.err.println("Failed to read " + htmlFilePath);
            e.printStackTrace();
        }
    });
}
```

**Mengapa kami membungkus logika dalam sebuah metode** (`extractBodyText`) akan menjadi jelas pada bagian berikutnya—ini membuat lambda tetap rapi dan memungkinkan kami menggunakan kembali kode ekstraksi di tempat lain.

---

## Mengekstrak Teks dari HTML – Logika Inti

Berikut helper yang dapat dipakai ulang yang sebenarnya **mengekstrak teks dari html** menggunakan Jsoup. Ia membuka file, mem-parsing DOM, dan mengembalikan teks body polos.

```java
/**
 * Reads an HTML file and returns the plain text inside the <body>.
 *
 * @param path absolute or relative path to the .html file
 * @return body text without tags
 * @throws IOException if the file cannot be read
 */
private static String extractBodyText(String path) throws IOException {
    // Jsoup parses the file into a Document object.
    org.jsoup.nodes.Document doc = org.jsoup.Jsoup.parse(new java.io.File(path), "UTF-8");
    // getBody() gives us the <body> element; text() strips all tags.
    return doc.body().text();
}
```

*Mengapa Jsoup?* Ia ringan, menangani markup yang tidak sempurna dengan elegan, dan tidak memerlukan mesin browser penuh. Metode ini melempar `IOException` sehingga pemanggil dapat memutuskan cara mencatat atau memulihkan—sempurna untuk skenario thread‑pool di mana Anda tidak ingin satu file buruk menghentikan seluruh executor.

---

## Menutup Executor dengan Anggun – Membuat Fixed Thread Pool

Setelah kami mengirimkan semua pekerjaan, kami harus memberi tahu pool untuk berhenti menerima pekerjaan baru dan menyelesaikan yang sudah berada dalam antrian.

```java
// Step 5: Initiate an orderly shutdown once all tasks are queued
executor.shutdown();
try {
    // Wait up to 30 seconds for all tasks to finish
    if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
        System.err.println("Timed out waiting for tasks; forcing shutdown.");
        executor.shutdownNow();
    }
} catch (InterruptedException ie) {
    // Preserve interrupt status and force shutdown
    Thread.currentThread().interrupt();
    executor.shutdownNow();
}
```

*Penjelasan:* `shutdown()` mencegah pengiriman baru, sementara `awaitTermination` memblokir hingga setiap pekerjaan parsing selesai (atau batas waktu habis). Jika ada yang macet, `shutdownNow()` berusaha membatalkan tugas yang sedang berjalan. Pola ini adalah cara yang direkomendasikan untuk **create fixed thread pool** dengan aman.

---

## Contoh Lengkap yang Dapat Dijalanin

Menggabungkan semuanya, berikut satu file yang dapat Anda kompilasi dan jalankan. Ia mencakup impor yang diperlukan, metode `main`, dan helper yang dijelaskan di atas.

```java
import java.io.IOException;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

/**
 * Demonstrates how to use executor with a fixed thread pool to
 * extract text from multiple HTML files concurrently.
 */
public class HtmlThreadPoolDemo {

    public static void main(String[] args) {
        // 1️⃣ Build a fixed‑size pool (adjust the size for your hardware)
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ Define the files we want to process
        List<String> htmlFilePaths = List.of(
                "YOUR_DIRECTORY/a.html",
                "YOUR_DIRECTORY/b.html",
                "YOUR_DIRECTORY/c.html",
                "YOUR_DIRECTORY/d.html"
        );

        // 3️⃣ Submit a parsing task for each file
        for (String htmlFilePath : htmlFilePaths) {
            executor.submit(() -> {
                try {
                    String text = extractBodyText(htmlFilePath);
                    System.out.println(htmlFilePath + " → " + text.length() + " chars");
                } catch (IOException e) {
                    System.err.println("Error processing " + htmlFilePath);
                    e.printStackTrace();
                }
            });
        }

        // 5️⃣ Shut down the pool cleanly
        executor.shutdown();
        try {
            if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("Tasks took too long; forcing shutdown.");
                executor.shutdownNow();
            }
        } catch (InterruptedException ie) {
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }

    /**
     * Reads an HTML file and returns the plain text inside the <body>.
     *
     * @param path path to the .html file
     * @return body text without markup
     * @throws IOException if file cannot be read
     */
    private static String extractBodyText(String path) throws IOException {
        Document doc = Jsoup.parse(new java.io.File(path), "UTF-8");
        return doc.body().text();
    }
}
```

**Output yang diharapkan** (asumsi tiap file berisi kira‑kira 1 200 karakter teks body):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

Jika ada file yang hilang atau rusak, Anda akan melihat jejak stack yang dicetak ke `stderr`, tetapi tugas‑tugas lain akan tetap berjalan—tepat seperti yang harus dilakukan oleh **java thread pool example** yang baik.

---

## Pertanyaan Umum & Kasus Pinggiran

| Pertanyaan | Jawaban |
|------------|---------|
| *Bagaimana jika saya memiliki lebih dari empat file?* | Pool akan menempatkan tugas tambahan dalam antrian dan menjalankannya begitu ada thread yang tersedia. Tidak perlu kode tambahan. |
| *Haruskah saya menggunakan `newCachedThreadPool` sebagai gantinya?* | `newCachedThreadPool` membuat thread sesuai permintaan dan dapat tumbuh tak terbatas, yang berisiko untuk pekerjaan I/O‑heavy. **Fixed thread pool** memberi Anda penggunaan memori dan CPU yang dapat diprediksi. |
| *Bagaimana cara mengubah ukuran pool berdasarkan core CPU?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` adalah pola umum. |
| *Bagaimana jika parsing gagal untuk satu file?* | `catch (IOException e)` di dalam lambda mengisolasi kegagalan, mencatatnya, dan membiarkan sisanya tetap bekerja. |
| *Bisakah saya mengembalikan teks yang diekstrak ke pemanggil?* | Ya—gunakan `Future<String>` alih‑alih `submit(Runnable)`. Kodenya akan menjadi `Future<String> f = executor.submit(() -> extractBodyText(path));` dan kemudian `String result = f.get();`. |

---

## Kesimpulan

Kami telah membahas **bagaimana cara menggunakan executor** untuk memutar **fixed thread pool java** yang memproses kumpulan file HTML secara paralel, mengekstrak teks body mereka, dan melaporkan jumlah karakter. **java thread pool example** lengkap ini menunjukkan manajemen sumber daya yang tepat, penanganan error, dan metode ekstraksi yang dapat dipakai ulang.

Langkah selanjutnya? Coba ganti implementasi `extractBodyText` dengan scraper yang lebih canggih, bereksperimen dengan ukuran pool yang lebih besar, atau alirkan hasilnya ke basis data. Anda juga dapat menjelajahi `CompletionService` untuk mengambil hasil segera setelah siap, yang berguna ketika ukuran file sangat bervariasi.

Silakan ubah path direktori, tambahkan lebih banyak file, atau integrasikan potongan kode ini ke dalam kerangka kerja perayapan yang lebih besar. Pola inti—membuat pool, mengirimkan tugas independen, dan menutup dengan anggun—tetap sama, tak peduli seberapa kompleks beban kerja Anda.

Selamat coding, dan semoga thread Anda selalu hidup (sampai Anda mematikannya, tentu saja)!

## Tutorial Terkait

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Use Aspose.HTML for Java - Mastering HTML5 Canvas Rendering](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}