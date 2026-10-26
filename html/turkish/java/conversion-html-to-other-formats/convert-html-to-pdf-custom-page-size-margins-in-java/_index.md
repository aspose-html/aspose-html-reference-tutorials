---
category: general
date: 2026-04-03
description: Aspose.HTML'i Java'da kullanarak HTML'yi PDF'ye dönüştürün; özel PDF
  sayfa boyutu, PDF kenar boşluklarını ayarlayın ve PDF sayfa genişliğini belirleyin.
  HTML'yi hızlı bir şekilde nasıl dönüştüreceğinizi öğrenin.
draft: false
keywords:
- convert html to pdf
- custom pdf page size
- set pdf margins
- how to convert html
- set pdf page width
language: tr
og_description: Aspose.HTML kullanarak Java'da HTML'yi PDF'ye dönüştürün. Bu kılavuz,
  mükemmel sonuçlar için özel PDF sayfa boyutu, kenar boşlukları ve sayfa genişliğini
  nasıl ayarlayacağınızı gösterir.
og_title: HTML'yi PDF'ye Dönüştür – Java'da Özel Sayfa Boyutu ve Kenar Boşlukları
tags:
- Java
- PDF
- Aspose.HTML
title: HTML'yi PDF'ye Dönüştür – Java'da Özel Sayfa Boyutu ve Kenar Boşlukları
url: /tr/java/conversion-html-to-other-formats/convert-html-to-pdf-custom-page-size-margins-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'yi PDF'ye Dönüştür – Java'da Özel Sayfa Boyutu ve Kenar Boşlukları

Hiç **HTML'yi PDF'ye dönüştürmek** ve sayfa boyutlarını nasıl kontrol edeceğinizi merak ettiniz mi? Bu öğreticide, **HTML'yi PDF'ye dönüştürmek** için *özel bir PDF sayfa boyutu* kullanarak, **PDF kenar boşluklarını ayarlamayı** ve hatta Aspose.HTML for Java kullanarak **PDF sayfa genişliğini ayarlamayı** gösteren tam, çalıştırmaya hazır bir çözümü adım adım anlatacağız.

Faturalar, raporlar veya e‑kitaplar oluşturuyorsanız, bu düzen ayarlamaları, metnin sade bir dökümü ile istediğiniz gibi tam olarak görünen cilalı bir belge arasındaki farkı yaratır.

## Öğrenecekleriniz

* Aspose.HTML ile basit bir Maven/Gradle projesi nasıl kurulur.
* Doğru sayfa boyutunu seçmenin baskı ve ekran render'ı için neden önemli olduğu.
* Yükseklik, genişlik ve kenar boşluklarını özelleştirerek **HTML'yi PDF'ye dönüştürmek** için adım adım kod.
* Yaygın tuzaklar (örneğin eksik CSS medya sorguları) ve bunlardan nasıl kaçınılacağı.
* PDF'nin doğru şekilde oluşturulduğunu nasıl doğrulayacağınız.

Aspose ile ilgili önceden bir deneyim gerekmez—sadece temel bir Java IDE'si ve bir `main` metodunu çalıştırabilme yeteneği.

## Önkoşullar

* **Java 17** (veya herhangi bir yeni JDK) makinenize kurulu.  
* **Aspose.HTML for Java** kütüphanesi – en son JAR'ı Maven Central'dan alabilirsiniz (`com.aspose:aspose-html:23.9` yazıldığı zaman).  
* PDF'ye dönüştürmek istediğiniz basit bir HTML dosyası (`input.html`).  
* İsteğe bağlı: PDF çıktısını önizlemek isterseniz bir görüntü düzenleyici.

> **Pro ipucu:** Maven kullanıyorsanız, aşağıdaki bağımlılığı `pom.xml` dosyanıza ekleyin. Gradle tercih ediyorsanız, aynı koordinatlar `implementation` yapılandırmasıyla çalışır.

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

```groovy
// Gradle
implementation 'com.aspose:aspose-html:23.9'
```

## HTML'yi PDF'ye Dönüştür – Projeyi Kurma

İlk olarak: `PdfConversionAdvanced` adlı yeni bir Java sınıfı oluşturun. Bu sınıf tüm dönüşüm mantığını tutacak. İhtiyacınız olan import'lar dosyanın en üstünde listelenmiştir—doğrudan kopyalayıp yapıştırabilirsiniz.

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.converters.pdf.*;

public class PdfConversionAdvanced {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1: Point to the source HTML file you want to convert.
        // -----------------------------------------------------------------
        String inputHtmlPath = "YOUR_DIRECTORY/input.html";

        // -----------------------------------------------------------------
        // Step 2: Create PdfSaveOptions and configure custom page size.
        // -----------------------------------------------------------------
        PdfSaveOptions pdfOptions = new PdfSaveOptions();

        // A5 size in points (1 pt = 1/72 inch). Adjust as needed.
        pdfOptions.setPageWidth(420);   // set pdf page width
        pdfOptions.setPageHeight(595);  // set pdf page height

        // -----------------------------------------------------------------
        // Step 3: Define margins – 10 mm ≈ 28.35 points.
        // -----------------------------------------------------------------
        pdfOptions.setMarginTop(28.35);
        pdfOptions.setMarginBottom(28.35);
        pdfOptions.setMarginLeft(28.35);
        pdfOptions.setMarginRight(28.35);

        // -----------------------------------------------------------------
        // Step 4: Make sure the converter uses the "print" media type.
        // -----------------------------------------------------------------
        pdfOptions.setMediaType("print");

        // -----------------------------------------------------------------
        // Step 5: Perform the conversion.
        // -----------------------------------------------------------------
        String outputPdfPath = "YOUR_DIRECTORY/output.pdf";
        Converter.convert(inputHtmlPath, outputPdfPath, pdfOptions);

        // -----------------------------------------------------------------
        // Step 6: Confirm the file was created.
        // -----------------------------------------------------------------
        System.out.println("PDF created with custom layout at " + outputPdfPath);
    }
}
```

### Bu Ayarların Önemi

* **Custom PDF page size** (`setPageWidth` / `setPageHeight`) A5, Letter veya ihtiyacınız olan herhangi bir özel boyutu hedeflemenizi sağlar. Bunu atlamanız durumunda, Aspose varsayılan olarak A4 kullanır; bu kağıt israfına ya da tasarımın bozulmasına yol açabilir.
* **Set PDF margins** içeriğin sayfa kenarlarına yapışmasını engeller—yazdırılamayan bir kenar boşluğu gerektiren yazıcılar için kritiktir.
* **Media type “print”** motorun tanımladığınız herhangi bir `@media print` CSS'yi uygulamasını zorlar, böylece ekran görünümünden farklı olarak fontlar, renkler ve düzen üzerinde ince ayar yapabilirsiniz.

## Özel Bir PDF Sayfa Boyutu Tanımlama

Varsayılan A4 boyutu projeniz için uygun değilse, istediğiniz herhangi bir boyutu kullanabilirsiniz. Yukarıdaki kod parçacığı zaten klasik bir A5 düzeni gösteriyor, ancak birkaç alternatif inceleyelim:

| Boyut | Genişlik (pt) | Yükseklik (pt) |
|------|------------|------------|
| **Letter** | 612 | 792 |
| **Legal** | 612 | 1008 |
| **Custom 8×10 inches** | 576 | 720 |

Özel bir boyut uygulamak için, `setPageWidth` ve `setPageHeight`'e geçirilen değerleri değiştirmeniz yeterlidir. Unutmayın: **1 point = 1/72 inç**, bu yüzden hızlı bir çarpma işlemi doğru sayıları verir.

> **Not:** Portre‑yönünden manzara‑yönüne geçiş yapmanız gerekiyorsa, sadece genişlik ve yükseklik değerlerini değiştirin.

## Kesin Düzen İçin PDF Kenar Boşluklarını Ayarlama

Kenar boşlukları da puan cinsinden ifade edilir. Örnek, tüm kenarlarda **10 mm** (≈ 28.35 pt) kullanır. Daha sıkı bir düzen mi istiyorsunuz? Sayıları değiştirin:

```java
pdfOptions.setMarginTop(14.18);    // 5 mm
pdfOptions.setMarginBottom(14.18);
pdfOptions.setMarginLeft(21.26);   // 7.5 mm
pdfOptions.setMarginRight(21.26);
```

Neden uğraşasınız? Yazıcıların çoğu minimum bir yazdırılabilir alana sahiptir—kenar boşlukları ayarlamak içeriğin kesilmesini önler. Ayrıca, tutarlı bir kenar boşluğu PDF'nize profesyonel bir görünüm kazandırır, özellikle sözleşme veya sertifika oluştururken.

## PDF Sayfa Genişliğini (ve Yüksekliğini) Dinamik Olarak Ayarlama

Bazen aldığınız HTML zaten bir genişlik ipucu içerir (ör. 800 px olarak stil verilen bir `<div>`). Gerekli PDF genişliğini anında hesaplayabilirsiniz:

```java
int htmlWidthPx = 800;                     // example from HTML
double pointsPerPixel = 0.75;              // 96 DPI => 0.75 pt per pixel
pdfOptions.setPageWidth(htmlWidthPx * pointsPerPixel);
```

Bu teknik, PDF'nin orijinal düzeni bozulmadan yansıtılmasını sağlar. Ekran görüntüsü için tasarlanmış **HTML'yi nasıl dönüştürürsünüz** konusunda kullanışlı bir hiledir.

## Dönüşümü Çalıştırın ve Çıktıyı Doğrulayın

Her şeyi ayarladıktan sonra `main` metodunu çalıştırın. Her şey doğru bağlandıysa, şunu göreceksiniz:

```
PDF created with custom layout at YOUR_DIRECTORY/output.pdf
```

Oluşan PDF'yi herhangi bir görüntüleyicide (Adobe Reader, Chrome veya işletim sisteminizin önizleme uygulaması) açın. Şunları görmelisiniz:

* Tanımladığınız tam sayfa boyutu.
* İçeriğin etrafında eşit kenar boşlukları.
* `setMediaType("print")` sayesinde sayfa yazdırılmış gibi CSS uygulanmış.

![HTML'yi PDF'ye Dönüştür örnek çıktısı](https://example.com/convert-html-to-pdf-output.png "HTML'yi PDF'ye dönüştür örnek çıktısı")

*Görsel alt metni SEO için ana anahtar kelimeyi içerir.*

## Yaygın Kenar Durumları ve Nasıl Ele Alınır

| Sorun | Semptom | Çözüm |
|-------|---------|-----|
| **CSS Eksik** | Metin sade görünüyor, font veya renk yok. | `pdfOptions.setMediaType("print")` ayarlandığından ve HTML'nizin stil sayfasına mutlak bir yol ile bağlandığından veya CSS'i satır içi gömdüğünden emin olun. |
| **Büyük Görseller Kesiliyor** | Görseller sayfa kenarlarında kesiliyor. | HTML'deki görselleri yeniden boyutlandırın veya DPI'yi artırmak için `pdfOptions.setImageResolution(300)` ayarlayın, ardından kenar boşluklarını düzenleyin. |
| **Unicode Karakterler Görüntülenmiyor** | Özel semboller kutu olarak görünüyor. | Karakterleri destekleyen bir font ekleyin ve CSS'inizde (`@font-face`) referans verin. |
| **Büyük Belgelerde Performans Gecikmesi** | Dönüşüm 30 saniyeden uzun sürüyor. | `pdfOptions.setEnableThreading(true)` kullanın (destekleniyorsa) veya HTML'yi daha küçük parçalara bölüp PDF'leri sonradan birleştirin. |

## Tam Çalışan Örnek (Hepsi Bir Arada)

İşte yeni bir projeye ekleyebileceğiniz tam dosya. `YOUR_DIRECTORY` ifadesini makinenizdeki gerçek bir klasör yolu ile değiştirin.

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.converters.pdf.*;

public class PdfConversionAdvanced {
    public static void main(String[] args) throws Exception {

        // Step 1: Source HTML location
        String inputHtmlPath = "C:/pdf-demo/input.html";

        // Step 2: Configure PDF options – custom size and margins
        PdfSaveOptions pdfOptions = new PdfSaveOptions();
        pdfOptions.setPageWidth(420);   // custom pdf page width (A5)
        pdfOptions.setPageHeight(595);  // custom pdf page height (A5)

        // Set margins – 10 mm ≈ 28.35 pt
        pdfOptions.setMarginTop(28.35);
        pdfOptions.setMarginBottom(28.35);
        pdfOptions.setMarginLeft(28.35);
        pdfOptions.setMarginRight(28.35);

        // Ensure print CSS is used
        pdfOptions.setMediaType("print");

        // Step 3: Destination PDF file
        String outputPdfPath = "C:/pdf-demo/output.pdf";

        // Step 4: Perform conversion
        Converter.convert(inputHtmlPath, outputPdfPath, pdfOptions);

        // Step 5: Confirmation
        System.out.println("PDF created with custom layout at " + outputPdfPath);
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}