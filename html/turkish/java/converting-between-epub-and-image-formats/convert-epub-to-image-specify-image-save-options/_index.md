---
date: 2026-03-13
description: Aspose.HTML for Java kullanarak EPUB dosyalarını görüntülere dönüştürmeyi,
  özel sayfa boyutu ayarlamayı ve optimal sonuçlar için görüntü arka plan rengini
  değiştirmeyi öğrenin.
linktitle: Specifying Image Save Options for EPUB to Image Conversion
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML for Java Kullanarak EPUB'yi Görsele Dönüştür – Özel Sayfa Boyutu
  Ayarla
url: /tr/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/
weight: 16
---

 necessarily UI strings. I'd translate but keep phrase maybe. However earlier we translated bold phrase "set custom page size" to "özel sayfa boyutu ayarlama". That's okay.

Also "convert epub to image" phrase appears; we translated to "epub'yi görüntüye dönüştür". Might be okay.

Make sure code block placeholders remain unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML for Java Kullanarak EPUB'yi Görüntüye Dönüştür – Özel Sayfa Boyutu Ayarlama

Web geliştirme dünyasının sürekli evrimleşen ortamında, Aspose.HTML for Java güçlü bir araç olarak öne çıkıyor ve bugün bir EPUB'yi görüntüye dönüştürürken **özel sayfa boyutu nasıl ayarlanır** konusuna odaklanacağız. Dijital bir kütüphane oluşturuyor, küçük resimler üretiyor ya da yüksek çözünürlüklü ekran görüntüleri yapıyor olsanız, bu ayarı ustalaşmak **EPUB'yi görüntüye dönüştürmenizi** sağlar ve tam istediğiniz düzen gereksinimlerine uyan dosyalar elde edersiniz.

## Hızlı Yanıtlar
- **“set custom page size” ne anlama geliyor?** Çıktı görüntü sayfasının genişliğini ve yüksekliğini tanımlamanızı sağlar.  
- **Görüntü arka plan rengini değiştirebilir miyim?** Evet, `ImageSaveOptions` kullanarak istediğiniz rengi belirtebilirsiniz.  
- **Hangi formatlar destekleniyor?** JPEG, PNG, GIF ve daha fazlası `ImageFormat` aracılığıyla.  
- **Lisans gerekli mi?** Test için ücretsiz deneme sürümü çalışır; üretim için ticari lisans gereklidir.  
- **Hangi Java sürümü gerekiyor?** Java 1.7 veya üzeri tam olarak desteklenir.

## EPUB'yi Görüntüye Dönüştürürken “set custom page size” nedir?
Özel bir sayfa boyutu ayarlamak, oluşturulan görüntünün boyutlarını kontrol etmeniz anlamına gelir (ör. 3000 × 1000 piksel). Bu, e‑kitapların yüksek çözünürlüklü ekran görüntülerine ihtiyaç duyduğunuzda ya da çıktının belirli bir düzenle eşleşmesini istediğinizde faydalıdır.

## Neden özel bir sayfa boyutu ayarlamalı ve görüntü arka plan rengini değiştirmelisiniz?
Özel sayfa boyutları, farklı görüntü hedefleri—mobil ekranlar, baskıya hazır PDF'ler veya web küçük resimleri—için esneklik sağlar. Arka plan rengini değiştirmek, markalaşmaya uyum sağlamanıza veya şeffaf öğeler içeren görüntülerin okunabilirliğini artırmanıza yardımcı olur.

## Önkoşullar

**epub'yi görüntüye dönüştürme** yolculuğumuza başlamadan önce, aşağıdakilere sahip olduğunuzdan emin olun:

1. **Java Ortamı** – Makinenizde kurulu bir Java geliştirme kiti. Henüz Java'nız yoksa, [buradan](https://www.java.com) indirebilirsiniz.

2. **Aspose.HTML for Java** – Aspose.HTML for Java kütüphanesi. En son sürümü [Aspose.HTML for Java sayfasından](https://releases.aspose.com/html/java/) alın.

## Paketleri İçe Aktarma

Aspose.HTML for Java ile çalışmak için gerekli paketleri içe aktarın:

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

## Adım‑Adım Kılavuz

### Adım 1: Okuma İçin Mevcut Bir EPUB Dosyasını Açın

```java
try (FileInputStream fileInputStream = new FileInputStream("input.epub")) {
```

Burada kaynak EPUB dosyasını açıyoruz. `"input.epub"` ifadesini e‑kitap dosyanızın yolu ile değiştirin.

### Adım 2: Özel Ayarlarla ImageSaveOptions'ı Başlatın (özel sayfa boyutu ayarla & görüntü arka plan rengini değiştir)

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

Bu blokta **özel sayfa boyutunu** 3000 × 1000 piksel olarak ayarlıyor ve arka planı AliceBlue olarak değiştiriyoruz. Projenize uygun şekilde `size` veya `Color` değerlerini serbestçe ayarlayabilirsiniz (ör. düz beyaz bir arka plan için `Color.getWhite()`).

### Adım 3: EPUB'yi Görüntüye Dönüştür

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    "output.jpg"
);
```

Bu satır gerçek dönüşümü gerçekleştirir. Çıktı dosyası (`"output.jpg"`), belirttiğiniz boyut ve arka plan ile oluşturulan görüntüyü içerir. **java convert epub png** tercih ederseniz dosya uzantısını `.png` olarak da değiştirebilirsiniz. Kütüphane hem **image format JPEG** hem de **image format PNG**'yi destekler, böylece sonraki işlemler için esneklik sağlar.

### Adım 4: Kaynakları Kapatma (otomatik olarak işlenir)

`try‑with‑resources` ifadesi `FileInputStream`'i otomatik olarak kapatır ve hiçbir dosya tanıtıcısının açık kalmamasını sağlar.

## Yaygın Kullanım Senaryoları

- **e‑kitap kütüphaneleri için küçük resimler** oluşturma.  
- **belgelendirme veya pazarlama için yüksek çözünürlüklü ekran görüntüleri** oluşturma.  
- **Toplu işleme** büyük EPUB koleksiyonlarını web galerileri için PNG/JPEG varlıklarına dönüştürme.  
- **Erişilebilirlik araçları için e‑kitapların görsel ön izlemelerini** otomatik olarak çıkartma.

## İpuçları ve En İyi Uygulamalar

- **Pro ipucu:** Piksel yerine fiziksel birimler tercih ediyorsanız `Length.fromInches()` veya `Length.fromCentimeters()` kullanın.  
- **Performans ipucu:** Büyük EPUB'lar için bellek baskısını önlemek amacıyla JVM yığın boyutunu (`-Xmx2g`) artırmayı düşünün.  
- **Hata yönetimi:** Dönüşüm çağrısını `try‑catch` bloğu içinde sararak `IOException` veya `AsposeException` yakalayın.  
- **Kalite kontrolü:** JPEG sıkıştırmasını fark edilir bir kayıp olmadan ince ayarlamak için `options.setQuality(90)` değerini ayarlayın.

## Yaygın Sorunlar ve Çözümleri

- **Bellek‑dışı‑bellek hataları:** Yığın boyutunu artırın veya EPUB'u tek tek sayfalar render ederek daha küçük parçalar halinde işleyin.  
- **Boş arka plan:** Bir arka plan rengi ayarladığınızdan emin olun; şeffaf arka planlar bazı görüntüleyicilerde siyah görünebilir.  
- **Beklenmeyen görüntü boyutları:** `Size` nesnesinin ihtiyacınız olan tam piksel değerlerini yansıttığını doğrulayın; DPI ayarlarının piksel boyutunu etkilemediğini unutmayın.  
- **Desteklenmeyen EPUB özellikleri:** Aspose.HTML EPUB3'ü tamamen işler, ancak özel yazı tiplerinin doğru şekilde gömülmesi veya referans verilmesi gerekebilir.

## Sıkça Sorulan Sorular

**S: EPUB dosalarını diğer görüntü formatlarına dönüştürebilir miyim?**  
C: Evet, `ImageFormat.Jpeg`'i `ImageFormat.Png` veya `ImageFormat.Gif` olarak değiştirerek PNG veya GIF gibi formatları belirtebilirsiniz.

**S: Aspose.HTML for Java EPUB3'ü destekliyor mu?**  
C: Kesinlikle. Kütüphane EPUB3'ü tam olarak destekler ve en yeni e‑kitap standartlarıyla çalışmanıza olanak tanır.

**S: Dönüşüm sürecinde hataları nasıl yönetebilirim?**  
C: Dönüşüm kodunun etrafına `try‑catch` blokları ekleyerek istisnaları yakalayabilir ve kaydedebilirsiniz; bu sayede uygulamanız sağlam kalır.

**S: Görüntü boyutunu ve kalitesini özelleştirebilir miyim?**  
C: Evet, boyutlar için `Size` nesnesini ayarlayın ve JPEG sıkıştırma kalitesini kontrol etmek için `options.setQuality(int)` kullanın.

**S: Aspose.HTML for Java tüm Java sürümleriyle uyumlu mu?**  
C: Kütüphane Java 1.7 ve üzeri sürümlerle çalışır, geniş bir geliştirme ortamını kapsar.

## Sonuç

Bu kılavuzu izleyerek artık Aspose.HTML for Java kullanarak **EPUB'yi görüntüye dönüştürmeyi**, **özel bir sayfa boyutu ayarlamayı** ve **görüntü arka plan rengini değiştirmeyi** biliyorsunuz. Bu yetenekler, küçük resim galerisi, pazarlama broşürü veya otomatik e‑kitap ön izleme hizmeti gibi herhangi bir sonraki iş akışı için mükemmel boyutlu, markalı görüntüler üretmenizi sağlar. İhtiyacınıza uygun farklı boyutlar, renkler ve çıktı formatlarıyla denemeler yapmaktan çekinmeyin.

---

**Son Güncelleme:** 2026-03-13  
**Test Edilen Versiyon:** Aspose.HTML for Java 24.10  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}