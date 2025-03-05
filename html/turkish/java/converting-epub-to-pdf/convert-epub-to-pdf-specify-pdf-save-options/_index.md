---
title: EPUB'dan PDF'e PDF Kaydetme Seçeneklerini Belirleme
linktitle: EPUB'dan PDF'e PDF Kaydetme Seçeneklerini Belirleme
second_title: Aspose.HTML ile Java HTML İşleme
description: Güçlü bir HTML düzenleme kütüphanesi olan Aspose.HTML'i kullanarak Java'da EPUB'u PDF'ye nasıl dönüştüreceğinizi öğrenin.
type: docs
weight: 12
url: /tr/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
---

## giriiş

Java için Aspose.HTML, HTML ve EPUB belgeleriyle çalışmak için güçlü bir araçtır. Bu adım adım kılavuzda, Aspose.HTML for Java kullanarak bir EPUB dosyasını PDF'ye dönüştürme sürecinde size yol göstereceğiz. İster deneyimli bir geliştirici olun, ister yeni başlıyor olun, bu eğitim size bu görevi etkili bir şekilde gerçekleştirmek için gereken bilgi ve becerileri sağlayacaktır.

## Ön koşullar

Başlamadan önce aşağıdaki ön koşulların mevcut olduğundan emin olun:

- Java Geliştirme Ortamı: Sisteminizde bir Java geliştirme ortamının kurulu olması gerekir.

-  Java için Aspose.HTML: Java için Aspose.HTML kitaplığını indirin ve kurun. Kitaplığı ve ilgili belgeleri şu adreste bulabilirsiniz:[web sitesi](https://releases.aspose.com/html/java/).

- EPUB Dosyası: PDF'ye dönüştürmek istediğiniz bir EPUB dosyasına ihtiyacınız olacak.

Şimdi, Java için Aspose.HTML kullanarak EPUB'ı PDF'ye dönüştürmeye yönelik adım adım kılavuza geçelim.

## Adım 1: EPUB Dosyasını Açın

 Başlamak için, okumak üzere mevcut bir EPUB dosyasını açın. Bir`FileInputStream` Bunu başarmak için. İşte bu adım için kod:

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Bundan sonraki adımlar için kodunuz buraya gelecek.
}
```

## Adım 2: PDF Kaydetme Seçeneklerini Tanımlayın

 Bir örnek oluşturun`PdfSaveOptions` özel sayfa boyutu ve arka plan rengiyle. Sayfa kurulumunu gereksinimlerinize göre yapılandırabilirsiniz. İşte bunu nasıl yapabileceğiniz:

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

## Adım 3: EPUB'ı PDF'ye dönüştürün

 Şimdi, arayın`ConvertEPUB` EPUB dosyasını PDF'ye dönüştürme yöntemi. Giriş akışını, PDF kaydetme seçeneklerini ve çıktı konumunu belirtin. İşte nasıl yapıldığı:

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

Tebrikler! Aspose.HTML for Java kullanarak bir EPUB dosyasını başarıyla PDF'ye dönüştürdünüz. Artık dönüştürülen PDF dosyasına belirtilen çıktı konumundan erişebilirsiniz.

## Tam Kaynak Kodu
```java
Specifying PDF Save Options for EPUB to PDF
        // Mevcut bir EPUB dosyasını okumak için açın.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Özel bir sayfa boyutu ve arka plan rengiyle PdfSaveOptions örneğini oluşturun.
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
            // EPUB'ı PDF'e dönüştürmek için ConvertEPUB metodunu çağırın.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```


## Çözüm

Bu eğitimde, EPUB dosyalarını PDF formatına dönüştürmek için Java için Aspose.HTML'i nasıl kullanacağımızı öğrendik. Bu çok yönlü kitaplık, geliştiricilere belge düzenleme için güçlü araçlar sağlar. Bu kılavuzda özetlenen adımları izleyerek, EPUB'dan PDF'e dönüştürmeyi Java uygulamalarınıza sorunsuz bir şekilde entegre edebilirsiniz.

## Sıkça Sorulan Sorular (SSS)

### Aspose.HTML for Java ücretsiz bir kütüphane midir?
 Java için Aspose.HTML ticari bir kütüphanedir, ancak ücretsiz deneme sürümünü kendilerinden edinebilirsiniz.[web sitesi](https://releases.aspose.com/).

### Dönüştürme için hangi EPUB formatları destekleniyor?
Java için Aspose.HTML, çeşitli EPUB formatlarının dönüştürülmesini destekleyerek çoğu EPUB belgesiyle uyumluluğu garanti eder.

### PDF çıktısını daha fazla özelleştirebilir miyim?
 Evet, sayfa düzenini, arka plan rengini ve diğer ayarları düzenleyerek PDF çıktısını özelleştirebilirsiniz.`PdfSaveOptions`.

### Aspose.HTML for Java'nın deneme sürümünde herhangi bir sınırlama var mı?
Deneme sürümünün bazı kısıtlamaları olabilir, bu nedenle ayrıntılar için dokümanları kontrol etmeniz önerilir.

### Java için Aspose.HTML desteğini nereden alabilirim?
Sorularınıza cevap bulabilir ve destek alabilirsiniz.[Aspose.HTML forumu](https://forum.aspose.com/).
