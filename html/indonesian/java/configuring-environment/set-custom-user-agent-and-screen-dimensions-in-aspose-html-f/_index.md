---
category: general
date: 2026-09-29
description: Atur agen pengguna khusus di Aspose.HTML untuk Java dan pelajari cara
  mengatur ukuran layar virtual untuk rendering HTML yang akurat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: id
lastmod: 2026-09-29
og_description: Atur agen pengguna khusus di Aspose.HTML untuk Java dan pelajari cara
  mengatur ukuran layar virtual untuk rendering HTML yang akurat.
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: Atur agen pengguna khusus dan dimensi layar di Aspose.HTML untuk Java
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: Atur agen pengguna khusus dan dimensi layar di Aspose.HTML untuk Java
url: /id/java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Atur agen pengguna khusus dan dimensi layar di Aspose.HTML untuk Java

Jika Anda perlu **set custom user agent** saat merender HTML dengan Aspose.HTML untuk Java, panduan ini menunjukkan secara tepat cara melakukannya. Dengan mengonfigurasi sandbox Anda juga mendapatkan kemampuan untuk **set virtual screen size**, memastikan tata letak cocok dengan viewport browser nyata.

Anda akan menyelesaikan tutorial ini dengan program lengkap yang dapat dijalankan yang **specifies user agent**, **sets screen width**, dan **sets screen height**. Tidak diperlukan alat eksternal—hanya Aspose.HTML untuk Java dan runtime Java 8+.

## Apa yang akan Anda pelajari

* Cara membuat `SandboxConfiguration` untuk mengisolasi proses rendering.
* Cara **set custom user agent** dan mengapa hal ini penting untuk halaman responsif.
* Cara **set virtual screen size** (lebar dan tinggi layar) untuk tata letak yang akurat.
* Cara memuat file HTML di dalam sandbox dan menyimpan hasil yang diproses.
* Kesulitan umum dan tip praktik terbaik untuk rendering dalam sandbox.

> **Prerequisites** – Anda memerlukan lisensi Aspose.HTML untuk Java yang valid, Java 8 atau lebih baru, dan sebuah IDE (IntelliJ IDEA, Eclipse, atau VS Code). Contoh ini menggunakan file lokal `input.html`, tetapi URL apa pun yang dapat dijangkau juga dapat digunakan.

![Sandbox flow diagram](sandbox-flow.png "set custom user agent example in Java")

## Langkah 1: Buat konfigurasi sandbox (dasar)

Sandbox mengisolasi lingkungan rendering dari JVM host, yang penting ketika Anda ingin **set custom user agent** atau mengubah ukuran viewport.

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*Mengapa langkah ini?*  
`SandboxConfiguration` menyimpan semua opsi rendering, termasuk **screen dimensions** dan string **user‑agent**. Dengan mengonfigurasikannya sebelum memuat dokumen, Anda menjamin mesin HTML menghormati pengaturan tersebut sejak permintaan pertama.

## Langkah 2: Atur dimensi layar untuk meniru perangkat nyata

Situs responsif sering membaca `window.innerWidth` dan `window.innerHeight`. Agar mesin berpikir berjalan pada layar 1024 × 768, Anda **set virtual screen size**:

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*Mengapa ini penting* – Jika Anda melewatkan **set screen dimensions**, renderer mungkin menggunakan viewport yang sangat kecil, sehingga kueri media CSS memilih tata letak seluler. Dengan secara eksplisit **set screen width** dan **set screen height**, Anda mengontrol aturan CSS mana yang diaktifkan.

## Langkah 3: Tentukan string user‑agent khusus

Beberapa halaman web menyajikan konten berbeda berdasarkan header user‑agent. Untuk **specify user agent** Anda cukup mengaturnya pada konfigurasi sandbox:

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*Mengapa menggunakan user agent khusus?*  
String khusus dapat melewati deteksi bot, memicu fitur hanya desktop, atau menguji bagaimana situs berperilaku untuk versi browser tertentu. Mesin Aspose meneruskan nilai ini pada setiap permintaan HTTP yang dibuat saat memuat sumber daya eksternal (CSS, gambar, skrip).

## Langkah 4: Muat dokumen HTML di dalam sandbox

Sekarang sandbox sudah sepenuhnya dikonfigurasi, muat file HTML. Konstruktor yang menerima jalur file dan `SandboxConfiguration` secara otomatis menerapkan semua pengaturan yang telah kita definisikan.

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

Jika Anda perlu memuat dari URL remote, ganti jalur file dengan string URL—Aspose.HTML tetap akan menghormati **set custom user agent** dan **screen dimensions**.

## Langkah 5: Simpan output yang telah diproses

Setelah dokumen selesai dimuat, Anda dapat menyimpannya dalam format apa pun yang didukung. Di sini kami menulis file HTML yang berada dalam sandbox dan mencerminkan perubahan DOM apa pun yang disebabkan oleh pengaturan khusus.

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

File yang disimpan akan berisi markup yang sama, tetapi skrip apa pun yang menanyakan `navigator.userAgent` atau memeriksa `window.innerWidth` kini akan melihat nilai yang Anda berikan.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua langkah memberikan Anda program mandiri yang dapat Anda salin, tempel, dan jalankan.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### Output yang diharapkan

Menjalankan program akan membuat `sandboxed_output.html`. Jika Anda membukanya di browser dan memeriksa `navigator.userAgent` melalui konsol, Anda akan melihat **AsposeHTML/1.0**. Begitu pula, `window.innerWidth` akan melaporkan **1024**, mengonfirmasi bahwa **set screen dimensions** berfungsi sebagaimana mestinya.

## Pertanyaan umum & penanganan kasus tepi

| Pertanyaan | Jawaban |
|------------|---------|
| **Bagaimana jika halaman memuat sumber daya tambahan dari domain berbeda?** | Sandbox meneruskan **custom user agent** pada setiap permintaan, tetapi kebijakan lintas‑origin tetap berlaku. Gunakan `sandboxConfig.setAllowCrossDomain(true)` jika Anda perlu melonggarkan pembatasan tersebut. |
| **Apakah saya dapat mengubah ukuran layar setelah dokumen dimuat?** | Tidak. Dimensi layar dibaca selama proses layout awal. Untuk merender dengan ukuran berbeda, buat `SandboxConfiguration` baru dan muat ulang dokumen. |
| **Apakah saya perlu memanggil `document.close()`?** | `HTMLDocument` mengimplementasikan `AutoCloseable`. Menggunakan blok try‑with‑resources memastikan pembersihan yang tepat, tetapi pemanggilan `close()` secara eksplisit bersifat opsional dalam skrip sederhana. |
| **Bagaimana perbedaannya dengan mengatur user‑agent pada klien HTTP?** | Mengatur user‑agent pada sandbox memengaruhi **all** permintaan sumber daya yang dibuat oleh mesin HTML, bukan hanya pengambilan HTML awal. Ini meniru perilaku browser nyata dengan lebih akurat. |
| **Apakah sandbox aman untuk HTML yang tidak terpercaya?** | Ya. Sandbox mengisolasi akses sistem file dan membatasi panggilan jaringan sesuai konfigurasi, sehingga mengurangi risiko skrip berbahaya memengaruhi JVM host Anda. |

## Pro tips

* **Reuse configurations** – Jika Anda merender banyak halaman dengan viewport yang sama, buat satu `SandboxConfiguration` dan gunakan kembali untuk menghindari overhead pembuatan objek.
* **Debug with logging** – Aktifkan logging Aspose.HTML (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`) untuk melihat sumber daya mana yang diambil dengan **custom user‑agent**.
* **Combine with CSS media queries** – Dengan menyesuaikan **set screen width** Anda dapat menguji bagaimana desain responsif Anda berperilaku pada tablet, ponsel, atau desktop besar tanpa membuka browser nyata.

## Kesimpulan

Anda kini tahu cara **set custom user agent** dan **set screen dimensions** saat merender HTML dengan Aspose.HTML untuk Java. Dengan mengonfigurasi sandbox, Anda mengisolasi lingkungan, mengontrol viewport, dan memastikan sumber daya eksternal melihat header tepat yang Anda tentukan. Teknik ini penting untuk menguji tata letak responsif, melewati pemblokiran bot, atau mereproduksi fitur hanya desktop dalam pipeline otomatis.

Selanjutnya, Anda mungkin ingin menjelajahi **how to set custom cookies** atau **capture rendered screenshots** menggunakan API rendering Aspose.HTML—kedua konsep tersebut dibangun di atas pola konfigurasi sandbox yang baru saja Anda kuasai.

Selamat mengoding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [High DPI Rendering in Java – Capture Webpage Screenshots with Custom User Agent](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [How to Load HTML, Set Device DPI & Read Background Color](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Create HTML File Java & Set Up Network Service (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}