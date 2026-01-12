---
category: general
date: 2026-01-01
description: Pelajari cara menggunakan fixed thread pool di Java untuk menghapus tag
  script dari file HTML. Contoh executorservice Java ini menunjukkan cara memuat dokumen
  HTML secara efisien.
draft: false
keywords:
- fixed thread pool java
- remove script tags
- remove javascript html
- executorservice example java
- load html document
language: id
og_description: Menguasai fixed thread pool Java untuk menghapus tag script dari file
  HTML. Contoh lengkap executorservice Java dengan langkah-langkah memuat dokumen
  HTML.
og_title: Fixed thread pool Java – Panduan Pembersihan HTML Paralel
tags:
- Java concurrency
- HTML processing
- Aspose.HTML
title: Fixed thread pool Java – Pembersihan HTML Paralel dengan ExecutorService
url: /id/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Fixed thread pool java – Pembersihan HTML Paralel dengan ExecutorService

Pernah membutuhkan **fixed thread pool java** untuk mempercepat pemrosesan HTML massal? Anda tidak sendirian. Ketika Anda memiliki puluhan—atau bahkan ratusan—file HTML yang dipenuhi elemen `<script>`, melakukan pekerjaan secara berurutan dapat terasa seperti menunggu cat mengering.  

Dalam tutorial ini kami akan menunjukkan secara tepat cara membuat **fixed thread pool java**, memuat setiap dokumen HTML, menghapus semua JavaScript (`<script>` tags), dan menyimpan file yang sudah dibersihkan—semua secara paralel menggunakan **executorservice example java**. Pada akhir tutorial Anda akan memiliki program siap‑jalankan yang menghapus tag script secara efisien, dan Anda akan memahami mengapa fixed thread pool sering menjadi pilihan tepat untuk beban kerja CPU‑bound.

## Apa yang Akan Anda Capai

- Menyiapkan `ExecutorService` dengan jumlah thread tetap.  
- Memuat file HTML menggunakan `HTMLDocument` dari Aspose.HTML.  
- Menggunakan selector CSS untuk **remove script tags** (atau elemen tidak diinginkan lainnya).  
- Menyimpan output yang sudah disanitasi dengan konvensi penamaan yang jelas.  
- Menangani shutdown dan terminasi yang elegan dari thread pool.

Tidak ada alat build eksternal, tidak ada sihir tersembunyi—hanya Java 8+ biasa dan Aspose.HTML.

---

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| **Java 8 atau lebih baru** | Diperlukan untuk ekspresi lambda dan API `ExecutorService`. |
| **Aspose.HTML for Java** (unduh dari <https://products.aspose.com/html/java/>) | Menyediakan kelas `HTMLDocument` yang digunakan untuk memuat dan memanipulasi HTML. |
| **Folder dengan contoh file HTML** | Demo memproses file seperti `input1.html`, `input2.html`, dll. |
| **IDE atau alat build baris perintah** (IntelliJ, Eclipse, Maven, Gradle) | Untuk mengompilasi dan menjalankan kode. |

Jika Anda belum menambahkan Aspose.HTML ke proyek Anda, letakkan JAR ke dalam folder `libs` dan tambahkan ke classpath, atau deklarasikan dependensi Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

---

## Langkah 1: Buat Fixed Thread Pool java

Sebuah **fixed thread pool java** memberi Anda jumlah thread pekerja yang dapat diprediksi dan tetap hidup selama seluruh pekerjaan. Ini menghindari overhead pembuatan dan penghancuran thread secara terus‑menerus, yang sangat membantu ketika setiap tugas bersifat singkat, seperti memuat dan membersihkan satu file HTML.

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;

public class ParallelProcessingDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
        // ...
    }
}
```

> **Pro tip:** Pilih ukuran pool berdasarkan jumlah core CPU (`Runtime.getRuntime().availableProcessors()`) ditambah sedikit buffer jika tugas melibatkan I/O.

---

## Langkah 2: Daftar File HTML yang Ingin Diproses

Anda dapat memindai direktori secara dinamis, tetapi demi kejelasan kami akan menuliskan array secara hard‑code. Ganti `"YOUR_DIRECTORY"` dengan path sebenarnya di mesin Anda.

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/input1.html",
    "YOUR_DIRECTORY/input2.html",
    "YOUR_DIRECTORY/input3.html",
    "YOUR_DIRECTORY/input4.html"
};
```

Jika Anda lebih suka pendekatan dinamis, `Files.list(Paths.get("YOUR_DIRECTORY"))` dapat mengisi array secara otomatis.

---

## Langkah 3: Kirim Tugas Pembersihan untuk Setiap File

Setiap file mendapatkan tugas **executorservice example java** masing‑masing. Di dalam lambda kita:

1. Membuka file dengan `HTMLDocument`.  
2. **Remove script tags** menggunakan selector CSS (`"script"`).  
3. Menyimpan versi yang sudah dibersihkan dengan akhiran `_clean.html`.

```java
for (String htmlFile : htmlFiles) {
    executor.submit(() -> {
        // Load the document (each thread works with its own instance)
        try (HTMLDocument doc = new HTMLDocument(htmlFile)) {
            // Remove all <script> elements from the document
            doc.querySelectorAll("script")
               .forEach(node -> node.getParentNode().removeChild(node));

            // Save the cleaned document with a new name
            doc.save(htmlFile.replace(".html", "_clean.html"));
        } catch (Exception e) {
            System.err.println("Failed to process " + htmlFile + ": " + e.getMessage());
        }
    });
}
```

> **Mengapa ini berhasil:** `querySelectorAll("script")` mengembalikan koleksi live dari setiap elemen `<script>`. Loop `forEach` kemudian memisahkan setiap node dari parent‑nya, secara efektif **remove javascript html** dari sumber.

---

## Langkah 4: Matikan Pool dan Tunggu Penyelesaian

Terminasi yang elegan sangat penting; Anda tidak ingin thread yang tersisa berkeliaran setelah pekerjaan selesai.

```java
// Step 4: Shut down the pool and wait for all tasks to finish
executor.shutdown();
if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
    System.err.println("Some tasks did not finish within the timeout.");
    executor.shutdownNow(); // Force shutdown if needed
}
System.out.println("All HTML files have been cleaned.");
```

Jika Anda memiliki banyak file atau dokumen besar, tingkatkan timeout ke nilai yang lebih besar.

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang dapat Anda salin‑tempel ke dalam `ParallelProcessingDemo.java` dan jalankan.

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelProcessingDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ List the HTML files to be processed
        String[] htmlFiles = {
            "YOUR_DIRECTORY/input1.html",
            "YOUR_DIRECTORY/input2.html",
            "YOUR_DIRECTORY/input3.html",
            "YOUR_DIRECTORY/input4.html"
        };

        // 3️⃣ Submit a cleaning task for each file
        for (String htmlFile : htmlFiles) {
            executor.submit(() -> {
                try (HTMLDocument doc = new HTMLDocument(htmlFile)) {
                    // 🌟 Remove all <script> elements (remove script tags)
                    doc.querySelectorAll("script")
                       .forEach(node -> node.getParentNode().removeChild(node));

                    // Save cleaned version
                    doc.save(htmlFile.replace(".html", "_clean.html"));
                } catch (Exception e) {
                    System.err.println("Error processing " + htmlFile + ": " + e.getMessage());
                }
            });
        }

        // 4️⃣ Shut down the pool and wait for completion
        executor.shutdown();
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            System.err.println("Timeout reached before all tasks finished.");
            executor.shutdownNow();
        } else {
            System.out.println("All files cleaned successfully!");
        }
    }
}
```

### Output yang Diharapkan

Saat Anda menjalankan program, Anda akan melihat pesan konsol seperti:

```
All files cleaned successfully!
```

Dan di direktori Anda akan menemukan:

- `input1_clean.html`
- `input2_clean.html`
- `input3_clean.html`
- `input4_clean.html`

Setiap file `_clean.html` akan identik dengan file aslinya, kecuali tanpa blok `<script>` apa pun.

---

## Pertanyaan yang Sering Diajukan (FAQ)

**T: Bisakah saya mengubah ukuran thread pool saat runtime?**  
J: Ya. Gunakan `Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() + 1)` untuk ukuran dinamis berdasarkan mesin host.

**T: Bagaimana jika file HTML saya mengandung handler inline (`onclick`, `onload`)?**  
J: Selector saat ini hanya menghapus tag `<script>`. Untuk menghapus handler inline, Anda perlu menelusuri semua elemen dan membersihkan atribut yang dimulai dengan `on`. Itu merupakan ekstensi yang baik untuk tutorial selanjutnya.

**T: Apakah Aspose.HTML satu‑satunya library yang mendukung `querySelectorAll`?**  
J: Tidak. Library seperti jsoup juga menawarkan selector CSS, tetapi Aspose.HTML memberikan API DOM lengkap yang meniru perilaku browser, sangat berguna untuk tugas pembersihan yang kompleks.

**T: Bagaimana cara menangani file HTML yang sangat besar sehingga mungkin tidak muat di memori?**  
J: Untuk file masif, pertimbangkan parser streaming (misalnya Saxon untuk XML) atau proses file dalam potongan. Pola fixed thread pool tetap berlaku; Anda hanya mengganti `HTMLDocument` dengan solusi streaming.

---

## Langkah Selanjutnya & Topik Terkait

- **Remove JavaScript HTML dengan jsoup** – alternatif ringan jika Anda tidak memerlukan dukungan DOM penuh.  
- **Dynamic thread pool sizing** – jelajahi `ThreadPoolExecutor` untuk kontrol yang lebih halus.  
- **Batch processing dengan `CompletableFuture`** – gabungkan futures untuk pipeline yang lebih kaya.  
- **Sanitisasi HTML di luar script** – hapus style, iframe, atau atribut tidak aman.  

Semua ini dibangun di atas fondasi **executorservice example java** yang sama yang telah kami paparkan di sini.

---

## Kesimpulan

Anda kini memiliki contoh solid, siap produksi tentang cara menggunakan **fixed thread pool java** untuk **remove script tags** dari sekumpulan file HTML. Dengan memanfaatkan `ExecutorService`, setiap file diproses secara paralel, secara dramatis mengurangi total waktu eksekusi. Pendekatan ini modular, mudah diperluas, dan bekerja dengan library HTML kompatibel Java apa pun yang menyediakan kemampuan `load html document`.

Cobalah, sesuaikan ukuran pool, atau tambahkan aturan pembersihan ekstra—petualangan pemrosesan HTML berikutnya hanya beberapa baris kode lagi.

---

![Ilustrasi Fixed thread pool java](https://example.com/fixed-thread-pool-java.png "Fixed thread pool java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}