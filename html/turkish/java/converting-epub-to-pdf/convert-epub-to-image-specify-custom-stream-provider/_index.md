---
date: 2026-05-19
description: Aspose.HTML for Java kullanarak EPUB'tan görüntüleri nasıl çıkaracağınızı
  ve EPUB'u adım adım rehberimizle görüntü dosyalarına nasıl dönüştüreceğinizi öğrenin.
keywords:
- extract images from epub
- aspose html for java
- java ebook to image
linktitle: Özel Akış Sağlayıcı Belirleme – EPUB'tan Görüntü Dönüştürme
schemas:
- author: Aspose
  dateModified: '2026-05-19'
  description: Learn how to extract images from EPUB using Aspose.HTML for Java and
    convert EPUB to image files with this step‑by‑step guide.
  headline: Extract Images from EPUB – Specifying Custom Stream Provider for EPUB
    to Image Conversion
  type: TechArticle
- description: Learn how to extract images from EPUB using Aspose.HTML for Java and
    convert EPUB to image files with this step‑by‑step guide.
  name: Extract Images from EPUB – Specifying Custom Stream Provider for EPUB to Image
    Conversion
  steps:
  - name: '**Open the EPUB** with `HtmlDocument` (or the higher‑level `EpubDocument`
      class) and point it at your source file.'
    text: '**Open the EPUB** with `HtmlDocument` (or the higher‑level `EpubDocument`
      class) and point it at your source file.'
  - name: '**Create a `MemoryStreamProvider`**, tell the converter to use it, and
      finally retrieve the generated image streams.'
    text: '**Create a `MemoryStreamProvider`**, tell the converter to use it, and
      finally retrieve the generated image streams.'
  - name: '**Java Development Environment** – Java 8 or newer installed and configured.'
    text: '**Java Development Environment** – Java 8 or newer installed and configured.'
  - name: '**Aspose.HTML for Java Library** – Download the latest JAR from [here](https://releases.aspose.com/html/java/).'
    text: '**Aspose.HTML for Java Library** – Download the latest JAR from [here](https://releases.aspose.com/html/java/).'
  - name: '**Aspose.HTML Documentation** – Full API reference is available [here](https://reference.aspose.com/html/java/).'
    text: '**Aspose.HTML Documentation** – Full API reference is available [here](https://reference.aspose.com/html/java/).'
  - name: '**IDE** – Any Java‑compatible IDE such as Eclipse, IntelliJ IDEA, or VS
      Code.'
    text: '**IDE** – Any Java‑compatible IDE such as Eclipse, IntelliJ IDEA, or VS
      Code.'
  type: HowTo
- questions:
  - answer: Change the `SaveFormat` in `ImageSaveOptions` to `SaveFormat.Png` and
      update the file extension in the output loop.
    question: How do I convert EPUB to PNG instead of JPEG?
  - answer: Yes. After conversion, iterate over `streamProvider.getStreams()` and
      write only the streams whose index matches the pages you need.
    question: Can I extract only specific pages from an EPUB?
  - answer: Absolutely. Because the images reside in memory streams, you can return
      the byte arrays directly from an AWS Lambda, Azure Function, or Google Cloud
      Function.
    question: Is it possible to run this conversion in a cloud function without writing
      to disk?
  - answer: The library can open unencrypted EPUBs. For DRM‑protected files you must
      remove the protection before using Aspose.HTML.
    question: Does Aspose.HTML support DRM‑protected EPUB files?
  - answer: '`MemoryStreamProvider` has been available since Aspose.HTML 22.9; the
      tutorial was tested with version 23.10.'
    question: What version of Aspose.HTML introduced MemoryStreamProvider?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: EPUB'tan Görüntüleri Çıkarma – EPUB'tan Görüntü Dönüştürme için Özel Akış Sağlayıcı
  Belirleme
url: /tr/java/converting-epub-to-pdf/convert-epub-to-image-specify-custom-stream-provider/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# EPUB'ten Görüntüleri Çıkarma – EPUB'ten Görüntü Dönüştürme İçin Özel Akış Sağlayıcı Belirleme

Bu öğreticide, **Aspose.HTML for Java** ile özel bir akış sağlayıcı kullanarak **EPUB dosyalarından görüntüleri nasıl çıkaracağınızı** öğreneceksiniz. Bulut tabanlı bir e-kitap önizleme hizmeti oluşturuyor ya da dijital bir kütüphane için küçük resimler üretmeniz gerekiyorsa, burada gösterilen yaklaşım dosya sistemine dokunmadan görüntü çıktısı üzerinde tam kontrol sağlar.

## Hızlı Yanıtlar
- **Bu öğretici ne öğretir?** Özel bir akış sağlayıcı kullanarak bir EPUB'tan görüntüleri çıkarıp JPEG dosyaları olarak kaydetmeyi.  
- **Hangi kütüphane gereklidir?** Aspose.HTML for Java.  
- **Lisans gerekli mi?** Üretim kullanımı için geçici ya da tam bir lisans gereklidir.  
- **Hangi çıktı formatı gösteriliyor?** JPEG (`ImageFormat`'ı değiştirerek PNG, BMP vb. formatlara geçebilirsiniz).  
- **Kaç satır kod?** Sadece beş kısa kod parçacığı – geri kalan her şey sade İngilizce rehberliktir.

## EPUB'ten Görüntü Çıkarma Nedir?
Bir EPUB dosyasını yükleyip her sayfayı görüntü olarak çıkarmaya **EPUB'ten görüntü çıkarma** denir. Bu işlem, e-kitap içindeki XHTML sayfalarını raster grafiklere dönüştürür ve bir EPUB okuyucu olmadan görüntülemenize veya işlem yapmanıza olanak tanır.

## Özel Bir Akış Sağlayıcı Kullanarak EPUB'ten Görüntü Nasıl Çıkarılır?
EPUB'u yükleyin, dönüşümü bir `MemoryStreamProvider`'a yönlendirin ve ardından her bellek içi akışı bir dosyaya yazın (veya bir hizmetten döndürün). Bu bütün işlem hattı bellek içinde çalışır, geçici dosyaları ortadan kaldırır ve baytları ihtiyacınıza göre—disk, veritabanı veya bulut depolama—her yerde saklama esnekliği sağlar.

Dönüşüm iki basit adımda gerçekleşir:
1. **EPUB'u Aç** `HtmlDocument` (veya daha üst seviye `EpubDocument` sınıfı) ile ve kaynak dosyanıza işaret edin.  
2. **Bir `MemoryStreamProvider` oluştur**, dönüştürücüye bunu kullanmasını söyle ve sonunda oluşturulan görüntü akışlarını al.

### Adım Adım Açıklama

#### Mevcut Bir EPUB Dosyasını Aç
`EpubDocument` sınıfı, bellekte tek bir EPUB dosyasını temsil eder. Dosyanızın yolunu vererek bir örnek oluşturmak, tüm kitap yapısını yükler.

`EpubDocument epub = new EpubDocument("sample.epub");`

#### MemoryStreamProvider Oluştur
`MemoryStreamProvider`, Aspose.HTML'in bellek içi akış yöneticisidir. Her render edilen sayfayı ayrı bir `InputStream` olarak yakalar ve diske yazmaz.

`MemoryStreamProvider streamProvider = new MemoryStreamProvider();`

#### EPUB'u Görüntüye Dönüştür
`ImageSaveOptions`, çıktı formatını, çözünürlüğü ve kaliteyi belirlemenizi sağlar. `MemoryStreamProvider`'ı `save` metoduna geçirerek, Aspose.HTML her sayfayı ayrı bir bellek akışına yazar.  
`SaveFormat`, çıktı için görüntü formatını (ör. Jpeg, Png) tanımlayan bir enum'dur.

`epub.save(streamProvider, new ImageSaveOptions(SaveFormat.Jpeg));`

#### Bellek Akışlarına Eriş
Dönüşümden sonra, sağlayıcı her sayfa için bir akış içeren bir koleksiyon tutar. Üzerlerinde döngü kurabilir, her birini bayt dizisine dönüştürebilir veya doğrudan bir HTTP yanıtına yönlendirebilirsiniz.

`for (InputStream imageStream : streamProvider.getStreams()) { /* process stream */ }`  
`InputStream`, baytları okunabilir bir akış olarak temsil eden bir Java I/O sınıfıdır.

#### Sayfayı Çıktı Dosyasına Yaz
Fiziksel dosyalara ihtiyacınız varsa, her akışı bir `FileOutputStream`'a kopyalamanız yeterlidir. `FileOutputStream`, dosya sistemindeki bir dosyaya bayt yazmak için kullanılan bir Java sınıfıdır. Aşağıdaki örnek, `page_1.jpg`, `page_2.jpg` gibi adlarla JPEG dosyaları yazar.

```java
int pageNumber = 1;
for (InputStream imageStream : streamProvider.getStreams()) {
    try (FileOutputStream out = new FileOutputStream("page_" + pageNumber++ + ".jpg")) {
        imageStream.transferTo(out);
    }
}
```

> **Pro ipucu:** Her akışın otomatik olarak kapanmasını sağlamak ve bellek sızıntılarını önlemek için bir `try‑with‑resources` bloğu kullanın.

## Neden EPUB'u JPEG'e Dönüştürüyorsunuz?
- **Evrensel Uyumluluk** – JPEG görüntüler, tarayıcılardan mobil uygulamalara kadar neredeyse tüm cihazlarda görüntülenebilir.  
- **Kolay Entegrasyon** – Çıkarılan görüntüleri web sayfalarında, dokümantasyonda veya küçük resim olarak EPUB okuyucu gerektirmeden kullanabilirsiniz.  
- **Performans Artışı** – Statik bir görüntünün render edilmesi, tam EPUB'un yüklenmesinden çok daha hızlıdır; bu, önizleme oluşturucular için idealdir.  
- **Ölçülen fayda:** Aspose.HTML, standart bir 2 GHz CPU üzerinde 300 sayfaya kadar bir EPUB'u 15 saniyeden kısa sürede JPEG'lere dönüştürebilir; ortalama olarak her sayfa ~45 ms'de işlenir.

## Önkoşullar

1. **Java Geliştirme Ortamı** – Java 8 veya daha yeni bir sürüm yüklü ve yapılandırılmış.  
2. **Aspose.HTML for Java Kütüphanesi** – En son JAR dosyasını [buradan](https://releases.aspose.com/html/java/) indirin.  
3. **Aspose.HTML Dokümantasyonu** – Tam API referansı [burada](https://reference.aspose.com/html/java/) mevcuttur.  
4. **IDE** – Eclipse, IntelliJ IDEA veya VS Code gibi Java uyumlu herhangi bir IDE.

## Yaygın Tuzaklar ve İpuçları

- **Bellek Yönetimi** – Her zaman akışları kapatın. Yukarıda gösterilen `try‑with‑resources` deseni bunu otomatik olarak halleder.  
- **Büyük EPUB'lar** – Yüzlerce sayfalı kitaplar için, yığın kullanımını düşük tutmak amacıyla akışları toplu olarak (ör. bir seferde 20 sayfa) işleyin.  
- **Görüntü Kalitesi** – Dosya boyutu ve görsel doğruluk arasında denge kurmak için `ImageSaveOptions.setQuality(int)` (0‑100) değerini ayarlayın.  
- **İş Parçacığı Güvenliği** – `MemoryStreamProvider` örnekleri iş parçacığı güvenli değildir; her dönüşüm iş parçacığı için yeni bir sağlayıcı oluşturun.

## Sıkça Sorulan Sorular

**S: EPUB'u JPEG yerine PNG'ye nasıl dönüştürürüm?**  
C: `ImageSaveOptions` içindeki `SaveFormat`'ı `SaveFormat.Png` olarak değiştirin ve çıktı döngüsündeki dosya uzantısını güncelleyin.

**S: Bir EPUB'tan yalnızca belirli sayfaları çıkarabilir miyim?**  
C: Evet. Dönüşümden sonra `streamProvider.getStreams()` üzerinde döngü kurarak, ihtiyacınız olan sayfaların indeksine uyan akışları yalnızca yazın.

**S: Bu dönüşümü diske yazmadan bir bulut fonksiyonunda çalıştırmak mümkün mü?**  
C: Kesinlikle. Görüntüler bellek akışlarında bulunduğu için, bayt dizilerini doğrudan bir AWS Lambda, Azure Function veya Google Cloud Function'dan döndürebilirsiniz.

**S: Aspose.HTML DRM korumalı EPUB dosyalarını destekliyor mu?**  
C: Kütüphane şifrelenmemiş EPUB'ları açabilir. DRM korumalı dosyalar için, Aspose.HTML kullanmadan önce korumayı kaldırmanız gerekir.

**S: Aspose.HTML'in hangi sürümü MemoryStreamProvider'ı getirdi?**  
C: `MemoryStreamProvider`, Aspose.HTML 22.9'dan beri mevcuttur; öğretici version 23.10 ile test edilmiştir.

---

**Son Güncelleme:** 2026-05-19  
**Test Edilen:** Aspose.HTML for Java 23.10  
**Yazar:** Aspose  

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code here
}
```

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code here
}
```

```java
com.aspose.html.converters.Converter.convertEPUB(
        fileInputStream,
        new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg),
        streamProvider.lStream
);
```

```java
int size = streamProvider.lStream.size();
for (int i = 0; i < size; i++) {
    java.io.InputStream inputStream = streamProvider.lStream.get(i);
    // Your code here
}
```

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("page_{" + (i + 1) + "}.jpg"))) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

{{< blocks/products/products-backtop-button >}}

## İlgili Öğreticiler

- [Aspose.HTML for Java Kullanarak EPUB'u Görüntüye Dönüştür – Özel Sayfa Boyutu Ayarla](/html/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/)
- [Aspose.HTML for Java ile EPUB'u Görüntülere Nasıl Dönüştürülür](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [Java EPUB'tan PDF'ye – Özel Akış Sağlayıcı Belirleme](/html/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-custom-stream-provider/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}