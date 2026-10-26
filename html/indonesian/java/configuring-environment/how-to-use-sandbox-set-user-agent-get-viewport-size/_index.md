---
category: general
date: 2026-04-03
description: Pelajari cara menggunakan sandbox di Aspose.HTML Java untuk mengatur
  user agent, mengatur ukuran, dan mendapatkan ukuran viewport secara instan. Kode
  lengkap, penjelasan, dan tips disertakan.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: id
og_description: Pelajari cara menggunakan sandbox di Aspose.HTML Java untuk mengatur
  user agent, mengatur ukuran, dan mendapatkan ukuran viewport secara instan. Panduan
  lengkap dengan kode dan praktik terbaik.
og_title: Cara Menggunakan Sandbox – Atur User Agent & Dapatkan Ukuran Viewport
tags:
- AsposeHTML
- Java
- Sandbox
title: Cara Menggunakan Sandbox – Atur User Agent & Dapatkan Ukuran Viewport
url: /id/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Sandbox – Mengatur User Agent & Mendapatkan Ukuran Viewport

Pernah bertanya-tanya **bagaimana cara menggunakan sandbox** saat merender HTML dengan Aspose.HTML for Java? Mungkin Anda mengalami kebuntuan saat mencoba mensimulasikan ukuran layar tertentu atau perlu memalsukan string user‑agent agar halaman berperilaku seolah‑olah diakses dari browser seluler.  

Kabar baiknya, API sandbox memungkinkan Anda melakukan hal tersebut, dan Anda juga dapat mengambil ukuran viewport yang dihitung setelah halaman dimuat. Dalam tutorial ini kami akan menuntun Anda melalui pembuatan sandbox, mengatur ukuran, mengatur user agent khusus, memuat halaman remote, dan akhirnya membaca dimensi viewport. Pada akhir tutorial Anda akan mengetahui **cara mengatur ukuran**, **cara mendapatkan viewport**, dan mengapa langkah‑langkah ini penting untuk rendering headless yang dapat diandalkan.

> **Quick win:** Anda akan memiliki kelas Java yang dapat dijalankan dan mencetak sesuatu seperti `Viewport: 1280×800` dalam hitungan detik.

---

## Apa yang Anda Butuhkan

- **Aspose.HTML for Java** versi 24.6 atau lebih baru (API yang kami gunakan diperkenalkan pada 24.5).  
- Kit pengembangan Java 17+ (sembarang JDK terbaru dapat dipakai).  
- IDE atau editor teks sederhana—tidak memerlukan plugin khusus.  
- Akses internet jika Anda ingin memuat URL eksternal seperti `https://example.com`.

Itu saja. Tidak ada keharusan menggunakan Maven/Gradle; Anda dapat menaruh JAR secara manual ke classpath jika lebih suka.  

---

## Cara Menggunakan Sandbox – Ikhtisar

Sandbox memisahkan mesin rendering dari sistem operasi host, memungkinkan Anda mendefinisikan layar virtual (lebar, tinggi, DPI) dan string **user agent** khusus. Anggaplah ini sebagai jendela browser miniatur yang sepenuhnya berada di memori. Ketika Anda kemudian meminta `HTMLDocument` untuk tampilan defaultnya, mesin akan melaporkan **ukuran viewport** yang dihitung berdasarkan pengaturan sandbox.  

Berikut alur tingkat tinggi:

1. **Buat** sebuah `DocumentSandbox` dan konfigurasikan lebar, tinggi, DPI, serta user‑agent.  
2. **Muat** sebuah `HTMLDocument` di dalam sandbox tersebut.  
3. **Tanya** tampilan default dokumen untuk ukuran viewport.  

Mari kita selami setiap langkah.

---

## Langkah 1: Buat Sandbox dan Atur Ukuran

Pertama, kami membuat sandbox dan memberi tahu berapa besar layar virtual yang harus dipakai. Di sinilah Anda menjawab pertanyaan **bagaimana cara mengatur ukuran** untuk render headless.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **Pro tip:** Jika Anda menguji layout responsif, coba lebar sempit seperti `360` untuk meniru ponsel, atau lebar lebar seperti `1920` untuk desktop. Sandbox menghormati DPI yang Anda set, sehingga layar ber‑density tinggi (misalnya 144 DPI) akan memengaruhi media‑queries yang menggunakan `device-pixel-ratio`.

---

## Langkah 2: Atur User Agent untuk Sandbox

Mengapa repot‑repot dengan **user agent** khusus? Beberapa situs menyajikan markup atau skrip yang berbeda tergantung pada browser yang dilaporkan. Dengan memanggil `setUserAgent` Anda dapat menipu halaman agar mengira sedang diakses dari Chrome, Firefox, atau perangkat seluler.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

Sekarang halaman akan mengira sedang dirender pada iPhone. Jika Anda perlu **mengatur user agent** kembali ke default, cukup gunakan string “AsposeHTML/24.6 …” yang sebelumnya.

---

## Langkah 3: Muat Dokumen HTML di Dalam Sandbox

Setelah sandbox siap, kami dapat memuat URL apa pun atau file HTML lokal. Konstruktor `HTMLDocument` menerima sandbox sebagai argumen kedua, mengikat keduanya bersama.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

Blok `try‑with‑resources` memastikan dokumen dibuang dengan benar, membebaskan sumber daya native yang dialokasikan Aspose.HTML di balik layar.

---

## Langkah 4: Dapatkan Ukuran Viewport dari Dokumen

Inilah momen yang Anda tunggu: mengambil **ukuran viewport** yang dihitung oleh mesin rendering. Ini menjawab **bagaimana cara mendapatkan viewport** setelah halaman selesai di‑layout.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

Saat Anda menjalankan program, Anda akan melihat sesuatu seperti:

```
Viewport: 1280×800
```

Jika Anda mengubah dimensi sandbox pada Langkah 1, angka yang tercetak akan mencerminkan nilai baru tersebut—sempurna untuk tes otomatis yang memverifikasi breakpoint responsif.

---

## Contoh Lengkap yang Siap Dijalan

Berikut adalah kelas lengkap yang siap dijalankan dan menggabungkan semua bagian. Salin‑tempel ke file bernama `SandboxExample.java`, tambahkan JAR Aspose.HTML ke classpath, dan jalankan `java SandboxExample`.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**Output yang diharapkan** (dengan pengaturan sandbox di atas):

```
Viewport: 1280×800
```

Jika Anda mengatur lebar/tinggi yang berbeda di sandbox, output akan berubah sesuai—tepat apa yang Anda butuhkan saat menguji desain responsif.

---

## Kasus Khusus & Pertanyaan Umum

### Bagaimana jika halaman menggunakan `window.innerWidth` alih‑alih media query CSS?

Ukuran layar virtual sandbox memengaruhi baik layout CSS maupun `window.innerWidth/innerHeight` pada JavaScript. Jadi **bagaimana cara mendapatkan viewport** melalui JavaScript akan mengembalikan angka yang sama seperti yang Anda lihat di konsol Java.

### Bisakah saya menjalankan beberapa sandbox secara paralel?

Ya. Setiap instance `DocumentSandbox` bersifat independen, sehingga Anda dapat membuat thread pool, memberi setiap thread sandboxnya masing‑masing dengan dimensi berbeda, dan merender puluhan halaman secara bersamaan. Pastikan JAR tetap thread‑safe (memang demikian).

### Apakah pengaturan DPI memengaruhi skala gambar?

Tentu saja. DPI yang lebih tinggi membuat satu piksel CSS dipetakan ke lebih banyak piksel perangkat, yang dapat membuat gambar beresolusi tinggi tampak lebih tajam. Jika Anda menguji aset gaya retina, coba `sandbox.setDeviceDpi(144)`.

### Bagaimana saya menangani sertifikat HTTPS yang self

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}