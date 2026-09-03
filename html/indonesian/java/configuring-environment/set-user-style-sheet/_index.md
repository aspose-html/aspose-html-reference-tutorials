---
date: 2026-02-04
description: Pelajari cara membuat PDF dari HTML dengan mengatur stylesheet pengguna
  khusus di Aspose.HTML untuk Java, dan dengan mudah mengonversi HTML ke PDF menggunakan
  Layanan Agen Pengguna.
linktitle: Set User Style Sheet in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Buat PDF dari HTML – Atur Lembar Gaya Pengguna di Aspose.HTML untuk Java
url: /id/java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat PDF dari HTML – Atur User Style Sheet di Aspose.HTML untuk Java

## Pendahuluan
Dalam tutorial ini Anda akan belajar cara **membuat PDF dari HTML** menggunakan Aspose.HTML untuk Java sambil menerapkan stylesheet pengguna khusus.  
Pernahkah Anda ingin mengubah tampilan dokumen HTML Anda dengan gaya unik Anda sendiri? Bayangkan Anda sedang membuat sebuah halaman web dan membutuhkan judul yang menonjol dengan warna tertentu atau paragraf yang tampak konsisten di semua perangkat. Di sinilah *user stylesheet* dan **User Agent Service** berperan. Kami akan membimbing Anda melalui setiap langkah—dari menulis file HTML sederhana, mengonfigurasi user agent, hingga akhirnya **mengonversi HTML ke PDF**—sehingga Anda dapat melihat hasilnya secara langsung.

## Jawaban Cepat
- **Apa arti “create PDF from HTML”?** Itu berarti merender dokumen HTML (dengan CSS, gambar, font, dll.) dan menyimpan output visualnya sebagai file PDF.  
- **Komponen Aspose apa yang diperlukan?** Library Aspose.HTML untuk Java menyediakan mesin konversi dan User Agent Service.  
- **Apakah saya memerlukan lisensi untuk pengujian?** Versi percobaan gratis cukup untuk pengembangan; lisensi komersial diperlukan untuk produksi.  
- **Bisakah saya menggunakan file CSS eksternal?** Ya – Anda dapat menautkan stylesheet eksternal seperti pada browser biasa.  
- **Berapa lama proses konversi?** Untuk dokumen sederhana seperti pada panduan ini, konversi selesai dalam kurang dari satu detik.

## Prasyarat
Sebelum kita masuk ke kode, pastikan Anda memiliki hal‑hal berikut:

1. **Aspose.HTML untuk Java** – unduh JAR terbaru dari [halaman rilis Aspose](https://releases.aspose.com/html/java/).  
2. **Java Development Kit (JDK) 8+** – pastikan `java -version` menampilkan 8 atau lebih tinggi.  
3. **IDE** – IntelliJ IDEA, Eclipse, atau NetBeans semuanya dapat digunakan.  
4. **Pengetahuan dasar HTML/CSS** – membantu tetapi tidak wajib.

## Impor Paket
Untuk memulai, impor kelas Java yang penting. Satu‑satunya impor eksplisit yang Anda perlukan untuk contoh ini adalah `java.io.IOException`; kelas‑kelas Aspose akan direferensikan dengan nama lengkapnya nanti.

```java
import java.io.IOException;
```

## Langkah 1: Buat Dokumen HTML Sederhana
Pertama, kita akan menulis file HTML minimal (`document.html`) yang akan menjadi sumber untuk konversi PDF kita.

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro tip:** Simpan file HTML di direktori yang sama dengan sumber Java Anda untuk menghindari masalah terkait jalur.

## Langkah 2: Siapkan Konfigurasi Aspose.HTML
Buat objek `Configuration`. Objek ini berfungsi sebagai wadah untuk semua layanan (termasuk User Agent Service) yang akan Anda gunakan nanti.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Mengapa Menggunakan User Agent Service?
**User Agent Service** memberi Anda kontrol tingkat rendah atas opsi rendering seperti set karakter default, bahasa, font, dan—yang paling penting untuk tutorial ini—stylesheet pengguna khusus. Dengan menerapkan gaya pada level ini, Anda menjamin output visual yang konsisten meskipun HTML asli tidak memiliki CSS sendiri.

## Langkah 3: Akses User Agent Service  
**User Agent Service** memungkinkan Anda menyuntikkan stylesheet khusus, mengatur set karakter default, dan mengontrol opsi rendering lainnya.

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## Langkah 4: Definisikan dan Terapkan User Stylesheet  
Sekarang kita menyediakan aturan CSS yang akan menata HTML saat dirender. Di sinilah kita **menggunakan user agent service** untuk menetapkan stylesheet.

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **Mengapa ini penting:** Dengan menerapkan stylesheet pada level user‑agent, Anda memastikan gaya tersebut dihormati bahkan jika HTML asli tidak merujuk ke file CSS.

## Langkah 5: Muat Dokumen HTML dengan Konfigurasi Kustom  
Berikan baik jalur file maupun instance `Configuration` ke konstruktor `HTMLDocument`. Ini mengikat user stylesheet ke dokumen.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## Langkah 6: Konversi HTML ke PDF  
Dengan dokumen yang sudah sepenuhnya ditata, panggil metode statis `convertHTML` untuk **mengonversi HTML ke PDF**. Objek `PdfSaveOptions` memungkinkan Anda menyesuaikan output (misalnya ukuran halaman, kompresi).

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **Hasil:** `user-agent-stylesheet_out.pdf` akan berisi judul berwarna coklat dan paragraf dengan latar belakang GhostWhite, persis seperti yang didefinisikan dalam stylesheet.

## Langkah 7: Bersihkan Sumber Daya  
Selalu dispose objek Aspose untuk membebaskan memori native.

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

## Masalah Umum & Solusinya
| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| **Blank PDF output** | Tidak ada stylesheet yang diterapkan atau dokumen tidak dimuat dengan konfigurasi. | Pastikan `configuration` diberikan ke `HTMLDocument` dan `setUserStyleSheet` dipanggil sebelum pemuatan. |
| **Unsupported CSS property warning** | Aspose.HTML tidak mendukung beberapa fitur CSS lanjutan. | Gunakan hanya properti CSS yang tercantum dalam dokumentasi Aspose.HTML atau gunakan gaya yang lebih sederhana. |
| **FileNotFoundException** | Jalur ke `document.html` salah. | Gunakan jalur absolut atau letakkan file HTML di root proyek. |

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya menerapkan gaya berbeda untuk elemen HTML yang berbeda?**  
J: Tentu saja! Anda dapat mendefinisikan sebanyak mungkin aturan CSS yang Anda perlukan dalam user stylesheet.

**T: Bagaimana jika saya perlu mengubah stylesheet secara dinamis?**  
J: Panggil `setUserStyleSheet` lagi sebelum membuat instance `HTMLDocument` baru; gaya baru akan diterapkan pada konversi berikutnya.

**T: Apakah memungkinkan menggunakan file CSS eksternal dengan Aspose.HTML untuk Java?**  
J: Ya – Anda dapat menautkan stylesheet eksternal di HTML atau memuat isinya dan memberikannya ke `setUserStyleSheet`.

**T: Bagaimana Aspose.HTML menangani properti CSS yang tidak didukung?**  
J: Properti yang tidak didukung diabaikan, sehingga sisanya tetap dapat dirender tanpa error.

**T: Bisakah saya mengonversi HTML ke format selain PDF?**  
J: Ya, Aspose.HTML mendukung konversi ke XPS, TIFF, PNG, JPEG, dan lainnya menggunakan kelas `SaveOptions` yang sesuai.

## Kesimpulan
Anda kini telah melihat cara **membuat PDF dari HTML** dengan mengatur stylesheet pengguna khusus menggunakan Aspose.HTML untuk Java. Alur kerja ini memberi Anda kontrol penuh atas tampilan visual PDF yang dihasilkan, menjadikannya ideal untuk pembuatan laporan otomatis, pembuatan faktur, atau skenario apa pun di mana konsistensi gaya sangat penting. Jangan ragu untuk bereksperimen dengan CSS yang lebih kompleks, font eksternal, atau format konversi tambahan untuk memperluas fondasi ini.

---

**Terakhir Diperbarui:** 2026-02-04  
**Diuji Dengan:** Aspose.HTML untuk Java 24.11 (terbaru pada saat penulisan)  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}