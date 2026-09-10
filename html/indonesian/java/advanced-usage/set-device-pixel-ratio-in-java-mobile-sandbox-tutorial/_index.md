---
category: general
date: 2026-02-10
description: atur rasio piksel perangkat di Java menggunakan sandbox Aspose.HTML.
  Pelajari cara mengatur lebar dan tinggi layar serta mendapatkan judul halaman Java
  dengan contoh lengkap yang dapat dijalankan.
draft: false
keywords:
- set device pixel ratio
- get page title java
- set screen width height
language: id
og_description: atur rasio piksel perangkat di Java dengan sandbox Aspose.HTML. Panduan
  ini menunjukkan cara mengatur lebar dan tinggi layar serta mendapatkan judul halaman
  Java dalam beberapa langkah mudah.
og_title: Atur Rasio Piksel Perangkat di Java – Tutorial Mobile Sandbox
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Atur rasio piksel perangkat di Java – Tutorial Mobile Sandbox
url: /id/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengatur device pixel ratio di Java – Tutorial Mobile Sandbox

Pernahkah Anda perlu **set device pixel ratio** saat menguji situs responsif di Java? Anda bukan satu-satunya. Banyak pengembang mengalami kesulitan ketika halaman terlihat sempurna di desktop tetapi rusak di ponsel high‑DPI. Kabar baiknya? Dengan sandbox Aspose.HTML Anda dapat meniru iPhone X (atau perangkat apa pun) langsung dari kode Java Anda—tanpa browser.

Dalam panduan ini kami akan menjelaskan **how to set screen width height**, mengonfigurasi **device pixel ratio**, dan akhirnya **get page title java** untuk memverifikasi semuanya ter-render dengan benar. Pada akhir tutorial Anda akan memiliki program mandiri yang dapat Anda masukkan ke proyek apa pun dan langsung mulai menguji tata letak seluler.

## Prasyarat

- Java 8 atau lebih baru (kode juga dapat dikompilasi dengan JDK 11)  
- Aspose.HTML for Java library (versi 23.7 atau lebih baru) – Anda dapat mengambilnya dari Maven Central  
- IDE atau setup baris perintah `javac` sederhana  
- Akses internet untuk URL demo (`https://responsive.example.com`)

Tidak ada kerangka kerja tambahan, tidak ada Selenium, hanya Java murni dan Aspose.HTML.

---

## Langkah 1: Set screen width height dan device pixel ratio

Hal pertama yang kita butuhkan adalah objek `SandboxOptions` yang memberi tahu sandbox perangkat “yang” kita pura-pura menjadi. Di sini kita akan menggunakan dimensi iPhone X (375 × 812 piksel CSS) dan **device pixel ratio** sebesar 3.0, yang meniru tampilan retina high‑DPI.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Mengapa ini penting:**  
> Panggilan `setDevicePixelRatio` memperbesar segala sesuatu—dari gambar hingga rendering font—sehingga halaman mengira berada di ponsel nyata. Jika Anda melewatkannya, tata letak mungkin kembali ke media query CSS gaya desktop, menghilangkan tujuan pengujian seluler.

---

## Langkah 2: Buat instance sandbox

Sekarang kami mengubah opsi tersebut menjadi sandbox yang aktif. Anggap sandbox sebagai browser kecil tanpa tampilan (headless) yang menghormati dimensi dan pixel ratio yang baru saja kita definisikan.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Tips pro:** Anda dapat menggunakan kembali objek `Sandbox` yang sama untuk memuat beberapa halaman; cukup ubah URL dan sandbox akan mempertahankan karakteristik perangkat yang sama.

---

## Langkah 3: Muat halaman di dalam sandbox

Dengan sandbox siap, memuat halaman semudah membuat `HTMLDocument` dan memberikan sandbox sebagai argumen kedua. Ini memaksa dokumen merender menggunakan perangkat virtual yang telah kita atur sebelumnya.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Jika URL tidak dapat dijangkau atau halaman mengandung kesalahan, Aspose.HTML akan melemparkan pengecualian. Untuk kode produksi Anda mungkin akan membungkusnya dalam `try‑catch` dan mencatat kegagalan, tetapi untuk tutorial ini kami tetap sederhana.

---

## Langkah 4: Verifikasi dengan get page title java

Pemeriksaan cepat paling sederhana adalah membaca judul dokumen. Jika sandbox berhasil menerapkan **device pixel ratio**, judulnya akan identik dengan yang Anda lihat pada iPhone X nyata.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Output yang diharapkan (contoh):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Jika Anda melihat judul tercetak, Anda telah berhasil **set device pixel ratio**, **set screen width height**, dan **got the page title** menggunakan Java.

---

## Contoh Lengkap yang Dapat Dijalankan

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke file bernama `SandboxDemo.java`. Pastikan JAR Aspose.HTML berada di classpath Anda (`-cp` flag) sebelum Anda mengompilasi.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.net.URL;

/**
 * Demonstrates how to set device pixel ratio, set screen width height,
 * and get page title java using Aspose.HTML sandbox.
 */
public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define device characteristics ----------
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixels width
        sandboxOptions.setScreenHeight(812);         // CSS pixels height
        sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI screen factor (set device pixel ratio)

        // ---------- Step 2: Create the sandbox ----------
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // ---------- Step 3: Load a web page inside the sandbox ----------
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("https://responsive.example.com"), mobileSandbox);

        // ---------- Step 4: Verify the document loaded correctly ----------
        System.out.println("Title under sandbox: " + htmlDoc.getTitle());
    }
}
```

Kompilasi dan jalankan:

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

Anda akan melihat judul tercetak di konsol, mengonfirmasi bahwa halaman dirender dengan **device pixel ratio** yang diinginkan.

---

## Pertanyaan yang Sering Diajukan & Kasus Tepi

| Pertanyaan | Jawaban |
|------------|---------|
| **Apakah saya dapat mengubah pixel ratio saat runtime?** | Ya—cukup buat `SandboxOptions` baru dengan nilai `setDevicePixelRatio` yang berbeda dan buat `Sandbox` baru. Menggunakan kembali sandbox yang sama setelah mengubah opsinya tidak didukung. |
| **Bagaimana jika saya perlu menguji beberapa perangkat?** | Iterasi melalui daftar `SandboxOptions` (misalnya iPhone 8, Pixel 4) dan jalankan logika load‑and‑title yang sama untuk masing‑masing. |
| **Apakah ini bekerja dengan situs HTTPS yang memiliki sertifikat self‑signed?** | Aspose.HTML menghormati trust store SSL default Java. Tambahkan sertifikat ke keystore JVM atau nonaktifkan verifikasi hanya untuk pengujian (tidak disarankan untuk produksi). |
| **Bagaimana cara mengambil screenshot alih-alih hanya judul?** | API `HTMLDocument` menyediakan metode `save` yang dapat mengekspor halaman yang dirender ke PNG atau JPEG. Gunakan `htmlDoc.save("output.png", SaveFormat.PNG);` setelah memuat. |
| **Apakah sandbox thread‑safe?** | Setiap instance `Sandbox` terisolasi, tetapi Anda sebaiknya menghindari berbagi satu instance di antara beberapa thread tanpa sinkronisasi. |

---

## Gambaran Visual

![Diagram yang menunjukkan set device pixel ratio dalam mobile sandbox](https://example.com/images/sandbox-diagram.png "diagram set device pixel ratio")

*Ilustrasi di atas memetakan alur dari konfigurasi `SandboxOptions` (termasuk **set screen width height** dan **set device pixel ratio**) hingga memuat URL dan mengekstrak judul.*

---

## Kesimpulan

Anda kini mengetahui **how to set device pixel ratio** di Java, cara **set screen width height** untuk emulasi seluler yang akurat, dan cara **get page title java** untuk mengonfirmasi bahwa rendering berhasil. Alur kerja ringkas ini menghilangkan kebutuhan akan browser berat selama pengujian UI otomatis dan cocok dimasukkan ke dalam pipeline CI.

Siap untuk langkah selanjutnya? Cobalah mengekspor halaman yang dirender sebagai gambar, atau bereksperimen dengan debugging media‑query CSS dengan mengubah `devicePixelRatio` antara 1.0 dan 3.0. Anda juga dapat menjelajahi fitur konversi PDF Aspose.HTML untuk menangkap versi cetak dari tampilan seluler.

Selamat coding, semoga tata letak seluler Anda selalu tampak tajam—tanpa mempedulikan kepadatan piksel!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}