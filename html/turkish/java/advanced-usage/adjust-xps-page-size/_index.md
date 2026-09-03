---
date: 2026-03-18
description: Aspose.HTML for Java kullanarak HTML'yi XPS'ye dönüştürmeyi ve XPS sayfa
  boyutunu ayarlamayı öğrenin. Çıktı boyutlarını kolayca kontrol edin.
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: HTML'yi XPS'ye Dönüştürün ve Aspose.HTML for Java ile XPS Sayfa Boyutunu Ayarlayın
url: /tr/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'yi XPS'ye Dönüştürme ve Aspose.HTML for Java ile XPS Sayfa Boyutunu Ayarlama

Bu öğreticide **HTML'yi XPS'ye nasıl dönüştüreceğinizi** ve ortaya çıkan sayfa boyutunu Aspose.HTML for Java kullanarak nasıl ince ayar yapacağınızı keşfedeceksiniz. Yazdırılabilir raporlar, faturalar veya arşiv belgeleri oluşturuyor olun, XPS boyutlarını kontrol etmek çıktının tam olarak beklediğiniz gibi görünmesini sağlar. Ortamı kurmaktan son XPS dosyasını oluşturmaya kadar her adımı adım adım göstereceğiz—bu yeteneği Java uygulamalarınıza hemen entegre edebilirsiniz.

## Hızlı Yanıtlar
- **“HTML'yi XPS'ye dönüştürmek” ne anlama geliyor?** Bir HTML belgesini XPS dosyasına render eder, düzeni ve stillemeyi korur.  
- **Bir lisansa ihtiyacım var mı?** Ücretsiz deneme sürümü geliştirme için çalışır; üretim için ticari lisans gereklidir.  
- **Hangi Java sürümü destekleniyor?** Java 8 ve üzeri (JDK 11+ önerilir).  
- **Sayfa boyutunu değiştirebilir miyim?** Evet – Aspose.HTML, render etmeden önce özel boyutlar belirlemenize izin verir.  
- **Dönüşüm ne kadar sürer?** Standart sayfalar için genellikle bir saniyenin altında; daha büyük belgeler daha uzun sürebilir.

## HTML'yi XPS'ye Dönüştürmek nedir?

HTML'yi XPS'ye dönüştürmek, web odaklı bir işaretleme dosyasını alıp bir XPS (XML Paper Specification) belgesi üretmek anlamına gelir—PDF'ye benzer, sabit düzenli, yazdırmaya hazır bir format. Bu, Java uygulamalarından arşivleme veya baskı için yüksek doğruluklu, cihaz bağımsız belgeler gerektiğinde faydalıdır.

## Neden XPS sayfa boyutunu ayarlamalısınız?

Sayfa boyutunu ayarlamak, son belgenin fiziksel boyutları (ör. A4, Letter, özel etiketler) üzerinde kontrol sağlar. İstenmeyen ölçeklemeyi önler, içeriğin mükemmel oturmasını garantiler ve gereksiz beyaz alanı ortadan kaldırarak dosya boyutunu azaltabilir.

## Önkoşullar

Başlamadan önce, aşağıdaki önkoşulların yerine getirildiğinden emin olun:

1. **Java Geliştirme Ortamı** – Sisteminizde yüklü Java Development Kit (JDK).  
2. **Aspose.HTML for Java Kütüphanesi** – Aspose.HTML for Java kütüphanesini projenize indirin ve ekleyin. Kütüphaneyi [buradan](https://releases.aspose.com/html/java/) bulabilirsiniz.  
3. **Giriş HTML Dosyası** – Render etmek ve XPS sayfa boyutunu ayarlamak istediğiniz bir HTML dosyası hazırlayın. Bu öğreticide kendi HTML dosyanızı kullanabilirsiniz.

## Paketleri İçe Aktarma

İhtiyacınız olan sınıfları içe aktarın. Bu paketler belge işleme, render etme ve sayfa‑ayar özelliklerine erişim sağlar.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Adım‑Adım Kılavuz

Aşağıda, orijinal adımları yansıtan ve açıklık için ek bağlam sağlayan özlü, numaralı bir yürütme bulunmaktadır.

### Adım 1: Giriş Dosya Adını Ayarlama

`FileInputStream` kullanarak kaynak HTML dosyasını okuyun. Bu akış, ham HTML'yi Aspose.HTML motoruna besler.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### Adım 2: HTML Document Oluşturma ve Stil Ayarlama

Render edeceğiniz içeriği temsil eden bir `HTMLDocument` örneği oluşturun. Bu örnekte, stil göstermesi için küçük bir CSS bloğu ekliyoruz—kendi işaretlemenizi eklemekten çekinmeyin.

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### Adım 3: XPS Rendering Options Oluşturma

HTML'den XPS'ye dönüşümü etkileyen tüm ayarları tutmak için `XpsRenderingOptions` nesnesini oluşturun.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### Adım 4: Sayfa Boyutunu Ayarlama  

**XPS sayfa boyutunu nasıl ayarlarsınız** – Özel bir sayfa boyutu (genişlik × yükseklik puan cinsinden) tanımlayın ve renderlayıcının en geniş sayfaya otomatik olarak genişleyip genişlemeyeceğini belirtin. `adjustToWidestPage` değerini `false` olarak ayarlamak, belirttiğiniz tam boyutları korur.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### Adım 5: Çıktıyı Render Etme

Son olarak, yapılandırılmış seçeneklerle bir `XpsDevice` oluşturun ve HTML belgesini renderlayın. Sonuç, belirlediğiniz özel sayfa boyutlarına sahip tam bir XPS dosyasıdır.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Yaygın Sorunlar ve Çözümleri

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|-------|
| **Boş XPS çıktısı** | Giriş akışı kapatılmadı veya HTMLDocument yanlış dosyaya işaret ediyor. | `FileInputStream`'in doğru bir şekilde try‑with‑resources bloğu içinde sarıldığından ve dosya yolunun doğru olduğundan emin olun. |
| **Sayfa boyutu uygulanmadı** | `adjustToWidestPage` `true` olarak bırakıldı. | Adım 4'te gösterildiği gibi `pageSetup.setAdjustToWidestPage(false);` ayarlayın. |
| **Desteklenmeyen CSS** | Aspose.HTML, CSS'in bir alt kümesini destekler. | Temel düzen, yazı tipleri ve renklerle sınırlı kalın; gelişmiş seçiciler veya CSS Grid'den kaçının. |
| **LicenseException** | Üretimde geçerli bir lisans olmadan çalıştırmak. | Render etmeden önce geçici veya satın alınmış lisansınızı uygulayın (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Sıkça Sorulan Sorular

**S: Aspose.HTML for Java nedir?**  
C: Aspose.HTML for Java, geliştiricilerin HTML belgelerini XPS, PDF ve görüntüler gibi çeşitli formatlara manipüle etmelerini ve dönüştürmelerini sağlayan bir Java kütüphanesidir.

**S: Aspose.HTML for Java'ı nereden indirebilirim?**  
C: Aspose.HTML for Java kütüphanesini [bu bağlantıdan](https://releases.aspose.com/html/java/) indirebilirsiniz.

**S: Aspose.HTML for Java için ücretsiz deneme mevcut mu?**  
C: Evet, Aspose.HTML for Java için ücretsiz denemeyi [buradan](https://releases.aspose.com/) alabilirsiniz.

**S: Aspose.HTML for Java için geçici lisans nasıl alabilirim?**  
C: Aspose.HTML for Java için geçici lisans almak üzere [bu sayfayı](https://purchase.aspose.com/temporary-license/) ziyaret edin.

**S: Aspose.HTML for Java için destek alabilir miyim?**  
C: Evet, Aspose topluluğundan [Aspose Forum](https://forum.aspose.com/) üzerinden yardım ve destek alabilirsiniz.

**S: HTML'yi XPS'ye başsız (headless) bir sunucuda dönüştürebilir miyim?**  
C: Kesinlikle. Aspose.HTML, GUI'siz ortamlarda çalışır; sadece Java çalışma zamanının doğru yapılandırıldığından emin olun.

**S: Kütüphane özel sayfa kenar boşluklarını destekliyor mu?**  
C: Evet. `PageSetup`'i render seçeneklerine atamadan önce `PageSetup.setMarginTop()`, `setMarginBottom()` vb. metodları kullanın.

## Sonuç

Aspose.HTML for Java ile **HTML'yi XPS'ye dönüştürme** ve sayfa boyutunu ayarlama sürecini tamamen ele aldık. Bu adımları izleyerek, tam olarak istediğiniz düzen gereksinimlerine uyan, yazdırmaya hazır XPS belgeleri oluşturabilirsiniz. Farklı sayfa boyutları, stiller denemekten veya projenizin ihtiyaçlarına göre üstbilgi ve altbilgi eklemekten çekinmeyin.

Herhangi bir sorunuz varsa veya daha fazla yardıma ihtiyacınız olursa, [Aspose.HTML for Java belgelerini](https://reference.aspose.com/html/java/) inceleyin veya [Aspose Forum](https://forum.aspose.com/) üzerinden sohbet edin.

---

**Son Güncelleme:** 2026-03-18  
**Test Edilen Versiyon:** Aspose.HTML for Java 24.11 (yazım anındaki en son)  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}