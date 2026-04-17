---
category: general
date: 2026-03-14
description: Pelajari cara memanggil Java dari JavaScript menggunakan Aspose.HTML.
  Panduan ini menunjukkan cara menambahkan objek host, menjalankan JavaScript di Java,
  dan mencatat dari JavaScript.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: id
og_description: Panggil Java dari JavaScript menggunakan Aspose.HTML. Tambahkan objek
  host, jalankan JavaScript di Java, dan catat log dari JavaScript dalam satu tutorial.
og_title: Panggil Java dari JavaScript – Panduan Lengkap dengan Objek Host
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: Panggil Java dari JavaScript – Tambahkan Objek Host dan Jalankan JavaScript
  di Java
url: /id/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

content with same structure.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Call Java from JavaScript – Add Host Object and Run JavaScript in Java

Pernahkah Anda perlu **memanggil Java dari JavaScript** di dalam aplikasi Java? Mungkin Anda sedang membangun mesin laporan HTML dinamis atau Anda hanya ingin mengekspos logger Java ke skrip yang Anda kontrol. Dalam tutorial ini Anda akan melihat secara tepat cara menambahkan host object, menjalankan JavaScript di Java, dan bahkan **mencatat dari JavaScript** kembali ke JVM—semua dengan Aspose.HTML.

Kami akan membahas contoh lengkap yang dapat dijalankan yang membuat dokumen HTML kosong, menyuntikkan kelas Java `Logger` sebagai host object, mengeksekusi skrip kecil, dan mencetak hasilnya ke konsol. Tidak diperlukan peramban web eksternal, tidak ada “sihir” misterius—hanya kode Java biasa yang dapat Anda salin‑tempel dan jalankan hari ini.

## Prasyarat

- Java 17 (atau JDK terbaru) terpasang dan terkonfigurasi.
- Perpustakaan Aspose.HTML untuk Java (versi 23.10 atau lebih baru). Anda dapat memperolehnya dari Maven Central atau situs web Aspose.
- IDE atau editor teks sederhana; contoh ini juga dapat dijalankan dari baris perintah.

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

Sekarang setelah dasar‑dasarnya sudah beres, mari kita selami solusi langkah‑demi‑langkah.

## Langkah 1: Buat Proyek Java Minimal

Pertama, siapkan kelas Java baru bernama `JsHostObjectDemo`. Kelas ini akan berisi metode `main` kami dan definisi host object. Menyimpan semuanya dalam satu file membuat tutorial ini mandiri dan mudah disalin.

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

Kelas `HTMLDocument` milik Aspose.HTML memulai lingkungan skrip yang sepenuhnya mematuhi HTML‑5. Meskipun kami tidak pernah memuat markup apa pun, objek `window` pada dokumen memberikan akses ke mesin JavaScript, tempat terjadinya keajaiban **menjalankan JavaScript di Java**.

## Langkah 2: Tambahkan Host Object – “javaLogger”

Baris

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

melakukan pekerjaan berat untuk kebutuhan **menambahkan host object**. Dengan mendaftarkan instance `Logger` dengan nama `"javaLogger"`, skrip apa pun yang dievaluasi dalam dokumen ini dapat memanggil `javaLogger.log(...)`. Ini adalah inti dari konsep **javascript host object**: sebuah jembatan yang memungkinkan JavaScript mengakses JVM.

### Kesalahan Umum

- **Tabrakan nama** – Jika Anda sudah memiliki variabel global bernama `javaLogger` dalam skrip Anda, host object akan ditimpa. Pilih nama yang unik.
- **Keamanan thread** – Host object dibagikan di antara eksekusi skrip pada dokumen yang sama. Jika Anda berencana menjalankan skrip secara bersamaan, buat kelas host menjadi thread‑safe (misalnya, gunakan `synchronized` atau primitif `java.util.concurrent`).

## Langkah 3: Tulis dan Jalankan JavaScript

Skrip yang kami masukkan ke dalam `eval` sengaja sangat kecil:

```javascript
javaLogger.log('Hello from JavaScript!');
```

Ketika `document.getWindow().eval(script)` dijalankan, mesin mencari `javaLogger` dalam ruang lingkup globalnya, menemukan objek Java yang kami tambahkan, dan memanggil metode `log`-nya dengan string yang diberikan.

### Output yang Diharapkan

Menjalankan metode `main` mencetak baris berikut ke konsol:

```
[JS] Hello from JavaScript!
```

Baris kecil itu membuktikan bahwa kami berhasil **memanggil java dari javascript**, dan **log dari javascript** muncul persis di tempat pesan `System.out` Java biasa akan tampil.

## Langkah 4: Memperluas Host – Lebih dari Sekadar Logging

Jika Anda perlu mengekspos fungsionalitas tambahan (misalnya, akses file, kueri basis data), cukup tambahkan lebih banyak metode ke kelas `Logger`—atau buat kelas host baru. Berikut contoh singkat yang juga mengembalikan nilai:

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

Ini menunjukkan fleksibilitas pola **javascript host object**: Anda dapat mengekspos API Java apa pun yang Anda butuhkan, selama tipe data dapat dikonversi antara Java dan JavaScript (primitif, string, array, dll.).

## Langkah 5: Bersihkan Sumber Daya

Setelah selesai dengan lingkungan skrip, buang (`dispose`) `HTMLDocument` untuk membebaskan sumber daya native:

```java
document.dispose(); // Important for long‑running applications
```

Melewatkan pembuangan dapat menyebabkan kebocoran memori, terutama jika Anda membuat banyak dokumen dalam sebuah loop.

## Contoh Lengkap yang Berfungsi

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

Itulah seluruh alur kerja **call java from javascript** dalam beberapa baris.

## Pertanyaan yang Sering Diajukan

### Apakah ini bekerja di Android?

Aspose.HTML adalah perpustakaan murni‑Java, sehingga dapat berjalan di JVM apa pun, termasuk Dalvik/ART Android. Cukup bundel JAR‑nya dan Anda akan memiliki kemampuan host‑object yang sama.

### Bagaimana jika saya perlu mengirim objek kompleks?

Anda dapat mengekspos POJO (plain old Java objects) yang berisi bidang, getter, dan setter. Mesin akan memetakan mereka ke objek JavaScript secara otomatis. Untuk koleksi, gunakan `java.util.List` atau array—keduanya dapat dikonversi.

### Bagaimana cara kerja penanganan error?

Jika skrip melempar error JavaScript, `eval` akan memunculkan `ScriptException`. Bungkus pemanggilan dalam blok try‑catch untuk mencatat atau memulihkan:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### Bisakah saya menjalankan beberapa skrip secara berurutan?

Tentu saja. Instance `HTMLDocument` yang sama mempertahankan ruang lingkup globalnya, sehingga Anda dapat memanggil `eval` berulang kali. Hanya perlu memperhatikan bentrok nama variabel antar skrip.

## Praktik Terbaik & Tips

- **Berikan nama host object Anda dengan jelas**—`javaLogger`, `javaUtils`, dll.—untuk menghindari kebingungan.
- **Jaga metode host tetap kecil dan bebas efek samping** bila memungkinkan; ini memudahkan debugging.
- **Buang (dispose) dokumen** segera setelah selesai; ini melepaskan memori native yang dialokasikan Aspose.HTML.
- **Validasi input** dari JavaScript, terutama jika skrip berasal dari sumber yang tidak terpercaya. Perlakukan mereka seperti data eksternal apa pun.

## Kesimpulan

Anda kini memiliki contoh lengkap yang solid tentang cara **memanggil java dari javascript** dengan **menambahkan host object**, **menjalankan JavaScript di Java**, dan **mencatat dari JavaScript** menggunakan Aspose.HTML. Pola ini kuat: layanan Java apa pun dapat diekspos ke skrip, menjadikan aplikasi Java Anda platform skrip ringan.

Selanjutnya, Anda mungkin ingin menjelajahi:

- Menyuntikkan halaman HTML lengkap dan memanipulasi DOM dari JavaScript.
- Menggunakan host object untuk mengalirkan data kembali ke sisi Java (misalnya, serialisasi JSON).
- Mengintegrasikan dengan mesin skrip lain seperti Nashorn atau GraalVM untuk dukungan bahasa yang lebih luas.

Cobalah, ubah kelas `Logger` atau `Utils`, dan lihat sejauh mana Anda dapat mengembangkan konsep **javascript host object** dalam proyek Anda sendiri

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}