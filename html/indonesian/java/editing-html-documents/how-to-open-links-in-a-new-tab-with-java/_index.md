---
category: general
date: 2026-10-28
description: Pelajari cara membuka tautan di tab baru dengan mem‑parsing HTML di Java,
  menemukan tautan eksternal, dan menambahkan target='_blank'.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: id
lastmod: 2026-10-28
og_description: 'Buka tautan di tab baru menggunakan Java: parsing HTML, temukan tautan
  eksternal, tambahkan target blank, dan simpan HTML yang telah dimodifikasi.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Buka tautan di tab baru dengan Java – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: Cara membuka tautan di tab baru dengan Java
url: /id/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuka tautan di tab baru dengan Java

Jika Anda perlu **membuka tautan di tab baru** dari file HTML statis, panduan ini menunjukkan secara tepat cara melakukannya. Anda akan belajar **mem-parse HTML di Java**, **menemukan tautan eksternal**, **menambahkan target blank**, dan **menyimpan HTML yang telah dimodifikasi** tanpa meninggalkan IDE Anda.

Membuka tautan eksternal di tab browser baru meningkatkan pengalaman pengguna dan menjaga pengunjung tetap berada di halaman asli. Solusi di bawah ini bekerja dengan dokumen HTML apa pun, hanya memerlukan pustaka jsoup yang populer, dan berjalan pada Java 8 atau yang lebih baru.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* JDK 8 + terpasang  
* Alat build (Maven atau Gradle) untuk mengambil dependensi **jsoup**  
* File HTML yang berisi tag anchor dengan kelas `external`

Anda tidak memerlukan server web atau kerangka kerja tambahan—jsoup menangani semuanya secara lokal.

## Langkah 1: Siapkan jsoup dalam proyek Anda

Tambahkan jsoup sebagai dependensi. Jika Anda menggunakan Maven, letakkan ini di `pom.xml`:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Untuk Gradle, tambahkan baris berikut ke `build.gradle`:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Koordinat ini mengambil rilis stabil terbaru (per Oktober 2026). Setelah sinkronisasi, Anda dapat mengimpor kelas `org.jsoup` dalam file sumber Java Anda.

## Langkah 2: Parse dokumen HTML

Mem-parse file adalah langkah pertama menuju **open links new tab**. Metode `Jsoup.parse` membaca file ke dalam struktur mirip DOM yang dapat diubah.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*Mengapa ini penting*: `Document` memberi Anda selector bergaya CSS, sehingga mudah menemukan elemen yang Anda butuhkan.

## Langkah 3: Temukan tautan eksternal

Sekarang temukan setiap elemen `<a>` yang memiliki kelas `external`. Ini memenuhi kebutuhan **find external links**.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` adalah kumpulan node yang cocok. Jika selector mengembalikan set kosong, HTML Anda mungkin tidak memiliki kelas tersebut atau menggunakan konvensi penamaan yang berbeda—sesuaikan selector sesuai kebutuhan.

## Langkah 4: Tambahkan `target="_blank"` ke setiap tautan

Untuk setiap node yang dikembalikan oleh **find external links**, setel atribut `target` menjadi `_blank`. Ini memenuhi langkah **add target blank** dan memastikan browser membuka tautan di tab baru.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

Metode `attr` menimpa nilai `target` yang ada, menjamin perilaku konsisten pada semua anchor eksternal.

## Langkah 5: Simpan HTML yang telah dimodifikasi

Setelah memperbarui DOM, tulis perubahan kembali ke file. Ini menyelesaikan bagian **save modified html** dari tutorial.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` men-serialize seluruh dokumen, mempertahankan indentasi dan format sebagaimana jsoup mem-parsenya.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua langkah menghasilkan program mandiri yang dapat Anda salin, tempel, dan jalankan.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### Output yang diharapkan

Anggap `sample.html` berisi:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

Setelah menjalankan program, `updated.html` akan berisi:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

Hanya tautan eksternal yang menerima atribut `target="_blank"`, yang berarti browser kini akan membuka tautan tersebut di tab baru.

## Tips profesional dan jebakan umum

* **Tip pro:** Jika Anda perlu memperlakukan tautan yang dimulai dengan `http://` atau `https://` sebagai eksternal meskipun tanpa kelas CSS, perluas selector: `doc.select("a[href^=http]")`.
* **Kasus tepi:** Beberapa halaman sudah menentukan `target="_self"`; pemanggilan `attr` akan menimpanya, memastikan perilaku konsisten.
* **Kinerja:** Untuk file HTML yang sangat besar, pertimbangkan parsing streaming (`Jsoup.parse(File, String, String, Parser.htmlParser())`) untuk mengurangi penggunaan memori.
* **Pengujian:** Verifikasi hasil dengan membuka `updated.html` di browser dan memeriksa tautan menggunakan developer tools—cari atribut `target`.

## Kesimpulan

Anda kini memiliki solusi lengkap dan dapat dijalankan untuk **open links in a new tab** menggunakan Java. Tutorial ini mencakup cara **parse html in java**, **find external links**, **add target blank**, dan **save modified html**, semuanya dengan pustaka ringan jsoup.

Dari sini Anda dapat:

* Memperluas selector untuk menangani pola tautan lain (mis., `rel="external"`).  
* Menggabungkan logika ini dengan langkah build yang memproses semua file HTML dalam proyek.  
* Mengintegrasikan kode ke dalam pipeline manajemen konten yang lebih besar.

Silakan bereksperimen dengan selector atau format output yang berbeda, dan bagikan hasil Anda dengan komunitas!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Create new html element with Java – Full Aspose.HTML Guide](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}