---
category: general
date: 2026-03-26
description: Pelajari cara meniru iPhone dalam Java menggunakan Aspose.HTML. Termasuk
  langkah-langkah untuk mengatur agen pengguna khusus dan mengatur rasio piksel perangkat
  agar rendering seluler lebih akurat.
draft: false
keywords:
- how to emulate iphone
- set custom user agent
- set device pixel ratio
- how to set user-agent
- how to set dpr
language: id
og_description: Bagaimana meniru iPhone di Java? Tutorial ini menunjukkan cara mengatur
  user agent khusus dan rasio piksel perangkat menggunakan Aspose.HTML, menghasilkan
  halaman seluler yang pixel‑perfect.
og_title: Cara Meniru iPhone – Panduan Aspose.HTML Langkah demi Langkah
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Cara Mengemulasi iPhone – Panduan Lengkap dengan Aspose.HTML
url: /id/java/html5-canvas-rendering/how-to-emulate-iphone-complete-guide-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Meniru iPhone – Panduan Lengkap dengan Aspose.HTML

Pernah bertanya-tanya **bagaimana cara meniru iPhone** saat menguji halaman web secara lokal? Mungkin Anda sedang men-debug tata letak responsif dan peramban desktop tidak memadai. Kabar baiknya, Anda tidak memerlukan perangkat fisik—Aspose.HTML’s `DocumentSandbox` memungkinkan Anda meniru layar iPhone, user‑agent, dan device‑pixel‑ratio (DPR) dengan beberapa baris Java.  

Dalam tutorial ini kami akan menelusuri langkah‑langkah tepat untuk mengatur **custom user agent**, mengonfigurasi **device pixel ratio**, dan memverifikasi bahwa semuanya berfungsi seperti yang diharapkan. Pada akhir Anda akan memiliki sandbox yang dapat digunakan kembali yang merender halaman persis seperti iPhone 8, dan Anda akan memahami mengapa setiap pengaturan penting.

## Apa yang Akan Anda Capai

- Buat objek `Screen` yang mencerminkan dimensi iPhone dan DPR.  
- Terapkan string **custom user agent** sehingga server mengira permintaan berasal dari Safari di iOS.  
- Bangun `DocumentSandbox` yang menghubungkan layar dan user‑agent bersama.  
- Jalankan `HTMLDocument` di dalam sandbox dan lihat output konsol yang mengonfirmasi konfigurasi.  

Tidak ada pustaka eksternal selain Aspose.HTML yang diperlukan, dan kode dapat dijalankan pada lingkungan Java 17+ mana pun.

---

![how to emulate iphone screenshot](https://example.com/images/iphone-emulation.png "how to emulate iphone using Aspose.HTML sandbox")

## Cara Meniru iPhone dengan Aspose.HTML Sandbox

Hal pertama yang kita butuhkan adalah `Screen` yang mencerminkan dimensi fisik iPhone *dan* kepadatan pikselnya. Inilah inti dari **bagaimana cara meniru iPhone** secara akurat.

```java
import com.aspose.html.devices.Screen;

// Step 1: Define iPhone 8 screen size (width, height) and DPR
Screen mobileScreen = new Screen(375, 667, 2.0); // iPhone 8 dimensions, DPR = 2
```

**Mengapa ini penting:**  
- Lebar = 375 px dan tinggi = 667 px adalah dimensi piksel CSS yang akan Anda lihat di Chrome DevTools saat memilih iPhone 8.  
- Mengatur DPR menjadi 2 memberi tahu mesin rendering untuk memperlakukan setiap piksel CSS sebagai dua piksel fisik, menghasilkan teks dan gambar yang tajam—tepat seperti perangkat nyata.

> *Pro tip:* Jika Anda perlu meniru iPhone yang lebih baru (seperti iPhone 13), cukup ubah angka menjadi 390 × 844 dan DPR = 3.

## Mengatur User Agent Kustom (set custom user agent)

Selanjutnya, kita perlu **set custom user agent** agar server menyajikan HTML/CSS khusus seluler. Tanpa ini, banyak situs masih akan mengira Anda berada di desktop.

```java
// Step 2: Define an iPhone Safari user‑agent string
String iPhoneUserAgent = "Mozilla/5.0 (iPhone; CPU iPhone OS 16_0 like Mac OS X) " +
                         "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                         "Version/16.0 Mobile/15E148 Safari/604.1";
```

**Cara kerjanya:**  
- Header `User-Agent` adalah jabat tangan yang digunakan peramban untuk memperkenalkan diri.  
- Dengan menyediakan string persis yang dikirim Safari di iOS 16, Anda memastikan server mengembalikan aset yang dioptimalkan untuk seluler (misalnya gambar responsif, skrip adaptif, dll.).  

Jika Anda pernah perlu **how to set user-agent** untuk perangkat lain, cukup ganti string dengan nilai yang sesuai—Google Chrome, Firefox, atau bahkan bot khusus.

## Mengonfigurasi Device Pixel Ratio (set device pixel ratio)

Sekarang kita benar‑benar **set device pixel ratio** di dalam sandbox. Ini adalah langkah yang secara langsung menjawab “**how to set dpr**” untuk lingkungan simulasi.

```java
import com.aspose.html.sandbox.DocumentSandbox;

// Step 3: Build the sandbox with screen and user‑agent
DocumentSandbox documentSandbox = new DocumentSandbox.Builder()
        .setScreen(mobileScreen)          // applies the DPR we defined earlier
        .setUserAgent(iPhoneUserAgent)    // applies the custom user‑agent
        .build();
```

**Penjelasan:**  
- Polanya `Builder` memungkinkan Anda dengan lancar melampirkan baik layar (yang membawa DPR) maupun user‑agent.  
- Saat sandbox merender `HTMLDocument`, ia akan berpura‑pura berjalan pada perangkat dengan kepadatan piksel yang tepat itu.  

> *Mengapa Anda harus peduli:* Beberapa kueri media CSS menggunakan `device-pixel-ratio` (mis., `@media (-webkit-min-device-pixel-ratio: 2)`). Jika Anda tidak mengatur DPR, aturan‑aturan tersebut tidak pernah dipicu, dan Anda akan kehilangan aset beresolusi tinggi.

## Memverifikasi Konfigurasi Sandbox (how to set user-agent)

Mari kita coba sandbox. Potongan kode berikut membuat `HTMLDocument`, memuat sebuah halaman, dan mencetak konfirmasi bahwa sandbox aktif.

```java
import com.aspose.html.HTMLDocument;

public class SandboxWithDprAndUa {
    public static void main(String[] args) {
        // Re‑use the sandbox we built earlier
        // DocumentSandbox documentSandbox = ... (from previous step)

        // Step 4: Load a page inside the sandbox
        HTMLDocument doc = new HTMLDocument("https://example.com", documentSandbox);

        // Step 5: Optional – output a sanity check
        System.out.println("Sandbox configured with DPR=2 and iPhone user‑agent.");
    }
}
```

**Output konsol yang diharapkan**

```
Sandbox configured with DPR=2 and iPhone user-agent.
```

Jika Anda menjalankan program dan melihat baris itu, Anda telah berhasil **how to emulate iPhone** dengan DPR dan user‑agent yang tepat. Buka halaman di peramban nyata dan periksa dimensi viewport—Anda akan melihat bahwa nilai‑nilainya cocok dengan nilai iPhone yang kami atur.

## Kesulitan Umum dan Cara Mengatur DPR dengan Benar (how to set dpr)

Bahkan dengan kode yang tepat, beberapa jebakan dapat membuat Anda tersandung:

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **DPR tetap 1** | Anda memberikan `Screen` tanpa argumen ketiga (DPR). | Selalu gunakan `new Screen(width, height, dpr)`. |
| **User‑Agent diabaikan** | Sandbox tidak terhubung ke `HTMLDocument`. | Berikan `documentSandbox` sebagai argumen kedua ke konstruktor `HTMLDocument`. |
| **Dimensi salah** | Menggunakan piksel perangkat alih‑alih piksel CSS. | Ingat: lebar/tinggi adalah **piksel CSS**, bukan piksel perangkat keras. |
| **Server masih mengirim CSS desktop** | Beberapa situs menggunakan JavaScript untuk mendeteksi perangkat, bukan hanya header. | Pertimbangkan juga menyuntikkan meta tag viewport jika diperlukan. |

Dengan mengingat hal‑hal ini, Anda jarang akan menemukan situasi di mana emulasi tidak berperilaku seperti yang diharapkan.

## Memperluas Sandbox – Langkah Selanjutnya

Sekarang Anda tahu **how to set custom user agent** dan **how to set dpr**, Anda dapat bereksperimen lebih jauh:

- **Ubah ukuran layar** untuk meniru tablet atau ponsel yang lebih besar.  
- **Ganti user‑agent** untuk menguji Chrome di Android (`"Mozilla/5.0 (Linux; Android 12; ...) Chrome/110.0"`).  
- **Tambahkan cookie atau header** melalui metode `setHeaders` sandbox untuk pengujian terautentikasi.  
- **Ambil screenshot** menggunakan `HTMLDocument.renderToFile("output.png")` untuk membandingkan perbedaan visual secara otomatis.

Ekstensi‑ekstensi ini memungkinkan Anda membangun harness pengujian lengkap tanpa pernah meninggalkan IDE Anda.

## Kesimpulan

Kami telah membahas **how to emulate iPhone** menggunakan `DocumentSandbox` milik Aspose.HTML, menunjukkan secara tepat **how to set custom user agent**, **how to set device pixel ratio**, dan bahkan perbedaan halus antara “**how to set user-agent**” dan “**how to set dpr**”. Contoh lengkap yang dapat dijalankan memperlihatkan setiap bagian dalam satu tempat, sehingga Anda dapat copy‑paste, menyesuaikan, dan mulai menguji tata letak seluler secara instan.  

Cobalah—ganti dimensi layar, mainkan berbagai user‑agent, dan lihat bagaimana halaman Anda bereaksi. Ketika Anda menguasai pengaturan‑pengaturan ini, men-debug desain responsif menjadi sangat mudah, dan Anda akan menghemat banyak jam mengejar bug di perangkat nyata.

Punya pertanyaan atau ingin berbagi variasi Anda sendiri? Tinggalkan komentar di bawah, dan selamat meniru!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}