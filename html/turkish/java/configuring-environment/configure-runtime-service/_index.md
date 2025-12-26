---
date: 2025-12-10
description: Aspose.HTML for Java'da zaman aşımını nasıl ayarlayacağınızı öğrenin,
  HTML'yi PNG'ye dönüştürmek için Runtime Service'i yapılandırın, sonsuz döngüleri
  önleyin ve performansı artırın.
linktitle: Configure Runtime Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML for Java Runtime Service'te Zaman Aşımı Nasıl Ayarlanır
url: /tr/java/configuring-environment/configure-runtime-service/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML for Java Runtime Service'de Zaman Aşımını Nasıl Ayarlarsınız

## Giriiş
Aspose.HTML for Java ile çalışırken betikler için **zaman aşımını nasıl ayarlayacağınızı**, doğru yerdesiniz. Betik yürütmesini kontrol etmek için yalnızca sonsuz döngüleri engellemez, aynı zamanda **html'yi png'ye dönüştür** işlemi hızlandırır ve uygulamanızın yanıt vermesini sağlar. Bu öğreticide Runtime Service'i çalıştırma, betik yürütmesini sınırlama ve sonunda HTML'den programınızın takılmasından bir PNG görüntüsü üretim adımlarını adım adım göstermez.

## Hızlı Yanıtlar
- **Çalışma Zamanı Hizmeti ne işe yarar?** HTML işlenirken betik yürütme süresinin kontrol edilmesini ve kaynakların yönetilmesini sağlar.
- **JavaScript için zaman aşımı nasıl dağıtılır?** `runtimeService.setJavaScriptTimeout(TimeSpan.fromSeconds(...))` kullanın.
- **Sonsuz döngüleri önleyebilir miyim?** Evet – zaman aşımı, tanımlı sınır aşan döngüleri durdurulur.
- **Bu, HTML'den PNG'ye dönüşümün etkileri mi?** Hayır, betik tamamlandığında veya zaman aşımla sonlandırıldığında dönüşüm devam eder.
- **Hangi Aspose.HTML sürümü gereklidir?** Aspose indirme sürümündeki son sürüm.

## Önkoşullar
Nitel ayrıntılara geçmeden önce aşağıdakilere sahip olduğunuzdan emin olun:

1. **Java Development Kit (JDK)** – [Oracle'ın web sitesinde](https://www.oracle.com/java/technologies/javase-downloads.html) kurun.
2. **Aspose.HTML for Java Library** – en yeni sürüm [Aspose sürüm sayfasından](https://releases.aspose.com/html/java/) alın.
3. **IDE** – IntelliJ IDEA, Eclipse veya NetBeans mevcuttur.
4. **Temel Java & HTML bilgisi** – kod örneklerini takip etmek için gereklidir.

## Paketleri İçe Aktarma
Öncelikle, ihtiyacınız olan sınıfları içe aktarın. Dosya işleme için `java.io.IOException` içe aktarımı gereklidir.

```java
import java.io.IOException;

```

## Adım 1: JavaScript Kodu İçeren Bir HTML Dosyası Oluşturma
We’ll start by generating a simple HTML file that contains a JavaScript loop. This loop would run forever if we didn’t enforce a timeout, making it a perfect demo for the Runtime Service.

```java
String code = "<h1>Runtime Service</h1>\r\n" +
        "<script> while(true) {} </script>\r\n" +
        "<p>The Runtime Service optimizes your system by helping it start apps and programs faster.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("runtime-service.html")) {
    fileWriter.write(code);
}
```

- `while(true) {}` betiği potansiyel bir sonsuz döngüyü temsil eder.  
- `FileWriter`, HTML içeriğini **runtime-service.html** dosyasına yazar.

## Adım 2: Yapılandırma Nesnesini Kurma
Next, create a `Configuration` instance. This object is the backbone for all Aspose.HTML services, including the Runtime Service.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Adım 3: Çalışma Zamanı Hizmetini Yapılandırma
Here’s where we actually **zaman aşımını nasıl ayarlayacağımız**. By retrieving the `IRuntimeService` from the configuration, we can define a JavaScript execution limit.

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

- `setJavaScriptTimeout`, betik yürütmesini **5 saniye** ile sınırlar ve etkili bir şekilde **sonsuz döngüleri önler**.  
- Bu aynı zamanda ağır istemci‑tarafı kodları için **betik yürütmesini sınırlar**.

## Adım 4: Yapılandırmayı İçeren HTML Belgesini Yükleyin
Now load the HTML file using the configuration that contains our timeout rule.

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

- Belge, daha önce tanımlanan zaman aşımına uyar; böylece sonsuz döngü 5 saniye sonra durdurulur.

## Adım 5: HTML'yi PNG'ye dönüştürün
With the document safely loaded, we can **convert html to png**. The conversion happens only after the script finishes or is terminated by the timeout.

```java
    com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.ImageSaveOptions(),
        "runtime-service_out.png"
    );
```

- `ImageSaveOptions`, Aspose.HTML'e PNG görüntüsü üretmesini söyler.  
- Oluşan dosya, **runtime-service_out.png**, takılmadan render edilen HTML'i gösterir.

## Adım 6: Kaynakları Temizleme
Finally, dispose of objects to free memory and avoid leaks.

```java
} finally {
    if (document != null) {
        document.dispose();
    }
    if (configuration != null) {
        configuration.dispose();
    }
}
```

- Doğru şekilde serbest bırakma, uzun süren uygulamalar için kritiktir.

## Çözüm
Aspose.HTML for Java'da JavaScript yürütmesi için **zaman aşımını nasıl ayarlayacağınızı**, **sonsuz döngüleri nasıl önleyeceğinizi** ve **convert html to png** işlemini güvenli bir şekilde nasıl yapacağınızı yeni öğrendiniz. Runtime Service'i yapılandırarak betik davranışı üzerinde ince ayar kontrolü elde eder, bu da daha hızlı başlangıç süreleri ve daha güvenilir dönüşümler sağlar. Çalışma yüklerinize uygun farklı zaman aşımı değerleriyle deneyler yapın; performansta belirgin bir artış göreceksiniz.

## Sıkça Sorulan Sorular

**S: Aspose.HTML for Java'da Runtime Service'in amacı nedir?**  
C: Betik yürütme süresini kontrol etmenizi sağlar, **sonsuz döngüleri önlemeye** yardımcı olur ve dönüşümlerin yanıt vermesini sağlar.

**S: Aspose.HTML for Java'ı nasıl indirebilirim?**  
C: En son sürümü [sürüm sayfasından](https://releases.aspose.com/html/java/) alın.

**S: `document` ve `configuration` nesnelerini serbest bırakmak gerekli mi?**  
C: Evet, serbest bırakma yerel kaynakları serbest eder ve bellek sızıntılarını önler.

**S: JavaScript zaman aşımını 5 saniyeden farklı bir değere ayarlayabilir miyim?**  
C: Tabii ki – `TimeSpan.fromSeconds()` argümanını senaryonuza uygun bir sınıra göre değiştirin.

**S: Sorun yaşarsam nereden yardım alabilirim?**  
C: Topluluk ve personel desteği için [Aspose.HTML forumunu](https://forum.aspose.com/c/html/29) ziyaret edin.

---

**Son Güncelleme:** 2025-12-10  
**Test Edilen Versiyon:** Aspose.HTML for Java 24.11 (latest)  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}