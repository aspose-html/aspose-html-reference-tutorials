---
category: general
date: 2026-03-29
description: Cara menyisipkan gambar saat mengonversi MHTML ke PDF dengan Aspose HTML.
  Kurangi ukuran file PDF dan kuasai teknik Aspose HTML ke PDF dalam hitungan menit.
draft: false
keywords:
- how to embed images
- convert mhtml to pdf
- reduce pdf file size
- aspose html to pdf
- reduce pdf size
language: id
og_description: Cara menyisipkan gambar saat mengonversi MHTML ke PDF dengan Aspose
  HTML. Pelajari cara mengurangi ukuran file PDF dan memanfaatkan Aspose HTML ke PDF
  secara maksimal.
og_title: Cara menyisipkan gambar saat mengonversi MHTML ke PDF – Panduan Aspose
tags:
- Aspose
- Java
- PDF
- MHTML
title: Cara menyematkan gambar saat mengonversi MHTML ke PDF – Panduan Aspose
url: /id/java/conversion-html-to-other-formats/how-to-embed-images-when-converting-mhtml-to-pdf-aspose-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyematkan gambar saat mengonversi MHTML ke PDF – Panduan Aspose

Pernah bertanya-tanya **cara menyematkan gambar** selama konversi MHTML‑ke‑PDF dan menjaga file hasil tetap ringan? Anda tidak sendirian. Banyak pengembang mengalami masalah ketika PDF mereka membengkak karena setiap sumber daya—font, skrip, bahkan ikon kecil—dimasukkan ke dalamnya. Kabar baiknya? Dengan Aspose.HTML untuk Java Anda dapat memberi tahu konverter untuk menyematkan **hanya gambar**, meninggalkan yang lainnya sebagai referensi eksternal. Penyesuaian tunggal ini sering kali memangkas ukuran PDF secara dramatis.

Dalam tutorial ini kami akan membahas cara mengonversi laporan MHTML ke PDF, fokus pada **cara menyematkan gambar**, dan menambahkan beberapa tips tambahan untuk **mengurangi ukuran file PDF**. Pada akhir tutorial Anda akan memiliki kelas Java siap‑jalankan, memahami mengapa menyematkan hanya gambar penting, dan tahu ke mana harus pergi jika nanti Anda perlu menyematkan font atau sumber daya lain. Tanpa jalan pintas “lihat dokumen”—hanya solusi lengkap yang dapat disalin‑tempel.

## Apa yang akan Anda pelajari

- Panggilan API yang tepat untuk **mengonversi MHTML ke PDF** dengan Aspose.HTML.
- Cara mengonfigurasi `PdfConversionOptions` sehingga konverter **menyematkan hanya gambar**.
- Mengapa menyematkan hanya gambar membantu **mengurangi ukuran PDF** dan kapan Anda mungkin memerlukan pengaturan berbeda.
- Contoh Java lengkap yang dapat dijalankan dan dapat dimasukkan ke dalam proyek Maven/Gradle apa pun.
- Kesalahan umum (sumber daya yang hilang, jalur file yang salah) dan cara memperbaikinya dengan cepat.

### Prasyarat

- Java 8 atau yang lebih baru terpasang.
- Maven atau Gradle untuk mengelola dependensi (kami akan menunjukkan cuplikan Maven).
- Perpustakaan Aspose.HTML untuk Java (Anda dapat mengunduh versi percobaan gratis dari situs Aspose).
- File MHTML yang ingin Anda ubah menjadi PDF (contoh menggunakan `report.mhtml`).

> **Pro tip:** Simpan MHTML dan PDF output dalam folder yang sama selama pengujian; jalur relatif membuat semuanya lebih rapi.

---

## Langkah 1 – Tambahkan Aspose.HTML ke proyek Anda

Jika Anda menggunakan Maven, tempelkan berikut ke dalam `pom.xml` Anda. Versi yang ditampilkan adalah yang terbaru per Maret 2026; periksa repositori Aspose untuk rilis yang lebih baru.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

Untuk Gradle, setaraannya adalah:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

Setelah dependensi terunduh, Anda siap mengimpor kelas‑kelas yang diperlukan.

## Langkah 2 – Buat opsi konversi dan atur mode penyematan

Inti dari **cara menyematkan gambar** terletak pada `PdfConversionOptions`. Secara default Aspose menyematkan *semua* sumber daya (font, CSS, gambar). Kita akan mengubahnya menjadi `EMBED_IMAGES_ONLY`.

```java
// Step 2: Prepare conversion options – embed only images
PdfConversionOptions options = new PdfConversionOptions();
options.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);
```

Mengapa ini penting? Bayangkan sebuah laporan korporat yang merujuk pada font perusahaan yang disimpan di share jaringan. Menyematkan font tersebut menambah ratusan kilobyte pada PDF meskipun pembaca dapat mengambilnya secara remote. Dengan menyematkan hanya gambar, PDF tetap mempertahankan kualitas visual yang Anda butuhkan sekaligus tetap ringan.

## Langkah 3 – Lakukan konversi

Sekarang panggil `Converter.convert`, berikan jalur MHTML sumber, jalur PDF tujuan, dan opsi yang baru saja kita konfigurasikan.

```java
// Step 3: Convert MHTML to PDF using the options above
String sourcePath = "YOUR_DIRECTORY/report.mhtml";
String targetPath = "YOUR_DIRECTORY/report.pdf";

Converter.convert(sourcePath, targetPath, options);
```

Jika semuanya terhubung dengan benar, Anda akan melihat `report.pdf` muncul di samping file MHTML Anda. Buka file tersebut—setiap gambar dari laporan asli harus muncul, sementara font dan CSS tetap sebagai referensi eksternal.

## Langkah 4 – Verifikasi pengurangan ukuran PDF

Pemeriksaan cepat membantu memastikan Anda memang **mengurangi ukuran PDF**. Bandingkan ukuran file sebelum dan sesudah mengubah mode penyematan:

```java
File before = new File("YOUR_DIRECTORY/report_full.pdf"); // generated with default settings
File after  = new File(targetPath); // our image‑only PDF

System.out.println("Full embed size: " + before.length() / 1024 + " KB");
System.out.println("Images‑only size: " + after.length() / 1024 + " KB");
```

Dalam kebanyakan kasus Anda akan melihat penurunan 30‑70 % tergantung berapa banyak font atau file CSS yang sebelumnya disematkan. Itu merupakan kemenangan signifikan bagi siapa saja yang mengirim PDF melalui web atau menyimpannya di bucket cloud.

## Langkah 5 – Contoh lengkap yang dapat dijalankan

Berikut seluruh kelas Java yang dapat Anda salin ke IDE. Ganti `YOUR_DIRECTORY` dengan jalur folder sebenarnya tempat `report.mhtml` berada.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.converters.ResourceEmbeddingMode;

import java.io.File;

public class MhtmlToPdf {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define source and destination ----------
        String sourcePath = "YOUR_DIRECTORY/report.mhtml";
        String targetPath = "YOUR_DIRECTORY/report.pdf";

        // ---------- Step 2: Set conversion options (embed only images) ----------
        PdfConversionOptions conversionOptions = new PdfConversionOptions();
        conversionOptions.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);

        // ---------- Step 3: Run the conversion ----------
        Converter.convert(sourcePath, targetPath, conversionOptions);
        System.out.println("Conversion complete! PDF saved to: " + targetPath);

        // ---------- Step 4: (Optional) Show size reduction ----------
        File outputPdf = new File(targetPath);
        System.out.println("Resulting PDF size: " + outputPdf.length() / 1024 + " KB");
    }
}
```

**Output yang diharapkan** (di konsol):

```
Conversion complete! PDF saved to: YOUR_DIRECTORY/report.pdf
Resulting PDF size: 842 KB
```

Buka `report.pdf` di penampil apa pun; Anda harus melihat semua gambar asli ditampilkan dengan benar. Jika ada gambar yang hilang, periksa kembali apakah URL gambar di MHTML bersifat absolut atau apakah file dapat diakses oleh mesin konversi.

## Pertanyaan umum & penanganan kasus tepi

### Bagaimana jika saya *perlu* menyematkan font?

Ubah `ResourceEmbeddingMode` menjadi `EMBED_ALL` atau `EMBED_FONTS_ONLY`. Enum ini menawarkan empat pilihan:

| Mode                     | Apa yang disematkan |
|--------------------------|---------------------|
| `EMBED_ALL`              | Gambar, font, CSS |
| `EMBED_IMAGES_ONLY`      | Hanya gambar (default kami) |
| `EMBED_FONTS_ONLY`       | Hanya font |
| `EMBED_NONE`             | Tidak ada (hanya referensi eksternal) |

### MHTML saya berisi CSS eksternal yang memengaruhi tata letak—apakah PDF akan rusak?

Karena kami tidak menyematkan CSS, konverter tetap akan mengunduhnya selama konversi. Jika CSS dihosting di intranet yang tidak dapat dijangkau server konversi, tata letak mungkin kembali ke nilai default. Dalam kasus tersebut, baik menyematkan CSS (`EMBED_ALL`) atau menyalin stylesheet secara lokal dan menyesuaikan MHTML agar merujuk ke file lokal.

### Bisakah saya memproses batch folder berisi file MHTML?

Tentu saja. Bungkus logika konversi dalam loop yang iterasi melalui `File.listFiles()` dan ubah nama file target sesuai kebutuhan. Ingat untuk menggunakan satu instance `PdfConversionOptions` untuk meningkatkan performa.

### Bagaimana dengan konsumsi memori untuk dokumen sangat besar?

Aspose.HTML melakukan streaming konten, sehingga penggunaan memori tetap wajar. Namun, gambar berukuran sangat besar masih dapat menyebabkan lonjakan memori. Jika Anda menemui `OutOfMemoryError`, pertimbangkan menurunkan resolusi gambar sebelum disematkan—Aspose menyediakan `ImageConversionOptions` untuk itu, tetapi itu topik untuk tutorial lain.

---

## Kesimpulan

Anda kini mengetahui **cara menyematkan gambar** saat mengonversi MHTML ke PDF dengan Aspose.HTML, dan telah melihat mengapa pengaturan kecil ini dapat **mengurangi ukuran PDF** secara dramatis. Contoh Java lengkap yang dapat disalin‑tempel menunjukkan alur penuh—dari menambahkan dependensi Maven hingga mencetak ukuran file akhir.

Selanjutnya Anda dapat:

- Bereksperimen dengan `EMBED_FONTS_ONLY` jika PDF Anda harus sepenuhnya mandiri.
- Mengotomatiskan konversi batch untuk seluruh folder laporan.
- Menggabungkan teknik ini dengan API optimasi PDF Aspose untuk file yang lebih kecil lagi.

Apakah Anda membangun layanan pelaporan, pipeline email‑ke‑PDF, atau sekadar merapikan halaman web yang diarsipkan, mengendalikan apa yang disematkan adalah tuas utama untuk kinerja dan biaya. Cobalah, sesuaikan opsi, dan biarkan PDF Anda tetap ramping.

*Selamat coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}