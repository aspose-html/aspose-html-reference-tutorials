---
title: Java için Aspose.HTML ile PDF Sayfa Boyutunu Ayarlayın
linktitle: PDF Sayfa Boyutunu Ayarlama
second_title: Aspose.HTML ile Java HTML İşleme
description: Java için Aspose.HTML ile PDF sayfa boyutunu nasıl ayarlayacağınızı öğrenin. HTML'den zahmetsizce yüksek kaliteli PDF'ler oluşturun. Sayfa boyutlarını etkili bir şekilde kontrol edin.
type: docs
weight: 15
url: /tr/java/advanced-usage/adjust-pdf-page-size/
---

Günümüzün dijital çağında, HTML içeriklerinden yüksek kaliteli PDF'ler üretme ihtiyacı artmaktadır. Aspose.HTML for Java, HTML belgelerini zahmetsizce PDF formatına dönüştürmenize olanak tanıyan güçlü bir Java kütüphanesidir. Bu eğitimde, Aspose.HTML for Java kullanarak HTML'yi PDF'ye dönüştürürken sayfa boyutunu ayarlamaya odaklanacağız.

## Ön koşullar

Başlamadan önce aşağıdaki ön koşulların mevcut olduğundan emin olun:

- Java Geliştirme Ortamı: Sisteminizde Java Geliştirme Kiti'nin (JDK) yüklü olduğundan emin olun.
-  Java için Aspose.HTML: Web sitesinden Java için Aspose.HTML'yi indirip yüklemeniz gerekiyor[Burada](https://releases.aspose.com/html/java/).
- HTML Belgesi: Dönüştürmeye hazır bir HTML belgeniz olmalı. Yoksa, bir tane oluşturun veya mevcut bir HTML dosyasını kullanın.

## Paketleri İçe Aktar

Başlamak için, Java için Aspose.HTML ile çalışmak için gerekli paketleri içe aktarmanız gerekir. Aşağıdaki kod parçacığı bunu nasıl yapacağınızı gösterir:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

Artık ön koşullara sahip olduğunuza ve gerekli paketleri içe aktardığınıza göre, PDF sayfa boyutunu ayarlama sürecini birden fazla adıma bölelim:

## Adım 1: HTML İçeriğini Okuma

Öncelikle, PDF'ye dönüştürmek istediğiniz HTML içeriğini okumanız gerekir. Bu örnekte, "FirstFile.html" adlı bir dosyadan HTML'yi okuyacağız.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Adım 2: HTML İçeriği Yazma

Daha sonra HTML içeriğini "FirstFileOut.html" adlı bir dosyaya yazacaksınız.

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Buraya özel HTML stilleri veya içerik ekleyin
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## Adım 3: HTML'yi PDF'ye dönüştürme

Şimdi, HTML içeriğini bir PDF dosyasına dönüştüreceksiniz. İki senaryoyu ele alacağız: birincisi sayfa boyutunun içerik genişliğine göre ayarlanmadığı senaryo, diğeri ise ayarlandığı senaryo.

### Sayfa Boyutu Ayarlanmamış

Bu senaryoda sayfa boyutu sabit bir genişliğe ve yüksekliğe ayarlanır ve bu boyutları aşarsa içerik kırpılabilir.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// HTML dosyasından bir HTMLDocument örneği oluşturun
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// PDF oluşturma seçeneklerini ayarlayın
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Çıktıyı oluştur
pdf_renderer.render(device, html_document);
```

### Sayfa Boyutu İçerik Genişliğine Göre Ayarlandı

Bu senaryoda sayfa boyutu içerik genişliğine göre ayarlanır.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Çıktıyı oluştur
pdf_renderer.render(device, html_document);
```

## Çözüm

Bu eğitimde, Aspose.HTML for Java kullanarak HTML'yi PDF'ye dönüştürürken PDF sayfa boyutunun nasıl ayarlanacağını inceledik. Ön koşulları öğrendiniz, gerekli paketleri içe aktardınız ve bu görevi başarmak için adım adım bir kılavuzu takip ettiniz. Aspose.HTML for Java ile, oluşturulan PDF'lerinizin sayfa boyutunu kolayca kontrol edebilir ve içeriğinizin amaçlandığı gibi görüntülenmesini sağlayabilirsiniz.

 Belirli gereksinimlerinizi karşılamak için farklı sayfa boyutları ve ayarları denemekten çekinmeyin. Herhangi bir sorunla karşılaşırsanız veya başka sorularınız varsa, yardım istemekten çekinmeyin[Java için Aspose.HTML belgeleri](https://reference.aspose.com/html/java/) veya[Aspose destek forumu](https://forum.aspose.com/).

## SSS

### S1: Java için Aspose.HTML nedir?

A1: Java için Aspose.HTML, HTML belgeleriyle çalışmanıza, bunları düzenlemenize, dönüştürmenize ve PDF de dahil olmak üzere çeşitli biçimlere dönüştürmenize olanak tanıyan bir Java kütüphanesidir.

### S2: Aspose.HTML for Java ile HTML'yi PDF'ye dönüştürürken PDF sayfa boyutunu nasıl ayarlayabilirim?

 A2: PDF sayfa boyutunu,`PageSetup` sınıf ve ayarlama`AdjustToWidestPage` mülk`true` veya ihtiyaçlarınıza bağlı olarak `false`.

### S3: HTML içeriğini PDF'e dönüştürmeden önce stilini özelleştirebilir miyim?

C3: Evet, eğitimde gösterildiği gibi, HTML içeriğinizi PDF'e dönüştürmeden önce CSS ve HTML öğelerini ekleyerek stili özelleştirebilirsiniz.

### S4: Java için Aspose.HTML belgelerini nerede bulabilirim?

 A4: Belgelere başvurabilirsiniz[Burada](https://reference.aspose.com/html/java/) Kapsamlı bilgi ve örnekler için.

### S5: Aspose.HTML for Java için ücretsiz deneme sürümü mevcut mu?

 C5: Evet, Java için Aspose.HTML'nin ücretsiz deneme sürümüne şu adresten erişebilirsiniz:[bu bağlantı](https://releases.aspose.com/).