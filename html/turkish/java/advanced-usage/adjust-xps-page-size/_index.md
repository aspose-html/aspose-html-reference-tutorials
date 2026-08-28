---
date: 2026-08-28
description: Aspose.HTML kullanarak Java'da HTML'yi XPS'ye dönüştürürken XPS sayfa
  boyutunu ayarlayın. HTML'yi XPS'ye kesin boyutlarla renderleyin.
keywords:
- adjust xps page size
- render html to xps
- aspose.html java
- xps conversion java
- html to xps
lastmod: 2026-08-28
linktitle: XPS Sayfa Boyutunu Ayarlama
og_description: Aspose.HTML kullanarak Java'da HTML'yi XPS'ye dönüştürürken XPS sayfa
  boyutunu ayarlayın. HTML'yi XPS'ye saniyeler içinde kesin boyutlarla renderlemeyi
  öğrenin.
og_image_alt: Tutorial showing how to adjust XPS page size during HTML to XPS conversion
  with Aspose.HTML for Java
og_title: Java'da HTML'yi XPS'ye dönüştürürken XPS sayfa boyutunu ayarlayın
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  headline: Adjust XPS page size when converting HTML to XPS in Java
  type: TechArticle
- description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  name: Adjust XPS page size when converting HTML to XPS in Java
  steps:
  - name: set the input file name
    text: The `FileInputStream` class reads raw bytes from a file, providing the HTML
      source to the renderer.
  - name: create an HTML document and set styles
    text: The `HTMLDocument` class represents an in‑memory HTML DOM used by Aspose.HTML
      for rendering.
  - name: create XPS rendering options
    text: The `XpsRenderingOptions` class holds settings that control how HTML is
      rendered to XPS, such as page size and image quality.
  - name: adjust the page size
    text: '**How to set XPS page size** – Define a custom page size (width × height
      in points) and tell the renderer whether it should automatically expand to the
      widest page. Setting `adjustToWidestPage` to `false` preserves the exact dimensions
      you specify. The `PageSetup` class defines page size, margins, a'
  - name: render the output
    text: The `XpsDevice` class is the rendering target that writes the processed
      content to an XPS file.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a Java library that allows developers to manipulate
      and convert HTML documents into various formats, such as XPS, PDF, and images.
      You can download the library from [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).
    question: What is Aspose.HTML for Java?
  - answer: You can download the Aspose.HTML for Java library from [Aspose product
      releases page](https://releases.aspose.com/).
    question: Where can I download Aspose.HTML for Java?
  - answer: Yes, you can get a free trial of Aspose.HTML for Java from the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: Is there a free trial available for Aspose.HTML for Java?
  - answer: To get a temporary license for Aspose.HTML for Java, visit the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: How can I obtain a temporary license for Aspose.HTML for Java?
  - answer: Yes, you can seek help and support from the Aspose community on the [Aspose
      Forum](https://forum.aspose.com/).
    question: Can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
tags:
- adjust xps page size
- Aspose.HTML
- Java XPS conversion
- HTML to XPS
- document rendering
title: Java'da HTML'yi XPS'ye dönüştürürken XPS sayfa boyutunu ayarlayın
url: /tr/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'yi XPS'ye Dönüştürürken XPS Sayfa Boyutunu Ayarlama (Java)

Bu öğreticide, Aspose.HTML for Java kullanarak HTML'yi XPS'ye dönüştürürken **XPS sayfa boyutunu nasıl ayarlayacağınızı** öğreneceksiniz. Yazdırılabilir faturalar, arşiv raporları veya özel boyutlu etiketler gibi ihtiyaçlarınız olsun, sayfa boyutlarını kontrol etmek, son XPS'nin tam olarak istediğiniz gibi görünmesini sağlar. Ortam kurulumunu, render seçeneklerini ve son XPS oluşturulmasını adım adım göstereceğiz, böylece bu yeteneği doğrudan Java uygulamalarınıza entegre edebilirsiniz.

## Hızlı Yanıtlar
- **“HTML'yi XPS'ye dönüştürmek” ne anlama geliyor?** Bir HTML belgesini XPS dosyasına render eder, düzeni ve stilini korur.  
- **Bir lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme sürümü çalışır; üretim için ticari bir lisans gereklidir.  
- **Hangi Java sürümü destekleniyor?** Java 8 ve üzeri (JDK 11+ önerilir).  
- **Sayfa boyutunu değiştirebilir miyim?** Evet – Aspose.HTML, render öncesinde özel boyutlar belirlemenize olanak tanır.  
- **Dönüşüm ne kadar sürer?** Standart sayfalar için genellikle bir saniyenin altında; daha büyük belgeler daha uzun sürebilir.

## HTML'yi XPS'ye Dönüştürmek Nedir?
HTML'yi XPS'ye dönüştürmek, web odaklı bir işaretleme dosyasını XPS (XML Paper Specification) belgesine üretmek anlamına gelir—PDF'ye benzer, sabit düzenli, yazdırmaya hazır bir format. Bu, Java uygulamalarından arşivleme veya yazdırma için yüksek doğruluklu, cihaz bağımsız belgeler gerektiğinde faydalıdır.

## Neden XPS Sayfa Boyutunu Ayarlamalısınız?
XPS sayfa boyutunu ayarlamak, son belgenin fiziksel boyutları üzerinde kontrol sağlar (ör. A4, Letter, özel etiketler). İstenmeyen ölçeklemeyi önler, içeriğin mükemmel oturmasını sağlar ve gereksiz boş alanları ortadan kaldırarak dosya boyutunu küçültebilir.

## Özel Sayfa Boyutu ile HTML'yi XPS'ye Nasıl Render Edersiniz?
HTML'nizi yükleyin, ihtiyacınız olan tam genişlik ve yüksekliği tanımlayan bir `PageSetup` ile `XpsRenderingOptions` yapılandırın, ardından bir `XpsDevice`'a render edin. Bu iki adımlı akış, düzeni bozmadan belirttiğiniz boyutları uygulamanıza ve tek bir API çağrısıyla gerçekleştirmenize olanak tanır.

## Ön Koşullar

1. **Java Geliştirme Ortamı** – Sisteminizde yüklü Java Development Kit (JDK).  
2. **Aspose.HTML for Java Kütüphanesi** – Aspose.HTML for Java kütüphanesini projenize indirin ve ekleyin. Kütüphaneyi [Aspose.HTML for Java indirme sayfasında](https://releases.aspose.com/html/java/) bulabilirsiniz.  
3. **Girdi HTML Dosyası** – Render etmek ve XPS sayfa boyutunu ayarlamak istediğiniz bir HTML dosyası hazırlayın. Bu öğreticide kendi HTML dosyanızı kullanabilirsiniz.

## Paketleri İçe Aktarma

`Page` sınıfı, XPS çıktısı için sayfa boyutlarını ve ayarlarını temsil eder. `HtmlRenderer` sınıfı, HTML'den XPS'ye dönüşümü gerçekleştirir.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Adım Adım Kılavuz

Aşağıda, orijinal adımları yansıtan ve açıklık kazandırmak için ek bağlam ekleyen özlü, numaralı bir yürütme bulunmaktadır.

### Adım 1: Girdi dosya adını ayarlama

`FileInputStream` sınıfı, bir dosyadan ham baytları okur ve HTML kaynağını render'a sağlar.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### Adım 2: HTML belgesi oluşturma ve stilleri ayarlama

`HTMLDocument` sınıfı, Aspose.HTML tarafından render için kullanılan bellek içi bir HTML DOM'u temsil eder.

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

### Adım 3: XPS render seçeneklerini oluşturma

`XpsRenderingOptions` sınıfı, HTML'nin XPS'ye nasıl render edileceğini kontrol eden ayarları (sayfa boyutu ve görüntü kalitesi gibi) tutar.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### Adım 4: Sayfa boyutunu ayarlama  

**XPS sayfa boyutunu nasıl ayarlarsınız** – Özel bir sayfa boyutu (genişlik × yükseklik puan cinsinden) tanımlayın ve render'ın en geniş sayfaya otomatik olarak genişleyip genişlemeyeceğini belirtin. `adjustToWidestPage` değerini `false` olarak ayarlamak, belirttiğiniz tam boyutları korur.

`PageSetup` sınıfı, XPS çıktısı için sayfa boyutunu, kenar boşluklarını ve yönlendirmeyi tanımlar.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### Adım 5: Çıktıyı render etme

`XpsDevice` sınıfı, işlenmiş içeriği bir XPS dosyasına yazan render hedefidir.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Yaygın Sorunlar ve Çözümler

| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| **Boş XPS çıktısı** | Girdi akışı kapatılmadı veya HTMLDocument yanlış dosyaya işaret ediyor. | `FileInputStream`'in doğru bir şekilde try‑with‑resources bloğuna sarıldığından ve dosya yolunun doğru olduğundan emin olun. |
| **Sayfa boyutu uygulanmadı** | `adjustToWidestPage` değeri `true` olarak bırakıldı. | Adım 4'te gösterildiği gibi `pageSetup.setAdjustToWidestPage(false);` ayarlayın. |
| **Desteklenmeyen CSS** | Aspose.HTML, CSS'in bir alt kümesini destekler. | Temel düzen, yazı tipleri ve renklerle sınırlı kalın; gelişmiş seçiciler veya CSS Grid'den kaçının. |
| **LicenseException** | Üretimde geçerli bir lisans olmadan çalıştırılıyor. | Render'dan önce geçici veya satın alınmış lisansınızı uygulayın (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Sıkça Sorulan Sorular

**Q: Aspose.HTML for Java nedir?**  
A: Aspose.HTML for Java, geliştiricilerin HTML belgelerini XPS, PDF ve görüntüler gibi çeşitli formatlara manipüle etmelerini ve dönüştürmelerini sağlayan bir Java kütüphanesidir. Kütüphaneyi [Aspose.HTML for Java indirme sayfasından](https://releases.aspose.com/html/java/) indirebilirsiniz.

**Q: Aspose.HTML for Java'yi nereden indirebilirim?**  
A: Aspose.HTML for Java kütüphanesini [Aspose ürün sürüm sayfasından](https://releases.aspose.com/) indirebilirsiniz.

**Q: Aspose.HTML for Java için ücretsiz deneme sürümü mevcut mu?**  
A: Evet, Aspose.HTML for Java için ücretsiz deneme sürümünü [geçici lisans talep sayfasından](https://purchase.aspose.com/temporary-license/) alabilirsiniz.

**Q: Aspose.HTML for Java için geçici lisans nasıl alabilirim?**  
A: Aspose.HTML for Java için geçici lisansı, [geçici lisans talep sayfasından](https://purchase.aspose.com/temporary-license/) edinebilirsiniz.

**Q: Aspose.HTML for Java için destek alabilir miyim?**  
A: Evet, Aspose topluluğundan [Aspose Forum](https://forum.aspose.com/) üzerinden yardım ve destek alabilirsiniz.

**Q: HTML'yi XPS'ye başsız (headless) bir sunucuda dönüştürebilir miyim?**  
A: Kesinlikle. Aspose.HTML, GUI olmayan ortamlarda çalışır; yalnızca Java çalışma zamanının doğru yapılandırıldığından emin olun.

**Q: Kütüphane özel sayfa kenar boşluklarını destekliyor mu?**  
A: Evet. `PageSetup`'i render seçeneklerine atamadan önce `PageSetup.setMarginTop()`, `setMarginBottom()` vb. yöntemlerini kullanın.

## Sonuç

Aspose.HTML for Java ile **HTML'yi XPS'ye dönüştürme** ve **XPS sayfa boyutunu ayarlama** sürecinin tamamını adım adım gösterdik. Bu adımları izleyerek, tam olarak istediğiniz düzen gereksinimlerine uyan, yazdırmaya hazır XPS belgeleri oluşturabilirsiniz. Farklı sayfa boyutları, stiller denemekten veya projenizin ihtiyaçlarına göre başlık ve altbilgi eklemekten çekinmeyin.

Herhangi bir sorunuz varsa veya daha fazla yardıma ihtiyacınız olursa, [Aspose.HTML for Java belgelerini](https://reference.aspose.com/html/java/) inceleyebilir veya [Aspose Forum](https://forum.aspose.com/) üzerinden sohbet edebilirsiniz.

---

**Son Güncelleme:** 2026-08-28  
**Denendiği Versiyon:** Aspose.HTML for Java 24.11 (yazım anındaki en yeni sürüm)  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Aspose.HTML for Java ile HTML'yi XPS'ye Dönüştürme](/html/java/conversion-html-to-other-formats/convert-html-to-xps/)
- [Aspose.HTML for Java ile PDF Sayfa Boyutunu Ayarlama](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Aspose.HTML for Java ile EPUB'ten XPS'ye Dönüştürme](/html/java/converting-epub-to-xps/convert-epub-to-xps/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}