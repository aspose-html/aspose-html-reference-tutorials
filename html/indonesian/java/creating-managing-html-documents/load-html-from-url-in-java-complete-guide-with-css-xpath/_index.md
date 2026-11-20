---
category: general
date: 2026-07-02
description: Muat HTML dari URL menggunakan Aspose.HTML untuk Java, lalu pilih elemen
  dengan atribut, ekstrak tautan unduhan, dan hitung node XPath dalam beberapa langkah
  mudah.
draft: false
keywords:
- load html from url
- select elements with attribute
- extract download links
- search html with css
- count xpath nodes
language: id
og_description: Muat HTML dari URL di Java, kemudian gunakan selector CSS dan XPath
  untuk memilih elemen dengan atribut, mengekstrak tautan unduhan, dan menghitung
  node XPath.
og_title: Muat HTML dari URL di Java – Tutorial Lengkap CSS & XPath
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Load HTML from URL using Aspose.HTML for Java, then select elements
    with attribute, extract download links, and count XPath nodes in a few easy steps.
  headline: Load HTML from URL in Java – Complete Guide with CSS & XPath
  type: TechArticle
- description: Load HTML from URL using Aspose.HTML for Java, then select elements
    with attribute, extract download links, and count XPath nodes in a few easy steps.
  name: Load HTML from URL in Java – Complete Guide with CSS & XPath
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-html</artifactId>
      <version>23.10</version> <!-- Check for the latest version --> </dependency>
      ```'
  - name: Gradle
    text: '```gradle implementation ''com.aspose:aspose-html:23.10'' ```'
  - name: What the selector means
    text: '| Part | Meaning | |------|---------| | `a` | any `<a>` element | | `[href*=''download'']`
      | attribute `href` that **contains** the substring `download` (`*=` is the “contains”
      operator) |'
  - name: Expected console output (may vary by site)
    text: '``` Document loaded from https://example.com'
  type: HowTo
tags:
- Java
- Aspose.HTML
- Web Scraping
title: Muat HTML dari URL di Java – Panduan Lengkap dengan CSS & XPath
url: /id/java/creating-managing-html-documents/load-html-from-url-in-java-complete-guide-with-css-xpath/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Memuat HTML dari URL di Java – Panduan Lengkap dengan CSS & XPath

Pernahkah Anda perlu **memuat HTML dari URL** dalam aplikasi Java dan mengambil tautan‑tautan tertentu tanpa menulis perayap web yang lengkap? Anda tidak sendirian. Baik Anda sedang membangun pengelola unduhan, agregator konten, atau sekadar penasaran dengan halaman‑halaman yang Anda kunjungi, kemampuan untuk mengambil sebuah halaman, **menelusuri HTML dengan CSS**, dan kemudian **menghitung node XPath** adalah keterampilan yang sangat berguna.

Dalam tutorial ini kami akan membahas seluruh proses: mulai dari mengambil halaman remote ke memori, menggunakan selector CSS untuk **memilih elemen dengan atribut**, mengekstrak **tautan unduhan**, dan akhirnya memverifikasi hasil yang sama dengan kueri XPath. Tanpa layanan eksternal, hanya Java murni dan pustaka Aspose.HTML untuk Java.

> **Prasyarat** – Anda memerlukan Java 8+ terpasang, Maven atau Gradle untuk manajemen dependensi, dan pemahaman dasar tentang HTML serta sintaks Java. Jika Anda baru mengenal Aspose.HTML, jangan khawatir; kami akan membahas penyiapannya langkah demi langkah.

---

## Apa yang Akan Anda Bangun

Pada akhir panduan ini Anda akan memiliki kelas Java yang dapat dijalankan yang:

1. **Memuat HTML dari sebuah URL** (misalnya `https://example.com`).
2. **Menelusuri DOM dengan selector CSS** untuk menemukan setiap tag `<a>` yang `href`‑nya mengandung kata “download”.
3. **Mengekstrak dan mencetak setiap tautan unduhan**.
4. **Menjalankan kueri XPath yang setara** dan mencetak berapa banyak node yang ditemukan.

Anda juga akan melihat diagram kecil yang memvisualisasikan alur—untuk membantu Anda yang belajar secara visual.

![Diagram yang menunjukkan alur memuat HTML dari URL, memilih elemen, mengekstrak tautan, dan menghitung node XPath](load-html-from-url-diagram.png)

---

## Langkah 1: Tambahkan Aspose.HTML untuk Java ke Proyek Anda

Langkah pertama. Aspose.HTML adalah pustaka komersial, tetapi menyediakan versi percobaan gratis yang bekerja sempurna untuk tujuan belajar.

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

### Gradle

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

> **Tips pro:** Jika Anda mendapatkan `NoClassDefFoundError` nanti, periksa kembali bahwa jar `aspose-html` berada di classpath runtime Anda.

---

## Langkah 2: Muat HTML dari URL dan Inisialisasi Dokumen

Setelah pustaka tersedia, kita dapat **memuat HTML dari URL**. Kelas `HTMLDocument` menerima string URL dan menangani permintaan HTTP, pengalihan, serta deteksi set karakter untuk Anda.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;

public class HtmlDownloader {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Define the target page
        String pageUrl = "https://example.com";

        // Step 2.2: Load the page into an HTMLDocument object
        HTMLDocument document = new HTMLDocument(pageUrl);

        System.out.println("Document loaded successfully.");
        // From here on we can query the DOM.
    }
}
```

**Mengapa ini berhasil:** `HTMLDocument` secara internal membuat `HttpWebRequest`, mengikuti pengalihan, dan membangun pohon DOM yang berperilaku seperti `document` pada browser. Itu berarti kita dapat langsung menggunakan selector CSS maupun XPath.

---

## Langkah 3: Telusuri HTML dengan CSS – Pilih Elemen dengan Atribut

Cara paling mudah dibaca untuk menemukan elemen adalah dengan selector CSS. Dalam kasus kita, kita menginginkan setiap `<a>` yang atribut `href`‑nya mengandung kata “download”. Sintaks selector `a[href*='download']` melakukan hal itu.

```java
// Step 3: Find all anchor elements whose href contains "download"
NodeList downloadLinks = document.selectElements("a[href*='download']");

// Quick sanity check – how many did we find?
System.out.println("CSS found " + downloadLinks.getLength() + " nodes.");
```

### Apa arti selector tersebut

| Bagian | Makna |
|--------|-------|
| `a` | elemen `<a>` apa saja |
| `[href*='download']` | atribut `href` yang **mengandung** substring `download` (`*=` adalah operator “contains”) |

> **Kasus khusus:** Jika halaman menggunakan URL relatif (misalnya `href="/files/download.zip"`), Aspose.HTML akan mempertahankannya apa adanya. Anda mungkin perlu menyelesaikannya terhadap URL dasar kemudian.

---

## Langkah 4: Ekstrak Tautan Unduhan

Setelah kita memiliki `NodeList`, mengekstrak URL sebenarnya menjadi sangat mudah. Kita akan meng-cast setiap node menjadi `Element` dan membaca atribut `href`‑nya.

```java
System.out.println("\n--- Extracted Download Links ---");
for (int i = 0; i < downloadLinks.getLength(); i++) {
    Element anchor = (Element) downloadLinks.item(i);
    String href = anchor.getAttribute("href");
    // Resolve relative URLs to absolute ones (optional but handy)
    String absoluteHref = document.getBaseUrl().resolve(href).toString();
    System.out.println(absoluteHref);
}
```

**Hasil yang akan Anda lihat** (contoh output):

```
CSS found 3 nodes.

--- Extracted Download Links ---
https://example.com/files/report-download.pdf
https://example.com/downloads/setup.exe
https://cdn.example.com/assets/manual-download.docx
```

Jika Anda hanya memerlukan nilai atribut mentah, lewati pemanggilan `resolve`. Langkah resolusi berguna ketika Anda nanti memberi tautan‑tautan tersebut ke pengunduh.

---

## Langkah 5: Telusuri HTML dengan XPath – Hitung Node XPath

Kadang Anda lebih suka XPath—terutama ketika membutuhkan kueri hierarki yang lebih kompleks. Ekspresi XPath yang setara dengan selector CSS kita adalah:

```xpath
//a[contains(@href,'download')]
```

Mari jalankan dan lihat berapa banyak node yang didapatkan.

```java
// Step 5: Perform the same search using XPath
NodeList xpathNodes = document.selectNodes("//a[contains(@href,'download')]");

// Output the count
System.out.println("\nXPath found " + xpathNodes.getLength() + " nodes.");
```

Output seharusnya cocok dengan hitungan CSS, menegaskan bahwa kedua pendekatan tersebut setara:

```
XPath found 3 nodes.
```

> **Mengapa keduanya?** Menggunakan kedua selector dalam basis kode yang sama memberi Anda fleksibilitas. CSS ringkas untuk pemeriksaan atribut sederhana, sementara XPath unggul ketika Anda perlu menavigasi ke atas/bawah pohon atau menggabungkan beberapa kondisi.

---

## Langkah 6: Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut kelas lengkap yang dapat Anda salin‑tempel ke IDE dan jalankan langsung.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;

public class QueryExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the HTML document from a web page
        String url = "https://example.com";
        HTMLDocument document = new HTMLDocument(url);
        System.out.println("Document loaded from " + url);

        // 2️⃣ Search HTML with CSS – select elements with attribute
        NodeList cssMatches = document.selectElements("a[href*='download']");
        System.out.println("\nCSS found " + cssMatches.getLength() + " nodes.");

        // 3️⃣ Extract download links
        System.out.println("\n--- Extracted Download Links ---");
        for (int i = 0; i < cssMatches.getLength(); i++) {
            Element anchor = (Element) cssMatches.item(i);
            String href = anchor.getAttribute("href");
            // Resolve relative URLs (optional)
            String absolute = document.getBaseUrl().resolve(href).toString();
            System.out.println(absolute);
        }

        // 4️⃣ Search HTML with XPath – count xpath nodes
        NodeList xpathMatches = document.selectNodes("//a[contains(@href,'download')]");
        System.out.println("\nXPath found " + xpathMatches.getLength() + " nodes.");
    }
}
```

### Output konsol yang diharapkan (bisa berbeda tergantung situs)

```
Document loaded from https://example.com

CSS found 3 nodes.

--- Extracted Download Links ---
https://example.com/files/report-download.pdf
https://example.com/downloads/setup.exe
https://cdn.example.com/assets/manual-download.docx

XPath found 3 nodes.
```

Jalankan program, dan Anda akan langsung melihat semua tautan yang mengandung “download”. Ubah selector atau string XPath untuk menyesuaikan kriteria Anda—misalnya `a[href$='.pdf']` untuk hanya PDF, atau `//div[@class='product']//a` untuk halaman produk.

---

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Gejala | Solusi |
|---------|--------|--------|
| **Kesalahan sertifikat HTTPS** | `javax.net.ssl.SSLHandshakeException` | Tambahkan trust manager atau gunakan URL dengan sertifikat yang valid. Untuk pengujian cepat, Anda dapat menonaktifkan validasi sertifikat, tetapi jangan pernah di produksi. |
| **Loop pengalihan** | Program hang atau melempar `Too many redirects` | Tetapkan batas pengalihan yang wajar (`document.setRedirectLimit(5)`) atau periksa URL target secara manual. |
| **URL relatif** | Tautan yang diekstrak dimulai dengan `/` alih‑alih domain lengkap | Gunakan `document.getBaseUrl().resolve(relative)` seperti pada contoh. |
| **Halaman besar** | Penggunaan memori tinggi | Stream respons atau gunakan overload `HTMLDocument` yang membatasi ukuran DOM. |
| **Lisensi Aspose hilang** | Runtime melempar `LicenseException` setelah percobaan berakhir | Beli lisensi atau terus gunakan percobaan untuk eksperimen non‑komersial. |

---

## Langkah Selanjutnya & Topik Terkait

- **Unduh berkas** – gabungkan URL yang diekstrak dengan `HttpURLConnection` Java atau Apache HttpClient untuk benar‑benarnya mengambil sumber daya.
- **Pemrosesan paralel** – gunakan `CompletableFuture` untuk mengunduh beberapa berkas secara bersamaan.
- **Selector CSS lanjutan** – coba `a[href$='.zip']` untuk ekstensi berkas, atau `div[data-id]` untuk memilih elemen dengan atribut khusus.
- **Fungsi XPath** – jelajahi `starts-with()`, `ends-with()`, dan operator logika (`and`, `or`) untuk kueri yang lebih detail.
- **Sanitisasi HTML** – jika Anda berencana menampilkan HTML yang diambil, pertimbangkan menggunakan pustaka seperti Jsoup untuk membersihkannya.

---

## Kesimpulan

Kami baru saja mendemonstrasikan cara **memuat HTML dari URL** di Java, kemudian **menelusuri HTML dengan CSS** untuk **memilih elemen dengan atribut**, **mengekstrak tautan unduhan**, dan akhirnya **menghitung node XPath** untuk memverifikasi hasil. Pendekatan ini ringkas, bergantung pada satu pustaka, dan bekerja untuk tugas‑tugas scraping sederhana maupun analisis DOM yang lebih canggih.

Silakan sesuaikan selector‑selectornya


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik‑topik yang berhubungan erat dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Load HTML Documents from Stream with Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Handle Document Load Events in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}