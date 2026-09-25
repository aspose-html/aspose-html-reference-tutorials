---
category: general
date: 2026-02-16
description: CompletableFuture ile Java’da JavaScript çalıştırmayı, JS’yi geciktirmeyi
  ve async kodu değerlendirmeyi öğrenin. Async JavaScript değerlendirmesi için adım
  adım tam rehber.
draft: false
keywords:
- how to run javascript
- how to use completablefuture
- how to delay js
- how to evaluate async
- evaluate javascript asynchronously
language: tr
og_description: Java'dan JavaScript çalıştırmayı, JS'yi geciktirmeyi ve CompletableFuture
  ile async kodu değerlendirmeyi bu kapsamlı öğreticide ustalaşın.
og_title: CompletableFuture Kullanarak JavaScript'i Asenkron Çalıştırma
tags:
- javascript
- java
- asynchronous
- completablefuture
title: CompletableFuture ile JavaScript'i Asenkron Çalıştırma
url: /tr/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaScript'i CompletableFuture Kullanarak Asenkron Çalıştırma

Hiç **JavaScript'i nasıl çalıştırılır** bir Java uygulaması içinde ana iş parçacığını engellemeden merak ettiniz mi? Belki veri çeken küçük bir betik çağırmanız gerekiyor, ancak UI'nizin donmasını istemiyorsunuz. İyi haber, modern Java kütüphaneleri JavaScript'i **asenkron** olarak değerlendirmenize izin veriyor ve bir tarayıcıda yaptığınız gibi gecikmeler ekleyebiliyorsunuz. Bu rehberde, Aspose HTML'nin `ScriptEngine`'ini `CompletableFuture` ile birlikte kullanan eksiksiz, çalıştırılabilir bir örnek göstereceğiz ve **JavaScript'i nasıl çalıştırılır** ifadesiyle JavaScript'i nasıl çalıştırıp sonucu Java'ya alacağınızı göstereceğiz.

Ayrıca **CompletableFuture'ı nasıl kullanılır**, **JS nasıl gecikirilir**, ve **asenkron olarak nasıl değerlendirilir** kodunu ele alacağız, böylece herhangi bir Java projesinde **JavaScript'i asenkron olarak değerlendirebilirsiniz**. Sonuna geldiğinizde, kopyalayıp‑yapıştırabileceğiniz, ayarlayabileceğiniz ve daha büyük sistemlere entegre edebileceğiniz sağlam bir şablona sahip olacaksınız.

Aspose HTML for Java JAR'ı sınıf yolunuza ekleyebileceğiniz dışında harici bir derleme aracı gerekmez. Hadi başlayalım.

## Öğrenecekleriniz

- Modern ES2022 JavaScript'i çalıştırabilen bir Java `ScriptEngine` kurun.
- Gecikme içeren bir `async` fonksiyon yazın (`how to delay js`).
- `evaluateAsync`'i çağırın ve bir `CompletableFuture` alın (`how to use completablefuture`).
- JavaScript promise'i çözüldüğünde sonucu alın (`how to evaluate async`).
- Hata yönetimi, iş parçacığı yönetimi ve deseni genişletme ipuçları.

## Adım 1: JavaScript'i Çalıştırma – Betik Motorunu Başlatma

İlk olarak. Aspose HTML kütüphanesi, JavaScript kodunu çalıştırabilen bir `ScriptEngine` sınıfı sağlar. Bunu, JVM içinde çalışan küçük bir Chromium motoru gibi düşünün.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Neden önemli:** `ScriptEngine`'i örnekleyerek, modern JavaScript'in (`async/await` dahil) kutudan çıkar çıkmaz çalıştığı izole bir ortam elde ederiz. Harici bir Node süreci başlatmaya gerek yok.

## Adım 2: JS'yi Geciktirme – Promise‑Tabanlı Zamanlayıcıyla Async Fonksiyon Yazma

JavaScript'in `setTimeout` fonksiyonu, yürütmeyi duraklatmanın klasik yoludur. Modern kodda bunu bir `Promise` içinde sararız, böylece `await` edebiliriz. Tam da bu, betik dizesinde yapacağımız şey.

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

> **JS'yi nasıl geciktiririz:** `delay` yardımcı fonksiyonu, `ms` milisaniye sonra çözülen bir promise oluşturur. `await` ederek, fonksiyon Java iş parçacığını engellemeden duraklar.

## Adım 3: Asenkron Değerlendirme – Betiği Çalıştır ve CompletableFuture Al

Senkron `evaluate` metodunu kullanmak yerine `evaluateAsync`'i çağırıyoruz. Bu, JavaScript promise'i çözüldüğünde tamamlanacak bir `CompletableFuture<Object>` döndürür.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **Asenkron nasıl değerlendirilir:** `evaluateAsync`, JavaScript olay döngüsü ile Java'nın `CompletableFuture`'ını birleştirir. Bu, **JavaScript'i asenkron olarak değerlendirme**nin çekirdeğidir.

## Adım 4: CompletableFuture Kullanımı – Geri Çağrı Ekleyip Demo İçin Blokla

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

## Görsel Genel Bakış

![CompletableFuture ile JavaScript'in asenkron çalıştırılmasını gösteren diyagram](https://example.com/diagram.png "JavaScript'i Çalıştırma – Asenkron Akış")

*Alt text:* **CompletableFuture ile JavaScript'in asenkron çalıştırılmasını gösteren diyagram** – görüntü, Java'dan betik motoruna, asenkron gecikmeye ve CompletableFuture tamamlanmasına kadar akışı gösterir.

## Yaygın Tuzaklar ve En İyi Uygulamalar (Asenkron Değerlendirmeyi Güvenli Yapma)

| Tuzak | Ne Olur | Çözüm |
|------|----------|------|
| Promise'i döndürmeyi unutmak | `evaluateAsync` hemen `undefined` ile çözülür | Betik'in son satırının promise olduğundan emin olun (`fetchMessage();`) |
| JS içinde engelleyici `Thread.sleep` kullanmak | Motorun olay döngüsünü engeller, asenkronluğu bozar | `delay` promise desenini kullanın (gösterildiği gibi) |
| İstisnaları görmezden gelmek | Future istisnai şekilde tamamlanır, ancak siz bunu görmezsiniz | `.exceptionally(e -> { e.printStackTrace(); return null; })` ekleyin |
| Motoru kapatmamamak | Uzun çalışan uygulamalarda kaynak sızıntısı | İşiniz bittiğinde `scriptEngine.dispose()` çağırın |

## Deseni Genişletme (Gerçek Projelerde CompletableFuture Kullanımı)

Birden fazla asenkron JavaScript çağrısını zincirleyebilir, diğer future'larla birleştirebilir veya hatta özel bir `Executor` üzerinde çalıştırabilirsiniz. İşte hızlı bir taslak:

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

> **CompletableFuture nasıl kullanılır:** Bir `Executor` geçirerek iş parçacığı havuzunu kontrol edersiniz, UI'nin yanıt vermesini sağlarsınız ve iş parçacığı açlığını önlersiniz.

## Beklenen Çıktı

`JsAsyncDemo` sınıfını çalıştırın ve şu çıktıyı görmelisiniz:

```
JS result: Hello from async JS!
```

500 ms'lik duraklama konsolda görünmez, ancak isterseniz zaman damgaları ekleyerek gecikmeyi doğrulayabilirsiniz.

## Özet – CompletableFuture ile JavaScript Çalıştırma

Java içinde **JavaScript'i nasıl çalıştırılır** ile başladık, **JS'yi nasıl geciktiririz** bir `async` fonksiyon yazdık, `evaluateAsync` (**asenkron nasıl değerlendirilir**) ile çalıştırdık ve **CompletableFuture nasıl kullanılır** ile sonucu yakaladık. Tüm akış, **JavaScript'i asenkron olarak değerlendirme**yi temiz ve yeniden kullanılabilir bir desenle gösterir.

## Sıradaki Adımlar?

- **HTTP istemcileriyle bütünleştirin:** Asenkron JS içinde bir REST uç noktasından veri çekin ve Java'ya döndürün.
- **Birden fazla betik kullanın:** Karmaşık işlem hatları için birkaç `evaluateAsync` çağrısını zincirleyin.
- **Motorları değiştirin:** Aynı desen Nashorn, GraalVM veya diğer JavaScript çalışma zamanlarıyla çalışır—sadece `ScriptEngine`'i değiştirin.

Daha uzun gecikmeler, hata fırlatan betikler veya hatta WebAssembly modülleriyle denemeler yapmaktan çekinmeyin. Java'nın eşzamanlılık primitive'lerini modern JavaScript ile birleştirdiğinizde sınır yoktur.

### Sorularınız mı var?

Bir şey net değilse—belki reddedilen bir promise nasıl ele alınır ya da Java'dan betiğe değişkenler nasıl geçirilir merak ediyorsunuzdur—aşağıya bir yorum bırakın. Kodlamanın tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}