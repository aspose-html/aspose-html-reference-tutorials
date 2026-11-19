---
category: general
date: 2026-03-20
description: Atur user agent dalam sandbox untuk mengekstrak judul halaman dengan
  rendering HTML tanpa kepala – pelajari cara mengatur DPI perangkat dan membuat instance
  sandbox.
draft: false
keywords:
- set user agent
- extract page title
- set device dpi
- create sandbox instance
- headless html rendering
language: id
og_description: Setel agen pengguna dalam sandbox, ekstrak judul halaman, dan kontrol
  DPI perangkat untuk rendering HTML headless yang andal.
og_title: Atur User Agent untuk Rendering HTML Tanpa Kepala – Panduan Lengkap
tags:
- Java
- Web Scraping
- Headless Rendering
title: Atur User Agent untuk Rendering HTML Tanpa Kepala – Panduan Lengkap
url: /id/java/configuring-environment/set-user-agent-for-headless-html-rendering-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Atur User Agent untuk Rendering HTML Headless – Panduan Lengkap

Pernah perlu **mengatur user agent** saat melakukan scraping situs tetapi tidak yakin bagaimana pengaruhnya terhadap halaman yang dirender? Anda tidak sendirian. Dalam banyak skenario headless, server memutuskan HTML apa yang dikirim berdasarkan string UA, jadi mengaturnya dengan benar dapat menjadi perbedaan antara halaman kosong dan konten yang sebenarnya Anda butuhkan.  

Dalam tutorial ini kita akan membahas cara mengonfigurasi sandbox, **membuat instance sandbox**, menyesuaikan **DPI perangkat**, dan akhirnya **mengekstrak judul halaman** dari sesi **rendering HTML headless**. Tanpa basa‑basi—hanya contoh Java yang dapat dijalankan dan Anda dapat menambahkannya ke proyek Anda hari ini.

> **Pro tip:** Jika Anda sudah menggunakan Aspose.HTML (atau perpustakaan serupa), langkah‑langkah di bawah ini cocok 1‑to‑1 dengan API‑nya. Jika Anda menggunakan stack yang berbeda, anggap sandbox sebagai konteks browser headless apa pun (Playwright, Selenium, dll.).

## Apa yang Akan Anda Bangun

- Sandbox dengan string **user‑agent** khusus.
- Rendering yang memperhatikan DPI sehingga satuan CSS (pt, in, cm) berperilaku seperti layar nyata.
- Cara bersih untuk **mengekstrak judul halaman** setelah halaman sepenuhnya dirender.
- Kelas Java mandiri yang dapat dijalankan dari command line.

Prasyarat? Hanya Java 8+ dan JAR Aspose.HTML for Java di classpath Anda. Tidak ada yang lain.

---

## Atur User Agent dan Konfigurasi Sandbox

Hal pertama yang harus Anda lakukan adalah memberi tahu mesin rendering browser apa yang Anda pura‑pura gunakan. Ini dilakukan melalui metode `SandboxConfiguration#setUserAgent`.

```java
import com.aspose.html.Sandbox;
import com.aspose.html.SandboxConfiguration;
import com.aspose.html.HTMLDocument;

/* Step 1: Configure the sandbox – screen size, DPI, and user‑agent */
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
sandboxConfig.setScreenSize(1280, 800);      // width × height in pixels
sandboxConfig.setDeviceDPI(96);              // DPI for CSS unit conversion
sandboxConfig.setUserAgent("AsposeHTML/1.0"); // <-- set user agent
```

Mengapa ini penting? Banyak situs menyajikan tata letak sederhana untuk agen yang tidak dikenal (pikirkan “bot”) dan menyembunyikan data yang sebenarnya Anda butuhkan. Dengan meniru browser nyata, Anda memaksa server mengembalikan halaman lengkap.

![set user agent configuration](/images/set-user-agent.png "Ilustrasi pengaturan user agent dalam konfigurasi sandbox")

*Teks alt gambar: tangkapan layar konfigurasi set user agent.*

## Buat Instance Sandbox untuk Rendering HTML Headless

Setelah konfigurasi siap, jalankan sandbox. Anggaplah ini seperti meluncurkan Chrome headless yang hanya hidup di memori.

```java
/* Step 2: Create the sandbox using the configuration */
try (Sandbox sandboxInstance = new Sandbox(sandboxConfig)) {
    // The sandbox is now ready for rendering tasks.
    // Anything you do inside this block runs headlessly.
}
```

Menggunakan pola try‑with‑resources menjamin sandbox dibuang dengan benar, membebaskan sumber daya native. Jika Anda lupa menutupnya, Anda mungkin mengalami kebocoran memori atau handle file—sesuatu yang sering membuat pemula terjebak.

## Atur DPI Perangkat untuk Rendering CSS yang Akurat

Pemanggilan `setDeviceDPI` bukan sekadar tambahan; ia secara langsung memengaruhi cara satuan CSS seperti `pt` atau `mm` dihitung. Jika Anda merender faktur, PDF, atau halaman sensitif tata letak lainnya, mencocokkan DPI target memastikan screenshot atau data yang diekstrak terlihat persis seperti di monitor nyata.

Anda sudah melihat pemanggilan ini di cuplikan konfigurasi, tetapi berikut pemeriksaan cepat:

```java
int dpi = sandboxConfig.getDeviceDPI(); // should return 96
System.out.println("Sandbox DPI set to: " + dpi);
```

Jika Anda memerlukan resolusi lebih tinggi (misalnya untuk aset gaya retina), naikkan nilai menjadi `144` atau `192`. Ingat untuk menjaga ukuran layar proporsional; jika tidak, tata letak dapat meluap.

## Ekstrak Judul Halaman dari Dokumen yang Dirender

Sekarang sandbox sudah berjalan, muat sebuah halaman dan ambil judulnya. Metode `HTMLDocument#getTitle` membaca tag `<title>` *setelah* DOM halaman sepenuhnya diparse.

```java
/* Step 3: Load a web page inside the sandboxed environment */
HTMLDocument htmlDoc = new HTMLDocument(sandboxInstance, "https://example.com");

/* Step 4: Work with the rendered document – extract its title */
String pageTitle = htmlDoc.getTitle();
System.out.println("Title: " + pageTitle);
```

Menjalankan kode di atas terhadap `https://example.com` akan mencetak:

```
Title: Example Domain
```

Itulah langkah **ekstrak judul halaman** yang beraksi. Jika situs menggunakan JavaScript untuk mengatur judul secara dinamis, sandbox akan mengeksekusi skrip tersebut (asalkan Anda mengaktifkan scripting, yang secara default sudah aktif). Jika Anda pernah melihat string kosong, periksa kembali bahwa halaman memang memiliki elemen `<title>` setelah skrip dijalankan.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut kelas lengkap yang siap dijalankan. Silakan salin‑tempel ke `Main.java` dan eksekusi `javac Main.java && java Main`.

```java
import com.aspose.html.Sandbox;
import com.aspose.html.SandboxConfiguration;
import com.aspose.html.HTMLDocument;

/**
 * Demonstrates how to set user agent, configure DPI,
 * create a sandbox instance, and extract the page title
 * using headless HTML rendering.
 */
public class Main {
    public static void main(String[] args) {
        // 1️⃣ Configure sandbox: screen, DPI, and user‑agent
        SandboxConfiguration config = new SandboxConfiguration();
        config.setScreenSize(1280, 800);
        config.setDeviceDPI(96);
        config.setUserAgent("AsposeHTML/1.0"); // <-- set user agent

        // 2️⃣ Create sandbox (auto‑close with try‑with‑resources)
        try (Sandbox sandbox = new Sandbox(config);
             // 3️⃣ Load the page inside the sandbox
             HTMLDocument doc = new HTMLDocument(sandbox, "https://example.com")) {

            // 4️⃣ Extract and print the title
            String title = doc.getTitle();
            System.out.println("Title: " + title);
        } catch (Exception e) {
            // Simple error handling – in real code you might log this
            System.err.println("Rendering failed: " + e.getMessage());
        }
    }
}
```

### Output yang Diharapkan

```
Title: Example Domain
```

Jika Anda mengganti `https://example.com` dengan URL lain, Anda akan melihat judul halaman tersebut—asalkan situs tidak memblokir agen headless. Itulah seluruh pipeline **rendering HTML headless** dalam kurang dari 30 baris Java.

---

## Pertanyaan Umum & Kasus Pinggir

| Pertanyaan | Jawaban |
|------------|---------|
| *Bagaimana jika situs memblokir UA yang tidak dikenal?* | Gunakan string browser umum, misalnya `"Mozilla/5.0 (Windows NT 10.0; Win64; x64) Chrome/119.0 Safari/537.36"`. Sandbox memungkinkan Anda mengatur UA apa pun secara arbitrer. |
| *Apakah saya perlu mengaktifkan JavaScript?* | Secara default sudah aktif. Jika Anda mematikannya sebelumnya, panggil `config.setEnableJavaScript(true)`. |
| *Bagaimana cara menangkap screenshot alih‑alih hanya judul?* | Setelah memuat dokumen, panggil `htmlDoc.save("page.png", SaveFormat.PNG)`. DPI yang Anda atur sebelumnya akan memengaruhi ukuran gambar. |
| *Bisakah saya merender beberapa halaman dalam satu sandbox?* | Ya. Gunakan kembali objek `Sandbox` yang sama; cukup buat objek `HTMLDocument` baru untuk setiap URL. |
| *Bagaimana dengan sertifikat HTTPS?* | Sandbox mempercayai keystore Java default. Untuk sertifikat self‑signed, impor ke trust store JVM atau nonaktifkan verifikasi melalui `config.setIgnoreCertificateErrors(true)`. |

---

## Tips untuk Scraping yang Siap Produksi

1. **Rotasi User Agents** – Simpan daftar string UA populer dan pilih satu secara acak per permintaan. Ini mengurangi peluang terdeteksi.
2. **Hormati Robots.txt** – Meskipun Anda headless, scraping yang etis berarti mematuhi kebijakan crawling situs.
3. **Batasi Kecepatan Permintaan** – Sisipkan `Thread.sleep(500)` di antara panggilan untuk menghindari membombardir server.
4. **Cache HTML yang Dirender** – Jika Anda membutuhkan halaman yang sama berulang kali, simpan HTML ke disk dan gunakan kembali; rendering memakan CPU.
5. **Pantau Memori** – Sandbox menyimpan sumber daya native. Pada pekerjaan yang berjalan lama, panggil `System.gc()` secara berkala atau restart sandbox setelah sekumpulan URL selesai.

---

## Kesimpulan

Anda kini tahu cara **mengatur user agent** untuk **rendering HTML headless** yang andal, mengonfigurasi **DPI perangkat**, **membuat instance sandbox**, dan **mengekstrak judul halaman** dalam alur kerja Java yang bersih. Contoh lengkap di atas dapat dijalankan langsung, mencetak judul, dan memberi ruang untuk ekstensi seperti screenshot atau konversi PDF.

Selanjutnya, coba ganti URL dengan situs yang menyajikan konten berbeda berdasarkan string UA, atau bereksperimen dengan nilai DPI yang lebih tinggi untuk melihat bagaimana tata letak CSS berubah. Anda juga dapat mengeksplorasi overload `HTMLDocument.save` pada perpustakaan untuk menghasilkan PDF—cara praktis lain untuk mengarsipkan halaman yang dirender.

Selamat coding, semoga scraper Anda tetap tak terdeteksi!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}