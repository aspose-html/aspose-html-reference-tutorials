---
category: general
date: 2026-03-04
description: Cara menyorot HTML dengan mencari teks dalam HTML dan membungkus setiap
  kecocokan dengan tag <mark>. Panduan Java langkah demi langkah untuk mengganti teks
  dengan elemen mark.
draft: false
keywords:
- how to highlight html
- search text in html
- highlight word in html
- highlight occurrences of word
- replace text with mark
language: id
og_description: Cara menyorot HTML dengan mencari teks dalam HTML dan membungkus kecocokan
  dengan tag <mark>. Contoh lengkap Java untuk mengganti teks dengan mark.
og_title: Cara Menyorot HTML – Cari Teks & Ganti dengan <mark>
tags:
- Aspose.HTML
- Java
- Text Processing
title: Cara Menyorot HTML – Cari Teks & Ganti dengan <mark>
url: /id/java/editing-html-documents/how-to-highlight-html-search-text-replace-with-mark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menyorot HTML – Cari Teks & Ganti dengan `<mark>`

Pernah bertanya‑tanya **cara menyorot HTML** ketika sebuah kata muncul berkali‑kali? Mungkin Anda sedang membangun situs dokumentasi, mesin blog, atau hanya perlu menekankan nama merek di halaman statis. Kabar baiknya? Ini cukup sederhana setelah Anda tahu cara mencari teks dalam HTML dan membungkus hasilnya dengan elemen `<mark>`.

Dalam tutorial ini kami akan membahas solusi Java lengkap yang memuat file HTML, mencari kata target, mengganti setiap kemunculannya dengan tag `<mark>`, dan akhirnya menyimpan versi yang sudah disorot. Pada akhir tutorial Anda akan dapat **menyorot kata dalam HTML**, **menyorot kemunculan kata**, dan bahkan **mengganti teks dengan mark** tanpa merusak markup di sekitarnya.

> **Apa yang Anda perlukan**  
> • Java 17 atau lebih baru (kode ini juga bekerja dengan versi sebelumnya)  
> • Perpustakaan Aspose.HTML untuk Java (versi trial gratis atau salinan berlisensi)  
> • Sebuah file HTML sederhana yang ingin Anda proses  

Jika semua hal di atas sudah siap, mari kita mulai.  

![Screenshot showing highlighted HTML output – how to highlight html](/images/highlight-html-example.png "how to highlight html example")

## Langkah 1 – Muat Dokumen HTML (Cara Menyorot HTML)

Pertama kita perlu membawa file sumber ke memori. Kelas `Document` milik Aspose.HTML melakukan semua pekerjaan berat, mem-parsing markup menjadi struktur mirip DOM yang dapat kita kueri.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Load the original HTML file
        Document document = new Document("YOUR_DIRECTORY/article.html");
```

**Mengapa ini penting:** Memuat dokumen memberi kita model objek yang bersih, sehingga kita dapat memanipulasi node teks dengan aman tanpa khawatir merusak tag atau atribut. Ini juga menormalkan spasi putih, yang membuat langkah **search text in html** berikutnya lebih dapat diandalkan.

## Langkah 2 – Cari Teks dalam HTML untuk Kata Target

Setelah dokumen siap, kita akan mencari setiap kemunculan kata yang ingin ditekankan. Metode `searchText` mengembalikan daftar objek `TextMatch`, masing‑masing menggambarkan lokasi kecocokan dalam DOM.

```java
        // Define what we want to highlight
        String searchTerm = "Aspose";

        // Find all matches – this is the core of "search text in html"
        List<TextMatch> matches = document.searchText(searchTerm);
```

**Tips profesional:** Pencarian bersifat case‑sensitive secara default. Jika Anda memerlukan pencarian case‑insensitive, ubah teks dokumen dan `searchTerm` ke huruf yang sama sebelum memanggil `searchText`, atau gunakan pendekatan berbasis regular‑expression yang disediakan perpustakaan.

## Langkah 3 – Ganti Teks dengan `<mark>` (Sorot Kata dalam HTML)

Untuk setiap kecocokan kita akan membangun kembali teks node yang memuatnya, menyisipkan elemen `<mark>` di sekitar kata yang tepat. Ini memastikan hanya teks target yang terpengaruh dan sisanya tetap tidak berubah.

```java
        // Iterate over each match and wrap it with <mark>
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();

            // Preserve text before and after the match
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;

            // Replace the node's content with the new fragment
            parentNode.setTextContent(highlightedFragment);
        }
```

**Penjelasan:**  
- `getStartOffset`/`getEndOffset` memberi kita posisi karakter tepat dari kecocokan di dalam node induknya.  
- Dengan memotong teks asli (`textBefore` dan `textAfter`) kita mempertahankan semua hal lain persis seperti semula.  
- Membungkus kecocokan dengan `<mark>` adalah cara kanonik untuk **replace text with mark** dan mendapatkan sorotan native browser tanpa CSS tambahan.

### Kasus Khusus & Tips

- **Beberapa kecocokan dalam node yang sama:** Loop memproses setiap `TextMatch` secara berurutan. Karena kita mengganti seluruh konten node setiap kali, offset selanjutnya bergeser. Aspose.HTML mengembalikan kecocokan dalam urutan dokumen, sehingga penggantian sederhana ini bekerja untuk kebanyakan kasus. Jika Anda menemukan kecocokan yang tumpang tindih, pertimbangkan mengumpulkan semua kecocokan terlebih dahulu, lalu membangun ulang node dalam satu kali proses.  
- **Elemen yang tidak dapat berisi HTML mentah:** Jika node induk adalah blok `<script>` atau `<style>`, menyisipkan `<mark>` akan merusak halaman. Anda dapat melewatkan node tersebut dengan memeriksa `parentNode.getNodeName()` sebelum melakukan penggantian.

## Langkah 4 – Simpan Dokumen yang Sudah Disorot (Sorot Kemunculan Kata)

Setelah semua penggantian selesai, kami menyimpan DOM yang telah dimodifikasi kembali ke disk. File output akan berisi markup asli ditambah tag `<mark>` baru, secara efektif **menyorot kemunculan kata** “Aspose”.

```java
        // Write the modified HTML back to a new file
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

Buka `highlighted.html` di browser apa pun, dan Anda akan melihat setiap “Aspose” dibungkus dengan latar belakang kuning‑keabu-abuan (gaya default untuk `<mark>`). Jika Anda menginginkan tampilan khusus, tambahkan aturan CSS kecil berikut:

```html
<style>
    mark { background-color: #fffa8b; color: #000; }
</style>
```

## Pertanyaan Umum (Search Text in HTML – FAQ)

**T: Bagaimana jika kata muncul di dalam nilai atribut?**  
J: `searchText` hanya mencari pada konten teks node, bukan string atribut. Untuk menyorot nilai atribut, Anda harus mengiterasi elemen dan memeriksa atribut secara manual.

**T: Bisakah saya menyorot beberapa kata berbeda sekaligus?**  
J: Tentu saja. Buat daftar istilah, loop melalui masing‑masing, dan jalankan logika penggantian yang sama. Hati‑hati dengan kecocokan yang tumpang tindih.

**T: Apakah ini bekerja dengan tag HTML5‑only seperti `<section>` atau `<article>`?**  
J: Ya. Aspose.HTML sepenuhnya mendukung elemen HTML5 modern, sehingga traversing DOM berfungsi terlepas dari tipe tag.

## Contoh Lengkap yang Berfungsi (Semua Langkah Digabung)

Berikut adalah program Java lengkap yang siap dijalankan, memperlihatkan seluruh alur kerja—dari memuat file hingga menyimpan output yang sudah disorot.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document
        Document document = new Document("YOUR_DIRECTORY/article.html");

        // Step 2: Search for the word "Aspose"
        String searchTerm = "Aspose";
        List<TextMatch> matches = document.searchText(searchTerm);

        // Step 3: Wrap each found occurrence with a <mark> element
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted HTML fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;
            parentNode.setTextContent(highlightedFragment);
        }

        // Step 4: Save the highlighted document
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

**Output yang diharapkan:** Buka `highlighted.html` dan Anda akan melihat setiap kemunculan “Aspose” disorot. Tidak ada bagian lain dari halaman yang berubah, dan file tetap menjadi dokumen HTML yang valid.

## Kesimpulan

Kami telah membahas **cara menyorot HTML** dengan cara programatis **mencari teks dalam HTML**, membungkus setiap kecocokan dengan tag `<mark>`, dan akhirnya menyimpan perubahan. Pendekatan ini memungkinkan Anda **menyorot kata dalam HTML**, **menyorot kemunculan kata**, dan **mengganti teks dengan mark** tanpa menulis kode manipulasi string yang rapuh.

Langkah selanjutnya? Coba kembangkan skrip dengan:

- Menerima istilah pencarian sebagai argumen baris perintah.  
- Menghasilkan file CSS yang mendefinisikan warna sorotan khusus.  
- Memproses seluruh folder file HTML dalam satu batch.  

Variasi tersebut akan memperdalam pemahaman Anda tentang API Aspose.HTML serta pola pemrosesan teks secara umum.  

Jika Anda mengalami kendala atau memiliki ide untuk perbaikan lebih lanjut, tinggalkan komentar di bawah. Selamat menyorot!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}