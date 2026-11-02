---
category: general
date: 2026-06-19
description: Cara memulai thread di Java dengan Runnable yang dapat digunakan kembali,
  memulai beberapa thread, mencetak nama thread, dan mengurai HTML dengan Java. Contoh
  langkah demi langkah.
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: id
og_description: Cara memulai thread di Java menggunakan Runnable, menjalankan beberapa
  thread, mencetak nama thread, dan mengurai HTML dengan Java dalam satu contoh yang
  dapat dijalankan.
og_title: Cara memulai thread di Java – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to start thread in Java with a reusable Runnable, start multiple
    threads, print thread name, and parse HTML with Java. Step‑by‑step example.
  headline: How to start thread in Java – Complete Guide
  type: TechArticle
tags:
- java
- multithreading
- html-parsing
- runnable
title: Cara memulai thread di Java – Panduan Lengkap
url: /id/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Memulai Thread di Java – Panduan Lengkap

Pernah bertanya-tanya **how to start thread** di Java tanpa tenggelam dalam kode boilerplate? Anda bukan satu-satunya. Baik Anda membangun web crawler, pembaruan UI, atau hanya perlu memindahkan perhitungan berat, menguasai pembuatan thread adalah keterampilan penting bagi setiap pengembang Java.

Dalam tutorial ini kami akan membahas skenario praktis: **parse HTML with Java**, mencetak nama thread saat ini, dan **start multiple threads** yang berbagi logika yang sama. Pada akhir tutorial Anda akan mengetahui **how to use Runnable**, memulai beberapa pekerja, dan melihat output yang diharapkan—semua dalam contoh mandiri yang dapat Anda salin‑tempel sekarang.

## Apa yang Akan Anda Pelajari

- Langkah tepat **how to start thread** menggunakan kelas `Thread` dan `Runnable`.
- Cara **start multiple threads** yang mengeksekusi tugas yang sama tanpa menduplikasi kode.
- Cara paling sederhana untuk **print thread name** bersamaan dengan hasil pemrosesan Anda.
- Metode bersih untuk **parse HTML with Java** menggunakan pembantu `HTMLDocument` ringan (atau parser apa pun yang Anda suka).
- Mengapa **how to use runnable** penting untuk kode yang dapat digunakan kembali dan dapat diuji.

Tidak ada pustaka eksternal yang diperlukan untuk contoh inti, tetapi kami akan mencatat di mana Anda dapat mengganti dengan Jsoup atau parser lain jika membutuhkan kekuatan lebih.

## Langkah 1: Definisikan tugas yang dapat digunakan kembali – **how to use runnable**

Hal pertama yang perlu Anda ketahui **how to use runnable** adalah membungkus pekerjaan yang ingin setiap thread lakukan. `Runnable` hanyalah antarmuka fungsional dengan satu metode `run()`, yang membuatnya sempurna untuk ekspresi lambda.

```java
// Define the reusable task
Runnable extractTextLength = () -> {
    // Open the HTML file inside a try‑with‑resources block
    try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
        // Get the length of the body text
        int textLength = doc.getBody().getTextContent().length();

        // Print the thread name and the length
        System.out.println(Thread.currentThread().getName() + ": " + textLength);
    } catch (Exception e) {
        e.printStackTrace();
    }
};
```

**Mengapa ini penting:** Dengan menjaga logika di dalam `Runnable`, Anda dapat memberikannya ke sejumlah objek `Thread`, thread pool, atau bahkan layanan executor nanti. Ini membuat kode Anda DRY dan dapat diuji.

## Langkah 2: **How to start thread** – buat pekerja pertama

Sekarang kita memiliki `Runnable`, meluncurkan thread semudah memanggil konstruktor `Thread`. Pertanyaan **how to start thread** terjawab dalam satu baris:

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

Perhatikan argumen kedua, `"Worker-1"`. Nama itu akan muncul ketika kita nanti **print thread name**, membuat proses debugging jauh lebih jelas.

## Langkah 3: **Start multiple threads** – gunakan kembali Runnable yang sama

Ingin memproses beberapa file HTML sekaligus? Cukup buat `Thread` lain dengan `Runnable` yang sama. Ini menunjukkan **start multiple threads** tanpa menyalin kode tugas:

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

Baik `Worker-1` maupun `Worker-2` akan mengeksekusi blok yang didefinisikan dalam `extractTextLength` secara bersamaan. Karena tugasnya tidak memiliki state (hanya membaca file), tidak ada kondisi balapan yang perlu dikhawatirkan.

## Langkah 4: **Print thread name** saat mem-parsing HTML

Di dalam `Runnable` kami sudah memanggil `Thread.currentThread().getName()`. Itu adalah cara kanonik untuk **print thread name**. Output akan terlihat seperti ini (asumsi isi `<body>` HTML memiliki 1 234 karakter):

```
Worker-1: 1234
Worker-2: 1234
```

Jika Anda menjalankan program pada file yang lebih besar, setiap baris akan menunjukkan panjang yang sama karena kedua thread membaca file yang sama. Ubah path atau berikan nama file sebagai parameter untuk melihat hasil yang berbeda.

## Langkah 5: Contoh lengkap, runnable – dari import hingga eksekusi

Berikut adalah program lengkap, **self‑contained** yang dapat Anda letakkan ke dalam file bernama `HtmlThreadDemo.java`. Program ini menyertakan stub `HTMLDocument` kecil sehingga kode dapat dikompilasi meskipun Anda tidak memiliki parser nyata. Ganti stub dengan Jsoup atau pustaka apa pun yang Anda pilih untuk penggunaan produksi.

```java
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Minimal HTMLDocument helper.
 * In a real project you would use Jsoup or another robust parser.
 */
class HTMLDocument implements AutoCloseable {
    private final String content;

    private HTMLDocument(String html) {
        this.content = html;
    }

    public static HTMLDocument load(String path) throws IOException {
        String html = new String(Files.readAllBytes(Paths.get(path)));
        return new HTMLDocument(html);
    }

    public Body getBody() {
        // Very naive extraction of <body>...</body>
        int start = content.indexOf("<body");
        if (start == -1) return new Body("");
        start = content.indexOf('>', start) + 1;
        int end = content.indexOf("</body>", start);
        if (end == -1) end = content.length();
        return new Body(content.substring(start, end));
    }

    @Override
    public void close() {
        // No resources to free in this stub
    }

    /** Simple wrapper for body text */
    static class Body {
        private final String text;
        Body(String text) { this.text = text; }
        public String getTextContent() { return text; }
    }
}

public class HtmlThreadDemo {

    public static void main(String[] args) {
        // Step 1: Define a reusable task (how to use runnable)
        Runnable extractTextLength = () -> {
            try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
                int textLength = doc.getBody().getTextContent().length();
                // Step 4: Print thread name and length
                System.out.println(Thread.currentThread().getName() + ": " + textLength);
            } catch (Exception e) {
                e.printStackTrace();
            }
        };

        // Step 2 & 3: How to start thread and start multiple threads
        new Thread(extractTextLength, "Worker-1").start();
        new Thread(extractTextLength, "Worker-2").start();
    }
}
```

### Output yang Diharapkan

Dengan asumsi `page.html` berisi 2 567 karakter di dalam tag `<body>`-nya, Anda akan melihat sesuatu seperti:

```
Worker-1: 2567
Worker-2: 2567
```

Jika file tidak dapat dibaca, jejak stack akan dicetak—berkat blok `catch`.

## Kesalahan Umum & Tips Pro

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **File tidak ditemukan** | Path `"YOUR_DIRECTORY/page.html"` bersifat relatif terhadap lokasi Anda menjalankan JVM. | Gunakan path absolut atau `Paths.get("").toAbsolutePath()` untuk debugging. |
| **Kondisi balapan** | Jika `Runnable` mengubah state yang dibagikan, thread dapat bertabrakan. | Jaga tugas tetap stateless, atau sinkronkan akses ke objek yang dibagikan. |
| **Terlalu banyak thread** | Membuat puluhan `Thread` dapat menghabiskan sumber daya OS. | Beralih ke `ExecutorService` dengan pool terbatas setelah Anda menguasai dasar-dasarnya. |
| **Parsing HTML tidak tepat** | Stub `HTMLDocument` terlalu sederhana; halaman kompleks akan gagal. | Ganti dengan Jsoup: `Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

## Memperluas Contoh

Sekarang Anda tahu **how to start thread**, Anda mungkin ingin:

- **Parse different files** dengan memberikan nama file ke dalam `Runnable` (gunakan konstruktor atau lambda yang menangkap variabel).
- **Collect results** dengan `ConcurrentLinkedQueue<Integer>` alih-alih hanya mencetak.
- **Leverage a thread pool** (`Executors.newFixedThreadPool(4)`) untuk skalabilitas yang lebih baik.
- **Swap the parser** dengan Jsoup, HtmlUnit, atau pustaka apa pun yang sesuai dengan kebutuhan proyek Anda.

Semua langkah tersebut masih bergantung pada ide inti yang kami bahas: mendefinisikan tugas yang dapat digunakan kembali, memberikannya ke satu atau banyak thread, dan mengamati thread mana yang melakukan pekerjaan dengan **print thread name**.

## Kesimpulan

Kami telah membahas **how to start thread** di Java, mendemonstrasikan **how to use runnable** untuk pekerjaan yang dapat digunakan kembali, menunjukkan cara **start multiple threads**, dan menggambarkan cara sederhana untuk **parse HTML with Java** sambil **print thread name** untuk setiap pekerja. Potongan kode lengkap di atas siap dijalankan, dan konsepnya dapat diterapkan pada aplikasi yang lebih kompleks dan produksi.

Silakan bereksperimen: ubah path file, tingkatkan jumlah pekerja, atau sambungkan parser HTML nyata. Dasar-dasarnya tetap sama, dan kini Anda memiliki fondasi yang kuat untuk proyek Java multithread apa pun.

Ada pertanyaan tentang keamanan thread, executor service, atau pustaka parsing HTML? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}