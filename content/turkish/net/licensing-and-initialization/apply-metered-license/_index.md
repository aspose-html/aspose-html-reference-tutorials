---
title: Aspose.HTML ile .NET'te Ölçülü Lisans uygulayın
linktitle: .NET'te Ölçülü Lisans Uygula
second_title: Aspose.HTML .NET HTML işleme API'si
description: Aspose.HTML for .NET'te ölçülü lisansın nasıl uygulanacağını öğrenin. HTML manipülasyon ihtiyaçlarınızı verimli bir şekilde yönetin. Şimdi başla!
type: docs
weight: 10
url: /tr/net/licensing-and-initialization/apply-metered-license/
---
Bu eğitimde, Aspose.HTML'yi kullanarak .NET uygulamanızda ölçülü lisans uygulama süreci boyunca size rehberlik edeceğiz. Ölçülü lisans, HTML işleme ihtiyaçlarınız için lisanslamayı yönetmenin kullanışlı bir yoludur. Aşağıdaki adımları izleyerek Aspose.HTML for .NET projenize ölçülü lisans uygulayabileceksiniz.

## Önkoşullar

Devam etmeden önce aşağıdaki önkoşulların mevcut olduğundan emin olun:

-  Geçerli bir Aspose.HTML for .NET lisansı. adresinden alabilirsiniz[Satın Almayı Düşün](https://purchase.aspose.com/buy).
-  Aspose.HTML for .NET kütüphanesini şu adresten indirebilirsiniz:[Burada](https://releases.aspose.com/html/net/).
- Giriş HTML dosyanızı sakladığınız veri dizini yolunuz.

Şimdi örnek kodu parçalara ayıralım ve her adımı ayrıntılı olarak açıklayalım:

## Ad Alanlarını İçe Aktar

.NET projenizde gerekli ad alanlarını eklemeniz gerekir. C# dosyanızın en üstüne aşağıdaki kullanma ifadelerini ekleyin:

```csharp
using Aspose.Html;
```

## Adım adım rehber

Burada örnek kodu birden çok adıma ayıracağız ve her adımı ayrıntılı olarak açıklayacağız.

### Veri Dizini Yolunu Ayarla:

    Öncelikle, giriş HTML dosyanızın bulunduğu veri dizininizin yolunu ayarlamanız gerekir. Değiştirmeniz gerekecek`"Your Data Directory"` gerçek yol ile.

   ```csharp
   string dataDir = "Your Data Directory";
   ```

### Ölçülen Genel ve Özel Anahtarları Ayarlayın:

    Ölçülü lisans uygulamak için genel ve özel anahtarlarınızı sağlamanız gerekir. Aspose'tan ölçülü lisans satın aldığınızda bu anahtarları alabilirsiniz. Yer değiştirmek`"*****"` gerçek genel ve özel anahtarlarınızla.

   ```csharp
   Aspose.Html.Metered metered = new Aspose.Html.Metered();
   metered.SetMeteredKey("YOUR_PUBLIC_KEY", "YOUR_PRIVATE_KEY");
   ```

### HTML Belgesini yükleyin:

    HTMLDocument sınıfını kullanarak HTML belgesini veri dizininizden yükleyin. Değiştirdiğinizden emin olun`"input.html"` gerçek dosya adıyla.

   ```csharp
   HTMLDocument document = new HTMLDocument(dataDir + "input.html");
   ```

### İç HTML'yi yazdırın:

   HTML belgesini yükledikten sonra doğrulama için dosyanın iç HTML'sine erişebilir ve konsola yazdırabilirsiniz.

   ```csharp
   Console.WriteLine(document.Body.InnerHTML);
   ```

Bu kadar! .NET projenize ölçülü lisansı başarıyla uyguladınız ve bir HTML belgesi yüklediniz.

## Çözüm

Bu eğitimde Aspose.HTML for .NET kullanarak ölçülü lisansın nasıl uygulanacağını gösterdik. Bu adımları izleyerek Aspose.HTML'yi HTML manipülasyonu için .NET uygulamalarınıza sorunsuz bir şekilde entegre edebilirsiniz.

---

## Sıkça Sorulan Sorular (SSS)

### Aspose.HTML for .NET'te ölçülü lisans nedir?
Tarifeli lisans, kullanımınıza bağlı olarak Aspose.HTML için kullandıkça öde esasına göre ödeme yapmanızı sağlar. Esnek bir lisanslama seçeneğidir.

### Aspose.HTML for .NET için ölçülü lisansı nereden edinebilirim?
 Ölçülü lisansı şu adresten satın alabilirsiniz:[Satın Almayı Düşün](https://purchase.aspose.com/buy).

### Aspose.HTML for .NET kütüphanesini nasıl indirebilirim?
 Kütüphaneyi adresinden indirebilirsiniz.[Burada](https://releases.aspose.com/html/net/).

### Aspose.HTML for .NET için ücretsiz deneme seçenekleri mevcut mu?
Evet, ücretsiz deneme sürümüne şuradan erişebilirsiniz:[Burada](https://releases.aspose.com/).

### Aspose.HTML for .NET hakkında nereden destek alabilirim veya soru sorabilirim?
 Topluluğa katılabilir ve destek arayabilirsiniz.[Forumlar](https://forum.aspose.com/).