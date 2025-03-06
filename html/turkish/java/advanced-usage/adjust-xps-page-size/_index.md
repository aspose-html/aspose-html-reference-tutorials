---
title: Java için Aspose.HTML ile XPS Sayfa Boyutunu Ayarlayın
linktitle: XPS Sayfa Boyutunu Ayarlama
second_title: Aspose.HTML ile Java HTML İşleme
description: Aspose.HTML for Java ile XPS sayfa boyutunu nasıl ayarlayacağınızı öğrenin. XPS belgelerinizin çıktı boyutlarını kolayca kontrol edin.
weight: 16
url: /tr/java/advanced-usage/adjust-xps-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java için Aspose.HTML ile XPS Sayfa Boyutunu Ayarlayın


Bu eğitimde, Java için Aspose.HTML kullanarak XPS sayfa boyutunu ayarlama sürecinde size rehberlik edeceğiz. Bu güçlü kütüphane, HTML belgelerini düzenlemenize ve bunları XPS dahil olmak üzere çeşitli biçimlere dönüştürmenize olanak tanır. XPS belgenizin çıktı boyutlarını kontrol etmeniz gerektiğinde sayfa boyutunu ayarlamak önemlidir.

## Ön koşullar

Başlamadan önce aşağıdaki ön koşulların mevcut olduğundan emin olun:

1. Java Geliştirme Ortamı: Sisteminizde Java Geliştirme Kiti'nin (JDK) yüklü olduğundan emin olun.

2.  Java Kütüphanesi için Aspose.HTML: Java projenize Aspose.HTML for Java kütüphanesini indirmeniz ve eklemeniz gerekir. Kütüphaneyi şurada bulabilirsiniz:[Burada](https://releases.aspose.com/html/java/).

3. Giriş HTML Dosyası: Oluşturmak istediğiniz bir HTML dosyası hazırlayın ve XPS sayfa boyutunu ayarlayın. Bu eğitim için kendi HTML dosyanızı kullanabilirsiniz.

## Paketleri İçe Aktar

Öncelikle, Java için Aspose.HTML ile çalışmak için gerekli paketleri içe aktarmanız gerekir. Bu paketleri Java sınıfınızın başına ekleyin:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Adım 1: Giriş Dosyası Adını Ayarlayın

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 Bu adımda, HTML giriş dosyanızı bir`FileInputStream`.

## Adım 2: Bir HTML Belgesi Oluşturun ve Stilleri Ayarlayın

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 Bu adım, bir`HTMLDocument` ve buna stiller ekleniyor.

## Adım 3: XPS İşleme Seçenekleri Oluşturun

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Burada, render sürecini yapılandırmak için XPS render seçenekleri oluşturuyoruz.

## Adım 4: Sayfa Boyutunu Ayarlayın

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

Bu adım, sayfa boyutunu ayarlamayı ve en geniş sayfaya ayarlanıp ayarlanmayacağını belirtmeyi içerir.

## Adım 5: Çıktıyı Oluşturun

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

Son adımda, yapılandırılmış seçenekleri kullanarak XPS çıktısını oluşturuyoruz.

## Çözüm

Bu eğitimde, Java için Aspose.HTML kullanarak XPS sayfa boyutunu nasıl ayarlayacağınızı gösterdik. XPS belgelerinizin çıktı boyutlarını kontrol edebilir, belirli gereksinimlerinizi karşıladıklarından emin olabilirsiniz. Sağlanan kod ve adımlarla, bu özelliği Java uygulamalarınızda kolayca uygulayabilirsiniz.

 Herhangi bir sorunuz varsa veya daha fazla yardıma ihtiyacınız varsa, lütfen şu adresi ziyaret edin:[Java için Aspose.HTML belgeleri](https://reference.aspose.com/html/java/) veya yardım isteyin[Aspose Forum](https://forum.aspose.com/).

## SSS

### S1: Java için Aspose.HTML nedir?

A1: Aspose.HTML for Java, geliştiricilerin HTML belgelerini XPS, PDF ve resim gibi çeşitli biçimlere dönüştürmesine ve düzenlemesine olanak tanıyan bir Java kütüphanesidir.

### S2: Java için Aspose.HTML'yi nereden indirebilirim?

 A2: Java kütüphanesi için Aspose.HTML'yi şu adresten indirebilirsiniz:[bu bağlantı](https://releases.aspose.com/html/java/).

### S3: Aspose.HTML for Java için ücretsiz deneme sürümü mevcut mu?

 A3: Evet, Java için Aspose.HTML'nin ücretsiz deneme sürümünü şu adresten edinebilirsiniz:[Burada](https://releases.aspose.com/).

### S4: Java için Aspose.HTML için geçici lisansı nasıl alabilirim?

 A4: Java için Aspose.HTML için geçici bir lisans almak için şu adresi ziyaret edin:[bu sayfa](https://purchase.aspose.com/temporary-license/).

### S5: Java için Aspose.HTML desteği alabilir miyim?

 C5: Evet, Aspose topluluğundan yardım ve destek alabilirsiniz.[Aspose Forum](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
