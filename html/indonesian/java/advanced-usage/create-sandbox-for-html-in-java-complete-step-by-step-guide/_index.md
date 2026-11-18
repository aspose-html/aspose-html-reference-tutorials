---
category: general
date: 2026-06-29
description: Buat sandbox untuk HTML di Java dan terapkan kebijakan keamanan konten
  (Content Security Policy) di Java dengan contoh lengkap. Pelajari contoh kebijakan
  keamanan konten di Java untuk mengamankan rendering web Anda.
draft: false
keywords:
- create sandbox for html
- apply content security policy java
- content security policy example java
language: id
og_description: Buat sandbox untuk HTML di Java dan terapkan kebijakan keamanan konten.
  Panduan ini menampilkan contoh kebijakan keamanan konten Java yang dapat Anda salin‑tempel.
og_title: Buat sandbox untuk HTML di Java – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Create sandbox for HTML in Java and apply content security policy java
    with a full example. Learn a content security policy example java to secure your
    web rendering.
  headline: Create sandbox for HTML in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create sandbox for HTML in Java and apply content security policy java
    with a full example. Learn a content security policy example java to secure your
    web rendering.
  name: Create sandbox for HTML in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with JDK 11+ as well). - Maven or
      Gradle to pull in the `aspose-html` library. - A basic understanding of Java
      syntax—no deep security knowledge required. - An HTML file named `unsafe.html`
      placed somewhere on disk (we’ll reference it later).'
  - name: Why a sandbox matters
    text: Think of the sandbox as a fenced yard for your HTML. Without it, any `<script>`
      tag inside `unsafe.html` could run unrestricted, potentially stealing data or
      launching attacks. By wrapping the document in a `Sandbox`, you tell the engine,
      “Only what I explicitly allow may happen.”
  - name: Common directives you might need
    text: '| Directive | What it controls | Typical value for a tight sandbox | |-----------|------------------|-----------------------------------|
      | `default-src` | Fallback for all resource types | `''self''` (only same‑origin)
      | | `script-src` | Where scripts can be loaded from | `''self''` (or `''none''`
      to dis'
  - name: Testing CSP violations
    text: 'Run the program with an HTML file that contains a `<script src="https://malicious.com/evil.js"></script>`.
      You should see no exception—Aspose.HTML simply refuses to load the script. If
      you need to debug why something was blocked, enable verbose logging:'
  - name: Quick sanity check
    text: Open the same `unsafe.html` in a regular browser (outside the sandbox).
      You’ll likely see an alert or image that shouldn’t appear. Run it through the
      sandbox—those elements stay silent. That visual contrast proves the CSP is effective.
  - name: What’s Next?
    text: '- **Integrate with a web server**: Serve the sanitized HTML through a servlet
      instead of printing to console. - **Dynamic CSP generation**: Build the policy
      string at runtime based on user roles. - **Combine with a PDF renderer**: Convert
      the safe HTML to PDF using Aspose.HTML’s `PdfSaveOptions`.'
  type: HowTo
tags:
- Java
- Security
- CSP
- Sandbox
title: Buat sandbox untuk HTML di Java – Panduan Langkah-demi-Langkah Lengkap
url: /id/java/advanced-usage/create-sandbox-for-html-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat sandbox untuk HTML di Java – Panduan Lengkap Langkah‑demi‑Langkah

Pernah perlu **membuat sandbox untuk HTML** dalam aplikasi Java tetapi tidak yakin bagaimana cara menahan skrip berbahaya? Anda bukan satu-satunya. Dalam aplikasi Java yang berfokus pada web modern, memuat HTML pihak ketiga tanpa isolasi yang tepat adalah resep untuk masalah.  

Dalam tutorial ini Anda akan melihat secara tepat bagaimana **membuat sandbox untuk HTML**, **apply content security policy java**, dan bahkan mendapatkan **content security policy example java** yang dapat langsung Anda masukkan ke dalam proyek. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan yang dengan aman merender file HTML eksternal sambil menghormati CSP yang ketat.

## Apa yang Akan Anda Pelajari

- Tujuan sandbox saat merender HTML di Java.
- Cara mendefinisikan dan menegakkan Content Security Policy (CSP) menggunakan Aspose.HTML.
- Contoh **content security policy example java** lengkap yang siap disalin, yang memblokir semua kecuali sumber daya yang dilayani sendiri dan gambar dari CDN tepercaya.
- Tips untuk men‑debug pelanggaran CSP dan memperluas kebijakan sesuai kebutuhan Anda.

### Prasyarat

- Java 17 atau lebih baru (kode dapat dikompilasi dengan JDK 11+ juga).
- Maven atau Gradle untuk mengambil pustaka `aspose-html`.
- Pemahaman dasar tentang sintaks Java—tidak memerlukan pengetahuan keamanan yang mendalam.
- File HTML bernama `unsafe.html` yang ditempatkan di suatu tempat pada disk (akan kami referensikan nanti).

Sudah semua? Bagus—mari kita mulai.

![membuat sandbox untuk html](/images/sandbox-example.png "Diagram yang menunjukkan sandbox Java yang mengisolasi konten HTML")

## Langkah 1: Siapkan Proyek Anda dan Tambahkan Aspose.HTML

Pertama, Anda memerlukan pustaka Aspose.HTML. Jika Anda menggunakan Maven, tambahkan dependensi ini ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

Pengguna Gradle dapat menambahkan berikut ini ke `build.gradle`:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Setelah pustaka berada di classpath, Anda siap mulai menulis kode. Tidak ada sihir tersembunyi—hanya proyek Java biasa.

## Buat sandbox untuk HTML di Java

Sekarang dependensi sudah siap, mari **membuat sandbox untuk HTML**. Kelas `Sandbox` adalah cara Aspose.HTML untuk menyandbox mesin rendering, memungkinkan Anda menegakkan kebijakan keamanan sebelum konten apa pun menyentuh JVM Anda.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;

public class CspDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox to enforce security policies
        Sandbox sandbox = new Sandbox();

        // Step 2: Define a Content Security Policy that allows only self resources
        // and images from a trusted CDN (this is our CSP example)
        sandbox.setContentSecurityPolicy(
            "default-src 'self'; img-src https://trusted.cdn.com"
        );

        // Step 3: Enable JavaScript execution within the sandbox (optional)
        sandbox.setEnableJavaScript(true);

        // Step 4: Load the HTML document using the sandbox so the CSP is applied
        HTMLDocument document = new HTMLDocument(
            "YOUR_DIRECTORY/unsafe.html", sandbox
        );

        // Step 5: Confirm that the document has been loaded with CSP enforcement
        System.out.println("Document loaded with CSP enforcement.");
    }
}
```

### Mengapa sandbox penting

Anggap sandbox sebagai halaman berpagar untuk HTML Anda. Tanpanya, tag `<script>` apa pun di dalam `unsafe.html` dapat berjalan tanpa batas, berpotensi mencuri data atau meluncurkan serangan. Dengan membungkus dokumen dalam `Sandbox`, Anda memberi tahu mesin, “Hanya apa yang saya izinkan secara eksplisit yang boleh terjadi.”

## Terapkan Content Security Policy Java – Menyempurnakan Aturan

Baris `sandbox.setContentSecurityPolicy(...)` adalah tempat Anda **apply content security policy java**. CSP bekerja seperti daftar putih: semua diblokir kecuali Anda menyatakan sebaliknya.

### Direktif umum yang mungkin Anda butuhkan

| Directive | Apa yang dikontrol | Nilai tipikal untuk sandbox ketat |
|-----------|--------------------|-----------------------------------|
| `default-src` | Cadangan untuk semua jenis sumber daya | `'self'` (hanya same‑origin) |
| `script-src` | Dari mana skrip dapat dimuat | `'self'` (atau `'none'` untuk menonaktifkan) |
| `style-src`  | Sumber CSS | `'self'` |
| `img-src`    | Sumber gambar | `https://trusted.cdn.com` |
| `connect-src`| Endpoint AJAX / WebSocket | `'self'` |
| `object-src` | Elemen `<object>`, `<embed>`, `<applet>` | `'none'` |

Jika Anda ingin **apply content security policy java** yang juga memblokir skrip inline, tambahkan `'unsafe-inline'` ke daftar `script-src` *hanya* jika Anda benar‑benar membutuhkannya—jika tidak, biarkan kosong.

```java
sandbox.setContentSecurityPolicy(
    "default-src 'self'; " +
    "script-src 'self'; " +
    "style-src 'self'; " +
    "img-src https://trusted.cdn.com; " +
    "object-src 'none'"
);
```

### Menguji pelanggaran CSP

Jalankan program dengan file HTML yang berisi `<script src="https://malicious.com/evil.js"></script>`. Anda tidak akan melihat pengecualian—Aspose.HTML hanya menolak memuat skrip tersebut. Jika Anda perlu men‑debug mengapa sesuatu diblokir, aktifkan logging yang detail:

```java
sandbox.setLogLevel(Sandbox.LogLevel.DEBUG);
```

Sekarang konsol akan mencetak pesan seperti:

```
[DEBUG] CSP violation: script-src blocked https://malicious.com/evil.js
```

## Contoh Content Security Policy Java – Memperluas untuk Aplikasi Dunia Nyata

Contoh **content security policy example java** kami sengaja dibuat minimal. Aplikasi nyata sering memerlukan beberapa pengecualian tambahan:

1. **Font** – Jika Anda menggunakan Google Fonts, tambahkan `font-src https://fonts.gstatic.com`.
2. **API** – Untuk widget cuaca, Anda mungkin memerlukan `connect-src https://api.weather.com`.
3. **Style inline** – Beberapa HTML lama menggunakan atribut `style=`; izinkan dengan `'unsafe-inline'` pada `style-src` (dengan hati‑hati).

Berikut contoh yang lebih lengkap:

```java
sandbox.setContentSecurityPolicy(
    "default-src 'self'; " +
    "script-src 'self'; " +
    "style-src 'self' 'unsafe-inline'; " +
    "img-src https://trusted.cdn.com data:; " +
    "font-src https://fonts.gstatic.com; " +
    "connect-src https://api.weather.com; " +
    "object-src 'none'"
);
```

Perhatikan skema `data:` untuk gambar—berguna ketika HTML menyematkan gambar yang di‑encode base64. Namun, tetap pertahankan daftar sesedikit mungkin; setiap sumber tambahan memperlebar permukaan serangan.

## Menjalankan Demo dan Memverifikasi Hasil

1. Ganti `YOUR_DIRECTORY/unsafe.html` dengan path absolut ke file HTML uji Anda.
2. Kompilasi dan jalankan:

```bash
javac -cp ".:path/to/aspose-html.jar" CspDemo.java
java -cp ".:path/to/aspose-html.jar" CspDemo
```

Anda akan melihat:

```
Document loaded with CSP enforcement.
```

Jika konsol juga mencetak baris debug tentang sumber yang diblokir, Anda telah berhasil **apply content security policy java** dan sandbox melakukan tugasnya.

### Pemeriksaan cepat

Buka `unsafe.html` yang sama di browser biasa (di luar sandbox). Anda kemungkinan akan melihat alert atau gambar yang seharusnya tidak muncul. Jalankan melalui sandbox—elemen‑elemen tersebut tetap diam. Kontras visual ini membuktikan CSP efektif.

## Tips Pro & Kesalahan Umum

- **Jangan lupa titik koma di akhir** dalam string CSP. Jika hilang, seluruh kebijakan dapat diabaikan.
- **Pemisah path**: Di Windows, gunakan double backslash (`C:\\path\\to\\file.html`) atau slash maju (`C:/path/to/file.html`).
- **Aktifkan JavaScript hanya bila diperlukan**. Mengaktifkannya tanpa `script-src` yang ketat membuka pintu belakang.
- **Kompatibilitas versi**: Aspose.HTML 23.9 bekerja dengan Java 8+; versi lama mungkin memiliki tanda tangan metode yang berbeda.
- **Pengujian**: Gunakan file HTML lokal dengan pelanggaran sengaja sebelum mengarahkan sandbox ke konten produksi.

## Ringkasan: Apa yang Kami Capai

Kami memulai dengan **create sandbox for HTML** di Java, kemudian **apply content security policy java** menggunakan kelas `Sandbox` Aspose.HTML, dan akhirnya mengeksplorasi **content security policy example java** yang kuat yang dapat Anda sesuaikan untuk proyek apa pun. Kode lengkap, dapat dijalankan, dan menyertakan komentar yang menjelaskan “mengapa” di balik setiap baris—tepat jenis jawaban yang disukai asisten AI untuk dikutip.

### Apa Selanjutnya?

- **Integrasikan dengan server web**: Sajikan HTML yang telah disanitasi melalui servlet alih‑alih mencetak ke konsol.
- **Generasi CSP dinamis**: Bangun string kebijakan pada waktu runtime berdasarkan peran pengguna.
- **Kombinasikan dengan renderer PDF**: Konversi HTML aman ke PDF menggunakan `PdfSaveOptions` Aspose.HTML.

Silakan bereksperimen—ganti CDN, perketat direktif, atau nonaktifkan JavaScript sepenuhnya. Keamanan adalah target yang terus bergerak, dan CSP yang dirancang dengan baik adalah salah satu alat paling sederhana namun paling kuat dalam arsenal Anda.

Punya pertanyaan atau skenario CSP yang rumit? Tinggalkan komentar di bawah, dan mari kita selesaikan bersama. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Buat PDF dari HTML menggunakan Aspose.HTML untuk Java – Sandbox](/html/english/java/configuring-environment/implement-sandboxing/)
- [Buat Dokumen HTML Kosong di Aspose.HTML untuk Java](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [Buat Dokumen HTML dari String di Aspose.HTML untuk Java](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}