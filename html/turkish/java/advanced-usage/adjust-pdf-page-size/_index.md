---
date: 2025-12-01
description: Aspose.HTML for Java kullanarak PDF sayfa boyutunu nasıl ayarlayacağınızı,
  HTML'yi PDF olarak nasıl render edeceğinizi ve HTML'den PDF oluşturacağınızı öğrenin.
  Sayfa boyutlarını kolayca kontrol edin.
linktitle: Adjusting PDF Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML for Java ile PDF Sayfa Boyutunu Ayarlayın
url: /tr/java/advanced-usage/adjust-pdf-page-size/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML for Java ile PDF Sayfa Boyutunu Ayarlama

HTML'den PDF oluşturmak, raporlar, faturalar ve e‑kitaplar için yaygın bir gereksinimdir. **PDF sayfa boyutunu ayarladığınızda**, son belgenin HTML'de tasarladığınız düzenle eşleşmesini sağlarsınız. Bu öğreticide, HTML'yi PDF olarak nasıl oluşturacağınızı, özel boyutlar nasıl ayarlayacağınızı ve sayfanın en geniş içeriğe otomatik olarak genişleyip genişlemeyeceğini nasıl kontrol edeceğinizi öğreneceksiniz. Aspose.HTML for Java kullanarak eksiksiz, uygulamalı bir örnek üzerinden ilerleyeceğiz.

## Hızlı Yanıtlar
- **“PDF sayfa boyutunu ayarlama” ne anlama geliyor?** Her PDF sayfasının genişliğini ve yüksekliğini tanımlamanızı sağlar veya renderlayıcının en geniş öğeye otomatik olarak uyum sağlamasına izin verir.  
- **Hangi kütüphane kullanılıyor?** Aspose.HTML for Java (en son sürüm).  
- **Lisans gerekli mi?** Geliştirme için ücretsiz deneme sürümü yeterlidir; üretim için ticari lisans gereklidir.  
- **Boyutları programlı olarak değiştirebilir miyim?** Evet – `PageSetup` ve `AdjustToWidestPage` özelliğini kullanın.  
- **Java 8+ ile uyumlu mu?** Kesinlikle – API, JDK 8 ve üzerindeki tüm sürümlerle çalışır.

## “PDF sayfa boyutunu ayarlama” nedir?
PDF sayfa boyutunu ayarlamak, HTML renderlayıcısının oluşturduğu her sayfanın boyutlarını yapılandırmak anlamına gelir. Sabit bir boyut (ör. A4, Letter) belirleyebilir veya renderlayıcının içeriğe göre optimal genişliği hesaplamasına izin verebilirsiniz. Bu, düzen, sayfalama ve görsel doğruluk üzerinde kesin kontrol sağlar.

## HTML'yi PDF'ye dönüştürürken PDF sayfa boyutunu neden ayarlamalısınız?
- **Tasarım amacını koruma:** İçeriğin kesilmesini veya uzatılmasını önler.  
- **Baskı için optimize et:** Sonraki süreçlerde gereken kağıt boyutuyla eşleşir.  
- **Okunabilirliği artır:** Aşırı boşluk veya sıkışık metinlerden kaçınır.  
- **Dinamik belgeler:** Geniş tabloları veya görselleri manuel hesaplama yapmadan otomatik olarak sığdırır.

## Önkoşullar
Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

- **Java Development Kit (JDK) 8 veya daha üstü** makinenizde kurulu.  
- **Aspose.HTML for Java** – en son JAR dosyasını [resmi sürüm sayfasından](https://releases.aspose.com/html/java/) indirin.  
- **Dönüştürmek istediğiniz bir HTML dosyası** (örnekte `FirstFile.html` dosyasını kullanacağız).

## Paketleri İçe Aktarma
İlk olarak, ihtiyacımız olan sınıfları içe aktarın. Aşağıdaki kod bloğu orijinal öğreticiden değiştirilmemiştir.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

## Adım 1: HTML İçeriğini Oku
`FileInputStream` kullanarak kaynak HTML dosyasını okuruz. Bu adım, ham işaretlemenin sonraki işlemler için hazırlanmasını sağlar.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Adım 2: HTML'i Yaz (ve isteğe bağlı olarak zenginleştir)
Burada orijinal HTML'i yeni bir dosyaya kopyalıyor ve stilin PDF çıktısını nasıl etkilediğini göstermek için birkaç satır içi stil ekliyoruz. Örnek CSS'i kendi stilinizle değiştirmekten çekinmeyin.

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Add custom HTML styles or content here
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

## Adım 3: HTML'i PDF'ye Renderla – İki Senaryo
Şimdi **HTML'den PDF oluşturma** işlemini iki farklı sayfa boyutu stratejisiyle göreceğiz.

### 3.1 Sayfa boyutu içeriğin genişliğine AYARLANMAMIŞ
Bu durumda sayfa boyutlarını (100 × 100 point) sabitleriz. Herhangi bir öğe bu sınırları aşarsa kırpılacaktır.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Create an HTMLDocument instance from the HTML file
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Set PDF rendering options
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

### 3.2 Sayfa boyutu içeriğin genişliğine AYARLANMIŞ
Burada `AdjustToWidestPage` özelliğini etkinleştiririz, böylece renderlayıcı en geniş öğeyi sığdırmak için sayfa genişliğini otomatik olarak genişletir, yüksekliği sabit tutar.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

## Kod içinde PDF boyutlarını (PDF sayfa boyutunu nasıl değiştiririz) ayarlama
`PageSetup` nesnesi anahtar:

- `setAnyPage(Page page)`: temel genişlik × yüksekliği tanımlar.  
- `setAdjustToWidestPage(boolean)`: otomatik genişlemeyi açar/kapatır.  

Bu iki özelliği ayarlayarak, statik bir A4 sayfasına ya da HTML düzeninizi takip eden dinamik bir genişliğe ihtiyacınız olsun, **PDF boyutlarını nasıl ayarlayacağınızı** her senaryo için yapabilirsiniz.

## Yaygın Sorunlar ve İpuçları
| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|------|
| İçerik kesiliyor | Sabit boyut çok küçük | `Size` değerlerini artırın veya `AdjustToWidestPage` özelliğini etkinleştirin. |
| Metin bulanık görünüyor | Render DPI varsayılanı düşük | Kaliteyi artırmak için `PdfRenderingOptions.setResolution(int dpi)` kullanın. |
| Stiller eksik | Harici CSS yüklenmedi | CSS'i satır içi gömün veya `HTMLDocument.setBaseUrl()` ile stil sayfası klasörünü gösterin. |
| Büyük HTML dosyaları OutOfMemoryError hatası verir | Renderlayıcı tüm belgeyi belleğe yüklüyor | Belgeyi parçalar halinde işleyin veya JVM yığın boyutunu artırın (`-Xmx`). |

## Sıkça Sorulan Sorular

**S: Aspose.HTML for Java nedir?**  
C: HTML belgeleri oluşturmanıza, düzenlemenize ve renderlamanıza olanak tanıyan bir Java kütüphanesidir; PDF, PNG ve diğer formatlara dönüştürme dahil.

**S: Aspose.HTML for Java ile HTML'yi PDF'ye dönüştürürken PDF sayfa boyutunu nasıl ayarlayabilirim?**  
C: `PageSetup` sınıfını kullanın ve `AdjustToWidestPage` özelliğini `true` (otomatik boyut) veya `false` (sabit boyut) olarak ayarlayın. Ardından istediğiniz `Size` değerini `new Page(new Size(width, height))` ile atayın.

**S: HTML içeriğinin stilini PDF'ye dönüştürmeden önce özelleştirebilir miyim?**  
C: Evet – CSS ekleyebilir, DOM'u değiştirebilir veya harici stil sayfaları kullanabilirsiniz. Öğreticide satır içi CSS enjeksiyonu gösterilmiştir.

**S: Aspose.HTML for Java belgelerine nereden ulaşabilirim?**  
C: Kapsamlı dokümantasyon [burada](https://reference.aspose.com/html/java/) mevcuttur.

**S: Aspose.HTML for Java için ücretsiz deneme sürümü var mı?**  
C: Kesinlikle – deneme sürümünü [sürüm sayfasından](https://releases.aspose.com/html/java/) indirebilirsiniz.

## Sonuç
Artık Aspose.HTML for Java kullanarak **PDF sayfa boyutunu nasıl ayarlayacağınızı**, **HTML'yi PDF olarak nasıl renderlayacağınızı** ve **özel PDF boyutlarını nasıl belirleyeceğinizi** biliyorsunuz. Farklı sayfa boyutları, DPI ayarları ve CSS ince ayarlarıyla denemeler yaparak çıktıyı kendi kullanım senaryonuza göre mükemmelleştirin. Zorluklarla karşılaşırsanız resmi dokümantasyona veya Aspose destek forumlarına başvurun.

---

**Son Güncelleme:** 2025-12-01  
**Test Edilen Versiyon:** Aspose.HTML for Java 24.12 (en son)  
**Yazar:** Aspose  
**İlgili Kaynaklar:** [API Referansı](https://reference.aspose.com/html/java/) | [Ücretsiz Deneme İndir](https://releases.aspose.com/html/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}