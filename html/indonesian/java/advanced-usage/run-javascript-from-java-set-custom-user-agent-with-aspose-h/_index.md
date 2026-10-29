---
category: general
date: 2026-04-26
description: Jalankan JavaScript dari Java menggunakan Aspose.HTML dan pelajari cara
  mengatur user-agent khusus untuk jendela peramban yang disimulasikan.
draft: false
keywords:
- run javascript from java
- set custom user-agent
- how to set user-agent
- configure window settings
- simulate browser java
language: id
og_description: Jalankan JavaScript dari Java dengan Aspose.HTML. Pelajari cara mengatur
  user-agent khusus dan mengonfigurasi pengaturan jendela untuk browser simulasi.
og_title: Jalankan JavaScript dari Java – Atur User-Agent Kustom
tags:
- Java
- Aspose.HTML
- JavaScript Execution
title: Jalankan JavaScript dari Java – Atur User-Agent Kustom dengan Aspose.HTML
url: /id/java/advanced-usage/run-javascript-from-java-set-custom-user-agent-with-aspose-h/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jalankan JavaScript dari Java – Atur User-Agent Kustom dengan Aspose.HTML

Pernah membutuhkan untuk **menjalankan JavaScript dari Java** sambil berpura-pura menjadi browser sungguhan? Mungkin Anda sedang melakukan scraping pada situs yang memblokir agen tidak dikenal, atau Anda hanya ingin menguji skrip tanpa membuka Chrome. Dalam tutorial ini kami akan menunjukkan secara tepat cara melakukannya, dan kami juga akan membahas **cara mengatur user-agent** sehingga server remote mengira Anda menggunakan browser desktop biasa.

Kami akan menggunakan library Aspose.HTML, yang memberikan Java lingkungan ringan mirip browser tanpa tampilan (head‑less). Pada akhir panduan ini Anda akan dapat mengeksekusi potongan JavaScript apa pun, mengonfigurasi pengaturan jendela, dan **simulate browser Java** behavior dengan string user‑agent kustom. Tanpa browser eksternal, tanpa Selenium, hanya kode Java murni.

## Apa yang Anda Butuhkan

- **Java 17** (atau JDK terbaru; API berfungsi pada Java 8+)
- **Aspose.HTML for Java** 23.9 (atau versi terbaru pada saat penulisan)
- IDE yang layak (IntelliJ IDEA, Eclipse, VS Code—pilihan Anda)
- Familiaritas dasar dengan konsep Java dan JavaScript

Jika Anda sudah memiliki semuanya, bagus—langsung saja ke kode. Jika belum, unduh JAR Aspose.HTML dari situs resmi dan tambahkan ke classpath proyek Anda; library sudah menyertakan semua dependensi, jadi Anda tidak memerlukan apa pun lagi.

> **Pro tip:** Saat Anda menambahkan JAR ke proyek Maven, gunakan koordinat berikut:  
> ```xml
> <dependency>
>     <groupId>com.aspose</groupId>
>     <artifactId>aspose-html</artifactId>
>     <version>23.9</version>
> </dependency>
> ```

---

## ## Menjalankan JavaScript dari Java: Ide Inti

Pada intinya, kelas `Window` milik Aspose.HTML meniru jendela browser. Anda dapat memberi HTML, CSS, dan JavaScript kepadanya, lalu meminta untuk mengevaluasi skrip dan mengembalikan hasilnya. Anggap saja ini seperti Chrome kecil yang hidup di dalam JVM Anda, tetapi tanpa UI.

Berikut adalah program lengkap yang siap dijalankan yang menunjukkan seluruh alur:

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class JsEngineExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create window settings and define a custom User‑Agent string
        WindowSettings windowSettings = new WindowSettings();
        windowSettings.setUserAgent(
            "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"
        );

        // Step 2: Open a browser‑like window using the configured settings
        try (Window browserWindow = new Window(windowSettings)) {

            // Step 3: Execute JavaScript that reads the navigator.userAgent property
            browserWindow.evaluateScript("var ua = navigator.userAgent; ua;");

            // Step 4: Retrieve the script result (the custom User‑Agent) and display it
            String userAgent = (String) browserWindow.getLastResult();
            System.out.println("Custom user‑agent: " + userAgent);
        }
    }
}
```

**Output yang diharapkan**

```
Custom user‑agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36
```

Menjalankan program ini membuktikan tiga hal sekaligus:

1. Anda **menjalankan JavaScript dari Java** (`evaluateScript`).
2. Anda **mengatur user-agent kustom** (`setUserAgent` pada `WindowSettings`).
3. Anda **mengonfigurasi pengaturan jendela** untuk mensimulasikan lingkungan browser nyata.

---

## ## Mengonfigurasi Pengaturan Jendela untuk Browser Realistis

Mengapa repot-repot dengan `WindowSettings`? Sebagian besar layanan web memeriksa header `User‑Agent` untuk memutuskan apakah akan menyajikan konten mobile, desktop, atau khusus bot. Jika Anda menghilangkan string yang realistis, Anda mungkin mendapatkan versi halaman yang dipangkas, atau bahkan diblokir total.

### Rincian Langkah‑per‑Langkah

| Langkah | Apa yang kami lakukan | Mengapa penting |
|------|------------|----------------|
| **Create `WindowSettings`** | `new WindowSettings()` | Memberikan kami wadah untuk semua opsi mirip browser. |
| **Set the user‑agent** | `windowSettings.setUserAgent("…")` | Meniru klien Chrome/Edge/Firefox, menghindari deteksi bot. |
| **Pass settings to `Window`** | `new Window(windowSettings)` | Jendela kini mewarisi konfigurasi kustom kami. |

Anda juga dapat menyesuaikan properti lain, seperti `setLocale`, `setScreenWidth`, atau `setScreenHeight`, untuk lebih **simulate browser Java** kondisi. Misalnya, mengatur lebar layar 1920 px membuat situs responsif mengira Anda berada di monitor desktop.

```java
windowSettings.setScreenWidth(1920);
windowSettings.setScreenHeight(1080);
```

---

## ## Mengatur User-Agent Kustom: Variasi Umum

Tidak ada satu string user‑agent yang cocok untuk semua. Tergantung pada situs target, Anda mungkin memerlukan:

- **Chrome di Windows** (contoh di atas)
- **Safari di macOS**  
  ```java
  windowSettings.setUserAgent(
      "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) " +
      "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.1 Safari/605.1.15"
  );
  ```
- **Chrome Mobile**  
  ```java
  windowSettings.setUserAgent(
      "Mozilla/5.0 (Linux; Android 11; Pixel 5) " +
      "AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.71 Mobile Safari/537.36"
  );
  ```

Ketika **how to set user-agent** menjadi pertanyaan, jawabannya sederhana: “panggil `setUserAgent` dengan string tepat yang Anda inginkan.” Tidak ada header tambahan, tidak ada manipulasi tingkat jaringan. Library menangani semuanya di balik layar.

---

## ## Simulate Browser Java: Lebih Dari Sekadar User-Agent

Jika Anda ingin **simulate browser java** secara lebih mendalam—misalnya Anda membutuhkan cookie, local storage, atau bahkan objek `navigator` kustom—Aspose.HTML menawarkan beberapa pengaturan tambahan:

```java
// Enable cookies
windowSettings.setCookiePolicy(CookiePolicy.ACCEPT_ALL);

// Pre‑populate local storage
browserWindow.getLocalStorage().setItem("token", "abc123");

// Override navigator.platform if needed
browserWindow.evaluateScript(
    "Object.defineProperty(navigator, 'platform', { get: () => 'Win32' });"
);
```

Potongan kode ini menggambarkan bagaimana Anda dapat membentuk lingkungan agar cocok dengan hampir semua skenario browser nyata. Perlu diingat bahwa setiap fitur tambahan dapat meningkatkan penggunaan memori, tetapi untuk sebagian besar tugas otomatisasi beban tambahan ini dapat diabaikan.

---

## ## Kesalahan Umum dan Cara Menghindarinya

1. **Lupa menutup `Window`** – Blok `try‑with‑resources` dalam contoh memastikan jendela dibuang. Jika Anda menginstansiasi secara manual, selalu panggil `browserWindow.close()` dalam klausa `finally`.
2. **Menggunakan user‑agent yang usang** – Situs web memperbarui logika deteksi mereka secara sering. Secara berkala perbarui string dari dev tools browser nyata (Network → Headers → User‑Agent).
3. **Menjalankan skrip yang bergantung pada DOM** – `evaluateScript` berfungsi baik untuk JavaScript murni, tetapi jika Anda membutuhkan dokumen HTML lengkap, muat dulu:  
   ```java
   browserWindow.navigate("about:blank");
   browserWindow.getDocument().write("<html><body></body></html>");
   ```
4. **Keamanan thread** – Setiap instance `Window` terikat pada thread yang membuatnya. Jangan bagikan jendela yang sama di beberapa thread; sebaliknya, buat yang baru per thread.

---

## ## Verifikasi Hasil – Tes Cepat

Setelah Anda mengompilasi dan menjalankan program, Anda harus melihat user‑agent kustom tercetak di konsol. Untuk memastikan bahwa library benar‑benar mengirim header, Anda dapat mengarahkan jendela ke layanan echo sederhana:

```java
browserWindow.navigate("https://httpbin.org/user-agent");
browserWindow.evaluateScript("document.body.textContent;");
String echoed = (String) browserWindow.getLastResult();
System.out.println("Echoed from server: " + echoed);
```

Output akan berisi string yang sama yang Anda setel sebelumnya, mengonfirmasi bahwa langkah **configure window settings** berhasil dari awal hingga akhir.

---

## ## Contoh Kerja Lengkap (Semua Langkah Digabungkan)

Berikut adalah kelas Java akhir yang berdiri sendiri yang dapat Anda salin‑tempel ke IDE mana pun:

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class JsEngineFullDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create and configure window settings
        WindowSettings settings = new WindowSettings();
        settings.setUserAgent(
            "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"
        );
        settings.setScreenWidth(1920);
        settings.setScreenHeight(1080);
        settings.setCookiePolicy(CookiePolicy.ACCEPT_ALL);

        // 2️⃣ Open the headless window
        try (Window win = new Window(settings)) {

            // 3️⃣ Run a simple script that returns navigator.userAgent
            win.evaluateScript("var ua = navigator.userAgent; ua;");
            String ua = (String) win.getLastResult();
            System.out.println("Custom user‑agent: " + ua);

            // 4️⃣ Optional: Verify via an external service
            win.navigate("https://httpbin.org/user-agent");
            win.evaluateScript("document.body.textContent;");
            String echoed = (String) win.getLastResult();
            System.out.println("Echoed from server: " + echoed);
        }
    }
}
```

Jalankan, perhatikan konsol, dan Anda telah berhasil **menjalankan JavaScript dari Java**, mengatur **user-agent kustom**, dan **mengonfigurasi pengaturan jendela** untuk mensimulasikan browser nyata—tanpa meninggalkan JVM.

---

## ## Ilustrasi Gambar

![Contoh menjalankan JavaScript dari Java dengan user-agent kustom](https://example.com/images/run-js-from-java.png "Contoh menjalankan JavaScript dari Java dengan user-agent kustom")

*Diagram menunjukkan alur: Java → Aspose.HTML `Window` → Eksekusi JavaScript → Hasil.*

---

## ## Langkah Selanjutnya dan Topik Terkait

- **Manipulasi DOM lanjutan** – Muat halaman HTML lengkap dan gunakan `document.querySelector` di dalam `evaluateScript`.
- **Pengujian headless** – Gabungkan Aspose.HTML dengan JUnit untuk memverifikasi hasil JavaScript secara otomatis.
- **Dukungan proxy** – Jika situs target memblokir IP Anda, konfigurasikan `WindowSettings.setProxy` untuk mengarahkan lalu lintas melalui server proxy.
- **Pengoptimalan kinerja** – Untuk operasi massal, gunakan kembali satu instance `Window` dan hanya bersihkan dokumennya di antara eksekusi.

Setiap topik ini dibangun di atas fondasi yang telah kami buat di sini: **run javascript from java**, **set custom user-agent**, dan **configure window settings**. Selami dokumentasi Aspose.HTML untuk cakupan API yang lebih mendalam, atau bereksperimen dengan potongan kode di atas untuk menyesuaikan dengan kasus penggunaan Anda.

---

## ## Kesimpulan

Kami telah melewati contoh lengkap yang dapat dijalankan yang menunjukkan cara **menjalankan JavaScript dari Java**, mengatur user‑agent kustom, dan sepenuhnya **mengonfigurasi pengaturan jendela** untuk **simulate browser java**. Pendekatannya ringan

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}