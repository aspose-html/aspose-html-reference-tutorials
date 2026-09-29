---
category: general
date: 2026-09-29
description: Pelajari cara memilih elemen berdasarkan kelas, membaca HTML dari file,
  dan menemukan tautan eksternal dalam Java. Panduan langkah demi langkah ini mencakup
  iterasi NodeList secara efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: id
lastmod: 2026-09-29
og_description: Pilih elemen berdasarkan kelas di Java, baca HTML dari file, dan temukan
  tautan eksternal menggunakan querySelectorAll. Ikuti contoh lengkap untuk mengiterasi
  NodeList.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Pilih elemen berdasarkan kelas di Java – panduan lengkap dengan querySelectorAll
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: Cara memilih elemen berdasarkan kelas di Java menggunakan querySelectorAll
url: /id/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara memilih elemen berdasarkan kelas di Java menggunakan querySelectorAll

Jika Anda perlu **memilih elemen berdasarkan kelas** saat memproses file HTML di Java, panduan ini menunjukkan secara tepat cara melakukannya. Anda akan belajar membaca HTML dari file, menggunakan `querySelectorAll` untuk menemukan tautan eksternal, dan mengiterasi `NodeList` yang dihasilkan dengan aman.

Bekerja dengan HTML di Java sering terasa berat, tetapi pustaka modern memberi Anda API berbasis selector CSS yang ringkas. Contoh di bawah menggunakan **jsoup** (versi 1.17.2) karena ia mengimplementasikan selector bergaya `querySelectorAll` dan mengembalikan koleksi `Elements` yang berperilaku seperti `NodeList`. Anda dapat menyesuaikan logika yang sama ke implementasi DOM lain bila diperlukan.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* JDK 17 atau lebih baru terpasang.
* Maven atau Gradle untuk manajemen dependensi.
* Familiaritas dasar dengan stream Java dan model DOM.

Tambahkan jsoup ke proyek Anda:

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## Langkah 1: Baca HTML dari file

Tugas pertama adalah memuat dokumen HTML dari disk. `Jsoup.parse(Path, Charset)` membaca file dan membangun pohon DOM yang dapat Anda query.

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*Mengapa ini penting*: Memuat file sekali saja menghindari I/O berulang saat Anda mengiterasi elemen nanti. Objek `Document` menyimpan seluruh DOM, memungkinkan query selector yang cepat.

## Langkah 2: Gunakan `querySelectorAll` untuk memilih elemen berdasarkan kelas

Setelah dokumen berada di memori, Anda dapat **memilih elemen berdasarkan kelas** menggunakan selector CSS. Selector `"a.external"` mencocokkan tag `<a>` yang memiliki kelas `external`—tepat apa yang Anda butuhkan untuk **menemukan tautan eksternal**.

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*Mengapa ini penting*: Menggunakan selector kelas bersifat ekspresif dan efisien. Pustaka menerjemahkan selector menjadi traversal yang dioptimalkan, sehingga Anda tidak perlu menulis loop manual untuk setiap node.

## Langkah 3: Iterasi NodeList (Elements) di Java

`Elements` mengimplementasikan `Iterable<Element>`, yang berarti Anda dapat menggunakan loop `for‑each` standar untuk **mengiterasi NodeList Java**. Loop di bawah mencetak atribut `href` setiap tautan.

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*Mengapa ini penting*: Iterasi langsung menjaga kode tetap terbaca dan menghindari overhead mengubah koleksi menjadi stream ketika Anda hanya memerlukan output sederhana.

## Contoh lengkap yang berfungsi

Menggabungkan ketiga langkah menghasilkan program mandiri yang dapat dijalankan dari baris perintah.

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### Output yang diharapkan

Misalkan `input.html` berisi:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

Menjalankan program mencetak:

```
External link: https://example.com
External link: https://openai.com
```

## Tips profesional dan jebakan umum

* **Encoding penting** – Selalu baca file dengan UTF‑8 (atau charset yang sesuai dengan sumber Anda). Encoding yang salah dapat merusak karakter dalam nilai atribut.
* **Beberapa kelas** – Jika sebuah elemen memiliki beberapa kelas (mis., `class="btn external"`), selector `"a.external"` tetap cocok karena selector kelas CSS memeriksa keberadaan token, bukan string lengkap.
* **Tip performa** – Jika Anda hanya membutuhkan atribut `href`, Anda dapat memintanya langsung dengan `doc.select("a.external[href]").eachAttr("href")`. Ini menghindari pembuatan objek `Element` lengkap untuk setiap kecocokan.
* **Keamanan null** – `link.attr("href")` mengembalikan string kosong jika atribut tidak ada, sehingga Anda tidak perlu memeriksa null sebelum mencetak.

## Pertanyaan yang sering diajukan

**T: Apakah ini bekerja dengan fragmen HTML yang tidak memiliki root `<html>`?**  
J: Ya. `Jsoup.parse` memperlakukan input sebagai fragmen dan secara otomatis menambahkan elemen root yang hilang, memungkinkan selector bekerja pada body fragmen.

**T: Bisakah saya menggunakan `querySelectorAll` tanpa jsoup?**  
J: API DOM standar Java (`org.w3c.dom`) tidak menyertakan `querySelectorAll`. Pustaka seperti **HTMLUnit** atau **jodd-lagarto** menyediakan metode serupa. Pola yang ditunjukkan di sini—memuat, memilih dengan CSS, mengiterasi—tetap sama.

**T: Bagaimana jika saya perlu memodifikasi tautan alih-alih hanya mencetaknya?**  
J: Setelah memperoleh setiap `Element`, Anda dapat memanggil `link.attr("href", "newUrl")` dan kemudian menulis kembali dokumen ke disk dengan `Files.writeString`.

## Kesimpulan

Anda kini tahu cara **memilih elemen berdasarkan kelas**, **membaca HTML dari file**, **menemukan tautan eksternal**, dan **mengiterasi NodeList di Java** menggunakan selector bergaya `querySelectorAll`. Contoh lengkap menunjukkan alur kerja bersih dan siap produksi yang dapat Anda sematkan dalam pipeline scraping atau transformasi yang lebih besar.

Selanjutnya, jelajahi topik terkait seperti **parsing konten dinamis dengan HTMLUnit**, **menulis HTML yang telah dimodifikasi kembali ke disk**, atau **menggunakan stream Java untuk mengumpulkan URL tautan ke dalam list**. Semua ini dibangun di atas teknik seleksi berbasis kelas yang ditunjukkan di sini. Selamat coding!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to query HTML in Java – Select elements, filter by attribute, and get text](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [Iterate NodeList Java – Read HTML & Get Image src](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}