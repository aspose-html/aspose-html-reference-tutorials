---
category: general
date: 2026-03-25
description: Cara menggunakan sandbox untuk menangkap screenshot halaman web dengan
  Aspose.HTML untuk Java. Pelajari cara menyimpan HTML sebagai PNG, konversi HTML
  ke gambar, dan konversi HTML ke PNG dalam hitungan menit.
draft: false
keywords:
- how to use sandbox
- capture webpage screenshot
- save html as png
- html to image conversion
- html to png conversion
language: id
og_description: Cara menggunakan sandbox untuk menangkap tangkapan layar halaman web.
  Tutorial ini menunjukkan cara menyimpan HTML sebagai PNG, mencakup konversi HTML
  ke gambar dan konversi HTML ke PNG dengan Aspose.HTML untuk Java.
og_title: Cara Menggunakan Sandbox untuk Mengambil Tangkapan Layar Halaman Web
tags:
- Aspose.HTML
- Java
- Web Automation
title: Cara Menggunakan Sandbox untuk Mengambil Tangkapan Layar Halaman Web
url: /id/java/conversion-html-to-various-image-formats/how-to-use-sandbox-to-capture-webpage-screenshot/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Sandbox untuk Mengambil Tangkapan Layar Halaman Web

Cara menggunakan sandbox untuk mengambil tangkapan layar halaman web adalah kebutuhan yang sering muncul ketika Anda memerlukan pratinjau pixel‑perfect dari sebuah halaman responsif. Dalam panduan ini kami juga akan menunjukkan cara **menyimpan HTML sebagai PNG** menggunakan Aspose.HTML for Java, mencakup semua hal mulai dari *html to image conversion* hingga *html to png conversion* dalam satu contoh yang dapat direproduksi.

Bayangkan Anda sedang menguji halaman landing page pemasaran yang tampil berbeda di ponsel, tablet, dan desktop. Daripada membuka tiga browser, Anda dapat memulai sandbox, mengarahkannya ke URL, dan langsung mendapatkan PNG yang persis mencerminkan apa yang akan dirender perangkat nyata. Pada akhir tutorial ini Anda akan memiliki program Java lengkap yang dapat dijalankan dan melakukan hal tersebut, serta beberapa tips praktis yang dapat Anda gunakan kembali dalam proyek Anda.

## Apa yang Anda Butuhkan

- **Aspose.HTML for Java** (v23.9 atau lebih baru). Perpustakaan ini tersedia melalui Maven Central, sehingga menambahkan dependensinya sangat mudah.  
- **JDK 11+** terpasang di mesin Anda.  
- IDE atau editor teks pilihan Anda (IntelliJ IDEA, VS Code, Eclipse… semuanya dapat).  
- Akses internet untuk URL contoh (`https://example.com/responsive.html`) atau ganti dengan halaman apa pun yang ingin Anda snapshot.

Tidak ada binari native tambahan atau browser headless yang diperlukan—sandbox berjalan sepenuhnya di memori.

---

## Cara Menggunakan Sandbox – Langkah 1: Tentukan Perangkat Virtual

Hal pertama yang Anda lakukan adalah memberi tahu sandbox ukuran layar yang ingin Anda tiru. Di sinilah kata kunci utama bersinar: *cara menggunakan sandbox* untuk viewport tertentu.

```java
// Step 1: Create a DeviceInfo that describes the virtual screen
DeviceInfo sandboxDevice = new DeviceInfo();
sandboxDevice.setWidth(800);               // width in pixels
sandboxDevice.setHeight(600);              // height in pixels
sandboxDevice.setDevicePixelRatio(1.0);    // 1 × for standard displays
sandboxDevice.setUserAgent("AsposeHTML/Java Sandbox");
```

**Mengapa ini penting:**  
Menetapkan lebar dan tinggi memaksa mesin tata letak memperlakukan halaman seolah‑olah ditampilkan pada monitor 800×600. `devicePixelRatio` memengaruhi cara media query berbasis CSS (`@media (min‑device‑pixel‑ratio: ...)`) berperilaku, memastikan tangkapan layar cocok dengan pengalaman dunia nyata.

> **Tip pro:** Jika Anda memerlukan tangkapan layar ber‑DPI tinggi (misalnya tampilan Retina), naikkan `devicePixelRatio` menjadi `2.0` dan sesuaikan lebar/tinggi secara proporsional.

---

## Tangkap Tangkapan Layar Halaman Web – Langkah 2: Muat Halaman di Dalam Sandbox

Sekarang kami meminta Aspose.HTML untuk mengambil HTML remote dan merendernya di dalam sandbox yang baru saja kami definisikan. Langkah ini adalah inti dari **capture webpage screenshot**.

```java
// Step 2: Load the remote HTML page using the sandboxed environment
HTMLDocument document = new HTMLDocument(
        "https://example.com/responsive.html",
        new HTMLDocumentLoadOptions(new Sandbox(sandboxDevice)));
```

**Apa yang terjadi di balik layar?**  
`HTMLDocumentLoadOptions` menerima instance `Sandbox` yang berisi `DeviceInfo` kami. Perpustakaan kemudian membuat konteks rendering headless yang menghormati viewport, string user‑agent, dan setiap JavaScript yang mungkin dijalankan halaman—*semua tanpa meluncurkan Chrome atau Firefox*.

Jika halaman target memerlukan autentikasi, Anda dapat menyuntikkan cookie atau header khusus melalui `HTMLDocumentLoadOptions` juga. Itu merupakan kasus tepi yang berguna ketika Anda berurusan dengan portal intranet.

---

## Simpan HTML sebagai PNG – Langkah 3: Konversi Dokumen yang Dirender menjadi Gambar

Setelah halaman dirender, bagian terakhir adalah **save HTML as PNG**. Ini adalah langkah *html to png conversion* yang sebenarnya.

```java
// Step 3: Convert the rendered document to PNG and write it to disk
try (FileOutputStream out = new FileOutputStream("output/responsive_page.png")) {
    Converter.convertDocument(
            document,
            new ConversionOptions(ConversionFormat.PNG),
            out);
}
```

Ketika `Converter` selesai, Anda akan menemukan file bernama `responsive_page.png` di dalam folder `output`. Buka file tersebut, dan Anda akan melihat persis seperti apa tampilan halaman pada 800×600 piksel—tanpa UI browser, tanpa scrollbar, hanya render murni.

**Jebakan umum:**  
- **Kesalahan izin file:** Pastikan direktori ada (`output/` pada contoh) dan proses Anda dapat menulis ke sana.  
- **Halaman besar:** Halaman yang sangat tinggi dapat menghasilkan file PNG yang sangat besar; Anda dapat membatasi tinggi pada `DeviceInfo` atau memotong setelah konversi.  
- **Konten dinamis:** Jika halaman memuat data via AJAX setelah pemuatan awal, Anda mungkin perlu menambahkan jeda singkat (`Thread.sleep(2000)`) sebelum konversi, atau gunakan `HTMLDocumentLoadOptions.setWaitForResources(true)`.

---

### html to image conversion – Opsi Lanjutan

Aspose.HTML menawarkan beberapa pengaturan yang dapat Anda sesuaikan untuk menyempurnakan **html to image conversion**:

| Opsi | Deskripsi | Kapan digunakan |
|------|-----------|-----------------|
| `ConversionOptions.setQuality(int)` | Menetapkan tingkat kompresi PNG (0‑100). | Mengurangi ukuran file untuk aset web. |
| `ConversionOptions.setBackgroundColor(Color)` | Memaksa warna latar belakang (default transparan). | Berguna ketika halaman memiliki bagian transparan. |
| `ConversionOptions.setPageSize(PageSize)` | Menimpa ukuran sandbox untuk gambar output. | Membuat thumbnail dengan resolusi berbeda. |

Berikut contoh singkat yang menetapkan latar belakang putih dan kualitas 90 %:

```java
ConversionOptions pngOptions = new ConversionOptions(ConversionFormat.PNG);
pngOptions.setBackgroundColor(java.awt.Color.WHITE);
pngOptions.setQuality(90);

try (FileOutputStream out = new FileOutputStream("output/white_bg_page.png")) {
    Converter.convertDocument(document, pngOptions, out);
}
```

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang dapat Anda salin‑tempel ke file `SandboxResponsiveExample.java` dan jalankan:

```java
import com.aspose.html.devices.DeviceInfo;
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.ConversionOptions;
import com.aspose.html.converters.ConversionFormat;
import com.aspose.html.render.HTMLDocument;
import com.aspose.html.render.HTMLDocumentLoadOptions;
import com.aspose.html.render.Sandbox;

import java.io.FileOutputStream;

public class SandboxResponsiveExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Define a sandbox with the desired viewport (800×600) and device pixel ratio
        DeviceInfo sandboxDevice = new DeviceInfo();
        sandboxDevice.setWidth(800);
        sandboxDevice.setHeight(600);
        sandboxDevice.setDevicePixelRatio(1.0);
        sandboxDevice.setUserAgent("AsposeHTML/Java Sandbox");

        // Step 2: Load the remote HTML page inside the sandboxed environment
        HTMLDocument document = new HTMLDocument(
                "https://example.com/responsive.html",
                new HTMLDocumentLoadOptions(new Sandbox(sandboxDevice)));

        // Step 3: Convert the document to PNG – the output reflects exactly how the page looks on the defined screen size
        try (FileOutputStream out = new FileOutputStream("output/responsive_page.png")) {
            Converter.convertDocument(
                    document,
                    new ConversionOptions(ConversionFormat.PNG),
                    out);
        }

        System.out.println("Screenshot saved to output/responsive_page.png");
    }
}
```

Menjalankan program akan mencetak baris konfirmasi dan menaruh PNG ke dalam folder `output`. Buka file tersebut, dan Anda akan melihat representasi yang setia dari halaman remote pada ukuran tepat yang Anda tentukan.

---

## Pertanyaan yang Sering Diajukan

**T: Apakah ini bekerja dengan file HTML lokal?**  
J: Tentu saja. Ganti URL dengan URI `file://` atau berikan path `java.io.File` ke konstruktor `HTMLDocument`.

**T: Bagaimana jika saya membutuhkan PDF alih‑alih PNG?**  
J: Ganti `ConversionFormat.PNG` dengan `ConversionFormat.PDF`. Sisanya tetap sama.

**T: Bisakah saya mengambil tangkapan layar halaman penuh (scrolling)?**  
J: Tetapkan tinggi `DeviceInfo` ke tinggi scroll halaman (`document.getDocumentElement().getScrollHeight()`) sebelum konversi, atau gunakan `ConversionOptions.setPageSize` untuk memperbesar kanvas.

---

## Kesimpulan

Anda kini tahu **cara menggunakan sandbox** untuk mengambil tangkapan layar halaman web, menyimpan HTML sebagai PNG, dan melakukan konversi html ke gambar yang dapat diandalkan dengan Aspose.HTML for Java. Pendekatan ini ringan, sepenuhnya dapat diprogram, dan menghindari beban overhead browser headless tradisional.

Apa selanjutnya? Coba ganti output PNG dengan PDF, bereksperimen dengan rasio piksel perangkat yang berbeda untuk meniru tampilan Retina, atau otomatisasi pemrosesan batch puluhan URL. Teknik sandbox yang sama juga dapat dipakai kembali untuk **html to png conversion** dalam pipeline CI, pengujian regresi visual, atau menghasilkan thumbnail untuk sistem manajemen konten.

Silakan tinggalkan komentar jika Anda mengalami kendala, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}