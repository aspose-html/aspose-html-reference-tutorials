---
category: general
date: 2026-06-16
description: Muat JSON dengan fetch menggunakan Java. Pelajari cara menjalankan JavaScript
  dari Java, optional chaining, dan membuat HTMLDocument di Java dalam satu tutorial.
draft: false
keywords:
- load json with fetch
- fetch json in javascript
- run javascript from java
- optional chaining tutorial
- create htmldocument in java
language: id
og_description: Muat JSON dengan fetch menggunakan Java. Tutorial ini menunjukkan
  cara menjalankan JavaScript dari Java, menggunakan optional chaining, dan membuat
  HTMLDocument di Java.
og_title: Muat JSON dengan Fetch di Java – Panduan Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Load JSON with fetch using Java. Learn how to run JavaScript from Java,
    optional chaining, and create HTMLDocument in Java in one tutorial.
  headline: Load JSON with Fetch in Java – Complete Guide
  type: TechArticle
- description: Load JSON with fetch using Java. Learn how to run JavaScript from Java,
    optional chaining, and create HTMLDocument in Java in one tutorial.
  name: Load JSON with Fetch in Java – Complete Guide
  steps:
  - name: Expected Output
    text: '``` Title: delectus aut autem ```'
  - name: 1. What if the target API returns a non‑JSON response?
    text: '`response.json()` will throw a `SyntaxError`. Our `try/catch` block captures
      that, logging “Fetch failed”. You can extend the catch to retry or fallback
      to a static payload.'
  - name: 2. Can I use this approach with HTTPS certificates that aren’t trusted?
    text: The built‑in `fetch` respects the JVM’s default SSL context. If you need
      to trust a self‑signed cert, set a custom `SSLContext` before creating the `HTMLDocument`.
      That’s a bit beyond this tutorial, but the principle stays the same.
  - name: 3. Does this work on Android?
    text: Unfortunately, `HTMLDocument` isn’t part of the Android SDK. For mobile,
      you’d need a different JavaScript engine (e.g., GraalVM) or a native HTTP client.
  - name: 4. How does optional chaining differ from classic null checks?
    text: 'Instead of writing:'
  type: HowTo
tags:
- Java
- JavaScript
- Fetch API
- HTMLDocument
- Scripting
title: Muat JSON dengan Fetch di Java – Panduan Lengkap
url: /id/java/creating-managing-html-documents/load-json-with-fetch-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Muat JSON dengan Fetch – Tutorial Java Lengkap

Pernah bertanya-tanya bagaimana cara **memuat JSON dengan fetch** sambil tetap berada di dalam aplikasi Java murni? Anda tidak sendirian. Banyak pengembang menemui kebuntuan ketika harus memanggil endpoint REST modern tetapi tidak ingin menambahkan pustaka klien HTTP yang berat. Kabar baiknya? Anda dapat memanfaatkan kekuatan kelas `HTMLDocument` yang mirip browser, menyiapkan mesin JavaScript, dan membiarkan `fetch` melakukan pekerjaan berat—semua dari Java.

Dalam panduan ini kami akan menelusuri contoh praktis yang **mengambil JSON dalam JavaScript**, mengeksekusi skrip tersebut dari Java, dan bahkan menampilkan optional chaining. Pada akhir tutorial Anda akan tahu cara **menjalankan JavaScript dari Java**, membuat `HTMLDocument` di Java, dan menangani bidang JSON yang hilang dengan elegan. Tanpa dependensi eksternal, hanya JDK dan sedikit kreativitas.

## Apa yang Dibahas dalam Tutorial Ini

- Menyiapkan instance `HTMLDocument` di Java (`create htmldocument in java`).
- Mendapatkan `ScriptEngine` yang tersemat dan memberi makan JavaScript modern.
- Menulis potongan **fetch JSON in JavaScript** yang menggunakan `async/await` dan optional chaining (`optional chaining tutorial`).
- Menjalankan skrip melalui `engine.evaluate` (`run javascript from java`).
- Memverifikasi output dan menangani kasus tepi seperti kesalahan jaringan atau properti yang hilang.

Anda memerlukan Java 17 atau lebih baru, karena demo ini bergantung pada mesin kompatibel Nashorn bawaan yang disertakan dalam JDK. Jika Anda menggunakan JDK yang lebih lama, cukup tambahkan pustaka skrip yang sesuai—rincian ada di bagian “Prasyarat”.

---

## Prasyarat

- **JDK 17+** terpasang dan `JAVA_HOME` telah dikonfigurasi.
- Familiaritas dasar dengan sintaks Java dan JavaScript asynchronous.
- IDE atau editor teks (IntelliJ IDEA, VS Code, Eclipse—pilihan Anda).

Tidak diperlukan klien HTTP pihak ketiga atau parser JSON; semuanya berada di dalam skrip.

---

## Langkah 1: Buat HTMLDocument di Java

Hal pertama—**create htmldocument in java**. Kelas `HTMLDocument` memberi kita DOM ringan dan, yang lebih penting, `ScriptEngine` terbundel yang dapat mengevaluasi JavaScript seperti halnya browser.

```java
import org.w3c.dom.html.HTMLDocument;
import javax.script.ScriptEngine;

// Step 1: Instantiate an empty HTMLDocument.
HTMLDocument doc = new HTMLDocument();
```

> **Mengapa ini penting:** `HTMLDocument` berfungsi sebagai sandbox. Ia menyediakan objek global `window`, `fetch`, dan API web lainnya yang dapat diakses skrip. Anggap saja sebagai mini‑browser tanpa UI.

---

## Langkah 2: Ambil Mesin JavaScript dari Dokumen

Sekarang kita perlu **run JavaScript from Java**. Dokumen menyediakan `ScriptEngine` yang memahami ECMAScript modern (termasuk `async/await`). Dapatkan seperti ini:

```java
// Step 2: Obtain the scripting engine linked to the document.
ScriptEngine engine = doc.getScriptEngine();
```

> **Pro tip:** Jika Anda pernah menemui `ScriptException` tentang fitur yang tidak didukung, pastikan Anda menggunakan JDK 17+. JDK lama menyertakan mesin Nashorn warisan yang tidak mendukung async.

---

## Langkah 3: Tulis Potongan JavaScript Modern (Optional Chaining Tutorial)

Di sinilah bagian **fetch json in javascript** bersinar. Kami akan mendefinisikan string multi‑baris (text block Java 15+ `"""`) yang mengambil payload JSON contoh, menggunakan `await`, dan mendemonstrasikan optional chaining (`??`) untuk menangani nilai yang hilang.

```java
// Step 3: Define a modern JavaScript snippet.
String script = """
    async function loadData() {
        try {
            const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
            if (!response.ok) {
                console.error('Network error:', response.status);
                return;
            }
            const data = await response.json();
            // optional chaining tutorial – safely access title
            console.log('Title:', data.title ?? 'No title');
        } catch (err) {
            console.error('Fetch failed:', err);
        }
    }
    loadData();
    """;
```

**Apa yang terjadi?**

- `fetch` mengirim permintaan GET ke API placeholder publik.
- `await` menunda eksekusi hingga promise selesai, menjaga kode tetap bersih.
- `data.title ?? 'No title'` adalah pola optional chaining: jika `title` `null` atau `undefined`, kita kembali ke `'No title'`.
- Seluruhnya dibungkus dalam blok `try/catch` untuk menampilkan masalah jaringan apa pun.

---

## Langkah 4: Jalankan Skrip di Dalam Dokumen

Akhirnya, kami menyerahkan skrip ke mesin. Mesin menjalankannya di thread yang sama, sehingga Anda akan melihat output konsol langsung di proses Java Anda.

```java
// Step 4: Run the JavaScript within the document's scripting environment.
engine.evaluate(script);
```

Saat Anda menjalankan program, Anda seharusnya melihat sesuatu seperti:

```
Title: delectus aut autem
```

Jika API berubah atau bidang `title` menghilang, output akan beralih secara elegan menjadi:

```
Title: No title
```

Itulah keindahan optional chaining—tidak ada `TypeError` yang menghentikan aplikasi Java Anda.

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut kelas Java mandiri yang dapat Anda salin‑tempel ke `Main.java` dan jalankan dengan `java Main.java`.

```java
import org.w3c.dom.html.HTMLDocument;
import javax.script.ScriptEngine;
import javax.script.ScriptException;

public class Main {
    public static void main(String[] args) throws ScriptException {
        // 1️⃣ Create an empty HTMLDocument.
        HTMLDocument doc = new HTMLDocument();

        // 2️⃣ Get the JavaScript engine tied to the document.
        ScriptEngine engine = doc.getScriptEngine();

        // 3️⃣ Define a script that loads JSON with fetch and uses optional chaining.
        String script = """
            async function loadData() {
                try {
                    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                    if (!response.ok) {
                        console.error('Network error:', response.status);
                        return;
                    }
                    const data = await response.json();
                    // optional chaining tutorial – safely access title
                    console.log('Title:', data.title ?? 'No title');
                } catch (err) {
                    console.error('Fetch failed:', err);
                }
            }
            loadData();
            """;

        // 4️⃣ Execute the script.
        engine.evaluate(script);
    }
}
```

### Output yang Diharapkan

```
Title: delectus aut autem
```

Jika Anda sengaja merusak URL (misalnya ubah `todos/1` menjadi `todos/9999`), Anda akan melihat pesan fallback atau kesalahan jaringan, yang menunjukkan penanganan error yang tangguh.

---

## Pertanyaan Umum & Kasus Tepi

### 1. Bagaimana jika API target mengembalikan respons non‑JSON?

`response.json()` akan melempar `SyntaxError`. Blok `try/catch` kami menangkapnya, mencatat “Fetch failed”. Anda dapat memperluas `catch` untuk melakukan retry atau fallback ke payload statis.

### 2. Bisakah saya menggunakan pendekatan ini dengan sertifikat HTTPS yang tidak dipercaya?

`fetch` bawaan menghormati konteks SSL default JVM. Jika Anda perlu mempercayai sertifikat self‑signed, atur `SSLContext` khusus sebelum membuat `HTMLDocument`. Itu agak di luar tutorial ini, tetapi prinsipnya tetap sama.

### 3. Apakah ini bekerja di Android?

Sayangnya, `HTMLDocument` bukan bagian dari SDK Android. Untuk mobile, Anda memerlukan mesin JavaScript lain (misalnya GraalVM) atau klien HTTP native.

### 4. Bagaimana optional chaining berbeda dari pemeriksaan null klasik?

Alih‑alih menulis:

```javascript
if (data && data.title) {
    console.log(data.title);
} else {
    console.log('No title');
}
```

Anda cukup menggunakan `data.title ?? 'No title'`. Lebih singkat, kurang rawan error, dan terbaca seperti bahasa alami—sempurna untuk **optional chaining tutorial**.

---

## Pro Tips & Praktik Terbaik

- **Gunakan kembali mesin:** Membuat `HTMLDocument` baru untuk setiap permintaan dapat mahal. Simpan satu instance hidup jika Anda melakukan banyak panggilan.
- **Keamanan thread:** `ScriptEngine` tidak thread‑safe secara default. Sinkronkan akses atau buat pool mesin untuk beban kerja bersamaan.
- **Logging:** `console.log` skrip menulis ke `System.out`. Jika Anda memerlukan kerangka logging yang tepat, alihkan dengan `engine.getContext().setWriter(new PrintWriter(...))`.
- **Timeouts:** `fetch` menghormati timeout default browser (biasanya tidak ada). Anda dapat mengimplementasikan abort manual menggunakan API `AbortController` di dalam skrip jika memerlukan kontrol yang lebih ketat.

---

## Kesimpulan

Kami baru saja menunjukkan cara **memuat JSON dengan fetch** dari program Java, memanfaatkan mesin JavaScript tersemat untuk menjalankan kode `async/await` modern, dan menggunakan optional chaining agar tetap rapi. Dengan **membuat HTMLDocument di Java**, Anda mendapatkan lingkungan sandbox yang membuat **menjalankan JavaScript dari Java** terasa alami, sambil tetap berada dalam kode Java murni.

Dari sini Anda dapat:

- Mengganti API placeholder dengan layanan Anda sendiri (`fetch json in javascript` dari endpoint privat).
- Menambahkan penanganan error atau retry yang lebih canggih.
- Menjelajahi kemampuan polyglot GraalVM untuk scripting yang lebih kaya.

Cobalah, ubah URL, bahkan tambahkan permintaan `POST`—ada dunia Java berorientasi web yang dapat Anda buka tanpa menambahkan pustaka berat.

Selamat coding, dan jangan ragu meninggalkan komentar jika Anda menemui kendala!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Run JavaScript in Java – Complete Guide](/html/english/java/advanced-usage/how-to-run-javascript-in-java-complete-guide/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Load HTML Documents from URL in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}