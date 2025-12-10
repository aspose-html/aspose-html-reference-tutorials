---
date: 2025-12-10
description: Pelajari cara mengatur batas waktu di Aspose.HTML untuk Java, mengonfigurasi
  Runtime Service untuk mengonversi HTML ke PNG, mencegah loop tak terbatas, dan meningkatkan
  kinerja.
linktitle: Configure Runtime Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Cara Mengatur Timeout di Layanan Runtime Aspose.HTML untuk Java
url: /id/java/configuring-environment/configure-runtime-service/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengatur Timeout di Aspose.HTML untuk Layanan Runtime Java

## Pendahuluan
Jika Anda mencari **how to set timeout** untuk skrip saat bekerja dengan Aspose.HTML untuk Java, Anda berada di tempat yang tepat. Mengontrol eksekusi skrip tidak hanya mencegah loop tak berujung tetapi juga membantu Anda **convert html to png** lebih cepat dan menjaga aplikasi tetap responsif. Dalam tutorial ini kami akan menjelaskan langkah‑langkah tepat untuk mengonfigurasi Runtime Service, membatasi eksekusi skrip, dan akhirnya menghasilkan gambar PNG dari HTML tanpa membuat program Anda macet.

## Jawaban Cepat
- **Apa yang dilakukan Runtime Service?** Ia memungkinkan Anda mengontrol waktu eksekusi skrip dan mengelola sumber daya saat memproses HTML.  
- **Bagaimana cara mengatur timeout untuk JavaScript?** Gunakan `runtimeService.setJavaScriptTimeout(TimeSpan.fromSeconds(...))`.  
- **Apakah saya dapat mencegah loop tak berujung?** Ya – timeout menghentikan loop yang melebihi batas yang ditentukan.  
- **Apakah ini memengaruhi konversi HTML‑to‑PNG?** Tidak, konversi berlanjut setelah skrip selesai atau dihentikan oleh timeout.  
- **Versi Aspose.HTML mana yang diperlukan?** Rilis terbaru dari halaman unduhan Aspose.

## Prasyarat
Sebelum kita masuk ke detail teknis, pastikan Anda memiliki hal‑hal berikut:

1. **Java Development Kit (JDK)** – instal dari [Oracle's website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java Library** – dapatkan build terbaru dari [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse, atau NetBeans dapat digunakan.  
4. **Pengetahuan dasar Java & HTML** – penting untuk mengikuti contoh kode.

## Impor Paket
Pertama, impor kelas yang Anda perlukan. Impor `java.io.IOException` diperlukan untuk penanganan file.

```java
import java.io.IOException;
```

## Langkah 1: Buat File HTML dengan Kode JavaScript
Kami akan memulai dengan menghasilkan file HTML sederhana yang berisi loop JavaScript. Loop ini akan berjalan selamanya jika kami tidak memberlakukan timeout, menjadikannya demo yang sempurna untuk Runtime Service.

```java
String code = "<h1>Runtime Service</h1>\r\n" +
        "<script> while(true) {} </script>\r\n" +
        "<p>The Runtime Service optimizes your system by helping it start apps and programs faster.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("runtime-service.html")) {
    fileWriter.write(code);
}
```

- Script `while(true) {}` mewakili potensi loop tak berujung.  
- `FileWriter` menulis konten HTML ke **runtime-service.html**.

## Langkah 2: Siapkan Objek Konfigurasi
Selanjutnya, buat instance `Configuration`. Objek ini adalah tulang punggung untuk semua layanan Aspose.HTML, termasuk Runtime Service.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Langkah 3: Konfigurasikan Runtime Service
Di sinilah kami benar‑benar **how to set timeout**. Dengan mengambil `IRuntimeService` dari konfigurasi, kami dapat menentukan batas eksekusi JavaScript.

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

- `setJavaScriptTimeout` membatasi eksekusi skrip pada **5 detik**, secara efektif **mencegah loop tak berujung**.  
- Ini juga **membatasi eksekusi skrip** untuk kode sisi klien yang berat.

## Langkah 4: Muat Dokumen HTML dengan Konfigurasi
Sekarang muat file HTML menggunakan konfigurasi yang berisi aturan timeout kami.

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

- Dokumen menghormati timeout yang telah ditetapkan sebelumnya, sehingga loop tak berujung akan dihentikan setelah 5 detik.

## Langkah 5: Konversi HTML ke PNG
Dengan dokumen yang sudah aman dimuat, kami dapat **convert html to png**. Konversi terjadi hanya setelah skrip selesai atau dihentikan oleh timeout.

```java
    com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.ImageSaveOptions(),
        "runtime-service_out.png"
    );
```

- `ImageSaveOptions` memberi tahu Aspose.HTML untuk menghasilkan gambar PNG.  
- File hasil, **runtime-service_out.png**, menampilkan HTML yang dirender tanpa macet.

## Langkah 6: Bersihkan Sumber Daya
Akhirnya, buang objek‑objek untuk membebaskan memori dan menghindari kebocoran.

```java
} finally {
    if (document != null) {
        document.dispose();
    }
    if (configuration != null) {
        configuration.dispose();
    }
}
```

- Pembuangan yang tepat penting untuk aplikasi yang berjalan lama.

## Kesimpulan
Anda baru saja mempelajari **how to set timeout** untuk eksekusi JavaScript di Aspose.HTML untuk Java, cara **prevent infinite loops**, dan cara **convert html to png** secara aman. Dengan mengonfigurasi Runtime Service Anda mendapatkan kontrol yang halus atas perilaku skrip, yang berujung pada waktu mulai yang lebih cepat dan konversi yang lebih andal. Bereksperimenlah dengan nilai timeout yang berbeda untuk menyesuaikan beban kerja spesifik Anda, dan Anda akan melihat peningkatan kinerja yang signifikan.

## Pertanyaan yang Sering Diajukan

**Q: Apa tujuan Runtime Service di Aspose.HTML untuk Java?**  
A: Ia memungkinkan Anda mengontrol waktu eksekusi skrip, membantu **prevent infinite loops** dan menjaga konversi tetap responsif.

**Q: Bagaimana cara mengunduh Aspose.HTML untuk Java?**  
A: Dapatkan versi terbaru dari [releases page](https://releases.aspose.com/html/java/).

**Q: Apakah perlu membuang objek `document` dan `configuration`?**  
A: Ya, pembuangan melepaskan sumber daya native dan mencegah kebocoran memori.

**Q: Bisakah saya mengatur timeout JavaScript ke nilai selain 5 detik?**  
A: Tentu – ubah argumen `TimeSpan.fromSeconds()` ke batas yang sesuai dengan skenario Anda.

**Q: Di mana saya dapat menemukan bantuan jika mengalami masalah?**  
A: Kunjungi [Aspose.HTML forum](https://forum.aspose.com/c/html/29) untuk bantuan komunitas dan staf.

---

**Terakhir Diperbarui:** 2025-12-10  
**Diuji Dengan:** Aspose.HTML for Java 24.11 (latest)  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}