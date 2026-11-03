---
category: general
date: 2026-02-21
description: ExecutorService'i kullanarak HTML'yi hızlı bir şekilde PNG'ye dönüştürme.
  Java'da paralel görevlerle HTML dosyalarını toplu olarak dönüştürmeyi öğrenin.
draft: false
keywords:
- how to use executorservice
- convert html to png
- how to run parallel tasks
- how to convert html to png
- batch convert html files
language: tr
og_description: HTML dosyalarını PNG'ye toplu dönüştürmek için ExecutorService nasıl
  kullanılır. Adım adım rehber ve tam Java örneği.
og_title: ExecutorService'i Paralel HTML‑to‑PNG Dönüştürme İçin Nasıl Kullanılır
tags:
- Java
- concurrency
- Aspose.HTML
- image‑conversion
title: ExecutorService'i Paralel HTML‑to‑PNG Toplu Dönüştürme İçin Nasıl Kullanılır
url: /tr/java/conversion-html-to-various-image-formats/how-to-use-executorservice-for-parallel-html-to-png-batch-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ExecutorService'i Paralel HTML‑to‑PNG Toplu Dönüştürme İçin Nasıl Kullanılır

Hiç **ExecutorService'i nasıl kullanılır** diye merak ettiniz mi, bir klasördeki HTML sayfalarının PNG görüntülerine dönüştürülmesi gerektiğinde? Tek thread'li dönüşüm döngüsüyle web‑raporlama hattı takıldığında yalnız değilsiniz—birçok geliştirici bu duvara çarpar.  

İyi haber? Birkaç Java satırı ve güçlü Aspose.HTML `Converter` ile bir işçi thread havuzu oluşturabilir, her HTML dosyasını dönüştürücüye besleyebilir ve görüntülerin paralel olarak ortaya çıkmasını izleyebilirsiniz. Bu öğreticide ayrıca **convert html to png** temellerine değinecek, **run parallel tasks** nasıl yapılacağını gösterecek ve size hazır‑çalıştırılabilir bir **batch convert html files** betiği sunacağız.

## Önkoşullar

- Java 17 veya daha yeni (kod modern `java.nio.file` API'sini kullanır).  
- Classpath'ınızda Aspose.HTML for Java kütüphanesi. Maven Central'dan alabilirsiniz:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

- Kaynak `.html` dosyalarını içeren bir dizin ve boş bir çıktı klasörü.  
- Makul miktarda RAM—her dönüşüm kendi thread'inde çalışır, bu yüzden havuz boyutu sahip olduğunuz CPU çekirdek sayısıyla eşleşmelidir.

> **Pro ipucu:** Hyper‑threading'li bir makinede iseniz, `Runtime.getRuntime().availableProcessors()` genellikle optimal çekirdek sayısını döndürür.

## Adım 1 – Giriş ve Çıkış Yollarını Tanımlama

İlk olarak Java'ya HTML dosyalarının nerede olduğunu ve PNG'lerin nereye kaydedileceğini söylememiz gerekiyor. `Path` nesnelerini kullanmak kodun platform‑bağımsız kalmasını sağlar.

```java
import java.nio.file.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Input folder containing .html files
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        // Output folder for the generated .png files
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");

        // Ensure the output folder exists
        Files.createDirectories(outputDir);
```

> **Neden önemli:** Çıktı dizinini önceden oluşturmak, ilk işçi thread'i bir dosya yazmaya çalıştığında `FileNotFoundException` oluşmasını önler.

## Adım 2 – Sabit‑Boyutlu Thread Havuzu Oluşturma

**how to use ExecutorService**'in kalbi, donanımınıza uygun bir havuz oluşturmakta yatar. *Sabit* bir havuz, çalıştırabileceğimizden daha fazla thread oluşturmayacağımızı garanti eder.

```java
        // Create a thread pool sized to the number of available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());
```

> **Açıklama:** `ExecutorService` düşük seviyeli thread yönetimini soyutlar. `newFixedThreadPool` kullanarak JVM'nin thread'leri yeniden kullanmasını sağlarız, bu da sürekli oluşturma ve yok etme yükünü azaltır.

## Adım 3 – Her HTML Dosyası İçin Bir Dönüşüm Görevi Gönderme

Şimdi giriş dizininde dolaşıp her `*.html` dosyasını seçiyoruz ve havuza teslim ediyoruz. Her görev, `Converter.convert` çağıran küçük bir lambda'dır.

```java
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        // Build the output filename by swapping .html for .png
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();

                        // Perform the actual conversion
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }
```

### Arkada Ne Oluyor?

1. **DirectoryStream** dosya adlarını tembel (lazy) şekilde okur, bu sayede binlerce dosya olsa bile bellek kullanımı düşük kalır.  
2. Lambda, `htmlFile` ve `outputDir` değişkenlerini yakalar—ayrı bir `Runnable` sınıfına ihtiyaç yok.  
3. `Converter.convert` HTML'i okuyan, render eden ve bir PNG yazan bloklayıcı bir çağrıdır. Her çağrı kendi thread'inde çalıştığı için birden fazla dosya aynı anda işlenir—tam da **run parallel tasks** beklediğiniz davranıştır.

## Adım 4 – Havuzu Zarifçe Kapatma

Tüm görevler kuyruğa alındıktan sonra, havuza yeni iş kabul etmemesini ve her şeyin bitmesini beklemesini söyleriz. Bir şey takılı kalırsa, zaman aşımı bir saat sonra iptal olur; bu çoğu toplu iş için cömert bir süredir.

```java
        // No more tasks will be submitted
        pool.shutdown();

        // Wait up to 1 hour for all conversions to complete
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }

        System.out.println("All conversions completed.");
    }
}
```

> **Köşe durum:** Çok büyük HTML dosyalarınız varsa, zaman aşımını artırmak veya bellek kullanımını izlemek isteyebilirsiniz. `pool.setRejectedExecutionHandler(new ThreadPoolExecutor.CallerRunsPolicy())` eklemek, çağıran thread'in fazla görevleri çalıştırmasını zorlar ve `RejectedExecutionException` oluşmasını önler.

## Tam, Hazır‑Çalıştırılabilir Örnek

Aşağıda tüm program yer alıyor, tek bir `ParallelBatchConversion.java` dosyasına kopyala‑yapıştır yapılabilir.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.*;
import java.util.concurrent.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Step 1: Define source and destination folders
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");
        Files.createDirectories(outputDir);

        // Step 2: Create a thread pool sized to the available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());

        // Step 3: Submit a conversion task for each HTML file found
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }

        // Step 4: Shut down the pool and wait for all conversions to finish
        pool.shutdown();
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }
        System.out.println("All conversions completed.");
    }
}
```

### Beklenen çıktı

Programı çalıştırmak, her başarılı dönüşüm için bir satır yazdırır:

```
Converted: report1.html
Converted: dashboard.html
Converted: summary.html
All conversions completed.
```

Bir dosya başarısız olursa, istisna mesajı ile bir hata satırı görürsünüz; bu da hata ayıklamayı basitleştirir.

## Bu Deseni Nasıl Genişletebilirsiniz

- **Farklı görüntü formatları:** `.png` uzantısını `.jpg` veya `.bmp` ile değiştirin ve Aspose dönüşüm seçeneklerini buna göre ayarlayın.  
- **Dinamik thread sayısı:** I/O‑ağırlıklı iş yükleri için havuz boyutunu (`availableProcessors() * 2`) artırabilirsiniz.  
- **İlerleme izleme:** `System.out.println` yerine `jline` gibi thread‑güvenli bir ilerleme çubuğu kütüphanesi kullanın veya bir dosyaya kaydedin.  
- **Hata yönetimi:** Başarısız yolları bir `List<Path>` içinde toplayın ve ana döngü bittikten sonra yeniden deneyin.

## Sıkça Sorulan Sorular

**S: Bu Windows ve Linux'ta çalışır mı?**  
C: Evet. `java.nio.file` alt dosya sistemini soyutlar, bu yüzden aynı kod Java destekleyen herhangi bir işletim sisteminde değişiklik yapmadan çalışır.

**S: 10 000'den fazla HTML dosyam olursa ne olur?**  
C: `DirectoryStream` yineleyicisi girdileri tembel şekilde okur, bu yüzden bellek düşük kalır. Sadece diskinizin PNG çıktısı için yeterli boş alana sahip olduğundan emin olun.

**S: Her dönüşümün kullandığı belleği sınırlayabilir miyim?**  
C: Aspose.HTML, `HtmlLoadOptions` ve `ImageSaveOptions` aracılığıyla render motorunu yapılandırmanıza izin verir. Maksimum bitmap boyutu belirleyebilir veya RAM tüketimini kontrol altında tutmak için düşük kalite render'ı etkinleştirebilirsiniz.

## Sonuç

**how to use ExecutorService**'i **batch convert html files** PNG görüntülerine dönüştürmek için adım adım inceledik, sabit‑boyutlu havuzun CPU‑ağırlıklı render için neden ideal olduğunu açıkladık ve size eksiksiz, kopyala‑yapıştır yapılabilir bir Java programı sunduk. Yukarıdaki adımları izleyerek yavaş, tek‑thread'li bir döngüyü, tek komutla binlerce dosyayı işleyebilen hızlı, ölçeklenebilir bir boru hattına dönüştüreceksiniz.

Bir sonraki meydan okumaya hazır mısınız? `Converter.convert`'i Aspose'un PDF dışa aktarımıyla değiştirerek **convert html to pdf** deneyin veya bu mantığı, yükle‑ve‑dönüştür isteklerini kabul eden bir Spring Boot mikroservisine entegre edin. Temel fikir—`ExecutorService` kullanarak **run parallel tasks**—aynı kalır ve sayısız toplu‑işleme senaryosunda faydalı bulacaksınız.

Kodlamaktan keyif alın, ve thread'leriniz her zaman canlı kalsın! 

![executorservice'i nasıl kullanılır diyagramı](placeholder.png "Paralel HTML‑to‑PNG dönüşümü için thread havuzu iş akışını gösteren diyagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}