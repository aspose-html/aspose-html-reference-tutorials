---
category: general
date: 2026-02-22
description: Java'da HTML'den PDF'ye dönüşümü verimli bir şekilde toplu işlemek için
  sabit bir iş parçacığı havuzu oluşturun. HTML'yi hızlıca PDF olarak kaydeden bir
  iş parçacığı havuzu Java örneğini öğrenin.
draft: false
keywords:
- create fixed thread pool
- convert html to pdf
- batch html to pdf
- thread pool java example
- save html as pdf
language: tr
og_description: HTML'den PDF'ye toplu dönüşüm için sabit bir iş parçacığı havuzu oluşturun.
  Bu rehber, HTML'yi verimli bir şekilde PDF olarak kaydeden bir iş parçacığı havuzu
  Java örneği üzerinden sizi yönlendirir.
og_title: Toplu HTML'den PDF'ye Dönüştürme için Sabit İş Parçacığı Havuzu Oluştur
tags:
- Java
- Concurrency
- PDF Generation
title: Toplu HTML'den PDF'ye Dönüşüm İçin Sabit İş Parçacığı Havuzu Oluştur
url: /tr/java/conversion-html-to-other-formats/create-fixed-thread-pool-for-batch-html-to-pdf-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sabit İş Parçacığı Havuzu Oluşturma: Toplu HTML'den PDF'ye Dönüştürme

Hiç **sabit iş parçacığı havuzu oluşturmanın** bir yığın HTML dosyasını CPU'nuzu zorlamadan PDF'ye dönüştürdüğünü merak ettiniz mi? Tek başınıza değilsiniz. İşlenecek onlarca—hatta yüzlerce—sayfanız olduğunda, bunları tek tek çalıştırmak zahmetli olur, ancak sınırsız bir iş parçacığı havuzunu çalıştırmak hafızayı hızla tüketebilir.  

Bu öğreticide bu ikilemi, **toplu HTML'den PDF'ye** dönüştüren, her sonucu kaydeden ve sorunsuz bir şekilde kapanan bir **thread pool Java örneği** göstererek çözeceğiz. Sonunda **HTML'yi PDF'ye dönüştürmeyi** paralel olarak yapabilecek ve sabit bir iş parçacığı havuzunun çoğu toplu iş için neden ideal olduğunu anlayacaksınız.

## Öğrenecekleriniz

- Sabit bir iş parçacığı havuzu oluşturan tam, çalıştırılabilir bir Java programı.
- Her satırın **neden** yapıldığını açıklayan adım‑adım açıklama.
- Bir PDF kütüphanesi seçimi konusunda rehberlik (kod parçacıkları aramadan **HTML'yi PDF olarak kaydedebilmeniz** için).
- Hata yönetimi, havuz boyutunu ayarlama ve çözümü daha büyük toplulara genişletme ipuçları.

**Önkoşullar** – Java 8+ yüklü, temel bir IDE (IntelliJ, Eclipse veya VS Code), ve sınıf yolunuzda bir PDF dönüşüm kütüphanesi (örnekte *OpenHTMLtoPDF* kullanacağız). Başka bir çerçeveye ihtiyaç yok.

---

## Sabit İş Parçacığı Havuzu Oluşturma – Neden Önemli

**Sabit iş parçacığı havuzu oluşturduğunuzda**, JVM'e aynı anda çalışabilecek çalışan iş parçacığı sayısını tam olarak söylersiniz. Bu, iş parçacığı oluşturma fırtınalarını önler, bellek kullanımını öngörülebilir tutar ve işletim sisteminin işi verimli bir şekilde zamanlamasını sağlar.  

Bunu bir marketteki kasiyer kuyruğuna benzetin: Belirli sayıda kasa açarsınız, müşteriler sıraya girer ve kuyruk kaybolduğunda kasaları kapatırsınız. `FixedThreadPool` da aynı şekilde çalışır—görevler sıraya girer, ancak ekstra iş parçacıkları anlık olarak oluşturulmaz.

```java
// Step 1: Build a fixed‑size thread pool with 4 workers
ExecutorService threadPool = Executors.newFixedThreadPool(4);
```

`4` sayısı, dört çekirdekli bir dizüstü bilgisayar için iyi bir başlangıç noktasıdır; CPU çekirdek sayınıza ve I/O özelliklerinize göre ayarlayabilirsiniz.

## Toplu HTML'den PDF'ye: Her Sayfayı Dönüştürme

Artık havuz var, **HTML'yi PDF'ye dönüştüren** görevleri ona beslememiz gerekiyor. Her görev şunları yapacak:

1. Diskten bir HTML belgesi yükleyecek.
2. PDF kütüphanesine teslim edecek.
3. Oluşan PDF'yi aynı dizine geri yazacak.

İş I/O‑ağır (dosya okuma, PDF yazma) olduğundan, küçük bir havuz genellikle diskin beklemesinden dolayı boşta duran büyük bir havuzdan daha iyi performans gösterir.

```java
// Step 2: Submit a conversion job for every HTML file you have
for (int i = 0; i < 4; i++) {
    final int pageIndex = i;               // capture loop variable for the lambda
    threadPool.submit(() -> {
        // Load the HTML file
        Path htmlPath = Paths.get("YOUR_DIRECTORY/page" + pageIndex + ".html");
        String html = Files.readString(htmlPath, StandardCharsets.UTF_8);

        // Convert and save as PDF
        Path pdfPath = Paths.get("YOUR_DIRECTORY/page" + pageIndex + ".pdf");
        convertHtmlToPdf(html, pdfPath);
    });
}
```

> **Pro ipucu:** Dörtten fazla sayfanız varsa, döngü sınırını artırın ya da dosya listesini dinamik olarak okuyun—`Files.list(Paths.get("YOUR_DIRECTORY")).filter(p -> p.toString().endsWith(".html"))` bunu zahmetsiz hâle getirir.

## Thread Pool Java Örneği Açıklaması

**thread pool Java örneğini** satır satır inceleyelim; böylece sadece kodu kopyalamak yerine akışı gerçekten anlayacaksınız.

| Satır | Ne Yapar | Neden Önemlidir |
|------|--------------|--------------------|
| `ExecutorService threadPool = Executors.newFixedThreadPool(4);` | Tam dört iş parçacığıyla bir havuz oluşturur. | Sınırlı sayıda eşzamanlı dönüşüm garantiler, bellek taşması hatalarını önler. |
| `for (int i = 0; i < 4; i++) { … }` | İşlemek istediğiniz sayfalar üzerinde döner. | Döngü görev oluşturmayı tetikler; statik sınırı dinamik bir listeyle değiştirebilirsiniz. |
| `final int pageIndex = i;` | Lambda içinde kullanılmak üzere döngü indeksini yakalar. | `final` (veya etkili final) olmadan lambda değişen bir değişken görür, dosya adları hatalı olur. |
| `threadPool.submit(() -> { … });` | Bir `Runnable`ı havuza asenkron çalıştırma için gönderir. | Havuz, runnable'ı boş bir çalışan iş parçacığına planlar, ana iş parçacığını yeni işler eklemeye devam eder. |
| `Files.readString(htmlPath, …);` | HTML dosyasını bir `String`e okur. | Çoğu PDF kütüphanesi HTML'yi string ya da akış olarak kabul eder. |
| `convertHtmlToPdf(html, pdfPath);` | Gerçek dönüşümü yapan yardımcı yöntemi çağırır. | Lambda'yı temiz tutar ve kütüphane‑özel kodunu izole eder. |

Aşağıda **OpenHTMLtoPDF** kullanan tam yardımcı yöntem yer alıyor; bu hafif kütüphane **HTML'yi PDF olarak kaydetmek** için tek bir çağrı yeterli.

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

private static void convertHtmlToPdf(String html, Path outputPdf) throws IOException {
    try (OutputStream os = Files.newOutputStream(outputPdf)) {
        PdfRendererBuilder builder = new PdfRendererBuilder();
        builder.withHtmlContent(html, null);     // base URI is null because we use absolute paths
        builder.toStream(os);
        builder.run();                           // blocks until PDF is written
    } catch (Exception e) {
        // Wrap any checked exception as an unchecked one so the lambda can compile
        throw new RuntimeException("Failed to convert HTML to PDF for " + outputPdf, e);
    }
}
```

> **Neden OpenHTMLtoPDF?** Saf Java, yerel bağımlılık yok ve CSS'yi destekler; bu sayede ortaya çıkan PDF'ler orijinal web sayfalarına çok benzer. iText ya da Flying Saucer tercih ederseniz, sadece `convertHtmlToPdf` içindeki uygulamayı değiştirin.

## HTML'yi PDF Olarak Kaydet – Kütüphane Seçimi

“Hangi kütüphane ile **HTML'yi PDF'ye dönüştürmeliyim**?” diye sorabilirsiniz. İşte hızlı bir karşılaştırma:

| Kütüphane | Maven Koordinatları | Artılar | Eksiler |
|---------|-------------------|------|------|
| OpenHTMLtoPDF | `com.openhtmltopdf:openhtmltopdf-pdfbox:1.0.10` | Saf Java, iyi CSS desteği, hafif | Sınırlı gelişmiş PDF özellikleri (ör. şifreleme) |
| iText 7 + html2pdf | `com.itextpdf:html2pdf:3.0.6` | Zengin özellik seti, ticari destek | Birçok kullanım senaryosu için ücretli lisans gerekir |
| Flying Saucer | `org.xhtmlrenderer:flying-saucer-pdf:9.1.22` | Olgun, eski Java sürümleriyle çalışır | Büyük belgelerde yavaş, CSS kapsamı daha az |

Projenizin ihtiyaçlarına uygun olanı seçin. **Toplu HTML'den PDF'ye** bir iş için, OpenHTMLtoPDF genellikle ideal: hızlı, basit ve ücretsiz.

## Zarif Kapatma ve Hata Yönetimi

Executor'ı çalışır durumda bırakmak JVM'inizin kapanmasını engelleyebilir ve bir iş parçacığındaki yakalanmamış istisnalar fark edilmesi zor olabilir. Aşağıdaki desen düzenli bir kapatmayı garanti eder:

```java
// Step 5: Initiate an orderly shutdown after all tasks are queued
threadPool.shutdown();                     // No new tasks accepted
try {
    // Wait up to 60 seconds for existing tasks to finish
    if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
        threadPool.shutdownNow();          // Force shutdown if tasks linger
    }
} catch (InterruptedException ex) {
    threadPool.shutdownNow();              // Preserve interrupt status
    Thread.currentThread().interrupt();
}
```

- `shutdown()` havuza mevcut işi bitirmesini söyler ancak yeni işleri reddeder.
- `awaitTermination` her şey bitene ya da zaman aşımına kadar bekler.
- `shutdownNow()` çalışan görevleri iptal etmeye çalışır—zorunlu durdurma için faydalıdır.

Herhangi bir dönüşüm başarısız olursa, fırlattığımız `RuntimeException` executor'a yayılır ve varsayılan olarak konsola kaydedilir. Üretimde, `afterExecute` yöntemi geçersiz kılınmış özel bir `ThreadPoolExecutor` ekleyerek hataları bir dosyaya ya da izleme sistemine kaydedebilirsiniz.

## Tam Çalışan Örnek

Her şeyi bir araya getirdiğimizde, `src/main/java/com/example/BatchPdfConverter.java` içine kopyalayıp yapıştırabileceğiniz bağımsız bir Java sınıfı elde edersiniz. OpenHTMLtoPDF bağımlılığının sınıf yolunuzda olduğundan emin olun.

```java
package com.example;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;
import java.util.concurrent.*;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;

/**
 * Demonstrates how to create a fixed thread pool to batch HTML to PDF conversion.
 * Adjust POOL_SIZE and DIRECTORY constants to fit your environment.
 */
public class BatchPdfConverter {

    private static final int POOL_SIZE = 4;                     // Number of parallel workers
    private static final Path DIRECTORY = Paths.get("YOUR_DIRECTORY"); // Change to your folder

    public static void main(String[] args) {
        ExecutorService threadPool = Executors.newFixedThreadPool(POOL_SIZE);

        // Discover all *.html files in the target directory
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(DIRECTORY, "*.html")) {
            for (Path htmlPath : stream) {
                threadPool.submit(() -> processFile(htmlPath));
            }
        } catch (IOException e) {
            System.err.println("Failed to list HTML files: " + e.getMessage());
        }

        // Graceful shutdown
        thread

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}