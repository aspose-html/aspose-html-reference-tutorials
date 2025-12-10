---
date: 2025-12-10
description: Aspose'u kullanarak kırık bağlantıları Java'da nasıl yöneteceğinizi,
  HTML'yi PNG'ye dönüştürmeyi ve Aspose.HTML for Java ile HTML belgesini Java'da nasıl
  yükleyeceğinizi öğrenin.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Aspose.HTML Mesaj İşleyicilerini Java'da Nasıl Kullanılır
url: /tr/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML Mesaj İşleyicilerini Java'da Nasıl Kullanılır

## Introduction
Bu öğreticide, **how to use aspose** HTML'de eksik kaynakları ele almak için adım adım gösterilmektedir. Eksik bir görüntüye referans veren basit bir HTML belgesi oluşturacağız, özel bir mesaj işleyicisi ekleyeceğiz ve kırık bağlantıları zarif bir şekilde ele alırken **load html document java** nasıl yapılır gösterilecektir. Sonunda, Aspose.HTML kullanarak **convert html to png** nasıl yapılır da göreceksiniz; bu da Java'da HTML‑to‑image dönüşümünün tam bir resmini sunar.

## Quick Answers
- **Message handler'ın temel amacı nedir?** Ağ işlemlerini yakalamak ve eksik kaynaklar gibi durum kodlarına yanıt vermektir.  
- **Aspose.HTML HTML'yi PNG'ye dönüştürebilir mi?** Evet, `Converter.convertHTML` kullanarak html'den görüntüye dönüşüm yapabilirsiniz.  
- **Bu örnek için lisansa ihtiyacım var mı?** Geçici bir lisans değerlendirme sınırlamalarını kaldırır; üretim için kalıcı bir lisans gereklidir.  
- **Hangi Java sürümü destekleniyor?** JDK 8+ (ders JDK 11 kullanıyor).  
- **Birden fazla kırık bağlantıyı işlemek mümkün mü?** Kesinlikle – farklı senaryoları yönetmek için birden fazla handler zincirleyebilirsiniz.

## Prerequisites
Adım adım kılavuza başlamadan önce, ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım:
1. Java Development Kit (JDK): Sisteminizde JDK kurulu olduğundan emin olun. [Oracle web sitesinden](https://www.oracle.com/java/technologies/javase-downloads.html) indirebilirsiniz.  
2. Aspose.HTML for Java: Aspose.HTML for Java kurulu olmalıdır. [Aspose sürüm sayfasından](https://releases.aspose.com/html/java/) indirebilirsiniz.  
3. IDE: IntelliJ IDEA, Eclipse veya NetBeans gibi sevdiğiniz Java Entegre Geliştirme Ortamını (IDE) kullanın.  
4. Java Temel Bilgisi: Java programlamaya aşina olmak, bu kılavuzu etkili bir şekilde takip etmek için gereklidir.  
5. Geçici Lisans: Aspose.HTML'in deneme sürümünü kullanıyorsanız, geliştirme sırasında sınırlamalardan kaçınmak için bir [geçici lisans](https://purchase.aspose.com/temporary-license/) almayı düşünün.

## Import Packages
Başlamadan önce, Java projenize gerekli paketlerin import edildiğinden emin olun. Aşağıda ihtiyacınız olan temel import'lar yer almaktadır:
```java
import java.io.IOException;
```
Bu import'lar, ağ işlemlerini yönetmek, HTML belgeleri oluşturmak ve HTML‑to‑PNG dönüşümünü gerçekleştirmek için gerekli sınıf ve metodlara erişmenizi sağlar.

## Step 1: Prepare the HTML Code
İlk olarak, bir görüntü dosyasına referans veren basit bir HTML snippet'ine ihtiyacımız var. Hata işleme mekanizmasını tetiklemek için var olmayan bir görüntüye kasıtlı olarak referans vereceğiz.
```java
String code = "<img src='missing.jpg'>";
```
Bu kod, `missing.jpg`'ye işaret eden bir `<img>` etiketi oluşturur. Görüntü eksik olduğu için ağ servisi 200 olmayan bir durum kodu dönecek ve bu bizim özel handler'ımız yakalayacak.

## Step 2: Write the HTML Code to a File
Sonra, Aspose.HTML'in belge olarak yükleyebilmesi için HTML snippet'ini kalıcı hale getirmemiz gerekiyor.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
`FileWriter` kullanarak HTML'i **document.html** dosyasına kaydediyoruz. Bu dosya, daha sonra **load html document java** adımının kaynağı olur.

## Step 3: Create a Custom Message Handler
Şimdi, görüntü bulunamadığında tepki veren özel bir mesaj işleyicisi oluşturalım. Handler HTTP durum kodunu kontrol eder ve dostça bir mesaj yazdırır.
```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```
`invoke` metodu `context.getResponse().getStatusCode()` inceler. Eğer **200** değilse, dosyanın eksik olduğuna dair net bir uyarı veririz. Son `invoke(context);` çağrısı, kontrolü zincirdeki bir sonraki handler'a aktarır.

## Step 4: Configure the Network Service
Aspose.HTML'in handler'ımızı tanıması için, onu `Configuration` sınıfı aracılığıyla ağ servisine kaydediyoruz.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Burada bir `Configuration` örneği oluşturuyor, `INetworkService`'i alıyor ve özel handler'ımızı koleksiyonuna ekliyoruz. Bu, handler'ın görüntü yükleme gibi herhangi bir ağ isteği sırasında çalışmasını sağlar.

## Step 5: Load the HTML Document
Yapılandırma hazır olduğunda, daha önce oluşturduğumuz HTML dosyasını yükleyebiliriz. Bu adım, eksik görüntünün handler'ımızı tetiklediği **load html document java**'yu gösterir.
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```
`HTMLDocument` yapıcı, dosya yolunu ve özel `configuration`'ı alır. Belge `<img>` etiketini ayrıştırdığında, ağ servisi `missing.jpg`'yi almaya çalışır, 404 alır ve handler'ımız uyarıyı yazdırır.

## Step 6: Convert HTML to PNG
Aspose.HTML'in daha geniş yeteneklerini göstermek için, yüklenen belgeyi PNG görüntüsüne dönüştüreceğiz. Bu klasik bir **convert html to png** senaryosudur.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML`, `HTMLDocument`, isteğe bağlı `ImageSaveOptions` (DPI, kalite vb. ayarlayabileceğiniz) ve çıktı dosya adını alır. Sonuç, render edilen HTML'in raster görüntüsüdür.

## Step 7: Clean Up Resources
Doğru kaynak yönetimi, herhangi bir Java uygulamasında esastır. Bellek sızıntılarını önlemek için hem `Configuration` hem de `HTMLDocument` nesnelerini serbest bırakıyoruz.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Temizleme işlemini bir `finally` bloğuna sarmak, daha önce bir istisna oluşsa bile çalışmasını garanti eder.

## Why Use Message Handlers?
Mesaj işleyicileri, **handle broken links java** gibi ağ işlemleri üzerinde ayrıntılı kontrol sağlar. Kütüphanenin sessizce başarısız olmasına izin vermek yerine, günlük kaydı tutabilir, yeniden deneyebilir, kaynakları değiştirebilir veya yedek içerik sağlayabilirsiniz—bu da HTML işleme sürecinizi sağlam ve üretime hazır hâle getirir.

## Common Issues and Solutions
- **Handler özyinelemesi** – Sonsuz döngüleri önlemek için `invoke(context);` çağrısını yalnızca bir kez yaptığınızdan emin olun.  
- **Lisans eksikliği** – Geçerli bir lisans olmadan dönüşüm su işareti (watermark) içeren bir görüntü üretebilir.  
- **Dosya yolu hataları** – `document.html` yüklerken mutlak yollar kullanın veya çalışma dizinini doğru ayarlayın.

## Frequently Asked Questions

**S: Birden fazla mesaj işleyicisi zincirleyebilir miyim?**  
C: Evet, `network.getMessageHandlers()` koleksiyonuna birden fazla handler ekleyebilirsiniz; ekleme sırasına göre çalıştırılırlar.

**S: Handler CSS veya script kaynakları için de çalışır mı?**  
C: Kesinlikle—HTML motoru tarafından yapılan herhangi bir ağ isteği (görüntüler, CSS, JS, fontlar) handler üzerinden geçer.

**S: HTTP isteğini gönderilmeden önce nasıl değiştirebilirim?**  
C: `invoke(context)` çağrısından önce `context.getRequest()`'i değiştiren bir handler uygulayın.

**S: Belirli URL'ler için uyarıyı bastırmanın bir yolu var mı?**  
C: Handler içinde `context.getRequest().getRequestUri()`'yi inceleyerek koşullu olarak loglamayı atlayabilirsiniz.

**S: Bu API'ler için hangi Aspose.HTML sürümü gerekiyor?**  
C: Kod, Aspose.HTML for Java 22.10 ve üzeri sürümlerle çalışır.

## Conclusion
İşte bu kadar—Java'da **how to use aspose** mesaj işleyicileri üzerine kapsamlı bir rehber. HTML dosyası oluşturmayı, **handle broken links java** için özel bir handler bağlamayı, belgeyi yüklemeyi ve **convert html to png** işlemini gerçekleştirmeyi ele aldık. Bu desenle eksik kaynakları güvenle yönetebilir, özel politikalar uygulayabilir ve Aspose.HTML'in ağ yeteneklerini herhangi bir Java uygulamasında genişletebilirsiniz.

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.HTML for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}