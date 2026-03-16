---
date: 2026-01-09
description: Pelajari cara menggunakan Aspose.HTML untuk Java untuk menentukan opsi
  penyimpanan XPS dan mengonversi EPUB ke XPS secara efisien.
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: Menentukan Opsi Penyimpanan Aspose HTML untuk Konversi EPUB ke XPS
url: /id/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menentukan Opsi Penyimpanan Aspose HTML untuk EPUB ke XPS

Mengonversi dokumen EPUB ke XPS dapat menjadi bagian yang berguna dalam alur kerja penerbitan, dan **Aspose HTML Save Options** memberi Anda kontrol yang sangat detail atas output. Pada tutorial ini kami akan menjelaskan langkah‑langkah tepat yang diperlukan untuk mengonfigurasi opsi penyimpanan tersebut dengan Aspose.HTML untuk Java dan menghasilkan file XPS berkualitas tinggi.

## Jawaban Cepat
- **Apa yang dilakukan Aspose HTML Save Options?** Ini memungkinkan Anda menyesuaikan ukuran halaman, warna latar belakang, dan pengaturan rendering lainnya saat menyimpan ke format seperti XPS.  
- **Perpustakaan apa yang diperlukan?** Aspose.HTML untuk Java (versi terbaru).  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis dapat digunakan untuk evaluasi; lisensi komersial diperlukan untuk produksi.  
- **Bisakah saya mengubah dimensi halaman?** Ya – Anda dapat mengatur lebar dan tinggi apa pun melalui `PageSetup`.  
- **Apakah konversi cepat?** Untuk file EPUB tipikal, konversi selesai dalam hitungan detik pada JVM modern.

## Apa Itu Aspose HTML Save Options?
Aspose HTML Save Options adalah sekumpulan properti yang mengontrol bagaimana HTML, EPUB, atau dokumen berbasis web lainnya dirender dan disimpan ke format target seperti XPS, PDF, atau file gambar. Mereka memungkinkan Anda menentukan tata letak halaman, warna latar belakang, margin, dan lainnya, memastikan file yang dihasilkan sesuai dengan kebutuhan desain Anda.

## Mengapa Menggunakan Aspose.HTML untuk Java untuk Mengonversi EPUB ke XPS?
- **Fidelity tinggi** – mempertahankan tata letak kompleks, font, dan grafik vektor.  
- **Kontrol programatik** – mengotomatisasi konversi batch dalam aplikasi Java.  
- **Tanpa dependensi eksternal** – perpustakaan Java murni, tanpa komponen native.  
- **Output yang dapat disesuaikan** – berkat opsi penyimpanan Anda dapat menyesuaikan XPS sesuai kebutuhan tepat Anda.

## Prasyarat

Sebelum kita masuk ke kode, pastikan Anda memiliki hal‑hal berikut:

1. **Lingkungan Pengembangan Java** – JDK 8 atau lebih tinggi terpasang.  
2. **Perpustakaan Aspose.HTML untuk Java** – unduh dari [tautan unduhan](https://releases.aspose.com/html/java/).  
3. **File EPUB** – EPUB sumber yang ingin Anda konversi.  

Menyiapkan hal‑hal ini akan memungkinkan Anda mengikuti langkah‑langkah tanpa gangguan.

## Mengimpor Paket

Pertama, impor kelas yang diperlukan. Letakkan pernyataan impor di bagian atas file sumber Java Anda:

```java
import java.io.FileInputStream;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import com.aspose.html.system.io.resources.Resources;
```

Impor ini memberi Anda akses ke mesin konversi dan **Aspose HTML Save Options** yang diperlukan untuk penyetelan detail.

## Membuka File EPUB

Selanjutnya, buka EPUB yang ingin Anda konversi. Pembantu `Resources.input` memuat file dari folder sumber daya demo:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

Menggunakan blok try‑with‑resources memastikan aliran ditutup secara otomatis.

## Membuat XPS Save Options (Mengonfigurasi Ukuran Halaman & Latar Belakang)

Sekarang kita membuat instance `XpsSaveOptions` dan menyesuaikannya. Di sinilah **opsi penyimpanan** benar‑benar bersinar:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **Ukuran halaman** – diatur menjadi 3000 × 1000 piksel dalam contoh ini; sesuaikan dengan ukuran kertas target Anda.  
- **Warna latar belakang** – `AliceBlue` menunjukkan cara mengubah latar belakang kanvas; Anda dapat memilih warna `Color` apa pun.  

Pengaturan ini merupakan bagian dari **Aspose HTML Save Options** yang memengaruhi dokumen XPS akhir.

## Mengonversi EPUB ke XPS

Akhirnya, panggil konverter dengan aliran, opsi yang telah dikonfigurasi, dan jalur output:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

Saat baris ini dijalankan, Aspose.HTML membaca EPUB, menerapkan pengaturan halaman dan warna latar belakang yang Anda definisikan, dan menulis file XPS yang sepenuhnya sesuai.

## Masalah Umum & Tips

- **Dimensi halaman tidak tepat** – pastikan dimensi dinyatakan dalam piksel (atau gunakan `Length.fromInches`).  
- **Font hilang** – sematkan font yang diperlukan dalam EPUB atau instal di host JVM untuk menghindari fallback.  
- **File besar** – untuk EPUB yang sangat besar, tingkatkan heap JVM (`-Xmx`) untuk mencegah `OutOfMemoryError`.  

## Kesimpulan

Dengan memanfaatkan **Aspose HTML Save Options**, Anda mendapatkan kontrol yang tepat atas cara EPUB dirender menjadi XPS. Langkah‑langkah di atas menunjukkan cara mengatur ukuran halaman, warna latar belakang, dan melakukan konversi dengan hanya beberapa baris kode Java. Integrasikan pola ini ke dalam pipeline pemrosesan batch Anda untuk mengotomatisasi tugas penerbitan secara efisien.

## Pertanyaan yang Sering Diajukan

**Q: Apa itu Aspose.HTML untuk Java?**  
A: Itu adalah perpustakaan Java yang memungkinkan pengembang membuat, mengedit, merender, dan mengonversi HTML, EPUB, dan dokumen berbasis web lainnya tanpa memerlukan peramban.

**Q: Bisakah saya menggunakan ini dalam proyek komersial?**  
A: Ya. Untuk penggunaan produksi Anda memerlukan lisensi yang valid. Anda dapat membeli satu pada [halaman pembelian](https://purchase.aspose.com/buy).

**Q: Apakah ada versi percobaan gratis?**  
A: Tentu saja. Unduh versi percobaan dari [di sini](https://releases.aspose.com/).

**Q: Di mana saya dapat mendapatkan dukungan?**  
A: Dukungan komunitas dan bantuan resmi tersedia melalui forum Aspose di [https://forum.aspose.com/](https://forum.aspose.com/).

**Q: Apa saja persyaratan sistem?**  
A: Java Development Kit (JDK) 8+ dan sistem operasi yang didukung oleh runtime Aspose. Pastikan lingkungan Anda memenuhi prasyarat yang tercantum sebelumnya.

**Last Updated:** 2026-01-09  
**Tested With:** Aspose.HTML for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}