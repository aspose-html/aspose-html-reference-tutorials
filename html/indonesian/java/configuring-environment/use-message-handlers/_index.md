---
title: Menggunakan Penanganan Pesan di Aspose.HTML untuk Java
linktitle: Menggunakan Penanganan Pesan di Aspose.HTML untuk Java
second_title: Pemrosesan HTML Java dengan Aspose.HTML
description: Pelajari cara menggunakan penanganan pesan di Aspose.HTML untuk Java untuk menangani gambar yang hilang dan operasi jaringan lainnya secara efektif.
weight: 12
url: /id/java/configuring-environment/use-message-handlers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menggunakan Penanganan Pesan di Aspose.HTML untuk Java

## Perkenalan
Dalam tutorial ini, kami akan memandu Anda melalui contoh praktis penggunaan pengendali pesan di Aspose.HTML untuk Java. Kami akan menyiapkan dokumen HTML sederhana yang merujuk pada gambar yang hilang dan menunjukkan cara menemukan dan menangani kesalahan menggunakan pengendali pesan kustom. Baik Anda baru mengenal Aspose.HTML atau ingin mengembangkan keterampilan Anda, panduan ini akan memberi Anda wawasan yang Anda butuhkan untuk mengelola operasi jaringan secara efektif.
## Prasyarat
Sebelum kita menyelami panduan langkah demi langkah, mari pastikan Anda memiliki semua yang Anda butuhkan:
1.  Java Development Kit (JDK): Pastikan Anda telah menginstal JDK di sistem Anda. Anda dapat mengunduhnya dari[Situs web Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
2.  Aspose.HTML untuk Java: Anda harus menginstal Aspose.HTML untuk Java. Anda dapat mengunduhnya dari[Aspose merilis halaman](https://releases.aspose.com/html/java/).
3. IDE: Gunakan Lingkungan Pengembangan Terpadu (IDE) Java favorit Anda seperti IntelliJ IDEA, Eclipse, atau NetBeans.
4. Pengetahuan Dasar Java: Keakraban dengan pemrograman Java sangat penting untuk mengikuti tutorial ini secara efektif.
5.  Lisensi Sementara: Jika Anda menggunakan versi uji coba Aspose.HTML, pertimbangkan untuk mendapatkan lisensi sementara.[lisensi sementara](https://purchase.aspose.com/temporary-license/) untuk menghindari keterbatasan apa pun selama pengembangan.

## Paket Impor
Sebelum memulai, pastikan Anda telah mengimpor paket-paket yang diperlukan ke dalam proyek Java Anda. Berikut ini adalah impor penting yang Anda perlukan:
```java
import java.io.IOException;
```
Impor ini akan memberi Anda akses ke kelas dan metode yang diperlukan untuk menangani operasi jaringan, membuat dokumen HTML, dan melakukan konversi HTML ke PNG.

## Langkah 1: Siapkan Kode HTML
Hal pertama yang kita perlukan adalah kode HTML sederhana yang merujuk ke berkas gambar. Kita akan secara sengaja merujuk ke gambar yang tidak ada untuk memicu mekanisme penanganan kesalahan.
```java
String code = "<img src='missing.jpg'>";
```
 Potongan kode ini membuat elemen HTML yang mencoba memuat gambar bernama`missing.jpg`Karena berkas gambar ini tidak ada, maka akan terjadi kesalahan selama proses pemuatan dokumen.
## Langkah 2: Tulis Kode HTML ke File
Berikutnya, kita perlu menulis kode HTML ini ke sebuah berkas yang dapat kita muat nanti.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
 Di sini, kami menggunakan`FileWriter` untuk menulis kode HTML kita ke file bernama`document.html`Berkas ini akan digunakan untuk membuat dokumen HTML pada langkah-langkah berikut.
## Langkah 3: Buat Penanganan Pesan Kustom
Sekarang, mari buat penangan pesan khusus untuk menangani skenario gambar yang hilang. Penangan pesan akan memeriksa kode status respons dan mencetak pesan jika berkas tidak ditemukan.
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
 Dalam penanganan ini,`invoke` metode memeriksa kode status respons operasi jaringan. Jika kode status bukan 200 (yang menunjukkan keberhasilan), ia mencetak pesan yang menunjukkan bahwa berkas tidak ditemukan.`invoke(context);` baris memastikan bahwa penangan berikutnya dalam rantai dipanggil.
## Langkah 4: Konfigurasikan Layanan Jaringan
 Untuk menggunakan pengendali pesan kustom, kita perlu menambahkannya ke rangkaian pengendali pesan yang ada di layanan jaringan. Hal ini dilakukan melalui`Configuration` kelas.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Di sini, kita membuat sebuah instance dari`Configuration` dan mengambil kembali`INetworkService`. Kemudian, kami menambahkan pengendali kustom kami ke daftar pengendali pesan. Pengaturan ini memastikan bahwa pengendali kami dipanggil selama operasi jaringan.
## Langkah 5: Muat Dokumen HTML
Setelah konfigurasi selesai, kita sekarang dapat memuat dokumen HTML kita. Dokumen tersebut akan mencoba memuat gambar yang hilang, yang memicu pengendali pesan kustom kita.
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Operasi tambahan akan dilakukan di sini
} finally {
    if (document != null) {
        document.dispose();
    }
}
```
Potongan kode ini memuat dokumen HTML menggunakan konfigurasi yang telah kita siapkan sebelumnya. Proses pemuatan dokumen akan mencoba memuat gambar yang hilang, dan pengendali pesan kita akan menangkap dan menangani kesalahan yang dihasilkan.
## Langkah 6: Ubah HTML ke PNG
Sebagai penutup, mari kita ubah dokumen HTML menjadi gambar PNG. Langkah ini tidak sepenuhnya diperlukan untuk menangani gambar yang hilang, tetapi ini menunjukkan fungsionalitas Aspose.HTML yang lebih luas.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
 Di sini, kami menggunakan`Converter.convertHTML` metode untuk mengubah dokumen HTML menjadi file PNG.`ImageSaveOptions`memungkinkan kita menentukan opsi untuk menyimpan gambar, seperti resolusi dan format.
## Langkah 7: Bersihkan Sumber Daya
 Terakhir, selalu pastikan Anda membersihkan sumber daya apa pun yang digunakan selama proses berlangsung. Ini termasuk membuang`Configuration` Dan`HTMLDocument` objek.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Ini memastikan bahwa semua sumber daya dibebaskan, mencegah kebocoran memori dan masalah potensial lainnya dalam aplikasi Anda.

## Kesimpulan
Nah, itu dia—panduan lengkap tentang penggunaan pengendali pesan di Aspose.HTML untuk Java! Kami telah membahas proses menyiapkan dokumen HTML, membuat pengendali pesan khusus, dan menangani sumber daya yang hilang seperti seorang profesional. Baik Anda menangani gambar yang hilang, tautan rusak, atau masalah terkait jaringan lainnya, pendekatan ini akan memberi Anda kendali yang Anda perlukan untuk mengelolanya secara efektif di aplikasi Java Anda.

## Tanya Jawab Umum
### Apa itu Aspose.HTML untuk Java?
Aspose.HTML untuk Java adalah pustaka hebat yang memungkinkan pengembang untuk membuat, memanipulasi, dan mengonversi dokumen HTML dalam aplikasi Java.
### Mengapa menggunakan penanganan pesan di Aspose.HTML untuk Java?
Penanganan pesan memungkinkan Anda untuk menyadap dan mengelola operasi jaringan, seperti menangani sumber daya yang hilang atau mengubah permintaan dan respons.
### Dapatkah saya menggunakan beberapa penanganan pesan dalam satu konfigurasi?
Ya, Anda dapat menggabungkan beberapa penangan pesan bersama-sama untuk menangani berbagai skenario selama operasi jaringan.
### Apakah perlu membuang objek Konfigurasi dan HTMLDocument?
Ya, membuang objek-objek ini memastikan semua sumber daya dilepaskan dengan benar, mencegah kebocoran memori.
### Bisakah saya menangani jenis kesalahan lain dengan penanganan pesan?
Tentu saja! Penanganan pesan dapat disesuaikan untuk menangani berbagai jenis kesalahan, bukan hanya sumber daya yang hilang.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
