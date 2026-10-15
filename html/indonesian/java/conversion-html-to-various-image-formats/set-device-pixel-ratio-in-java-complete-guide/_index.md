---
category: general
date: 2026-02-22
description: Atur rasio piksel perangkat di Java dengan sandbox Aspose.HTML. Pelajari
  cara mengatur agen pengguna khusus, mendapatkan judul halaman Java, dan mengonversi
  HTML ke PNG dalam satu tutorial.
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- save html as image
- convert html to png
- get page title java
language: id
og_description: Atur rasio piksel perangkat di Java menggunakan sandbox Aspose.HTML.
  Tutorial ini menunjukkan cara mengatur agen pengguna khusus, mengambil judul halaman
  Java, dan mengonversi HTML ke PNG.
og_title: Mengatur Rasio Piksel Perangkat di Java – Panduan Lengkap
tags:
- Aspose.HTML
- Java
- Web Rendering
title: Mengatur Rasio Piksel Perangkat di Java – Panduan Lengkap
url: /id/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengatur Device Pixel Ratio di Java – Panduan Lengkap

Pernah bertanya-tanya bagaimana cara **set device pixel ratio** saat merender halaman web dari Java? Anda bukan satu-satunya. Banyak pengembang perlu meniru layar seluler high‑DPI sehingga tangkapan layar terlihat tajam, terutama ketika mereka kemudian **save html as image** untuk laporan atau aset pemasaran. Dalam tutorial ini kami akan membahas contoh praktis yang melakukan hal tersebut—serta menunjukkan cara **set custom user agent**, **get page title java**, dan **convert html to png** menggunakan Aspose.HTML.

Kami akan memulai dengan gambaran singkat tentang sandbox API, kemudian menyelami setiap langkah konfigurasi, dan akhirnya menghasilkan file PNG yang meniru tampilan iPhone nyata. Pada akhir tutorial, Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat dimasukkan ke proyek Java mana pun. Tidak diperlukan alat eksternal, hanya Java biasa dan Aspose.HTML 7.x (atau yang lebih baru).

---

## Prasyarat

- Java 17 atau lebih baru (kode dapat dikompilasi dengan versi sebelumnya tetapi 17 disarankan).
- Aspose.HTML untuk Java (unduh dari situs resmi Aspose; koordinat Maven: `com.aspose:aspose-html:23.10`).
- IDE atau editor teks pilihan Anda (IntelliJ IDEA, VS Code, Eclipse… semuanya dapat digunakan).
- Akses internet untuk URL demo (`https://example.com/responsive.html`), atau ganti dengan halaman HTML publik apa pun yang Anda miliki.

> **Pro tip:** Jika Anda berada di belakang proxy, konfigurasikan properti sistem JVM `http.proxyHost` dan `http.proxyPort` sebelum menjalankan kode.

---

## Langkah 1: Mengatur Device Pixel Ratio dan Opsi Sandbox Lainnya

Hal pertama yang kita butuhkan adalah instance **SandboxOptions** di mana kita mendefinisikan ukuran layar virtual dan *device pixel ratio* (DPR). Anggap DPR sebagai faktor yang memberi tahu browser berapa banyak piksel fisik yang sesuai dengan satu piksel CSS. Pada iPhone Retina, DPR biasanya **2.0**, itulah mengapa kita akan menggunakan nilai tersebut.

```java
// Step 1: Create and configure SandboxOptions
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS width of an iPhone X
sandboxOptions.setScreenHeight(667);         // CSS height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
```

> **Mengapa ini penting:** Tanpa mengatur DPR yang tepat, gambar yang dirender akan terlihat buram atau terlalu besar karena rasterizer mengasumsikan pemetaan piksel 1:1.

---

## Langkah 2: Mengatur User Agent Kustom

Situs web sering menyajikan markup yang berbeda berdasarkan header **User‑Agent**. Untuk memastikan halaman kami berperilaku seperti pada iPhone nyata, kami menyuntikkan string kustom yang meniru Safari di iOS.

```java
// Step 2: Define a mobile‑specific user agent
String iphoneUA = "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                  "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                  "Version/14.0 Mobile/15E148 Safari/604.1";

sandboxOptions.setUserAgent(iphoneUA);   // <-- set custom user agent
```

> **Kasus khusus:** Beberapa situs juga memeriksa header `Accept-Language`. Jika Anda melihat terjemahan yang hilang, tambahkan `sandboxOptions.setAcceptLanguage("en-US,en;q=0.9");`.

---

## Langkah 3: Memuat Halaman di Dalam Sandbox dan Mengambil Judul

Sekarang kami memulai sandbox dengan opsi yang baru saja kami definisikan. Objek **Sandbox** mengisolasi proses rendering, memastikan pengaturan DPR dan user‑agent kami dihormati.

```java
// Step 3: Create the sandbox and load the HTML document
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
HTMLDocument htmlDoc = new HTMLDocument(
        "https://example.com/responsive.html", mobileSandbox);
```

Setelah halaman dimuat, mengambil judul semudah memanggil `getTitle()`. Ini memenuhi persyaratan **get page title java**.

```java
// Step 3b: Print the page title to the console
System.out.println("Title: " + htmlDoc.getTitle());   // <-- get page title java
```

**Output konsol yang diharapkan**

```
Title: Responsive Demo – Mobile View
```

Jika judul kosong, periksa kembali URL atau pastikan halaman tidak diblokir oleh kebijakan CORS.

---

## Langkah 4: Mengonversi HTML ke PNG dan Menyimpan HTML sebagai Gambar

Aspose.HTML memungkinkan Anda merender DOM langsung ke file gambar. Karena kami sudah mengatur DPR menjadi 2.0, PNG yang dihasilkan akan memiliki kepadatan piksel dua kali lipat, menghasilkan tangkapan layar yang tajam.

```java
// Step 4: Render and save as PNG (convert html to png)
htmlDoc.save("mobile_view.png");   // <-- save html as image
```

Metode `save` secara otomatis mendeteksi ekstensi file dan memilih renderer yang sesuai. Jika Anda membutuhkan format lain (JPEG, BMP), cukup ubah nama file sesuai.

> **Bagaimana jika Anda membutuhkan ukuran gambar tertentu?**  
> Gunakan `ImageSaveOptions` untuk mengontrol lebar, tinggi, dan warna latar belakang:

```java
ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
pngOptions.setWidth(750);   // 375 CSS px * DPR 2
pngOptions.setHeight(1334);
htmlDoc.save("mobile_view_custom.png", pngOptions);
```

---

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap dijalankan yang menggabungkan semua langkah. Salin‑tempelkan ke file `SandboxDemo.java`, tambahkan dependensi Aspose.HTML, dan jalankan `java SandboxDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.rendering.image.ImageSaveOptions;
import com.aspose.html.rendering.image.SaveFormat;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Configure sandbox – set device pixel ratio, screen size, and user agent
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS width (iPhone)
        sandboxOptions.setScreenHeight(667);         // CSS height
        sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                "Version/14.0 Mobile/15E148 Safari/604.1");   // <-- set custom user agent

        // 2️⃣ Create sandbox instance
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // 3️⃣ Load the target page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox);

        // 4️⃣ Retrieve and print the page title (get page title java)
        System.out.println("Title: " + htmlDoc.getTitle());

        // 5️⃣ Render the page – convert html to png and save html as image
        // Simple save (auto‑detect PNG)
        htmlDoc.save("mobile_view.png");   // <-- save html as image

        // 6️⃣ Optional: custom size rendering
        ImageSaveOptions opts = new ImageSaveOptions(SaveFormat.PNG);
        opts.setWidth(750);   // 375 * DPR 2
        opts.setHeight(1334);
        htmlDoc.save("mobile_view_custom.png", opts); // another convert html to png example
    }
}
```

Menjalankan program menghasilkan dua file PNG:

| File | Deskripsi |
|------|-----------|
| `mobile_view.png` | Render default menggunakan DPR yang dikonfigurasi. |
| `mobile_view_custom.png` | Render dengan lebar/tinggi eksplisit (berguna untuk aset berukuran tetap). |

Anda dapat membuka salah satu file di penampil gambar apa pun untuk memverifikasi output beresolusi tinggi.

---

## Pertanyaan Umum & Kasus Khusus

| Pertanyaan | Jawaban |
|------------|---------|
| **Bagaimana jika halaman mengandung JavaScript yang memodifikasi DOM setelah dimuat?** | Aspose.HTML mengeksekusi skrip secara default. Jika Anda membutuhkan snapshot statis sebelum eksekusi skrip, set `sandboxOptions.setEnableJavaScript(false)`. |
| **Bisakah saya merender halaman yang memerlukan autentikasi?** | Ya. Gunakan `sandboxOptions.setCredentials(new NetworkCredential("user","pass"))` atau suntikkan cookie melalui `sandboxOptions.getCookies().add(...)`. |
| **Apakah DPR terbatas pada 2.0?** | Tidak. Anda dapat mengatur nilai double positif apa pun (misalnya 3.0 untuk perangkat ultra‑high‑DPI). Ingat bahwa DPR yang lebih besar berarti file gambar yang lebih besar. |
| **Bagaimana cara menangani halaman dengan aset besar (gambar, font)?** | Tingkatkan batas memori sandbox dengan `sandboxOptions.setMemoryLimit(512 * 1024 * 1024)` (byte). Ini mencegah error out‑of‑memory pada halaman berat. |
| **Apakah saya perlu menutup sandbox secara manual?** | `Sandbox` mengimplementasikan `AutoCloseable`. Bungkus dalam blok try‑with‑resources untuk pembersihan otomatis. |

---

## Kesimpulan

Kami telah menunjukkan cara **set device pixel ratio** di sandbox Java, **set custom user agent**, **get page title java**, dan **convert html to png** (secara efektif **save html as image**) menggunakan Aspose.HTML. Contoh lengkap ini memperlihatkan alur kerja praktis yang dapat Anda adaptasi untuk pembuatan tangkapan layar otomatis, pengujian regresi visual, atau skenario apa pun yang memerlukan representasi pixel‑perfect dari halaman web.

Silakan bereksperimen—ubah DPR menjadi 3.0, ganti user‑agent dengan string Android, atau arahkan URL ke file HTML lokal. Pola yang sama berlaku untuk PDF, SVG, atau bahkan rendering multi‑halaman.

Jika Anda menemukan panduan ini berguna, pertimbangkan untuk menjelajahi topik terkait seperti **PDF generation with Aspose.HTML**, **headless Chrome alternatives**, atau **batch rendering of multiple URLs**. Selamat coding, semoga tangkapan layar Anda selalu tajam!

![set device pixel ratio in Java sandbox](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}