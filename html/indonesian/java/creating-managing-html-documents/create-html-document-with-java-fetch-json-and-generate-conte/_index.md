---
category: general
date: 2026-02-11
description: Buat dokumen HTML dalam Java menggunakan Aspose.HTML. Pelajari cara mengambil
  JSON JavaScript, menambahkan elemen script, menghasilkan HTML dari JSON, dan mengonversi
  JSON menjadi pre.
draft: false
keywords:
- create html document
- fetch json javascript
- add script element
- generate html from json
- convert json to pre
language: id
og_description: Buat dokumen HTML di Java dengan Aspose.HTML. Ambil JSON JavaScript,
  tambahkan elemen script, hasilkan HTML dari JSON, dan ubah JSON menjadi elemen pre—semua
  dalam satu tutorial.
og_title: Buat Dokumen HTML di Java – Panduan Lengkap
tags:
- Aspose.HTML
- Java
- Web Automation
title: Buat Dokumen HTML dengan Java – Ambil JSON dan Hasilkan Konten
url: /id/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Dokumen HTML – Tutorial Java Lengkap

Pernah membutuhkan **create HTML document** secara cepat tetapi tidak yakin bagaimana menarik data remote ke dalamnya? Anda tidak sendirian. Dalam banyak proyek Anda ingin mengambil JSON dengan JavaScript, menyuntikkan hasilnya ke halaman, dan kemudian menyimpan markup akhir sebagai file statis. Panduan ini menunjukkan secara tepat cara melakukannya menggunakan Aspose.HTML untuk Java.

Kami akan melangkah melalui setiap langkah: dari menginstansiasi dokumen kosong, ke **fetch JSON JavaScript**, ke **add script element**, dan akhirnya ke **generate HTML from JSON** dan **convert JSON to pre** tags. Pada akhirnya Anda akan memiliki `fetchResult.html` yang siap pakai yang berisi data yang diambil dan ditampilkan sebagai JSON yang diformat rapi.

## Prasyarat

- Java 17 atau lebih baru (kode dapat dikompilasi dengan JDK 11+ juga)
- Perpustakaan Aspose.HTML untuk Java (tersedia melalui Maven Central)
- Familiaritas dasar dengan HTML dan JavaScript async
- IDE atau baris perintah `javac`/`java` biasa

Tidak ada kerangka kerja tambahan yang diperlukan—semua berjalan secara lokal.

## Langkah 1: Siapkan Proyek dan Impor Aspose.HTML

Pertama, tambahkan dependensi Aspose.HTML ke `pom.xml` Anda (atau unduh JAR secara manual).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

> **Pro tip:** Jaga nomor versi tetap terbaru; rilis yang lebih baru memperbaiki bug dan meningkatkan mesin skrip.

## Langkah 2: **Create HTML Document** – Kanvas Kosong

Kami memulai dengan membuat `HTMLDocument` kosong. Anggaplah itu sebagai halaman baru di mana nanti kami akan menaruh skrip kami.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();
```

Mengapa kita membutuhkan objek dokumen? `ScriptEngine` Aspose.HTML bekerja terhadap DOM, bukan string mentah. Dengan membangun dokumen yang tepat, kami memberikan mesin lingkungan nyata untuk mengeksekusi **fetch JSON JavaScript** kami.

## Langkah 3: Tulis Potongan JavaScript – **Fetch JSON JavaScript** dan **Convert JSON to pre**

Inti tutorial berada dalam string multiline ini. Ia melakukan `fetch` asynchronous, mengurai JSON, lalu menulis elemen `<pre>` dengan data yang diformat rapi.

```java
        // Step 3: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;
```

Perhatikan komentar *Convert JSON to <pre>* – itulah tepatnya apa yang dilakukan panggilan `JSON.stringify(..., null, 2)`. Ia menambahkan indentasi, membuat output dapat dibaca manusia.

## Langkah 4: **Add Script Element** ke Dokumen

Sekarang kami membuat tag `<script>`, menaruh kode kami di dalamnya, dan melampirkannya ke body. Ini adalah bagian **add script element**.

```java
        // Step 4: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);
```

Mengapa melampirkannya ke body? Di browser nyata skrip akan dijalankan segera setelah diparsing. Dengan menambahkannya ke DOM kami meniru perilaku itu secara tepat, memastikan fetch asynchronous berjalan ketika kami kemudian memanggil mesin.

## Langkah 5: Jalankan Script Engine – Biarkan Async Fetch Selesai

Aspose.HTML menyediakan `ScriptEngine` yang dapat mengeksekusi JavaScript berbasis DOM. Kami memanggil `run()` dan menunggu rantai promise selesai.

```java
        // Step 5: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();
```

Mesin akan memblokir hingga semua tugas tertunda (fetch kami) selesai, menjamin bahwa HTML yang dihasilkan sudah berisi data.

## Langkah 6: **Generate HTML from JSON** – Simpan Hasil

Akhirnya kami menyimpan dokumen ke disk. File kini berisi blok `<pre>` dengan payload JSON.

```java
        // Step 6: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

Menjalankan program menghasilkan `fetchResult.html`. Buka di browser apa pun dan Anda akan melihat sesuatu seperti:

```html
<pre>{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}</pre>
```

Itulah hasil **generate HTML from JSON** yang Anda cari.

## Contoh Lengkap yang Berfungsi

Di bawah ini adalah file sumber lengkap yang siap dijalankan. Salin, tempel, sesuaikan jalur output, dan jalankan `java JsFetchExample`.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();

        // Step 2: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;

        // Step 3: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);

        // Step 4: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();

        // Step 5: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

## Output yang Diharapkan & Verifikasi

1. **Console:** Anda akan melihat `HTML with fetched data saved.`  
2. **File (`fetchResult.html`):** Membukanya menampilkan JSON di dalam blok `<pre>`, dengan indentasi yang rapi.  
3. **Validation:** Jika Anda melihat sumber halaman, Anda hanya akan menemukan elemen `<pre>`—tidak ada tag skrip tambahan karena mesin sudah mengeksekusinya.

## Pertanyaan Umum & Kasus Pinggir

| Question | Answer |
|----------|--------|
| *Bagaimana jika API mengembalikan error?* | Bungkus pemanggilan `fetch` dalam blok `try…catch` dan tulis pesan error ke body alih-alih JSON. |
| *Apakah saya dapat mengambil beberapa sumber daya?* | Ya—cukup rangkai pemanggilan `await fetch(...)` tambahan atau gunakan `Promise.all`. `innerHTML` akhir dapat menggabungkan beberapa blok `<pre>`. |
| *Apakah saya perlu mengatur header CORS?* | Karena skrip berjalan di dalam sandbox Aspose.HTML, ia menghormati kebijakan same‑origin. Endpoint publik JSONPlaceholder sudah mengizinkan permintaan cross‑origin. |
| *Bagaimana mengubah direktori output saat runtime?* | Berikan path sebagai argumen baris perintah (`args[0]`) dan ganti string yang di‑hard‑code di `htmlDoc.save`. |
| *Apakah ada cara menyematkan CSS untuk styling?* | Tentu saja. Buat elemen `<style>`, set `textContent`‑nya ke CSS Anda, dan tambahkan ke `<head>` sebelum menjalankan mesin. |

## Tips untuk Penggunaan Produksi

- **Cache the JSON** jika endpoint lambat; Anda dapat menulis string yang di‑fetch ke file dan menggunakannya kembali.
- **Sanitize the data** sebelum menyuntikkannya, terutama jika sumber tidak terpercaya. Gunakan `JSON.stringify` dengan aman atau escape entitas HTML.
- **Configure the ScriptEngine timeout** (`scriptEngine.setTimeout(5000)`) untuk menghindari hang pada layanan yang tidak responsif.

## Ringkasan Visual

![contoh create html document yang menunjukkan HTML yang dihasilkan dengan JSON di dalam tag pre](fetchResult.png "Tangkapan layar dokumen HTML yang dihasilkan")

*Teks alt:* *contoh create html document – file HTML yang dihasilkan menampilkan JSON yang di‑fetch di dalam elemen pre.*

## Kesimpulan

Anda kini tahu cara **create HTML document** secara programatis di Java, **fetch JSON JavaScript**, **add script element**, **generate HTML from JSON**, dan **convert JSON to pre** untuk output yang dapat dibaca. Seluruh alur kerja berjalan offline, hanya memerlukan Aspose.HTML, dan menghasilkan file statis bersih yang dapat Anda layani di mana saja.

Selanjutnya, cobalah memperluas skrip untuk mengulang array objek, menambahkan styling CSS, atau menulis beberapa halaman menggunakan teknik yang sama. Anda juga dapat mengganti URL `fetch` dengan API Anda sendiri untuk mengubah data dinamis menjadi snapshot statis—sempurna untuk pre‑rendering yang ramah SEO.

Selamat coding, dan silakan bagikan eksperimen Anda di komentar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}