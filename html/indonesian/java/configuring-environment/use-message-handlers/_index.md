---
date: 2026-05-04
description: Pelajari cara melakukan konversi HTML ke PNG, menyadap permintaan jaringan
  Java, dan menangani tautan rusak Java menggunakan Aspose.HTML untuk Java.
keywords:
- html to png conversion
- intercept network requests java
- html to image conversion
- load html document java
- handle broken links java
linktitle: Gunakan Penangan Pesan di Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Konversi HTML ke PNG dengan Handler Pesan Aspose.HTML di Java
url: /id/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konversi HTML ke PNG dengan Penangan Pesan Aspose.HTML di Java

## Pendahuluan tentang Konversi HTML ke PNG
Dalam tutorial ini Anda akan menemukan **cara mengonversi HTML ke PNG** sambil menangani sumber daya yang hilang secara elegan menggunakan Aspose.HTML untuk Java. Kami akan memandu Anda membuat halaman HTML kecil yang mengarah ke gambar yang tidak ada, menyambungkan **custom message handler** untuk **menyadap permintaan jaringan**, mengonfigurasi **network service**, memuat dokumen, dan akhirnya melakukan **html to image conversion**. Pada akhir tutorial Anda akan memiliki pola yang solid untuk **handle broken links java** dan output PNG berkualitas tinggi—sempurna untuk laporan, thumbnail, atau pratinjau email.

## Jawaban Cepat
- **Apa yang dilakukan penangan pesan?** Ia menyadap operasi jaringan (seperti permintaan gambar) dan memungkinkan Anda merespons kode status seperti 404.  
- **Apakah Aspose.HTML dapat mengonversi HTML ke PNG?** Ya—`Converter.convertHTML` melakukan konversi dalam satu panggilan.  
- **Apakah saya memerlukan lisensi untuk contoh ini?** Lisensi sementara menghapus batas evaluasi; lisensi permanen diperlukan untuk penggunaan produksi.  
- **Versi Java mana yang bekerja?** Semua JDK 8+ (contoh berjalan pada JDK 11).  
- **Bisakah saya mengonfigurasi layanan jaringan?** Tentu—gunakan `configuration.getService(INetworkService.class)` untuk menambahkan penangan Anda.

## Apa Itu Konversi HTML ke PNG?
Konversi HTML ke PNG merender halaman web (atau fragmen HTML) menjadi gambar raster. Ini berguna ketika Anda memerlukan pratinjau statis dari konten dinamis, menghasilkan thumbnail untuk buletin email, atau mengarsipkan halaman web sebagai gambar.

## Mengapa Menggunakan Penangan Pesan untuk Menyadap Permintaan Jaringan di Java?
Penangan pesan memberi Anda **kontrol halus** atas setiap permintaan jaringan—baik itu gambar, CSS, JavaScript, atau file font. Dengan menyadap permintaan ini Anda dapat **mencatat aset yang hilang**, menyediakan konten cadangan, atau bahkan mencoba kembali unduhan yang gagal, menjadikan pipeline pemrosesan HTML Anda **tangguh** dan **siap produksi**.

## Prasyarat
1. **Java Development Kit (JDK)** – unduh dari [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – dapatkan perpustakaan dari [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse, atau NetBeans works fine.  
4. **Basic Java knowledge** – Anda harus nyaman dengan kelas, try‑with‑resources, dan penanganan pengecualian.  
5. **Temporary License** – jika Anda berada dalam masa percobaan, dapatkan [temporary license](https://purchase.aspose.com/temporary-license/) untuk menghindari watermark.

## Impor Paket
Pertama, tarik kelas Java I/O yang akan kita perlukan untuk penanganan file. Sisanya kelas Aspose direferensikan dengan nama lengkap nanti, menjaga daftar impor tetap rapi.

```java
import java.io.IOException;
```

## Langkah 1: Siapkan Kode HTML
Kami membuat potongan HTML minimal yang sengaja merujuk ke gambar yang tidak ada. Ini akan memicu penangan kami ketika mesin mencoba mengambil sumber daya tersebut.

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

## Langkah 3: Tulis Penangan Pesan Kustom
Sekarang kami membangun **custom message handler** yang memeriksa status HTTP setiap permintaan jaringan. Jika respons bukan `200`, kami mencatat peringatan yang ramah. Perhatikan pemanggilan `invoke(context);` di akhir—ini meneruskan permintaan ke penangan berikutnya dalam rantai, mencegah rekursi.

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
Agar Aspose.HTML menyadari penangan kami, kami mengambil **network service** dari instance `Configuration` dan menambahkan penangan ke koleksinya. Ini adalah langkah di mana kami **configure network service** untuk perilaku khusus.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Langkah 5: Muat Dokumen HTML
Dengan konfigurasi siap, kami memuat *document.html*. Mesin kini menggunakan layanan jaringan kami, sehingga permintaan gambar yang hilang disadap oleh penangan yang baru saja kami tambahkan.

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
Berikut inti dari proses **html to image conversion**. Metode `Converter.convertHTML` menerima `HTMLDocument` yang telah dimuat, `ImageSaveOptions` opsional (di mana Anda dapat menyesuaikan DPI atau kualitas), dan nama file output.

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

## Masalah Umum dan Solusinya
- **Handler recursion** – Panggil `invoke(context);` hanya sekali untuk menghindari loop tak terbatas.  
- **Missing license** – Tanpa lisensi yang valid PNG output akan berisi watermark.  
- **Incorrect file paths** – Gunakan jalur absolut atau atur direktori kerja dengan benar saat memuat `document.html`.  
- **Unsupported resource types** – Pastikan sumber daya yang ingin Anda sadap (gambar, CSS, dll.) memang diminta oleh mesin HTML.

## Pertanyaan yang Sering Diajukan

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

---

**Terakhir Diperbarui:** 2026-05-04  
**Diuji Dengan:** Aspose.HTML for Java 24.11  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}