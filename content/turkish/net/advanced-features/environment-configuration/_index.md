---
title: Aspose.HTML ile .NET'te Ortam Yapılandırması
linktitle: .NET'te Ortam Yapılandırması
second_title: Aspose.HTML .NET HTML işleme API'si
description: Komut dosyası yönetimi, özel stiller, JavaScript yürütme kontrolü ve daha fazlası gibi görevler için Aspose.HTML kullanarak .NET'te HTML belgeleriyle nasıl çalışılacağını öğrenin. Bu kapsamlı eğitim, başlamanıza yardımcı olacak adım adım örnekler ve SSS'ler sağlar.
type: docs
weight: 10
url: /tr/net/advanced-features/environment-configuration/
---

Günümüzün dijital dünyasında HTML belgeleri oluşturmak ve değiştirmek birçok geliştirici için temel bir görevdir. İster bir web uygulaması oluşturuyor olun, ister HTML'yi PDF veya görseller gibi diğer formatlara dönüştürmeniz gerekiyor olsun, Aspose.HTML for .NET, araç setinizde bulunması gereken güçlü bir araçtır. Bu eğitimde, önkoşullar, ad alanlarının içe aktarılması ve ayrıntılı açıklamalarla adım adım örnekler dahil olmak üzere Aspose.HTML for .NET'in çeşitli yönlerini inceleyeceğiz.

## Önkoşullar

Aspose.HTML for .NET'i kullanmaya başlamadan önce aşağıdaki önkoşulların mevcut olduğundan emin olmanız gerekir:

1. Visual Studio: Geliştirme makinenizde Visual Studio'nun kurulu olduğundan emin olun. Aspose.HTML for .NET, Visual Studio ile sorunsuz çalışacak şekilde tasarlanmıştır.

2.  Aspose.HTML for .NET: Aspose.HTML for .NET kütüphanesini web sitesinden indirebilirsiniz. İndirme sayfasına erişmek için aşağıdaki bağlantıyı kullanın:[.NET için Aspose.HTML'yi indirin](https://releases.aspose.com/html/net/).

3. Kurulum ve Lisans: Kütüphaneyi indirdikten sonra dokümantasyonda verilen kurulum talimatlarını takip edin. Gelişmiş özelliklerden bazılarını kullanmak için geçerli bir lisansa da ihtiyacınız olabilir. Aspose web sitesinden lisans alabilirsiniz:[Aspose.HTML Lisansını Satın Alın](https://purchase.aspose.com/buy).

4.  Ücretsiz Deneme: Lisans satın almadan önce Aspose.HTML'yi denemek istiyorsanız bu bağlantıdan ücretsiz deneme sürümünü edinebilirsiniz:[Aspose.HTML Ücretsiz Deneme](https://releases.aspose.com/).

Artık gerekli önkoşullara sahip olduğunuza göre, gerekli ad alanlarını içe aktaracağımız bir sonraki bölüme geçelim.

## Ad Alanlarını İçe Aktar

Aspose.HTML for .NET ile etkili bir şekilde çalışmak için uygun ad alanlarını projenize aktarmanız gerekir. Aşağıda ele alacağımız örnekler için ihtiyaç duyduğunuz ad alanlarını listeleyeceğiz:

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

İçe aktarılan bu ad alanları ile Aspose.HTML for .NET tarafından sağlanan işlevselliğe erişebilirsiniz.

## Komut Dosyalarının Yürütülmesini Devre Dışı Bırak

Bir HTML belgesinde komut dosyası yürütmeyi devre dışı bırakma ve onu PDF'ye dönüştürme konusunda temel bir örnekle başlayalım. Bu adımları takip et:

1. Bir HTML kod pasajı oluşturun ve bunu "document.html" adlı bir dosyaya kaydedin.

```csharp
var code = "<span>Hello World!!</span> " +
           "<script>document.write('Have a nice day!');</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. 'Komut dosyalarını' güvenilmeyen bir kaynak olarak işaretleyerek Aspose.HTML yapılandırmasını başlatın.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    configuration.Security |= Aspose.Html.Sandbox.Scripts;
    
    // Belirtilen yapılandırmayla bir HTML belgesini başlat
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTML'yi PDF'ye dönüştür
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

Bu örnekte, HTML belgesindeki komut dosyalarının yürütülmesini engelleyerek, belgeyi PDF'ye dönüştürürken güvenliği sağladık. Şimdi bir sonraki örneğe geçelim.

## Kullanıcı Stil Sayfasını Belirtin

Bazen bir HTML belgesindeki öğelere özel stiller uygulamak isteyebilirsiniz. Aspose.HTML for .NET'i kullanarak bunu şu şekilde yapabilirsiniz:

1. Bir HTML kod pasajı oluşturun ve bunu "document.html" adlı bir dosyaya kaydedin.

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2.  için özel bir renk ayarlayın.`<span>` Bir kullanıcı stil sayfası kullanan öğe.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var userAgent = configuration.GetService<Aspose.Html.Services.IUserAgentService>();
    userAgent.UserStyleSheet = "span { color: green; }";
    
    // Belirtilen yapılandırmayla bir HTML belgesini başlat
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTML'yi PDF'ye dönüştür
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

 Bu örnekte, özel bir stil uyguladık.`<span>`öğesi, metin rengini yeşil olarak ayarlıyor. Aspose.HTML for .NET, stilleri kolaylıkla değiştirmenize olanak tanır.

## JavaScript Yürütme Zaman Aşımı

Potansiyel olarak zaman alıcı JavaScript koduyla uğraşırken, süresiz yürütmeyi önlemek için bir zaman aşımı ayarlamak önemlidir. Bunu nasıl yapabileceğiniz aşağıda açıklanmıştır:

1. Sonsuz döngüye sahip bir HTML kod pasajı oluşturun ve bunu "document.html" adlı bir dosyaya kaydedin.

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
    
    // Belirtilen yapılandırmayla bir HTML belgesini başlat
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Tüm komut dosyaları bitene/iptal edilene kadar bekleyin ve HTML'yi PNG'ye dönüştürün
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

Bu örnekte, JavaScript yürütme süresini 10 saniyeyle sınırlandırdık, böylece komut dosyasının süresiz olarak çalışmamasını sağladık, bu da performans sorunlarına neden olabilir.

## Özel Mesaj İşleyicisi

Bazen bir HTML belgesini yüklerken hata mesajlarıyla veya eksik kaynaklarla ilgilenmeniz gerekebilir. Özel mesaj işleyicisinin nasıl oluşturulacağına ilişkin bir örnek:

1. Eksik resim dosyası referansına sahip bir HTML kod pasajı oluşturun ve bunu "document.html" adlı bir dosyaya kaydedin.

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
    
    // Belirtilen yapılandırmayla bir HTML belgesini başlat
    // Belge yükleme sırasında uygulama görseli yüklemeye çalışacak ve bu işlemin sonucunu konsolda göreceğiz.
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // HTML'yi PNG'ye dönüştür
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

Bu örnekte özel bir mesaj işleyicisi ekledik (`LogMessageHandler`) başarısız isteklerle ilgili bilgileri günlüğe kaydetmek için. Bu, özellikle eksik kaynakların düzgün bir şekilde ayıklanması ve işlenmesi için yararlı olabilir.

## Çözüm

Aspose.HTML for .NET, geliştiricilerin HTML belgeleriyle verimli bir şekilde çalışmasını sağlayan çok yönlü bir kitaplıktır. Bu eğitimde temel kavramları ele aldık ve komut dosyası yönetimi, stil sayfası özelleştirme, JavaScript yürütme kontrolü ve özel mesaj işleme dahil olmak üzere ortak görevler için adım adım örnekler sunduk.

Bu eğitimde özetlenen adımları takip ederek, Aspose.HTML for .NET'in gücünden yararlanarak .NET uygulamalarınızda HTML belgelerini güvenle oluşturabilir, yönetebilir ve dönüştürebilirsiniz.

## SSS'ler

### S1: Aspose.HTML for .NET'i lisans satın almadan kullanabilir miyim?

Cevap1: Evet, Aspose.HTML for .NET'i ücretsiz deneme sürümüyle deneyebilirsiniz, ancak bazı gelişmiş özellikler geçerli bir lisans gerektirebilir.

### S2: Aspose.HTML for .NET lisansını nasıl edinebilirim?

 Cevap2: Aspose web sitesinden lisans satın alabilirsiniz:[Aspose.HTML Lisansını Satın Alın](https://purchase.aspose.com/buy).

### S3: Aspose.HTML for .NET kullanarak HTML belgelerini hangi formatlara dönüştürebilirim?

Cevap3: Aspose.HTML for .NET, PDF, görseller ve daha fazlası dahil olmak üzere çeşitli formatlara dönüştürmeyi destekler.

### S4: Aspose.HTML for .NET için bir topluluk veya destek forumu var mı?

 C4: Evet, Aspose forumlarında yardım ve destek bulabilirsiniz:[Aspose.HTML Destek Forumu](https://forum.aspose.com/).

### S5: Aspose.HTML for .NET dokümantasyon ve eğitimler sağlıyor mu?

 C5: Evet, belgelere buradan ulaşabilirsiniz:[Aspose.HTML for .NET Belgeleri](https://reference.aspose.com/html/net/).