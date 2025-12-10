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

## Introduction
Dalam tutorial ini, **how to use aspose** untuk menangani sumber daya yang hilang dalam HTML ditunjukkan langkah demi langkah. Kami akan membuat dokumen HTML sederhana yang merujuk ke gambar yang tidak ada, melampirkan message handler khusus, dan menunjukkan cara **load html document java** sambil menangani tautan yang rusak dengan elegan. Pada akhir tutorial, Anda juga akan melihat cara **convert html to png** menggunakan Aspose.HTML, memberikan gambaran lengkap tentang konversi HTML‑ke‑gambar di Java.

## Quick Answers
- **Apa tujuan utama dari sebuah message handler?** Untuk menyela operasi jaringan dan merespons kode status seperti sumber daya yang hilang.  
- **Apakah Aspose.HTML dapat mengonversi HTML ke PNG?** Ya, dengan menggunakan `Converter.convertHTML` Anda dapat melakukan konversi html ke gambar.  
- **Apakah saya memerlukan lisensi untuk contoh ini?** Lisensi sementara menghapus batas evaluasi; lisensi permanen diperlukan untuk produksi.  
- **Versi Java mana yang didukung?** Semua JDK 8+ (tutorial ini menggunakan JDK 11).  
- **Apakah memungkinkan menangani beberapa tautan yang rusak?** Tentu – Anda dapat menambahkan beberapa handler untuk mengelola berbagai skenario.

## Prerequisites
Sebelum kita masuk ke panduan langkah demi langkah, pastikan Anda memiliki semua yang diperlukan:
1. Java Development Kit (JDK): Pastikan JDK terpasang di sistem Anda. Anda dapat mengunduhnya dari [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).
2. Aspose.HTML for Java: Anda perlu menginstal Aspose.HTML for Java. Unduh dari [Aspose releases page](https://releases.aspose.com/html/java/).
3. IDE: Gunakan Integrated Development Environment (IDE) Java favorit Anda seperti IntelliJ IDEA, Eclipse, atau NetBeans.
4. Pengetahuan Dasar tentang Java: Familiaritas dengan pemrograman Java penting untuk mengikuti tutorial ini dengan efektif.
5. Lisensi Sementara: Jika Anda menggunakan versi percobaan Aspose.HTML, pertimbangkan untuk memperoleh [temporary license](https://purchase.aspose.com/temporary-license/) agar tidak ada batasan selama pengembangan.

## Import Packages
Sebelum memulai, pastikan paket-paket yang diperlukan telah diimpor ke dalam proyek Java Anda. Berikut adalah impor penting yang Anda perlukan:
```java
import java.io.IOException;
```
Impor ini memberikan akses ke kelas dan metode yang diperlukan untuk menangani operasi jaringan, membuat dokumen HTML, dan melakukan konversi HTML‑ke‑PNG.

## Step 1: Prepare the HTML Code
Hal pertama yang kita butuhkan adalah potongan HTML sederhana yang merujuk ke file gambar. Kami akan sengaja merujuk ke gambar yang tidak ada untuk memicu mekanisme penanganan error.
```java
String code = "<img src='missing.jpg'>";
```
Kode ini membuat tag `<img>` yang mengarah ke `missing.jpg`. Karena gambar tidak ada, layanan jaringan akan mengembalikan kode status non‑200, yang akan ditangkap oleh handler khusus kami.

## Step 2: Write the HTML Code to a File
Selanjutnya, kita perlu menyimpan potongan HTML agar Aspose.HTML dapat memuatnya sebagai dokumen.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
Dengan menggunakan `FileWriter` kami menyimpan HTML ke **document.html**. File ini menjadi sumber untuk langkah **load html document java** nanti.

## Step 3: Create a Custom Message Handler
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

## Step 4: Configure the Network Service
Agar Aspose.HTML menyadari handler kami, kami mendaftarkannya ke layanan jaringan melalui kelas `Configuration`.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Di sini kami membuat instance `Configuration`, mengambil `INetworkService`, dan menambahkan handler khusus kami ke koleksinya. Ini memastikan handler dijalankan selama setiap permintaan jaringan, seperti memuat gambar.

## Step 5: Load the HTML Document
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

## Step 6: Convert HTML to PNG
Untuk memperlihatkan kemampuan lebih luas Aspose.HTML, kami akan mengonversi dokumen yang dimuat ke gambar PNG. Ini adalah skenario klasik **convert html to png**.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` menerima `HTMLDocument`, opsional `ImageSaveOptions` (di mana Anda dapat mengatur DPI, kualitas, dll.), dan nama file output. Hasilnya adalah gambar raster dari HTML yang dirender.

## Step 7: Clean Up Resources
Manajemen sumber daya yang tepat penting dalam setiap aplikasi Java. Kami membuang (`dispose`) baik `Configuration` maupun `HTMLDocument` untuk menghindari kebocoran memori.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Membungkus pembersihan dalam blok `finally` menjamin eksekusi bahkan jika terjadi pengecualian sebelumnya.

## Why Use Message Handlers?
Message handler memberi Anda kontrol halus atas operasi jaringan seperti **handle broken links java**. Daripada membiarkan perpustakaan gagal secara diam-diam, Anda dapat mencatat, mencoba kembali, mengganti sumber daya, atau menyediakan konten fallback—menjadikan pemrosesan HTML Anda kuat dan siap produksi.

## Common Issues and Solutions
- **Handler recursion** – Pastikan Anda memanggil `invoke(context);` hanya sekali untuk menghindari loop tak berujung.  
- **Missing license** – Tanpa lisensi yang valid, konversi dapat menghasilkan gambar ber watermark.  
- **File path errors** – Gunakan jalur absolut atau atur direktori kerja dengan benar saat memuat `document.html`.

## Frequently Asked Questions

**Q: Can I chain multiple message handlers?**  
A: Yes, you can add several handlers to the `network.getMessageHandlers()` collection; they will be executed in the order added.

**Q: Does the handler work for CSS or script resources as well?**  
A: Absolutely—any network request made by the HTML engine (images, CSS, JS, fonts) passes through the handler.

**Q: How do I change the HTTP request before it’s sent?**  
A: Implement a handler that modifies `context.getRequest()` before calling `invoke(context)`.

**Q: Is there a way to suppress the warning for specific URLs?**  
A: Inside the handler, inspect `context.getRequest().getRequestUri()` and conditionally skip the log.

**Q: What version of Aspose.HTML is required for these APIs?**  
A: The code works with Aspose.HTML for Java 22.10 and later.

## Conclusion
Dan itulah panduan komprehensif tentang **how to use aspose** message handlers di Java. Kami telah membahas cara membuat file HTML, menghubungkan handler khusus untuk **handle broken links java**, memuat dokumen, dan melakukan **convert html to png**. Dengan pola ini Anda dapat dengan percaya diri mengelola sumber daya yang hilang, menerapkan kebijakan khusus, dan memperluas kemampuan jaringan Aspose.HTML dalam aplikasi Java apa pun.

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.HTML for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}