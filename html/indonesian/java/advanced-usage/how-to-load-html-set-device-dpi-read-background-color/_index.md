---
category: general
date: 2026-02-16
description: Cara memuat HTML di Java, mengatur DPI perangkat, mendefinisikan ukuran
  layar virtual, dan membaca warna latar belakang yang dihitung dari elemen mana pun.
draft: false
keywords:
- how to load html
- read background color
- set device dpi
- set virtual screen size
- get computed background color
language: id
og_description: Cara memuat HTML di Java, mengatur DPI perangkat, menentukan ukuran
  layar virtual, dan membaca warna latar belakang yang dihitung dari elemen apa pun.
og_title: Cara Memuat HTML, Mengatur DPI Perangkat, dan Membaca Warna Latar Belakang
tags:
- Aspose.HTML
- Java
title: Cara Memuat HTML, Mengatur DPI Perangkat & Membaca Warna Latar Belakang
url: /id/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Memuat HTML, Mengatur DPI Perangkat & Membaca Warna Latar Belakang

Pernah bertanya-tanya **cara memuat html** dalam aplikasi Java dan kemudian memeriksa gaya halaman? Anda tidak sendirian—para pengembang sering perlu merender halaman web secara off‑screen, mengambil nilai CSS akhir, dan menggunakannya untuk konversi PDF, screenshot, atau bahkan pengujian otomatis.  

Dalam panduan ini kami akan membahas langkah demi langkah: kami akan memuat file HTML, **mengatur DPI perangkat**, menentukan **ukuran layar virtual**, dan akhirnya **membaca warna latar belakang** dari elemen `<body>`. Pada akhir tutorial Anda akan memiliki cuplikan kode yang dapat dijalankan sepenuhnya yang mencetak **warna latar belakang yang dihitung**—tidak ada misteri, hanya Java biasa.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki:

* Java 17 atau lebih baru (kode ini bekerja dengan JDK terbaru apa pun).  
* Aspose.HTML untuk Java 23.9 atau lebih baru—unduh JAR dari situs Aspose atau tambahkan melalui Maven.  
* File HTML sederhana (misalnya `responsive.html`) yang mendefinisikan warna latar belakang dalam CSS.

Itu saja—tanpa kerangka kerja tambahan, tanpa driver browser. Siap? Mari kita mulai.

![Diagram yang menggambarkan cara memuat html dan mengekstrak gaya terhitung](/images/load-html-diagram.png){alt="Diagram yang menggambarkan cara memuat html"}

## Langkah 1: Cara Memuat HTML dan Mengonfigurasi Opsi Rendering

Hal pertama yang Anda lakukan adalah membuat objek `HtmlLoadOptions`. Objek ini memberi tahu Aspose.HTML **cara memuat html**—termasuk dimensi layar virtual dan DPI yang ingin Anda tirukan.

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create load options and define the virtual screen size and DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        // setVirtualScreenSize – width × height in CSS pixels
        loadOptions.setScreenSize(new Size(1280, 800));
        // setDeviceDpi – typical desktop DPI (96 is the default for most monitors)
        loadOptions.setDeviceDpi(96);
```

**Mengapa ini penting:**  
Menetapkan ukuran layar virtual memastikan bahwa media query seperti `@media (max-width: 600px)` berperilaku seolah‑olah halaman dirender pada monitor nyata. DPI memengaruhi bagaimana satuan CSS `px` dipetakan ke piksel fisik—krusial ketika Anda kemudian menghasilkan gambar atau PDF.

## Langkah 2: Memuat File HTML Menggunakan Opsi yang Dikonfigurasi

Sekarang kita benar‑benarnya memuat file tersebut. Perhatikan bahwa kami melewatkan `loadOptions` yang sama yang baru saja kami konfigurasikan.

```java
        // 2️⃣ Load the HTML file with the options we just set.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);
```

Jika file tidak ditemukan, Aspose akan melempar `FileNotFoundException` yang jelas. Dalam produksi Anda mungkin ingin membungkusnya dalam try‑catch dan menggunakan string HTML default sebagai fallback.

## Langkah 3: Mengatur Ukuran Layar Virtual dan DPI Perangkat (Secara Eksplisit)

Meskipun kami sudah memanggil `setScreenSize` dan `setDeviceDpi` di atas, penting untuk menekankan bahwa **set virtual screen size** dan **set device dpi** dapat disesuaikan kapan saja sebelum rendering. Misalnya, Anda dapat meningkatkan DPI untuk screenshot beresolusi tinggi:

```java
        // 3️⃣ Adjust DPI for a high‑resolution render (optional).
        loadOptions.setDeviceDpi(300);   // 300 DPI is common for print‑ready images
        // 4️⃣ Change screen size for a mobile layout test.
        loadOptions.setScreenSize(new Size(375, 667)); // iPhone X viewport
```

Ingat untuk memuat ulang dokumen jika Anda mengubah pengaturan ini setelah pemuatan pertama—Aspose memperlakukan mereka sebagai tidak dapat diubah setelah `Document` dibuat.

## Langkah 4: Membaca Warna Latar Belakang dan Mendapatkan Warna Latar Belakang yang Dihitung

Dengan dokumen berada di memori, Anda dapat menanyakan gaya terhitung dari elemen mana pun. Di sini kami fokus pada tag `<body>`, tetapi pendekatan yang sama berlaku untuk `<div>`, `<p>`, atau bahkan pseudo‑elemen.

```java
        // 5️⃣ Retrieve the <body> element.
        Element bodyElement = document.getBody();

        // 6️⃣ Output the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

**Apa yang akan Anda lihat:** Jika `responsive.html` berisi `body { background: #ff5722; }`, konsol akan mencetak sesuatu seperti:

```
Computed background color: rgba(255,87,34,1)
```

Itulah hasil **get computed background color**—Aspose menyelesaikan semua aturan cascade CSS, media query, dan bahkan deklarasi `!important` sebelum mengembalikan nilai akhir.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang siap disalin‑tempel:

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create load options – virtual screen size + DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setScreenSize(new Size(1280, 800)); // set virtual screen size
        loadOptions.setDeviceDpi(96);                  // set device DPI (default desktop)

        // Optional: tweak for high‑resolution or mobile rendering.
        // loadOptions.setDeviceDpi(300);
        // loadOptions.setScreenSize(new Size(375, 667));

        // Step 2: Load the HTML document with the options.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);

        // Step 3: Grab the <body> element.
        Element bodyElement = document.getBody();

        // Step 4: Print the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

### Output yang Diharapkan

```
Computed background color: rgba(255,255,255,1)
```

*(Nilai RGBA yang tepat tergantung pada CSS dalam file HTML Anda.)*

## Kesalahan Umum & Tips Profesional

* **Pengaturan DPI hilang?** Aspose secara default menggunakan 96 DPI, yang dapat membuat screenshot beresolusi tinggi menjadi buram. Selalu atur secara eksplisit jika Anda memerlukan output yang tajam.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}