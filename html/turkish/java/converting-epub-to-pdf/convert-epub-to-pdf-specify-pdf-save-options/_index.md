---
date: 2026-01-02
description: Aspose.HTML ile Java'da EPUB'yi PDF'ye dönüştürmeyi, özel bir PDF sayfa
  boyutu ve diğer PDF kaydetme seçeneklerini ayarlamayı öğrenin.
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 'Özel PDF Sayfa Boyutu: EPUB''ten PDF''ye Dönüştürme İçin PDF Kaydetme Seçeneklerini
  Belirleme'
url: /tr/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Özel PDF Sayfa Boyutu: EPUB'ten PDF'ye PDF Kaydetme Seçeneklerini Belirleme

## Giriş

Aspose.HTML for Java, **EPUB'ten PDF'ye dönüştürmeyi** kolaylaştırır ve çıktının tam kontrolünü sağlar; buna **özel PDF sayfa boyutu** ayarlama da dahildir. Bu adım‑adım kılavuzda, ortam hazırlığından `PdfSaveOptions` ayarlarına kadar, oluşturulan PDF'nin tam olarak istediğiniz sayfa boyutlarına uymasını nasıl sağlayacağınızı öğreneceksiniz. Yayın akışı, e‑öğrenme platformu oluşturma ya da belge dönüşümünü otomatikleştirme gibi senaryolarda bu teknikler işinize yarayacaktır.

## Hızlı Yanıtlar
- **Bu öğreticinin temel amacı nedir?** Bir EPUB dosyasını PDF'ye dönüştürürken özel bir PDF sayfa boyutu uygulamak.  
- **Hangi kütüphane kullanılıyor?** Aspose.HTML for Java.  
- **Lisans gerekli mi?** Ücretsiz deneme sürümü mevcuttur; üretim ortamı için ticari lisans gereklidir.  
- **Arka plan rengini değiştirebilir miyim?** Evet, `PdfSaveOptions` kullanarak.  
- **Java 8+ destekleniyor mu?** Kesinlikle—herhangi bir modern Java çalışma zamanı ile çalışır.

## Özel PDF sayfa boyutu nedir?

Özel PDF sayfa boyutu, çıktı PDF'sindeki her sayfanın genişlik ve yüksekliğini standart A4 veya Letter gibi ön tanımlı boyutlar yerine tam olarak tanımlamanıza olanak tanır. Bu, e‑kitaplar, broşürler veya görsel düzenin belirli bir tasarıma tam olarak uyması gereken diğer senaryolar için özellikle faydalıdır.

## Neden Aspose.HTML ile EPUB‑den PDF’ye dönüşüm yapılmalı?

- **Yüksek doğruluk:** Karmaşık düzenleri, yazı tiplerini ve görselleri korur.  
- **İnce ayar kontrolü:** `PdfSaveOptions` aracılığıyla sayfa boyutu, arka plan, kenar boşlukları ve daha fazlasını ayarlayabilirsiniz.  
- **Çapraz platform:** Aynı Java kodu Windows, Linux ve macOS'ta çalışır.  
- **Performans:** Hızlı dönüşümler için optimize edilmiş render motoru.

## Ön Koşullar

Başlamadan önce şunların kurulu olduğundan emin olun:

- **Java Geliştirme Ortamı:** JDK 8 veya üzeri yüklü ve yapılandırılmış.  
- **Aspose.HTML for Java:** En son JAR dosyasını [web sitesinden](https://releases.aspose.com/html/java/) indirin.  
- **EPUB Dosyası:** Dönüştürmek istediğiniz bir `.epub` belgesi.  

Her şey hazır olduğuna göre, gerçek dönüşüm adımlarına geçelim.

## Adım 1: EPUB Dosyasını Açın

İlk olarak, EPUB dosyasını bir `FileInputStream` ile açmamız gerekiyor. Bu akış daha sonra dönüştürücüye geçirilecek.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## Adım 2: PDF Kaydetme Seçeneklerini Tanımlayın

Burada **özel PDF sayfa boyutunu** ve isteğe bağlı arka plan rengini ayarlıyoruz. Piksel değerlerini istediğiniz boyutlara göre düzenleyin.

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

### Uzman ipucu:
- **Piksel vs. Nokta:** `Length.fromPixels`, ekran pikselini PDF noktalarına çevirir (1 nokta = 1/72 inç). İhtiyacınız olan son baskı boyutunu yansıtacak değerleri seçin.

## Adım 3: EPUB’u PDF’ye Dönüştürün

Girdi akışı ve özel seçenekler hazır olduğunda, dönüştürücüyü çağırın. Çıktı PDF, belirttiğiniz konuma kaydedilecektir.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## Tam Kaynak Kodu

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

## Yaygın Sorunlar ve Çözümleri

| Sorun | Neden | Çözüm |
|-------|-------|-----|
| **PDF sayfaları boş** | Dönüştürmeden önce giriş akışı kapatıldı | `try‑with‑resources` bloğunu `convertEPUB` işleminden sonra da açık tutun. |
| **Sayfa boyutları hatalı** | İstenen baskı boyutuna eşleşmeyen pikseller kullanıldı | İstenen inç değerini noktalara çevirin (`1 inch = 72 points`) ve ardından `Length.fromPixels` ile piksele dönüştürün. |
| **Yazı tipleri eksik** | Yazı tipleri EPUB içinde paketlenmemiş | Yazı tiplerinin EPUB içinde paketlendiğinden emin olun veya host makinede yüklü olduğundan emin olun. |

## Sık Sorulan Sorular (SSS)

### Aspose.HTML for Java ücretsiz bir kütüphane mi?
Aspose.HTML for Java ticari bir kütüphanedir, ancak [web sitesinden](https://releases.aspose.com/) ücretsiz deneme sürümü alabilirsiniz.

### Hangi EPUB formatları dönüşüm için destekleniyor?
Aspose.HTML for Java, çeşitli EPUB formatlarını destekler ve çoğu EPUB belgesiyle uyumludur.

### PDF çıktısını daha da özelleştirebilir miyim?
Evet, `PdfSaveOptions` içinde sayfa ayarlarını, arka plan rengini ve diğer ayarları değiştirerek PDF çıktısını özelleştirebilirsiniz.

### Aspose.HTML for Java deneme sürümünün sınırlamaları var mı?
Deneme sürümünde bazı sınırlamalar bulunabilir; detaylar için belgeleri kontrol etmeniz önerilir.

### Aspose.HTML for Java için destek nereden alınır?
Sorularınıza yanıt bulmak ve destek almak için [Aspose.HTML forumunu](https://forum.aspose.com/) ziyaret edebilirsiniz.

---

**Son Güncelleme:** 2026-01-02  
**Test Edilen Sürüm:** Aspose.HTML for Java 24.11 (yazım anındaki en yeni sürüm)  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}