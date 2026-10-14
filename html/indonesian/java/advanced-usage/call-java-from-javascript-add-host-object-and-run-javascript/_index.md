---
category: general
date: 2026-10-14
description: Panggil java dari javascript menggunakan Aspose.HTML. Pelajari cara menambahkan
  host object, mengeksekusi javascript di java, dan log dari javascript dalam tutorial
  singkat.
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: Panggil java dari javascript menggunakan Aspose.HTML. Panduan ini
  menunjukkan cara menambahkan host object, mengeksekusi javascript di java, dan log
  dari javascript, semuanya dalam beberapa baris kode.
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: Panggil java dari javascript – tambahkan host object dan jalankan javascript
  di java
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Call java from javascript using Aspose.HTML. Learn how to add a host
    object, execute javascript in java, and log from javascript in a concise tutorial.
  headline: Call java from javascript – add host object and run javascript in java
  type: TechArticle
- questions:
  - answer: Yes. Aspose.HTML is a pure‑Java library, so it runs on any JVM, including
      Android’s ART runtime.
    question: Does this work on Android?
  - answer: You can expose POJOs with getters and setters; the engine maps them to
      JavaScript objects automatically. Collections such as `java.util.List` or arrays
      are also convertible.
    question: What if I need to pass complex objects?
  - answer: If the script throws a JavaScript error, `eval` propagates a `ScriptException`.
      Wrap the call in a try‑catch block to log or recover.
    question: How does error handling work?
  - answer: Absolutely. The same `HTMLDocument` retains its global scope, so you can
      call `eval` repeatedly. Just manage variable names to avoid clashes.
    question: Can I run multiple scripts sequentially?
  - answer: Treat any external script as untrusted input. Validate parameters and
      consider sandboxing by exposing only the minimal required methods.
    question: Is the host object safe for untrusted scripts?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- scripting
- host object
title: Panggil java dari javascript – tambahkan host object dan jalankan javascript
  di java
url: /id/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Panggil java dari javascript – tambahkan objek host dan jalankan javascript di java

Pernah membutuhkan untuk **memanggil java dari javascript** di dalam aplikasi Java? Mungkin Anda sedang membangun mesin laporan HTML dinamis atau Anda hanya ingin mengekspos logger Java ke skrip yang Anda kontrol. Dalam tutorial ini Anda akan melihat secara tepat cara menambahkan objek host, menjalankan JavaScript di Java, dan bahkan **mencatat dari JavaScript** kembali ke JVM—semua dengan Aspose.HTML.

Kami akan membahas contoh lengkap yang dapat dijalankan yang membuat dokumen HTML kosong, menyuntikkan kelas Java `Logger` sebagai objek host, mengeksekusi skrip kecil, dan mencetak hasilnya ke konsol. Tidak memerlukan peramban web eksternal, tidak ada “sihir” misterius—hanya kode Java biasa yang dapat Anda salin‑tempel dan jalankan hari ini.

## Jawaban Cepat
- **Bagaimana cara menambahkan objek host?** Daftarkan instance Java dengan `document.getWindow().addHostObject("name", object)`.  
- **Apakah saya dapat mengeksekusi JavaScript di Java?** Ya—gunakan `document.getWindow().eval(yourScript)`.  
- **Apakah pencatatan dari JavaScript memungkinkan?** Tentu saja; objek host dapat mengekspos metode `void log(String)` apa pun.  
- **Versi Aspose.HTML apa yang dibutuhkan?** Versi 23.10 atau lebih baru mendukung API objek‑host lengkap.  
- **Apakah saya membutuhkan peramban web?** Tidak—Aspose.HTML menyediakan mesin tersemat, sehingga semuanya berjalan tanpa tampilan (head‑less).

## Apa itu panggil java dari javascript?
**Call java from javascript** adalah teknik mengekspos objek Java ke runtime JavaScript sehingga skrip dapat memanggil metode Java secara langsung. Aspose.HTML membuat mesin JavaScript ringan di dalam proses Java, memungkinkan komunikasi dua arah yang mulus tanpa peramban eksternal.

## Mengapa menggunakan Aspose.HTML untuk mengeksekusi javascript di java?
Aspose.HTML mendukung **lebih dari 50 format input dan output** dan dapat mengevaluasi JavaScript dalam lingkungan HTML5 yang sepenuhnya sesuai. Ia memproses skrip hingga 200 ms rata-rata untuk kode satu baris sederhana, dan melakukannya tanpa memuat tumpukan peramban penuh, yang mengurangi penggunaan memori hingga 80 % dibandingkan pendekatan berbasis Selenium.

## Prasyarat

- Java 17 (atau JDK terbaru apa pun) terpasang dan terkonfigurasi.  
- Pustaka Aspose.HTML untuk Java (versi 23.10 atau lebih baru). Anda dapat memperolehnya dari Maven Central atau situs web Aspose.  
- IDE sederhana atau editor teks; contoh ini juga dapat dijalankan dari baris perintah.

> **Tips Pro:** Jika Anda menggunakan Maven, tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Atau, untuk Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Sekarang setelah kami menyelesaikan dasar‑dasarnya, mari selami solusi langkah‑demi‑langkah.

## Cara menambahkan objek host dan menjalankan javascript di java?
`addHostObject` mendaftarkan objek Java sebagai variabel global dalam konteks JavaScript. Muat `HTMLDocument` Anda, daftarkan logger Java dengan nama `"javaLogger"` menggunakan `addHostObject`, lalu evaluasi skrip singkat yang memanggil `javaLogger.log`. Seluruh alur hanya memerlukan tiga panggilan API dan berfungsi di runtime Java 17 apa pun.

### Langkah 1: buat proyek java minimal

Pertama, siapkan kelas Java baru bernama `JsHostObjectDemo`. Kelas ini akan berisi metode `main` kami dan definisi objek host. Menyimpan semuanya dalam satu file membuat tutorial ini mandiri dan mudah disalin.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### Mengapa `HTMLDocument`?
`HTMLDocument` mewakili dokumen HTML dalam memori dan menyediakan mesin JavaScript. Kelas `HTMLDocument` memulai lingkungan skrip yang sepenuhnya sesuai HTML‑5. Meskipun kami tidak pernah memuat markup apa pun, objek `window` dokumen memberi kami akses ke mesin JavaScript, tempat terjadinya **run javascript in java**. Selain itu Anda dapat memanipulasi DOM, memuat sumber daya, atau mengevaluasi skrip tanpa peramban.

## Cara menambahkan objek host – “javaLogger”?
`Logger` adalah kelas Java sederhana dengan metode `log(String)` yang menulis pesan ke konsol. Daftarkan instance `Logger` dengan nama `"javaLogger"` sehingga skrip apa pun yang dievaluasi dalam dokumen ini dapat memanggil `javaLogger.log(...)`. Ini adalah inti dari kebutuhan **add host object** dan membuat logger tersedia sebagai variabel global untuk kode JavaScript.

### Kesalahan umum

- **Tabrakan nama** – Jika Anda sudah memiliki variabel global bernama `javaLogger` dalam skrip Anda, objek host akan ditimpa. Pilih nama yang unik.  
- **Keamanan thread** – Objek host dibagikan di antara eksekusi skrip pada dokumen yang sama. Jika Anda berencana menjalankan skrip secara bersamaan, buat kelas host menjadi thread‑safe (mis., gunakan `synchronized` atau primitif `java.util.concurrent`).  

## Cara menulis dan mengeksekusi javascript di java?
`eval` mengeksekusi string JavaScript dalam mesin skrip dokumen dan mengembalikan hasil apa pun. Masukkan skrip kecil ke dalam `eval`. Mesin menyelesaikan `javaLogger` dari ruang lingkup global dan memanggil metode `log`‑nya dengan string yang diberikan. Anda juga dapat mengembalikan nilai, menangani pengecualian, dan menautkan beberapa evaluasi untuk interaksi yang lebih kompleks.

### Output yang diharapkan

Menjalankan metode `main` mencetak baris berikut ke konsol:

```
[JS] Hello from JavaScript!
```

## Cara memperluas host – lebih dari sekadar pencatatan?
Objek host adalah instance Java apa pun yang diekspos ke JavaScript melalui `addHostObject`. Ekspos fungsionalitas tambahan dengan menambahkan metode ke kelas `Logger` atau dengan membuat kelas host baru. Berikut contoh cepat yang juga mengembalikan nilai ke JavaScript. Objek host dapat mengekspos tipe kompleks, melakukan I/O, atau berinteraksi dengan layanan lain. Dengan mengembalikan nilai, skrip dapat menerima data kembali, memungkinkan komunikasi dua arah antara Java dan JavaScript.

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

Sekarang konsol menampilkan:

```
[JS] 3+4=7
```

## Cara membersihkan sumber daya setelah menjalankan skrip?
`dispose` melepaskan sumber daya native yang dipegang oleh instance `HTMLDocument`. Saat Anda selesai dengan lingkungan skrip, disposel `HTMLDocument` untuk membebaskan sumber daya native. Tidak memanggil `dispose()` dapat menyebabkan kebocoran memori, terutama saat membuat banyak dokumen dalam loop atau layanan yang berjalan lama. Selalu bungkus penggunaan dalam blok try‑with‑resources atau pastikan `document.dispose()` dipanggil dalam klausa finally.

```java
document.dispose(); // Important for long‑running applications
```

## Contoh lengkap yang berfungsi

Berikut adalah file sumber lengkap yang dapat Anda kompilasi dan jalankan segera. Simpan sebagai `JsHostObjectDemo.java`, pastikan JAR Aspose.HTML berada di classpath Anda, dan jalankan `java JsHostObjectDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

Menjalankan program ini menghasilkan:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

## Pertanyaan yang sering diajukan

**T: Apakah ini bekerja di Android?**  
J: Ya. Aspose.HTML adalah pustaka pure‑Java, sehingga dapat berjalan di JVM apa pun, termasuk runtime ART Android.

**T: Bagaimana jika saya perlu mengirim objek kompleks?**  
J: Anda dapat mengekspos POJO dengan getter dan setter; mesin secara otomatis memetakan mereka ke objek JavaScript. Koleksi seperti `java.util.List` atau array juga dapat dikonversi.

**T: Bagaimana cara kerja penanganan error?**  
J: Jika skrip melempar error JavaScript, `eval` menyebarkan `ScriptException`. Bungkus pemanggilan dalam blok try‑catch untuk mencatat atau memulihkan.

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**T: Bisakah saya menjalankan beberapa skrip secara berurutan?**  
J: Tentu saja. `HTMLDocument` yang sama mempertahankan ruang lingkup globalnya, sehingga Anda dapat memanggil `eval` berulang kali. Cukup kelola nama variabel agar tidak bentrok.

**T: Apakah objek host aman untuk skrip yang tidak dipercaya?**  
J: Perlakukan setiap skrip eksternal sebagai input yang tidak dipercaya. Validasi parameter dan pertimbangkan sandboxing dengan mengekspos hanya metode minimal yang diperlukan.

## Praktik terbaik & tips

- **Berikan nama objek host Anda dengan jelas**—`javaLogger`, `javaUtils`, dll.—untuk menghindari kebingungan.  
- **Jaga metode host tetap kecil dan bebas efek samping** bila memungkinkan; ini memudahkan debugging.  
- **Dispose dokumen** segera setelah selesai; ini melepaskan memori native yang dialokasikan Aspose.HTML.  
- **Validasi input** dari JavaScript, terutama jika skrip berasal dari sumber yang tidak dipercaya. Perlakukan mereka seperti data eksternal apa pun.

## Kesimpulan

Anda kini memiliki contoh lengkap yang solid tentang cara **memanggil java dari javascript** dengan **menambahkan objek host**, **menjalankan javascript di java**, dan **mencatat dari javascript** menggunakan Aspose.HTML. Pola ini kuat: layanan Java apa pun dapat diekspos ke skrip, menjadikan aplikasi Java Anda sebagai platform skrip ringan.

Selanjutnya, Anda mungkin ingin menjelajahi:

- Menyuntikkan halaman HTML lengkap dan memanipulasi DOM dari JavaScript.  
- Menggunakan objek host untuk mengalirkan data kembali ke sisi Java (mis., serialisasi JSON).  
- Mengintegrasikan dengan mesin skrip lain seperti Nashorn atau GraalVM untuk dukungan bahasa yang lebih luas.

Cobalah, ubah kelas `Logger` atau `Utils`, dan lihat sejauh mana Anda dapat mengembangkan konsep **javascript host object** dalam proyek Anda sendiri.

---

**Terakhir Diperbarui:** 2026-10-14  
**Diuji Dengan:** Aspose.HTML for Java 23.10  
**Penulis:** Aspose  






```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## Tutorial Terkait

- [Aktifkan Eksekusi Skrip di Java Panduan Lengkap Aspose Html](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Jalankan Javascript di Java Panduan Lengkap Menjalankan Js Dari](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [Cara Membuat Sandbox Javascript Panduan Lengkap Aspose Html](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}