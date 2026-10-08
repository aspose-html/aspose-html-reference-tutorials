---
category: general
date: 2026-03-14
description: Aspose.HTML kullanarak JavaScript'ten Java'ya nasıl çağrı yapılacağını
  öğrenin. Bu kılavuz, host nesnesi eklemeyi, Java içinde JavaScript çalıştırmayı
  ve JavaScript'ten log almayı gösterir.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: tr
og_description: Aspose.HTML kullanarak JavaScript'ten Java'ya çağrı yapın. Host nesnesi
  ekleyin, Java içinde JavaScript çalıştırın ve tek bir öğreticide JavaScript'ten
  günlük kaydı alın.
og_title: JavaScript'ten Java'ya Çağrı – Host Nesnesi ile Tam Kılavuz
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: JavaScript'ten Java'yı Çağır – Host Nesnesi Ekle ve Java'da JavaScript Çalıştır
url: /tr/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaScript'ten Java'ya Çağrı – Host Nesnesi Ekle ve Java'da JavaScript Çalıştır

Hiç bir Java uygulaması içinde **JavaScript'ten Java'ya çağrı** yapmanız gerekti mi? Belki dinamik bir HTML rapor motoru oluşturuyorsunuz ya da sadece kontrol ettiğiniz bir betiğe bir Java logger'ı sunmak istiyorsunuz. Bu öğreticide, bir host nesnesi eklemeyi, Java'da JavaScript çalıştırmayı ve hatta **JavaScript'ten Java'ya log** atmayı Aspose.HTML ile nasıl yapacağınızı adım adım göreceksiniz.

Boş bir HTML belgesi oluşturan, bir Java `Logger` sınıfını host nesnesi olarak enjekte eden, küçük bir betik çalıştıran ve sonucu konsola yazdıran eksiksiz, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Harici bir web tarayıcısına ihtiyaç yok, gizemli bir “sihir” de yok—sadece bugün kopyalayıp yapıştırıp çalıştırabileceğiniz sade Java kodu.

## Ön Koşullar

- Java 17 (veya herhangi bir yeni JDK) yüklü ve yapılandırılmış.
- Aspose.HTML for Java kütüphanesi (sürüm 23.10 veya daha yeni). Maven Central'dan ya da Aspose web sitesinden edinebilirsiniz.
- Basit bir IDE veya metin düzenleyici; örnek komut satırından da çalışır.

> **Pro ipucu:** Maven kullanıyorsanız, `pom.xml` dosyanıza aşağıdaki bağımlılığı ekleyin:

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

Temel konuları hallettik, şimdi adım adım çözüme dalalım.

## Adım 1: Minimal Bir Java Projesi Oluşturun

İlk olarak, `JsHostObjectDemo` adlı yeni bir Java sınıfı oluşturun. Bu sınıf `main` metodumuzu ve host nesnesi tanımını barındıracak. Her şeyi tek bir dosyada tutmak öğreticiyi bağımsız ve kopyalamayı kolay hâle getirir.

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

### Neden `HTMLDocument`?

Aspose.HTML'in `HTMLDocument` sınıfı tam bir HTML‑5 uyumlu betik ortamı oluşturur. Herhangi bir işaretleme yüklemesesek bile, belgenin `window` nesnesi JavaScript motoruna erişim sağlar; işte **Java'da JavaScript çalıştır** sihrinin gerçekleştiği yer burası.

## Adım 2: Host Nesnesi Ekle – “javaLogger”

Şu satır

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

**host nesnesi ekleme** gereksinimini yerine getirir. `Logger` örneğini `"javaLogger"` adıyla kaydederek, bu belgede değerlendirilen herhangi bir betik `javaLogger.log(...)` çağrısı yapabilir. Bu, **javascript host object** kavramının özüdür: JavaScript'in JVM'e ulaşmasını sağlayan bir köprü.

### Yaygın Tuzaklar

- **İsim çakışmaları** – Betiğinizde zaten `javaLogger` adlı bir global değişken varsa, host nesnesi üzerine yazılır. Benzersiz bir ad seçin.
- **İş parçacığı güvenliği** – Host nesnesi aynı belge üzerindeki betik çalıştırmaları arasında paylaşılır. Betikleri eşzamanlı çalıştırmayı planlıyorsanız, host sınıfını iş parçacığı‑güvenli yapın (ör. `synchronized` veya `java.util.concurrent` primitiflerini kullanın).

## Adım 3: JavaScript Yaz ve Çalıştır

`eval`'e verdiğimiz betik kasıtlı olarak çok küçüktür:

```javascript
javaLogger.log('Hello from JavaScript!');
```

`document.getWindow().eval(script)` çalıştığında, motor global kapsamda `javaLogger`'ı arar, eklediğimiz Java nesnesini bulur ve sağlanan dizeyle `log` metodunu çağırır.

### Beklenen Çıktı

`main` metodunu çalıştırmak, konsola aşağıdaki satırı yazar:

```
[JS] Hello from JavaScript!
```

Bu küçük satır, **javascript'ten java'ya çağrı** yaptığımızı ve **javascript'ten log**'un normal bir Java `System.out` mesajı gibi göründüğünü kanıtlar.

## Adım 4: Host Nesnesini Genişlet – Sadece Loglamadan Daha Fazlası

Ek işlevsellik (ör. dosya erişimi, veritabanı sorguları) sunmanız gerekiyorsa, sadece `Logger` sınıfına daha fazla metod ekleyin—veya tamamen yeni bir host sınıfı oluşturun. İşte bir değer döndüren hızlı bir örnek:

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

Şimdi konsol şu şekilde gösterir:

```
[JS] 3+4=7
```

Bu, **javascript host object** deseninin esnekliğini gösterir: Java ve JavaScript arasında dönüştürülebilen veri tipleri (primitifler, dizeler, diziler vb.) olduğu sürece ihtiyacınız olan herhangi bir Java API'sini ortaya çıkarabilirsiniz.

## Adım 5: Kaynakları Temizle

Betik ortamıyla işiniz bittiğinde, yerel kaynakları serbest bırakmak için `HTMLDocument`'i dispose edin:

```java
document.dispose(); // Important for long‑running applications
```

Dispose edilmezse bellek sızıntılarına yol açabilir, özellikle bir döngüde çok sayıda belge oluşturuyorsanız.

## Tam Çalışan Örnek

Aşağıda hemen derleyip çalıştırabileceğiniz tam kaynak dosyası verilmiştir. `JsHostObjectDemo.java` olarak kaydedin, Aspose.HTML JAR'ının sınıf yolunuzda olduğundan emin olun ve `java JsHostObjectDemo` komutunu çalıştırın.

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

Bu, birkaç satırda **javascript'ten java'ya çağrı** iş akışının tamamıdır.

## Sıkça Sorulan Sorular

### Android'de çalışır mı?

Aspose.HTML saf bir Java kütüphanesidir, bu yüzden Android'in Dalvik/ART dahil olmak üzere herhangi bir JVM'de çalışır. JAR'ı paketleyin, aynı host‑object yeteneklerine sahip olursunuz.

### Karmaşık nesneler geçmem gerekirse?

Alanlar, getter ve setter'lar içeren POJO'ları (plain old Java objects) ortaya çıkarabilirsiniz. Motor bunları otomatik olarak JavaScript nesnelerine eşler. Koleksiyonlar için `java.util.List` veya dizileri kullanın—her ikisi de dönüştürülebilir.

### Hata yönetimi nasıl çalışır?

Betik bir JavaScript hatası fırlatırsa, `eval` bir `ScriptException` yayar. Çağrıyı bir try‑catch bloğuna sararak loglayabilir veya kurtarabilirsiniz:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### Birden fazla betiği sıralı çalıştırabilir miyim?

Kesinlikle. Aynı `HTMLDocument` örneği global kapsamını korur, bu yüzden `eval`'i tekrar tekrar çağırabilirsiniz. Betikler arasındaki değişken adı çakışmalarına dikkat edin.

## En İyi Uygulamalar ve İpuçları

- **Host nesnelerinizi açık bir şekilde adlandırın**—`javaLogger`, `javaUtils` vb.—karışıklığı önlemek için.
- **Mümkün olduğunca host metodlarını küçük ve yan etkisiz tutun**; bu hata ayıklamayı kolaylaştırır.
- **Belgeyi hemen dispose edin**; Aspose.HTML'in ayırdığı yerel belleği serbest bırakır.
- **JavaScript'ten gelen girdileri doğrulayın**, özellikle betikler güvenilmeyen kaynaklardan geliyorsa. Onları herhangi bir dış veri gibi ele alın.

## Sonuç

Artık **javascript'ten java'ya çağrı** yapmanın, **host nesnesi ekleyerek**, **Java'da JavaScript çalıştırarak** ve Aspose.HTML kullanarak **JavaScript'ten log atarak** nasıl yapılacağını gösteren sağlam, uçtan uca bir örneğe sahipsiniz. Bu desen güçlüdür: herhangi bir Java servisi betiklere açılabilir, Java uygulamanızı hafif bir betik platformuna dönüştürür.

Sonraki adımda şunları keşfedebilirsiniz:

- Tam bir HTML sayfası enjekte edip JavaScript'ten DOM'u manipüle etmek.
- Host nesnesini kullanarak veriyi Java tarafına akıtmak (ör. JSON serileştirme).
- Daha geniş dil desteği için Nashorn veya GraalVM gibi diğer betik motorlarıyla bütünleştirmek.

Deneyin, `Logger` veya `Utils` sınıflarını değiştirin ve kendi projelerinizde **javascript host object** kavramını ne kadar ileriye taşıyabileceğinizi görün.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}