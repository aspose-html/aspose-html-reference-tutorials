---
category: general
date: 2026-02-14
description: Cara mengatur DPI untuk konversi SVG ke PNG menggunakan Java. Mengekspor
  PNG resolusi tinggi, pelajari cara mengonversi SVG ke PNG, dan gunakan pustaka konversi
  gambar Java.
draft: false
keywords:
- how to set dpi
- convert svg to png
- export high resolution png
- how to convert svg
- java image conversion library
language: id
og_description: Cara mengatur DPI untuk konversi SVG ke PNG menggunakan Java. Panduan
  ini menunjukkan cara mengekspor PNG beresolusi tinggi dan menggunakan pustaka konversi
  gambar Java.
og_title: Cara Mengatur DPI Saat Mengonversi SVG ke PNG dengan Java
tags:
- java
- image-conversion
- svg
- png
title: Cara Mengatur DPI Saat Mengonversi SVG ke PNG dengan Java
url: /id/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengatur DPI Saat Mengonversi SVG ke PNG dengan Java

Pernah bertanya-tanya **how to set DPI** untuk konversi SVG‑to‑PNG agar hasilnya tampak tajam pada poster siap cetak? Anda bukan satu-satunya. Dalam banyak proyek—misalnya flyer pemasaran, mock‑up UI, atau diagram teknis—mendapatkan PNG beresolusi tinggi dari SVG adalah hal yang tidak dapat ditawar.  

Dalam tutorial ini kami akan membahas langkah‑langkah tepat untuk **convert SVG to PNG**, **export high resolution PNG**, dan, yang paling penting, mengontrol DPI menggunakan pustaka Aspose.HTML for Java. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat disisipkan ke dalam aplikasi Java apa pun, baik Anda membangun alat desktop maupun layanan backend.

## Apa yang Anda Butuhkan

- **Java 8+** (kode ini dapat dikompilasi dengan JDK terbaru apa pun)
- **Aspose.HTML for Java** JARs (tersedia di Maven Central atau situs web Aspose)
- Sebuah file SVG yang ingin Anda rasterisasi  
- Sedikit rasa ingin tahu—tidak ada yang lain.

Jika Anda nyaman dengan Maven, cukup tambahkan dependensi yang ditunjukkan pada bagian berikut; jika tidak, unduh JAR secara manual dan tambahkan ke classpath Anda.

## Langkah 1: Tambahkan Pustaka Konversi Gambar Java

Pertama-tama—proyek Anda memerlukan **java image conversion library** yang benar‑benar dapat membaca SVG dan menulis PNG. Aspose.HTML adalah pilihan yang solid karena menangani CSS, font, dan fitur vektor kompleks secara langsung.

**Pengguna Maven** dapat menempelkan ini ke dalam `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- use the latest stable version -->
</dependency>
```

**Pengguna Gradle** dapat menambahkan:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

Jika Anda lebih suka cara manual, unduh JAR dari halaman unduhan Aspose dan letakkan di `libs/`, lalu tambahkan ke jalur build IDE Anda.

> **Pro tip:** Perhatikan nomor versi; rilis yang lebih baru sering meningkatkan penanganan DPI dan memperbaiki bug kasus tepi.

## Langkah 2: Buat Opsi Konversi dan Atur DPI yang Diinginkan

Sekarang pustaka sudah siap, kita perlu memberi tahu *bagaimana* PNG output harus terlihat. Di sinilah kata kunci utama—**how to set DPI**—berperan. Kelas `ImageConversionOptions` memberi Anda kontrol granular atas resolusi horizontal (`dpiX`) dan vertikal (`dpiY`).

```java
import com.aspose.html.converters.ImageConversionOptions;

// Step 2: Build the options object and set DPI
ImageConversionOptions conversionOptions = new ImageConversionOptions();
conversionOptions.setDpiX(300); // 300 DPI horizontally
conversionOptions.setDpiY(300); // 300 DPI vertically
```

Mengapa 300 DPI? Untuk kebanyakan alur kerja cetak, 300 dots‑per‑inch dianggap “kualitas cetak”. Jika Anda menargetkan aset hanya untuk web, Anda dapat menurunkannya menjadi 72 atau 96 DPI untuk menjaga ukuran file tetap kecil.

> **Bagaimana jika saya membutuhkan DPI yang berbeda untuk lebar dan tinggi?**  
> Cukup ubah `setDpiX` dan `setDpiY` secara terpisah. Pustaka menghormati nilai non‑uniform, yang berguna untuk gambar anamorfik.

## Langkah 3: Lakukan Konversi SVG‑to‑PNG

Dengan opsi siap, konversi sebenarnya cukup dengan satu pemanggilan statis. Kami akan menggunakan `java.nio.file.Paths` untuk menjaga kompatibilitas lintas platform.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.Paths;

public class SvgToPng {
    public static void main(String[] args) throws Exception {
        // Paths to input SVG and output PNG
        var inputSvg  = Paths.get("YOUR_DIRECTORY/input.svg").toUri();
        var outputPng = Paths.get("YOUR_DIRECTORY/output.png").toUri();

        // Convert using the DPI settings we defined earlier
        Converter.convert(inputSvg, outputPng, conversionOptions);
    }
}
```

Itu saja—jalankan metode `main` dan Anda akan menemukan PNG tajam 300 DPI berada di `YOUR_DIRECTORY`. Pustaka secara otomatis menskalakan grafik vektor agar sesuai dengan DPI yang Anda tentukan, mempertahankan rasio aspek dan kejernihan teks.

## Langkah 4: Verifikasi Hasil (Opsional tetapi Disarankan)

Pemeriksaan cepat dapat menyelamatkan Anda dari masalah di kemudian hari. Buka PNG yang dihasilkan di penampil gambar apa pun yang menampilkan metadata DPI (mis., Photoshop, GIMP, atau bahkan tab “Details” di Windows Explorer). Anda harus melihat **300 DPI** terdaftar di resolusi horizontal dan vertikal.

Jika file terlihat buram, periksa kembali:

1. SVG asli tidak beresolusi rendah sejak awal (file vektor bersifat agnostik resolusi, tetapi gambar raster yang disematkan di dalamnya dapat membatasi kualitas).  
2. Anda benar‑benar menyimpan file setelah mengatur DPI—kadang IDE menyimpan cache build lama.  
3. Opsi konversi tidak ditimpa di tempat lain dalam kode Anda.

## Mengapa DPI Penting untuk Export High Resolution PNG

Anda mungkin bertanya, “Mengapa repot‑repot dengan DPI? Bukankah PNG hanya piksel?” Faktanya DPI adalah tag *metadata* yang memberi tahu aplikasi hilir (terutama yang berorientasi cetak) berapa banyak piksel yang sesuai dengan satu inci ruang fisik. Jika Anda memberikan PNG 1200 × 800 ke printer tanpa metadata DPI yang tepat, printer mungkin mengasumsikan nilai default (sering 72 DPI) dan memperbesar gambar, menghasilkan output yang buram.

Mengatur DPI dengan benar juga meningkatkan kinerja: Anda menghindari kebutuhan untuk memperbesar gambar raster nanti, yang dapat memakan banyak komputasi dan menurunkan kualitas.

## Kasus Edge & Kesalahan Umum

| Situation | What to Watch For | How to Fix |
|-----------|-------------------|------------|
| **SVG contains embedded bitmap images** | Bitmap yang disematkan mungkin beresolusi rendah, menyebabkan PNG akhir tampak pixelated meskipun DPI tinggi. | Ganti bitmap dengan versi beresolusi lebih tinggi atau edit SVG untuk merujuk ke gambar eksternal. |
| **Large DPI values (e.g., 1200 DPI)** | Konsumsi memori melonjak; Anda mungkin mengalami `OutOfMemoryError`. | Tingkatkan ukuran heap JVM (`-Xmx2g`) atau batasi DPI ke nilai maksimum yang wajar untuk kasus penggunaan Anda. |
| **Non‑square pixels** | Beberapa tampilan menginterpretasikan DPI secara berbeda, menyebabkan gambar terdistorsi. | Pastikan `setDpiX` sama dengan `setDpiY` kecuali Anda memiliki alasan khusus untuk berbeda. |
| **Missing fonts** | Teks dalam SVG mungkin kembali ke font default, mengubah tata letak. | Sematkan font dalam SVG atau instal font yang diperlukan pada mesin runtime. |

## Ringkasan Cepat (dalam Satu Kalimat)

Untuk **how to set DPI** pada konversi SVG‑to‑PNG, buat objek `ImageConversionOptions`, atur `dpiX`/`dpiY`, dan panggil `Converter.convert` dari pustaka Aspose.HTML Java.

## Langkah Selanjutnya & Topik Terkait

- **Batch processing:** Loop melalui direktori file SVG dan terapkan pengaturan DPI yang sama.  
- **Dynamic DPI:** Baca file konfigurasi atau argumen baris perintah untuk mengatur DPI pada runtime.  
- **Alternative libraries:** Jika Anda tidak dapat menggunakan Aspose, pertimbangkan **Batik** (Apache) atau **SVG Salamander**, meskipun mungkin memerlukan kode tambahan untuk menangani DPI.  
- **Export high resolution PNG** untuk aset Android: gabungkan teknik ini dengan folder `drawable‑hdpi`, `xhdpi`, dll., pada Android.

Silakan bereksperimen—coba 72 DPI untuk thumbnail web, 600 DPI untuk cetakan format besar, atau bahkan 150 DPI sebagai kompromi. Kode tetap sama; hanya angka yang berubah.

---

![cara mengatur dpi](placeholder-image.png "Ilustrasi pengaturan DPI dalam alur kerja konversi Java")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}