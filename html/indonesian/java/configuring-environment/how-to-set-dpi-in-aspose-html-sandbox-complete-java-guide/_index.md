---
category: general
date: 2026-04-02
description: Pelajari cara mengatur DPI, mengatur ukuran viewport, dan mengatur user
  agent di Aspose.HTML Sandbox. Contoh Java langkah demi langkah dengan kode lengkap
  dan tips.
draft: false
keywords:
- how to set dpi
- set viewport size
- set user agent
- Aspose.HTML sandbox
- Java rendering settings
language: id
og_description: Kuasi cara mengatur DPI, ukuran viewport, dan user agent di Aspose.HTML
  Sandbox dengan contoh Java lengkap.
og_title: Cara Mengatur DPI di Aspose.HTML Sandbox – Tutorial Java
tags:
- Aspose.HTML
- Java
- Rendering
- Sandbox
title: Cara Mengatur DPI di Aspose.HTML Sandbox – Panduan Lengkap Java
url: /id/java/configuring-environment/how-to-set-dpi-in-aspose-html-sandbox-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengatur DPI di Aspose.HTML Sandbox – Panduan Lengkap Java

Pernah bertanya-tanya **bagaimana cara mengatur DPI** saat merender halaman web dengan Aspose.HTML? Anda tidak sendirian. Dalam banyak skenario pengujian Anda perlu tata letak sesuai dengan kepadatan layar tertentu—bayangkan PDF siap cetak atau tangkapan layar resolusi tinggi. Kabar baiknya, sandbox Aspose.HTML memungkinkan Anda mengontrol DPI, ukuran viewport, dan bahkan string user‑agent dalam satu paket yang rapi.

Dalam tutorial ini kami akan membahas contoh Java praktis yang **mengatur DPI**, **mengatur ukuran viewport**, dan **mengatur user agent** sekaligus. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan, memahami mengapa setiap pengaturan penting, dan siap menyesuaikan sandbox untuk proyek Anda sendiri.

---

## Apa yang Anda Butuhkan

- **Java 17** (atau JDK terbaru; API kompatibel dengan Java 8+)
- **Aspose.HTML for Java** library (versi 23.12 atau lebih baru)
- Sebuah IDE atau editor teks sederhana + kompilasi baris perintah
- Akses internet untuk URL contoh (`https://example.com`)

Tidak diperlukan alat build eksternal; kode dapat dikompilasi dengan `javac` dan dijalankan dengan `java`. Jika Anda lebih suka Maven atau Gradle, cukup tambahkan dependensi Aspose.HTML—tidak ada yang rumit.

---

## Langkah 1: Buat Sandbox yang Menentukan Lingkungan Rendering

Sandbox adalah tempat Anda memberi tahu Aspose.HTML “layar” apa yang Anda pura-pura miliki. Di sini kami mengatur **viewport 1024 × 768**, **DPI 96**, dan string **user‑agent** khusus.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Define the sandbox – this is the core of how to set dpi, viewport, and user agent.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent
```

**Mengapa ini penting:**  
- **DPI** memengaruhi cara unit CSS `pt` diterjemahkan ke piksel; DPI yang lebih tinggi menghasilkan rendering yang lebih tajam.  
- **Ukuran viewport** menentukan breakpoint tata letak yang akan dipicu oleh CSS responsif.  
- **User‑agent** dapat memicu variasi konten sisi server (mobile vs desktop).

> **Tips pro:** Jika Anda akan menghasilkan PDF nanti, sesuaikan DPI dengan resolusi cetak target (mis., 300 dpi untuk cetakan berkualitas tinggi).

---

## Langkah 2: Muat Halaman Web di Dalam Sandbox

Sekarang kami mengarahkan sandbox ke sebuah URL. Konstruktor `HTMLDocument` menerima sandbox, sehingga mesin tata letak menghormati pengaturan yang baru saja kami definisikan.

```java
        // Load the page using the sandbox we just configured.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {
```

**Apa yang terjadi di balik layar?**  
Aspose.HTML membuat konteks rendering terisolasi, mirip dengan headless browser, tetapi tanpa beban penuh dari instance Chromium. Hal ini membuat operasi cepat dan ringan memori—sempurna untuk pemrosesan batch.

---

## Langkah 3: Berinteraksi dengan DOM – Baca Judul Halaman

Untuk demonstrasi kami akan mengambil judul dan mencetaknya. Dalam skenario dunia nyata Anda dapat mengambil screenshot, mengekspor ke PDF, atau mengikis data.

```java
            // Simple DOM interaction – fetch and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());
        }
    }
}
```

**Output yang diharapkan** (ketika `https://example.com` dapat dijangkau):

```
Title inside sandbox: Example Domain
```

Jika situs mengembalikan judul yang berbeda, Anda akan melihatnya—tidak ada yang perlu diubah.

---

## Langkah 4: Verifikasi Pengaturan (Debug Opsional)

Kadang-kadang Anda ingin memeriksa kembali bahwa sandbox benar‑benar menghormati DPI dan viewport Anda. Aspose.HTML tidak menampilkan nilai tersebut secara langsung, tetapi Anda dapat menyimpulkannya dengan mengukur dimensi elemen.

```java
        // Example: measure a known element's width in pixels.
        int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
        System.out.println("Measured width (px): " + elementWidth);
```

Jika Anda mengetahui CSS mendeklarasikan elemen sebagai `width: 200pt;`, pada **96 dpi** Anda akan melihat `200pt * (96/72) ≈ 267px`. Sesuaikan DPI dan jalankan kembali untuk melihat angka berubah—bukti bahwa **cara mengatur dpi** memang berfungsi.

---

## Kode Sumber Lengkap dalam Satu Blok

Salin‑tempel berikut ke dalam `SandboxExample.java`. Kode ini dapat dikompilasi apa adanya; pastikan JAR Aspose.HTML ada di classpath Anda.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox that defines the rendering environment
        // (viewport size 1024×768 and 96 dpi) and a custom user‑agent string.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent

        // Step 2: Load a web page inside the sandbox so layout respects the settings.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {

            // Step 3: Interact with the DOM – here we simply read and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());

            // Optional: verify DPI effect by measuring an element (if you know its CSS size).
            // int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
            // System.out.println("Measured width (px): " + elementWidth);
        }
    }
}
```

Kompilasi dan jalankan:

```bash
javac -cp "aspose-html-23.12.jar" SandboxExample.java
java -cp ".:aspose-html-23.12.jar" SandboxExample
```

Anda akan melihat judul tercetak, mengonfirmasi bahwa sandbox berfungsi dengan **dpi yang diatur**, **ukuran viewport yang diatur**, dan **user agent yang diatur** yang Anda berikan.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya membutuhkan DPI yang berbeda?

Cukup ubah argumen kedua dari `DocumentSandbox`. Untuk PDF siap cetak Anda dapat menggunakan `300`:

```java
new DocumentSandbox(new Size(1024, 768), 300, "MyCustomUserAgent/1.0");
```

DPI yang lebih tinggi menghasilkan dimensi piksel yang lebih besar untuk poin CSS yang sama, yang meningkatkan kualitas raster tetapi mengonsumsi lebih banyak memori.

### Bisakah saya memuat file HTML lokal alih-alih URL?

Tentu saja. Ganti URL dengan path file:

```java
HTMLDocument webDoc = new HTMLDocument("file:///C:/myfolder/page.html", renderingSandbox);
```

Pastikan path tersebut absolut dan menggunakan skema `file:///`.

### Bagaimana cara mengubah user‑agent setelah sandbox dibuat?

Sandbox bersifat immutable—setelah Anda memberikannya ke `HTMLDocument`, pengaturan terkunci. Untuk menggunakan user‑agent yang berbeda, buat instance baru `DocumentSandbox` dengan string yang diinginkan.

### Apakah Aspose.HTML mendukung eksekusi JavaScript?

Ya, mesin menjalankan sebagian besar skrip sisi klien. Jika skrip memodifikasi DOM setelah dimuat, Anda dapat menunggu sedikit:

```java
webDoc.waitForLoad();
```

Atau gunakan logika mirip `setTimeout` di dalam halaman sebelum menanyakan elemen.

---

## Konfirmasi Visual (Gambar)

Di bawah ini adalah screenshot konsol yang menunjukkan eksekusi berhasil. Perhatikan output judul yang cocok dengan halaman, mengonfirmasi sandbox menghormati pengaturan kami.

![Output konsol yang menunjukkan cara mengatur dpi di Aspose.HTML Sandbox](/images/console-output.png)

*Teks alt:* *Output konsol yang menunjukkan cara mengatur dpi, mengatur ukuran viewport, dan mengatur user agent di Aspose.HTML Sandbox.*

---

## Ringkasan & Langkah Selanjutnya

Kami telah membahas **cara mengatur DPI** (96 dpi dalam contoh), **mengatur ukuran viewport** (1024 × 768), dan **mengatur user agent** (string khusus) menggunakan API sandbox Aspose.HTML. Program Java lengkap yang dapat dijalankan membuktikan bahwa pengaturan ini bukan sekadar teori—mereka secara langsung memengaruhi rendering dan interaksi DOM.

Ready for more?

- **Ekspor ke PDF:** Setelah memuat halaman, panggil `webDoc.save("output.pdf", SaveFormat.PDF);` untuk menghasilkan PDF resolusi tinggi yang mencerminkan DPI yang Anda atur.  
- **Ambil Screenshot:** Gunakan `webDoc.renderToBitmap("screenshot.png");` untuk gambar pixel‑perfect.  
- **Bereksperimen dengan Layout Responsif:** Ubah dimensi viewport untuk menguji breakpoint mobile tanpa perangkat nyata.  

Bereksperimen dengan nilai DPI yang berbeda, kombinasi viewport, dan user‑agent untuk melihat bagaimana server dan CSS bereaksi. Sandbox adalah playground ringan yang menghemat Anda dari harus menjalankan browser penuh.

---

### Terus Menjelajah

- **Dokumentasi Aspose.HTML** – penjelajahan mendalam ke opsi `DocumentSandbox`.  
- **Media Queries CSS Lanjutan** – pelajari bagaimana ukuran viewport memicu gaya yang berbeda.  
- **User‑Agent Spoofing** – temukan bagaimana beberapa situs menyajikan markup alternatif berdasarkan string agent.  

Ada pertanyaan atau kasus rumit? Tinggalkan komentar, dan mari kita selesaikan bersama. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}