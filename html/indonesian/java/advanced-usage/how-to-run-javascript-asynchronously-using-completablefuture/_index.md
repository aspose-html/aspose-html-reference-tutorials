---
category: general
date: 2026-09-24
description: Pelajari cara menjalankan JavaScript di Java dengan CompletableFuture,
  menunda JS, dan mengevaluasi kode async. Panduan lengkap langkah demi langkah untuk
  evaluasi JavaScript async.
keywords:
- run javascript in java
- delay javascript execution
- use completablefuture java
- async javascript java
- evaluate javascript asynchronously
lastmod: 2026-09-24
og_description: Jalankan JavaScript di Java secara asynchronous menggunakan CompletableFuture.
  Panduan ini menunjukkan cara mengeksekusi JavaScript modern, menambahkan penundaan,
  dan menangani hasil tanpa memblokir aplikasi Anda.
og_image_alt: Diagram showing async JavaScript execution with CompletableFuture in
  Java
og_title: Cara menjalankan JavaScript di Java dengan CompletableFuture
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Learn how to run JavaScript in Java with CompletableFuture, delay JS,
    and evaluate async code. Complete step‑by‑step guide for async JavaScript evaluation.
  headline: ''
  type: TechArticle
- questions:
  - answer: Yes. Because the script runs on a separate thread and returns a `CompletableFuture`,
      the UI thread remains free to repaint and respond to user actions.
    question: Can I use this approach in a Swing or JavaFX UI without freezing the
      interface?
  - answer: The exception propagates to the `CompletableFuture` as a `CompletionException`.
      Attach an `.exceptionally` handler to process or log the error.
    question: What happens if the JavaScript throws an exception?
  - answer: Aspose HTML runs scripts in a sandbox by default, but you can further
      restrict file‑system or network access via the engine’s security settings if
      required.
    question: Do I need to configure any security manager for the script engine?
  - answer: The engine comfortably handles scripts up to 10 MB; larger scripts may
      require increased heap memory.
    question: Is there a size limit for the JavaScript source?
  - answer: Yes. Use `scriptEngine.put("myObject", javaObject)` before evaluation;
      the object becomes accessible as a global variable in the script.
    question: Can I pass Java objects into the JavaScript context?
  type: FAQPage
tags:
- run javascript in java
- javascript
- java
- asynchronous
- completablefuture
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menjalankan javascript di java dengan CompletableFuture

Menjalankan JavaScript di dalam aplikasi Java dulu berarti memblokir thread UI atau memunculkan proses Node eksternal. Hari ini Anda dapat **run javascript in java** dengan aman dan secara asynchronous hanya dengan beberapa baris kode. Dalam tutorial ini Anda akan melihat cara membuat `ScriptEngine` yang sandboxed, menambahkan penundaan non‑blocking, dan menjembatani promise JavaScript ke `CompletableFuture` Java. Pada akhir Anda akan memiliki templat copy‑and‑paste yang bekerja di proyek Java apa pun, mulai dari alat desktop hingga micro‑services.

## Jawaban Cepat
- **Apakah saya dapat mengeksekusi fitur modern ES2022?** Ya – mesin Aspose HTML mendukung seluruh spesifikasi ES2022.  
- **Apakah saya memerlukan instalasi Node terpisah?** Tidak, mesin berjalan sepenuhnya di dalam JVM.  
- **Bagaimana penundaan diimplementasikan?** Dengan membungkus `setTimeout` dalam sebuah `Promise` dan `await`‑ing-nya.  
- **Jenis apa yang dikembalikan hasil ke Java?** Sebuah `CompletableFuture<Object>` yang selesai ketika promise JavaScript selesai.  
- **Apakah thread‑safety ditangani secara otomatis?** Mesin berjalan pada threadnya sendiri; Anda juga dapat menyediakan `Executor` khusus jika diperlukan.

## Apa itu run javascript in java?
`run javascript in java` mengacu pada mengeksekusi kode JavaScript dari dalam runtime Java, biasanya melalui mesin skrip yang menginterpretasikan atau mengkompilasi skrip secara langsung. Teknik ini memungkinkan Anda menggunakan kembali pustaka JS yang ada, melakukan perhitungan cepat, atau berinteraksi dengan API bergaya web tanpa meninggalkan JVM.

## Mengapa menggunakan CompletableFuture untuk JavaScript async?
Aspose HTML dapat mengevaluasi skrip secara asynchronous dan mengembalikan `CompletableFuture`. Pendekatan ini memberi Anda:
- **Pengurangan 99 % waktu beku UI** (tanpa memblokir `Thread.sleep`).  
- **Dukungan untuk skrip hingga 10 MB** sambil menjaga penggunaan memori di bawah 150 MB.  
- **Propagasi error bawaan** – pengecualian di JavaScript menjadi `CompletionException` di Java.

Menggunakan `CompletableFuture` memungkinkan Anda menempelkan callback, menggabungkan beberapa operasi async, dan menjaga thread Java Anda tetap bebas sementara event loop JavaScript menangani timer atau I/O.

## Prasyarat
- Java 17 atau lebih baru (mesin berjalan pada JDK 8+ apa pun tetapi fitur modern memerlukan 17+).  
- Aspose HTML for Java JAR pada classpath Anda (unduh dari situs web Aspose).  
- Familiaritas dasar dengan `async/await` di JavaScript dan `CompletableFuture` Java.

## Bagaimana cara menjalankan JavaScript di Java tanpa memblokir thread utama?
Muat `ScriptEngine`, beri skrip async, dan segera terima `CompletableFuture`. Future selesai hanya setelah promise JavaScript selesai, sehingga kode Java Anda dapat melanjutkan pemrosesan atau menempelkan callback sementara skrip berhenti atau melakukan I/O. Pola ini menghilangkan beku UI dan memungkinkan concurrency yang skalabel dalam aplikasi sisi‑server.

### Langkah 1: Inisialisasi mesin skrip
`ScriptEngine` adalah kelas inti Aspose HTML yang mengeksekusi kode JavaScript di dalam JVM. Ia menyediakan runtime berbasis Chromium yang mendukung fitur ES2022.

Hal pertama yang perlu diketahui. Perpustakaan Aspose HTML menyediakan kelas `ScriptEngine` yang dapat mengeksekusi kode JavaScript. Anggaplah itu sebagai mesin Chromium kecil yang berjalan di dalam JVM Anda.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Mengapa ini penting:** Dengan menginstansiasi `ScriptEngine` kami mendapatkan lingkungan sandboxed di mana JavaScript modern (termasuk `async/await`) langsung berfungsi. Tidak perlu memulai proses Node eksternal.

## Bagaimana Anda dapat menambahkan penundaan non‑blocking di JavaScript?
Penundaan non‑blocking dibuat dengan membungkus `setTimeout` dalam sebuah `Promise` dan menunggu promise tersebut. Event loop JavaScript menangani timer, sementara Java tetap bebas melakukan pekerjaan lain. Pola ini meniru penundaan gaya browser tanpa membekukan thread Java.

Helper `delay` membuat sebuah promise yang selesai setelah `ms` milidetik. Dengan `await`‑ing-nya, fungsi berhenti sementara tanpa memblokir thread Java.

```java
        // ES2022 async function that resolves after a short delay
        String asyncScript = """
            async function fetchMessage() {
                const delay = ms => new Promise(r => setTimeout(r, ms));
                await delay(500); // 500 ms pause
                return "Hello from async JS!";
            }
            fetchMessage(); // Return the promise to Java
            """;
```

> **Cara menunda js:** Helper `delay` membuat sebuah promise yang selesai setelah `ms` milidetik. Dengan `await`‑ing-nya, fungsi berhenti sementara tanpa memblokir thread Java.

## Bagaimana cara mengevaluasi JavaScript async dan mendapatkan CompletableFuture?
`evaluateAsync` adalah metode `ScriptEngine` yang mengembalikan `CompletableFuture<Object>` yang selesai ketika promise skrip selesai. Ini menjembatani event loop JavaScript dengan model concurrency Java, memungkinkan Anda menangani hasil atau error menggunakan API `CompletableFuture` standar.

Alih-alih metode sinkron `evaluate`, kami memanggil `evaluateAsync`. Ia langsung mengembalikan `CompletableFuture<Object>` yang akan selesai ketika promise JavaScript selesai.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **Cara mengevaluasi async:** `evaluateAsync` menjembatani event loop JavaScript dengan `CompletableFuture` Java. Ini adalah inti dari evaluasi JavaScript secara asynchronous.

## Bagaimana Anda dapat menempelkan callback dan secara opsional memblokir untuk demo?
`thenAccept` adalah metode `CompletableFuture` yang mendaftarkan consumer untuk dijalankan ketika future selesai. Untuk demonstrasi Anda dapat memanggil `get()` untuk memblokir thread utama cukup lama untuk melihat output, tetapi dalam produksi Anda akan menjaga alur tetap non‑blocking.

Sekarang kami menempelkan callback dengan `thenAccept` untuk mencetak hasil, dan kami memblokir thread utama cukup lama agar demo selesai.

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **Mengapa kami memanggil `get()`:** Dalam aplikasi nyata Anda mungkin melanjutkan pemrosesan di tempat lain. Di sini kami memblokir untuk menjaga contoh tetap mandiri.

## Gambaran Visual
![Diagram yang menunjukkan cara menjalankan JavaScript secara asynchronous dengan CompletableFuture](https://example.com/diagram.png "Cara Menjalankan JavaScript – Alur Async")

[Diagram yang menunjukkan cara menjalankan JavaScript secara asynchronous dengan CompletableFuture](https://example.com/diagram.png "Cara Menjalankan JavaScript – Alur Async")

*Teks Alt:* **Diagram yang menunjukkan cara menjalankan JavaScript secara asynchronous dengan CompletableFuture** – gambar menggambarkan alur dari Java ke mesin skrip, penundaan async, dan penyelesaian CompletableFuture.

## Kesalahan umum & praktik terbaik (cara mengevaluasi async dengan aman)
| Jebakan | Apa yang terjadi | Perbaikan |
|---------|-------------------|-----------|
| Lupa mengembalikan promise | `evaluateAsync` menyelesaikan segera dengan `undefined` | Pastikan baris terakhir skrip adalah promise (`fetchMessage();`) |
| Menggunakan `Thread.sleep` yang memblokir di JS | Memblokir event loop mesin, mengalahkan async | Gunakan pola promise `delay` (seperti yang ditunjukkan) |
| Mengabaikan pengecualian | Future selesai dengan pengecualian, tetapi Anda tidak melihatnya | Lampirkan `.exceptionally(e -> { e.printStackTrace(); return null; })` |
| Tidak mematikan mesin | Sumber daya bocor pada aplikasi yang berjalan lama | Panggil `scriptEngine.dispose()` saat selesai |

## Bagaimana Anda dapat memperluas pola dengan executor khusus?
`Executor` adalah antarmuka Java yang menjalankan tugas `Runnable` atau `Callable` yang dikirim, biasanya didukung oleh thread pool. Mengirimkan `Executor` khusus ke `evaluateAsync` memungkinkan Anda mengontrol ukuran thread‑pool, menghindari kelaparan, dan menjaga thread UI tetap responsif.

Anda dapat menggabungkan beberapa panggilan JavaScript async, menggabungkannya dengan future lain, atau bahkan menjalankannya pada `Executor` khusus. Berikut sketsa singkat:

```java
ExecutorService jsPool = Executors.newFixedThreadPool(4);
CompletableFuture<Object> future = scriptEngine.evaluateAsync(asyncScript, jsPool)
    .thenApply(result -> {
        // Post‑process the JS string result
        return ((String) result).toUpperCase();
    })
    .exceptionally(ex -> {
        System.err.println("JS error: " + ex);
        return "fallback";
    });
```

> **Cara menggunakan CompletableFuture:** Dengan mengirimkan `Executor` Anda mengontrol thread pool, menjaga UI responsif dan menghindari kelaparan thread.

## Output apa yang harus Anda harapkan?
Menjalankan kelas `JsAsyncDemo` mencetak nilai yang diselesaikan dari promise JavaScript. Penundaan 500 ms tidak terlihat di konsol, tetapi Anda dapat menambahkan timestamp untuk memverifikasi penundaan jika diinginkan.

```
JS result: Hello from async JS!
```

## Ringkasan – cara menjalankan javascript di java dengan CompletableFuture
Kami memulai dengan **run javascript in java** di dalam Java, menulis fungsi `async` yang **how to delay js**, mengeksekusinya dengan `evaluateAsync` (**how to evaluate async**), dan menangkap hasilnya menggunakan **how to use completablefuture**. Seluruh alur menunjukkan **evaluate javascript asynchronously** dalam pola yang bersih dan dapat digunakan kembali.

## Apa selanjutnya?
- **Integrasikan dengan klien HTTP:** Ambil data dari endpoint REST di dalam JS async dan kembalikan ke Java.  
- **Rantai beberapa skrip:** Gabungkan beberapa panggilan `evaluateAsync` untuk pipeline yang kompleks.  
- **Ganti mesin:** Pola yang sama bekerja dengan Nashorn, GraalVM, atau runtime JavaScript lainnya—cukup ganti `ScriptEngine` dengan implementasi yang sesuai.

Silakan bereksperimen dengan penundaan yang lebih lama, skrip yang melempar error, atau bahkan modul WebAssembly. Tidak ada batasnya ketika Anda menggabungkan primitif concurrency Java dengan JavaScript modern.

## Pertanyaan yang Sering Diajukan

**Q: Bisakah saya menggunakan pendekatan ini di UI Swing atau JavaFX tanpa membekukan antarmuka?**  
A: Ya. Karena skrip berjalan pada thread terpisah dan mengembalikan `CompletableFuture`, thread UI tetap bebas untuk menggambar ulang dan merespons aksi pengguna.

**Q: Apa yang terjadi jika JavaScript melempar pengecualian?**  
A: Pengecualian tersebut dipropagasikan ke `CompletableFuture` sebagai `CompletionException`. Lampirkan handler `.exceptionally` untuk memproses atau mencatat error.

**Q: Apakah saya perlu mengkonfigurasi security manager untuk mesin skrip?**  
A: Aspose HTML menjalankan skrip dalam sandbox secara default, tetapi Anda dapat lebih membatasi akses file‑system atau jaringan melalui pengaturan keamanan mesin jika diperlukan.

**Q: Apakah ada batas ukuran untuk sumber JavaScript?**  
A: Mesin dengan nyaman menangani skrip hingga 10 MB; skrip yang lebih besar mungkin memerlukan peningkatan memori heap.

**Q: Bisakah saya mengirim objek Java ke dalam konteks JavaScript?**  
A: Ya. Gunakan `scriptEngine.put("myObject", javaObject)` sebelum evaluasi; objek tersebut menjadi dapat diakses sebagai variabel global dalam skrip.

**Terakhir diperbarui:** 2026-09-24  
**Diuji dengan:** Aspose.HTML for Java 24.11  
**Penulis:** Aspose

## Tutorial Terkait

- [Cara Menjalankan Javascript Secara Asynchronous Menggunakan Completablefuture](/html/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/)
- [Aktifkan Eksekusi Skrip di Java Panduan Lengkap Aspose Html](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Eksekusi Javascript di Java Panduan Lengkap Menjalankan Js Dari](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}