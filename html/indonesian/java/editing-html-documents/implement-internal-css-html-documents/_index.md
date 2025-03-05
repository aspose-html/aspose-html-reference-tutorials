---
title: Menerapkan CSS Internal dalam Dokumen HTML dengan Aspose.HTML untuk Java
linktitle: Menerapkan CSS Internal dalam Dokumen HTML dengan Aspose.HTML untuk Java
second_title: Pemrosesan HTML Java dengan Aspose.HTML
description: Pelajari cara menerapkan CSS internal dalam dokumen HTML menggunakan Aspose.HTML untuk Java dengan tutorial langkah demi langkah yang mudah.
type: docs
weight: 16
url: /id/java/editing-html-documents/implement-internal-css-html-documents/
---
## Perkenalan
Membuat halaman web yang indah dan terstruktur dengan baik sering kali bergantung pada satu elemen penting: gaya. Dalam pengembangan web, CSS (Cascading Style Sheets) seperti hiasan untuk HTML Anda—yang membuat semuanya tampak menarik dan teratur. Hari ini, kita akan membahas cara mengintegrasikan CSS internal dalam dokumen HTML menggunakan Aspose.HTML untuk Java. Baik Anda seorang pemula atau pengembang berpengalaman, tutorial ini akan menguraikan langkah-langkahnya dengan cara yang sederhana dan menarik.
## Prasyarat
Sebelum kita langsung memulai, mari pastikan Anda memiliki semua yang dibutuhkan untuk mengikuti tutorial ini. Berikut ini adalah prasyaratnya:
1.  Java Development Kit (JDK): Pastikan Anda telah menginstal JDK di komputer Anda. Anda dapat mengunduhnya dari[Situs web Oracle](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) atau[Bahasa pemrograman OpenJDK](https://openjdk.java.net/).
2.  Pustaka Aspose.HTML untuk Java: Anda memerlukan pustaka Aspose.HTML untuk menangani dan memanipulasi dokumen HTML dengan mudah. Anda dapat mengunduh pustaka tersebut dari[Situs web Aspose](https://releases.aspose.com/html/java/).
3. Lingkungan Pengembangan Terpadu (IDE): IDE yang bagus seperti IntelliJ IDEA atau Eclipse dapat membuat pengkodean lebih lancar.
4. Pengetahuan dasar tentang Java: Tutorial ini mengasumsikan bahwa Anda memiliki pengetahuan tentang pemrograman Java.
5. Waktu dan Kesabaran: Meskipun proses ini mudah, melakukannya selangkah demi selangkah adalah kuncinya.
## Paket Impor
Sebelum memulai pengkodean, mari impor paket yang diperlukan untuk memastikan bahwa program kita memiliki akses ke fitur yang disediakan oleh Aspose.HTML.
```java
import java.io.IOException;
```
Pastikan untuk menambahkan pernyataan impor ini di bagian atas berkas Java Anda. Ini akan memungkinkan kita untuk memanfaatkan kelas-kelas yang dibutuhkan untuk membuat dan memanipulasi dokumen HTML dan merendernya sebagai PDF.
Mari kita uraikan prosesnya ke dalam beberapa langkah terpisah agar Anda dapat mengikutinya dengan mudah.
## Langkah 1: Buat Contoh Dokumen HTML
Pertama-tama, kita perlu membuat contoh dokumen HTML. Berikut cara melakukannya:
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(content, ".");
```
 Di sini, kami mendefinisikan struktur HTML sederhana dengan dua paragraf di dalam`div` . Itu`HTMLDocument` instance menginisialisasi struktur ini, siap untuk modifikasi dan penataan.
## Langkah 2: Buat dan Tambahkan Elemen Gaya
Selanjutnya, kita akan membuat gaya CSS internal. Di sinilah keajaiban gaya dimulai!
```java
com.aspose.html.dom.Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;}" +
                      ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```
 Pada langkah ini, kita membuat sebuah`<style>` elemen dan mendefinisikan dua kelas CSS—`frame1` Dan`frame2`. Setiap kelas memiliki gaya khusus untuk margin, padding, warna latar belakang, dan properti font. Di sinilah CSS internal kita mulai terbentuk.
## Langkah 3: Tambahkan Elemen Gaya ke Header Dokumen
Sekarang setelah kita membuat gaya, kita perlu menambahkannya ke header dokumen.
```java
com.aspose.html.dom.Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```
 Potongan kode ini menemukan`head` dari dokumen dan menambahkan kami`<style>` elemen padanya. Ini menghubungkan gaya CSS kita dengan konten HTML di bawahnya.
## Langkah 4: Menetapkan Kelas CSS ke Elemen HTML
Berikutnya, mari terapkan gaya yang kita tentukan ke elemen paragraf dalam dokumen kita.
```java
com.aspose.html.HTMLElement paragraph = (com.aspose.html.HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```
 Di sini, kita mengambil elemen paragraf dan menetapkan nama kelasnya menjadi`frame1` Dan`frame2`Sekarang paragraf kita akan mewarisi gaya yang baru saja kita definisikan!
## Langkah 5: Sesuaikan Properti Gaya
Mari tingkatkan presentasi visual lebih jauh dengan menyesuaikan properti gaya paragraf kita.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```
Pada langkah ini, kami mengubah ukuran font dan perataan paragraf pertama, serta menyesuaikan warna dan font paragraf kedua. Penyesuaian ini menambah kepribadian dan kejelasan pada dokumen Anda.
## Langkah 6: Simpan Dokumen HTML
Sekarang setelah kita menyelesaikan CSS internal dan membuat perubahan, saatnya menyimpan dokumen ke dalam sebuah berkas.
```java
document.save("edit-internal-css.html");
```
 Itu`save` metode menyimpan dokumen kita ke file HTML bernama`edit-internal-css.html`Anda dapat membuka berkas ini di peramban web mana pun untuk melihat perubahan yang terjadi!
## Langkah 7: Render Dokumen HTML ke PDF
Sebagai langkah terakhir, mari kita ubah dokumen HTML yang telah diberi gaya ke dalam format PDF. Ini sangat berguna untuk berbagi atau mencetak konten yang telah diberi gaya.
```java
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```
 Di sini, kita membuat`PdfDevice` contoh yang menunjuk ke file keluaran yang kita inginkan.`renderTo` Metode ini kemudian mengubah dokumen HTML menjadi PDF. Keren, bukan?
## Kesimpulan
Nah, itu dia! Sekarang Anda tahu cara menerapkan CSS internal dalam dokumen HTML menggunakan Aspose.HTML untuk Java. Dengan mengikuti tutorial ini, Anda tidak hanya mempelajari cara menata HTML, tetapi juga cara menyimpan dan merendernya sebagai PDF. Dengan alat-alat ini, Anda dapat membuat halaman web Anda tampil menarik dengan gaya dan profesionalisme. Jadi, tunggu apa lagi? Langsung saja dan bereksperimen dengan berbagai opsi penataan!

## Pertanyaan yang Sering Diajukan
### Apa keuntungan menggunakan CSS internal?  
CSS internal memungkinkan Anda memberi gaya pada dokumen HTML tunggal tanpa memengaruhi dokumen HTML lainnya, membuatnya sempurna untuk desain yang unik.
### Bisakah Aspose.HTML menangani berkas CSS eksternal?  
Ya, Aspose.HTML dapat menangani file CSS eksternal; Anda dapat menautkannya mirip dengan gaya internal.
### Apakah Aspose.HTML sumber terbuka?  
Tidak, Aspose.HTML adalah pustaka komersial, tetapi Anda dapat memulai dengan uji coba gratis untuk menjelajahi fitur-fiturnya.
### Bagaimana saya dapat menghubungi dukungan jika saya mengalami masalah?  
 Anda dapat mengunjungi[Forum dukungan Aspose](https://forum.aspose.com/c/html/29) untuk bantuan.
### Apakah ada pertimbangan kinerja saat merender HTML ke PDF?  
Ya, dokumen HTML yang rumit mungkin memerlukan waktu lebih lama untuk ditampilkan; mengoptimalkan konten dapat meningkatkan kinerja.