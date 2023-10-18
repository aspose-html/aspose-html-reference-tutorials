---
title: Aspose.HTML ile HTML Sayfa Kenar Boşluklarını Özelleştirin
linktitle: CSS Uzantıları - Başlık ve Sayfa Numarası Ekleme
second_title: Aspose.HTML ile Java HTML İşleme
description: Aspose.HTML for Java kullanarak sayfa kenar boşluklarını nasıl özelleştireceğinizi, HTML belgelerine sayfa numaraları ve başlıklar eklemeyi öğrenin.
type: docs
weight: 10
url: /tr/java/advanced-usage/css-extensions-adding-title-page-number/
---
Aspose.HTML for Java, Java uygulamalarında HTML belgelerini işlemek için güçlü bir kütüphanedir. Bu eğitimde Aspose.HTML for Java kullanarak özel sayfa kenar boşlukları oluşturmayı ve HTML belgelerinize sayfa numaralarını ve başlıklarını nasıl ekleyeceğinizi inceleyeceğiz. Bu adım adım kılavuz, bu özellikleri HTML belgelerinize kolayca entegre etmenize yardımcı olmak için süreci yönetilebilir adımlara ayıracaktır.

## Önkoşullar

Başlamadan önce aşağıdaki önkoşulların mevcut olduğundan emin olun:

1. Java Geliştirme Ortamı: Bilgisayarınızda bir Java geliştirme ortamının kurulu olduğundan emin olun.

2.  Aspose.HTML for Java: Aspose.HTML for Java kütüphanesini şu adresten indirip yükleyin:[Burada](https://releases.aspose.com/html/java/).

## Paketleri İçe Aktar

Başlamak için gerekli paketleri Aspose.HTML for Java'dan içe aktarmanız gerekir. Aşağıdaki içe aktarma ifadelerini Java kodunuza ekleyin:

```java
// Aspose.HTML paketlerini içe aktar
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

Şimdi özel sayfa kenar boşluklarını, sayfa numaralarını ve başlıkları ekleme sürecini yönetilebilir adımlara ayıralım:

## 1. Adım: Yapılandırmayı ve Sayfa Kenar Boşluklarını Başlatın

```java
// Yapılandırma nesnesini başlatın ve belge için sayfa kenar boşluklarını ayarlayın
Configuration configuration = new Configuration();
try {
    // Kullanıcı Aracısı hizmetini edinin
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Özel kenar boşluklarının stilini ayarlayın ve üzerinde işaretler oluşturun
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

Bu adımda, yapılandırma nesnesini başlatıyoruz ve sayfa sayacının ve sayfa başlığının konumu da dahil olmak üzere özel sayfa kenar boşluklarını ayarlıyoruz.

## Adım 2: Bir HTML Belgesini Başlatın

```java
// Bir HTML belgesini başlat
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Burada örnek içerikli bir HTML belgesi oluşturuyoruz (bu durumda bir "Merhaba Dünya" mesajı) ve 1. Adımdaki yapılandırmayı uyguluyoruz.

## Adım 3: Bir Çıkış Aygıtını Başlatın ve Belgeyi Oluşturun

```java
// Bir çıkış cihazını başlat
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    //Belgeyi çıkış aygıtına gönderin
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Bu adımda bir çıktı cihazı kuruyoruz ve HTML belgesini oluşturuyoruz. Belge işlenecek ve belirtilen sayfa kenar boşlukları, sayfa numaraları ve başlıkla bir XPS dosyası olarak kaydedilecektir.

## Çözüm

Tebrikler! Aspose.HTML for Java'yı kullanarak özel sayfa kenar boşlukları oluşturmayı ve HTML belgelerinize sayfa numaralarını ve başlıklarını nasıl ekleyeceğinizi başarıyla öğrendiniz. Bu özelleştirme, daha profesyonel ve görsel olarak çekici belgeler oluşturmanıza olanak tanır.

 Herhangi bir sorunuz varsa veya herhangi bir sorunla karşılaşırsanız, ziyaret etmekten çekinmeyin.[Java belgeleri için Aspose.HTML](https://reference.aspose.com/html/java/) veya bu konuda yardım isteyin[Aspose destek forumu](https://forum.aspose.com/).

## SSS'ler

### S1: Java için Aspose.HTML nedir?

Cevap1: Aspose.HTML for Java, Java uygulamalarında HTML belgeleriyle çalışmak için güçlü araçlar sağlayan bir Java kütüphanesidir.

### S2: Sayfa kenar boşluklarını daha da özelleştirebilir miyim?

C2: Evet, sayfa kenar boşluklarını gereksinimlerinize göre özelleştirmek için 1. Adımda CSS stillerini değiştirebilirsiniz.

### S3: HTML belgesine nasıl daha fazla içerik ekleyebilirim?

C3: Örnek içeriği kendi içeriğinizle değiştirerek 2. Adımda HTML içeriğini değiştirebilirsiniz.

### S4: Aspose.HTML for Java diğer belge formatlarıyla uyumlu mudur?

Cevap4: Evet, Aspose.HTML for Java, HTML belgelerini PDF, XPS ve görseller dahil olmak üzere çeşitli formatlara dönüştürmek için kullanılabilir.

### S5: Aspose.HTML for Java'yı kullanmak için lisansa ihtiyacım var mı?

 C5: Evet, adresinden lisans veya ücretsiz deneme sürümü alabilirsiniz.[Burada](https://purchase.aspose.com/buy) veya[Burada](https://releases.aspose.com/).