---
category: general
date: 2026-03-26
description: contoh top‑level await yang menunjukkan await delay JavaScript, kelas
  increment counter, dan public class fields JavaScript dalam demo langsung.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: id
og_description: Contoh top‑level await yang menunjukkan await delay JavaScript, kelas
  penghitung increment, dan bidang kelas publik JavaScript dalam tutorial singkat.
og_title: contoh top-level await – Menggunakan penundaan await di JavaScript
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: Contoh top‑level await – Menggunakan await delay dalam JavaScript
url: /id/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# contoh top level await – Menggunakan await delay dalam JavaScript

Pernah bertanya-tanya bagaimana cara menjeda eksekusi modul tanpa membungkus semuanya dalam async IIFE? Itulah yang dilakukan oleh **top level await example**. Dalam tutorial ini kami akan menelusuri sebuah halaman web kecil yang menggunakan `await delay javascript` untuk menunda pekerjaan, lalu membuat sebuah `increment counter class` yang memanfaatkan **public class fields javascript**. Pada akhir tutorial Anda akan memiliki potongan kode lengkap yang dapat disalin‑tempel dan berjalan di semua browser modern.

Kami akan membahas segala hal mulai dari mendefinisikan kelas dengan field publik hingga menyusun helper delay berbasis promise yang sederhana. Tanpa pustaka eksternal, tanpa langkah build—hanya HTML biasa, sebuah `<script type="module">`, dan fitur ECMAScript terbaru. Jika Anda sudah nyaman dengan fungsi async, Anda akan melihat mengapa top‑level await terasa seperti ekstensi alami. Jika Anda baru dengan sintaks **javascript class public field**, jangan khawatir—kami menjelaskan alasan di balik setiap baris.

## Apa yang Akan Anda Pelajari

- Cara kerja **top level await example** di dalam skrip modul.
- Pola untuk helper `await delay javascript` yang meniru `setTimeout` dengan promise.
- Cara menulis **increment counter class** yang menggunakan field publik (`count`) dan blok inisialisasi statis.
- Output konsol yang diharapkan dan cara memverifikasi bahwa blok statis dijalankan sebelum sisa skrip.
- Tips untuk memecahkan masalah umum, seperti browser lama yang tidak mendukung top‑level await.

> **Pro tip:** Browser modern (Chrome 106+, Firefox 102+, Edge 106+) sudah mendukung top‑level await. Jika Anda perlu mendukung lingkungan lama, pertimbangkan bundling dengan alat seperti Vite atau Babel.

## Step 1 – Define a Class with a Public Field and a Static Block

Potongan pertama dari demo kami adalah kelas yang menyimpan penghitung numerik. Perhatikan baris `count = 0;`—ini adalah sintaks **public class fields javascript** yang diperkenalkan di ES2022. Ia membuat properti instance tanpa konstruktor.

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**Mengapa blok statis?** Ia memungkinkan kita menjalankan logika inisialisasi satu kali (seperti logging) pada saat modul diparsing, *sebelum* top‑level await dijalankan. Ini menjamin pesan muncul pertama di konsol, membuktikan bahwa kelas dievaluasi lebih awal.

## Step 2 – Create an `await delay javascript` Helper

Selanjutnya kita membutuhkan fungsi delay berbasis promise yang kecil. Pada dasarnya ia adalah pembungkus `setTimeout`, tetapi mengembalikan promise sehingga dapat di‑await.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**Kasus tepi:** Jika `ms` bernilai negatif atau bukan angka, `setTimeout` memperlakukannya sebagai `0`. Anda dapat menambahkan validasi, tetapi untuk demo satu baris ini cukup terbaca.

## Step 3 – Use Top‑Level Await to Pause Execution

Sekarang hadir bintang utama: top‑level await. Karena skrip kami adalah modul (`type="module"`), kami dapat menempatkan `await` langsung di ruang lingkup atas. Ini menjeda modul sampai promise selesai, memungkinkan kami mengontrol urutan efek samping.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**Pertanyaan umum:** “Apakah saya bisa menggunakan top‑level await di tag `<script>` biasa?” Tidak—hanya skrip modul yang mendukungnya. Jika Anda lupa menambahkan `type="module"`, Anda akan mendapatkan error sintaks.

## Step 4 – Instantiate the Class, Increment, and Log the Result

Akhirnya kami menyatukan semuanya: membuat instance, memanggil `increment()`, dan menampilkan hitungan akhir. Ini memperlihatkan **increment counter class** dalam aksi.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### Output Konsol yang Diharapkan

```
Counter class initialized
Final count: 1
```

Jika Anda membuka halaman di DevTools, Anda akan melihat pesan blok‑statis muncul **sebelum** delay selesai, mengonfirmasi bahwa kelas dievaluasi terlebih dahulu.

## Step 5 – Why Use Public Class Fields Instead of a Constructor?

Anda mungkin bertanya mengapa kami tidak menulis:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

Kedua pendekatan berfungsi, tetapi **public class fields javascript** memberikan sintaks yang lebih bersih dan deklaratif. Field didefinisikan sekali, bukan di dalam setiap pemanggilan konstruktor, yang dapat lebih mudah dibaca ketika kelas menjadi lebih besar. Selain itu, blok statis tidak dapat ditempatkan di dalam konstruktor, sehingga memisahkan logika inisialisasi menjadi lebih natural.

## Step 6 – Adapting the Example for Real‑World Apps

Di produksi Anda sering membutuhkan lebih dari satu penghitung. Berikut beberapa ide cepat:

- **Multiple counters:** Simpan mereka dalam `Map` yang di‑key oleh identifier.
- **Persisted state:** Ganti `console.log` dengan penulisan ke `localStorage`.
- **Async initialization:** Gunakan blok statis untuk mengambil konfigurasi dari server sebelum instance apa pun dibuat.

Semua pola ini tetap mendapat manfaat dari top‑level await, karena Anda dapat mengambil data sekali saat modul dimuat dan menjamin siap untuk setiap konsumen.

## Frequently Asked Questions

**Q: Apakah top‑level await memblokir modul lain?**  
A: Tidak. Setiap modul berjalan secara independen. Hanya modul yang berisi await yang dijeda; modul lain terus memuat secara paralel.

**Q: Bagaimana jika promise delay ditolak?**  
A: Penolakan yang tidak ditangani akan menghentikan evaluasi modul dan muncul sebagai error di konsol. Bungkus await dengan `try…catch` jika Anda memerlukan fallback yang elegan.

**Q: Apakah kata kunci `static` diperlukan?**  
A: Tidak untuk penghitung itu sendiri, tetapi blok statis merupakan cara praktis untuk menunjukkan bahwa kode dijalankan *sekali* pada saat pemuatan—bagus untuk logging atau deteksi fitur.

## Conclusion

Anda baru saja membangun **top level await example** yang menampilkan `await delay javascript`, sebuah **increment counter class**, dan kekuatan **public class fields javascript**. Potongan kode lengkap yang dapat dijalankan berada di atas, dan output konsol membuktikan bahwa blok statis dijalankan sebelum kode delay dieksekusi.  

Dari sini Anda dapat bereksperimen dengan alur async yang lebih kompleks, mengganti delay dengan panggilan API nyata, atau memperluas kelas dengan metode tambahan. Ingat, JavaScript modern memungkinkan Anda memperlakukan modul sebagai entitas async kelas‑satu—tanpa pembungkus tambahan.

Selamat coding, dan silakan bagikan variasi Anda di komentar. Jika panduan ini berguna, bagikan kepada rekan yang masih bergulat dengan pola async!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}