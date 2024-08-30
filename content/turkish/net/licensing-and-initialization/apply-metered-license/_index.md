---
title: Aspose.HTML ile .NET'te Ölçülü Lisans Uygulayın
linktitle: .NET'te Ölçülü Lisansı Uygula
second_title: Aspose.HTML .NET HTML işleme API'si
description: Aspose.HTML for .NET'te ölçülü bir lisansın nasıl uygulanacağını öğrenin. HTML işleme ihtiyaçlarınızı verimli bir şekilde yönetin. Hemen başlayın!
type: docs
weight: 10
url: /tr/net/licensing-and-initialization/apply-metered-license/
---
Bu eğitimde, Aspose.HTML kullanarak .NET uygulamanızda ölçülü bir lisans uygulama sürecinde size rehberlik edeceğiz. Ölçülü lisans, HTML düzenleme ihtiyaçlarınız için lisanslamayı yönetmenin kullanışlı bir yoludur. Aşağıdaki adımları izleyerek, Aspose.HTML for .NET projenize ölçülü bir lisans uygulayabileceksiniz.

## Ön koşullar

Devam etmeden önce aşağıdaki ön koşulların mevcut olduğundan emin olun:

-  Geçerli bir Aspose.HTML for .NET lisansı. Bunu şuradan edinebilirsiniz:[Aspose Satın Alma](https://purchase.aspose.com/buy).
-  .NET için Aspose.HTML kütüphanesini şu adresten indirebilirsiniz:[Burada](https://releases.aspose.com/html/net/).
- Giriş HTML dosyanızı kaydettiğiniz veri dizin yolunuz.

Şimdi örnek kodu parçalara ayıralım ve her adımı detaylıca açıklayalım:

## Ad Alanlarını İçe Aktar

.NET projenizde gerekli ad alanlarını eklemeniz gerekir. Aşağıdaki using ifadelerini C# dosyanızın en üstüne ekleyin:

```csharp
using Aspose.Html;
```

## Adım Adım Kılavuz

Burada örnek kodu birden fazla adıma böleceğiz ve her adımı ayrıntılı olarak açıklayacağız.

### Veri Dizini Yolunu Ayarla:

   İlk olarak, giriş HTML dosyanızın bulunduğu veri dizininize giden yolu ayarlamalısınız. Bunu değiştirmeniz gerekecektir`"Your Data Directory"` gerçek yol ile.

   ```csharp
   string dataDir = "Your Data Directory";
   ```

### Ölçülü Genel ve Özel Anahtarları Ayarlayın:

    Ölçülü bir lisans uygulamak için, genel ve özel anahtarlarınızı sağlamanız gerekir. Bu anahtarları Aspose'dan ölçülü bir lisans satın aldığınızda edinebilirsiniz. Değiştir`"*****"` gerçek açık ve özel anahtarlarınızla.

   ```csharp
   Aspose.Html.Metered metered = new Aspose.Html.Metered();
   metered.SetMeteredKey("YOUR_PUBLIC_KEY", "YOUR_PRIVATE_KEY");
   ```

### HTML Belgesini Yükle:

    HTMLDocument sınıfını kullanarak HTML belgesini veri dizininizden yükleyin. Değiştirdiğinizden emin olun`"input.html"` gerçek dosya adıyla.

   ```csharp
   HTMLDocument document = new HTMLDocument(dataDir + "input.html");
   ```

### İç HTML'yi yazdır:

   HTML belgesini yükledikten sonra dosyanın iç HTML'ine erişebilir ve doğrulama amacıyla konsola yazdırabilirsiniz.

   ```csharp
   Console.WriteLine(document.Body.InnerHTML);
   ```

İşte bu kadar! .NET projenize ölçülü lisansı başarıyla uyguladınız ve bir HTML belgesi yüklediniz.

## Çözüm

Bu eğitimde, .NET için Aspose.HTML kullanarak ölçülü bir lisansın nasıl uygulanacağını gösterdik. Bu adımları izleyerek, HTML düzenlemesi için Aspose.HTML'yi .NET uygulamalarınıza sorunsuz bir şekilde entegre edebilirsiniz.

---

## Sıkça Sorulan Sorular (SSS)

### Aspose.HTML for .NET'te ölçülü lisans nedir?
Ölçülü lisans, kullanımınıza bağlı olarak Aspose.HTML için ödeme yapmanıza olanak tanır. Esnek bir lisanslama seçeneğidir.

### Aspose.HTML for .NET için ölçülü lisansı nereden alabilirim?
 Ölçülü bir lisansı şu adresten satın alabilirsiniz:[Aspose Satın Alma](https://purchase.aspose.com/buy).

### Aspose.HTML for .NET kütüphanesini nasıl indirebilirim?
 Kütüphaneyi şu adresten indirebilirsiniz:[Burada](https://releases.aspose.com/html/net/).

### Aspose.HTML for .NET için ücretsiz deneme seçenekleri mevcut mu?
 Evet, ücretsiz denemeye şu adresten erişebilirsiniz:[Burada](https://releases.aspose.com/).

### Aspose.HTML for .NET hakkında destek alabilir veya sorularımı nereden sorabilirim?
 Topluluğa katılabilir ve destek arayabilirsiniz[Aspose Forumları](https://forum.aspose.com/).