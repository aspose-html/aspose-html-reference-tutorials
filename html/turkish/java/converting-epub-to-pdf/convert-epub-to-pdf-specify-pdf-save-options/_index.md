---
date: 2026-05-30
description: Java'da Aspose.HTML kullanarak EPUB'ten PDF'ye dönüştürmeyi, özel bir
  PDF sayfa boyutu ve diğer PDF kaydetme seçeneklerini ayarlamayı öğrenin.
keywords:
- custom pdf page size
- convert epub to pdf
- change pdf background color
- specify pdf page dimensions
- aspose.html java
linktitle: EPUB'ten PDF'ye PDF Kaydetme Seçeneklerini Belirleme
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  headline: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  type: TechArticle
- description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  name: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  steps:
  - name: Open the EPUB File
    text: First, create a `FileInputStream` that points to your source `.epub`. Keeping
      the stream open until the conversion finishes prevents “blank page” errors.
  - name: Define PDF Save Options
    text: '`PdfSaveOptions` is Aspose.HTML''s configuration class that controls PDF
      output settings such as page size, background color, and margins. `Length.fromPixels`
      converts screen pixels to PDF points (1 point = 1/72 inch), allowing you to
      specify dimensions in familiar pixel units.'
  - name: Convert EPUB to PDF
    text: With the input stream and custom options ready, invoke the converter. The
      output PDF will be saved to the location you specify, preserving the exact page
      dimensions you defined. `PdfSaveOptions.setEnableParallelProcessing` is a method
      that enables parallel processing of pages during PDF conversion.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a commercial library, but you can obtain a free
      trial version from their [website](https://releases.aspose.com/).
    question: Is Aspose.HTML for Java a free library?
  - answer: Aspose.HTML for Java supports EPUB 2.0, EPUB 3.0, and EPUB 3.1, handling
      re‑flowable and fixed‑layout books with full CSS support.
    question: What EPUB formats are supported for conversion?
  - answer: Yes, you can customize the PDF output by adjusting the page setup, background
      color, compression level, and other settings in the `PdfSaveOptions`.
    question: Can I customize the PDF output further?
  - answer: The trial version may add a watermark to the first few pages and limits
      the maximum file size to 10 MB; purchase a license to remove these restrictions.
    question: Are there any limitations to the trial version of Aspose.HTML for Java?
  - answer: You can find answers to your questions and seek support on the [Aspose.HTML
      forum](https://forum.aspose.com/).
    question: Where can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Özel PDF Sayfa Boyutu - EPUB'ten PDF'ye PDF Kaydetme Seçeneklerini Belirleme
url: /tr/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Özel PDF Sayfa Boyutu: EPUB'ten PDF'ye PDF Kaydetme Seçeneklerini Belirleme

## Giriş

Aspose.HTML for Java, **EPUB'ten PDF'ye dönüştürmeyi** kolaylaştırır ve çıktının tam kontrolünü sağlar; buna **özel bir PDF sayfa boyutu** ayarlama da dahildir. Bu adım adım rehberde, ortamınızı hazırlamaktan `PdfSaveOptions`'ı ayarlamaya kadar ihtiyacınız olan her şeyi ele alacağız, böylece oluşturulan PDF, ihtiyaç duyduğunuz tam sayfa boyutlarıyla eşleşir. Yayınlama hattı, e‑öğrenme platformu oluşturuyor ya da sadece belge dönüşümünü otomatikleştirmeniz gerekiyorsa, burada bulunan teknikler sizin için değerli olacaktır.

## Hızlı Yanıtlar
- **Bu öğreticinin temel amacı nedir?** Özel bir PDF sayfa boyutu uygulayarak bir EPUB dosyasını PDF'ye dönüştürmek.  
- **Hangi kütüphane kullanılıyor?** Aspose.HTML for Java.  
- **Bir lisansa ihtiyacım var mı?** Ücretsiz deneme sürümü mevcuttur; üretim için ticari bir lisans gereklidir.  
- **Arka plan rengini değiştirebilir miyim?** Evet, `PdfSaveOptions` kullanarak.  
- **Java 8+ destekleniyor mu?** Kesinlikle—herhangi bir modern Java çalışma zamanı çalışır.

## Özel bir PDF sayfa boyutu nedir?

Özel bir PDF sayfa boyutu, A4 veya Letter gibi standart boyutlara güvenmek yerine, çıktı PDF'sindeki her sayfanın tam genişlik ve yüksekliğini tanımlamanıza olanak tanır.  
Boyutları puan cinsinden (1 puan = 1/72 inç) ayarlayabilir veya piksellerden dönüştürebilirsiniz; bu, nihai yerleşim üzerinde piksel‑tam kontrol sağlar. Bu, e‑kitaplar, broşürler veya önceden tanımlanmış bir formatla manuel işlem yapmadan eşleşmesi gereken herhangi bir tasarım için idealdir.

## EPUB'ten PDF'ye Dönüştürme için Aspose.HTML Neden Kullanılmalı?

Aspose.HTML, karmaşık düzenleri, gömülü yazı tiplerini ve yüksek çözünürlüklü görüntüleri koruyarak EPUB'u iki satır kodla PDF'ye dönüştürür. **50+ giriş ve çıkış formatını** destekler, **2.000 sayfaya** kadar PDF'yi tüm dosyayı belleğe yüklemeden işleyebilir ve Windows, Linux ve macOS'ta aynı sonuçlarla çalışır. Kütüphane ayrıca ayrıntılı PDF‑kaydetme seçenekleri sunar; sayfa boyutu, arka plan rengi, kenar boşlukları ve sıkıştırma ayarlarını Java üzerinden ayarlayabilirsiniz.

## Önkoşullar
- **Java Geliştirme Ortamı:** JDK 8 veya daha yeni bir sürüm yüklü ve yapılandırılmış.  
- **Aspose.HTML for Java:** En son JAR'ı [website](https://releases.aspose.com/html/java/) adresinden indirin.  
- **EPUB Dosyası:** Dönüştürmek istediğiniz bir `.epub` belgesi.  

Şimdi her şey hazır olduğuna göre, gerçek dönüşüm adımlarına dalalım.

## Özel bir sayfa boyutu ile EPUB'u PDF'ye nasıl dönüştürürsünüz?

`FileInputStream`, bir dosyadan ham baytları okuyan bir Java sınıfıdır.  
`PdfSaveOptions`, Aspose.HTML içinde PDF çıktısı ayarlarını (sayfa boyutu ve arka plan rengi gibi) yapılandıran bir sınıftır.  
EPUB'unuzu bir `FileInputStream` ile yükleyin, `PdfSaveOptions`'ı tam sayfa boyutlarını belirleyecek şekilde yapılandırın ve dönüştürücüyü çağırın. Aşağıdaki üç adımlı iş akışı, tipik e‑kitap boyutları için bir dakikadan kısa sürede dönüşümü gerçekleştirir ve daha büyük koleksiyonlara minimal kod değişikliğiyle ölçeklenir.

### Adım 1: EPUB Dosyasını Açın

İlk olarak, kaynak `.epub` dosyanıza işaret eden bir `FileInputStream` oluşturun. Dönüşüm tamamlanana kadar akışı açık tutmak, “boş sayfa” hatalarını önler.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

### Adım 2: PDF Kaydetme Seçeneklerini Tanımlayın

`PdfSaveOptions`, sayfa boyutu, arka plan rengi ve kenar boşlukları gibi PDF çıktı ayarlarını kontrol eden Aspose.HTML'in yapılandırma sınıfıdır.  
`Length.fromPixels`, ekran pikselini PDF puanına (1 puan = 1/72 inç) dönüştürür; böylece boyutları tanıdık piksel birimlerinde belirtebilirsiniz.

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

#### Pro ipucu:
- **Piksel vs. Puan:** `Length.fromPixels`, ekran pikselini PDF puanına (1 puan = 1/72 inç) dönüştürür. İhtiyacınız olan nihai baskı boyutunu yansıtan değerleri seçin.

### Adım 3: EPUB'u PDF'ye Dönüştürün

Giriş akışı ve özel seçenekler hazır olduğunda, dönüştürücüyü çağırın. Çıktı PDF, belirttiğiniz konuma kaydedilecek ve tanımladığınız tam sayfa boyutlarını koruyacaktır.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

`PdfSaveOptions.setEnableParallelProcessing`, PDF dönüşümü sırasında sayfaların paralel işlenmesini sağlayan bir yöntemdir.

## Tam Kaynak Kodu

Tam, çalıştırılabilir örnek, yukarıdaki üç adımı tek bir Java sınıfında birleştirir. Yer tutucu yolları kendi dosya konumlarınızla değiştirin.

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## Yaygın Sorunlar ve Çözümler

| Sorun | Sebep | Çözüm |
|-------|-------|-----|
| **PDF sayfaları boş** | Dönüşümden önce giriş akışı kapatıldı | `try‑with‑resources` bloğunu `convertEPUB` sonrası açık tutun. |
| **Yanlış sayfa boyutları** | İstenen baskı boyutuna eşleşmeyen pikseller kullanılıyor | İstenen inçleri puanlara (`1 inch = 72 points`) dönüştürün ve ardından `Length.fromPixels` ile piksellere çevirin. |
| **Eksik yazı tipleri** | Yazı tipleri EPUB içinde gömülü değil | Yazı tiplerinin EPUB içinde paketlendiğinden emin olun veya host makineye kurun. |
| **Büyük kitaplarda performans yavaşlaması** | Her sayfa sırayla işleniyor | 500+ sayfalı EPUB'lar için daha hızlı işleme amacıyla `PdfSaveOptions.setEnableParallelProcessing(true)` ile çok iş parçacıklı işleme etkinleştirin. |

## Sık Sorulan Sorular (SSS)

**S: Aspose.HTML for Java ücretsiz bir kütüphane mi?**  
C: Aspose.HTML for Java ticari bir kütüphanedir, ancak ücretsiz deneme sürümünü [website](https://releases.aspose.com/) adresinden edinebilirsiniz.

**S: Hangi EPUB formatları dönüşüm için destekleniyor?**  
C: Aspose.HTML for Java, EPUB 2.0, EPUB 3.0 ve EPUB 3.1'i destekler; yeniden akışlı ve sabit düzenli kitapları tam CSS desteğiyle işler.

**S: PDF çıktısını daha da özelleştirebilir miyim?**  
C: Evet, `PdfSaveOptions` içinde sayfa ayarlarını, arka plan rengini, sıkıştırma seviyesini ve diğer ayarları değiştirerek PDF çıktısını özelleştirebilirsiniz.

**S: Aspose.HTML for Java deneme sürümünde herhangi bir sınırlama var mı?**  
C: Deneme sürümü ilk birkaç sayfaya filigran ekleyebilir ve maksimum dosya boyutunu 10 MB ile sınırlar; bu kısıtlamaları kaldırmak için bir lisans satın alın.

**S: Aspose.HTML for Java için destek nereden alınabilir?**  
C: Sorularınıza yanıt bulabilir ve desteğe [Aspose.HTML forum](https://forum.aspose.com/) üzerinden ulaşabilirsiniz.

**Son Güncelleme:** 2026-05-30  
**Test Edilen Versiyon:** Aspose.HTML for Java 24.11 (yazım anındaki en son sürüm)  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Aspose.HTML for Java ile PDF Sayfa Boyutunu Ayarlama](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Java ile EPUB'u PDF'ye Dönüştürme – Aspose.HTML Kullanarak](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-pdf/)
- [Aspose.HTML for Java ile EPUB'u PDF ve Görsellere Dönüştürme](/html/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}