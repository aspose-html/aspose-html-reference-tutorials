---
category: general
date: 2026-03-04
description: Aspose.HTML kullanarak JavaScript'ten Java'yı çağırın, asenkron JavaScript
  çalıştırın ve basit bir örnekle Java'da JSON alın. JavaScript motorunu verimli bir
  şekilde çalıştırmayı öğrenin.
draft: false
keywords:
- call java from javascript
- run async javascript
- fetch json in java
- asynchronous fetch api
- execute javascript engine
language: tr
og_description: Aspose.HTML ile JavaScript'ten Java'yı çağırın, async JavaScript çalıştırın
  ve Java'da JSON alın. Tam kod, açıklamalar ve ipuçları dahil.
og_title: JavaScript'ten Java'yı Çağırma – Adım Adım Asenkron Fetch Öğreticisi
tags:
- Java
- JavaScript
- Aspose.HTML
- Async Programming
title: Java'yı JavaScript'ten Çağırma – Asenkron Fetch ve JS Motoru Çalıştırması İçin
  Tam Kılavuz
url: /tr/java/advanced-usage/call-java-from-javascript-complete-guide-to-async-fetch-js-e/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'yı JavaScript'ten Çağırma – Async Fetch API ile Tam Kılavuz

Hiç Java uygulamanızdan çıkmadan **Java'yı JavaScript'ten çağırmayı** merak ettiniz mi? Belki sunucu‑tarafı bir HTML renderlayıcı oluşturuyorsunuz ya da bir belgenin içinde çalışan bir betiğe bazı Java mantığını açığa çıkarmanız gerekiyor. İyi haber, Aspose.HTML bunu çocuk oyuncağı haline getiriyor. Bu rehberde sadece Java‑destekli bir belgede *run async JavaScript* çalıştırmayı göstermekle kalmayacağız, aynı zamanda modern **asynchronous fetch API** kullanarak **fetch JSON in Java** etmeyi ve sonunda **execute JavaScript engine** çağrılarını güvenli bir şekilde yapmayı da göstereceğiz.

Kısaca, kamu bir uç noktadan bir JSON yükü çeken, bunu bir Java host nesnesine teslim eden ve sonucu konsola yazdıran tam, çalıştırılabilir bir örnek elde edeceksiniz. Harici web sunucuları yok, ekstra kütüphane yok—sadece saf Java ve Aspose.HTML.

## Öğrenecekleriniz

- Aspose.HTML ile boş bir HTML belgesi nasıl oluşturulur.
- Java'dan **execute JavaScript engine** nasıl elde edilir.
- JavaScript'in çağırabileceği bir Java host nesnesi nasıl kaydedilir.
- **asynchronous JavaScript** fonksiyonunun **asynchronous fetch API** kullanarak nasıl yazılır.
- Çekilen verinin Java'da temiz bir callback ile nasıl işlenir.
- Beklenen çıktı ve sorun giderme ipuçları.

### Önkoşullar

- Java 17 veya daha yeni (kod JDK 11 ile de derlenebilir).
- Aspose.HTML for Java 23.7 (veya yazım anındaki en son sürüm).
- Java ve JavaScript promises konusunda temel bilgi.
- Demo `jsonplaceholder` isteği için internet erişimi.

Eğer bunlardan herhangi biri size yabancı geliyorsa panik yapmayın—her adım sade İngilizce açıklanıyor ve ne yaptığımızı tam olarak göreceksiniz.

---

## Adım 1 – Boş bir HTML Belgesi Oluşturun ve JavaScript Motorunu Alın

İlk ihtiyacımız, bize izole bir JavaScript ortamı sağlayan boş bir belge. Aspose.HTML’in `Document` sınıfı tam da bunu yapar.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Create an empty HTML document
        Document document = new Document();

        // Obtain the JavaScript engine associated with the document's window
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();
```

**Why this matters:** `Document` nesnesi bir tarayıcı penceresini taklit eder ve `JavaScriptEngine` sayesinde betikleri tam bir tarayıcı gibi çalıştırabiliriz. Bu, **call java from javascript** için temeldir—motor köprü görevi görür.

---

## Adım 2 – JavaScript'in Java'ya Geri Çağırma Yapabilmesi İçin Bir Host Nesnesi Kaydedin

Aspose.HTML, herhangi bir Java nesnesini script dünyasına açığa çıkarmanıza izin verir. Tek bir `onResult` metodu olan anonim bir sınıf oluşturacağız; bu metod aldığımız JSON'u basitçe yazdıracak.

```java
        // Register a Java host object that the script can invoke
        jsEngine.addHostObject("javaCallback", new Object() {
            // This method will be called from JavaScript with the fetched JSON string
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });
```

**Explanation:**  
- `addHostObject` adı `javaCallback`i anonim Java nesnesine bağlar.  
- JavaScript içinde `javaCallback.onResult(...)` çağrısı yapacağız.  
- Bu, **call java from javascript** in çekirdeğidir—script Java dünyasına uzanır ve Java yanıt verir.

> **Pro tip:** Host nesnesinin metodlarını `public` ve basit tutun; karmaşık nesneler serileştirme sorunlarına yol açabilir.

---

## Adım 3 – Asynchronous Fetch API Kullanarak Asenkron JavaScript Fonksiyonu Yazın

Şimdi eğlenceli kısım: uzaktaki bir uç noktadan JSON çeken minik bir betik. `async/await` kullanacağız; bu, **run async JavaScript** için modern yoldur.

```java
        // Asynchronous script that fetches JSON and passes it to the Java host object
        String asyncScript =
            "async function fetchData() {" +
            "  const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "  const json = await response.json();" +
            "  javaCallback.onResult(JSON.stringify(json));" +
            "}" +
            "fetchData();";
```

**Why we choose `fetch` over older XHR:**  
- `fetch` bir `Promise` döndürür, kodu daha temiz hâle getirir.  
- `await` ile doğal olarak çalışır, akış üst‑den‑alta okunur—**asynchronous fetch api** demoları için mükemmeldir.  
- API geleceğe dayanıklıdır; çoğu tarayıcı ve motor (Aspose dahil) kutudan çıkar çıkmaz destekler.

---

## Adım 4 – Belgenin JavaScript Motoru İçinde Betiği Çalıştırın

Son olarak betiği motora teslim ediyoruz. Motor küçük bir event loop başlatacak, `fetch` sözünü çözecek ve tamamlandığında Java'ya geri çağırma yapacak.

```java
        // Execute the async script
        jsEngine.execute(asyncScript);
    }
}
```

`AsyncJsTutorial` sınıfını çalıştırdığınızda aşağıdakine benzer bir şey görmelisiniz:

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

Bu çıktı üç şeyi doğrular:

1. **asynchronous fetch API** veriyi başarıyla getirdi.  
2. JSON serileştirildi ve Java'ya teslim edildi.  
3. **execute javascript engine** çağrımız deadlock olmadan tamamlandı.

---

## Adım 5 – Hataları ve Kenar Durumlarını Ele Alma (İsteğe Bağlı Geliştirmeler)

Gerçek dünyada kod nadiren her seferinde kusursuz çalışır. İşte birkaç yaygın tuzak ve bunlardan korunma yolları.

### 5.1 Ağ Hataları

Uzak sunucu kapalıysa `fetch` hata fırlatır. Çağrıyı bir `try/catch` bloğuna sarın:

```java
String asyncScript =
    "async function fetchData() {" +
    "  try {" +
    "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
    "    if (!response.ok) throw new Error('Network response was not ok');" +
    "    const json = await response.json();" +
    "    javaCallback.onResult(JSON.stringify(json));" +
    "  } catch (e) {" +
    "    javaCallback.onResult('Error: ' + e.message);" +
    "  }" +
    "}" +
    "fetchData();";
```

Şimdi Java tarafı asılı kalmak yerine bir hata mesajı alacak.

### 5.2 Zaman Aşımı

Aspose’un motoru `fetch` için yerel bir zaman aşımı sunmaz, ancak bunu JavaScript içinde uygulayabilirsiniz:

```javascript
const controller = new AbortController();
setTimeout(() => controller.abort(), 5000); // 5‑second timeout
const response = await fetch(url, { signal: controller.signal });
```

### 5.3 Çoklu Çağrılar

Birden fazla kaynak çekmeniz gerekiyorsa, URL dizisi üzerinde döngü ya da map yapın. Host nesnesi bir tanımlayıcı alacak şekilde genişletilebilir, böylece yanıtları ilişkilendirebilirsiniz.

---

## Tam Çalışan Örnek

Aşağıda IDE'nize kopyalayıp‑yapıştırabileceğiniz **full source file** bulunuyor. Gizli bağımlılık yok, sadece classpath'te Aspose.HTML JAR'ı yeterli.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an empty HTML document and obtain its JavaScript engine
        Document document = new Document();
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();

        // Step 2: Register a host object that JavaScript can call back into Java
        jsEngine.addHostObject("javaCallback", new Object() {
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });

        // Step 3: Write an async function that uses the asynchronous fetch API
        String asyncScript =
            "async function fetchData() {" +
            "  try {" +
            "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "    if (!response.ok) throw new Error('Network error');" +
            "    const json = await response.json();" +
            "    javaCallback.onResult(JSON.stringify(json));" +
            "  } catch (e) {" +
            "    javaCallback.onResult('Error: ' + e.message);" +
            "  }" +
            "}" +
            "fetchData();";

        // Step 4: Execute the script inside the document's JavaScript engine
        jsEngine.execute(asyncScript);
    }
}
```

**Expected console output**

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

`Error:` ile başlayan bir hata satırı görürseniz bir şeyler ters gitmiştir—muhtemelen ağda bir kesinti.

---

## Görsel Genel Bakış

![Java'nın JavaScript'i çağırdığı ve async fetch sonuçlarını aldığı diyagram – call java from javascript](/images/java-js-async.png)

*Görsel akışı gösterir: Java → JavaScriptEngine → async fetch → JavaCallback.*

---

## Sıkça Sorulan Sorular

**Can I use this approach with other JavaScript engines?**  
Evet, host nesne mekanizması sunan herhangi bir motor (ör. Nashorn, GraalVM) çalışabilir, ancak Aspose.HTML yerleşik `fetch` ile tam özellikli bir tarayıcı‑benzeri ortam sağlar.

**What if I need to return a complex Java object instead of a string?**  
Nesneyi Java tarafında JSON'a serileştirebilir ve JavaScript'in parse etmesini sağlayabilirsiniz, ya da host nesnesinde birden fazla metod açarak ayrı alanları alabilirsiniz.

**Is the `fetch` implementation fully standards‑compliant?**  
Aspose.HTML WHATWG Fetch Standard'ını uygular, böylece yönlendirmeler, CORS ve akış işlemleri doğru şekilde yönetilir.

**Does this block the Java thread while waiting for the network?**  
Hayır. `execute` çağrısı hemen döner ve iç motor sözleşmeyi asenkron olarak işler. Ancak ana thread, script bitene kadar ya da motoru açıkça kapatana kadar yaşamaya devam eder.

---

## Sonuç

**call Java from JavaScript**, **run async JavaScript** ve **fetch JSON in Java** işlemlerini **asynchronous fetch API** ile nasıl yapacağınızı pratik bir senaryo üzerinden gösterdik. Bir host nesnesi oluşturarak, düzenli bir `async` fonksiyon yazarak ve Aspose.HTML’in **JavaScript engine** iyle çalıştırarak iki çalışma zamanını birbirine bağlayan temiz, bloklamayan bir köprü elde ettiniz.

Deneyin, URL'yi değiştirin ya da daha fazla callback ekleyin—hayal gücünüz sınır. Bir sonraki adımda şunları keşfedebilirsiniz:

- **Executing JavaScript engine** ile birden fazla eşzamanlı script çalıştırma.  
- **run async javascript** kullanarak büyük veri setlerini paralel işleme.  
- Bu deseni, dinamik HTML üreten bir web‑servise entegre etme.

Deney yapmaktan çekinmeyin ve beklenmedik bir sorunla karşılaşırsanız yorum bırakın. Mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}