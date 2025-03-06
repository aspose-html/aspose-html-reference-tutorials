---
title: Tambahkan CSS Sebaris ke Dokumen HTML di Aspose.HTML untuk Java
linktitle: Tambahkan CSS Sebaris ke Dokumen HTML di Aspose.HTML untuk Java
second_title: Pemrosesan HTML Java dengan Aspose.HTML
description: Pelajari cara menambahkan CSS sebaris ke dokumen HTML menggunakan Aspose.HTML untuk Java. Panduan langkah demi langkah ini membantu Anda menata HTML dan mengonversinya ke PDF dengan mudah.
weight: 14
url: /id/java/editing-html-documents/add-inline-css-html-documents/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan CSS Sebaris ke Dokumen HTML di Aspose.HTML untuk Java

## Perkenalan
Jika Anda berurusan dengan dokumen HTML dan ingin membumbui konten dengan beberapa CSS sebaris, Anda berada di tempat yang tepat! Aspose.HTML untuk Java menawarkan cara yang hebat untuk memanipulasi file HTML, memungkinkan Anda untuk menambahkan gaya, membuat desain responsif, dan banyak lagi. Apakah Anda seorang pengembang yang ingin mengotomatiskan pembuatan dokumen atau hanya tertarik pada cara memberi gaya dinamis pada konten HTML menggunakan Java, panduan ini akan memandu Anda melalui proses tersebut langkah demi langkah.
## Prasyarat
Sebelum kita masuk ke tutorialnya, mari pastikan Anda memiliki semua yang dibutuhkan:
1.  Aspose.HTML untuk Java: Anda harus menginstal Aspose.HTML untuk Java di lingkungan pengembangan Anda. Jika Anda belum menginstalnya, Anda dapat mengunduhnya dari[Halaman Unduh Aspose.HTML untuk Java](https://releases.aspose.com/html/java/).
2. Java Development Kit (JDK): Pastikan Anda telah menginstal JDK 8 atau yang lebih baru. Jika belum, Anda dapat mengunduhnya dari situs web Oracle.
3. Lingkungan Pengembangan Terpadu (IDE): Anda dapat menggunakan IDE pilihan Anda, seperti IntelliJ IDEA, Eclipse, atau NetBeans.
4.  Lisensi Aspose.HTML: Meskipun Anda dapat mencoba Aspose.HTML untuk Java dengan uji coba gratis, disarankan untuk mendapatkan lisensi Aspose.HTML untuk Java dengan uji coba gratis.[lisensi sementara](https://purchase.aspose.com/temporary-license/) atau membeli lisensi penuh untuk fungsionalitas penuh.

## Paket Impor
Untuk mulai menggunakan Aspose.HTML untuk Java, Anda perlu mengimpor paket yang diperlukan ke dalam kelas Java Anda. Berikut cara menyiapkan impor Anda:
```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.HTMLElement;
```
Impor ini menyertakan kelas-kelas yang dibutuhkan untuk membuat dokumen HTML, memanipulasi elemen, dan menyajikan output sebagai PDF.
## Langkah 1: Buat Dokumen HTML
Langkah pertama dalam menambahkan CSS sebaris ke dokumen HTML adalah membuat dokumen itu sendiri. Dokumen ini akan menjadi kanvas Anda, dan bisa sesederhana atau serumit yang Anda inginkan. Untuk tutorial ini, kita akan mulai dengan elemen paragraf dasar.
```java
String content = "<p>Inline CSS Example</p>";
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(content, ".");
```
 Pada langkah ini, Anda membuat`HTMLDocument` objek dari string yang berisi konten HTML Anda. Argumen kedua`"."` menunjukkan URL dasar, yang dalam kasus ini, adalah direktori saat ini.
## Langkah 2: Temukan Elemen Paragraf
 Sekarang dokumen Anda sudah disiapkan, langkah selanjutnya adalah menemukan elemen HTML yang ingin Anda beri gaya. Dalam kasus ini, kita fokus pada`<p>` elemen.
```java
com.aspose.html.HTMLElement paragraph = (com.aspose.html.HTMLElement) document.getElementsByTagName("p").get_Item(0);
```
 Di sini, Anda mengakses yang pertama`<p>` elemen dalam dokumen menggunakan`getElementsByTagName` Metode ini mengembalikan daftar elemen, dan`get_Item(0)` mengambil yang pertama dalam daftar.
## Langkah 3: Terapkan CSS Sebaris
Setelah elemen paragraf di tangan, saatnya menambahkan beberapa gaya. CSS sebaris sangat cocok untuk perubahan kecil dan spesifik langsung di dalam elemen HTML.
```java
paragraph.setAttribute("style", "font-size: 250%; font-family: verdana; color: #cd66aa");
```
 Pada langkah ini,`setAttribute`metode ini digunakan untuk menambahkan`style` atribut ke elemen paragraf. Gaya CSS ditulis sebagai string, yang mengatur ukuran font, jenis font, dan warna teks.
## Langkah 4: Simpan Dokumen HTML
 Setelah menerapkan gaya, Anda mungkin ingin menyimpan dokumen HTML yang dimodifikasi. Ini dapat dilakukan dengan mudah dengan`save` metode yang disediakan oleh Aspose.HTML untuk Java.
```java
document.save("edit-inline-css.html");
```
 Di sini, Anda menyimpan dokumen HTML dengan CSS sebaris ke file bernama`edit-inline-css.html` di direktori saat ini. Ini memungkinkan Anda untuk melihat konten HTML yang diberi gaya di browser.
## Langkah 5: Render Dokumen HTML sebagai PDF
Terakhir, jika Anda ingin mengonversi dokumen HTML bergaya Anda menjadi PDF, Aspose.HTML untuk Java telah menyediakannya untuk Anda. Ini sangat berguna jika Anda memerlukan versi dokumen yang siap cetak.
```java
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice("edit-inline-css.pdf");
document.renderTo(device);
```
 Pada langkah terakhir ini, Anda membuat`PdfDevice` misalnya, menentukan nama file keluaran sebagai`edit-inline-css.pdf`Kemudian, Anda merender dokumen HTML ke perangkat PDF ini, yang secara efektif mengubah HTML Anda menjadi berkas PDF.

## Kesimpulan
Selesai! Anda baru saja mempelajari cara menambahkan CSS sebaris ke dokumen HTML menggunakan Aspose.HTML untuk Java. Pustaka canggih ini memudahkan Anda memanipulasi konten HTML dan mengekspornya ke berbagai format, termasuk PDF. Baik Anda mengotomatiskan pembuatan dokumen atau mengerjakan proyek berbasis web, alat ini menawarkan fleksibilitas dan kekuatan yang Anda butuhkan.
## Pertanyaan yang Sering Diajukan
### Bisakah saya menerapkan beberapa gaya menggunakan CSS sebaris?
 Ya, Anda dapat menerapkan beberapa gaya dengan memisahkan setiap properti CSS dengan titik koma di dalam`setAttribute` metode.
### Apakah Aspose.HTML untuk Java kompatibel dengan semua versi Java?
Aspose.HTML untuk Java kompatibel dengan JDK 8 dan di atasnya.
### Dapatkah saya menggunakan Aspose.HTML untuk Java untuk mengedit berkas HTML yang ada?
Ya, Anda dapat memuat berkas HTML yang ada, memanipulasinya, dan menyimpan perubahan kembali ke sistem berkas.
### Format apa lagi yang dapat dikonversi ke HTML oleh Aspose.HTML untuk Java?
Aspose.HTML untuk Java dapat mengonversi HTML ke berbagai format, termasuk PDF, XPS, dan gambar.
### Apakah saya memerlukan koneksi internet untuk menggunakan Aspose.HTML untuk Java?
Tidak, Aspose.HTML untuk Java bekerja secara offline, meskipun koneksi internet diperlukan untuk mengunduh pustaka atau mengakses dokumentasi online.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
