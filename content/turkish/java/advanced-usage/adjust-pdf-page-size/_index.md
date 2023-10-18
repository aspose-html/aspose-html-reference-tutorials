---
title: Aspose.HTML for Java ile PDF Sayfa Boyutunu Ayarlama
linktitle: PDF Sayfa Boyutunu Ayarlama
second_title: Aspose.HTML ile Java HTML İşleme
description: Aspose.HTML for Java ile PDF sayfa boyutunu nasıl ayarlayacağınızı öğrenin. Zahmetsizce HTML'den yüksek kaliteli PDF'ler oluşturun. Sayfa boyutlarını etkili bir şekilde kontrol edin.
type: docs
weight: 15
url: /tr/java/advanced-usage/adjust-pdf-page-size/
---

Günümüzün dijital çağında, HTML içeriğinden yüksek kaliteli PDF'ler oluşturma ihtiyacı artıyor. Aspose.HTML for Java, HTML belgelerini zahmetsizce PDF formatına dönüştürmenize olanak tanıyan güçlü bir Java kütüphanesidir. Bu eğitimde Aspose.HTML for Java kullanarak HTML'yi PDF'ye dönüştürürken sayfa boyutunu ayarlamaya odaklanacağız.

## Önkoşullar

Başlamadan önce aşağıdaki önkoşulların mevcut olduğundan emin olun:

- Java Geliştirme Ortamı: Sisteminizde Java Geliştirme Kitinin (JDK) kurulu olduğundan emin olun.
-  Aspose.HTML for Java: Aspose.HTML for Java'yı web sitesinden indirip yüklemeniz gerekir.[Burada](https://releases.aspose.com/html/java/).
- HTML Belgesi: Dönüşüme hazır bir HTML belgeniz olmalıdır. Değilse, bir tane oluşturun veya mevcut bir HTML dosyasını kullanın.

## Paketleri İçe Aktar

Başlamak için Aspose.HTML for Java ile çalışmak üzere gerekli paketleri içe aktarmanız gerekir. Aşağıdaki kod parçacığı bunun nasıl yapılacağını gösterir:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

Artık önkoşulları yerine getirdiğinize ve gerekli paketleri içe aktardığınıza göre, PDF sayfa boyutunu ayarlama sürecini birden fazla adıma ayıralım:

## 1. Adım: HTML İçeriğini Okumak

Öncelikle PDF'ye dönüştürmek istediğiniz HTML içeriğini okumanız gerekir. Bu örnekte HTML'yi "FirstFile.html" adlı bir dosyadan okuyacağız.

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
    // Buraya özel HTML stilleri veya içeriği ekleyin
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

## 3. Adım: HTML'yi PDF'ye dönüştürme

Şimdi HTML içeriğini bir PDF dosyasına dönüştüreceksiniz. İki senaryoyu ele alacağız: Biri sayfa boyutunun içerik genişliğine göre ayarlanmadığı, diğeri ayarlandığı senaryo.

### Sayfa Boyutu Ayarlanmadı

Bu senaryoda sayfa boyutu sabit bir genişliğe ve yüksekliğe ayarlanmıştır; bu boyutların aşılması durumunda içerik kırpılabilir.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// HTML dosyasından bir HTMLDocument örneği oluşturma
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// PDF oluşturma seçeneklerini ayarlama
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

Bu eğitimde Aspose.HTML for Java kullanarak HTML'yi PDF'ye dönüştürürken PDF sayfa boyutunun nasıl ayarlanacağını araştırdık. Bu görevi gerçekleştirmek için önkoşulları öğrendiniz, gerekli paketleri içe aktardınız ve adım adım kılavuzu izlediniz. Aspose.HTML for Java ile, oluşturduğunuz PDF'lerin sayfa boyutunu kolayca kontrol edebilir, içeriğinizin istediğiniz gibi görüntülendiğinden emin olabilirsiniz.

 Özel gereksinimlerinizi karşılamak için farklı sayfa boyutları ve ayarlarıyla denemeler yapmaktan çekinmeyin. Herhangi bir sorunla karşılaşırsanız veya başka sorularınız varsa, yardım istemekten çekinmeyin.[Java belgeleri için Aspose.HTML](https://reference.aspose.com/html/java/) ya da[Aspose destek forumu](https://forum.aspose.com/).

## SSS'ler

### S1: Java için Aspose.HTML nedir?

Cevap1: Aspose.HTML for Java, HTML belgeleriyle çalışmanıza, bunları değiştirmenize, dönüştürmenize ve PDF dahil çeşitli formatlara dönüştürmenize olanak tanıyan bir Java kitaplığıdır.

### S2: Aspose.HTML for Java ile HTML'yi PDF'ye dönüştürürken PDF sayfa boyutunu nasıl ayarlayabilirim?

 Cevap 2: PDF sayfa boyutunu, düğmesini kullanarak ayarlayabilirsiniz.`PageSetup` sınıf ve ayarlama`AdjustToWidestPage` mülkiyet`true` veya 'yanlış, gereksinimlerinize bağlı olarak.

### S3: HTML içeriğinin stilini PDF'ye dönüştürmeden önce özelleştirebilir miyim?

C3: Evet, öğreticide gösterildiği gibi, PDF'ye dönüştürmeden önce HTML içeriğinize CSS ve HTML öğeleri ekleyerek stili özelleştirebilirsiniz.

### S4: Aspose.HTML for Java belgelerini nerede bulabilirim?

 A4: Belgelere başvurabilirsiniz[Burada](https://reference.aspose.com/html/java/) Kapsamlı bilgi ve örnekler için.

### S5: Aspose.HTML for Java'nın ücretsiz deneme sürümü mevcut mu?

 Cevap5: Evet, Aspose.HTML for Java'nın ücretsiz deneme sürümüne şu adresten erişebilirsiniz:[bu bağlantı](https://releases.aspose.com/).