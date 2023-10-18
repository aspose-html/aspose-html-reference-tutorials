---
title: EPUB'dan PDF'ye Dönüştürmek için PDF Kaydetme Seçeneklerini Belirleme
linktitle: EPUB'dan PDF'ye Dönüştürmek için PDF Kaydetme Seçeneklerini Belirleme
second_title: Aspose.HTML ile Java HTML İşleme
description: Güçlü bir HTML işleme kütüphanesi olan Aspose.HTML'yi kullanarak EPUB'u Java'da PDF'ye nasıl dönüştüreceğinizi öğrenin.
type: docs
weight: 12
url: /tr/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
---

## giriiş

Aspose.HTML for Java, HTML ve EPUB belgeleriyle çalışmak için güçlü bir araçtır. Bu adım adım kılavuzda, Aspose.HTML for Java kullanarak bir EPUB dosyasını PDF'ye dönüştürme sürecinde size yol göstereceğiz. İster deneyimli bir geliştirici olun ister yeni başlıyor olun, bu eğitim size bu görevi verimli bir şekilde gerçekleştirmek için gerekli bilgi ve becerileri sağlayacaktır.

## Önkoşullar

Başlamadan önce aşağıdaki önkoşulların mevcut olduğundan emin olun:

- Java Geliştirme Ortamı: Sisteminizde Java geliştirme ortamının kurulu olması gerekir.

-  Aspose.HTML for Java: Aspose.HTML for Java kitaplığını indirip yükleyin. Kütüphaneyi ve ilgili belgeleri şu adreste bulabilirsiniz:[İnternet sitesi](https://releases.aspose.com/html/java/).

- EPUB Dosyası: PDF'ye dönüştürmek istediğiniz bir EPUB dosyasına ihtiyacınız olacak.

Şimdi Aspose.HTML for Java kullanarak EPUB'u PDF'ye dönüştürmek için adım adım kılavuza bakalım.

## Adım 1: EPUB Dosyasını Açın

 Başlamak için mevcut bir EPUB dosyasını okumak üzere açın. Bir kullanabilirsiniz`FileInputStream` Bunu başarmak için. İşte bu adımın kodu:

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Sonraki adımlara ilişkin kodunuz buraya gelecek.
}
```

## 2. Adım: PDF Kaydetme Seçeneklerini Tanımlayın

 Bir örneğini oluşturun`PdfSaveOptions` özel sayfa boyutu ve arka plan rengiyle. Sayfa düzenini ihtiyaçlarınıza göre yapılandırabilirsiniz. Bunu nasıl yapabileceğiniz aşağıda açıklanmıştır:

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

## 3. Adım: EPUB'u PDF'ye dönüştürün

 Şimdi ara`ConvertEPUB` EPUB dosyasını PDF'ye dönüştürme yöntemi. Giriş akışını, PDF kaydetme seçeneklerini ve çıktı konumunu belirtin. İşte nasıl yapıldığı:

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

Tebrikler! Aspose.HTML for Java'yı kullanarak bir EPUB dosyasını başarıyla PDF'ye dönüştürdünüz. Artık dönüştürülen PDF dosyasına belirtilen çıktı konumundan erişebilirsiniz.

## Kaynak Kodunu Tamamlayın
```java
Specifying PDF Save Options for EPUB to PDF
        // Okumak için mevcut bir EPUB dosyasını açın.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Özel sayfa boyutuna ve arka plan rengine sahip bir PdfSaveOptions örneği oluşturun.
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
            // EPUB'u PDF'ye dönüştürmek için ConvertEPUB yöntemini çağırın.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```


## Çözüm

Bu eğitimde, EPUB dosyalarını PDF formatına dönüştürmek için Aspose.HTML for Java'nın nasıl kullanılacağını öğrendik. Bu çok yönlü kitaplık, geliştiricilere belge işleme için güçlü araçlar sağlar. Bu kılavuzda özetlenen adımları izleyerek EPUB'dan PDF'ye dönüştürmeyi Java uygulamalarınıza sorunsuz bir şekilde entegre edebilirsiniz.

## Sıkça Sorulan Sorular (SSS)

### Aspose.HTML for Java ücretsiz bir kütüphane midir?
 Aspose.HTML for Java ticari bir kütüphanedir, ancak ücretsiz deneme sürümünü buradan edinebilirsiniz.[İnternet sitesi](https://releases.aspose.com/).

### Dönüştürme için hangi EPUB formatları destekleniyor?
Aspose.HTML for Java, çeşitli EPUB formatlarının dönüştürülmesini destekleyerek çoğu EPUB belgesiyle uyumluluk sağlar.

### PDF çıktısını daha da özelleştirebilir miyim?
 Evet, sayfa düzenini, arka plan rengini ve diğer ayarları değiştirerek PDF çıktısını özelleştirebilirsiniz.`PdfSaveOptions`.

### Aspose.HTML for Java'nın deneme sürümünde herhangi bir sınırlama var mı?
Deneme sürümünün bazı sınırlamaları olabilir, bu nedenle ayrıntılar için belgelere göz atmanız önerilir.

### Aspose.HTML for Java desteğini nereden alabilirim?
Sorularınıza cevap bulabilir ve destek alabilirsiniz.[Aspose.HTML forumu](https://forum.aspose.com/).
