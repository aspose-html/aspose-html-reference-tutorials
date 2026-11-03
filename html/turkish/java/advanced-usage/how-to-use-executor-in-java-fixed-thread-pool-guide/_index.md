---
category: general
date: 2026-05-28
description: Java'da sabit bir iş parçacığı havuzu ile executor nasıl kullanılır,
  HTML'den metin çıkarma ve işleme hızını artırma – tam bir Java iş parçacığı havuzu
  örneği.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: tr
og_description: Java'da sabit bir iş parçacığı havuzu ile executor nasıl kullanılır.
  HTML dosyalarından metni verimli bir şekilde çıkaran eksiksiz bir Java iş parçacığı
  havuzu örneğini öğrenin.
og_title: Java’da Executor Kullanımı – Sabit İş Parçacığı Havuzu Rehberi
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: how to use executor in Java with a fixed thread pool, extract text
    from HTML and speed up processing – a complete java thread pool example.
  headline: How to Use Executor in Java – Fixed Thread Pool Guide
  type: TechArticle
tags:
- Java
- Concurrency
- HTML Parsing
title: Java'da Executor Nasıl Kullanılır – Sabit İş Parçacığı Havuzu Kılavuzu
url: /tr/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Executor Nasıl Kullanılır – Fixed Thread Pool Rehberi

Birçok görevi aynı anda çalıştırmak için **executor nasıl kullanılır** diye hiç merak ettiniz mi, belleğinizi tüketmeden? Tek başınıza değilsiniz. Gerçek dünyadaki birçok uygulamada bir klasördeki HTML dosyalarını taramanız, gövde metnini çıkarmanız ve bunu hızlı yapmanız gerekir—tam da bu öğreticinin çözdüğü senaryo.

Sizlere HTML'den metin çıkaran, her dosyanın karakter sayısını yazdıran ve temiz bir şekilde kapatan bir **fixed thread pool java** uygulamasını adım adım göstereceğiz. Sonunda, herhangi bir projeye ekleyebileceğiniz kendi içinde **java thread pool example** bir örnek ve havuz boyutunu özelleştirme ve uç durumları ele alma konusunda birkaç ipucu elde edeceksiniz.

> **İhtiyacınız olanlar**  
> * Java 17 (veya herhangi bir yeni JDK)  
> * Küçük bir HTML‑parsing kütüphanesi – *jsoup* kullanacağız çünkü test edilmiş ve sıfır‑konfigürasyonlu.  
> * Seçtiğiniz bir dizinde bir avuç örnek *.html* dosyası.

---

## Sabit İş Parçacığı Havuzu ile Executor Nasıl Kullanılır

Yoğun eşzamanlılık içeren herhangi bir Java programının kalbi `ExecutorService`'dir. **fixed thread pool** oluşturarak JVM'e tam N işçi iş parçacığını canlı tutmasını söyleriz; bu, iş parçacığı oluşturma maliyetini önler ve kaynak kullanımını sınırlar.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Why this matters:*  
* **Neden bu önemli:**  
  Her HTML dosyası için yeni bir `Thread` başlatırsanız, işletim sistemi mütevazı bir dizüstü bilgisayarda onlarca iş parçacığını zamanlamak zorunda kalır ve bağlam geçişi (context‑switch) sorununa yol açar. Sabit bir havuz aynı dört iş parçacığını yeniden kullanır, size öngörülebilir CPU kullanımı sağlar.

---

## İşlenecek HTML Dosyalarını Tanımlama – Fixed Thread Pool Java

Sonra havuza beslemek istediğimiz dosyaları listeliyoruz. Gerçek bir uygulamada muhtemelen bir dizin ağacını dolaşırdınız; burada basit tutuyoruz.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Tip:* `List.of` değiştirilemez bir liste döndürür, ek senkronizasyon olmadan iş parçacıkları arasında güvenle paylaşılabilir.

---

## Her HTML Dosyası İçin Ayrı Bir Görev Gönderme

Şimdi her yolu executor'e veriyoruz. Gönderdiğimiz lambda, dört işçi iş parçacığından birinde **paralel** olarak çalışacak.

```java
// Step 3: Dispatch a parsing job for every file
for (String htmlFilePath : htmlFilePaths) {
    executor.submit(() -> {
        // Each lambda runs on a thread from the pool
        try {
            // Step 4: Open the document, extract its text, and display the length
            String text = extractBodyText(htmlFilePath);
            System.out.println(htmlFilePath + " → " + text.length() + " chars");
        } catch (IOException e) {
            System.err.println("Failed to read " + htmlFilePath);
            e.printStackTrace();
        }
    });
}
```

**Why we wrap the logic in a method** (`extractBodyText`) bir sonraki bölümde netleşecek—lambda'yı düzenli tutar ve çıkarma kodunu başka yerlerde yeniden kullanmamızı sağlar.

---

## HTML'den Metin Çıkarma – Temel Mantık

İşte Jsoup kullanarak **html'den metin çıkaran** yeniden kullanılabilir yardımcı. Dosyayı açar, DOM'u ayrıştırır ve düz gövde metnini döndürür.

```java
/**
 * Reads an HTML file and returns the plain text inside the <body>.
 *
 * @param path absolute or relative path to the .html file
 * @return body text without tags
 * @throws IOException if the file cannot be read
 */
private static String extractBodyText(String path) throws IOException {
    // Jsoup parses the file into a Document object.
    org.jsoup.nodes.Document doc = org.jsoup.Jsoup.parse(new java.io.File(path), "UTF-8");
    // getBody() gives us the <body> element; text() strips all tags.
    return doc.body().text();
}
```

*Why Jsoup?* Hafiftir, hatalı işaretlemeyi zarifçe işler ve tam bir tarayıcı motoru gerektirmez. Metot `IOException` fırlatır, böylece çağıran nasıl kaydedileceğine veya kurtarılacağına karar verebilir—tek bir hatalı dosyanın tüm executor'ı sonlandırmasını istemediğiniz bir thread‑pool senaryosu için mükemmeldir.

---

## Executor'ı Zarifçe Kapatma – Sabit İş Parçacığı Havuzu Oluşturma

Tüm işleri gönderdikten sonra, havuza yeni iş kabul etmemesini ve zaten kuyruğa alınmış olanları bitirmesini söylemeliyiz.

```java
// Step 5: Initiate an orderly shutdown once all tasks are queued
executor.shutdown();
try {
    // Wait up to 30 seconds for all tasks to finish
    if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
        System.err.println("Timed out waiting for tasks; forcing shutdown.");
        executor.shutdownNow();
    }
} catch (InterruptedException ie) {
    // Preserve interrupt status and force shutdown
    Thread.currentThread().interrupt();
    executor.shutdownNow();
}
```

*Explanation:* `shutdown()` yeni gönderimleri engeller, `awaitTermination` ise her ayrıştırma işi bitene kadar (veya zaman aşımı dolana kadar) bloklar. Bir şey takılırsa, `shutdownNow()` çalışan görevleri iptal etmeye çalışır. Bu desen, **create fixed thread pool** güvenli bir şekilde oluşturmanın önerilen yoludur.

---

## Tam, Çalıştırılabilir Örnek

Her şeyi bir araya getirerek, derleyip çalıştırabileceğiniz tek bir dosya burada. Gerekli importları, `main` metodunu ve yukarıda açıklanan yardımcıyı içerir.

```java
import java.io.IOException;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

/**
 * Demonstrates how to use executor with a fixed thread pool to
 * extract text from multiple HTML files concurrently.
 */
public class HtmlThreadPoolDemo {

    public static void main(String[] args) {
        // 1️⃣ Build a fixed‑size pool (adjust the size for your hardware)
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ Define the files we want to process
        List<String> htmlFilePaths = List.of(
                "YOUR_DIRECTORY/a.html",
                "YOUR_DIRECTORY/b.html",
                "YOUR_DIRECTORY/c.html",
                "YOUR_DIRECTORY/d.html"
        );

        // 3️⃣ Submit a parsing task for each file
        for (String htmlFilePath : htmlFilePaths) {
            executor.submit(() -> {
                try {
                    String text = extractBodyText(htmlFilePath);
                    System.out.println(htmlFilePath + " → " + text.length() + " chars");
                } catch (IOException e) {
                    System.err.println("Error processing " + htmlFilePath);
                    e.printStackTrace();
                }
            });
        }

        // 5️⃣ Shut down the pool cleanly
        executor.shutdown();
        try {
            if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("Tasks took too long; forcing shutdown.");
                executor.shutdownNow();
            }
        } catch (InterruptedException ie) {
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }

    /**
     * Reads an HTML file and returns the plain text inside the <body>.
     *
     * @param path path to the .html file
     * @return body text without markup
     * @throws IOException if file cannot be read
     */
    private static String extractBodyText(String path) throws IOException {
        Document doc = Jsoup.parse(new java.io.File(path), "UTF-8");
        return doc.body().text();
    }
}
```

**Expected output** (her dosyanın yaklaşık 1 200 karakter gövde metni içerdiğini varsayarsak):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

Eğer bir dosya eksik ya da hatalıysa, `stderr`'e bir istisna yığını (stack trace) yazdırılır, ancak diğer görevler etkilenmeden devam eder—tam da iyi davranan bir **java thread pool example**'ın yapması gereken şey.

---

## Yaygın Sorular & Uç Durumlar

| Question | Answer |
|----------|--------|
| *Daha fazla dört dosyam olursa ne olur?* | Havuz ekstra görevleri kuyruğa alır ve bir iş parçacığı boşaldığında hemen çalıştırır. Ek bir koda gerek yok. |
| *Yerine `newCachedThreadPool` kullanmalı mıyım?* | `newCachedThreadPool` talep üzerine iş parçacıkları oluşturur ve sınırsız büyüyebilir, bu da I/O‑ağır işler için risklidir. **fixed thread pool** size öngörülebilir bellek ve CPU kullanımı sağlar. |
| *CPU çekirdeklerine göre havuz boyutunu nasıl değiştiririm?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` yaygın bir desendir. |
| *Bir dosya için ayrıştırma başarısız olursa ne olur?* | Lambda içindeki `catch (IOException e)` hatayı izole eder, kaydeder ve havuzun geri kalanının çalışmaya devam etmesini sağlar. |
| *Çıkarılan metni çağırana döndürebilir miyim?* | Evet—`submit(Runnable)` yerine `Future<String>` kullanın. Kod şu şekilde olur `Future<String> f = executor.submit(() -> extractBodyText(path));` ve daha sonra `String result = f.get();`. |

---

## Sonuç

**executor nasıl kullanılır** konusunu, **fixed thread pool java**'yu paralel olarak bir HTML dosyası koleksiyonunu işleyen, gövde metnini çıkaran ve karakter sayısını raporlayan bir şekilde başlatmayı kapsadık. Tam **java thread pool example** doğru kaynak yönetimini, hata işleme ve yeniden kullanılabilir bir çıkarma metodunu gösterir.

Sonraki adımlar? `extractBodyText` uygulamasını daha gelişmiş bir kazıyıcıyla değiştirin, daha büyük bir havuz boyutuyla deney yapın veya sonuçları bir veritabanına gönderin. Ayrıca `CompletionService`'i keşfedebilir, sonuçları hazır olduğunda alabilirsiniz; bu, dosya boyutları büyük ölçüde değiştiğinde kullanışlıdır.

İstediğiniz gibi dizin yolunu ayarlayın, daha fazla dosya ekleyin veya bu kod parçacığını daha büyük bir tarama çerçevesine entegre edin. Temel desen—havuzu oluştur, bağımsız görevler gönder ve zarifçe kapat—çalışma yükünüz ne kadar karmaşık olursa olsun aynı kalır.

İyi kodlamalar, ve iş parçacıklarınız her zaman (kapatana kadar) canlı kalsın!

## İlgili Öğreticiler

- [Fixed thread pool java – ExecutorService ile Paralel HTML Temizleme](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [Java'da HTML Sorgulama – Tam Öğretici](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Java için Aspose.HTML Kullanımı – HTML5 Canvas Rendering'i Ustalaştırma](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}