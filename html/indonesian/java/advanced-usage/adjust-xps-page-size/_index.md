---
date: 2026-03-18
description: Pelajari cara mengonversi HTML ke XPS dan menyesuaikan ukuran halaman
  XPS menggunakan Aspose.HTML untuk Java. Kendalikan dimensi output dengan mudah.
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Konversi HTML ke XPS dan Sesuaikan Ukuran Halaman XPS dengan Aspose.HTML untuk
  Java
url: /id/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengonversi HTML ke XPS dan Menyesuaikan Ukuran Halaman XPS dengan Aspose.HTML untuk Java

Dalam tutorial ini Anda akan menemukan **cara mengonversi HTML ke XPS** dan menyesuaikan ukuran halaman yang dihasilkan menggunakan Aspose.HTML untuk Java. Baik Anda membuat laporan yang dapat dicetak, faktur, atau dokumen arsip, mengontrol dimensi XPS memastikan output terlihat persis seperti yang Anda harapkan. Kami akan membimbing Anda melalui setiap langkah—dari menyiapkan lingkungan hingga merender file XPS akhir—sehingga Anda dapat mengintegrasikan kemampuan ini ke dalam aplikasi Java Anda segera.

## Jawaban Cepat
- **Apa arti “mengonversi HTML ke XPS”?** Itu merender dokumen HTML menjadi file XPS, mempertahankan tata letak dan gaya.  
- **Apakah saya memerlukan lisensi?** Versi percobaan gratis cukup untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Versi Java mana yang didukung?** Java 8 atau lebih tinggi (JDK 11+ disarankan).  
- **Bisakah saya mengubah ukuran halaman?** Ya – Aspose.HTML memungkinkan Anda menentukan dimensi khusus sebelum merender.  
- **Berapa lama proses konversi?** Biasanya kurang dari satu detik untuk halaman standar; dokumen yang lebih besar mungkin memerlukan waktu lebih lama.

## Apa itu mengonversi HTML ke XPS?
Mengonversi HTML ke XPS berarti mengambil file markup yang berorientasi web dan menghasilkan dokumen XPS (XML Paper Specification) — format tata letak tetap yang siap cetak, mirip dengan PDF. Ini berguna ketika Anda memerlukan dokumen dengan fidelitas tinggi dan independen perangkat untuk pengarsipan atau pencetakan dari aplikasi Java.

## Mengapa menyesuaikan ukuran halaman XPS?
Menyesuaikan ukuran halaman memberi Anda kontrol atas dimensi fisik dokumen akhir (misalnya A4, Letter, label khusus). Hal ini mencegah skala yang tidak diinginkan, memastikan konten pas dengan sempurna, dan dapat mengurangi ukuran file dengan menghilangkan ruang putih yang tidak diperlukan.

## Prasyarat

Sebelum memulai, pastikan Anda telah menyiapkan prasyarat berikut:

1. **Lingkungan Pengembangan Java** – Java Development Kit (JDK) terpasang di sistem Anda.  
2. **Pustaka Aspose.HTML untuk Java** – Unduh dan sertakan pustaka Aspose.HTML untuk Java dalam proyek Anda. Anda dapat menemukan pustaka tersebut [di sini](https://releases.aspose.com/html/java/).  
3. **File HTML Masukan** – Siapkan file HTML yang ingin Anda render dan sesuaikan ukuran halaman XPS‑nya. Anda dapat menggunakan file HTML Anda sendiri untuk tutorial ini.

## Impor Paket

Pertama, impor kelas‑kelas yang diperlukan. Paket‑paket ini memberi Anda akses ke penanganan dokumen, rendering, dan fitur pengaturan halaman.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Panduan Langkah‑per‑Langkah

Berikut adalah panduan singkat berurutan yang mencerminkan langkah‑langkah asli sambil menambahkan konteks tambahan untuk kejelasan.

### Langkah 1: Tetapkan Nama File Masukan

Baca file HTML sumber menggunakan `FileInputStream`. Stream ini menyuplai HTML mentah ke mesin Aspose.HTML.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### Langkah 2: Buat Dokumen HTML dan Atur Gaya

Buat instance `HTMLDocument` yang mewakili konten yang akan Anda render. Pada contoh ini kami juga menyisipkan blok CSS kecil untuk mendemonstrasikan styling—ganti dengan markup Anda sendiri bila diperlukan.

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### Langkah 3: Buat Opsi Rendering XPS

Instansiasi `XpsRenderingOptions` untuk menampung semua pengaturan yang memengaruhi konversi dari HTML ke XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### Langkah 4: Sesuaikan Ukuran Halaman  

**Cara mengatur ukuran halaman XPS** – Tentukan ukuran halaman khusus (lebar × tinggi dalam poin) dan beri tahu renderer apakah harus secara otomatis memperluas ke halaman terlebar. Menetapkan `adjustToWidestPage` ke `false` mempertahankan dimensi tepat yang Anda tentukan.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### Langkah 5: Render Output

Akhirnya, buat `XpsDevice` dengan opsi yang telah dikonfigurasi dan render dokumen HTML. Hasilnya adalah file XPS lengkap dengan dimensi halaman khusus yang Anda setel.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Masalah Umum dan Solusinya

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **Output XPS kosong** | Stream masukan tidak ditutup atau HTMLDocument menunjuk ke file yang salah. | Pastikan `FileInputStream` dibungkus dalam blok try‑with‑resources dan jalur file akurat. |
| **Ukuran halaman tidak diterapkan** | `adjustToWidestPage` dibiarkan `true`. | Setel `pageSetup.setAdjustToWidestPage(false);` seperti yang ditunjukkan pada Langkah 4. |
| **CSS tidak didukung** | Aspose.HTML mendukung subset CSS. | Gunakan layout, font, dan warna dasar; hindari selector lanjutan atau CSS Grid. |
| **LicenseException** | Menjalankan tanpa lisensi yang valid di produksi. | Terapkan lisensi sementara atau berbayar sebelum rendering (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Pertanyaan yang Sering Diajukan

**T: Apa itu Aspose.HTML untuk Java?**  
J: Aspose.HTML untuk Java adalah pustaka Java yang memungkinkan pengembang memanipulasi dan mengonversi dokumen HTML ke berbagai format, seperti XPS, PDF, dan gambar.

**T: Di mana saya dapat mengunduh Aspose.HTML untuk Java?**  
J: Anda dapat mengunduh pustaka Aspose.HTML untuk Java dari [tautan ini](https://releases.aspose.com/html/java/).

**T: Apakah ada versi percobaan gratis untuk Aspose.HTML untuk Java?**  
J: Ya, Anda dapat memperoleh versi percobaan gratis Aspose.HTML untuk Java dari [sini](https://releases.aspose.com/).

**T: Bagaimana cara mendapatkan lisensi sementara untuk Aspose.HTML untuk Java?**  
J: Untuk mendapatkan lisensi sementara Aspose.HTML untuk Java, kunjungi [halaman ini](https://purchase.aspose.com/temporary-license/).

**T: Apakah saya dapat mendapatkan dukungan untuk Aspose.HTML untuk Java?**  
J: Ya, Anda dapat mencari bantuan dan dukungan dari komunitas Aspose di [Forum Aspose](https://forum.aspose.com/).

**T: Bisakah saya mengonversi HTML ke XPS di server tanpa tampilan (headless)?**  
J: Tentu saja. Aspose.HTML berfungsi di lingkungan tanpa GUI; pastikan runtime Java telah dikonfigurasi dengan benar.

**T: Apakah pustaka ini mendukung margin halaman khusus?**  
J: Ya. Gunakan `PageSetup.setMarginTop()`, `setMarginBottom()`, dll., sebelum menetapkan `PageSetup` ke opsi rendering.

## Kesimpulan

Kami telah menelusuri proses lengkap **mengonversi HTML ke XPS** dan menyesuaikan ukuran halaman dengan Aspose.HTML untuk Java. Dengan mengikuti langkah‑langkah ini Anda dapat menghasilkan dokumen XPS siap cetak yang sesuai dengan persyaratan tata letak Anda. Jangan ragu bereksperimen dengan dimensi halaman yang berbeda, gaya, atau bahkan menambahkan header dan footer untuk memenuhi kebutuhan proyek Anda.

Jika Anda memiliki pertanyaan atau memerlukan bantuan lebih lanjut, jelajahi dokumentasi [Aspose.HTML untuk Java](https://reference.aspose.com/html/java/) atau bergabung dalam percakapan di [Forum Aspose](https://forum.aspose.com/).

---

**Terakhir Diperbarui:** 2026-03-18  
**Diuji Dengan:** Aspose.HTML untuk Java 24.11 (terbaru pada saat penulisan)  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}