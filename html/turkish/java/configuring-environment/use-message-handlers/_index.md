---
date: 2026-02-10
description: Aspose'u kullanarak bozuk bağlantıları Java'da nasıl yöneteceğinizi,
  HTML'yi PNG'ye dönüştürmeyi ve Aspose.HTML for Java ile HTML belgesini Java'da nasıl
  yükleyeceğinizi öğrenin.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Java'da Aspose.HTML Mesaj İşleyicileriyle HTML'yi PNG'ye Dönüştür
url: /tr/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'yi PNG'ye Dönüştürme Aspose.HTML Mesaj İşleyicileri ile Java'da

## Giriş
Bu öğreticide **HTML'yi PNG'ye nasıl dönüştüreceğinizi** keşfedecek ve eksik kaynakları zarif bir şekilde yönetmek için Aspose.HTML for Java'yı kullanacaksınız. Var olmayan bir resmi işaret eden küçük bir HTML sayfası oluşturacağız, **özel bir mesaj işleyicisi** aracılığıyla **ağ isteklerini yakalayacağız**, **ağ servis**ini yapılandıracağız, belgeyi yükleyeceğiz ve sonunda **html'den görüntüye dönüşüm** gerçekleştireceğiz. Sonunda hem **kırık bağlantılar java** için sağlam bir desen hem de raporlar, küçük resimler veya e‑posta ön izlemeleri için yüksek kaliteli PNG çıktısı elde edeceksiniz.

## Hızlı Yanıtlar
- **Bir mesaj işleyicisi ne yapar?** Ağ işlemlerini (ör. resim istekleri) yakalar ve 404 gibi durum kodlarına yanıt vermenizi sağlar.  
- **Aspose.HTML HTML'yi PNG'ye dönüştürebilir mi?** Evet—`Converter.convertHTML` tek bir çağrıyla dönüşümü gerçekleştirir.  
- **Bu örnek için lisansa ihtiyacım var mı?** Geçici bir lisans değerlendirme sınırlamalarını kaldırır; üretim kullanımı için kalıcı lisans gereklidir.  
- **Hangi Java sürümü çalışır?** JDK 8+ (örnek JDK 11 üzerinde çalışır).  
- **Ağ servisini yapılandırabilir miyim?** Kesinlikle—`configuration.getService(INetworkService.class)` kullanarak işleyicinizi ekleyebilirsiniz.

## Önkoşullar
Başlamadan önce aşağıdakilerin hazır olduğundan emin olun:

1. **Java Development Kit (JDK)** – [Oracle web sitesinden](https://www.oracle.com/java/technologies/javase-downloads.html) indirin.  
2. **Aspose.HTML for Java** – Kütüphaneyi [Aspose releases sayfasından](https://releases.aspose.com/html/java/) edinin.  
3. **IDE** – IntelliJ IDEA, Eclipse veya NetBeans işinizi görecektir.  
4. **Temel Java bilgisi** – sınıflar, try‑with‑resources ve istisna yönetimi konularına hâkim olmalısınız.  
5. **Geçici Lisans** – Deneme sürümündeyseniz, filigranları önlemek için bir [geçici lisans](https://purchase.aspose.com/temporary-license/) alın.

## Paketleri İçe Aktarma
Dosya işlemleri için ihtiyacımız olan Java I/O sınıfını alalım. Geri kalan Aspose sınıfları daha sonra tam nitelikli adlarıyla referans verilecek, böylece import listesi sade kalır.

```java
import java.io.IOException;
```

## Adım 1: HTML Kodunu Hazırlama
Eksik bir resmi kasıtlı olarak referans eden minimal bir HTML parçacığı oluşturuyoruz. Bu, motor kaynağı almaya çalıştığında işleyicimizi tetikleyecek.

```java
String code = "<img src='missing.jpg'>";
```

## Adım 2: HTML Kodunu Bir Dosyaya Yazma
Parçacığı *document.html* dosyasına kalıcı hâle getiriyoruz. try‑with‑resources bloğu, `FileWriter`'ın düzgün kapanmasını garanti eder.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Adım 3: Özel Bir Mesaj İşleyicisi Yazma
Şimdi **özel bir mesaj işleyicisi** oluşturacağız; her ağ isteğinin HTTP durumunu kontrol eder. Yanıt `200` değilse dostça bir uyarı kaydeder. Zincirdeki bir sonraki işleyiciye geçişi sağlamak için `invoke(context);` çağrısına dikkat edin—bu, özyinelemeyi önler.

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

## Adım 4: Ağ Servisini Yapılandırma
Aspose.HTML'in işleyicimizi tanıması için, bir `Configuration` örneğinden **ağ servisini** alıp işleyiciyi koleksiyonuna ekliyoruz. İşte **ağ servisini yapılandırma** adımı.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Adım 5: HTML Belgesini Yükleme
Yapılandırma hazır olduğunda *document.html* dosyasını yüklüyoruz. Motor artık ağ servisimizi kullanacak, bu yüzden eksik resim isteği az önce eklediğimiz işleyici tarafından yakalanacak.

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
İşte **html'den görüntüye dönüşüm** sürecinin kalbi. `Converter.convertHTML` metodu, yüklenmiş `HTMLDocument`'i, isteğe bağlı `ImageSaveOptions` (DPI veya kalite ayarları gibi) ve çıktı dosya adını alır.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Adım 7: Kaynakları Temizleme
İyi bir Java pratiği, tüm yerel kaynakların serbest bırakılmasını gerektirir. `finally` bloğu, bir istisna yükselse bile `Configuration`'ın dispose edilmesini sağlar.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Neden Mesaj İşleyicileri Kullanmalı?
Mesaj işleyicileri, her ağ isteği üzerinde **ince ayarlı kontrol** sunar—resim, CSS, JavaScript veya font dosyası olsun. Kütüphanenin sessizce başarısız olmasına izin vermek yerine, eksik varlıkları kaydedebilir, yedek içerik sağlayabilir veya isteği yeniden deneyebilirsiniz. Bu, HTML işleme hattınızı **sağlam**, **üretim‑hazır** ve hata ayıklaması daha kolay hâle getirir.

## Yaygın Sorunlar ve Çözümler
- **İşleyici özyinelemesi** – Sonsuz döngüyü önlemek için `invoke(context);` sadece bir kez çağırın.  
- **Lisans eksikliği** – Geçerli bir lisans olmadan çıktı PNG'de filigran bulunur.  
- **Yanlış dosya yolları** – `document.html` yüklerken mutlak yollar kullanın veya çalışma dizinini doğru ayarlayın.  
- **Desteklenmeyen kaynak türleri** – Yakalamak istediğiniz kaynağın (resim, CSS vb.) HTML motoru tarafından gerçekten isteniyor olduğundan emin olun.

## Sık Sorulan Sorular

**S: Birden fazla mesaj işleyicisi zincirleyebilir miyim?**  
C: Evet, `network.getMessageHandlers()` koleksiyonuna birkaç işleyici ekleyebilirsiniz; ekleme sırasına göre çalıştırılırlar.

**S: İşleyici CSS veya script kaynakları için de çalışır mı?**  
C: Kesinlikle—HTML motoru tarafından yapılan tüm ağ istekleri (resimler, CSS, JS, fontlar) işleyiciden geçer.

**S: HTTP isteğini gönderilmeden önce nasıl değiştirebilirim?**  
C: `invoke(context)` çağrısının öncesinde `context.getRequest()`'i değiştiren bir işleyici uygulayın.

**S: Belirli URL'ler için uyarıyı nasıl devre dışı bırakırım?**  
C: İşleyicide `context.getRequest().getRequestUri()`'yi inceleyip koşullu olarak loglamayı atlayabilirsiniz.

**S: Bu API'lar için hangi Aspose.HTML sürümü gerekiyor?**  
C: Kod, Aspose.HTML for Java 22.10 ve sonrası sürümlerle çalışır.

## Sonuç
Artık **HTML'yi PNG'ye nasıl dönüştüreceğinizi**, **özel bir mesaj işleyicisi**yle **ağ isteklerini yakalayarak** ve **kırık bağlantılar java**'yı ele alarak gösteren eksiksiz bir uç‑uç örneğe sahipsiniz. Ağ servisini yapılandırıp belgeyi yükleyip dönüştürücüyü çağırarak, herhangi bir Java uygulamasında güvenilir şekilde PNG küçük resimleri veya tam sayfa ekran görüntüleri üretebilirsiniz.

---

**Son Güncelleme:** 2026-02-10  
**Test Edilen:** Aspose.HTML for Java 24.11  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}