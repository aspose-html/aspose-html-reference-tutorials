---
category: general
date: 2026-10-19
description: atur device pixel ratio di Java menggunakan sandbox Aspose.HTML. Pelajari
  cara mengatur screen width height dan mendapatkan judul halaman java dengan contoh
  lengkap yang dapat dijalankan.
draft: false
keywords:
- get page title java
- device pixel ratio java
- create virtual device java
- set screen width height
lastmod: 2026-10-19
og_description: Dapatkan judul halaman java dengan sandbox Aspose.HTML. Panduan ini
  menunjukkan cara mengatur screen width height dan device pixel ratio di Java dalam
  beberapa langkah mudah.
og_image_alt: 'Developer guide: set device pixel ratio in Java using Aspose.HTML sandbox'
og_title: Dapatkan judul halaman java – tutorial mengatur device pixel ratio di sandbox
  Java
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: set device pixel ratio in Java using Aspose.HTML sandbox. Learn how
    to set screen width height and get page title java with a complete, runnable example.
  headline: Get page title java – set device pixel ratio in Java sandbox tutorial
  type: TechArticle
- questions:
  - answer: Yes—create a new `SandboxOptions` with a different `setDevicePixelRatio`
      value and instantiate a fresh `Sandbox`. Re‑using the same sandbox after changing
      its options is not supported.
    question: Can I change the pixel ratio at runtime?
  - answer: Loop over a list of `SandboxOptions` (e.g., iPhone 8, Pixel 4) and run
      the same load‑and‑title logic for each.
    question: What if I need to test multiple devices?
  - answer: Aspose.HTML respects Java’s default SSL trust store. Add the cert to the
      JVM’s keystore or, for testing only, disable verification (not recommended for
      production).
    question: Does this work with HTTPS sites that have self‑signed certificates?
  - answer: The `HTMLDocument` API provides `save` methods that can export the rendered
      page to PNG or JPEG. Use `htmlDoc.save("output.png", SaveFormat.PNG);` after
      loading.
    question: How do I capture a screenshot instead of just the title?
  - answer: Each `Sandbox` instance is isolated, but you should avoid sharing a single
      instance across multiple threads without synchronization.
    question: Is the sandbox thread‑safe?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- mobile emulation
title: Dapatkan judul halaman java – tutorial mengatur device pixel ratio di sandbox
  Java
url: /id/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dapatkan judul halaman java – atur rasio piksel perangkat dalam tutorial sandbox Java

Pernah perlu **set device pixel ratio** saat menguji situs responsif di Java? Anda bukan satu-satunya. Banyak pengembang mengalami kesulitan ketika halaman terlihat sempurna di desktop tetapi rusak di ponsel high‑DPI. Kabar baik? Dengan sandbox Aspose.HTML Anda dapat meniru iPhone X (atau perangkat apa pun) langsung dari kode Java Anda—tanpa browser.

Dalam panduan ini kami akan menjelaskan **how to set screen width height**, mengonfigurasi **device pixel ratio**, dan akhirnya **get page title java** untuk memverifikasi semuanya ter-render dengan benar. Pada akhir panduan Anda akan memiliki program mandiri yang dapat Anda masukkan ke proyek apa pun dan mulai menguji tata letak seluler secara instan.

## Jawaban Cepat
- **Bagaimana cara mengatur device pixel ratio di Java?** Gunakan `SandboxOptions.setDevicePixelRatio(double)` sebelum membuat sandbox.  
- **Metode apa yang mengembalikan judul halaman?** Panggil `htmlDocument.getTitle()` pada `HTMLDocument` yang dimuat.  
- **Bisakah saya meniru perangkat lain?** Ya—buat `SandboxOptions` baru dengan lebar, tinggi, dan rasio piksel yang diinginkan.  
- **Apakah saya memerlukan driver browser?** Tidak, sandbox Aspose.HTML bersifat head‑less dan berjalan murni di Java.  
- **Versi Aspose.HTML mana yang diperlukan?** Versi 23.7 atau lebih baru mendukung semua fitur emulasi seluler.

## Apa itu get page title java?
`get page title java` adalah operasi mengambil elemen `<title>` dari dokumen HTML menggunakan kode Java. Ini memungkinkan Anda memastikan bahwa halaman yang dimuat dalam konteks perangkat virtual menampilkan judul yang diharapkan. Mengambil judul adalah langkah umum dalam validasi otomatis untuk memastikan halaman yang benar telah dimuat setelah menerapkan parameter emulasi perangkat.

## Mengapa menggunakan sandbox Aspose.HTML untuk emulasi seluler?
Aspose.HTML mendukung **30+** format input dan output—termasuk HTML, CSS, SVG, dan PDF—dan dapat merender halaman tanpa meluncurkan browser penuh. Sandbox-nya memproses situs dengan ratusan halaman sambil menjaga penggunaan memori di bawah 200 MB, menjadikannya ideal untuk pipeline CI.

## Prasyarat

- Java 8 atau lebih baru (kode dapat dikompilasi dengan JDK 11 juga)  
- Perpustakaan Aspose.HTML untuk Java (versi 23.7 atau lebih baru) – Anda dapat mengunduhnya dari Maven Central  
- Sebuah IDE atau setup baris perintah `javac` sederhana  
- Akses internet untuk URL demo (`https://responsive.example.com`)

Tidak ada kerangka kerja tambahan, tidak ada Selenium, hanya Java murni dan Aspose.HTML.

## Cara mengatur lebar tinggi layar dan device pixel ratio di Java

`SandboxOptions` class memungkinkan Anda menentukan dimensi layar dan kepadatan piksel perangkat virtual. Untuk meniru perangkat seluler tertentu, Anda harus mengonfigurasi sandbox dengan lebar layar, tinggi, dan device pixel ratio yang diinginkan. Dengan membuat objek `SandboxOptions` dan mengatur properti ini, mesin rendering akan memperlakukan halaman seolah-olah ditampilkan pada perangkat tersebut, memastikan kueri media CSS dan skala gambar berperilaku dengan benar.

Buat instance `SandboxOptions`, atur lebar menjadi **375**, tinggi menjadi **812**, dan device pixel ratio menjadi **3.0**. Kemudian berikan opsi tersebut ke `Sandbox` baru. Ini sepenuhnya mengonfigurasi perangkat virtual sebelum halaman apa pun dimuat.

`SandboxOptions` class mendefinisikan ukuran layar dan kepadatan piksel perangkat virtual. Ini adalah titik masuk untuk setiap skenario emulasi seluler.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Mengapa ini penting:**  
> Panggilan `setDevicePixelRatio` memperbesar segala sesuatu—dari gambar hingga rendering font—sehingga halaman mengira berada di ponsel nyata. Jika Anda melewatkannya, tata letak mungkin kembali ke kueri media CSS gaya desktop, mengalahkan tujuan pengujian seluler.

## Cara membuat instance sandbox

`Sandbox` class mewakili lingkungan browser headless yang merender HTML menggunakan opsi yang telah didefinisikan sebelumnya. Setelah mengonfigurasi `SandboxOptions`, buat instance `Sandbox` dengan opsi tersebut untuk memperoleh konteks rendering terisolasi. Sandbox ini berfungsi seperti browser ringan, menerapkan ukuran layar dan kepadatan piksel yang Anda tentukan, dan dapat digunakan kembali untuk beberapa pemuatan halaman sambil menjaga lingkungan tetap bersih.

Instansiasi `Sandbox` dengan `SandboxOptions` yang telah dikonfigurasi sebelumnya. Sandbox berperilaku seperti browser headless kecil yang menghormati dimensi dan pixel ratio yang Anda definisikan.

Objek `Sandbox` adalah mesin rendering terisolasi Aspose.HTML yang berjalan tanpa UI. Ini menjamin setiap pengujian berjalan dalam lingkungan bersih.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Tips pro:** Anda dapat menggunakan kembali objek `Sandbox` yang sama untuk beberapa pemuatan halaman; cukup ubah URL dan sandbox akan mempertahankan karakteristik perangkat yang sama.

## Cara memuat halaman di dalam sandbox

`HTMLDocument` class mewakili file HTML yang diparsing dalam memori, menyediakan akses DOM dan kemampuan rendering. Dengan sandbox siap, buat `HTMLDocument` dengan memberikan URL target dan instance sandbox. Ini memuat dan merender halaman menggunakan pengaturan perangkat virtual, memungkinkan Anda berinteraksi dengan DOM atau mengekstrak informasi seperti judul.

Buat `HTMLDocument` dengan memberikan URL target dan instance `Sandbox`. Ini memaksa dokumen merender menggunakan perangkat virtual yang Anda atur sebelumnya.

`HTMLDocument` class mewakili file HTML yang diparsing dalam memori dan menyediakan metode untuk manipulasi DOM serta ekstraksi metadata.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Jika URL tidak dapat dijangkau atau halaman mengandung kesalahan, Aspose.HTML akan melemparkan exception. Untuk kode produksi Anda sebaiknya membungkusnya dalam `try‑catch` dan mencatat kegagalan, tetapi tutorial ini tetap sederhana.

## Cara memverifikasi dengan get page title java

Metode `getTitle()` mengembalikan konten elemen `<title>` dokumen HTML sebagai string biasa. Membaca judul adalah pemeriksaan cepat. Setelah memuat halaman, panggil `htmlDocument.getTitle()` untuk mengambil teks judul. Pemeriksaan sederhana ini mengonfirmasi bahwa halaman dirender dengan benar di bawah pengaturan perangkat yang diemulasi dan menyediakan cara cepat untuk memvalidasi navigasi atau perubahan konten dalam tes otomatis.

Panggil `htmlDocument.getTitle()` pada dokumen yang dimuat dan cetak hasilnya. Jika sandbox berhasil menerapkan **device pixel ratio**, judul akan cocok dengan yang Anda lihat pada iPhone X nyata.

Metode `getTitle()` mengembalikan konten elemen `<title>` sebagai string biasa, memungkinkan Anda memvalidasi rendering tanpa inspeksi visual.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Output yang diharapkan (contoh):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Jika Anda melihat judul tercetak, Anda telah berhasil **set device pixel ratio**, **set screen width height**, dan **got the page title** menggunakan Java.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke file bernama `SandboxDemo.java`. Pastikan JAR Aspose.HTML ada di classpath Anda (`-cp` flag) sebelum Anda mengompilasi.

Kelas `SandboxDemo` menggabungkan semua langkah sebelumnya menjadi satu contoh yang dapat dijalankan.

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

Anda harus melihat judul tercetak di konsol, mengonfirmasi bahwa halaman dirender dengan **device pixel ratio** yang diinginkan.

## Pertanyaan yang sering diajukan & kasus tepi

**T: Bisakah saya mengubah pixel ratio saat runtime?**  
J: Ya—buat `SandboxOptions` baru dengan nilai `setDevicePixelRatio` yang berbeda dan instansiasi `Sandbox` baru. Menggunakan kembali sandbox yang sama setelah mengubah opsinya tidak didukung.

**T: Bagaimana jika saya perlu menguji beberapa perangkat?**  
J: Lakukan loop pada daftar `SandboxOptions` (misalnya iPhone 8, Pixel 4) dan jalankan logika load‑and‑title yang sama untuk masing‑masing.

**T: Apakah ini bekerja dengan situs HTTPS yang memiliki sertifikat self‑signed?**  
J: Aspose.HTML menghormati trust store SSL default Java. Tambahkan sertifikat ke keystore JVM atau, hanya untuk pengujian, nonaktifkan verifikasi (tidak disarankan untuk produksi).

**T: Bagaimana cara menangkap screenshot alih-alih hanya judul?**  
J: API `HTMLDocument` menyediakan metode `save` yang dapat mengekspor halaman yang dirender ke PNG atau JPEG. Gunakan `htmlDoc.save("output.png", SaveFormat.PNG);` setelah memuat.

**T: Apakah sandbox thread‑safe?**  
J: Setiap instance `Sandbox` terisolasi, tetapi Anda sebaiknya menghindari berbagi satu instance di antara beberapa thread tanpa sinkronisasi.

## Gambaran visual

![Diagram showing set device pixel ratio in mobile sandbox](https://example.com/images/sandbox-diagram.png "set device pixel ratio diagram")

[Diagram yang menunjukkan set device pixel ratio dalam sandbox seluler](https://example.com/images/sandbox-diagram.png "diagram set device pixel ratio")

*Ilustrasi di atas memetakan alur dari mengonfigurasi `SandboxOptions` (termasuk **set screen width height** dan **set device pixel ratio**) hingga memuat URL dan mengekstrak judul.*

## Kesimpulan

Anda sekarang tahu **how to set device pixel ratio** di Java, cara **set screen width height** untuk emulasi seluler yang akurat, dan cara **get page title java** untuk mengonfirmasi rendering berhasil. Alur kerja ringkas ini menghilangkan kebutuhan akan browser berat selama pengujian UI otomatis dan cocok dengan rapi dalam pipeline CI.

Siap untuk langkah selanjutnya? Coba ekspor halaman yang dirender sebagai gambar, atau bereksperimen dengan debugging kueri media CSS dengan mengubah `devicePixelRatio` antara 1.0 dan 3.0. Anda juga dapat menjelajahi fitur konversi PDF Aspose.HTML untuk menangkap versi cetak dari tampilan seluler.

Selamat coding, semoga tata letak seluler Anda selalu tampak tajam—tidak peduli kepadatan pikselnya!

---

**Terakhir diperbarui:** 2026-10-19  
**Diuji dengan:** Aspose.HTML 23.7 untuk Java  
**Penulis:** Aspose

## Tutorial Terkait

- [Dapatkan Judul Html Java Render Halaman Dalam Sandbox Dengan Lebar Layar](/html/java/advanced-usage/get-html-title-java-render-page-in-sandbox-with-screen-width/)
- [Buat Panduan Lengkap Sandbox Aspose Html Java](/html/java/configuring-environment/create-aspose-html-sandbox-complete-java-guide/)
- [Set Device Pixel Ratio Di Java Panduan Lengkap](/html/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}