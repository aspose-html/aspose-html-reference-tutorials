---
date: 2026-02-10
description: Pelajari cara menggunakan Aspose untuk menangani tautan rusak di Java,
  mengonversi HTML ke PNG, dan memuat dokumen HTML Java dengan Aspose.HTML untuk Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Konversi HTML ke PNG dengan Penangan Pesan Aspose.HTML di Java
url: /id/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengonversi HTML ke PNG dengan Aspose.HTML Message Handlers di Java

## Pendahuluan
Dalam tutorial ini Anda akan menemukan **cara mengonversi HTML ke PNG** sambil menangani sumber daya yang hilang secara elegan menggunakan Aspose.HTML untuk Java. Kami akan memandu Anda membuat halaman HTML kecil yang merujuk ke gambar yang tidak ada, menyambungkan **custom message handler** untuk **mencegat permintaan jaringan**, mengonfigurasi **network service**, memuat dokumen, dan akhirnya melakukan **html to image conversion**. Pada akhir tutorial Anda akan memiliki pola yang solid untuk **handle broken links java** serta output PNG berkualitas tinggi—sempurna untuk laporan, thumbnail, atau pratinjau email.

## Jawaban Cepat
- **Apa yang dilakukan message handler?** Ia mencegat operasi jaringan (seperti permintaan gambar) dan memungkinkan Anda merespons kode status seperti 404.  
- **Apakah Aspose.HTML dapat mengonversi HTML ke PNG?** Ya—`Converter.convertHTML` melakukan konversi dalam satu panggilan.  
- **Apakah saya memerlukan lisensi untuk contoh ini?** Lisensi sementara menghapus batas evaluasi; lisensi permanen diperlukan untuk penggunaan produksi.  
- **Versi Java mana yang kompatibel?** Semua JDK 8+ (contoh berjalan pada JDK 11).  
- **Bisakah saya mengonfigurasi network service?** Tentu—gunakan `configuration.getService(INetworkService.class)` untuk menambahkan handler Anda.

## Prasyarat
Sebelum kita mulai, pastikan Anda telah menyiapkan hal‑hal berikut:

1. **Java Development Kit (JDK)** – unduh dari [situs Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – dapatkan perpustakaan dari [halaman rilis Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse, atau NetBeans dapat digunakan.  
4. **Pengetahuan dasar Java** – Anda harus nyaman dengan kelas, try‑with‑resources, dan penanganan pengecualian.  
5. **Lisensi Sementara** – jika Anda masih dalam masa percobaan, dapatkan [lisensi sementara](https://purchase.aspose.com/temporary-license/) untuk menghindari watermark.

## Impor Paket
Pertama, tarik kelas Java I/O yang akan kita gunakan untuk penanganan file. Sisanya kelas Aspose akan direferensikan dengan nama lengkap nanti, sehingga daftar impor tetap rapi.

```java
import java.io.IOException;
```

## Langkah 1: Siapkan Kode HTML
Kami membuat potongan HTML minimal yang secara sengaja merujuk ke gambar yang tidak ada. Ini akan memicu handler kami ketika mesin mencoba mengambil sumber daya tersebut.

```java
String code = "<img src='missing.jpg'>";
```

## Langkah 2: Tulis Kode HTML ke File
Selanjutnya, kami menyimpan potongan tersebut ke *document.html*. Menggunakan blok try‑with‑resources menjamin `FileWriter` ditutup dengan benar.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Langkah 3: Tulis Message Handler Kustom
Sekarang kami membangun **custom message handler** yang memeriksa status HTTP setiap permintaan jaringan. Jika respons bukan `200`, kami mencatat peringatan yang bersahabat. Perhatikan pemanggilan `invoke(context);` di akhir—ini meneruskan permintaan ke handler berikutnya dalam rantai, mencegah rekursi.

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

## Langkah 4: Konfigurasikan Layanan Jaringan
Agar Aspose.HTML menyadari handler kami, kami mengambil **network service** dari instance `Configuration` dan menambahkan handler ke koleksinya. Ini adalah langkah di mana kami **configure network service** untuk perilaku khusus.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Langkah 5: Muat Dokumen HTML
Dengan konfigurasi siap, kami memuat *document.html*. Mesin kini menggunakan network service kami, sehingga permintaan gambar yang hilang diintersep oleh handler yang baru saja kami tambahkan.

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

## Langkah 6: Konversi HTML ke PNG
Berikut inti proses **html to image conversion**. Metode `Converter.convertHTML` menerima `HTMLDocument` yang telah dimuat, opsional `ImageSaveOptions` (di mana Anda dapat menyesuaikan DPI atau kualitas), dan nama file output.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Langkah 7: Bersihkan Sumber Daya
Praktik Java yang baik menuntut kita melepaskan semua sumber daya native. Blok `finally` memastikan `Configuration` dibuang meskipun terjadi pengecualian.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Mengapa Menggunakan Message Handlers?
Message handlers memberi Anda **kontrol halus** atas setiap permintaan jaringan—baik itu gambar, CSS, JavaScript, atau file font. Alih‑alih membiarkan perpustakaan gagal secara diam‑diam, Anda dapat mencatat aset yang hilang, menyediakan konten fallback, atau bahkan mencoba kembali permintaan. Ini membuat pipeline pemrosesan HTML Anda **robust**, **siap produksi**, dan lebih mudah untuk debug.

## Masalah Umum dan Solusinya
- **Rekursi handler** – Panggil `invoke(context);` hanya sekali untuk menghindari loop tak berujung.  
- **Lisensi tidak ada** – Tanpa lisensi yang valid, PNG output akan berisi watermark.  
- **Path file tidak tepat** – Gunakan path absolut atau atur direktori kerja dengan benar saat memuat `document.html`.  
- **Tipe sumber daya tidak didukung** – Pastikan sumber daya yang ingin Anda intercept (gambar, CSS, dll.) memang diminta oleh mesin HTML.

## Pertanyaan yang Sering Diajukan

**T: Bisakah saya menambahkan beberapa message handler?**  
J: Ya, Anda dapat menambahkan beberapa handler ke koleksi `network.getMessageHandlers()`; mereka akan dieksekusi sesuai urutan penambahan.

**T: Apakah handler bekerja untuk sumber daya CSS atau script juga?**  
J: Tentu—setiap permintaan jaringan yang dibuat oleh mesin HTML (gambar, CSS, JS, font) melewati handler.

**T: Bagaimana cara mengubah permintaan HTTP sebelum dikirim?**  
J: Implementasikan handler yang memodifikasi `context.getRequest()` sebelum memanggil `invoke(context)`.

**T: Apakah ada cara menonaktifkan peringatan untuk URL tertentu?**  
J: Di dalam handler, periksa `context.getRequest().getRequestUri()` dan lewati pencatatan secara kondisional.

**T: Versi Aspose.HTML apa yang diperlukan untuk API ini?**  
J: Kode ini bekerja dengan Aspose.HTML for Java 22.10 ke atas.

## Kesimpulan
Anda kini memiliki contoh lengkap end‑to‑end tentang **cara mengonversi HTML ke PNG** sambil menggunakan **custom message handler** untuk **mencegat permintaan jaringan** dan **handle broken links java**. Dengan mengonfigurasi network service, memuat dokumen, dan memanggil konverter, Anda dapat secara andal menghasilkan thumbnail PNG atau screenshot halaman penuh dalam aplikasi Java apa pun.

---

**Terakhir Diperbarui:** 2026-02-10  
**Diuji Dengan:** Aspose.HTML for Java 24.11  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}