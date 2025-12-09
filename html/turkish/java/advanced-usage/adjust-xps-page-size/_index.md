---
date: 2025-11-29
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

# HTML'yi XPS'ye Dönüştürme ve XPS Sayfa Boyutunu Aspose.HTML for Java ile Ayarlama

Bu öğreticide **HTML'yi XPS'ye nasıl dönüştüreceğinizi** ve ortaya çıkan sayfa boyutunu Aspose.HTML for Java kullanarak nasıl ince ayar yapacağınızı keşfedeceksiniz. Yazdırılabilir raporlar, faturalar veya arşiv belgeleri oluşturuyor olun, XPS boyutlarını kontrol etmek çıktının tam istediğiniz gibi görünmesini sağlar. Ortamı kurmaktan son XPS dosyasını oluşturmaya kadar her adımı adım adım göstereceğiz; böylece bu yeteneği Java uygulamalarınıza hemen entegre edebilirsiniz.

## Hızlı Yanıtlar
- **“HTML'yi XPS'ye dönüştürmek” ne anlama geliyor?** Bir HTML belgesini XPS dosyasına render eder, düzeni ve stillemeyi korur.  
- **Lisans gerekir mi?** Geliştirme için ücretsiz deneme çalışır; üretim için ticari lisans gereklidir.  
- **Hangi Java sürümü destekleniyor?** Java 8 ve üzeri (JDK 11+ önerilir).  
- **Sayfa boyutunu değiştirebilir miyim?** Evet – Aspose.HTML, render etmeden önce özel boyutlar belirlemenize izin verir.  
- **Dönüşüm ne kadar sürer?** Standart sayfalar için genellikle bir saniyenin altında; daha büyük belgeler daha uzun sürebilir.

## HTML'yi XPS'ye dönüştürmek nedir?
HTML'yi XPS'ye dönüştürmek, web odaklı bir işaretleme dosyasını XPS (XML Paper Specification) belgesine üretmek anlamına gelir; bu, PDF'ye benzer sabit‑düzen, yazdırmaya hazır bir formattır. Java uygulamalarından arşivleme veya baskı için yüksek doğruluklu, cihaz‑bağımsız belgeler gerektiğinde kullanışlıdır.

## XPS sayfa boyutunu ayarlamanın nedeni nedir?
Sayfa boyutunu ayarlamak, son belgenin fiziksel boyutları üzerinde (ör. A4, Letter, özel etiketler) kontrol sağlar. İstenmeyen ölçeklemeyi önler, içeriğin mükemmel oturmasını garantiler ve gereksiz beyaz alanları ortadan kaldırarak dosya boyutunu azaltabilir.

## Önkoşullar

Başlamadan önce aşağıdaki önkoşulların yerine getirildiğinden emin olun:

1. **Java Geliştirme Ortamı** – Sisteminizde Java Development Kit (JDK) kurulu olmalı.  
2. **Aspose.HTML for Java Kütüphanesi** – Aspose.HTML for Java kütüphanesini indirin ve projenize ekleyin. Kütüphaneyi [buradan](https://releases.aspose.com/html/java/) bulabilirsiniz.  
3. **Giriş HTML Dosyası** – Render edip XPS sayfa boyutunu ayarlamak istediğiniz bir HTML dosyası hazırlayın. Bu öğreticide kendi HTML dosyanızı kullanabilirsiniz.

## Paketleri İçe Aktarma

İlk olarak ihtiyacınız olan sınıfları içe aktarın. Bu paketler işleme, render etme ve sayfa‑ayarları özelliklerine erişim sağlar.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Adım 1: Giriş Dosya Adını Ayarlama

Kaynak HTML dosyasını bir `FileInputStream` ile okuyun. Bu akış, ham HTML'yi Aspose.HTML motoruna besler.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## Adım 2: HTML Belgesi Oluşturma ve Stil Ayarlama

Render edeceğiniz içeriği temsil eden bir `HTMLDocument` örneği oluşturun. Bu örnekte, stil göstermesi için küçük bir CSS bloğu enjekte ediyoruz—kendi işaretlemenizi eklemekten çekinmeyin.

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

## Adım 3: XPS Render Seçeneklerini Oluşturma

HTML'den XPS'ye dönüşümü etkileyen tüm ayarları tutmak için `XpsRenderingOptions` nesnesini örnekleyin.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## Adım 4: Sayfa Boyutunu Ayarlama

Özel bir sayfa boyutu (genişlik × yükseklik puan cinsinden) tanımlayın ve renderlayıcının en geniş sayfaya otomatik olarak genişleyip genişlemeyeceğini belirtin. `adjustToWidestPage` değerini `false` olarak ayarlamak, belirttiğiniz kesin boyutları korur.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## Adım 5: Çıktıyı Render Etme

Son olarak, yapılandırılmış seçeneklerle bir `XpsDevice` oluşturun ve HTML belgesini render edin. Sonuç, belirlediğiniz özel sayfa boyutlarına sahip tam bir XPS dosyasıdır.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Yaygın Sorunlar ve Çözümler

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|-------|
| **Boş XPS çıktısı** | Giriş akışı kapatılmamış veya HTMLDocument yanlış dosyaya işaret ediyor. | `FileInputStream`'i try‑with‑resources bloğu içinde doğru şekilde sarmaladığınızdan ve dosya yolunun doğru olduğundan emin olun. |
| **Sayfa boyutu uygulanmıyor** | `adjustToWidestPage` `true` olarak bırakılmış. | Adım 4'te gösterildiği gibi `pageSetup.setAdjustToWidestPage(false);` ayarlayın. |
| **Desteklenmeyen CSS** | Aspose.HTML sınırlı bir CSS alt kümesini destekler. | Temel düzen, yazı tipleri ve renklerle kalın; gelişmiş seçiciler veya CSS Grid kullanımından kaçının. |
| **LicenseException** | Üretimde geçerli bir lisans olmadan çalıştırılıyor. | Renderlemeden önce geçici veya satın alınmış lisansınızı uygulayın (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Sık Sorulan Sorular

**S: Aspose.HTML for Java nedir?**  
C: Aspose.HTML for Java, geliştiricilerin HTML belgelerini XPS, PDF ve görüntüler gibi çeşitli formatlara dönüştürmelerine ve manipüle etmelerine olanak tanıyan bir Java kütüphanesidir.

**S: Aspose.HTML for Java'yi nereden indirebilirim?**  
C: Aspose.HTML for Java kütüphanesini [bu bağlantıdan](https://releases.aspose.com/html/java/) indirebilirsiniz.

**S: Aspose.HTML for Java için ücretsiz deneme mevcut mu?**  
C: Evet, Aspose.HTML for Java için ücretsiz deneme sürümünü [buradan](https://releases.aspose.com/) alabilirsiniz.

**S: Aspose.HTML for Java için geçici bir lisans nasıl alabilirim?**  
C: Aspose.HTML for Java için geçici lisans almak üzere [bu sayfayı](https://purchase.aspose.com/temporary-license/) ziyaret edin.

**S: Aspose.HTML for Java desteği alabilir miyim?**  
C: Evet, Aspose topluluğundan [Aspose Forum](https://forum.aspose.com/) üzerinden yardım ve destek alabilirsiniz.

**S: HTML'yi XPS'ye bir başsız sunucuda dönüştürebilir miyim?**  
C: Kesinlikle. Aspose.HTML, GUI gerektirmeyen ortamlarda çalışır; sadece Java çalışma zamanının doğru şekilde yapılandırıldığından emin olun.

**S: Kütüphane özel sayfa kenar boşluklarını destekliyor mu?**  
C: Evet. `PageSetup.setMarginTop()`, `setMarginBottom()` vb. metodları, `PageSetup`'ı render seçeneklerine atamadan önce kullanabilirsiniz.

## Sonuç

**HTML'yi XPS'ye dönüştürme** ve sayfa boyutunu Aspose.HTML for Java ile ayarlama sürecini tamamen gözden geçirdik. Bu adımları izleyerek, tam olarak istediğiniz düzen gereksinimlerine uyan, baskıya hazır XPS belgeleri üretebilirsiniz. Farklı sayfa boyutları, stiller denemek ya da projeleriniz için başlık ve alt bilgi eklemekten çekinmeyin.

Herhangi bir sorunuz varsa veya daha fazla yardıma ihtiyaç duyarsanız, [Aspose.HTML for Java belgelerine](https://reference.aspose.com/html/java/) göz atın veya [Aspose Forum](https://forum.aspose.com/) üzerinden topluluğa katılın.

---

**Son Güncelleme:** 2025-11-29  
**Test Edilen Versiyon:** Aspose.HTML for Java 24.11 (yazım anındaki en yeni sürüm)  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}