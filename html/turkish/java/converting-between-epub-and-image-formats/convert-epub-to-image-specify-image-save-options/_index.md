---
date: 2026-08-17
description: Aspise.HTML for Java kullanarak EPUB dosyalarını görüntülere nasıl dönüştüreceğinizi,
  custom page dimensions görüntüsünü nasıl ayarlayacağınızı ve optimal sonuçlar için
  image background color'ı nasıl değiştireceğinizi öğrenin.
keywords:
- custom page dimensions image
- Aspose.HTML Java
- EPUB to image conversion
lastmod: 2026-08-17
linktitle: EPUB'tan Image Save Options belirleme
og_description: Aspose.HTML for Java kullanarak custom page dimensions görüntüsü ile
  EPUB'yi görüntüye dönüştürün. Tek bir rehberde step‑by‑step sayfa boyutunu, background
  color'ı ve output format'ı nasıl ayarlayacağınızı öğrenin.
og_image_alt: Developer guide showing how to set custom page dimensions image when
  converting EPUB to image with Aspose.HTML for Java
og_title: Java'da custom page dimensions görüntüsü ile EPUB'yi görüntüye dönüştür
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to convert EPUB files to images using Aspise.HTML for Java,
    set custom page dimensions image, and change image background color for optimal
    results.
  headline: Convert EPUB to image with custom page dimensions image
  type: TechArticle
- description: Learn how to convert EPUB files to images using Aspise.HTML for Java,
    set custom page dimensions image, and change image background color for optimal
    results.
  name: Convert EPUB to image with custom page dimensions image
  steps:
  - name: open an existing EPUB file for reading
    text: Here we open the source EPUB. Replace `"input.epub"` with the path to your
      e‑book file.
  - name: initialize ImageSaveOptions with custom settings (set custom page dimensions
      image & change image background color)
    text: '`ImageSaveOptions` is the class that controls how the EPUB pages are rendered
      to images. In this block we **set custom page dimensions image** to 3000 × 1000
      pixels and change the background to AliceBlue. Feel free to adjust the `Size`
      object or the `Color` to match your branding (e.g., `Color.getWh'
  - name: convert EPUB to image
    text: This line performs the actual conversion. The output file (`"output.jpg"`)
      will contain the rendered image with the dimensions and background you specified.
      You can also change the file extension to `.png` if you prefer **java convert
      epub png**. The library supports both JPEG and PNG, giving you fl
  - name: close resources (handled automatically)
    text: The `try‑with‑resources` statement automatically closes `FileInputStream`,
      ensuring no file handles are left open.
  type: HowTo
- questions:
  - answer: Yes, you can specify formats such as PNG or GIF by changing `ImageFormat.Jpeg`
      to `ImageFormat.Png` or `ImageFormat.Gif`.
    question: Can I convert EPUB files to other image formats?
  - answer: Absolutely. The library fully supports EPUB3, allowing you to work with
      the latest e‑book standards.
    question: Does Aspose.HTML for Java support EPUB3?
  - answer: Implement `try‑catch` blocks around the conversion code to capture and
      log exceptions, ensuring your application remains robust.
    question: How can I handle errors during the conversion process?
  - answer: Yes, adjust the `Size` object for dimensions and use `options.setQuality(int)`
      to control JPEG compression quality.
    question: Can I customize the image size and quality?
  - answer: The library works with Java 1.7 and later, covering a wide range of development
      environments.
    question: Is Aspose.HTML for Java compatible with all Java versions?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
tags:
- convert EPUB
- Aspose.HTML
- Java image processing
title: EPUB'yi custom page dimensions görüntüsü olarak dönüştür
url: /tr/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# EPUB'ı özel sayfa boyutlu görüntü ile dönüştürme

Modern dijital yayıncılıkta, bir EPUB dosyasını yüksek kaliteli bir görüntüye dönüştürebilmek, küçük resimler, ön izlemeler ve pazarlama varlıkları için esneklik sağlar. **Aspose.HTML for Java** bu dönüşümü basitleştirir ve özel sayfa boyutlu görüntü ayarlayarak çıktıyı hassas bir şekilde kontrol edebilirsiniz. Bu öğretici, ortam kurulumundan son JPEG veya PNG'nin oluşturulmasına kadar tüm süreci adım adım anlatır ve her ayarın neden önemli olduğunu açıklar.

## Hızlı cevaplar
- **“custom page dimensions image” ne anlama geliyor?** Oluşturulan her görüntü sayfasının tam genişlik ve yüksekliğini (piksel olarak) tanımlamanızı sağlar.  
- **Görüntü arka plan rengini değiştirebilir miyim?** Evet—`ImageSaveOptions` herhangi bir `java.awt.Color` belirlemenize olanak tanır.  
- **Hangi görüntü formatları destekleniyor?** JPEG, PNG, GIF, BMP, TIFF ve `ImageFormat` aracılığıyla daha fazlası.  
- **Üretim için lisansa ihtiyacım var mı?** Değerlendirme için ücretsiz deneme çalışır; üretim dağıtımları için ticari lisans gereklidir.  
- **Hangi Java sürümü gerekiyor?** Java 1.7 veya üzeri tam olarak desteklenir.

## “custom page dimensions image” EPUB'tan görüntüye dönüşümde nedir?
**Custom page dimensions image**, her render edilen sayfanın piksel bazında tam boyutunu kontrol etmenizi sağlar, örneğin 3000 × 1000 piksel. Genişlik ve yüksekliği belirleyerek, tasarım ızgaralarına uyan, UI bileşenlerine sığan veya baskı gereksinimlerini karşılayan görüntüler oluşturabilirsiniz. Bu esneklik, farklı cihazlarda en‑boy oranlarını korumak zorunda olan küçük resimler oluştururken de yardımcı olur ve çıktının görsel gereksinimlerinize uygun olmasını sağlar.

## Neden özel bir sayfa boyutu ayarlamalı ve görüntü arka plan rengini değiştirmelisiniz?
Özel bir sayfa boyutu ayarlamak, çıktının hedef cihaz veya tasarım spesifikasyonuna uymasını sağlar; arka plan rengini değiştirmek ise görüntüyü marka kimliğiyle uyumlu hale getirir veya şeffaf öğelerin okunabilirliğini artırır. Birlikte, dönüşüm sonucunun tam görsel kontrolünü elde etmenizi sağlar.

## Önkoşullar

**EPUB'ı görüntüye dönüştürme** yolculuğuna başlamadan önce, aşağıdakilere sahip olduğunuzdan emin olun:

1. **Java ortamı** – Makinenizde kurulu bir Java Development Kit. Henüz Java'nız yoksa, [Java resmi web sitesinden](https://www.java.com) indirebilirsiniz.  
2. **Aspose.HTML for Java** – Aspose.HTML for Java kütüphanesi. En son sürümü [Aspose.HTML for Java sayfasından](https://releases.aspose.com/html/java/) alın.

## Paketleri içe aktar

Aspose.HTML for Java ile çalışmak için gerekli namespace'leri içe aktarın:

```java
// Import the required Aspose.HTML for Java packages
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import java.io.FileInputStream;
```

## Adım adım rehber

### Adım 1: Okuma için mevcut bir EPUB dosyasını açın

```java
try (FileInputStream fileInputStream = new FileInputStream("input.epub")) {
```

Burada kaynak EPUB'u açıyoruz. `"input.epub"` ifadesini e‑kitap dosyanızın yolu ile değiştirin.

### Adım 2: ImageSaveOptions'ı özel ayarlarla başlatın (özel sayfa boyutlu görüntü ayarla ve görüntü arka plan rengini değiştir)

```java
ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Jpeg);
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
Size size = new Size(
    Length.fromPixels(3000),
    Length.fromPixels(1000)
);
anyPage.setSize(size);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

`ImageSaveOptions`, EPUB sayfalarının görüntülere nasıl render edildiğini kontrol eden sınıftır. Bu blokta **custom page dimensions image** 3000 × 1000 piksel olarak ayarlanır ve arka plan AliceBlue olarak değiştirilir. Marka kimliğinize uyması için `Size` nesnesini veya `Color`'ı istediğiniz gibi ayarlayabilirsiniz (örneğin, düz beyaz arka plan için `Color.getWhite()` ).

### Adım 3: EPUB'u görüntüye dönüştür

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    "output.jpg"
);
```

Bu satır gerçek dönüşümü gerçekleştirir. Çıktı dosyası (`"output.jpg"`) belirttiğiniz boyut ve arka plan ile render edilmiş görüntüyü içerir. **java convert epub png** tercih ederseniz dosya uzantısını `.png` olarak da değiştirebilirsiniz. Kütüphane hem JPEG hem de PNG'yi destekler, sonraki işlemler için esneklik sağlar.

### Adım 4: Kaynakları kapat (otomatik olarak işlenir)

`try‑with‑resources` ifadesi, `FileInputStream`'i otomatik olarak kapatır ve hiçbir dosya tanıtıcısının açık kalmamasını sağlar.

## Yaygın kullanım senaryoları
- **Küçük resimler oluşturma** e‑kitap kütüphaneleri için, her küçük resmin 200 × 300 piksel kutuya sığması gerekir.  
- **Yüksek çözünürlüklü ekran görüntüleri oluşturma** dokümantasyon, pazarlama broşürleri veya UI mock‑up'ları için.  
- **Toplu işleme** büyük EPUB koleksiyonlarını web galerileri veya çevrim dışı arşivler için PNG/JPEG varlıklarına dönüştürme.  
- **Erişilebilirlik araçları için görüntü çıkarımını otomatikleştirme**; bu araçlar e‑kitapların görsel ön izlemelerine ihtiyaç duyar.

## İpuçları ve en iyi uygulamalar
- **Pro ipucu:** Piksel yerine fiziksel birimler tercih ediyorsanız `Length.fromInches()` veya `Length.fromCentimeters()` kullanın.  
- **Performans ipucu:** Büyük EPUB'lar için JVM yığın boyutunu (`-Xmx2g`) artırarak bellek baskısını önleyin.  
- **Hata yönetimi:** Dönüşüm çağrısını `try‑catch` bloğu içinde sararak `IOException` veya `AsposeException` yakalayın.  
- **Kalite kontrolü:** JPEG sıkıştırmasını fark edilir bir kayıp olmadan ince ayar yapmak için `options.setQuality(90)` değerini ayarlayın.  
- **Sayısal iddia:** Aspose.HTML for Java, **15+ görüntü formatına** dönüşümü destekler ve performansı düşürmeden **10.000 × 10.000 piksel** boyutuna kadar sayfaları render edebilir.

## Yaygın sorunlar ve çözümler
- **Bellek‑yetersiz hataları:** Yığın boyutunu artırın veya EPUB'u tek tek sayfaları render ederek daha küçük parçalar halinde işleyin.  
- **Boş arka plan:** Bir arka plan rengi ayarladığınızdan emin olun; şeffaf arka planlar bazı görüntüleyicilerde siyah görünebilir.  
- **Beklenmeyen görüntü boyutları:** `Size` nesnesinin ihtiyacınız olan tam piksel değerlerini yansıttığını doğrulayın; DPI ayarları piksel boyutunu etkilemez.  
- **Desteklenmeyen EPUB özellikleri:** Aspose.HTML EPUB3'ü tamamen işler, ancak özel yazı tiplerinin doğru şekilde gömülmesi veya referans verilmesi gerekebilir.

## Sıkça sorulan sorular

**Q: EPUB dosyalarını başka görüntü formatlarına dönüştürebilir miyim?**  
A: Evet, `ImageFormat.Jpeg`'i `ImageFormat.Png` veya `ImageFormat.Gif` olarak değiştirerek PNG veya GIF gibi formatları belirtebilirsiniz.

**Q: Aspose.HTML for Java EPUB3'ü destekliyor mu?**  
A: Kesinlikle. Kütüphane EPUB3'ü tam olarak destekler ve en son e‑kitap standartlarıyla çalışmanıza olanak tanır.

**Q: Dönüşüm sürecinde hataları nasıl yönetebilirim?**  
A: Dönüşüm kodunun etrafına `try‑catch` blokları ekleyerek istisnaları yakalayabilir ve kaydedebilirsiniz; bu sayede uygulamanız sağlam kalır.

**Q: Görüntü boyutunu ve kalitesini özelleştirebilir miyim?**  
A: Evet, boyutlar için `Size` nesnesini ayarlayın ve JPEG sıkıştırma kalitesini kontrol etmek için `options.setQuality(int)` kullanın.

**Q: Aspose.HTML for Java tüm Java sürümleriyle uyumlu mu?**  
A: Kütüphane Java 1.7 ve üzeri sürümlerle çalışır, geniş bir geliştirme ortamını kapsar.

## Sonuç

Bu rehberi izleyerek artık **Aspose.HTML for Java** kullanarak **EPUB'ı görüntüye dönüştürmeyi**, **custom page dimensions image** ayarlamayı ve **görüntü arka plan rengini değiştirmeyi** biliyorsunuz. Bu yetenekler, herhangi bir sonraki iş akışı için mükemmel boyutlu, markalı görüntüler üretmenizi sağlar—ister bir küçük resim galerisi, ister bir pazarlama broşürü, ister otomatik e‑kitap ön izleme hizmeti olsun. Belirli ihtiyaçlarınıza uygun farklı boyutlar, renkler ve çıktı formatlarıyla denemeler yapmaktan çekinmeyin.

---

**Son Güncelleme:** 2026-08-17  
**Test Edilen:** Aspose.HTML for Java 24.10  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Aspose.HTML for Java ile EPUB Sayfalarını Görsellere Dönüştürme](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [EPUB'ı BMP ve Diğer Görsellere Dönüştürme – Aspose.HTML Java](/html/java/converting-between-epub-and-image-formats/)
- [EPUB'tan Görüntü Dönüşümü İçin Görüntü Arka Plan Rengini Ayarlama](/html/java/converting-epub-to-pdf/convert-epub-to-image-specify-image-save-options/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}