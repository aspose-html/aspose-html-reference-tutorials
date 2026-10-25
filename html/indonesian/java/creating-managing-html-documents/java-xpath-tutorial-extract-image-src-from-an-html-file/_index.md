---
category: general
date: 2026-10-25
description: Tutorial Java XPath menunjukkan cara membaca file HTML dengan Java, memuat
  dokumen HTML dengan Java, dan mengekstrak src gambar dengan Java menggunakan XPath.
  Contoh lengkap yang dapat dijalankan disertakan.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- java xpath tutorial
- read html file java
- load html document java
- get attribute xpath java
- extract image src java
language: id
lastmod: 2026-10-25
og_description: Tutorial Java XPath memandu Anda melalui membaca file HTML, memuat
  dokumen, dan mengekstrak atribut src gambar dengan XPath di Java.
og_image_alt: Diagram illustrating a Java XPath query that extracts image src attributes
  from an HTML document
og_title: Tutorial Java XPath – ekstrak src gambar dari file HTML
schemas:
- author: Aspose
  dateModified: '2026-10-25'
  description: Java XPath tutorial shows how to read HTML file Java, load HTML document
    Java, and extract image src Java using XPath. Complete, runnable example included.
  headline: 'Java XPath tutorial: extract image src from an HTML file'
  type: TechArticle
tags:
- Java
- XPath
- HTML parsing
- Aspose.HTML
title: 'Tutorial Java XPath: mengekstrak src gambar dari file HTML'
url: /id/java/creating-managing-html-documents/java-xpath-tutorial-extract-image-src-from-an-html-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java XPath tutorial – mengekstrak src gambar dari file HTML

Jika Anda membutuhkan **java xpath tutorial**, panduan ini menunjukkan cara membaca file HTML, memuat dokumen HTML, dan mengekstrak atribut `src` setiap gambar menggunakan XPath. Anda akan melihat program lengkap yang siap dikompilasi dan memahami mengapa setiap langkah penting.

Membaca file HTML di Java dapat terasa rumit, terutama ketika Anda juga perlu melakukan kueri pada DOM. Tutorial ini menghilangkan dugaan dengan menggunakan Aspose.HTML untuk Java, sebuah pustaka yang mengimplementasikan W3C DOM dan dukungan XPath penuh. Pada akhir panduan Anda akan dapat menjalankan kode, melihat URL gambar yang dicetak, dan menyesuaikan pola ini untuk atribut lain yang Anda perlukan.

## Prasyarat

Anda harus memiliki:

- JDK 17 atau yang lebih baru terpasang  
- Maven 3.8+ (atau alat build apa pun yang dapat menambahkan dependensi Maven)  
- Familiaritas dasar dengan sintaks Java dan konsep XPath  

Tidak ada plugin IDE tambahan yang diperlukan; editor apa pun yang dapat mengompilasi Java akan berfungsi.

## Langkah 1: Tambahkan Aspose.HTML untuk Java ke proyek Anda

Aspose.HTML menyediakan implementasi DOM yang kuat dan bekerja mulus dengan XPath. Tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Jika Anda lebih suka Gradle, setaraannya adalah  
> `implementation 'com.aspose:aspose-html:23.12'`.

Menyertakan pustaka ini memberi Anda kelas `HTMLDocument` yang akan digunakan nanti untuk **load html document java**‑style files.

## Langkah 2: Baca file HTML dan muat dokumen

Aksi kode pertama yang sesungguhnya adalah **read html file java**‑wise. Letakkan file HTML bernama `page.html` di folder bernama `resources` yang berada relatif terhadap root proyek Anda:

```html
<!-- resources/page.html -->
<!DOCTYPE html>
<html>
<head><title>Sample Page</title></head>
<body>
    <h1>Welcome</h1>
    <img src="images/logo.png" alt="Logo">
    <img src="images/banner.jpg" alt="Banner">
</body>
</html>
```

Sekarang muat file tersebut dengan Aspose.HTML:

```java
import com.aspose.html.HTMLDocument;

public class XPathQuery {
    public static void main(String[] args) throws Exception {
        // Load the HTML document from the file system
        HTMLDocument document = new HTMLDocument("resources/page.html");
        // Further processing follows...
    }
}
```

Konstruktor `HTMLDocument` melakukan operasi **load html document java** yang mengurai markup menjadi pohon DOM siap untuk kueri XPath.

## Langkah 3: Jalankan kueri XPath untuk memilih semua elemen `<img>`

XPath memungkinkan Anda menemukan node dengan satu ekspresi. Untuk **extract image src java**, kita membutuhkan setiap elemen `<img>`:

```java
import com.aspose.html.dom.NodeList;

// Inside main, after loading the document
NodeList imageNodes = document.selectNodes("//img");
```

Ekspresi `//img` berarti “pilih setiap elemen `img` di mana saja dalam dokumen.” Aspose.HTML mengevaluasi kueri tersebut terhadap DOM yang baru saja kita muat.

## Langkah 4: Dapatkan atribut `src` untuk setiap gambar

Sekarang kita **get attribute xpath java**‑style nilai dari node yang dipilih. Setiap node di‑cast ke `HTMLElement` sehingga kita dapat memanggil `getAttribute`:

```java
import com.aspose.html.dom.HTMLElement;

for (int i = 0; i < imageNodes.getLength(); i++) {
    HTMLElement img = (HTMLElement) imageNodes.item(i);
    String src = img.getAttribute("src");
    System.out.println("Image src: " + src);
}
```

Pemanggilan `getAttribute` mengambil string `src` mentah persis seperti yang muncul dalam sumber HTML. Inilah inti dari operasi **extract image src java**.

## Langkah 5: Jalankan program dan verifikasi output

Kompilasi dan jalankan kelas:

```bash
mvn compile exec:java -Dexec.mainClass=XPathQuery
```

Anda seharusnya melihat:

```
Image src: images/logo.png
Image src: images/banner.jpg
```

Jika output cocok dengan tag `<img>` di `page.html`, **java xpath tutorial** berhasil. Anda kini dapat mengganti ekspresi XPath atau nama atribut untuk menyesuaikan tugas ekstraksi lain (mis., `//a/@href` untuk mengumpulkan tautan).

## Variasi umum dan kasus tepi

| Situasi | Penyesuaian | Mengapa penting |
|-----------|------------|----------------|
| **HTML berisi namespace** | Use `document.selectNodes("//*[local-name()='img']")` | XPath tanpa prefiks namespace tetap dapat mencocokkan elemen. |
| **Path relatif** | Resolve `src` against the document’s base URI with `new URL(document.getBaseUrl(), src)` | Menjamin URL absolut untuk pemrosesan selanjutnya. |
| **File besar** | Stream the file with `HTMLDocument`’s `load` overload that accepts an `InputStream` | Mengurangi tekanan memori untuk HTML berukuran gigabyte. |
| **Atribut `src` hilang** | Check `src != null` before printing | Mencegah output `null` untuk tag yang tidak terbentuk dengan benar. |

Variasi‑variasi ini menjaga tutorial tetap relevan di proyek dunia nyata.

## Kode sumber lengkap yang dapat dijalankan

```java
// File: src/main/java/XPathQuery.java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.*;

public class XPathQuery {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the HTML document from a file
        HTMLDocument document = new HTMLDocument("resources/page.html");

        // Step 2: Use XPath to select all <img> elements
        NodeList imageNodes = document.selectNodes("//img");

        // Step 3: Iterate over the selected nodes and print each image's src attribute
        for (int i = 0; i < imageNodes.getLength(); i++) {
            HTMLElement imgElement = (HTMLElement) imageNodes.item(i);
            String src = imgElement.getAttribute("src");
            System.out.println("Image src: " + src);
        }
    }
}
```

Letakkan file Java di bawah `src/main/java/`, pertahankan `page.html` di bawah `resources/`, dan jalankan perintah Maven yang ditunjukkan sebelumnya. Program ini mendemonstrasikan **java xpath tutorial** yang bersih untuk membaca file HTML, memuat dokumen, menjalankan kueri XPath, dan mengekstrak nilai atribut.

## Kesimpulan

**java xpath tutorial** ini telah memandu Anda melalui proses membaca file HTML, memuat dokumen dengan Aspose.HTML, mengeksekusi kueri XPath, dan **extracting image src java**. Anda kini memiliki pola yang dapat digunakan kembali untuk ekstraksi atribut apa pun (`get attribute xpath java`) dan dapat memperluasnya ke kueri yang lebih kompleks.

Selanjutnya, jelajahi topik terkait seperti **read html file java** dengan Jsoup untuk parsing ringan, atau gabungkan XPath dengan selector CSS untuk strategi hibrida. Bereksperimenlah dengan berbagai sumbu XPath (`ancestor::`, `following-sibling::`) untuk mengambil konteks sekitarnya, dan Anda akan cepat menguasai navigasi DOM di Java.

Selamat berkoding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Muat Dokumen HTML Java – Panduan Lengkap dengan XPath & CSS](/html/english/java/creating-managing-html-documents/load-html-document-java-complete-guide-with-xpath-css/)
- [Iterasi NodeList Java – Baca HTML & Dapatkan src Gambar](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Cara Menggunakan XPath di Java – Baca HTML dan Ekstrak Teks](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}