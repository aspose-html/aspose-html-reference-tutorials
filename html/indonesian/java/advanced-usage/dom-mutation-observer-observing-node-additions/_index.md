---
title: Pengamat Mutasi DOM dengan Aspose.HTML untuk Java
linktitle: Pengamat Mutasi DOM - Mengamati Penambahan Node
second_title: Pemrosesan HTML Java dengan Aspose.HTML
description: Pelajari cara menggunakan Aspose.HTML untuk Java guna menerapkan DOM Mutation Observer dalam panduan langkah demi langkah ini. Pantau dan tanggapi perubahan DOM secara efektif.
weight: 11
url: /id/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pengamat Mutasi DOM dengan Aspose.HTML untuk Java


Apakah Anda seorang pengembang Java yang ingin mengamati dan bereaksi terhadap perubahan dalam Document Object Model (DOM) dari sebuah dokumen HTML? Aspose.HTML untuk Java menyediakan solusi yang ampuh untuk tugas ini. Dalam panduan langkah demi langkah ini, kita akan menjelajahi cara menggunakan Aspose.HTML untuk Java untuk membuat dokumen HTML dan mengamati penambahan node dengan Mutation Observer. Tutorial ini akan memandu Anda melalui prosesnya, dengan membagi setiap contoh menjadi beberapa langkah. Pada akhirnya, Anda akan dapat mengimplementasikan DOM Mutation Observer dalam proyek Java Anda dengan mudah.

## Prasyarat

Sebelum kita mulai menggunakan Aspose.HTML untuk Java, mari pastikan Anda memiliki prasyarat yang diperlukan:

1. Lingkungan Pengembangan Java: Pastikan Anda telah menginstal Java Development Kit (JDK) di sistem Anda.

2.  Aspose.HTML untuk Java: Anda perlu mengunduh dan menginstal Aspose.HTML untuk Java. Anda dapat menemukan tautan unduhannya[Di Sini](https://releases.aspose.com/html/java/).

3. IDE (Integrated Development Environment): Gunakan IDE Java pilihan Anda, seperti IntelliJ IDEA atau Eclipse, untuk menulis dan menjalankan kode Java.

## Paket Impor

Untuk memulai Aspose.HTML untuk Java, Anda perlu mengimpor paket yang diperlukan ke dalam kode Java Anda. Berikut cara melakukannya:

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

Sekarang setelah Anda mengimpor paket yang diperlukan, mari beralih ke panduan langkah demi langkah untuk mengimplementasikan DOM Mutation Observer di Java.

## Langkah 1: Buat Instansi Pengamat Mutasi

Pertama, Anda perlu membuat instance Mutation Observer. Observer ini akan mengamati perubahan dalam DOM dan menjalankan fungsi callback saat terjadi mutasi.

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

Pada langkah ini, kami membuat pengamat dengan fungsi panggilan balik yang mencetak pesan saat node ditambahkan ke DOM.

## Langkah 2: Konfigurasikan Observer

Sekarang, mari konfigurasikan pengamat dengan opsi yang diinginkan. Kita ingin mengamati perubahan daftar anak dan perubahan sub-pohon, serta perubahan pada data karakter.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// Lewatkan node target untuk diamati dengan konfigurasi yang ditentukan
observer.observe(document.getBody(), config);
```

 Di sini, kami mengatur`config` objek untuk memungkinkan pengamatan perubahan daftar anak, sub pohon, dan data karakter. Kami kemudian meneruskan simpul target (dalam hal ini, dokumen`<body>`) dan konfigurasi kepada pengamat.

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

## Langkah 4: Tunggu Observasi (Asynchronous)

Karena mutasi diamati secara tidak sinkron, kita perlu menunggu beberapa saat agar pengamat dapat menangkap perubahannya. Kita akan menggunakan`synchronized` Dan`wait` untuk tujuan ini, seperti ditunjukkan di bawah ini.

```java
// Karena mutasi bekerja dalam mode async, tunggu beberapa detik
synchronized (this) {
    wait(5000);
}
```

Di sini, kita menunggu selama 5 detik untuk memastikan pengamat memiliki kesempatan menangkap mutasi apa pun.

## Langkah 5: Berhenti Mengamati

Akhirnya, ketika Anda selesai mengamati, penting untuk melepaskan pengamat untuk melepaskan sumber daya.

```java
// Berhenti mengamati
observer.disconnect();
```

Dengan langkah ini, Anda telah menyelesaikan pengamatan dan dapat membersihkan sumber daya.

## Kesimpulan

Dalam tutorial ini, kami telah membahas proses penggunaan Aspose.HTML untuk Java guna mengimplementasikan DOM Mutation Observer. Anda telah mempelajari cara membuat observer, mengonfigurasinya, membuat perubahan pada DOM, menunggu observasi, dan menghentikan observasi. Kini, Anda memiliki keterampilan untuk menerapkan DOM Mutation Observer dalam proyek Java Anda guna memantau dan bereaksi terhadap perubahan DOM dokumen HTML secara efektif.

Jika Anda memiliki pertanyaan atau mengalami masalah, jangan ragu untuk mencari bantuan di[Forum Aspose.HTML](https://forum.aspose.com/) Selain itu, Anda dapat mengakses[dokumentasi](https://reference.aspose.com/html/java/) untuk informasi terperinci tentang Aspose.HTML untuk Java.

## Pertanyaan yang Sering Diajukan

### Q1: Apa itu DOM Mutation Observer?

A1: DOM Mutation Observer adalah fitur JavaScript yang memungkinkan Anda mengamati perubahan pada Document Object Model (DOM) dari dokumen HTML. Fitur ini menyediakan cara untuk bereaksi terhadap penambahan, penghapusan, atau modifikasi node DOM secara real-time.

### Q2: Dapatkah saya menggunakan Aspose.HTML untuk Java dalam proyek komersial saya?

 A2: Ya, Anda dapat menggunakan Aspose.HTML untuk Java dalam proyek komersial. Anda dapat menemukan informasi lisensi dan pembelian[Di Sini](https://purchase.aspose.com/buy).

### Q3: Apakah ada uji coba gratis yang tersedia untuk Aspose.HTML untuk Java?

 A3: Ya, Anda bisa mendapatkan uji coba gratis Aspose.HTML untuk Java[Di Sini](https://releases.aspose.com/)Ini memungkinkan Anda menjelajahi fitur dan kemampuannya sebelum melakukan pembelian.

### Q4: Apa manfaat mengamati perubahan data karakter dengan Mutation Observer?

A4: Mengamati perubahan data karakter berguna untuk skenario saat Anda ingin memantau dan bereaksi terhadap perubahan konten teks elemen HTML. Misalnya, Anda dapat menggunakannya untuk melacak dan merespons masukan pengguna dalam formulir web.

### Q5: Bagaimana cara membuang sumber daya saat menggunakan Aspose.HTML untuk Java?

 A5: Penting untuk melepaskan sumber daya saat Anda selesai. Dalam contoh kami, kami menggunakan`document.dispose()` untuk membersihkan sumber daya yang terkait dengan dokumen HTML. Pastikan untuk membuang semua objek dan sumber daya yang Anda buat untuk menghindari kebocoran memori.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
