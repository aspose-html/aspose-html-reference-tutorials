---
title: Aspose.HTML ile .NET'te Ortam Yapılandırması
linktitle: .NET'te Ortam Yapılandırması
second_title: Aspose.HTML .NET HTML işleme API'si
description: Komut dosyası yönetimi, özel stiller, JavaScript yürütme denetimi ve daha fazlası gibi görevler için Aspose.HTML kullanarak .NET'te HTML belgeleriyle nasıl çalışacağınızı öğrenin. Bu kapsamlı eğitim, başlamanız için adım adım örnekler ve SSS sağlar.
type: docs
weight: 10
url: /tr/net/advanced-features/environment-configuration/
---

Günümüzün dijital dünyasında, HTML belgeleri oluşturmak ve düzenlemek birçok geliştirici için temel bir görevdir. İster bir web uygulaması oluşturuyor olun, ister HTML'yi PDF veya resim gibi diğer biçimlere dönüştürmeniz gereksin, .NET için Aspose.HTML araç setinizde bulundurmanız gereken güçlü bir araçtır. Bu eğitimde, ön koşullar, ad alanlarını içe aktarma ve ayrıntılı açıklamalarla adım adım örnekler dahil olmak üzere .NET için Aspose.HTML'nin çeşitli yönlerini keşfedeceğiz.

## Ön koşullar

Aspose.HTML'i .NET için kullanmaya başlamadan önce, aşağıdaki ön koşulların mevcut olduğundan emin olmanız gerekir:

1. Visual Studio: Geliştirme makinenizde Visual Studio'nun yüklü olduğundan emin olun. Aspose.HTML for .NET, Visual Studio ile sorunsuz bir şekilde çalışmak üzere tasarlanmıştır.

2.  Aspose.HTML for .NET: Aspose.HTML for .NET kütüphanesini web sitesinden indirebilirsiniz. İndirme sayfasına erişmek için aşağıdaki bağlantıyı kullanın:[.NET için Aspose.HTML'yi indirin](https://releases.aspose.com/html/net/).

3.  Kurulum ve Lisans: Kütüphaneyi indirdikten sonra, belgelerde verilen kurulum talimatlarını izleyin. Ayrıca, gelişmiş özelliklerden bazılarını kullanmak için geçerli bir lisansa ihtiyacınız olabilir. Lisansı Aspose web sitesinden edinebilirsiniz:[Aspose.HTML Lisansı Satın Alın](https://purchase.aspose.com/buy).

4.  Ücretsiz Deneme: Lisans satın almadan önce Aspose.HTML'yi denemek istiyorsanız, bu bağlantıdan ücretsiz deneme sürümünü edinebilirsiniz:[Aspose.HTML Ücretsiz Deneme](https://releases.aspose.com/).

Artık gerekli ön koşullara sahip olduğumuza göre, gerekli ad alanlarını içe aktaracağımız bir sonraki bölüme geçelim.

## Ad Alanlarını İçe Aktar

.NET için Aspose.HTML ile etkili bir şekilde çalışmak için, projenize uygun ad alanlarını içe aktarmanız gerekir. Aşağıda, ele alacağımız örnekler için ihtiyaç duyduğunuz ad alanlarını listeleyeceğiz:

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

Bu ad alanlarını içe aktararak, Aspose.HTML for .NET tarafından sağlanan işlevselliğe erişebilirsiniz.

## Komut Dosyası Çalıştırmasını Devre Dışı Bırak

Bir HTML belgesindeki betik yürütmeyi devre dışı bırakıp bunu PDF'e dönüştürmenin temel bir örneğiyle başlayalım. Şu adımları izleyin:

1. Bir HTML kod parçacığı oluşturun ve bunu "document.html" adlı bir dosyaya kaydedin.

```csharp
var code = "<span>Hello World!!</span> " +
           "<script>document.write('Have a nice day!');</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Aspose.HTML yapılandırmasını başlatın ve 'scripts'i güvenilmeyen kaynak olarak işaretleyin.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    configuration.Security |= Aspose.Html.Sandbox.Scripts;
    
    // Belirtilen yapılandırmayla bir HTML belgesi başlatın
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTML'yi PDF'ye dönüştür
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

Bu örnekte, HTML belgesi içindeki betiklerin yürütülmesini önledik ve PDF'ye dönüştürülürken güvenliği sağladık. Şimdi bir sonraki örneğe geçelim.

## Kullanıcı Stil Sayfasını Belirle

Bazen, bir HTML belgesindeki öğelere özel stiller uygulamak isteyebilirsiniz. İşte bunu .NET için Aspose.HTML kullanarak nasıl yapabileceğiniz:

1. Bir HTML kod parçacığı oluşturun ve bunu "document.html" adlı bir dosyaya kaydedin.

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2.  İçin özel bir renk ayarlayın`<span>` Kullanıcı stil sayfasını kullanan öğe.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var userAgent = configuration.GetService<Aspose.Html.Services.IUserAgentService>();
    userAgent.UserStyleSheet = "span { color: green; }";
    
    // Belirtilen yapılandırmayla bir HTML belgesi başlatın
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTML'yi PDF'ye dönüştür
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

 Bu örnekte, özel bir stil uyguladık`<span>` öğesini, metin rengini yeşil olarak ayarlayarak. Aspose.HTML for .NET, stilleri kolaylıkla düzenlemenize olanak tanır.

## JavaScript Yürütme Zaman Aşımı

Potansiyel olarak zaman alıcı JavaScript koduyla uğraşırken, belirsiz yürütmeyi önlemek için bir zaman aşımı ayarlamak önemlidir. Bunu nasıl yapabileceğiniz aşağıda açıklanmıştır:

1. Sonsuz döngü içeren bir HTML kod parçacığı oluşturun ve bunu "document.html" adlı bir dosyaya kaydedin.

```csharp
var code = @"<script>while(true){}</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. JavaScript yürütme zaman aşımını 10 saniyeye ayarlayın.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var runtime = configuration.GetService<Aspose.Html.Services.IRuntimeService>();
    runtime.JavaScriptTimeout = TimeSpan.FromSeconds(10);
    
    // Belirtilen yapılandırmayla bir HTML belgesi başlatın
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Tüm betikler bitene/iptal edilene kadar bekleyin ve HTML'yi PNG'ye dönüştürün
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

Bu örnekte, JavaScript yürütme süresini 10 saniyeyle sınırladık; böylece betiğin süresiz olarak çalışmasını ve bunun da performans sorunlarına yol açmasını önledik.

## Özel Mesaj İşleyicisi

Bazen, bir HTML belgesini yüklerken hata mesajlarını veya eksik kaynakları işlemeniz gerekebilir. İşte özel bir mesaj işleyicisinin nasıl oluşturulacağına dair bir örnek:

1. Eksik resim dosyası referansını içeren bir HTML kod parçacığı oluşturun ve bunu "document.html" adlı bir dosyaya kaydedin.

```csharp
var code = @"<img src='missing.jpg'>";
System.IO.File.WriteAllText("document.html", code);
```

2. Başarısız istekleri günlüğe kaydetmek için ağ hizmetine bir hata mesajı işleyicisi ekleyin.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var network = configuration.GetService<Aspose.Html.Services.INetworkService>();
    network.MessageHandlers.Add(new LogMessageHandler());
    
    // Belirtilen yapılandırmayla bir HTML belgesi başlatın
    // Belge yükleme sırasında uygulama resmi yüklemeye çalışacak ve bu işlemin sonucunu konsolda göreceğiz.
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTML'yi PNG'ye dönüştür
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

Bu örnekte, özel bir mesaj işleyicisi ekledik (`LogMessageHandler`) başarısız istekler hakkında bilgi kaydetmek için. Bu özellikle hata ayıklama ve eksik kaynakları zarif bir şekilde işlemek için yararlı olabilir.

## Çözüm

.NET için Aspose.HTML, geliştiricilerin HTML belgeleriyle verimli bir şekilde çalışmasını sağlayan çok yönlü bir kütüphanedir. Bu eğitimde, temel kavramları ele aldık ve betik yönetimi, stil sayfası özelleştirmesi, JavaScript yürütme denetimi ve özel mesaj işleme gibi yaygın görevler için adım adım örnekler sağladık.

Bu eğitimde özetlenen adımları izleyerek, .NET uygulamalarınızda HTML belgelerini güvenle oluşturmak, düzenlemek ve dönüştürmek için Aspose.HTML for .NET'in gücünden yararlanabilirsiniz.

## SSS

### S1: Lisans satın almadan Aspose.HTML for .NET'i kullanabilir miyim?

C1: Evet, Aspose.HTML for .NET'i ücretsiz deneme sürümüyle deneyebilirsiniz, ancak bazı gelişmiş özellikler geçerli bir lisans gerektirebilir.

### S2: Aspose.HTML for .NET için lisansı nasıl alabilirim?

 A2: Lisansınızı Aspose web sitesinden satın alabilirsiniz:[Aspose.HTML Lisansı Satın Alın](https://purchase.aspose.com/buy).

### S3: Aspose.HTML for .NET kullanarak HTML belgelerini hangi formatlara dönüştürebilirim?

C3: Aspose.HTML for .NET, PDF, resim ve daha fazlası dahil olmak üzere çeşitli biçimlere dönüştürmeyi destekler.

### S4: Aspose.HTML for .NET için bir topluluk veya destek forumu var mı?

 C4: Evet, Aspose forumlarında yardım ve destek bulabilirsiniz:[Aspose.HTML Destek Forumu](https://forum.aspose.com/).

### S5: Aspose.HTML for .NET dokümantasyon ve eğitimler sağlıyor mu?

 C5: Evet, dokümanlara buradan ulaşabilirsiniz:[.NET için Aspose.HTML Belgeleri](https://reference.aspose.com/html/net/).