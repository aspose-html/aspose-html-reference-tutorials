---
date: 2025-12-05
description: Aspose.HTML kullanarak Java'da HTML sayfa kenar boşluklarını nasıl ayarlayacağınızı
  öğrenin ve belgelerinize sayfa numaraları ve başlıklar ekleyin.
language: tr
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML ile Java’da HTML Sayfa Kenar Boşluklarını Nasıl Ayarlarsınız
url: /java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML Sayfa Kenar Boşluklarını Java ile Aspose.HTML Kullanarak Nasıl Ayarlarsınız

Bu öğreticide **HTML sayfa kenar boşluklarını Java**‑tarzı olarak Aspose.HTML for Java kullanarak nasıl ayarlayacağınızı keşfedeceksiniz. Özel sayfa kenar boşlukları oluşturmayı, sayfa numaraları eklemeyi ve bir belge başlığı eklemeyi adım adım, kopyalayıp projenize yapıştırabileceğiniz net kod örnekleriyle göstereceğiz.

## Hızlı Yanıtlar
- **Hangi kütüphane gerekiyor?** Aspose.HTML for Java  
- **Kenar boşluklarını programlı olarak kontrol edebilir miyim?** Evet, kullanıcı stil sayfasındaki bir CSS `@page` kuralı ile  
- **Hangi çıktı formatları kenar boşluklarını destekliyor?** XPS, PDF ve diğer raster formatlar  
- **Üretim için lisansa ihtiyacım var mı?** Deneme dışı kullanım için geçerli bir Aspose.HTML lisansı gereklidir  
- **Java 11+ ile uyumlu mu?** Kesinlikle – kütüphane modern Java sürümleriyle çalışır  

## “HTML Sayfa Kenar Boşluklarını Java ile Ayarlama” Nedir?
Java’da HTML sayfa kenar boşluklarını ayarlamak, Aspose.HTML tarafından sağlanan render motorunu, belge XPS veya PDF gibi yazdırılabilir bir formata dönüştürülmeden önce CSS sayfa‑kutusu özelliklerini uygulayacak şekilde yapılandırmak anlamına gelir. Özel bir `@page` kuralı tanımlayarak yazdırılabilir alanı, sayfa numaralarını ve üst/bottom içeriklerini kontrol edersiniz.

## Neden Kenar Kontrolü İçin Aspose.HTML Kullanmalı?
- **Kesin düzen** – CSS `@page` ile kenar boşlukları, üst‑alt bölümleri piksel‑tam hassasiyetle kontrol edebilirsiniz.  
- **Çoklu format tutarlılığı** – Aynı kenar tanımları XPS, PDF ve görüntü çıktıları için geçerlidir.  
- **Tarayıcı bağımlılığı yok** – Render sunucu‑tarafında gerçekleşir, headless tarayıcıya ihtiyaç duymazsınız.  

## Ön Koşullar

Başlamadan önce aşağıdaki ön koşulların karşılandığından emin olun:

1. **Java Geliştirme Ortamı** – JDK 11 veya daha yeni bir sürüm yüklü.  
2. **Aspose.HTML for Java** – Kütüphaneyi [buradan](https://releases.aspose.com/html/java/) indirip kurun.  

## Paketleri İçe Aktarma

Başlamak için gerekli Aspose.HTML sınıflarını içe aktarın:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## HTML Sayfa Kenar Boşluklarını Java – Adım Adım Kılavuz

### Adım 1: Yapılandırmayı Başlat ve Özel Sayfa Kenar Boşluklarını Tanımla

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
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

Bu blokta bir `Configuration` nesnesi oluşturur, `IUserAgentService` elde eder ve kenar boşluklarını, sağ‑alt sayfa sayacını ve üst‑orta belge başlığını tanımlayan bir CSS `@page` kuralı enjekte ederiz.

### Adım 2: HTML Belgesini Oluştur

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Burada basit bir “Hello World” snippet’i ile bir `HTMLDocument` örneği oluştururuz. Adım 1’deki aynı yapılandırma uygulanır, böylece özel kenar boşlukları belge render edildiğinde geçerli olur.

### Adım 3: XPS Dosyasına (veya desteklenen herhangi bir çıktıya) Render Et

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Bu adım, render edilen sayfaları `output.xps` dosyasına yazan bir `XpsDevice` oluşturur. Önceden tanımladığınız kenar boşlukları, sayfa numaraları ve başlık nihai dosyada görünecektir.

## Yaygın Sorunlar & İpuçları

- **Kenar boşlukları değişmemiş gibi görünüyor** – `@page` kuralının diğer stil sayfaları tarafından geçersiz kılınmadığından emin olun. `setUserStyleSheet` çağrısı en yüksek önceliği sağlar.  
- **Sayfa numaraları “NaN” gösteriyor** – Aspose.HTML 23.10 veya daha yeni bir sürüm kullandığınızı doğrulayın; eski sürümlerde `currentPageNumber()` işlevi bulunmaz.  
- **Çıktı dosyası boş** – `Resources.output` yolunun doğru çözüldüğünden ve yazma izniniz olduğundan emin olun.  

## Sıkça Sorulan Sorular

### S1: Aspose.HTML for Java nedir?

**C:** Aspose.HTML for Java, Java uygulamalarında HTML belgeleriyle çalışmak için dönüşüm, render ve manipülasyon gibi güçlü araçlar sunan bir Java kütüphanesidir.

### S2: Sayfa kenar boşluklarını daha da özelleştirebilir miyim?

**C:** Evet, `setUserStyleSheet` içindeki CSS’i düzenleyerek `margin-*` değerlerini değiştirebilir veya ek `@top-*` / `@bottom-*` kutuları ekleyebilirsiniz.

### S3: HTML belgesine daha fazla içerik ekleyebilir miyim?

**C:** `new HTMLDocument("<div>Hello World!!!</div>", …)` içindeki dizeyi kendi HTML işaretlemenizin ile değiştirin veya `HTMLDocument(String url, …)` yapıcısını kullanarak harici bir dosya yükleyin.

### S4: Aspose.HTML for Java diğer belge formatlarıyla uyumlu mu?

**C:** Kesinlikle. Aynı `HTMLDocument` PDF, XPS, görüntüler veya hatta EPUB gibi formatlara, çıkış cihazını (ör. `PdfDevice`, `PngDevice`) değiştirerek render edilebilir.

### S5: Aspose.HTML for Java kullanmak için lisansa ihtiyacım var mı?

**C:** Evet, üretim kullanımı için lisans gereklidir. Deneme lisansı alabilir veya lisansı [buradan](https://purchase.aspose.com/buy) ya da [buradan](https://releases.aspose.com/) satın alabilirsiniz.

### S6: Tek ve çift sayfalar için farklı kenar boşlukları ayarlayabilir miyim?

**C:** Stil sayfanıza `@page :left` ve `@page :right` pseudo‑class’larını ekleyerek sol‑el (çift) ve sağ‑el (tek) sayfalar için ayrı kenar boşlukları tanımlayabilirsiniz.

### S7: Render edilen belgede özel yazı tipleri gömebilir miyim?

**C:** Evet. Kullanıcı stil sayfasına `@font-face` kuralları ekleyip HTML içeriğinizde bu yazı tiplerine referans verin.

## Sonuç

Artık Aspose.HTML kullanarak **HTML sayfa kenar boşluklarını Java** ile nasıl ayarlayacağınızı, sayfa numaraları ve başlık ekleyerek belgelerinizi profesyonel bir görünüme kavuşturduğunuzu biliyorsunuz. Projenizin ihtiyaçlarına göre ek `@page` kutuları, özel yazı tipleri veya farklı çıktı formatlarıyla denemeler yapmaktan çekinmeyin.

Herhangi bir sorunla karşılaşırsanız, resmi [Aspose.HTML for Java belgeleri](https://reference.aspose.com/html/java/) ve [Aspose destek forumu](https://forum.aspose.com/) mükemmel yardım kaynaklarıdır.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Son Güncelleme:** 2025-12-05  
**Test Edilen Sürüm:** Aspose.HTML for Java 23.12  
**Yazar:** Aspose  

---