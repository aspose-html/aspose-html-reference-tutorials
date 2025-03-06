---
title: Terapkan CSS Eksternal ke Dokumen HTML di Aspose.HTML untuk Java
linktitle: Terapkan CSS Eksternal ke Dokumen HTML di Aspose.HTML untuk Java
second_title: Pemrosesan HTML Java dengan Aspose.HTML
description: Temukan cara menerapkan CSS eksternal ke dokumen HTML menggunakan Aspose.HTML untuk Java! Ikuti panduan langkah demi langkah ini untuk tutorial lengkap.
weight: 12
url: /id/java/editing-html-documents/apply-external-css-html-documents/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Terapkan CSS Eksternal ke Dokumen HTML di Aspose.HTML untuk Java

## Perkenalan
Saat bekerja dengan dokumen HTML, penerapan gaya dapat membuat perbedaan besar dalam presentasi dan pengalaman pengguna. Jika Anda mendalami Java dan ingin mempelajari cara menerapkan gaya CSS eksternal ke dokumen HTML Anda menggunakan pustaka Aspose.HTML, Anda berada di tempat yang tepat! Panduan ini bertujuan untuk menjelaskan prosesnya langkah demi langkah, membuatnya mudah bahkan bagi mereka yang mungkin baru mengenal Java atau CSS.
## Prasyarat
Sebelum menyelami kode, ada beberapa hal yang perlu Anda siapkan:
### 1. Kit Pengembangan Java (JDK)
 Pastikan Anda telah menginstal JDK di komputer Anda. Anda dapat mengunduh versi terbaru dari[Situs web Java Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
### 2. Aspose.HTML untuk Java
Anda perlu menyiapkan Aspose.HTML untuk Java. Jika Anda belum melakukannya, kunjungi[Halaman unduhan Aspose](https://releases.aspose.com/html/java/) dan ambil perpustakaannya.
### 3. IDE atau Editor Teks
Pilih Lingkungan Pengembangan Terpadu (IDE) seperti IntelliJ IDEA, Eclipse, atau bahkan editor teks sederhana untuk menulis kode Java Anda.
### 4. Pengetahuan Dasar Java
Pemahaman terhadap pemrograman Java dan dasar-dasar CSS tentu akan membantu Anda mengikutinya dengan lebih nyaman.
## Paket Impor
Setelah semuanya siap, langkah selanjutnya adalah mengimpor paket yang diperlukan ke dalam proyek Java Anda. Berikut ini yang Anda perlukan:
```java
import com.aspose.html.HTMLDocument;
```
Impor ini akan memungkinkan Anda memanipulasi dokumen HTML dan menyajikannya ke dalam format lain, seperti PDF.

Kami akan membagi tutorial ini menjadi beberapa langkah yang mudah dipahami. Setiap langkah akan memandu Anda melalui proses penerapan gaya CSS eksternal ke dokumen HTML menggunakan Aspose.HTML untuk Java.
## Langkah 1: Buat Dokumen HTML
Pertama-tama, kita perlu membuat dokumen HTML. Kita akan mulai dengan mendefinisikan konten dengan struktur HTML sederhana.
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

 Di sini, kami mendefinisikan struktur HTML dasar, termasuk`<div>` dengan dua paragraf.`HTMLDocument` Kelas digunakan untuk membuat representasi dokumen dari konten HTML kita.
## Langkah 2: Buat Elemen Gaya
 Selanjutnya kita akan membuat`style` elemen untuk menampung aturan CSS kita.
```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

 Menggunakan`createElement` metode`HTMLDocument` , kita membuat yang baru`<style>` elemen dan mengatur kontennya agar menyertakan definisi CSS kita untuk dua kelas:`frame1` Dan`frame2`Kelas-kelas ini menentukan margin, padding, dimensi, warna latar belakang, jenis font, dan warna teks.
## Langkah 3: Tambahkan Gaya ke Header Dokumen
Sekarang setelah CSS kita siap, kita perlu menambahkan elemen gaya ke kepala dokumen.
```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

 Kami mengambil kepala dokumen dan menambahkan yang baru kami buat`style` elemen. Tindakan ini secara efektif mengintegrasikan CSS kita ke dalam dokumen HTML, yang memungkinkannya untuk memberi gaya pada konten HTML kita.
## Langkah 4: Terapkan Kelas ke Elemen HTML
Berikutnya, kita akan menerapkan kelas CSS yang telah didefinisikan sebelumnya ke elemen paragraf kita.
```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

Di sini, kita mengakses elemen paragraf pertama dan terakhir dalam dokumen dan menetapkan kelas CSS yang kita buat. Penetapan ini memastikan bahwa elemen tersebut mematuhi gaya yang ditetapkan dalam CSS kita.
## Langkah 5: Tetapkan Properti Gaya Tambahan
Untuk lebih meningkatkan tampilan, kita akan menetapkan properti gaya tambahan untuk paragraf kita.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

Pada langkah ini, kami menyempurnakan gaya kami. Ukuran fon paragraf pertama diperbesar dan dipusatkan, sementara warna, ukuran fon, dan jenis fon paragraf terakhir ditetapkan. Penyempurnaan ini penting untuk keterbacaan dan daya tarik estetika.
## Langkah 6: Simpan Dokumen HTML
Setelah gaya kita diterapkan, waktunya menyimpan dokumen HTML.
```java
document.save("edit-internal-css.html");
```

 Di sini, kami memanfaatkan`save` metode dari`HTMLDocument` kelas untuk menuliskan konten HTML yang dimodifikasi ke dalam sebuah berkas, sehingga mempertahankan gaya dan perubahan kita.
## Langkah 7: Render Dokumen ke PDF
Terakhir, mari kita ubah dokumen tersebut ke format PDF untuk keluaran.
```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

 Menggunakan`PdfDevice` kelas, kami menyiapkan rendering dokumen HTML kami menjadi PDF. Langkah ini penting jika Anda ingin membagikan dokumen bergaya dalam format yang dapat diakses secara universal.
## Kesimpulan
Nah, itu dia—menerapkan CSS eksternal ke dokumen HTML menggunakan Aspose.HTML untuk Java mudah dan bermanfaat! Hanya dengan beberapa baris kode, Anda dapat mengubah teks biasa menjadi dokumen yang menarik secara visual dan bergaya profesional. Jadi, baik Anda mendesain untuk penggunaan pribadi, membuat laporan, atau mengembangkan konten web, memahami cara memanipulasi HTML dan CSS di Java adalah keterampilan hebat yang harus dimiliki dalam perangkat Anda.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.HTML untuk Java?
Aspose.HTML untuk Java adalah pustaka hebat yang memungkinkan pengembang bekerja dengan dokumen HTML dalam aplikasi Java, menyediakan berbagai fitur, mulai dari manipulasi HTML hingga rendering.
### Apakah saya memerlukan koneksi internet untuk menggunakan Aspose.HTML?
Tidak, setelah Anda mengunduh file pustaka yang diperlukan, Anda dapat menggunakan Aspose.HTML secara offline.
### Bisakah saya menerapkan beberapa berkas CSS ke dokumen HTML?
 Ya, Anda dapat membuat beberapa`<link>` elemen dan menambahkannya ke kepala dokumen untuk berbagai file CSS.
### Apakah ada perbedaan antara CSS internal dan eksternal?
Ya! CSS internal didefinisikan dalam dokumen HTML, sedangkan CSS eksternal ditempatkan dalam berkas terpisah dan ditautkan ke dokumen.
### Bagaimana saya bisa mendapatkan dukungan untuk Aspose.HTML untuk Java?
 Anda dapat mengakses dukungan komunitas melalui[Forum Aspose](https://forum.aspose.com/c/html/29) untuk pertanyaan atau masalah apa pun yang mungkin Anda temui.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
