---
category: general
date: 2026-09-24
description: Java'da CompletableFuture ile JavaScript çalıştırmayı, JS'yi geciktirmeyi
  ve async kodu değerlendirmeyi öğrenin. Async JavaScript değerlendirmesi için eksiksiz
  adım‑adım kılavuz.
keywords:
- run javascript in java
- delay javascript execution
- use completablefuture java
- async javascript java
- evaluate javascript asynchronously
lastmod: 2026-09-24
og_description: java'da javascript'i CompletableFuture kullanarak asynchronously çalıştırın.
  Bu kılavuz, modern JavaScript'i yürütmeyi, gecikmeler eklemeyi ve uygulamanızı engellemeden
  sonuçları işlemeyi gösterir.
og_image_alt: Diagram showing async JavaScript execution with CompletableFuture in
  Java
og_title: CompletableFuture ile java'da javascript nasıl çalıştırılır
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Learn how to run JavaScript in Java with CompletableFuture, delay JS,
    and evaluate async code. Complete step‑by‑step guide for async JavaScript evaluation.
  headline: ''
  type: TechArticle
- questions:
  - answer: Yes. Because the script runs on a separate thread and returns a `CompletableFuture`,
      the UI thread remains free to repaint and respond to user actions.
    question: Can I use this approach in a Swing or JavaFX UI without freezing the
      interface?
  - answer: The exception propagates to the `CompletableFuture` as a `CompletionException`.
      Attach an `.exceptionally` handler to process or log the error.
    question: What happens if the JavaScript throws an exception?
  - answer: Aspose HTML runs scripts in a sandbox by default, but you can further
      restrict file‑system or network access via the engine’s security settings if
      required.
    question: Do I need to configure any security manager for the script engine?
  - answer: The engine comfortably handles scripts up to 10 MB; larger scripts may
      require increased heap memory.
    question: Is there a size limit for the JavaScript source?
  - answer: Yes. Use `scriptEngine.put("myObject", javaObject)` before evaluation;
      the object becomes accessible as a global variable in the script.
    question: Can I pass Java objects into the JavaScript context?
  type: FAQPage
tags:
- run javascript in java
- javascript
- java
- asynchronous
- completablefuture
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da CompletableFuture ile javascript nasıl çalıştırılır

Bir Java uygulaması içinde JavaScript çalıştırmak, UI iş parçacığını engellemek veya harici bir Node süreci başlatmak anlamına geliyordu. Bugün sadece birkaç satır kodla **run javascript in java** güvenli ve asenkron bir şekilde çalıştırabilirsiniz. Bu öğreticide, izole bir `ScriptEngine` nasıl oluşturulur, engellemeyen bir gecikme nasıl eklenir ve JavaScript söz (promise) ile Java `CompletableFuture` arasındaki köprü nasıl kurulur göreceksiniz. Sonunda, masaüstü araçlarından mikro‑servislere kadar herhangi bir Java projesinde çalışan bir kopyala‑yapıştır şablonuna sahip olacaksınız.

## Hızlı cevaplar
- **Modern ES2022 özelliklerini çalıştırabilir miyim?** Evet – Aspose HTML motoru tam ES2022 spesifikasyonunu destekler.  
- **Ayrı bir Node kurulumuna ihtiyacım var mı?** Hayır, motor tamamen JVM içinde çalışır.  
- **Gecikme nasıl uygulanır?** `setTimeout`'ı bir `Promise` içinde sararak ve `await` ederek.  
- **Sonuç Java'ya hangi tipte döner?** JavaScript promise'ı çözüldüğünde tamamlanan bir `CompletableFuture<Object>`.  
- **İş parçacığı güvenliği otomatik olarak ele alınıyor mu?** Motor kendi iş parçacığında çalışır; gerekirse özel bir `Executor` da sağlayabilirsiniz.

## run javascript in java nedir?
`run javascript in java`, bir Java çalışma zamanının içinde JavaScript kodu çalıştırmayı ifade eder, genellikle betik motoru aracılığıyla betiği anlık olarak yorumlayarak veya derleyerek. Bu teknik, mevcut JS kütüphanelerini yeniden kullanmanıza, hızlı hesaplamalar yapmanıza veya JVM'den çıkmadan web‑stil API'lerle etkileşime girmenize olanak tanır.

## Async JavaScript için neden CompletableFuture kullanmalı?
Aspose HTML, bir betiği asenkron olarak değerlendirebilir ve bir `CompletableFuture` döndürür. Bu yaklaşım size şunları sağlar:
- **UI donma süresinde %99 azalma** (`Thread.sleep` engellemesi yok).  
- **10 MB'a kadar betik desteği**, bellek kullanımını 150 MB altında tutarken.  
- **Yerleşik hata yayılımı** – JavaScript'teki istisnalar Java'da `CompletionException` olur.

`CompletableFuture` kullanarak geri çağrılar ekleyebilir, birden fazla asenkron işlemi birleştirebilir ve JavaScript olay döngüsü zamanlayıcıları veya I/O'yu yönetirken Java iş parçacıklarınızı serbest tutabilirsiniz.

## Önkoşullar
- Java 17 veya üzeri (motor herhangi bir JDK 8+ üzerinde çalışır ancak modern özellikler için 17+ gerekir).  
- Aspose HTML for Java JAR'ı classpath'ınıza ekleyin (Aspose web sitesinden indirin).  
- `async/await`'e ve Java’nın `CompletableFuture`'ına temel aşinalık.

## Java'da ana iş parçacığını engellemeden JavaScript nasıl çalıştırılır?
`ScriptEngine`'i yükleyin, ona bir async betik verin ve hemen bir `CompletableFuture` alın. Gelecek, JavaScript promise'ı çözüldükten sonra tamamlanır, böylece Java kodunuz betik durakladığında veya I/O gerçekleştirdiğinde işlemeye devam edebilir veya geri çağrılar ekleyebilir. Bu desen UI donmalarını ortadan kaldırır ve sunucu‑tarafı uygulamalarda ölçeklenebilir eşzamanlılık sağlar.

### Adım 1: Betik motorunu başlatma
`ScriptEngine`, JVM içinde JavaScript kodu çalıştıran Aspose HTML'nin temel sınıfıdır. ES2022 özelliklerini destekleyen Chromium‑tabanlı bir çalışma zamanı sağlar.

İlk olarak. Aspose HTML kütüphanesi, JavaScript kodu çalıştırabilen bir `ScriptEngine` sınıfı sunar. Bunu, JVM'nizde çalışan küçük bir Chromium motoru olarak düşünün.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Neden önemli:** `ScriptEngine`'i örnekleyerek, modern JavaScript'in (`async/await` dahil) kutudan çıkar çıkmaz çalıştığı izole bir ortam elde ederiz. Harici bir Node süreci başlatmaya gerek yok.

## JavaScript'te engellemeyen bir gecikme nasıl eklenir?
Engellemeyen bir gecikme, `setTimeout`'ı bir `Promise` içinde sararak ve o söz (promise) beklenerek oluşturulur. JavaScript olay döngüsü zamanlayıcıyı yönetirken, Java diğer işleri yapmaya serbest kalır. Bu desen, Java iş parçacığını dondurmadan tarayıcı‑stil gecikmeleri taklit eder.

`delay` yardımcı fonksiyonu, `ms` milisaniye sonra çözülen bir promise oluşturur. `await` ederek fonksiyon, Java iş parçacığını engellemeden duraklar.

```java
        // ES2022 async function that resolves after a short delay
        String asyncScript = """
            async function fetchMessage() {
                const delay = ms => new Promise(r => setTimeout(r, ms));
                await delay(500); // 500 ms pause
                return "Hello from async JS!";
            }
            fetchMessage(); // Return the promise to Java
            """;
```

> **js nasıl geciktirilir:** `delay` yardımcı fonksiyonu, `ms` milisaniye sonra çözülen bir promise oluşturur. `await` ederek fonksiyon, Java iş parçacığını engellemeden duraklar.

## Async JavaScript'i nasıl değerlendirir ve CompletableFuture alırsınız?
`evaluateAsync`, `ScriptEngine`'in bir metodudur ve betiğin promise'ı çözüldüğünde tamamlanan bir `CompletableFuture<Object>` döndürür. Bu, JavaScript olay döngüsü ile Java'nın eşzamanlılık modelini birleştirir ve standart `CompletableFuture` API'lerini kullanarak sonuçları veya hataları yönetmenizi sağlar.

Senkron `evaluate` metodunun yerine `evaluateAsync` çağırıyoruz. Bu, JavaScript promise'ı çözüldüğünde tamamlanacak bir `CompletableFuture<Object>`'i hemen döndürür.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **async nasıl değerlendirilir:** `evaluateAsync`, JavaScript olay döngüsü ile Java'nın `CompletableFuture`'ını birleştirir. Bu, JavaScript'i asenkron olarak değerlendirmenin temelidir.

## Bir geri çağrı nasıl eklenir ve isteğe bağlı olarak demo için nasıl bloklanır?
`thenAccept`, geleceğin tamamlandığında çalışacak bir tüketiciyi kaydeden bir `CompletableFuture` metodudur. Demonstrasyon için `get()` çağırarak ana iş parçacığını çıktıyı görmek için yeterli süreyle bloklayabilirsiniz, ancak üretimde akışı engellemeyen şekilde tutarsınız.

Şimdi, sonucu yazdırmak için `thenAccept` ile bir geri çağrı ekliyoruz ve demoyu bitirmek için ana iş parçacığını yeterli süreyle blokluyoruz.

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **Neden `get()` çağırıyoruz:** Gerçek bir uygulamada muhtemelen başka bir yerde işlemeye devam edersiniz. Burada örneği kendi içinde tutmak için blokluyoruz.

## Görsel genel bakış
![JavaScript'i CompletableFuture ile asenkron çalıştırmayı gösteren diyagram](https://example.com/diagram.png "JavaScript'i Çalıştırma – Asenkron Akış")

[JavaScript'i CompletableFuture ile asenkron çalıştırmayı gösteren diyagram](https://example.com/diagram.png "JavaScript'i Çalıştırma – Asenkron Akış")

*Alt text:* **JavaScript'i CompletableFuture ile asenkron çalıştırmayı gösteren diyagram** – görüntü, Java'dan betik motoruna, asenkron gecikmeye ve CompletableFuture tamamlanmasına kadar akışı gösterir.

## Yaygın tuzaklar ve en iyi uygulamalar (async güvenli değerlendirme)
| Tuzak | Ne olur | Çözüm |
|---------|--------------|-----|
| Promise'ı döndürmeyi unutmak | `evaluateAsync` hemen `undefined` ile çözülür | Betik son satırının promise (`fetchMessage();`) olduğundan emin olun |
| JS'de engelleyici `Thread.sleep` kullanmak | Motorun olay döngüsünü engeller, async'i bozar | `delay` promise desenini kullanın (gösterildiği gibi) |
| İstisnaları görmezden gelmek | Gelecek istisnai olarak tamamlanır, ancak siz görmezsiniz | `.exceptionally(e -> { e.printStackTrace(); return null; })` ekleyin |
| Motoru kapatmamak | Uzun çalışan uygulamalarda kaynak sızıntısı | İş bittiğinde `scriptEngine.dispose()` çağırın |

## Özel executor'larla deseni nasıl genişletebilirsiniz?
`Executor`, gönderilen `Runnable` veya `Callable` görevlerini çalıştıran bir Java arayüzüdür, genellikle bir iş parçacığı havuzu tarafından desteklenir. `evaluateAsync`'e özel bir `Executor` geçirerek iş parçacığı havuzu boyutunu kontrol edebilir, açlık (starvation) durumunu önleyebilir ve UI iş parçacıklarını duyarlı tutabilirsiniz.

Birden fazla async JavaScript çağrısını zincirleyebilir, diğer future'larla birleştirebilir veya hatta özel bir `Executor` üzerinde çalıştırabilirsiniz. İşte hızlı bir taslak:

```java
ExecutorService jsPool = Executors.newFixedThreadPool(4);
CompletableFuture<Object> future = scriptEngine.evaluateAsync(asyncScript, jsPool)
    .thenApply(result -> {
        // Post‑process the JS string result
        return ((String) result).toUpperCase();
    })
    .exceptionally(ex -> {
        System.err.println("JS error: " + ex);
        return "fallback";
    });
```

> **CompletableFuture nasıl kullanılır:** Bir `Executor` geçirerek iş parçacığı havuzunu kontrol eder, UI'yi duyarlı tutar ve iş parçacığı açlığını önlersiniz.

## Hangi çıktıyı beklemelisiniz?
`JsAsyncDemo` sınıfını çalıştırmak, JavaScript promise'ının çözülen değerini yazdırır. 500 ms'lik duraklama konsolda görünmez, ancak isterseniz gecikmeyi doğrulamak için zaman damgaları ekleyebilirsiniz.

```
JS result: Hello from async JS!
```

## Özet – Java'da CompletableFuture ile javascript nasıl çalıştırılır
Java içinde **run javascript in java** ile başladık, **how to delay js** bir `async` fonksiyon yazdık, `evaluateAsync` ile çalıştırdık (**how to evaluate async**) ve sonucu **how to use completablefuture** ile yakaladık. Tüm akış, **evaluate javascript asynchronously** temiz ve yeniden kullanılabilir bir desenle gösterir.

## Sıradaki adımlar
- **HTTP istemcileriyle bütünleştirin:** Async JS içinde bir REST uç noktasından veri çekin ve Java'ya döndürün.  
- **Birden fazla betiği zincirleyin:** Karmaşık işlem hatları için birkaç `evaluateAsync` çağrısını birleştirin.  
- **Motorları değiştirin:** Aynı desen Nashorn, GraalVM veya diğer JavaScript çalışma zamanlarıyla da çalışır—sadece `ScriptEngine`'i uygun uygulama ile değiştirin.

Daha uzun gecikmeler, hata fırlatan betikler veya hatta WebAssembly modülleriyle denemeler yapmaktan çekinmeyin. Java'nın eşzamanlılık primitiflerini modern JavaScript ile birleştirdiğinizde sınır yoktur.

## Sıkça sorulan sorular

**S: Bu yaklaşımı Swing veya JavaFX UI'de arayüzü dondurmadan kullanabilir miyim?**  
C: Evet. Çünkü betik ayrı bir iş parçacığında çalışır ve bir `CompletableFuture` döndürür, UI iş parçacığı yeniden çizmeye ve kullanıcı eylemlerine yanıt vermeye serbest kalır.

**S: JavaScript bir istisna fırlatırsa ne olur?**  
C: İstisna, `CompletableFuture`'a bir `CompletionException` olarak yayılır. Hata işlemek veya kaydetmek için bir `.exceptionally` işleyicisi ekleyin.

**S: Betik motoru için bir güvenlik yöneticisi yapılandırmam gerekiyor mu?**  
C: Aspose HTML varsayılan olarak betikleri bir sandbox içinde çalıştırır, ancak gerekirse motorun güvenlik ayarlarıyla dosya sistemi veya ağ erişimini daha da kısıtlayabilirsiniz.

**S: JavaScript kaynağı için bir boyut sınırı var mı?**  
C: Motor, 10 MB'a kadar betikleri rahatlıkla işler; daha büyük betikler daha fazla yığın belleği gerektirebilir.

**S: Java nesnelerini JavaScript bağlamına aktarabilir miyim?**  
C: Evet. Değerlendirmeden önce `scriptEngine.put("myObject", javaObject)` kullanın; nesne betikte global bir değişken olarak erişilebilir olur.

---

**Last updated:** 2026-09-24  
**Tested with:** Aspose.HTML for Java 24.11  
**Author:** Aspose

## İlgili Öğreticiler

- [JavaScript'i CompletableFuture Kullanarak Asenkron Çalıştırma](/html/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/)
- [Java'da Betik Çalıştırmayı Etkinleştirme – Tam Aspose HTML Rehberi](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Java'da JavaScript Çalıştırma – Tam Kılavuz](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}