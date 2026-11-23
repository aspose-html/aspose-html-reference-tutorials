---
category: general
date: 2026-06-16
description: Pelajari cara mengatur DPI perangkat Aspose dan mengatur lebar serta
  tinggi viewport saat merender HTML dengan sandbox Aspose.HTML di Java. Kode langkah
  demi langkah disertakan.
draft: false
keywords:
- set device dpi aspose
- set viewport width height
language: id
og_description: Temukan cara mengatur DPI perangkat Aspose dan mengatur lebar serta
  tinggi viewport menggunakan Aspose.HTML sandbox untuk Java. Kode lengkap dan penjelasan.
og_title: atur DPI perangkat Aspose di Java – Panduan Sandbox Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to set device dpi aspose and set viewport width height when
    rendering HTML with Aspose.HTML sandbox in Java. Step‑by‑step code included.
  headline: set device dpi aspose in Java – Complete Sandbox Guide
  type: TechArticle
- description: Learn how to set device dpi aspose and set viewport width height when
    rendering HTML with Aspose.HTML sandbox in Java. Step‑by‑step code included.
  name: set device dpi aspose in Java – Complete Sandbox Guide
  steps:
  - name: Configure sandbox options (including DPI and viewport size).
    text: Configure sandbox options (including DPI and viewport size).
  - name: Instantiate a `DocumentSandbox` with those options.
    text: Instantiate a `DocumentSandbox` with those options.
  - name: Load an external HTML page inside the sandbox.
    text: Load an external HTML page inside the sandbox.
  - name: Perform a simple DOM operation—printing the page title.
    text: Perform a simple DOM operation—printing the page title.
  type: HowTo
tags:
- Aspose.HTML
- Java
- HTML rendering
- Sandbox
title: Mengatur DPI Perangkat Aspose di Java – Panduan Lengkap Sandbox
url: /id/java/advanced-usage/set-device-dpi-aspose-in-java-complete-sandbox-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# set device dpi aspose – Tutorial Sandbox Java

Pernah bertanya-tanya bagaimana cara **set device dpi aspose** saat merender halaman web di Java? Anda bukan satu-satunya. Banyak pengembang mengalami kebuntuan ketika mereka membutuhkan halaman yang dirender terlihat persis seperti di layar nyata—terutama ketika DPI penting untuk perhitungan tata letak.  

Dalam panduan ini kami akan membimbing Anda melalui contoh praktis yang tidak hanya **set device dpi aspose**, tetapi juga menunjukkan cara **set viewport width height** sehingga halaman berperilaku persis seperti di jendela browser berukuran 1280 × 800 piksel. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat dijalankan, penjelasan jelas setiap langkah, serta tips untuk menghindari jebakan umum.

## Apa yang Dibahas dalam Tutorial Ini

Kami akan memulai dengan merinci prasyarat, kemudian menyelami empat langkah singkat:

1. Mengonfigurasi opsi sandbox (termasuk DPI dan ukuran viewport).  
2. Membuat instance `DocumentSandbox` dengan opsi tersebut.  
3. Memuat halaman HTML eksternal di dalam sandbox.  
4. Melakukan operasi DOM sederhana—mencetak judul halaman.

Anda akan melihat mengapa setiap bagian penting, cara menyesuaikan pengaturan untuk perangkat berbeda, dan seperti apa output yang diharapkan. Tidak perlu dokumentasi eksternal; semua yang Anda butuhkan ada di sini.

## Prasyarat

- Java 8 atau lebih baru (perpustakaan Aspose.HTML untuk Java mendukung JDK 8+).  
- JAR Aspose.HTML untuk Java sudah ditambahkan ke classpath proyek Anda.  
- IDE atau alat build (Maven/Gradle) untuk mengompilasi dan menjalankan kode.  
- Akses internet jika Anda berencana memuat URL langsung seperti `https://example.com`.

Jika semua poin di atas sudah terpenuhi, mari kita mulai.

## Langkah 1: Set device DPI aspose – Definisikan Opsi Sandbox

Hal pertama yang harus Anda lakukan adalah memberi tahu sandbox “layar” apa yang Anda tirukan. Di sinilah **set device dpi aspose** berperan. DPI (dots per inch) memengaruhi cara unit CSS `px` diinterpretasikan, yang dapat mengubah ukuran font, skala gambar, dan media query.

```java
// Step 1: Create sandbox options and configure DPI and viewport.
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setDeviceDpi(96);               // set device dpi aspose
sandboxOptions.setViewportWidth(1280);         // set viewport width height
sandboxOptions.setViewportHeight(800);         // set viewport width height
```

> **Mengapa ini penting:**  
> *Pemanggilan `setDeviceDpi` memberi tahu Aspose.HTML untuk memperlakukan satu piksel CSS sebagai 1/96 inci, meniru kebanyakan monitor desktop. Jika Anda melewatkannya, tata letak dapat terlihat terlalu kecil atau terlalu besar pada layar ber‑DPI tinggi.*

## Langkah 2: Buat Sandbox dengan Opsi yang Telah Dikonfigurasi

Setelah opsi siap, Anda memerlukan instance sandbox yang menghormatinya. Anggap sandbox sebagai mesin peramban kecil yang terisolasi dan tidak menyentuh sistem file Anda.

```java
// Step 2: Initialise the DocumentSandbox using the options above.
DocumentSandbox documentSandbox = new DocumentSandbox(sandboxOptions);
```

> **Tips profesional:**  
> Menggunakan kembali `DocumentSandbox` yang sama untuk beberapa halaman menghemat memori, tetapi ingat untuk mereset opsi jika Anda memerlukan DPI atau viewport yang berbeda di kemudian hari.

## Langkah 3: Muat Dokumen HTML di Dalam Sandbox

Dengan sandbox siap, memuat halaman menjadi sangat mudah. Konstruktor `HTMLDocument` menerima URL dan sandbox yang baru saja Anda buat.

```java
// Step 3: Load a remote HTML page using the sandbox.
HTMLDocument htmlDoc = new HTMLDocument("https://example.com", documentSandbox);
```

> **Kasus tepi:**  
> Jika situs target memblokir permintaan otomatis, Anda mungkin mendapatkan error 403. Dalam hal ini, unduh HTML secara lokal dan muat dari jalur file, atau atur string user‑agent khusus melalui `sandboxOptions`.

## Langkah 4: Lakukan Operasi DOM Normal – Cetak Judul Halaman

Pada titik ini halaman sudah sepenuhnya dirender di dalam sandbox, sehingga setiap kueri DOM berfungsi persis seperti di peramban lengkap. Mari kita buat sederhana dan ambil judulnya.

```java
// Step 4: Access the DOM – print the page title.
System.out.println("Title: " + htmlDoc.getTitle());
```

**Output yang diharapkan**

```
Title: Example Domain
```

Jika Anda melihat sesuatu yang berbeda, periksa kembali apakah URL dapat dijangkau dan apakah Anda tidak sengaja mengubah nilai DPI atau viewport.

## Mengapa Menetapkan Viewport Width Height Sangat Penting

Anda mungkin bertanya, “Mengapa kita **set viewport width height**?” Jawabannya terletak pada desain responsif. Media query seperti `@media (max-width: 600px)` bereaksi terhadap dimensi viewport, bukan ukuran layar fisik. Dengan menentukan `1280` × `800`, Anda menjamin halaman merender tata letak “desktop”, bahkan jika kode dijalankan di server headless tanpa tampilan.

```java
sandboxOptions.setViewportWidth(1280);   // set viewport width height
sandboxOptions.setViewportHeight(800);   // set viewport width height
```

Mengubah angka‑angka tersebut memungkinkan Anda mensimulasikan tablet, ponsel, atau bahkan monitor ultra‑wide tanpa meninggalkan IDE.

## Contoh Lengkap yang Siap Dijalan

Berikut adalah kelas Java lengkap yang siap dijalankan dan menggabungkan semua langkah. Salin‑tempel ke file bernama `SandboxExample.java`, tambahkan JAR Aspose.HTML ke classpath, lalu jalankan `javac SandboxExample.java && java SandboxExample`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.sandbox.SandboxOptions;

public class SandboxExample {
    public static void main(String[] args) {
        // Step 1: Define sandbox options – set device DPI and viewport.
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setDeviceDpi(96);               // set device dpi aspose
        sandboxOptions.setViewportWidth(1280);         // set viewport width height
        sandboxOptions.setViewportHeight(800);         // set viewport width height

        // Step 2: Create a DocumentSandbox using the defined options.
        DocumentSandbox documentSandbox = new DocumentSandbox(sandboxOptions);

        // Step 3: Load an HTML document inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com", documentSandbox);

        // Step 4: Perform normal DOM operations – print the page title.
        System.out.println("Title: " + htmlDoc.getTitle());
    }
}
```

> **Verifikasi cepat:**  
> Jalankan program. Jika Anda melihat `Title: Example Domain`, semuanya telah terhubung dengan benar. Jika tidak, periksa konsol untuk pengecualian—kebanyakan masalah berasal dari JAR yang hilang atau pembatasan jaringan.

## Kesalahan Umum & Cara Menghindarinya

| Gejala | Penyebab Kemungkinan | Solusi |
|---|---|---|
| `NullPointerException` pada `htmlDoc.getTitle()` | Sandbox gagal memuat halaman | Verifikasi URL, tambahkan try‑catch di sekitar konstruktor `HTMLDocument`, atau aktifkan logging via `sandboxOptions.setLogLevel(...)`. |
| Tata letak terlihat terlalu diperbesar/kecil | DPI tidak diatur dengan benar | Pastikan `sandboxOptions.setDeviceDpi(96)` (atau DPI target Anda). |
| Media query tidak pernah terpanggil | Dimensi viewport tidak disetel | Periksa kembali bahwa Anda memanggil baik `setViewportWidth` **maupun** `setViewportHeight`. |
| Out‑of‑memory pada halaman besar | Menggunakan satu sandbox untuk banyak halaman berat | Buat `DocumentSandbox` baru per halaman atau panggil `documentSandbox.dispose()` setelah selesai. |

## Memperluas Contoh

Setelah Anda menguasai **set device dpi aspose** dan **set viewport width height**, Anda dapat bereksperimen lebih jauh:

- **Ambil screenshot** halaman yang dirender menggunakan `htmlDoc.renderToBitmap(...)`.  
- **Sisipkan CSS khusus** sebelum rendering untuk menguji tema mode gelap.  
- **Jalankan JavaScript** di dalam sandbox dengan `htmlDoc.getWindow().eval(...)`.  

Semua tindakan ini menghormati DPI dan viewport yang telah Anda konfigurasikan, memberikan lingkungan pengujian yang dapat diandalkan untuk layout responsif.

## Kesimpulan

Kami baru saja menelusuri solusi singkat end‑to‑end yang menunjukkan cara **set device dpi aspose** dan **set viewport width height** menggunakan sandbox Aspose.HTML di Java. Anda kini memiliki fondasi kuat untuk merender halaman persis seperti yang akan terlihat pada perangkat apa pun, semuanya dari lingkungan yang aman dan terisolasi.

Siap untuk langkah selanjutnya? Cobalah merender halaman yang menggunakan layout CSS grid, atau tarik stylesheet remote dan lihat bagaimana DPI memengaruhi rendering font. Sandbox memberi Anda kebebasan bereksperimen tanpa memengaruhi sistem host.

Jika Anda menemui kendala, tinggalkan komentar di bawah atau periksa dokumentasi Aspose.HTML untuk Java—meskipun semua yang Anda butuhkan sudah disajikan di sini. Selamat coding!  

![set device dpi aspose sandbox diagram](https://example.com/images/set-device-dpi-aspose.png "Diagram showing DPI and viewport configuration in Aspose.HTML sandbox")


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Create PDF from HTML using Aspose.HTML for Java – Sandbox](/html/english/java/configuring-environment/implement-sandboxing/)
- [Create PDF from HTML – Set User Style Sheet in Aspose.HTML for Java](/html/english/java/configuring-environment/set-user-style-sheet/)
- [How to Set Charset in Aspose.HTML for Java](/html/english/java/configuring-environment/set-character-set/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}