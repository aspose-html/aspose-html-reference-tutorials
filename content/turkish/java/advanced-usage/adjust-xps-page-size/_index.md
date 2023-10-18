---
title: Aspose.HTML for Java ile XPS Sayfa Boyutunu Ayarlayın
linktitle: XPS Sayfa Boyutunu Ayarlama
second_title: Aspose.HTML ile Java HTML İşleme
description: Aspose.HTML for Java ile XPS sayfa boyutunu nasıl ayarlayacağınızı öğrenin. XPS belgelerinizin çıktı boyutlarını kolayca kontrol edin.
type: docs
weight: 16
url: /tr/java/advanced-usage/adjust-xps-page-size/
---

Bu eğitimde, Aspose.HTML for Java'yı kullanarak XPS sayfa boyutunu ayarlama sürecinde size rehberlik edeceğiz. Bu güçlü kitaplık, HTML belgelerini değiştirmenize ve bunları XPS dahil çeşitli formatlara dönüştürmenize olanak tanır. XPS belgenizin çıktı boyutlarını kontrol etmeniz gerektiğinde sayfa boyutunu ayarlamak çok önemlidir.

## Önkoşullar

Başlamadan önce aşağıdaki önkoşulların mevcut olduğundan emin olun:

1. Java Geliştirme Ortamı: Sisteminizde Java Geliştirme Kitinin (JDK) kurulu olduğundan emin olun.

2.  Aspose.HTML for Java Library: Aspose.HTML for Java kütüphanesini indirip Java projenize eklemeniz gerekir. Kütüphaneyi bulabilirsiniz[Burada](https://releases.aspose.com/html/java/).

3. HTML Dosyasını Girin: Oluşturmak istediğiniz bir HTML dosyası hazırlayın ve XPS sayfa boyutunu ayarlayın. Bu eğitim için kendi HTML dosyanızı kullanabilirsiniz.

## Paketleri İçe Aktar

Öncelikle Aspose.HTML for Java ile çalışmak için gerekli paketleri içe aktarmanız gerekir. Bu paketleri Java sınıfınızın başına ekleyin:

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

 Bu adımda, HTML giriş dosyanızı bir kullanarak okuyoruz.`FileInputStream`.

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

 Bu adım bir oluşturmayı içerir`HTMLDocument` ve ona stiller ekleme.

## 3. Adım: XPS İşleme Seçenekleri Oluşturun

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Burada render işlemini yapılandırmak için XPS render seçeneklerini oluşturuyoruz.

## 4. Adım: Sayfa Boyutunu Ayarlayın

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

Bu adım, sayfa boyutunun ayarlanmasını ve sayfanın en geniş sayfaya ayarlanıp ayarlanmayacağını belirtmeyi içerir.

## Adım 5: Çıktıyı Oluşturun

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

Son adımda, yapılandırılan seçenekleri kullanarak XPS çıktısını oluşturuyoruz.

## Çözüm

Bu eğitimde size Aspose.HTML for Java kullanarak XPS sayfa boyutunu nasıl ayarlayacağınızı gösterdik. XPS belgelerinizin çıktı boyutlarını kontrol ederek özel gereksinimlerinizi karşıladıklarından emin olabilirsiniz. Verilen kod ve adımlarla bu özelliği Java uygulamalarınızda kolaylıkla uygulayabilirsiniz.

 Herhangi bir sorunuz varsa veya daha fazla yardıma ihtiyacınız varsa, şu adresi ziyaret etmekten çekinmeyin:[Java belgeleri için Aspose.HTML](https://reference.aspose.com/html/java/) veya bu konuda yardım isteyin[Aspose Forumu](https://forum.aspose.com/).

## SSS'ler

### S1: Java için Aspose.HTML nedir?

Cevap1: Aspose.HTML for Java, geliştiricilerin HTML belgelerini XPS, PDF ve görüntüler gibi çeşitli formatlara dönüştürmesine ve değiştirmesine olanak tanıyan bir Java kitaplığıdır.

### S2: Aspose.HTML for Java'yı nereden indirebilirim?

 Cevap2: Aspose.HTML for Java kütüphanesini şu adresten indirebilirsiniz:[bu bağlantı](https://releases.aspose.com/html/java/).

### S3: Aspose.HTML for Java'nın ücretsiz deneme sürümü mevcut mu?

 Cevap3: Evet, Aspose.HTML for Java'nın ücretsiz deneme sürümünü şu adresten edinebilirsiniz:[Burada](https://releases.aspose.com/).

### S4: Aspose.HTML for Java için nasıl geçici lisans alabilirim?

 Cevap4: Aspose.HTML for Java'ya yönelik geçici bir lisans almak için şu adresi ziyaret edin:[bu sayfa](https://purchase.aspose.com/temporary-license/).

### S5: Aspose.HTML for Java desteği alabilir miyim?

 C5: Evet, Aspose topluluğundan yardım ve destek isteyebilirsiniz.[Aspose Forumu](https://forum.aspose.com/).