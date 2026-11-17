---
category: general
date: 2026-05-28
description: mengambil data API di Java menggunakan Aspose.HTML – pelajari cara mengeksekusi
  JavaScript async, menjalankan skrip async, dan mengatur atribut DOM dari JSON yang
  diambil.
draft: false
keywords:
- fetch api data
- execute async javascript
- run async script
- set dom attribute
- how to run async
language: id
og_description: mengambil data API di Java dengan Aspose.HTML. Tutorial ini menunjukkan
  cara mengeksekusi JavaScript async, menjalankan skrip async, dan mengatur atribut
  DOM dari hasil API.
og_title: Mengambil Data API di Java – Panduan Aspose.HTML Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: fetch api data in Java using Aspose.HTML – learn how to execute async
    javascript, run async script, and set dom attribute from fetched JSON.
  headline: fetch api data in Java with Aspose.HTML - Complete Guide
  type: TechArticle
- description: fetch api data in Java using Aspose.HTML – learn how to execute async
    javascript, run async script, and set dom attribute from fetched JSON.
  name: fetch api data in Java with Aspose.HTML - Complete Guide
  steps:
  - name: Expected Output
    text: '``` GitHub stars: 84327 ```'
  - name: What if the fetch call fails?
    text: 'The script will throw a JavaScript exception, which propagates to `ScriptEngine.evaluate`.
      You can catch it in Java:'
  - name: Can I fetch from a private API that requires authentication?
    text: 'Sure—just add the appropriate headers in the script:'
  - name: Does this work on older Java versions?
    text: Aspose.HTML ships with its own JavaScript engine, so you don’t need Nashorn
      or GraalVM. However, the `try‑with‑resources` syntax requires Java 7+. For Java
      6 you’d have to close the document manually.
  type: HowTo
tags:
- Java
- Aspose.HTML
- Async JavaScript
title: Mengambil data API di Java dengan Aspose.HTML - Panduan Lengkap
url: /id/java/message-handling-networking/fetch-api-data-in-java-with-aspose-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fetch api data in Java dengan Aspose.HTML – Panduan Lengkap

Pernah bertanya-tanya bagaimana cara **fetch api data** di Java tanpa meninggalkan kenyamanan IDE Anda? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan ketika mereka perlu memanggil layanan remote dari halaman HTML yang dirender oleh Aspose.HTML dan kemudian menarik hasilnya kembali ke Java.  

Dalam tutorial ini kami akan membahas contoh praktis yang **executes async javascript**, menjalankan **async script**, dan akhirnya **sets a DOM attribute** dengan nilai yang di‑fetch. Pada akhir tutorial Anda akan tahu persis *how to run async* operasi dengan aman dan mengambil data yang Anda butuhkan.

## Apa yang Akan Anda Bangun

Kami akan membuat aplikasi konsol Java kecil yang:

1. Memuat file HTML yang berisi fungsi async.  
2. Menjalankan skrip yang menggunakan **fetch API** untuk memanggil endpoint publik GitHub.  
3. Menunggu promise selesai (hingga 10 detik).  
4. Menyimpan jumlah bintang ke atribut khusus `data-stars` pada elemen `<body>`.  
5. Membaca kembali atribut tersebut di Java dan mencetaknya.

Tanpa pustaka klien HTTP eksternal, tanpa kode threading tambahan—hanya Aspose.HTML yang melakukan pekerjaan berat.

## Prasyarat

- **Java 17** atau yang lebih baru (kode dapat dikompilasi dengan versi sebelumnya, tetapi 17 adalah LTS saat ini).  
- **Aspose.HTML for Java** library (versi 23.9 atau lebih baru).  
- File HTML sederhana (`async-page.html`) yang ditempatkan di suatu tempat di disk Anda.  
- Koneksi internet (panggilan fetch menuju `https://api.github.com`).  

Jika Anda sudah memiliki proyek Maven, tambahkan dependensi Aspose.HTML:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

Sekarang, mari kita selami kode.

## Langkah 1: Siapkan Halaman HTML

Pertama, buat file HTML minimal yang akan menampung fungsi async. Anda tidak memerlukan markup yang rumit—hanya tag `<body>`.

```html
<!-- async-page.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Async Demo</title>
</head>
<body>
    <!-- The script we’ll inject later will populate this attribute -->
</body>
</html>
```

Simpan file ini di lokasi yang dapat dijangkau, misalnya `C:/temp/async-page.html`. Path tersebut akan digunakan dalam kode Java.

![contoh fetch api data](https://example.com/fetch-api-data.png "contoh fetch api data")

*Teks alt gambar: contoh fetch api data yang menampilkan output konsol bintang GitHub.*

## Langkah 2: Muat Dokumen HTML di Java

Dengan file HTML siap, kami membukanya menggunakan `HTMLDocument` milik Aspose.HTML. Blok `try‑with‑resources` menjamin dokumen dibuang dengan benar.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsExample {
    public static void main(String[] args) throws Exception {

        // Load the HTML page that contains an async function
        try (HTMLDocument doc = new HTMLDocument("C:/temp/async-page.html")) {
            // The rest of the steps go here...
        }
    }
}
```

Mengapa menggunakan `HTMLDocument`? Ia memberi kami DOM lengkap, mesin JavaScript bawaan, dan cara yang nyaman untuk berinteraksi dengan halaman dari Java—semua tanpa harus menjalankan browser.

## Langkah 3: Tulis Skrip Async

Sekarang kami menyusun potongan JavaScript yang **fetches API data**, menunggu promise, dan kemudian **sets a DOM attribute**. Perhatikan penggunaan `async/await`—pola yang sama seperti yang Anda tulis di browser.

```java
String script =
    "async function run() {" +
    "  const data = await fetch('https://api.github.com').then(r => r.json());" +
    "  document.body.setAttribute('data-stars', data.stargazers_count);" +
    "}" +
    "run();";
```

Beberapa hal yang perlu dicatat:

- Fungsi `run` dideklarasikan `async`, sehingga kami dapat `await` panggilan `fetch`.  
- Setelah JSON di‑parse, kami menyimpan `data.stargazers_count` ke dalam atribut khusus `data-stars`.  
- Akhirnya kami memanggil `run()` secara langsung.  

Skrip kecil ini melakukan semua yang kami butuhkan untuk **run async script** dan menangkap hasilnya.

## Langkah 4: Jalankan Skrip dan Tunggu

`ScriptEngine` milik Aspose.HTML dapat mengevaluasi JavaScript dengan batas waktu. Dengan memberikan `10000` kami memberi tahu mesin untuk menunggu hingga **10 detik** agar operasi async selesai.

```java
// Execute the script and wait (up to 10 seconds) for the async operation to finish
ScriptEngine engine = doc.getScriptEngine();
engine.evaluate(script, 10000);   // timeout in milliseconds
```

Jika permintaan memakan waktu lebih lama dari batas waktu, `ScriptException` akan dilempar—sangat cocok untuk menangani kondisi jaringan yang tidak stabil. Di produksi Anda mungkin akan membungkus ini dalam try‑catch dan melakukan retry bila diperlukan.

## Langkah 5: Ambil Atribut dari Java

Setelah skrip selesai, atribut `data-stars` kini menjadi bagian dari DOM. Tarik kembali ke Java dengan panggilan sederhana:

```java
// Retrieve the value set by the script from the document
String stars = doc.getBody().getAttribute("data-stars");
System.out.println("GitHub stars: " + stars);
```

Baris itu mencetak sesuatu seperti `GitHub stars: 12345`. Angka tepat berubah setiap hari, tetapi pola tetap sama.

## Contoh Lengkap yang Berfungsi

Menggabungkan semua bagian, berikut program lengkap yang siap dijalankan:

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML page that contains an async function
        try (HTMLDocument doc = new HTMLDocument("C:/temp/async-page.html")) {

            // Step 2: Define a script that calls the async function and stores the result in a DOM attribute
            String script =
                "async function run() {" +
                "  const data = await fetch('https://api.github.com').then(r => r.json());" +
                "  document.body.setAttribute('data-stars', data.stargazers_count);" +
                "}" +
                "run();";

            // Step 3: Execute the script and wait (up to 10 seconds) for the async operation to finish
            ScriptEngine engine = doc.getScriptEngine();
            engine.evaluate(script, 10000);

            // Step 4: Retrieve the value set by the script from the document
            String stars = doc.getBody().getAttribute("data-stars");
            System.out.println("GitHub stars: " + stars);
        }
    }
}
```

### Output yang Diharapkan

```
GitHub stars: 84327
```

(Angka Anda akan berbeda; bagian pentingnya adalah nilai tersebut adalah **string** yang mewakili jumlah bintang.)

## Pertanyaan Umum & Kasus Edge

### Bagaimana jika panggilan fetch gagal?

Skrip akan melemparkan pengecualian JavaScript, yang diteruskan ke `ScriptEngine.evaluate`. Anda dapat menangkapnya di Java:

```java
try {
    engine.evaluate(script, 10000);
} catch (ScriptException e) {
    System.err.println("Failed to fetch data: " + e.getMessage());
}
```

### Bisakah saya fetch dari API pribadi yang memerlukan otentikasi?

Tentu—cukup tambahkan header yang sesuai dalam skrip:

```javascript
await fetch('https://api.example.com/secure', {
    headers: { 'Authorization': 'Bearer YOUR_TOKEN' }
}).then(r => r.json());
```

Ingat untuk menjaga rahasia tetap di luar kontrol sumber.

### Apakah ini bekerja pada versi Java yang lebih lama?

Aspose.HTML dilengkapi dengan mesin JavaScript-nya sendiri, jadi Anda tidak memerlukan Nashorn atau GraalVM. Namun, sintaks `try‑with‑resources` memerlukan Java 7+. Untuk Java 6 Anda harus menutup dokumen secara manual.

## Tips Pro

- **Reuse the ScriptEngine**: Jika Anda perlu menjalankan banyak skrip async, pertahankan satu instance engine yang tetap hidup—mengurangi overhead.  
- **Increase the timeout** untuk API yang lebih lambat, tetapi jangan set ke `Integer.MAX_VALUE`; Anda tetap menginginkan jaring pengaman.  
- **Validate the attribute** sebelum menggunakannya. Atribut DOM mungkin `null` jika skrip tidak pernah dijalankan.  
- **Log the raw JSON** selama pengembangan; ini membantu ketika API berubah struktur.

## Langkah Selanjutnya

Sekarang Anda tahu cara **fetch api data**, Anda dapat memperluas pola ini:

- **Parse more complex JSON** dan sisipkan beberapa atribut.  
- **Create tables** di dalam halaman HTML berdasarkan data yang di‑fetch.  
- **Combine with Aspose.PDF** untuk menghasilkan PDF yang berisi hasil API secara langsung.

Setiap hal ini dibangun di atas ide inti yang sama: **execute async javascript**, **run async script**, dan **set dom attribute** dari hasilnya. Silakan bereksperimen—banyak kekuatan tersembunyi dalam mesin skrip Aspose.HTML.

*Selamat coding! Jika Anda mengalami kendala, tinggalkan komentar di bawah dan kami akan membantu memecahkan bersama.*

## Tutorial Terkait

- [Cara Menjalankan JavaScript di Java – Panduan Lengkap](/html/english/java/advanced-usage/how-to-run-javascript-in-java-complete-guide/)
- [Tambahkan Elemen ke Body dengan Aspose.HTML untuk Java menggunakan DOM Mutation Observer](/html/english/java/advanced-usage/dom-mutation-observer-observing-node-additions/)
- [Cara Mengatur Timeout – Mengelola Network Timeout di Aspose.HTML untuk Java](/html/english/java/message-handling-networking/network-timeout/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}