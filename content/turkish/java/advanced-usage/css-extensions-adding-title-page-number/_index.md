---
title: Aspose.HTML ile HTML Sayfa Kenar Boşluklarını Özelleştirin
linktitle: CSS Uzantıları - Başlık ve Sayfa Numarası Ekleme
second_title: Aspose.HTML ile Java HTML İşleme
description: Aspose.HTML for Java kullanarak HTML belgelerine sayfa kenar boşluklarını nasıl özelleştireceğinizi, sayfa numaralarını ve başlıkları nasıl ekleyeceğinizi öğrenin.
type: docs
weight: 10
url: /tr/java/advanced-usage/css-extensions-adding-title-page-number/
---
Java için Aspose.HTML, Java uygulamalarında HTML belgelerini işlemek için güçlü bir kütüphanedir. Bu eğitimde, Aspose.HTML for Java kullanarak özel sayfa kenar boşlukları oluşturmayı ve HTML belgelerinize sayfa numaraları ve başlıklar eklemeyi inceleyeceğiz. Bu adım adım kılavuz, bu özellikleri HTML belgelerinize kolayca entegre etmenize yardımcı olmak için süreci yönetilebilir adımlara bölecektir.

## Ön koşullar

Başlamadan önce aşağıdaki ön koşulların mevcut olduğundan emin olun:

1. Java Geliştirme Ortamı: Bilgisayarınızda bir Java geliştirme ortamının kurulu olduğundan emin olun.

2.  Java için Aspose.HTML: Java için Aspose.HTML kitaplığını şu adresten indirin ve yükleyin:[Burada](https://releases.aspose.com/html/java/).

## Paketleri İçe Aktar

Başlamak için, Java için Aspose.HTML'den gerekli paketleri içe aktarmanız gerekir. Java kodunuza aşağıdaki içe aktarma ifadelerini ekleyin:

```java
// Aspose.HTML paketlerini içe aktarın
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

Şimdi, özel sayfa kenar boşlukları, sayfa numaraları ve başlıklar ekleme sürecini yönetilebilir adımlara bölelim:

## Adım 1: Yapılandırmayı ve Sayfa Kenar Boşluklarını Başlatın

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

Bu adımda yapılandırma nesnesini başlatıyoruz ve sayfa sayacının ve sayfa başlığının konumu da dahil olmak üzere özel sayfa kenar boşluklarını ayarlıyoruz.

## Adım 2: Bir HTML Belgesi Başlatın

```java
// Bir HTML belgesini başlatın
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Burada, örnek bir içerik (bu durumda bir "Merhaba Dünya" mesajı) içeren bir HTML belgesi oluşturuyoruz ve 1. Adımdaki yapılandırmayı uyguluyoruz.

## Adım 3: Bir Çıktı Aygıtı Başlatın ve Belgeyi İşleyin

```java
// Bir çıktı aygıtını başlat
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    //Belgeyi çıktı aygıtına gönder
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Bu adımda bir çıktı aygıtı ayarlayıp HTML belgesini oluşturuyoruz. Belge işlenecek ve belirtilen sayfa kenar boşlukları, sayfa numaraları ve başlıkla bir XPS dosyası olarak kaydedilecek.

## Çözüm

Tebrikler! Aspose.HTML for Java kullanarak HTML belgelerinize özel sayfa kenar boşlukları oluşturmayı ve sayfa numaraları ve başlıklar eklemeyi başarıyla öğrendiniz. Bu özelleştirme, daha profesyonel ve görsel olarak çekici belgeler oluşturmanıza olanak tanır.

 Herhangi bir sorunuz varsa veya herhangi bir sorunla karşılaşırsanız, lütfen şu adresi ziyaret edin:[Java için Aspose.HTML belgeleri](https://reference.aspose.com/html/java/) veya yardım isteyin[Aspose destek forumu](https://forum.aspose.com/).

## SSS

### S1: Java için Aspose.HTML nedir?

A1: Aspose.HTML for Java, Java uygulamalarında HTML belgeleriyle çalışmak için güçlü araçlar sağlayan bir Java kütüphanesidir.

### S2: Sayfa kenar boşluklarını daha fazla özelleştirebilir miyim?

C2: Evet, 1. Adımda CSS stillerini değiştirerek sayfa kenar boşluklarını ihtiyaçlarınıza göre özelleştirebilirsiniz.

### S3: HTML belgesine nasıl daha fazla içerik ekleyebilirim?

C3: Adım 2'deki örnek içeriği kendi içeriğinizle değiştirerek HTML içeriğini değiştirebilirsiniz.

### S4: Aspose.HTML for Java diğer belge formatlarıyla uyumlu mudur?

C4: Evet, Aspose.HTML for Java, HTML belgelerini PDF, XPS ve resimler dahil olmak üzere çeşitli biçimlere dönüştürmek için kullanılabilir.

### S5: Java için Aspose.HTML kullanmak için lisansa ihtiyacım var mı?

 A5: Evet, lisans veya ücretsiz denemeyi şu adresten edinebilirsiniz:[Burada](https://purchase.aspose.com/buy) veya[Burada](https://releases.aspose.com/).