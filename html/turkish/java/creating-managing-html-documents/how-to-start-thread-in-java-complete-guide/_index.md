---
category: general
date: 2026-06-19
description: Java'da yeniden kullanılabilir bir Runnable ile nasıl thread başlatılır,
  birden fazla thread başlatılır, thread adı yazdırılır ve Java ile HTML nasıl ayrıştırılır.
  Adım adım örnek.
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: tr
og_description: Java'da Runnable kullanarak nasıl thread başlatılır, birden fazla
  thread çalıştırılır, thread adı yazdırılır ve tek bir çalıştırılabilir örnek içinde
  Java ile HTML nasıl ayrıştırılır.
og_title: Java'da Thread Nasıl Başlatılır – Tam Rehber
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to start thread in Java with a reusable Runnable, start multiple
    threads, print thread name, and parse HTML with Java. Step‑by‑step example.
  headline: How to start thread in Java – Complete Guide
  type: TechArticle
tags:
- java
- multithreading
- html-parsing
- runnable
title: Java'da Thread Başlatma – Tam Kılavuz
url: /tr/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da Thread Nasıl Başlatılır – Tam Kılavuz

Boş kod yığınına boğulmadan **thread nasıl başlatılır** diye merak ettiniz mi? Tek başınıza değilsiniz. İster bir web tarayıcısı, bir UI güncelleyici ya da sadece ağır bir hesaplamayı arka plana atmak isteyin, thread oluşturmayı öğrenmek her Java geliştiricisi için olmazsa olmaz bir beceridir.

Bu öğreticide pratik bir senaryoyu adım adım inceleyeceğiz: **Java ile HTML ayrıştırma**, mevcut thread’in adını yazdırma ve aynı mantığı paylaşan **birden fazla thread başlatma**. Sonuna geldiğinizde **Runnable nasıl kullanılır**, birkaç worker nasıl oluşturulur ve beklediğiniz çıktıyı nasıl alırsınız—hepsini şimdi kopyalayıp yapıştırabileceğiniz bir örnekle göreceksiniz.

## Öğrenecekleriniz

- `Thread` sınıfı ve bir `Runnable` kullanarak **thread nasıl başlatılır** adımlarını tam olarak öğrenin.
- Aynı görevi tekrarlamadan **birden fazla thread başlatma** yöntemini keşfedin.
- İşlem sonuçlarınızla birlikte **thread adını yazdırma** en basit yolunu öğrenin.
- Hafif bir `HTMLDocument` yardımcı sınıfı (veya tercih ettiğiniz başka bir ayrıştırıcı) ile **Java’da HTML ayrıştırma** yöntemini görün.
- **Runnable nasıl kullanılır** sorusunun yeniden kullanılabilir ve test edilebilir kod için neden önemli olduğunu anlayın.

Çekirdek örnek için harici bir kütüphane gerekmez, ancak daha güçlü bir çözüm isterseniz Jsoup gibi bir parser’a geçiş yapabileceğinizi belirteceğiz.

---

## Adım 1: Yeniden kullanılabilir bir görev tanımlayın – **runnable nasıl kullanılır**

İlk olarak **runnable nasıl kullanılır** bilmeniz gereken, her thread’in gerçekleştireceği işi kapsüllemektir. `Runnable`, tek bir `run()` metoduna sahip bir fonksiyonel arayüzdür ve lambda ifadeleri için mükemmeldir.

```java
// Define the reusable task
Runnable extractTextLength = () -> {
    // Open the HTML file inside a try‑with‑resources block
    try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
        // Get the length of the body text
        int textLength = doc.getBody().getTextContent().length();

        // Print the thread name and the length
        System.out.println(Thread.currentThread().getName() + ": " + textLength);
    } catch (Exception e) {
        e.printStackTrace();
    }
};
```

**Neden önemli:** Mantığı bir `Runnable` içinde tutarak, bu runnable’ı istediğiniz kadar `Thread` nesnesine, bir thread havuzuna ya da ileride bir executor servisine verebilirsiniz. Bu sayede kodunuz DRY (tekrarsız) ve test edilebilir olur.

---

## Adım 2: **thread nasıl başlatılır** – ilk worker’ı oluşturun

Artık bir `Runnable`’ımız olduğuna göre, bir thread başlatmak `Thread` yapıcısını çağırmak kadar basittir. **thread nasıl başlatılır** sorusunun cevabı tek bir satırda:

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

İkinci argümana, `"Worker-1"` dikkat edin. Bu isim, daha sonra **thread adını yazdır** yaptığımızda görünecek ve hata ayıklamayı çok daha anlaşılır kılacaktır.

---

## Adım 3: **Birden fazla thread başlat** – aynı Runnable’ı yeniden kullanın

Birden fazla HTML dosyasını aynı anda işlemek mi istiyorsunuz? Aynı `Runnable` ile başka bir `Thread` oluşturmanız yeterli. Bu, **birden fazla thread başlat** konseptini görev kodunu kopyalamadan gösterir:

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

`Worker-1` ve `Worker-2` her ikisi de `extractTextLength` içinde tanımlı bloğu eşzamanlı olarak çalıştıracak. Görev durum bilgisini tutmadığı (sadece bir dosya okur) için yarış koşulu (race condition) olmayacaktır.

---

## Adım 4: **Thread adını yazdır** while parsing HTML

`Runnable` içinde zaten `Thread.currentThread().getName()` çağrısını yaptık. Bu, **thread adını yazdır** için kanuni yoldur. Çıktı aşağıdaki gibi görünecektir (HTML gövdesi 1 234 karakter içeriyorsa):

```
Worker-1: 1234
Worker-2: 1234
```

Programı daha büyük bir dosyada çalıştırırsanız, her satır aynı uzunluğu gösterecektir çünkü iki thread de aynı dosyayı okur. Farklı sonuçlar görmek için yolu değiştirin ya da dosya adını parametre olarak geçirin.

---

## Adım 5: Tam, runnable örnek – import’tan çalıştırmaya kadar

Aşağıda `HtmlThreadDemo.java` adlı bir dosyaya yapıştırabileceğiniz **tamamen kendi içinde** çalışan program yer alıyor. Gerçek bir parser’ınız olmasa bile kodun derlenebilmesi için minik bir `HTMLDocument` stub’u içerir. Üretim ortamında stub’u Jsoup ya da tercih ettiğiniz başka bir kütüphane ile değiştirin.

```java
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Minimal HTMLDocument helper.
 * In a real project you would use Jsoup or another robust parser.
 */
class HTMLDocument implements AutoCloseable {
    private final String content;

    private HTMLDocument(String html) {
        this.content = html;
    }

    public static HTMLDocument load(String path) throws IOException {
        String html = new String(Files.readAllBytes(Paths.get(path)));
        return new HTMLDocument(html);
    }

    public Body getBody() {
        // Very naive extraction of <body>...</body>
        int start = content.indexOf("<body");
        if (start == -1) return new Body("");
        start = content.indexOf('>', start) + 1;
        int end = content.indexOf("</body>", start);
        if (end == -1) end = content.length();
        return new Body(content.substring(start, end));
    }

    @Override
    public void close() {
        // No resources to free in this stub
    }

    /** Simple wrapper for body text */
    static class Body {
        private final String text;
        Body(String text) { this.text = text; }
        public String getTextContent() { return text; }
    }
}

public class HtmlThreadDemo {

    public static void main(String[] args) {
        // Step 1: Define a reusable task (how to use runnable)
        Runnable extractTextLength = () -> {
            try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
                int textLength = doc.getBody().getTextContent().length();
                // Step 4: Print thread name and length
                System.out.println(Thread.currentThread().getName() + ": " + textLength);
            } catch (Exception e) {
                e.printStackTrace();
            }
        };

        // Step 2 & 3: How to start thread and start multiple threads
        new Thread(extractTextLength, "Worker-1").start();
        new Thread(extractTextLength, "Worker-2").start();
    }
}
```

### Beklenen çıktı

`page.html` dosyasının `<body>` etiketi içinde 2 567 karakter olduğunu varsayalım; aşağıdaki gibi bir çıktı alacaksınız:

```
Worker-1: 2567
Worker-2: 2567
```

Dosya okunamazsa, `catch` bloğu sayesinde istisna yığını (stack trace) yazdırılacaktır.

---

## Yaygın Tuzaklar & Pro İpuçları

| Sorun | Neden oluşur | Çözüm |
|-------|--------------|------|
| **Dosya bulunamadı** | `"YOUR_DIRECTORY/page.html"` yolu, JVM’i başlattığınız konuma göre görecelidir. | Mutlak yol kullanın ya da `Paths.get("").toAbsolutePath()` ile debug yapın. |
| **Yarış koşulları** | `Runnable` paylaşılan durumu değiştiriyorsa, thread’ler çakışabilir. | Görevi durum bilgisiz (stateless) tutun ya da paylaşılan nesnelere erişimi senkronize edin. |
| **Çok fazla thread** | Yüzlerce `Thread` oluşturmak OS kaynaklarını tüketir. | Temelleri kavradıktan sonra sınırlı bir havuzla `ExecutorService` kullanın. |
| **Yanlış HTML ayrıştırma** | Stub `HTMLDocument` basittir; karmaşık sayfalar kırılabilir. | Jsoup ile değiştirin: `Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

---

## Örneği Genişletmek

Artık **thread nasıl başlatılır** bildiğinize göre şunları yapabilirsiniz:

- **Farklı dosyalar ayrıştır** – dosya adını `Runnable`’a parametre olarak geçirin (yapıcı ya da değişken yakalayan lambda kullanın).
- **Sonuçları topla** – sadece yazdırmak yerine `ConcurrentLinkedQueue<Integer>` gibi bir yapı kullanın.
- **Thread havuzu kullan** – daha iyi ölçeklenebilirlik için `Executors.newFixedThreadPool(4)` gibi bir havuza geçin.
- **Parser’ı değiştir** – projenizin ihtiyacına göre Jsoup, HtmlUnit ya da başka bir kütüphane ekleyin.

Tüm bu adımlar, temel fikri değişmez tutar: yeniden kullanılabilir bir görev tanımla, bir ya da birden çok thread’e ver, ve **thread adını yazdır** ile hangi thread’in çalıştığını gözlemle.

---

## Sonuç

Java’da **thread nasıl başlatılır** konusunu, **runnable nasıl kullanılır** ile birlikte ele aldık; **birden fazla thread başlat** ve **HTML parse** ederken **thread adını yazdır** yöntemlerini gösterdik. Yukarıdaki tam kod parçacığı çalıştırılmaya hazır ve kavramlar daha karmaşık, üretim‑ağırlıklı uygulamalara da ölçeklenebilir.

Deney yapmaktan çekinmeyin: dosya yolunu değiştirin, worker sayısını artırın ya da gerçek bir HTML parser ekleyin. Temel prensipler aynı kalır ve artık çoklu thread’li Java projeleriniz için sağlam bir temele sahipsiniz.

Thread güvenliği, executor servisleri ya da HTML parsing kütüphaneleri hakkında sorularınız mı var? Aşağıya yorum bırakın, mutlu kodlamalar!

## Bir Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakın konuları kapsar. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri içerir; böylece ek API özelliklerini öğrenebilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}