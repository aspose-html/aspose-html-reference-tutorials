---
category: general
date: 2026-04-12
description: Pelajari cara memblokir HTML di Java dengan membuat sandbox, membuka
  file HTML secara aman, dan mengambil judul halaman. Contoh kode langkah demi langkah.
draft: false
keywords:
- how to block html
- open html file sandbox
- retrieve html title java
og_description: Pelajari cara memblokir HTML di Java menggunakan sandbox Aspose.HTML,
  membuka file HTML dengan aman, dan mengekstrak judul.
og_title: Cara memblokir HTML di Java – Tutorial Lengkap
tags:
- Java
- Aspose.HTML
- Sandbox
- HTML Processing
title: Cara memblokir HTML di Java – Buat sandbox dan ambil judul
url: /id/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara memblokir HTML di Java – Tutorial Lengkap

Jika Anda pernah membutuhkan **how to block HTML** saat memproses halaman pihak ketiga dalam aplikasi Java, Anda pasti tahu rasa sakit dari panggilan jaringan yang tidak terduga dan eksekusi skrip. Dalam tutorial ini kami akan menunjukkan secara tepat cara membuat sandbox, **open HTML file sandbox** dengan aman, dan **retrieve HTML title Java** tanpa membiarkan sumber daya eksternal masuk. Langkah‑langkahnya singkat, kode siap dijalankan, dan Anda akan memahami mengapa setiap pengaturan penting.

## Jawaban Cepat
- **Bagaimana saya dapat memblokir HTML agar tidak memuat sumber daya eksternal?** Set `setEnableNetworkAccess(false)` di `SandboxOptions`.  
- **Library mana yang menangani sandboxing di Java?** Aspose.HTML for Java menyediakan kelas `Sandbox` bawaan.  
- **Apakah saya memerlukan Maven untuk menggunakan kode ini?** Tidak, cukup tambahkan JAR Aspose.HTML ke classpath Anda.  
- **Apakah saya masih dapat menjalankan JavaScript di dalam sandbox?** Ya, tetapi Anda harus mengaktifkannya secara eksplisit dan menangani izin jaringan.  
- **Apa output setelah menjalankan demo?** Dua baris: pesan keberhasilan dan judul halaman yang diambil dari tag `<title>`.

## Apa yang Akan Anda Dapatkan
Kami akan membahas semuanya mulai dari menyiapkan opsi sandbox hingga mencetak judul dokumen. Pada akhir tutorial Anda akan mengetahui:

* Mengapa sandbox penting saat memproses HTML pihak ketiga.  
* Cara mengonfigurasi dimensi layar dan menonaktifkan akses jaringan.  
* Kode Java tepat yang membuka file HTML di dalam sandbox.  
* Cara membaca tag title dengan aman, bahkan jika halaman mencoba memuat skrip eksternal.  

**Prasyarat?** Hanya JDK terbaru (8 atau lebih baru) dan pustaka Aspose.HTML untuk Java di classpath Anda. Tidak diperlukan Maven, tetapi jika Anda menggunakan Maven cukup tambahkan dependensi Aspose dan Anda siap.

## Cara memblokir HTML di Java? – Mengonfigurasi Lingkungan Sandbox

Sebelum kita dapat memuat dokumen apa pun, kita memerlukan sandbox yang meniru jendela peramban tetapi menolak berkomunikasi dengan dunia luar. Anggaplah sebagai halaman belakang yang dipagari di mana anak (HTML Anda) dapat bermain, namun pintunya terkunci.

```java
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;

// Step 1: Define sandbox options – screen size and network policy
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(1280);               // width in pixels
sandboxOptions.setScreenHeight(800);               // height in pixels
sandboxOptions.setEnableNetworkAccess(false);      // blocks all remote resources

// Pro tip: you can also set a custom user‑agent string here if needed.
```

**Mengapa ini penting:**  
Mengatur `setEnableNetworkAccess(false)` menjamin bahwa setiap `<script src="…">`, `<img src="…">`, atau impor CSS tidak akan mengakses internet. Inilah inti dari **how to block HTML**—Anda mendapatkan isolasi tanpa mengorbankan ketelitian rendering.

## Buka sandbox file HTML – Memuat Dokumen dengan Aman

Sekarang sandbox sudah siap, kita dapat menaruh file HTML ke dalamnya. Metode `Sandbox.open()` mengembalikan sebuah `HTMLDocument` yang berada sepenuhnya di dalam lingkungan yang dipagari.

```java
import com.aspose.html.HTMLDocument;

try (Sandbox sandbox = new Sandbox(sandboxOptions)) {
    // Step 2: Open the HTML file inside the sandbox
    // Replace YOUR_DIRECTORY/complex.html with the actual path to your file.
    HTMLDocument htmlDoc = sandbox.open("YOUR_DIRECTORY/complex.html");

    // At this point the document is parsed, but no network calls were made.
    System.out.println("Document loaded successfully inside sandbox.");
}
catch (Exception e) {
    // Handle errors such as file not found or parsing issues.
    System.err.println("Failed to open HTML file sandbox: " + e.getMessage());
}
```

**Pertanyaan umum:** *Bagaimana jika file tidak ada?*  
Blok `try‑with‑resources` secara otomatis menutup sandbox, dan klausa catch akan memberi Anda pesan kesalahan yang jelas. Anda juga dapat memvalidasi jalur terlebih dahulu dengan `Files.exists()` jika diinginkan.

## Ambil judul HTML Java – Ekstrak Tag `<title>`

Dengan dokumen yang dimuat dengan aman, mengambil judul halaman menjadi sangat mudah. Metode `HTMLDocument.getTitle()` membaca elemen `<title>` dari DOM, sepenuhnya tidak memperhatikan sumber daya eksternal yang diblokir.

```java
// Continuing inside the try block from Step 2
String pageTitle = htmlDoc.getTitle();
System.out.println("Title inside sandbox: " + pageTitle);
```

**Output yang diharapkan** (asumsi file HTML berisi `<title>My Complex Page</title>`):

```
Document loaded successfully inside sandbox.
Title inside sandbox: My Complex Page
```

Jika HTML tidak memiliki tag `<title>`, `getTitle()` hanya mengembalikan string kosong—tidak ada pengecualian yang dilempar. Ini membuat **retrieve HTML title Java** menjadi operasi aman bahkan pada halaman yang rusak.

## Contoh Lengkap yang Dapat Dijalankan

Menggabungkan semuanya, berikut adalah kelas Java mandiri yang dapat Anda kompilasi dan jalankan langsung. Ingat untuk mengganti `YOUR_DIRECTORY/complex.html` dengan jalur sebenarnya ke file uji Anda.

```java
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.HTMLDocument;

public class SandboxDemo {
    public static main(String[] args) {
        // 1️⃣ Configure sandbox options
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(1280);
        sandboxOptions.setScreenHeight(800);
        sandboxOptions.setEnableNetworkAccess(false); // blocks remote resources

        // 2️⃣ Create sandbox and open HTML file
        try (Sandbox sandbox = new Sandbox(sandboxOptions)) {
            HTMLDocument htmlDoc = sandbox.open("YOUR_DIRECTORY/complex.html");

            // 3️⃣ Retrieve and display the title
            String title = htmlDoc.getTitle();
            System.out.println("Title inside sandbox: " + title);
        } catch (Exception e) {
            System.err.println("Error during sandbox operation: " + e.getMessage());
        }
    }
}
```

**Menjalankan demo:**  

```bash
javac -cp "path/to/aspose-html.jar" SandboxDemo.java
java -cp ".:path/to/aspose-html.jar" SandboxDemo
```

Anda akan melihat output dua baris yang ditunjukkan sebelumnya, mengonfirmasi bahwa Anda berhasil **created sandbox for HTML**, **opened HTML file sandbox**, dan **retrieved HTML title Java**.

## Tips, Kasus Tepi, dan Praktik Terbaik

* **Beberapa halaman?** Jika Anda perlu memproses beberapa file HTML, gunakan kembali instance `Sandbox` yang sama—cukup panggil `open()` berulang kali. Sandbox tetap terisolasi untuk setiap panggilan.  
* **Konten dinamis?** Untuk halaman yang bergantung pada JavaScript untuk mengatur judul, Anda harus mengaktifkan eksekusi skrip (`sandboxOptions.setEnableScript(true)`). Ingatlah bahwa mengaktifkan skrip juga membuka pintu bagi panggilan jaringan, jadi Anda mungkin ingin memasukkan domain tertentu ke whitelist alih-alih menonaktifkan semua akses jaringan.  
* **File besar?** Sandbox menyimpan seluruh DOM di memori. Untuk dokumen yang sangat besar, pertimbangkan untuk melakukan streaming file dan mengekstrak `<title>` dengan parser ringan sebelum memuatnya ke dalam sandbox.  
* **Logging:** Aspose.HTML dapat menghasilkan log terperinci melalui `System.setProperty("aspose.html.logging", "true")`. Berguna saat menelusuri mengapa sumber daya tertentu diblokir.

## Pertanyaan yang Sering Diajukan

**T: Apakah saya dapat memblokir semua sumber daya eksternal sambil tetap mengizinkan skrip inline?**  
J: Ya. Pertahankan `setEnableNetworkAccess(false)` dan set `setEnableScript(true)` untuk mengizinkan JavaScript inline tetapi mencegah semua pengambilan jaringan.

**T: Apa yang terjadi jika HTML mencoba memuat file CSS dari internet?**  
J: Permintaan diblokir oleh sandbox, dan CSS hanya diabaikan, sehingga tata letak dokumen tetap berdasarkan gaya yang tersedia.

**T: Apakah sandbox thread‑safe?**  
J: Sebuah instance `Sandbox` tunggal tidak thread‑safe. Buat sandbox terpisah per thread atau sinkronkan akses jika Anda memerlukan pemrosesan bersamaan.

**T: Apakah saya memerlukan lisensi untuk Aspose.HTML dalam pengembangan?**  
J: Lisensi evaluasi gratis dapat digunakan untuk pengembangan dan pengujian. Lisensi komersial diperlukan untuk penerapan produksi.

**T: Bagaimana saya dapat menangkap kesalahan yang terjadi selama parsing?**  
J: Bungkus pemanggilan `sandbox.open()` dalam blok try‑catch seperti yang ditunjukkan; pesan pengecualian akan berisi detail parsing.

---

**Terakhir Diperbarui:** 2026-04-12  
**Diuji Dengan:** Aspose.HTML for Java 24.11  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}