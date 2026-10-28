---
category: general
date: 2026-10-28
description: Cara membaca HTML di Java dan mengekstrak teks dari file HTML. Pelajari
  cara mengonversi HTML menjadi teks dengan Jsoup, mencakup teknik membaca HTML dari
  file dan mengubah HTML menjadi teks di Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: id
lastmod: 2026-10-28
og_description: Cara membaca HTML di Java dan mengekstrak teks dari file HTML. Tutorial
  ini menunjukkan solusi lengkap untuk mengonversi HTML menjadi teks menggunakan Jsoup.
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: Cara membaca HTML dan mengekstrak teks di Java – panduan singkat
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  headline: How to read HTML and extract text in Java – a step‑by‑step guide
  type: TechArticle
- description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  name: How to read HTML and extract text in Java – a step‑by‑step guide
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>org.jsoup</groupId> <artifactId>jsoup</artifactId>
      <version>1.17.2</version> </dependency> ```'
  - name: Gradle
    text: '```gradle implementation ''org.jsoup:jsoup:1.17.2'' ```'
  - name: Expected output
    text: 'Assuming `input.html` contains:'
  - name: Running the program
    text: '```bash javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java java -cp .:jsoup-1.17.2.jar
      HtmlToTextDemo ```'
  type: HowTo
tags:
- Java
- HTML parsing
- Text extraction
title: Cara membaca HTML dan mengekstrak teks di Java – panduan langkah demi langkah
url: /id/java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membaca HTML dan mengekstrak teks di Java – panduan langkah demi langkah

Jika Anda perlu **how to read html** dari file lokal, panduan ini menyediakan solusi lengkap. Anda akan belajar memuat dokumen HTML, mengekstrak teks polos, dan secara opsional mengonversi HTML ke teks dengan kontrol yang halus. Pada akhir tutorial Anda dapat menjalankan kode contoh dan melihat teks yang diekstrak dicetak di konsol.

Membaca file HTML adalah tugas umum saat memproses data yang di‑scrape dari web, menghasilkan laporan, atau membersihkan konten yang dibuat pengguna. Langkah‑langkah di bawah ini mencakup semua yang Anda butuhkan, mulai dari menambahkan pustaka yang diperlukan hingga menangani kasus tepi seperti markup yang rusak atau masalah pengkodean karakter.

## Apa yang Anda butuhkan

- Java 17 atau lebih baru (kode dapat dikompilasi dengan versi sebelumnya juga)
- Maven atau Gradle untuk manajemen dependensi, atau JAR Jsoup yang ditambahkan secara manual
- File HTML bernama `input.html` yang ditempatkan di direktori `src/main/resources` proyek (Anda dapat mengubah jalurnya nanti)

## Siapkan pustaka Jsoup

Jsoup adalah pustaka ringan yang terdokumentasi dengan baik yang mem‑parse HTML menjadi struktur mirip DOM. Ia menangani HTML yang rusak dengan elegan, sehingga ideal untuk tugas **extract text from html**.

### Maven

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

### Gradle

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Jika Anda lebih suka mengunduh secara manual, letakkan JAR pada classpath Anda dan impor `org.jsoup.*` di file sumber Anda.

## Muat HTML dari file

Langkah programatik pertama adalah membaca file ke dalam objek `Document`. Jsoup menyediakan metode statis `parse` yang menerima `File` dan nama charset.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Path to the HTML file – adjust if your file lives elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Parse the file using UTF‑8 encoding
            Document doc = Jsoup.parse(input, "UTF-8");
            // Continue with text extraction…
        } catch (IOException e) {
            System.err.println("Failed to read the HTML file: " + e.getMessage());
        }
    }
}
```

**Mengapa ini penting:** `Jsoup.parse(File, String)` membaca byte mentah, mendekodenya sesuai charset yang diberikan, dan membangun DOM yang bersih. Pendekatan ini lebih aman daripada membaca file ke string sendiri karena Jsoup menormalkan akhir baris dan memperbaiki kesalahan markup umum secara otomatis.

## Ekstrak teks polos dari HTML

Setelah Anda memiliki `Document`, mengambil teks yang terlihat cukup dengan satu pemanggilan metode. Metode `text()` menggabungkan konten tekstual semua elemen sambil membuang tag, skrip, dan gaya.

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

Pemanggilan `body()` membatasi ekstraksi ke elemen `<body>`, yang biasanya menjadi target ketika Anda **read html from file** untuk analisis konten. String yang dihasilkan berisi spasi yang dipadatkan menjadi satu spasi, meniru cara browser menampilkan teks.

### Output yang diharapkan

Misalkan `input.html` berisi:

```html
<!DOCTYPE html>
<html>
<head><title>Sample</title></head>
<body>
  <h1>Hello World</h1>
  <p>This is a <strong>demo</strong> page.</p>
</body>
</html>
```

Menjalankan program mencetak:

```
Extracted text:
Hello World This is a demo page.
```

## Konversi HTML ke teks dengan opsi tambahan

Kadang‑kadang Anda memerlukan kontrol lebih daripada yang disediakan `text()`—misalnya, mempertahankan jeda baris, menjaga penomoran daftar, atau mengabaikan tag tertentu. `NodeTraversor` Jsoup yang dipadukan dengan `NodeVisitor` khusus memberi Anda fleksibilitas tersebut.

```java
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

public class HtmlToTextDemo {

    // ... (main method unchanged)

    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();
        NodeVisitor visitor = new NodeVisitor() {
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Preserve line breaks for block elements
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }
            public void tail(Node node, int depth) {
                // No action needed on exit
            }
        };
        NodeTraversor.traverse(visitor, doc.body());
        // Collapse multiple newlines into a single one
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

Ganti pemanggilan sederhana `doc.body().text()` dengan:

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**Mengapa ini berhasil:** Visitor berjalan menelusuri DOM secara depth‑first, menambahkan baris baru sebelum setiap elemen tingkat blok (mis., `<p>`, `<div>`, `<h1>`). Ini menjaga pemisahan paragraf, yang berguna ketika Anda **convert html to text** untuk keterbacaan atau pipeline NLP selanjutnya.

## Kesalahan umum dan praktik terbaik

| Issue | Why it occurs | Recommended fix |
|-------|---------------|-----------------|
| Wrong charset | Files saved in ISO‑8859‑1 but parsed as UTF‑8 produce garbled characters. | Detect the charset from the file’s meta tag (`<meta charset="...">`) or pass the correct name to `Jsoup.parse`. |
| Large files | Loading a very large HTML file into memory can cause `OutOfMemoryError`. | Stream the file with `Jsoup.parse(File, String, String baseUri)` and process nodes incrementally, or increase the JVM heap size. |
| Unwanted script/style text | `text()` removes script and style content, but custom visitors may unintentionally include it. | Skip nodes whose tag name is `script` or `style` inside the visitor’s `head` method. |
| Preserving whitespace | Collapsing spaces may lose formatting needed for markdown conversion. | Use `Element.wholeText()` for raw text nodes, then post‑process whitespace manually. |

Menangani masalah‑masalah ini memastikan solusi **html to text java** Anda bekerja secara andal pada berbagai input.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program mandiri yang mendemonstrasikan seluruh alur kerja—dari penyiapan dependensi hingga verifikasi output. Salin kode ke file bernama `HtmlToTextDemo.java`, letakkan file `input.html` di sampingnya, dan jalankan `javac && java` seperti yang ditunjukkan.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Adjust the path if your HTML file is located elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Load and parse the HTML file using UTF‑8
            Document doc = Jsoup.parse(input, "UTF-8");

            // Simple extraction – suitable for most cases
            String plain = doc.body().text();
            System.out.println("=== Simple extraction ===");
            System.out.println(plain);
            System.out.println();

            // Detailed conversion – keeps line breaks for readability
            String detailed = convertHtmlToText(doc);
            System.out.println("=== Detailed conversion ===");
            System.out.println(detailed);
        } catch (IOException e) {
            System.err.println("Error reading HTML file: " + e.getMessage());
        }
    }

    /**
     * Walks the DOM and builds a text representation that preserves
     * line breaks for block‑level elements.
     *
     * @param doc the parsed HTML document
     * @return a readable plain‑text version of the HTML body
     */
    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();

        NodeVisitor visitor = new NodeVisitor() {
            @Override
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Add a newline before block elements (e.g., <p>, <div>, <h1>)
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }

            @Override
            public void tail(Node node, int depth) {
                // No operation needed when exiting a node
            }
        };

        NodeTraversor.traverse(visitor, doc.body());

        // Collapse consecutive newlines and trim leading/trailing whitespace
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

### Menjalankan program

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

Konsol menampilkan baik ekstraksi sederhana maupun yang detail

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Use XPath in Java – Read HTML and Extract Text](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Extract text from HTML with Java – Complete Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}