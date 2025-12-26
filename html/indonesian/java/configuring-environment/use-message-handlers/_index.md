---
date: 2025-12-10
description: Pelajari cara menggunakan Aspose untuk menangani tautan rusak di Java,
  mengonversi HTML ke PNG, dan memuat dokumen HTML Java dengan Aspose.HTML untuk Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Cara Menggunakan Penangan Pesan Aspose.HTML di Java
url: /id/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Aspose.HTML Message Handlers di Java

## Perkenalan
Dalam tutorial ini, **cara menggunakan aspose** untuk menangani sumber daya yang hilang dalam HTML ditunjukkan langkah demi langkah. Kami akan membuat dokumen HTML sederhana yang Merujuk ke gambar yang tidak ada, melampirkan message handler khusus, dan menunjukkan cara **load html document java** sambil menangani tautan yang rusak dengan elegan. Pada akhir tutorial, Anda juga akan melihat cara **convert html to png** menggunakan Aspose.HTML, memberikan gambaran lengkap tentang konversi HTML‑ke‑gambar di Java.

## Jawaban Cepat
- **Apa tujuan utama dari sebuah message handler?** Untuk menyela operasi jaringan dan merespons kode status seperti sumber daya yang hilang.
- **Apakah Aspose.HTML dapat mengonversi HTML ke PNG?** Ya, dengan menggunakan `Converter.convertHTML` Anda dapat melakukan konversi html ke gambar.
- **Apakah saya memerlukan lisensi untuk contoh ini?** Lisensi sementara menghapus batas evaluasi; lisensi permanen diperlukan untuk produksi.
- **Versi Java mana yang didukung?** Semua JDK 8+ (tutorial ini menggunakan JDK11).
- **Apakah memungkinkan menangani beberapa tautan yang rusak?** Tentu – Anda dapat menambahkan beberapa handler untuk mengelola berbagai skenario.

## Prasyarat
Sebelum kita masuk ke panduan langkah demi langkah, pastikan Anda memiliki semua yang diperlukan:
1. Java Development Kit (JDK): Pastikan JDK terpasang di sistem Anda. Anda dapat mengunduhnya dari [situs web Oracle](https://www.Oracle.com/java/technologies/javase-downloads.html).
2. Aspose.HTML for Java: Anda perlu menginstal Aspose.HTML for Java. Unduh dari [Halaman rilis Aspose](https://releases.aspose.com/html/java/).
3. IDE: Gunakan Integrated Development Environment (IDE) Java favorit Anda seperti IntelliJ IDEA, Eclipse, atau NetBeans.
4. Pengetahuan Dasar tentang Java: Familiaritas dengan pemrograman Java penting untuk mengikuti tutorial ini dengan efektif.
5. Lisensi Sementara: Jika Anda menggunakan versi percobaan Aspose.HTML, pertimbangkan untuk memperoleh [lisensi sementara](https://purchase.aspose.com/temporary-license/) agar tidak ada batasan selama pengembangan.

## Impor Paket
Sebelum memulai, pastikan paket-paket yang diperlukan telah diimpor ke dalam proyek Java Anda. Berikut adalah impor penting yang Anda perlukan:
```java
import java.io.IOException;
```
Impor ini memberikan akses ke kelas dan metode yang diperlukan untuk menangani operasi jaringan, membuat dokumen HTML, dan melakukan konversi HTML‑ke‑PNG.

## Langkah 1: Siapkan Kode HTML
Hal pertama yang kita butuhkan adalah potongan HTML sederhana yang merujuk ke file gambar. Kami akan sengaja merujuk ke gambar yang tidak ada untuk memicu mekanisme penanganan error.
```java
String code = "<img src='missing.jpg'>";
```
Kode ini membuat tag `<img>` yang mengarah ke `missing.jpg`. Karena gambar tidak ada, layanan jaringan akan mengembalikan kode status non‑200, yang akan ditangkap oleh handler khusus kami.

## Langkah 2: Tulis Kode HTML ke dalam File
Selanjutnya, kita perlu menyimpan potongan HTML agar Aspose.HTML dapat memuatnya sebagai dokumen.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
Dengan menggunakan `FileWriter` kami menyimpan HTML ke **document.html**. File ini menjadi sumber untuk langkah **load html document java** nanti.

## Langkah 3: Membuat Penanganan Pesan Kustom
Sekarang mari buat message handler khusus yang bereaksi ketika gambar tidak dapat ditemukan. Handler memeriksa kode status HTTP dan mencetak pesan yang ramah.
```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```
Metode `invoke` memeriksa `context.getResponse().getStatusCode()`. Jika bukan **200**, kami menampilkan peringatan jelas bahwa file tidak ditemukan. Panggilan `invoke(context);` terakhir meneruskan kontrol ke handler berikutnya dalam rantai.

## Langkah 4: Konfigurasi Layanan Jaringan
Agar Aspose.HTML menyadari handler kami, kami mendaftarkannya ke layanan jaringan melalui kelas `Configuration`.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Di sini kami membuat instance `Configuration`, mengambil `INetworkService`, dan menambahkan handler khusus kami ke koleksinya. Ini memastikan handler dijalankan selama setiap permintaan jaringan, seperti memuat gambar.

## Langkah 5: Muat Dokumen HTML
Dengan konfigurasi siap, kita kini dapat memuat file HTML yang telah dibuat sebelumnya. Langkah ini mendemonstrasikan **load html document java** sementara gambar yang hilang memicu handler kami.
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```
Konstruktor `HTMLDocument` menerima baik jalur file maupun `configuration` khusus. Ketika dokumen mem-parsing tag `<img>`, layanan jaringan mencoba mengambil `missing.jpg`, menerima 404, dan handler kami mencetak peringatan.

## Langkah 6: Konversi HTML ke PNG
Untuk memperlihatkan kemampuan lebih luas Aspose.HTML, kami akan mengonversi dokumen yang dimuat ke gambar PNG. Ini adalah skenario klasik **convert html to png**.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` menerima `HTMLDocument`, opsional `ImageSaveOptions` (di mana Anda dapat mengatur DPI, kualitas, dll.), dan nama file output. Hasilnya adalah gambar raster dari HTML yang dirender.

## Langkah 7: Bersihkan Sumber Daya
Manajemen sumber daya yang tepat penting dalam setiap aplikasi Java. Kami membuang (`dispose`) baik `Configuration` maupun `HTMLDocument` untuk menghindari kebocoran memori.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Membungkus pembersihan dalam blok `finally` menjamin eksekusi bahkan jika terjadi pengecualian sebelumnya.

## Mengapa Menggunakan Penangan Pesan?
Pengendali pesan memberi Anda kontrol halus atas operasi jaringan seperti **menangani tautan rusak java**. Daripada membiarkan perpustakaan gagal secara diam-diam, Anda dapat mencatat, mencoba kembali, mengganti sumber daya, atau menyediakan konten fallback—menjadikan pemrosesan HTML Anda kuat dan siap produksi.

## Masalah Umum dan Solusinya
- **Handler recursion** – Pastikan Anda memanggil `invoke(context);` hanya sekali untuk menghindari loop tak berujung.
- **Lisensi hilang** – Tanpa lisensi yang valid, konversi dapat menghasilkan gambar ber watermark.
- **Kesalahan jalur file** – Gunakan jalur absolut atau atur direktori kerja dengan benar saat memuat `document.html`.

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya merangkai beberapa penangan pesan?**
A: Ya, Anda dapat menambahkan beberapa penangan ke koleksi `network.getMessageHandlers()`; mereka akan dieksekusi dalam urutan yang ditambahkan.

**T: Apakah handler ini juga berfungsi untuk sumber daya CSS atau skrip?**
J: Tentu saja—setiap permintaan jaringan yang dibuat oleh mesin HTML (gambar, CSS, JS, font) akan melewati handler ini.

**T: Bagaimana cara mengubah permintaan HTTP sebelum dikirim?**
J: Implementasikan handler yang memodifikasi `context.getRequest()` sebelum memanggil `invoke(context)`.

**T: Apakah ada cara untuk menekan peringatan untuk URL tertentu?**
J: Di dalam handler, periksa `context.getRequest().getRequestUri()` dan lewati log secara kondisional.

**T: Versi Aspose.HTML apa yang dibutuhkan untuk API ini?**
J: Kode ini berfungsi dengan Aspose.HTML untuk Java 22.10 dan yang lebih baru.

## Kesimpulan
Dan itulah panduan komprehensif tentang **cara menggunakan handler pesan Aspose** di Java. Kami telah membahas cara membuat file HTML, menghubungkan handler khusus untuk **menangani tautan rusak java**, memuat dokumen, dan melakukan **convert html to png**. Dengan pola ini Anda dapat percaya diri mengelola sumber daya yang hilang, menerapkan kebijakan khusus, dan memperluas kemampuan jaringan Aspose.HTML dalam aplikasi Java apa pun.

---

**Terakhir Diperbarui:** 10-12-2025
**Diuji Dengan:** Aspose.HTML untuk Java 24.11
**Penulis:** Beranggapan 

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}