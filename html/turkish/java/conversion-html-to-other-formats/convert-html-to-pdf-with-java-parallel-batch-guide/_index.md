---
category: general
date: 2026-06-07
description: Java'nın ExecutorService'ini kullanarak HTML'yi PDF'ye dönüştürün. HTML
  dosyalarını toplu olarak nasıl dönüştüreceğinizi, HTML belgesini PDF olarak nasıl
  kaydedeceğinizi ve ExecutorService'i sorunsuz bir şekilde nasıl kapatacağınızı öğrenin.
draft: false
keywords:
- convert html to pdf
- save html document as pdf
- shutdown executorservice gracefully
- batch convert html to pdf
language: tr
og_description: Java'nın ExecutorService'i kullanarak HTML'yi PDF'ye dönüştürün. Toplu
  dönüşümde uzmanlaşın, HTML belgesini PDF olarak kaydedin ve ExecutorService'in sorunsuz
  kapatılmasını sağlayın.
og_title: Java ile HTML'yi PDF'ye Dönüştür – Paralel Toplu Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  headline: Convert HTML to PDF with Java – Parallel Batch Guide
  type: TechArticle
- description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  name: Convert HTML to PDF with Java – Parallel Batch Guide
  steps:
  - name: The HTML file is read into a string.
    text: The HTML file is read into a string.
  - name: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
    text: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
  - name: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
    text: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
  type: HowTo
tags:
- Java
- Concurrency
- PDF Generation
title: Java ile HTML'yi PDF'ye Dönüştür – Paralel Toplu Kılavuz
url: /tr/java/conversion-html-to-other-formats/convert-html-to-pdf-with-java-parallel-batch-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java ile HTML'yi PDF'ye Dönüştür – Paralel Toplu Kılavuz

Hiç **convert HTML to PDF** yapmanız gerektiğinde ama onlarca dosyayla uğraşırken takılmış hissettiniz mi? Tek başınıza değilsiniz—birçok geliştirici rapor oluşturucular veya fatura dışa aktarıcıları geliştirirken bu duvara çarpıyor. İyi haber? Birkaç satır Java ve akıllı bir thread havuzu ile **batch convert HTML to PDF**'yi anında gerçekleştirebilir, **save HTML document as PDF** yapabilir ve iş bittiğinde **shutdown ExecutorService gracefully** yapabilirsiniz.

Bu öğreticide, eksiksiz, çalıştırmaya hazır bir örnek üzerinden adım adım ilerleyeceğiz. Sabit boyutlu bir thread havuzunun paralel dönüşüm için neden ideal olduğunu, dönüşüm kodunun nasıl göründüğünü ve executor'ı temiz bir şekilde sonlandırmak için gereken adımları göreceksiniz. Sonunda, herhangi bir projeye ekleyebileceğiniz, eksik parçası olmayan, belirsiz “see docs” bağlantıları içermeyen kendi içinde çalışan bir programınız olacak.

---

## Oluşturacağınız Şey

- Yerel HTML dosyalarının bir listesini okuyan bir Java konsol uygulaması.  
- Her dosya, PDF sürümünü oluşturan bir worker thread'e teslim edilir.  
- Uygulama, dönüşümleri paralel olarak çalıştırmak için **ExecutorService** kullanır.  
- Tüm görevler kuyruğa alındıktan sonra havuz **shutdown gracefully** yapılır, böylece hiçbir thread açık kalmaz.

**Prerequisites**  
- Java 17 (veya herhangi bir güncel JDK).  
- HTML'yi render edebilen bir PDF kütüphanesi, örneğin **OpenHTMLtoPDF**, **iText** veya **Flying Saucer**. Kodda bir yer tutucu `HTMLDocument` sınıfına referans vereceğiz; bunu kütüphanenizin API'siyle değiştirin.  
- Java eşzamanlılığı hakkında temel bilgi (karmaşık bir şey değil).

![ExecutorService kullanarak HTML dosyalarının toplu olarak PDF'ye dönüştürülmesini gösteren diyagram](batch-convert-diagram.png "ExecutorService ile paralel olarak HTML'yi PDF'ye dönüştür")

*Alt metin: Bir thread havuzu kullanarak HTML'yi PDF'ye dönüştürmenin toplu işleme nasıl yapıldığını gösteren diyagram.*

## Paralel Olarak HTML'yi PDF'ye Dönüştür (HTML'yi Toplu Olarak PDF'ye Dönüştür)

Çok sayıda—belki binlerce—HTML dosyanız olduğunda, bunları tek tek ana thread üzerinde dönüştürmek bir darboğaz haline gelir. Sabit boyutlu bir thread havuzu, JVM'nin belirli sayıda worker thread'i yeniden kullanmasını sağlar, CPU kullanımını yüksek tutar ve sistemi aşırı yüklemez.

```java
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

/**
 * Simple demo that batch converts HTML files to PDF using a fixed thread pool.
 * Replace HTMLDocument with the actual class from your chosen PDF library.
 */
public class HtmlToPdfBatch {

    public static void main(String[] args) {
        // 1️⃣ Prepare a list of HTML files to convert
        List<String> htmlPaths = List.of(
            "src/main/resources/page1.html",
            "src/main/resources/page2.html",
            "src/main/resources/page3.html"
        );

        // 2️⃣ Create a fixed‑size thread pool – 4 workers is a good starting point
        ExecutorService pool = Executors.newFixedThreadPool(4);

        // 3️⃣ Submit a conversion task for each HTML file
        for (String htmlPath : htmlPaths) {
            pool.submit(() -> convertAndSave(htmlPath));
        }

        // 4️⃣ Shutdown ExecutorService gracefully – no new tasks, wait for running ones
        shutdownGracefully(pool);
    }

    /**
     * Core conversion logic – this is where we **save HTML document as PDF**.
     */
    private static void convertAndSave(String htmlPath) {
        try {
            // Imagine HTMLDocument is from OpenHTMLtoPDF, iText, etc.
            HTMLDocument doc = new HTMLDocument(htmlPath);
            String pdfPath = htmlPath.replace(".html", ".pdf");
            doc.save(pdfPath);
            System.out.println("✅ Converted: " + htmlPath + " → " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Failed to convert " + htmlPath + ": " + e.getMessage());
        }
    }

    /**
     * Helper that **shutdowns ExecutorService gracefully**.
     */
    private static void shutdownGracefully(ExecutorService executor) {
        executor.shutdown(); // stop accepting new tasks
        try {
            // Wait a maximum of 60 seconds for existing tasks to finish
            if (!executor.awaitTermination(60, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("⚠️ Pool didn’t terminate in time – forcing shutdown");
                executor.shutdownNow(); // cancel currently executing tasks
            } else {
                System.out.println("🛑 All tasks completed – executor shut down cleanly.");
            }
        } catch (InterruptedException ie) {
            // Preserve interrupt status & force shutdown
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }
}
```

### Bunun Neden Çalıştığı

- **Parallelism**: Each `submit` call hands the conversion to a worker thread, so four files can be processed simultaneously on a quad‑core machine.  
- **Isolation**: The `convertAndSave` method contains all the logic needed to **save HTML document as PDF**, making it easy to swap the underlying library later.  
- **Graceful termination**: By calling `shutdown()` first, we tell the pool “no more work, please finish what you have.” The `awaitTermination` loop gives those threads a chance to wrap up, and only if they’re stubborn do we invoke `shutdownNow()`. This pattern is the recommended way to **shutdown ExecutorService gracefully**.

## HTML Belgesini PDF Olarak Kaydet – Temel Dönüşüm Mantığı

Any **convert HTML to PDF** workflow'ün kalbi dönüşüm kütüphanesidir. Örnek, sahte bir `HTMLDocument` kullansa da, işte **OpenHTMLtoPDF** ile nasıl yapabileceğinize dair hızlı bir bakış:

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

public class HTMLDocument {
    private final String htmlPath;

    public HTMLDocument(String htmlPath) {
        this.htmlPath = htmlPath;
    }

    public void save(String pdfPath) throws IOException {
        try (OutputStream os = new FileOutputStream(pdfPath);
             InputStream is = new FileInputStream(htmlPath)) {

            PdfRendererBuilder builder = new PdfRendererBuilder();
            builder.withHtmlContent(new String(is.readAllBytes()), null);
            builder.toStream(os);
            builder.run();
        }
    }
}
```

**What’s happening?**  
1. The HTML file is read into a string.  
2. `PdfRendererBuilder` parses the markup, applies CSS, and streams the result to a PDF file.  
3. Any `IOException` bubbles up to `convertAndSave`, where we log success or failure.

Bu snippet'i iText’in `HtmlConverter.convertToPdf` ya da Flying Saucer’ın `ITextRenderer` ile değiştirmekten çekinmeyin. Çevreleyen thread‑pool kodu tamamen aynı kalır; bu yüzden **save HTML document as PDF**’yi ayrı bir sorumluluk olarak vurguladık.

## ExecutorService'i Sorunsuz Bir Şekilde Kapat – En İyi Uygulamalar

Yaygın bir tuzak, görevler gönderildikten hemen sonra `shutdownNow()` çağırmaktır. Bu, thread'leri aniden keser ve diskte yarım kalmış PDF dosyalarına yol açabilir. Kullandığımız desen—`shutdown()` → `awaitTermination()` → isteğe bağlı `shutdownNow()`—şu garantileri verir:

- **No new tasks** are accepted after you’ve queued everything.  
- **Running tasks** get a chance to finish cleanly.  
- **Blocked threads** are only interrupted if they exceed a reasonable timeout (here, 60 seconds).  

Çok büyük PDF'ler ya da yavaş bir render motoru bekliyorsanız, timeout süresini artırabilir veya daha sıkı kontrol için `executor.invokeAll(tasks, timeout, unit)` kullanabilirsiniz.

## Tam Çalışan Örnek (Tüm Parçalar Bir Arada)

Aşağıda, tek bir `HtmlToPdfBatch.java` dosyasına kopyalayıp yapıştırabileceğiniz bütün program yer alıyor. Sadece OpenHTMLtoPDF bağımlılığını (veya tercih ettiğiniz kütüphaneyi) `pom.xml` ya da Gradle build dosyanıza ekleyin, hazırsınız.



## Sonraki Öğrenmeniz Gerekenler

- [HTML'yi PDF'ye Dönüştürme Java – Aspose.HTML for Java Kullanarak](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [HTML'yi PDF'ye Dönüştürme Java – Aspose.HTML'de Ortamı Yapılandırma](/html/english/java/configuring-environment/)
- [Java'da HTML'yi PDF'ye Dönüştürme – Sayfa Boyutu Ayarlarıyla Adım‑Adım Kılavuz](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}