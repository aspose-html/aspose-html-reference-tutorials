---
date: 2025-12-05
description: Aspose.HTML for Java kullanarak özel hata yönetimiyle HTML dosyası oluşturmayı,
  ağ kaynaklarını yönetmeyi ve HTML'yi PNG'ye dönüştürmeyi öğrenin.
language: tr
linktitle: Set Up Network Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: HTML Dosyası Oluştur ve Ağ Servisini Kur (Aspose.HTML Java)
url: /java/configuring-environment/setup-network-service/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML Dosyası Oluşturma ve Ağ Servisini Kurma (Aspose.HTML Java)

## Introduction
Eğer web'den resimleri çeken ve ardından bu sayfayı bir resme dönüştüren **html dosyası oluşturmanız** gerekiyorsa, doğru yerdesiniz. Bu öğreticide, Aspose.HTML for Java'ı yapılandırmak, **ağ kaynaklarını yönetmek**, eksik varlıkları özel bir hata işleyicisiyle ele almak, **html'yi png'ye dönüştürmek** ve son olarak **kaynakları temizlemek** için gereken tüm adımları göstereceğiz, böylece uygulamanız sağlıklı kalır. Raporlama motoru, otomatik küçük resim oluşturucu geliştiriyor ya da sadece HTML‑to‑image dönüşümüyle deneme yapıyor olun, burada gösterilen desen zaman ve baş ağrısını tasarruf ettirecek.

## Quick Answers
- **İlk adım nedir?** Ağ‑hostlu resimlere referans veren bir HTML dosyası oluşturun.  
- **Ağ yapılandırmasını hangi sınıf yapar?** `com.aspose.html.Configuration`.  
- **Yükleme hatalarını nasıl yakalarım?** `INetworkService`'e özel bir `MessageHandler` ekleyin.  
- **Bu örnek hangi çıktı formatını üretir?** PNG resmi (`output.png`).  
- **Nesneleri serbest bırakmam gerekiyor mu?** Evet – hem belge hem de yapılandırma için `dispose()` çağırın.

## Prerequisites
- **Java Development Kit (JDK)** 1.8 veya daha yeni bir sürüm.  
- **Aspose.HTML for Java** kütüphanesi – en son sürümü [resmi sürüm sayfasından](https://releases.aspose.com/html/java/) indirin.  
- **IDE** tercihiniz (IntelliJ IDEA, Eclipse, NetBeans, vb.).  
- Java sözdizimi ve Maven/Gradle proje kurulumu konusunda temel bilgi.

## Import Packages
İlk olarak, Java projenize gerekli paketleri içe aktarmanız gerekir. Bu paketler, Aspose.HTML for Java'ın çeşitli işlevlerini kullanmanızı sağlar.

```java
import java.io.IOException;
```

Bu importlar tartışacağımız işlevselliğin temelini oluşturur; bu yüzden Java dosyanızın başında doğru konumlandırıldıklarından emin olun.

## Step 1: Create an HTML File with Network‑Dependent Images
**ağ‑bağımlı resimlere** sahip bir HTML dosyası oluşturmak için, dış kaynaklara işaret eden birkaç `<img>` etiketi ekleyen küçük bir kod parçacığı yazın.

```java
String code = "<img src=\"https://docs.aspose.com/svg/net/drawing-basics/filters-and-gradients/park.jpg\" >\r\n" +
        "<img src=\"https://docs.aspose.com/html/net/missing1.jpg\" >\r\n" +
        "<img src=\"https://docs.aspose.com/html/net/missing2.jpg\" >\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

Bu HTML dosyası ağ servisi için giriş noktasıdır; belge yüklendiğinde resimler HTTP üzerinden alınacaktır.

## Step 2: Initialize the Configuration Object
Şimdi **yapılandırma** nesnemizi oluşturalım; bu nesne ağ‑servisi ayarlarımızı barındıracak.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

`Configuration` nesnesi, Aspose.HTML'ın ağ trafiğini, günlük kaydını ve hata yönetimini nasıl ele alacağını belirlediğiniz yerdir.

## Step 3: Add a Custom Error Message Handler
Özel bir `MessageHandler`, eksik resimler veya zaman aşımı gibi sorunları görmenizi sağlar.

```java
com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
com.aspose.html.net.MessageHandler logHandler = new LogMessageHandler();
network.getMessageHandlers().addItem(logHandler);
```

`LogMessageHandler`'ı ekleyerek, her ağ‑ile ilgili uyarı veya hata yakalanır ve hata ayıklama çok daha basit hale gelir.

## Step 4: Load the HTML Document with the Configuration
Ağ servisi hazır olduğunda, daha önce oluşturduğumuz HTML dosyasını yükleyin.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

Belge yüklendiğinde, Aspose.HTML özel ağ yapılandırmasını kullanacak ve herhangi bir sorun için mesaj işleyicimizi devreye sokacaktır.

## Step 5: Convert HTML to PNG
Şimdi **html'yi png'ye dönüştürelim**, yüklenen sayfayı (başarıyla alınan resimler dahil) raster bir resme çevirerek.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

Sonuç, başka bir yerde gömebileceğiniz veya kullanıcılara sunabileceğiniz tek bir PNG dosyası (`output.png`) olacaktır.

## Step 6: Clean Up Resources
Doğru kaynak yönetimi çok önemlidir. Dönüştürmeden sonra, **kaynakları temizlemek** için nesneleri serbest bırakın ve bellek sızıntılarını önleyin.

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

Bunu bir yemeğin ardından bulaşıkları yıkamak gibi düşünün—kaynakların etrafta kalması ileride performans sorunlarına yol açabilir.

## Common Issues and Solutions
| Sorun | Neden Oluşur | Nasıl Çözülür |
|-------|----------------|------------|
| Resimler yüklenemiyor | Ağ zaman aşımı veya hatalı URL | URL'leri doğrulayın, `NetworkService` ayarlarıyla zaman aşımını artırın veya `LogMessageHandler` içinde yedekleme mantığı ekleyin. |
| PNG boş | Dönüştürmeden önce belge tam olarak yüklenmemiş | `HTMLDocument`'i özel işleyiciyi içeren yapılandırma ile başlatın; isteğe bağlı olarak asenkron yükleme kullanıyorsanız `document.waitForLoad()` çağırın. |
| Bellek yetersiz hatası | Çok büyük HTML veya yüksek çözünürlüklü çok sayıda resim | Çıktı boyutunu sınırlamak için `ImageSaveOptions.setMaxWidth/MaxHeight` kullanın veya ara nesneleri hemen serbest bırakın. |

## Frequently Asked Questions

**S: Aspose.HTML for Java'da bir ağ servisi kurmanın temel amacı nedir?**  
C: Uzaktan resimler, betikler veya stil sayfaları gibi **ağ kaynaklarını yönetmenizi** sağlar ve hata işleme ve günlük kaydı üzerinde kontrol sunar.

**S: Bu kurulumu başka görüntü formatları (ör. JPEG, BMP) üretmek için kullanabilir miyim?**  
C: Evet—`ImageSaveOptions` format özelliğini istediğiniz çıktı türüne değiştirmeniz yeterlidir.

**S: Özel `MessageHandler` varsayılan logger'dan nasıl farklıdır?**  
C: Özel işleyici, mesajları kendi günlükleme çerçevrenize yönlendirmenize, belirli uyarıları filtrelemenize veya uyarılar tetiklemenize olanak tanır; varsayılan logger sadece konsola yazar.

**S: Hem belge hem de yapılandırma için `dispose()` çağırmak gerekli mi?**  
C: Kesinlikle. `dispose()` yerel kaynakları serbest bırakır ve kütüphanenin içinde tuttuğu **kaynakları temizler**.

**S: Java'da HTML'yi resimlere dönüştüren daha fazla örnek nerede bulunabilir?**  
C: Aspose.HTML for Java belgelerine ve resmi GitHub örnekleri sayfasına bakın; PDF dönüşümü, SVG renderleme ve toplu işleme gibi ek kullanım senaryoları mevcuttur.

---

**Last Updated:** 2025-12-05  
**Tested With:** Aspose.HTML for Java 24.12 (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}