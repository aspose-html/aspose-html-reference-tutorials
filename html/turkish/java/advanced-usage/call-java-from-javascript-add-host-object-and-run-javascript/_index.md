---
category: general
date: 2026-10-14
description: Aspose.HTML kullanarak javascript'ten java'yı çağırın. Host object eklemeyi,
  java içinde javascript çalıştırmayı ve javascript'ten log almayı kısa bir öğreticide
  öğrenin.
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: Aspose.HTML kullanarak javascript'ten java'yı çağırın. Bu kılavuz,
  host object eklemeyi, java içinde javascript çalıştırmayı ve javascript'ten log
  almayı, sadece birkaç satır kodla gösterir.
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: Java'yı javascript'ten çağırın – host object ekleyin ve java içinde javascript
  çalıştırın
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Call java from javascript using Aspose.HTML. Learn how to add a host
    object, execute javascript in java, and log from javascript in a concise tutorial.
  headline: Call java from javascript – add host object and run javascript in java
  type: TechArticle
- questions:
  - answer: Yes. Aspose.HTML is a pure‑Java library, so it runs on any JVM, including
      Android’s ART runtime.
    question: Does this work on Android?
  - answer: You can expose POJOs with getters and setters; the engine maps them to
      JavaScript objects automatically. Collections such as `java.util.List` or arrays
      are also convertible.
    question: What if I need to pass complex objects?
  - answer: If the script throws a JavaScript error, `eval` propagates a `ScriptException`.
      Wrap the call in a try‑catch block to log or recover.
    question: How does error handling work?
  - answer: Absolutely. The same `HTMLDocument` retains its global scope, so you can
      call `eval` repeatedly. Just manage variable names to avoid clashes.
    question: Can I run multiple scripts sequentially?
  - answer: Treat any external script as untrusted input. Validate parameters and
      consider sandboxing by exposing only the minimal required methods.
    question: Is the host object safe for untrusted scripts?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- scripting
- host object
title: Java'yı javascript'ten çağırın – host object ekleyin ve java içinde javascript
  çalıştırın
url: /tr/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'dan JavaScript'e Çağrı – Host Nesnesi Ekle ve Java'da JavaScript Çalıştır

Java uygulaması içinde **java'yı javascript'ten çağırmaya** hiç ihtiyaç duydunuz mu? Belki dinamik bir HTML rapor motoru oluşturuyorsunuz ya da kontrol ettiğiniz bir betiğe bir Java logger'ı sunmak istiyorsunuz. Bu öğreticide, bir host nesnesi eklemeyi, Java içinde JavaScript çalıştırmayı ve hatta **JavaScript'ten Java'ya loglamayı** Aspose.HTML ile nasıl yapacağınızı adım adım göreceksiniz.

Boş bir HTML belgesi oluşturup, bir Java `Logger` sınıfını host nesnesi olarak enjekte eden, küçük bir betiği çalıştıran ve sonucu konsola yazdıran tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Harici bir web tarayıcısına gerek yok, gizemli bir “sihir” yok — sadece bugün kopyalayıp çalıştırabileceğiniz sade Java kodu.

## Hızlı yanıtlar
- **Host nesnesi nasıl eklenir?** `document.getWindow().addHostObject("name", object)` ile bir Java örneğini kaydedin.  
- **Java içinde JavaScript çalıştırabilir miyim?** Evet—`document.getWindow().eval(yourScript)` kullanın.  
- **JavaScript'ten loglama mümkün mü?** Kesinlikle; host nesnesi herhangi bir `void log(String)` metodunu ortaya çıkarabilir.  
- **Hangi Aspose.HTML sürümü gerekli?** 23.10 veya daha yeni sürüm, tam host‑object API'sini destekler.  
- **Web tarayıcısına ihtiyacım var mı?** Hayır—Aspose.HTML gömülü bir motor sağlar, her şey başsız (head‑less) çalışır.

## java'dan javascript'e çağrı nedir?
**java'dan javascript'e çağrı**, Java nesnelerinin bir JavaScript çalışma zamanına açılması ve betiklerin Java metodlarını doğrudan çağırabilmesi tekniğidir. Aspose.HTML, bir Java süreci içinde hafif bir JavaScript motoru oluşturarak dış tarayıcılara ihtiyaç duymadan iki‑yönlü iletişimi mümkün kılar.

## Aspose.HTML'i java içinde javascript çalıştırmak için neden kullanmalıyım?
Aspose.HTML **50+ giriş ve çıkış formatını** destekler ve JavaScript'i tam uyumlu bir HTML5 ortamında değerlendirebilir. Basit tek‑satırlık kodlar için ortalama 200 ms sürede çalışır ve tam bir tarayıcı yığını yüklemez; bu da Selenium‑tabanlı yaklaşımlara göre bellek kullanımını %80'e kadar azaltır.

## Önkoşullar

- Java 17 (veya güncel bir JDK) kurulu ve yapılandırılmış.  
- Aspose.HTML for Java kütüphanesi (versiyon 23.10 veya daha yeni). Maven Central ya da Aspose web sitesinden temin edilebilir.  
- Basit bir IDE ya da metin editörü; örnek komut satırından da çalıştırılabilir.

> **Pro tip:** Maven kullanıyorsanız, `pom.xml` dosyanıza aşağıdaki bağımlılığı ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Veya Gradle için:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Temel ayarları hallettik, şimdi adım adım çözüme dalalım.

## Host nesnesi ekleyip java içinde javascript nasıl çalıştırılır?
`addHostObject`, bir Java nesnesini JavaScript bağlamında global bir değişken olarak kaydeder. `HTMLDocument`'inizi yükleyin, `addHostObject` ile `"javaLogger"` adı altında bir Java logger kaydedin ve ardından `javaLogger.log` çağıran kısa bir betiği değerlendirin. Tüm akış sadece üç API çağrısı gerektirir ve herhangi bir Java 17 ortamında çalışır.

### Adım 1: minimal bir java projesi oluşturun

İlk olarak `JsHostObjectDemo` adlı yeni bir Java sınıfı oluşturun. Bu sınıf `main` metodunu ve host nesnesi tanımını barındıracak. Her şeyi tek bir dosyada tutmak öğreticiyi bağımsız ve kopyalanması kolay hâle getirir.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### Neden bir `HTMLDocument`?
`HTMLDocument`, bellek içi bir HTML belgesi temsil eder ve bir JavaScript motoru sağlar. `HTMLDocument` sınıfı tam uyumlu bir HTML‑5 betik ortamı başlatır. Herhangi bir işaretleme yüklemesesek bile, belgenin `window` nesnesi JavaScript motoruna erişim verir; işte **java içinde javascript çalıştırma** sihri burada gerçekleşir. Ayrıca DOM'u manipüle edebilir, kaynakları yükleyebilir veya betikleri tarayıcı kullanmadan değerlendirebilirsiniz.

## Host nesnesi – “javaLogger” nasıl eklenir?
`Logger`, `log(String)` metodu ile mesajları konsola yazdıran basit bir Java sınıfıdır. `Logger` örneğini `"javaLogger"` adıyla kaydedin; böylece bu belgede değerlendirilen herhangi bir betik `javaLogger.log(...)` çağırabilir. Bu, **host nesnesi ekleme** gereksiniminin çekirdeğidir ve logger'ı JavaScript koduna global bir değişken olarak sunar.

### Yaygın tuzaklar

- **İsim çakışmaları** – Betiğinizde zaten `javaLogger` adlı bir global değişken varsa, host nesnesi üzerine yazılır. Benzersiz bir ad seçin.  
- **İş parçacığı güvenliği** – Host nesnesi aynı belge üzerindeki betik yürütmelerinde paylaşılır. Betikleri eşzamanlı çalıştırmayı planlıyorsanız, host sınıfını iş parçacığı‑güvenli yapın (ör. `synchronized` ya da `java.util.concurrent` primitifleri kullanın).

## java içinde javascript nasıl yazılır ve çalıştırılır?
`eval`, belgeye ait betik motorunda bir JavaScript dizesini çalıştırır ve herhangi bir sonucu döndürür. Küçük bir betiği `eval`'a verin. Motor, global kapsamdan `javaLogger`'ı çözer ve verilen dizeyi `log` metoduna iletir. Değer döndürebilir, istisnaları yakalayabilir ve daha karmaşık etkileşimler için birden fazla değerlendirme zinciri kurabilirsiniz.

### Beklenen çıktı

`main` metodunu çalıştırdığınızda konsola aşağıdaki satır yazdırılır:

```
[JS] Hello from JavaScript!
```

## Host nesnesini genişletmek – sadece loglamanın ötesinde?
Host nesnesi, `addHostObject` aracılığıyla JavaScript'e açılan herhangi bir Java örneğidir. `Logger` sınıfına ek metodlar ekleyerek ya da yeni bir host sınıfı oluşturarak işlevselliği artırın. Aşağıda, aynı zamanda bir değer döndüren hızlı bir örnek bulunuyor. Host nesnesi karmaşık tipler, I/O işlemleri ya da diğer servislerle etkileşim sağlayabilir. Değer döndürerek, betiğin Java'dan veri alması mümkün olur; bu da Java ile JavaScript arasında iki‑yönlü iletişimi sağlar.

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

Şimdi konsol şu çıktıyı verir:

```
[JS] 3+4=7
```

## Betikler çalıştırıldıktan sonra kaynakları nasıl temizlerim?
`dispose`, `HTMLDocument` örneğinin tuttuğu yerel kaynakları serbest bırakır. Betik ortamı ile işiniz bittiğinde `HTMLDocument`'i dispose ederek yerel kaynakları boşaltın. `dispose()` çağrısı yapılmazsa, özellikle döngülerde ya da uzun süren servislerde bellek sızıntılarına yol açabilir. Kullanımı bir try‑with‑resources bloğu içinde sarın ya da `finally` bloğunda `document.dispose()` çağrısını garanti edin.

```java
document.dispose(); // Important for long‑running applications
```

## Tam çalışan örnek

Aşağıda derleyip hemen çalıştırabileceğiniz tam kaynak dosyası yer alıyor. `JsHostObjectDemo.java` olarak kaydedin, Aspose.HTML JAR'ını sınıf yolunuza ekleyin ve `java JsHostObjectDemo` komutunu çalıştırın.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

Bu programı çalıştırdığınızda şu çıktı elde edilir:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

## Sıkça Sorulan Sorular

**S: Bu Android'de çalışır mı?**  
C: Evet. Aspose.HTML saf‑Java bir kütüphane olduğundan, Android'in ART çalışma zamanı dahil tüm JVM'lerde çalışır.

**S: Karmaşık nesneler geçmem gerekirse ne yapmalıyım?**  
C: Getter ve setter'ları olan POJO'ları açabilirsiniz; motor bunları otomatik olarak JavaScript nesnelerine dönüştürür. `java.util.List` gibi koleksiyonlar ya da diziler de dönüştürülebilir.

**S: Hata yönetimi nasıl olur?**  
C: Betik bir JavaScript hatası fırlattığında, `eval` bir `ScriptException` yayar. Çağrıyı try‑catch bloğuna alarak loglayabilir ya da kurtarabilirsiniz.

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**S: Birden fazla betiği sıralı çalıştırabilir miyim?**  
C: Kesinlikle. Aynı `HTMLDocument` global kapsamını korur, bu yüzden `eval`'ı tekrar tekrar çağırabilirsiniz. Çakışmaları önlemek için değişken adlarını yönetin.

**S: Host nesnesi güvensiz betikler için güvenli mi?**  
C: Dışarıdan gelen her betiği güvensiz kabul edin. Parametreleri doğrulayın ve yalnızca gerekli minimum metodları açarak sandbox uygulamayı düşünün.

## En iyi uygulamalar & ipuçları

- **Host nesnelerinizi açıkça adlandırın**—`javaLogger`, `javaUtils` vb.—karışıklığı önlemek için.  
- **Host metodlarını mümkün olduğunca küçük ve yan etkisiz tutun**; bu hata ayıklamayı kolaylaştırır.  
- **Belgeyi işiniz bittiğinde dispose edin**; Aspose.HTML'in ayırdığı yerel belleği serbest bırakır.  
- **JavaScript'ten gelen girdileri doğrulayın**, özellikle betikler dış kaynaklardan geliyorsa. Her dış veriyi normal bir veri gibi ele alın.

## Sonuç

Artık **java'dan javascript'e çağrı** yaparak **host nesnesi ekleme**, **java içinde javascript çalıştırma** ve **javascript'ten loglama** işlemlerini Aspose.HTML ile nasıl gerçekleştireceğinize dair eksiksiz bir örnek elinizde. Bu desen güçlü: Herhangi bir Java servisini betiklere açabilir, uygulamanızı hafif bir betik platformuna dönüştürebilirsiniz.

İleride şunları keşfedebilirsiniz:

- Tam bir HTML sayfası enjekte edip DOM'u JavaScript'ten manipüle etmek.  
- Host nesnesi aracılığıyla veriyi Java tarafına akıtmak (ör. JSON serileştirme).  
- Daha geniş dil desteği için Nashorn ya da GraalVM gibi diğer betik motorlarıyla bütünleştirmek.

Deneyin, `Logger` ya da `Utils` sınıflarını özelleştirin ve **javascript host nesnesi** kavramını kendi projelerinizde ne kadar ileriye taşıyabileceğinizi görün.

---

**Son Güncelleme:** 2026-10-14  
**Test Edilen Versiyon:** Aspose.HTML for Java 23.10  
**Yazar:** Aspose  






```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## İlgili Öğreticiler

- [Enable Script Execution In Java Complete Aspose Html Guide](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Execute Javascript In Java Complete Guide To Running Js From](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [How To Sandbox Javascript Complete Aspose Html Guide](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}