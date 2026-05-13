---
category: general
date: 2026-03-14
description: Pelajari cara mengatur rasio piksel perangkat di Java dan menyimpan halaman
  web sebagai PNG menggunakan Aspose.HTML – panduan lengkap konversi HTML ke PNG.
draft: false
keywords:
- set device pixel ratio
- save webpage as png
- how to render png
- html to png conversion
- java html to image
language: id
og_description: Pelajari cara mengatur rasio piksel perangkat di Java dan menyimpan
  halaman web sebagai PNG dengan Aspose.HTML, mencakup konversi HTML ke PNG langkah
  demi langkah.
og_title: atur rasio piksel perangkat di Java – Render HTML ke PNG
tags:
- java
- aspose-html
- image-rendering
title: Atur rasio piksel perangkat di Java – Render HTML ke PNG
url: /id/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-render-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# mengatur rasio piksel perangkat di Java – Render HTML ke PNG

Pernahkah Anda perlu **mengatur rasio piksel perangkat** saat membuat tangkapan layar sebuah halaman web di Java? Mungkin Anda sedang membangun layanan pratinjau untuk perangkat seluler, atau Anda hanya menginginkan thumbnail yang tajam dan terlihat tepat di layar Retina. Apapun situasinya, Anda berada di tempat yang tepat. Dalam tutorial ini kami akan membahas seluruh proses **konversi html ke png**, dan Anda akan melihat secara tepat cara **menyimpan halaman web sebagai png** menggunakan pustaka Aspose.HTML.

Kami akan membahas semuanya mulai dari mengonfigurasi sandbox yang meniru viewport iPhone, memuat halaman HTML remote, hingga menulis hasilnya ke disk. Pada akhir tutorial Anda akan mengetahui **cara merender png** secara programatis, dan Anda akan memiliki potongan kode yang dapat digunakan kembali dalam proyek Java mana pun yang memerlukan kemampuan **java html to image**.

## Apa yang Anda Butuhkan

- **Java Development Kit (JDK) 8 atau lebih baru** – pustaka ini bekerja dengan JDK terbaru mana pun.
- **Aspose.HTML for Java** – Anda dapat mengambil JAR terbaru dari repositori Maven Aspose atau mengunduh zip dari situs resmi.
- Sebuah **IDE** (IntelliJ IDEA, Eclipse, atau bahkan VS Code) – apa saja yang memungkinkan Anda mengompilasi dan menjalankan Java.
- Koneksi internet jika Anda berencana memuat URL langsung (contoh menggunakan `https://example.com/mobile.html`).

## Langkah 1: Konfigurasikan Sandbox dan atur rasio piksel perangkat

Hal pertama yang harus Anda lakukan adalah membuat **Sandbox** yang berpura‑pura menjadi perangkat seluler. Di sinilah Anda benar‑benar **mengatur rasio piksel perangkat** agar sesuai dengan layar ber‑densitas tinggi (misalnya, tampilan retina 2× pada iPhone).

```java
import com.aspose.html.rendering.SandboxOptions;

// Create sandbox options
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixel width of iPhone 6/7/8
sandboxOptions.setScreenHeight(667);         // CSS pixel height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
sandboxOptions.setUserAgent(
    "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
    "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1");

// Build the sandbox
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

**Mengapa ini penting:** `devicePixelRatio` memberi tahu mesin rendering berapa banyak piksel fisik yang sesuai dengan satu piksel CSS. Tanpa mengaturnya, gambar keluaran Anda akan tampak buram pada layar ber‑DPI tinggi. Dengan mendefinisikannya secara eksplisit, Anda memastikan PNG yang dihasilkan memiliki detail yang tepat.

> **Tip pro:** Jika Anda menargetkan perangkat Android, Anda dapat menggunakan `3.0` untuk perangkat dengan skala 3×. Sesuaikan lebar/tinggi secara tepat.

## Langkah 2: Muat halaman HTML untuk konversi html ke png

Setelah sandbox siap, kita dapat memuat halaman yang ingin di‑capture. Kelas `HTMLDocument` dari Aspose.HTML menerima sebuah URL dan instance sandbox, sehingga halaman dirender persis seperti pada perangkat yang disimulasikan.

```java
import com.aspose.html.HTMLDocument;

// Load the remote page inside the sandbox
HTMLDocument document = new HTMLDocument(
    "https://example.com/mobile.html", // Replace with your own URL
    mobileSandbox);
```

**Apa yang terjadi di balik layar?** Pustaka ini mengambil HTML, mengurai CSS, menjalankan JavaScript apa pun (jika diaktifkan), dan menata halaman menggunakan dimensi viewport yang Anda tentukan sebelumnya. Langkah ini merupakan inti dari konversi **java html to image** karena memberikan DOM yang sepenuhnya dirender siap untuk rasterisasi.

> **Kasus khusus:** Jika halaman mengandalkan font eksternal, pastikan font tersebut dapat diakses dari mesin yang menjalankan kode. Jika tidak, teks dapat beralih ke font default, mengubah hasil visual.

## Langkah 3: Simpan halaman web sebagai PNG – cara merender png dengan Aspose.HTML

Setelah dokumen dirender, langkah terakhir adalah menulis file PNG ke disk. Kelas `PngSaveOptions` memungkinkan Anda menyesuaikan tingkat kompresi dan pengaturan khusus PNG lainnya, namun nilai default sudah cukup baik untuk kebanyakan skenario.

```java
import com.aspose.html.saving.PngSaveOptions;

// Define PNG options (optional)
PngSaveOptions pngOptions = new PngSaveOptions();
// You could adjust pngOptions.setCompressionLevel(9); for maximum compression

// Save the rendered page as a PNG image
document.save("output/mobile_view.png", pngOptions);

System.out.println("Mobile view rendered and saved as PNG.");
```

Saat Anda menjalankan program, Anda akan mendapatkan `mobile_view.png` di folder `output`. Buka file tersebut, dan Anda akan melihat snapshot persis dari halaman remote, dirender pada resolusi ber‑densitas tinggi yang Anda tentukan melalui **set device pixel ratio**.

### Quick verification

```text
$ java -jar MobileRenderTutorial.jar
Mobile view rendered and saved as PNG.
$ ls output
mobile_view.png
```

Buka gambar dengan penampil apa pun; teks harus tajam, ikon jelas, dan tata letak identik dengan yang Anda lihat pada iPhone asli.

## Opsional: Menyesuaikan Pipeline Rendering

### Mengubah DPI secara dinamis

Jika Anda perlu menghasilkan gambar untuk berbagai kepadatan layar, bungkus pembuatan sandbox dalam sebuah metode:

```java
private static Sandbox createSandbox(double dpr) {
    SandboxOptions opts = new SandboxOptions();
    opts.setScreenWidth(375);
    opts.setScreenHeight(667);
    opts.setDevicePixelRatio(dpr); // Pass 1.0, 2.0, 3.0, etc.
    opts.setUserAgent("...");
    return new Sandbox(opts);
}
```

Kemudian panggil `createSandbox(3.0)` untuk perangkat 3×. Fleksibilitas ini berguna saat Anda membangun layanan yang mengembalikan thumbnail untuk iPhone, iPad, dan tablet Android sekaligus.

### Rendering tanpa JavaScript

Jika halaman yang Anda capture berisi skrip berat yang tidak diperlukan, Anda dapat menonaktifkan JavaScript untuk **konversi html ke png** yang lebih cepat:

```java
sandboxOptions.setJavaScriptEnabled(false);
```

Menonaktifkan skrip dapat memotong waktu rendering hingga setengahnya, namun perlu diingat bahwa beberapa konten dinamis mungkin menghilang.

## Kesalahan Umum dan Cara Menghindarinya

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Output buram** | `devicePixelRatio` dibiarkan pada nilai default (1.0) | Secara eksplisit **atur device pixel ratio** ke 2.0 atau lebih tinggi |
| **Font hilang** | Font remote diblokir oleh firewall | Pastikan mesin memiliki akses internet atau sematkan font secara lokal |
| **Kesalahan out‑of‑memory** | Merender halaman sangat besar pada DPI tinggi | Batasi ukuran viewport atau turunkan `devicePixelRatio` |
| **URL tidak tepat** | Menggunakan path relatif tanpa URL dasar | Berikan URL absolut penuh atau setel `document.setBaseUrl()` |

## Contoh Lengkap yang Berfungsi

Berikut adalah program Java lengkap yang siap dijalankan. Salin‑tempelkan ke dalam file bernama `MobileRenderTutorial.java`, tambahkan JAR Aspose.HTML ke classpath Anda, dan jalankan.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.Sandbox;
import com.aspose.html.rendering.SandboxOptions;
import com.aspose.html.saving.PngSaveOptions;

public class MobileRenderTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox that mimics a mobile device viewport
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixel width
        sandboxOptions.setScreenHeight(667);         // CSS pixel height
        sandboxOptions.setDevicePixelRatio(2.0);     // High‑density screen (set device pixel ratio)
        sandboxOptions.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1");

        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // Step 2: Load the HTML page inside the sandbox
        HTMLDocument document = new HTMLDocument(
            "https://example.com/mobile.html", // Replace with your own URL
            mobileSandbox);

        // Step 3: Render the page to a PNG image
        PngSaveOptions pngOptions = new PngSaveOptions();
        document.save("output/mobile_view.png", pngOptions);

        System.out.println("Mobile view rendered.");
    }
}
```

> **Hasil:** Program ini membuat `output/mobile_view.png`, sebuah tangkapan layar ber‑resolusi tinggi yang menghormati **set device pixel ratio** yang Anda definisikan.

## Konfirmasi Visual

<img src="output/mobile_view.png" alt="contoh screenshot set device pixel ratio" width="400"/>

Gambar di atas (placeholder) menunjukkan PNG akhir setelah proses rendering. Perhatikan teks yang tajam dan elemen UI yang berskala tepat—tepat seperti yang Anda harapkan ketika **set device pixel ratio** diterapkan dengan benar.

## Kesimpulan

Anda kini memiliki pemahaman yang kuat tentang cara **set device pixel ratio** di Java, melakukan **konversi html ke png**, dan **menyimpan halaman web sebagai png** menggunakan Aspose.HTML. Ini mencakup alur kerja penting “cara merender png” dan memberi Anda pola yang dapat digunakan kembali untuk tugas **java html to image** apa pun yang mungkin Anda temui.

Siap untuk langkah selanjutnya? Cobalah mengganti URL dengan halaman dinamis, bereksperimen dengan nilai `devicePixelRatio` yang berbeda, atau integrasikan potongan kode ini ke dalam endpoint Spring Boot yang mengembalikan PNG sesuai permintaan. Tidak ada batasan, dan dengan dasar yang sudah dikuasai, Anda akan menemukan bahwa memperluas solusi ini sangat mudah.

Selamat coding, dan silakan tinggalkan komentar

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}