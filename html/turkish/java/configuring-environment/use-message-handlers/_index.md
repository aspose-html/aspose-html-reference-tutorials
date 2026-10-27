---
date: 2026-05-04
description: Aspose.HTML for Java kullanarak html'den png'ye dönüşüm, ağ isteklerini
  yakalama (java) ve bozuk bağlantıları (java) nasıl ele alacağınızı öğrenin.
keywords:
- html to png conversion
- intercept network requests java
- html to image conversion
- load html document java
- handle broken links java
linktitle: Aspose.HTML'de Mesaj İşleyicilerini Kullanın
second_title: Java HTML Processing with Aspose.HTML
title: Java'da Aspose.HTML Mesaj İşleyicileri ile HTML'den PNG'ye Dönüştürme
url: /tr/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Aspose.HTML Mesaj İşleyicileri ile HTML'den PNG'ye Dönüştürme

## HTML'den PNG Dönüştürmeye Giriş
Bu öğreticide, Aspose.HTML for Java kullanarak eksik kaynakları zarif bir şekilde yönetirken **HTML'den PNG'ye nasıl dönüştürüleceğini** keşfedeceksiniz. Var olmayan bir görsele işaret eden küçük bir HTML sayfası oluşturmayı, **özel bir mesaj işleyicisi** ile **ağ isteklerini yakalamayı**, **ağ hizmetini** yapılandırmayı, belgeyi yüklemeyi ve sonunda **html'den görüntüye dönüştürmeyi** adım adım göstereceğiz. Sonunda, **handle broken links java** ve yüksek kaliteli PNG çıktısı için sağlam bir deseniniz olacak—raporlar, küçük resimler veya e-posta ön izlemeleri için mükemmel.

## Hızlı Yanıtlar
- **Bir mesaj işleyicisi ne yapar?** Ağ işlemlerini (örneğin görüntü isteklerini) yakalar ve 404 gibi durum kodlarına tepki vermenizi sağlar.  
- **Aspose.HTML HTML'yi PNG'ye dönüştürebilir mi?** Evet—`Converter.convertHTML` dönüşümü tek bir çağrıda gerçekleştirir.  
- **Bu örnek için lisansa ihtiyacım var mı?** Geçici bir lisans değerlendirme sınırlamalarını kaldırır; üretim kullanımı için kalıcı bir lisans gereklidir.  
- **Hangi Java sürümü çalışır?** JDK 8+ herhangi bir sürüm (örnek JDK 11'de çalışır).  
- **Ağ hizmetini yapılandırabilir miyim?** Kesinlikle—`configuration.getService(INetworkService.class)` kullanarak işleyicinizi ekleyin.

## HTML'den PNG Dönüştürme Nedir?
HTML'den PNG'ye dönüşüm, bir web sayfasını (veya HTML parçacığını) raster bir görüntüye render eder. Dinamik içeriğin statik ön izlemelerine ihtiyaç duyduğunuzda, e-posta bültenleri için küçük resimler oluşturmak veya web sayfalarını görüntü olarak arşivlemek istediğinizde faydalıdır.

## Neden Java'da Ağ İsteklerini Yakalamak İçin Mesaj İşleyicileri Kullanılır?
Mesaj işleyicileri, her ağ isteği üzerinde **ince ayarlı kontrol** sağlar—ister görüntü, CSS, JavaScript, ister font dosyası olsun. Bu istekleri yakalayarak **eksik varlıkları kaydedebilir**, yedek içerik sağlayabilir veya başarısız indirmeleri yeniden deneyebilirsiniz; bu da HTML işleme hattınızı **sağlam** ve **üretime hazır** hâle getirir.

## Önkoşullar
1. **Java Development Kit (JDK)** – [Oracle web sitesinden](https://www.oracle.com/java/technologies/javase-downloads.html) indirin.  
2. **Aspose.HTML for Java** – kütüphaneyi [Aspose sürüm sayfasından](https://releases.aspose.com/html/java/) edinin.  
3. **IDE** – IntelliJ IDEA, Eclipse veya NetBeans sorunsuz çalışır.  
4. **Temel Java bilgisi** – sınıflar, try‑with‑resources ve istisna yönetimi konusunda rahat olmalısınız.  
5. **Geçici Lisans** – deneme sürümündeyseniz, filigranları önlemek için bir [geçici lisans](https://purchase.aspose.com/temporary-license/) alın.

## Paketleri İçe Aktarma
İlk olarak, dosya işlemleri için ihtiyacımız olan Java I/O sınıfını içe aktarın. Geri kalan Aspose sınıfları daha sonra tam nitelikli adlarıyla referans verilir, böylece import listesi düzenli kalır.

```java
import java.io.IOException;
```

## Adım 1: HTML Kodunu Hazırlama
Eksik bir görüntüyü kasıtlı olarak referans eden minimal bir HTML snippet'i oluşturuyoruz. Motor kaynağı almaya çalıştığında bu, işleyicimizi tetikleyecek.

```java
String code = "<img src='missing.jpg'>";
```

## Adım 2: HTML Kodunu Bir Dosyaya Yazma
Sonra, snippet'i *document.html* dosyasına kaydediyoruz. try‑with‑resources bloğu kullanmak, `FileWriter`'ın düzgün şekilde kapatılmasını garanti eder.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Adım 3: Özel Bir Mesaj İşleyicisi Yazma
Şimdi, her ağ isteğinin HTTP durumunu kontrol eden bir **özel mesaj işleyicisi** oluşturuyoruz. Yanıt `200` değilse, dostça bir uyarı kaydediyoruz. Sonundaki `invoke(context);` çağrısına dikkat edin—bu, isteği zincirdeki bir sonraki işleyiciye yönlendirir ve özyinelemeyi önler.

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

## Adım 4: Ağ Hizmetini Yapılandırma
Aspose.HTML'in işleyicimizi tanıması için, bir `Configuration` örneğinden **ağ hizmetini** alıp işleyiciyi koleksiyonuna ekliyoruz. Bu adım, özel davranış için **ağ hizmetini yapılandırdığımız** adımdır.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Adım 5: HTML Belgesini Yükleme
Yapılandırma hazır olduğunda, *document.html* dosyasını yüklüyoruz. Motor artık bizim ağ hizmetimizi kullanıyor, böylece eksik görüntü isteği az önce eklediğimiz işleyici tarafından yakalanıyor.

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

## Adım 6: HTML'yi PNG'ye Dönüştürme
İşte **html'den görüntüye dönüştürme** sürecinin kalbi. `Converter.convertHTML` metodu, yüklenmiş `HTMLDocument`, isteğe bağlı `ImageSaveOptions` (DPI veya kaliteyi ayarlayabileceğiniz) ve çıktı dosya adını alır.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Adım 7: Kaynakları Temizleme
İyi bir Java uygulaması, tüm yerel kaynakları serbest bırakmamızı önerir. `finally` bloğu, bir istisna yükselse bile `Configuration`'ın serbest bırakılmasını sağlar.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Yaygın Sorunlar ve Çözümler
- **İşleyici özyinelemesi** – Sonsuz döngüleri önlemek için `invoke(context);` sadece bir kez çağırın.  
- **Lisans eksikliği** – Geçerli bir lisans olmadan çıktı PNG bir filigran içerir.  
- **Yanlış dosya yolları** – `document.html` yüklerken mutlak yollar kullanın veya çalışma dizinini doğru ayarlayın.  
- **Desteklenmeyen kaynak türleri** – Yakalamak istediğiniz kaynağın (görsel, CSS vb.) gerçekten HTML motoru tarafından istenip istenmediğini kontrol edin.

## Sıkça Sorulan Sorular

**S: Birden fazla mesaj işleyicisini zincirleyebilir miyim?**  
C: Evet, `network.getMessageHandlers()` koleksiyonuna birden fazla işleyici ekleyebilirsiniz; eklenme sırasına göre çalıştırılacaklar.

**S: İşleyici CSS veya script kaynakları için de çalışır mı?**  
C: Kesinlikle—HTML motoru tarafından yapılan herhangi bir ağ isteği (görseller, CSS, JS, fontlar) işleyiciden geçer.

**S: Gönderilmeden önce HTTP isteğini nasıl değiştirebilirim?**  
C: `invoke(context)` çağırmadan önce `context.getRequest()`'i değiştiren bir işleyici uygulayın.

**S: Belirli URL'ler için uyarıyı bastırmanın bir yolu var mı?**  
C: İşleyici içinde `context.getRequest().getRequestUri()`'yi inceleyerek koşullu olarak loglamayı atlayabilirsiniz.

**S: Bu API'ler için hangi Aspose.HTML sürümü gereklidir?**  
C: Kod, Aspose.HTML for Java 22.10 ve sonrası ile çalışır.

---

**Son Güncelleme:** 2026-05-04  
**Test Edilen:** Aspose.HTML for Java 24.11  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}