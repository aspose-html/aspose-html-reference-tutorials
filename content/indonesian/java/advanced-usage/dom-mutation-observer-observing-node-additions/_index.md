---
title: Pengamat Mutasi DOM dengan Aspose.HTML untuk Java
linktitle: Pengamat Mutasi DOM - Mengamati Penambahan Node
second_title: Pemrosesan Java HTML dengan Aspose.HTML
description: Pelajari cara menggunakan Aspose.HTML untuk Java untuk mengimplementasikan DOM Mutation Observer dalam panduan langkah demi langkah ini. Pantau dan tanggapi perubahan DOM secara efektif.
type: docs
weight: 11
url: /id/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

Apakah Anda seorang pengembang Java yang ingin mengamati dan bereaksi terhadap perubahan Model Objek Dokumen (DOM) dokumen HTML? Aspose.HTML untuk Java memberikan solusi ampuh untuk tugas ini. Dalam panduan langkah demi langkah ini, kita akan mempelajari cara menggunakan Aspose.HTML untuk Java untuk membuat dokumen HTML dan mengamati penambahan node dengan Mutation Observer. Tutorial ini akan memandu Anda melalui prosesnya, membagi setiap contoh menjadi beberapa langkah. Pada akhirnya, Anda akan dapat mengimplementasikan DOM Mutation Observers di proyek Java Anda dengan mudah.

## Prasyarat

Sebelum kita mendalami penggunaan Aspose.HTML untuk Java, pastikan Anda memiliki prasyarat yang diperlukan:

1. Lingkungan Pengembangan Java: Pastikan Anda telah menginstal Java Development Kit (JDK) di sistem Anda.

2.  Aspose.HTML untuk Java: Anda perlu mengunduh dan menginstal Aspose.HTML untuk Java. Anda dapat menemukan tautan unduhan[Di Sini](https://releases.aspose.com/html/java/).

3. IDE (Lingkungan Pengembangan Terpadu): Gunakan IDE Java pilihan Anda, seperti IntelliJ IDEA atau Eclipse, untuk menulis dan menjalankan kode Java.

## Paket Impor

Untuk memulai Aspose.HTML untuk Java, Anda perlu mengimpor paket yang diperlukan ke dalam kode Java Anda. Inilah cara Anda melakukannya:

```java
// Impor paket yang diperlukan
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

// Buat dokumen HTML kosong
HTMLDocument document = new HTMLDocument();
```

Sekarang Anda telah mengimpor paket yang diperlukan, mari beralih ke panduan langkah demi langkah untuk mengimplementasikan DOM Mutation Observer di Java.

## Langkah 1: Buat Instance Pengamat Mutasi

Pertama, Anda perlu membuat instance Mutation Observer. Pengamat ini akan mengamati perubahan di DOM dan menjalankan fungsi panggilan balik ketika terjadi mutasi.

```java
MutationObserver observer = new MutationObserver(new MutationCallback() {
    @Override
    public void invoke(IGenericList<MutationRecord> mutations, MutationObserver mutationObserver) {
        mutations.forEach(mutationRecord -> {
            mutationRecord.getAddedNodes().forEach(node -> {
                synchronized (this) {
                    System.out.println("The '" + node + "' node was added to the document.");
                    notifyAll();
                }
            });
        });
    }
});
```

Pada langkah ini, kita membuat pengamat dengan fungsi panggilan balik yang mencetak pesan ketika node ditambahkan ke DOM.

## Langkah 2: Konfigurasikan Pengamat

Sekarang, mari konfigurasikan pengamat dengan opsi yang diinginkan. Kami ingin mengamati perubahan daftar anak dan perubahan subpohon, serta perubahan pada data karakter.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// Lewati node target untuk diamati dengan konfigurasi yang ditentukan
observer.observe(document.getBody(), config);
```

 Di sini, kami mengaturnya`config` objek untuk memungkinkan mengamati perubahan data daftar anak, subpohon, dan karakter. Kami kemudian meneruskan node target (dalam hal ini, dokumen`<body>`) dan konfigurasinya ke pengamat.

## Langkah 3: Ubah DOM

Sekarang, kita akan membuat beberapa perubahan pada DOM untuk memicu pengamat. Kita akan membuat elemen paragraf dan menambahkannya ke badan dokumen.

```java
// Buat elemen paragraf dan tambahkan ke badan dokumen
Element p = document.createElement("p");
document.getBody().appendChild(p);

// Buat teks dan tambahkan ke paragraf
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

Pada langkah ini, kita membuat elemen paragraf HTML dan menambahkannya ke badan dokumen. Kemudian, kita membuat simpul teks dengan konten "Halo Dunia" dan menambahkannya ke paragraf.

## Langkah 4: Tunggu Pengamatan (Asynchronous)

Karena mutasi diamati secara asinkron, kita perlu menunggu beberapa saat agar pengamat dapat menangkap perubahannya. Kami akan menggunakan`synchronized` Dan`wait` untuk tujuan ini, seperti yang ditunjukkan di bawah ini.

```java
// Karena mutasi bekerja dalam mode asinkron, tunggu beberapa detik
synchronized (this) {
    wait(5000);
}
```

Di sini, kami menunggu selama 5 detik untuk memastikan pengamat memiliki kesempatan untuk menangkap adanya mutasi.

## Langkah 5: Berhenti Mengamati

Terakhir, setelah Anda selesai mengamati, penting untuk memutuskan sambungan pengamat untuk melepaskan sumber daya.

```java
// Berhenti mengamati
observer.disconnect();
```

Dengan langkah ini, Anda telah menyelesaikan observasi dan dapat membersihkan sumber daya.

## Kesimpulan

Dalam tutorial ini, kita telah mempelajari proses penggunaan Aspose.HTML untuk Java untuk mengimplementasikan DOM Mutation Observer. Anda telah mempelajari cara membuat pengamat, mengonfigurasinya, membuat perubahan pada DOM, menunggu observasi, dan berhenti mengamati. Sekarang, Anda memiliki keterampilan untuk menerapkan Pengamat Mutasi DOM di proyek Java Anda untuk memantau dan bereaksi terhadap perubahan DOM dokumen HTML secara efektif.

Jika Anda memiliki pertanyaan atau mengalami masalah, jangan ragu untuk mencari bantuan di[Forum Aspose.HTML](https://forum.aspose.com/) . Selain itu, Anda dapat mengakses[dokumentasi](https://reference.aspose.com/html/java/) untuk informasi rinci tentang Aspose.HTML untuk Java.

## FAQ

### Q1: Apa itu Pengamat Mutasi DOM?

A1: Pengamat Mutasi DOM adalah fitur JavaScript yang memungkinkan Anda mengamati perubahan dalam Model Objek Dokumen (DOM) dokumen HTML. Ini memberikan cara untuk bereaksi terhadap penambahan, penghapusan, atau modifikasi node DOM secara real-time.

### Q2: Dapatkah saya menggunakan Aspose.HTML untuk Java dalam proyek komersial saya?

 A2: Ya, Anda dapat menggunakan Aspose.HTML untuk Java dalam proyek komersial. Anda dapat menemukan informasi perizinan dan pembelian[Di Sini](https://purchase.aspose.com/buy).

### Q3: Apakah tersedia uji coba gratis untuk Aspose.HTML untuk Java?

 A3: Ya, Anda bisa mendapatkan uji coba gratis Aspose.HTML untuk Java[Di Sini](https://releases.aspose.com/). Ini memungkinkan Anda menjelajahi fitur dan kemampuannya sebelum melakukan pembelian.

### Q4: Apa keuntungan mengamati perubahan data karakter dengan Mutation Observer?

A4: Mengamati perubahan data karakter berguna untuk skenario di mana Anda ingin memantau dan bereaksi terhadap perubahan konten teks elemen HTML. Misalnya, Anda bisa menggunakannya untuk melacak dan merespons masukan pengguna di formulir web.

### Q5: Bagaimana cara membuang sumber daya saat menggunakan Aspose.HTML untuk Java?

 A5: Penting untuk melepaskan sumber daya setelah selesai. Dalam contoh kami, kami menggunakan`document.dispose()` untuk membersihkan sumber daya yang terkait dengan dokumen HTML. Pastikan untuk membuang semua objek dan sumber daya yang Anda buat untuk menghindari kebocoran memori.