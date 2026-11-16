---
category: general
date: 2026-04-05
description: Java çoklu iş parçacığı öğreticisi, sabit bir iş parçacığı havuzu kullanarak
  görevleri paralel çalıştırmayı ve ExecutorService'i güvenli bir şekilde kapatmayı
  gösterir.
draft: false
keywords:
- java multithreading tutorial
- fixed thread pool java
- shutdown executorservice
- print thread name
- run tasks parallel
language: tr
og_description: Paralel görev çalıştırma, sabit bir iş parçacığı havuzu oluşturma,
  iş parçacığı adını yazdırma ve ExecutorService'i temiz bir şekilde kapatma konusunda
  size rehberlik eden Java çoklu iş parçacığı öğreticisi.
og_title: java çoklu iş parçacığı öğreticisi – Sabit İş Parçacığı Havuzu ile Paralel
  Yürütme
tags:
- Java
- Concurrency
- ExecutorService
title: 'java çoklu iş parçacığı öğreticisi: Sabit İş Parçacığı Havuzu ile Görevleri
  Paralel Çalıştırma'
url: /tr/java/advanced-usage/java-multithreading-tutorial-run-tasks-parallel-with-fixed-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java multithreading tutorial – Paralel Çalıştırma Basitleştirildi

Java'da düşük seviyeli iş parçacığı yönetimine boğulmadan **run tasks parallel** nasıl yapılır hiç merak ettiniz mi? Bu **java multithreading tutorial**'da tam olarak bunu göstereceğiz: **fixed thread pool java** kullanarak, her iş parçacığının adını yazdırarak ve iş bittiğinde **shutdown executorservice**'i temiz bir şekilde kapatarak.  

Eğer ağ I/O'sunda bloklayan bir döngü yazdıysanız ya da aynı anda birkaç web sayfasını scrape ihtiyacınız varsa, aşağıda ele aldığımız desen size hem zaman hem de baş ağrısı kazandıracak.  

İhtiyacınız olan her şeyi ele alacağız—harici dokümanlar yok, sadece kopyala‑yapıştırabileceğiniz, çalıştırabileceğiniz ve sonuçları görebileceğiniz saf Java kodu. Sonunda, **fixed thread pool**'un sınırlı paralellik için neden genellikle ideal bir seçim olduğunu, onu nasıl güvenli bir şekilde sonlandıracağınızı ve iş parçacığı adını yazarak loglarınızı nasıl daha okunabilir hâle getireceğinizi anlayacaksınız.  

> **Prerequisites**: Java 8+ (`java.util.concurrent` paketi yıllardır kararlıdır), bir IDE ya da basit `javac`/`java` komut satırı ve OOP'nin temel bir kavramı. Aspose HTML for Java jar'ı dışında ek bir kütüphane gerekmez.

---

![java multithreading tutorial diyagramı, bir iş parçacığı havuzunun görevleri beslediğini gösterir](https://example.com/images/java-multithreading-tutorial.png "java multithreading tutorial diyagramı")

## java multithreading tutorial – Sabit İş Parçacığı Havuzu Kurulumu

**fixed thread pool** aynı anda çalışan iş parçacığı sayısını sınırlar, uygulamanızın çok fazla OS iş parçacığı oluşturmasını ve kaynakların tükenmesini önler. Burada dört çalışanlı bir havuz oluşturuyoruz:

```java
import java.util.concurrent.*;

public class ParallelProcessingTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Why four?* Çekeceğimiz URL sayısıyla eşleşir, ancak bu sayıyı CPU çekirdekleri, I/O yoğunluğu veya bellek limitlerine göre ayarlayabilirsiniz. `Executors` fabrikası, düşük seviyeli `Thread` yapıcısından sizi korur ve daha sonra **shutdown executorservice** yapacağınız temiz bir `ExecutorService` referansı sağlar.

## URL'leri Hazırlama ve Paralel Görevleri Tanımlama

Sonra, işlemek istediğimiz sayfaları listeliyoruz. Gerçek bir scraper'da muhtemelen bunları bir dosya ya da veritabanından okursunuz, ancak statik bir dizi örneği bağımsız tutar:

```java
        // Step 2: List the web pages to process
        String[] pageUrls = {
            "https://example.com/a.html",
            "https://example.com/b.html",
            "https://example.com/c.html",
            "https://example.com/d.html"
        };
```

Şimdi **run tasks parallel** kısmı geliyor. Her URL için belgeyi yükleyen ve başlığını yazdıran bir lambda gönderiyoruz. `Thread.currentThread().getName()` kullanımına dikkat edin – bu, hata ayıklamayı çok daha kolay hâle getiren **print thread name** hilesidir:

```java
        // Step 3: Submit a task for each URL that loads the document and prints its title
        for (String url : pageUrls) {
            executor.submit(() -> {
                try (HTMLDocument doc = new HTMLDocument(url)) {
                    String title = doc.getTitle();
                    // Print the thread name alongside the title
                    System.out.println(Thread.currentThread().getName() + " – " + title);
                } catch (Exception e) {
                    System.err.println(Thread.currentThread().getName() + " failed: " + e.getMessage());
                }
            });
        }
```

> **Pro tip**: `HTMLDocument`'i bir try‑with‑resources bloğuna sarmak, sayfa yüklenemese bile alttaki akışın kapatılmasını garanti eder.

## ExecutorService'i Zarifçe Kapatma

İşini bitirdikten sonra bir iş parçacığı havuzunu açık bırakmak JVM'nizin takılı kalmasına neden olabilir. Doğru yol **shutdown executorservice** yapmak, ardından sonlanmayı beklemektir:

```java
        // Step 4: Shut down the pool and wait for all tasks to finish
        executor.shutdown();                         // No new tasks will be accepted
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            // Force shutdown if tasks exceed the timeout
            executor.shutdownNow();
        }
    }
}
```

*Why the timeout?* Geri dönmeyen bir görevden (örneğin, takılan bir ağ çağrısı) korunmanızı sağlar. Havuz bir dakika içinde bitmezse, kalan iş parçacıklarını kesmek için `shutdownNow()` çağırırız.

### Expected Output

Programı çalıştırdığınızda aşağıdakine benzer bir çıktı alırsınız:

```
pool-1-thread-1 – Example A
pool-1-thread-3 – Example C
pool-1-thread-2 – Example B
pool-1-thread-4 – Example D
```

Tam sıralama değişebilir—sonuçta görevler gerçekten paraleldir. Sürekli kalan şey, **print thread name** önekidir; bu, hangi çalışanının her URL'yi işlediğini tam olarak gösterir.

---

## Common Variations & Edge Cases

| Situation | What to Change | Reason |
|-----------|----------------|--------|
| **İş parçacıklarından daha fazla URL** | Aynı havuz boyutunu koruyun; ekstra görevler otomatik olarak kuyruğa alınır. | Sabit havuz sizin için geri basıncı yönetir. |
| **CPU‑ağırlıklı iş** | Havuz boyutunu sabit 4 yerine `Runtime.getRuntime().availableProcessors()` olarak ayarlayın. | Aşırı tahsis etmeden CPU kullanımını maksimize eder. |
| **Belirli bir görevi iptal etme ihtiyacı** | `executor.submit()`'dan bir `Future<?>` referansı tutun ve `future.cancel(true)` çağırın. | Bireysel görevler üzerinde ayrıntılı kontrol sağlar. |
| **Büyük dosyaları işleme** | Havuz boyutunu makul bir şekilde artırın *veya* patlamalar bekliyorsanız `newCachedThreadPool()`'a geçin. | Önbellek havuzları talep üzerine iş parçacığı oluşturur, ancak sınırsız büyümeye dikkat edin. |

---

## Conclusion

Artık **java multithreading tutorial**'ı, **run tasks parallel**'ı **fixed thread pool java** kullanarak, **print thread name** ile net loglama ve **shutdown executorservice**'i temiz bir şekilde yaparak gösteren sağlam bir örneğe sahipsiniz. Tam ve çalıştırılabilir kod tek bir sınıfta bulunur, böylece herhangi bir projeye ekleyebilir ve I/O‑ağırlıklı işinizi anında ölçeklendirmeye başlayabilirsiniz.

Sırada ne var? `HTMLDocument`'i kendi HTTP istemcinizle değiştirin, farklı havuz boyutlarıyla deney yapın veya sonuçları tamamlandıkça toplamak için bir `CompletionService` entegre edin. Basit bir kuyruğun ötesinde geri basınç yönetimi gerekiyorsa `java.util.concurrent.Flow` ile reaktif akışları da keşfedebilirsiniz.

Kodlamaktan keyif alın ve unutmayın: doğru iş parçacığı havuzu stratejisiyle eşzamanlılık bir *çocuk oyuncağı* olur, hata kaynağı değil. Sorularınız varsa yorum bırakın—Java eşzamanlılığı hakkında sohbet etmeye her zaman hazırım!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}