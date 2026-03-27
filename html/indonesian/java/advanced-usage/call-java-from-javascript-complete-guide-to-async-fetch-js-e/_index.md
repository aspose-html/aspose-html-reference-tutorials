---
category: general
date: 2026-03-04
description: Panggil Java dari JavaScript menggunakan Aspose.HTML, jalankan JavaScript
  secara async, dan ambil JSON di Java dengan contoh sederhana. Pelajari cara mengeksekusi
  mesin JavaScript secara efisien.
draft: false
keywords:
- call java from javascript
- run async javascript
- fetch json in java
- asynchronous fetch api
- execute javascript engine
language: id
og_description: Panggil Java dari JavaScript dengan Aspose.HTML, jalankan JavaScript
  async, dan ambil JSON di Java. Kode lengkap, penjelasan, dan tips disertakan.
og_title: Panggil Java dari JavaScript – Tutorial Fetch Asinkron Langkah demi Langkah
tags:
- Java
- JavaScript
- Aspose.HTML
- Async Programming
title: Memanggil Java dari JavaScript – Panduan Lengkap untuk Pengambilan Asinkron
  & Eksekusi Mesin JS
url: /id/java/advanced-usage/call-java-from-javascript-complete-guide-to-async-fetch-js-e/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Panggil Java dari JavaScript – Tutorial Lengkap dengan Async Fetch API

Pernah bertanya-tanya bagaimana cara **memanggil Java dari JavaScript** tanpa meninggalkan aplikasi Java Anda? Mungkin Anda sedang membangun renderer HTML sisi‑server, atau Anda perlu mengekspos logika Java ke skrip yang berjalan di dalam sebuah dokumen. Kabar baiknya, Aspose.HTML membuat ini menjadi sangat mudah. Dalam panduan ini kami tidak hanya akan menunjukkan cara *menjalankan JavaScript async* di dalam dokumen yang didukung Java, tetapi juga cara **mengambil JSON di Java** menggunakan **asynchronous fetch API** modern dan akhirnya **mengeksekusi panggilan mesin JavaScript** secara aman.

Singkatnya, Anda akan mendapatkan contoh lengkap yang dapat dijalankan yang mengambil payload JSON dari endpoint publik, menyerahkannya ke objek host Java, dan mencetak hasilnya di konsol. Tanpa server web eksternal, tanpa pustaka tambahan—hanya Java murni dan Aspose.HTML.

## Apa yang Akan Anda Pelajari

- Cara membuat dokumen HTML kosong dengan Aspose.HTML.  
- Cara memperoleh dan **mengeksekusi mesin JavaScript** dari Java.  
- Cara mendaftarkan objek host Java yang dapat dipanggil oleh JavaScript.  
- Cara menulis fungsi **JavaScript asynchronous** yang menggunakan **asynchronous fetch API**.  
- Cara menangani data yang di‑fetch kembali di Java dengan callback yang bersih.  
- Output yang diharapkan dan tips pemecahan masalah.

### Prasyarat

- Java 17 atau lebih baru (kode juga dapat dikompilasi dengan JDK 11).  
- Aspose.HTML for Java 23.7 (atau versi terbaru pada saat penulisan).  
- Familiaritas dasar dengan Java dan promise JavaScript.  
- Akses internet untuk permintaan demo `jsonplaceholder`.

Jika ada yang belum Anda kenal, jangan khawatir—setiap langkah dijelaskan dalam bahasa yang mudah dipahami, dan Anda akan melihat mengapa kami melakukan hal tersebut.

---

## Langkah 1 – Buat Dokumen HTML Kosong dan Dapatkan Mesin JavaScript‑nya

Hal pertama yang kita butuhkan adalah dokumen kosong yang menyediakan lingkungan JavaScript yang terisolasi. Kelas `Document` milik Aspose.HTML melakukan hal itu dengan tepat.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Create an empty HTML document
        Document document = new Document();

        // Obtain the JavaScript engine associated with the document's window
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();
```

**Mengapa ini penting:** Objek `Document` meniru jendela browser, dan `JavaScriptEngine`‑nya memungkinkan kita menjalankan skrip persis seperti yang dilakukan browser. Inilah dasar untuk **call java from javascript**—mesin berfungsi sebagai jembatan.

---

## Langkah 2 – Daftarkan Objek Host Agar JavaScript Dapat Memanggil Kembali ke Java

Aspose.HTML memungkinkan Anda mengekspos objek Java apa pun ke dunia skrip. Kami akan membuat kelas anonim dengan satu metode `onResult` yang cukup mencetak JSON apa pun yang kami terima.

```java
        // Register a Java host object that the script can invoke
        jsEngine.addHostObject("javaCallback", new Object() {
            // This method will be called from JavaScript with the fetched JSON string
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });
```

**Penjelasan:**  
- `addHostObject` mengikat nama `javaCallback` ke objek Java anonim.  
- Di dalam JavaScript kami akan memanggil `javaCallback.onResult(...)`.  
- Inilah inti dari **call java from javascript**—skrip menjangkau ke dunia Java, dan Java merespons.

> **Pro tip:** Jadikan metode objek host `public` dan sederhana; objek yang kompleks dapat menyebabkan masalah serialisasi.

---

## Langkah 3 – Tulis Fungsi JavaScript Asynchronous Menggunakan Asynchronous Fetch API

Sekarang bagian yang menyenangkan: skrip kecil yang mengambil JSON dari endpoint remote. Kami akan menggunakan `async/await`, cara modern untuk **run async JavaScript**.

```java
        // Asynchronous script that fetches JSON and passes it to the Java host object
        String asyncScript =
            "async function fetchData() {" +
            "  const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "  const json = await response.json();" +
            "  javaCallback.onResult(JSON.stringify(json));" +
            "}" +
            "fetchData();";
```

**Mengapa kami memilih `fetch` daripada XHR lama:**  
- `fetch` mengembalikan sebuah `Promise`, membuat kode lebih bersih.  
- Ia bekerja secara native dengan `await`, sehingga alur baca dari atas ke bawah—sempurna untuk demo **asynchronous fetch api**.  
- API ini future‑proof; sebagian besar browser dan mesin (termasuk milik Aspose) mendukungnya langsung.

---

## Langkah 4 – Eksekusi Skrip di Dalam Mesin JavaScript Dokumen

Akhirnya, kami menyerahkan skrip ke mesin. Mesin akan memutar event loop kecil, menyelesaikan promise `fetch`, dan memanggil kembali ke Java ketika selesai.

```java
        // Execute the async script
        jsEngine.execute(asyncScript);
    }
}
```

Saat Anda menjalankan kelas `AsyncJsTutorial`, Anda akan melihat sesuatu seperti:

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

Output tersebut mengonfirmasi tiga hal:

1. **asynchronous fetch API** berhasil mengambil data.  
2. JSON diserialisasi dan diserahkan ke Java.  
3. Panggilan **execute javascript engine** kami selesai tanpa deadlock.

---

## Langkah 5 – Menangani Kesalahan dan Kasus Tepi (Peningkatan Opsional)

Kode dunia nyata jarang berjalan sempurna setiap saat. Berikut beberapa jebakan umum dan cara melindungi diri darinya.

### 5.1 Kegagalan Jaringan

Jika server remote tidak tersedia, `fetch` akan melempar. Bungkus panggilan dalam blok `try/catch`:

```java
String asyncScript =
    "async function fetchData() {" +
    "  try {" +
    "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
    "    if (!response.ok) throw new Error('Network response was not ok');" +
    "    const json = await response.json();" +
    "    javaCallback.onResult(JSON.stringify(json));" +
    "  } catch (e) {" +
    "    javaCallback.onResult('Error: ' + e.message);" +
    "  }" +
    "}" +
    "fetchData();";
```

Sekarang sisi Java akan menerima pesan error alih‑alih menggantung.

### 5.2 Timeout

Mesin Aspose tidak menyediakan timeout native untuk `fetch`, tetapi Anda dapat mengimplementasikannya di JavaScript:

```javascript
const controller = new AbortController();
setTimeout(() => controller.abort(), 5000); // 5‑second timeout
const response = await fetch(url, { signal: controller.signal });
```

### 5.3 Banyak Panggilan

Jika Anda perlu mengambil beberapa sumber daya, cukup lakukan loop atau `map` pada array URL. Objek host dapat diperluas untuk menerima identifier, sehingga Anda dapat mengkorelasikan respons.

---

## Contoh Lengkap yang Dapat Dijalankan

Berikut adalah **file sumber lengkap** yang dapat Anda salin‑tempel ke IDE. Tanpa dependensi tersembunyi, hanya JAR Aspose.HTML di classpath.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an empty HTML document and obtain its JavaScript engine
        Document document = new Document();
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();

        // Step 2: Register a host object that JavaScript can call back into Java
        jsEngine.addHostObject("javaCallback", new Object() {
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });

        // Step 3: Write an async function that uses the asynchronous fetch API
        String asyncScript =
            "async function fetchData() {" +
            "  try {" +
            "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "    if (!response.ok) throw new Error('Network error');" +
            "    const json = await response.json();" +
            "    javaCallback.onResult(JSON.stringify(json));" +
            "  } catch (e) {" +
            "    javaCallback.onResult('Error: ' + e.message);" +
            "  }" +
            "}" +
            "fetchData();";

        // Step 4: Execute the script inside the document's JavaScript engine
        jsEngine.execute(asyncScript);
    }
}
```

**Output console yang diharapkan**

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

Jika Anda melihat baris error yang dimulai dengan `Error:` maka ada yang tidak beres—kemungkinan besar gangguan jaringan.

---

## Gambaran Visual

![Diagram illustrating how Java calls JavaScript and receives async fetch results – call java from javascript](/images/java-js-async.png)

*Gambar menunjukkan alur: Java → JavaScriptEngine → async fetch → JavaCallback.*

---

## Pertanyaan yang Sering Diajukan

**Apakah saya dapat menggunakan pendekatan ini dengan mesin JavaScript lain?**  
Ya, mesin apa pun yang menyediakan mekanisme objek host (misalnya Nashorn, GraalVM) dapat bekerja, tetapi Aspose.HTML memberi Anda lingkungan mirip browser yang lengkap dengan `fetch` bawaan.

**Bagaimana jika saya perlu mengembalikan objek Java yang kompleks alih‑alih string?**  
Anda dapat menserialisasi objek ke JSON di sisi Java dan membiarkan JavaScript mem‑parsenya, atau mengekspos beberapa metode pada objek host untuk menerima field terpisah.

**Apakah implementasi `fetch` sepenuhnya sesuai standar?**  
Aspose.HTML mengimplementasikan WHATWG Fetch Standard, sehingga Anda mendapatkan penanganan yang tepat untuk redirect, CORS, dan streaming.

**Apakah ini memblokir thread Java saat menunggu jaringan?**  
Tidak. Panggilan `execute` mengembalikan segera, dan mesin internal memproses promise secara asynchronous. Namun, thread utama akan tetap hidup sampai skrip selesai atau Anda secara eksplisit mematikan mesin.

---

## Kesimpulan

Kami baru saja menelusuri skenario praktis yang memungkinkan Anda **memanggil Java dari JavaScript**, **menjalankan JavaScript async**, dan **mengambil JSON di Java** menggunakan **asynchronous fetch API**. Dengan membuat objek host, menulis fungsi `async` yang rapi, dan mengeksekusinya lewat **mesin JavaScript** Aspose.HTML, Anda mendapatkan jembatan bersih dan non‑blocking antara dua runtime.

Cobalah, ubah URL, atau tambahkan lebih banyak callback—imajinasi Anda adalah batasnya. Selanjutnya Anda bisa menjelajahi:

- **Executing JavaScript engine** dengan banyak skrip bersamaan.  
- Menggunakan **run async javascript** untuk memproses dataset besar secara paralel.  
- Mengintegrasikan pola ini ke dalam layanan web yang merender HTML dinamis secara on‑the‑fly.

Jangan ragu bereksperimen, dan beri komentar jika Anda menemukan masalah yang tidak terduga. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}