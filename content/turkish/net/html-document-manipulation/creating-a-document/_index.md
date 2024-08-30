---
title: Aspose.HTML ile .NET'te Belge Oluşturma
linktitle: .NET'te Belge Oluşturma
second_title: Aspose.HTML .NET HTML işleme API'si
description: .NET için Aspose.HTML'nin Gücünü Serbest Bırakın. HTML ve SVG Belgelerini Kolayca Oluşturmayı, Düzenlemeyi ve Optimize Etmeyi Öğrenin. Adım Adım Örnekleri ve SSS'leri keşfedin.
type: docs
weight: 14
url: /tr/net/html-document-manipulation/creating-a-document/
---

Sürekli gelişen web geliştirme dünyasında, eğrinin önünde kalmak esastır. Aspose.HTML for .NET, geliştiricilere HTML belgeleriyle çalışmak için sağlam bir araç takımı sağlar. Sıfırdan başlıyor, bir dosyadan yüklüyor, bir URL'den çekiyor veya SVG belgeleriyle uğraşıyor olun, bu kitaplık ihtiyacınız olan çok yönlülüğü sunar.

Bu adım adım kılavuzda, .NET için Aspose.HTML'i kullanmanın temellerine inerek, web geliştirme projelerinizde bu güçlü aracı kullanmak için iyi donanımlı olduğunuzdan emin olacağız. Ayrıntılara dalmadan önce, yolculuğunuza başlamak için ön koşulları ve gerekli ad alanlarını gözden geçirelim.

## Ön koşullar

Bu eğitimi başarıyla takip etmek ve .NET için Aspose.HTML'nin gücünden yararlanmak için aşağıdaki ön koşullara ihtiyacınız olacak:

- .NET Framework veya .NET Core yüklü bir Windows bilgisayarı.
- Visual Studio benzeri bir kod editörü.
- C# programlamanın temel bilgisi.

Artık ön koşullarınızı tamamladığınıza göre, başlayalım.

## Ad Alanlarını İçe Aktarma

.NET için Aspose.HTML kullanmaya başlamadan önce, gerekli ad alanlarını içe aktarmanız gerekir. Bu ad alanları, HTML belgeleriyle çalışmak için hayati önem taşıyan sınıflar ve yöntemler içerir. Aşağıda içe aktarmanız gereken ad alanlarının bir listesi bulunmaktadır:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Bu ad alanlarını içe aktardıktan sonra artık adım adım örneklere dalmaya hazırsınız.

## Sıfırdan Bir HTML Belgesi Oluşturma

### Adım 1: Boş bir HTML Belgesi Başlatın

```csharp
// Boş bir HTML Belgesi başlatın.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Bir metin öğesi oluşturun ve bunu belgeye ekleyin
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Belgeyi diske kaydedin.
    document.Save("document.html");
}
```

Bu örnekte, boş bir HTML belgesi oluşturarak ve ona bir "Hello World!" metni ekleyerek başlıyoruz. Daha sonra belgeyi bir dosyaya kaydediyoruz.

## Bir Dosyadan HTML Belgesi Oluşturma

### Adım 1: Bir 'document.html' dosyası hazırlayın

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### Adım 2: 'document.html' dosyasından yükleyin

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Belge içeriğini çıktı akışına yaz.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Burada, "Hello World!" içeriğine sahip bir dosya hazırlıyoruz ve ardından bunu bir HTML belgesi olarak yüklüyoruz. Belgenin içeriğini konsola yazdırıyoruz.

## URL'den HTML Belgesi Oluşturma

### Adım 1: Bir web sayfasından bir belge yükleyin

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // Belge içeriğini çıktı akışına yaz.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Bu örnekte bir HTML belgesini doğrudan bir web sayfasından yükleyip içeriğini görüntülüyoruz.

## Bir Dizeden HTML Belgesi Oluşturma

### Adım 1: Bir HTML kodu hazırlayın

```csharp
var html_code = "<p>Hello World!</p>";
```

### Adım 2: Belgeyi dize değişkeninden başlatın

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Belgeyi diske kaydedin.
    document.Save("document.html");
}
```

Burada bir dize değişkeninden bir HTML belgesi oluşturup bunu bir dosyaya kaydediyoruz.

## MemoryStream'den bir HTML Belgesi Oluşturma

### Adım 1: Bir bellek akışı nesnesi oluşturun

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // HTML Kodunu bellek nesnesine yazın
    sw.Write("<p>Hello World!</p>");
    // Pozisyonu başlangıca ayarlayın
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // Belgeyi bellek akışından başlat
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // Belgeyi diske kaydedin.
        document.Save("document.html");
    }
}
```

Bu örnekte, bir bellek akışından bir HTML belgesi oluşturup bunu bir dosyaya kaydediyoruz.

## SVG Belgeleriyle Çalışma

### Adım 1: SVG Belgesini bir dizeden başlatın

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><daire cx='50' cy='50' r='40'/></svg>", "."))
{
    // Belge içeriğini çıktı akışına yaz.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Burada bir dizgeden bir SVG belgesi oluşturup görüntülüyoruz.

## Bir HTML Belgesini Eşzamansız Olarak Yükleme

### Adım 1: HTML Belgesi örneğini oluşturun

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Adım 2: 'ReadyStateChange' etkinliğine abone olun

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    // 'ReadyState' özelliğinin değerini kontrol edin.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Adım 3: Belirtilen Uri'de eşzamansız olarak gezinin

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Bu örnekte, bir HTML belgesini eş zamanlı olarak yüklüyoruz ve yükleme tamamlandığında içeriği görüntülemek için 'ReadyStateChange' olayını işliyoruz.

## 'OnLoad' Olayının İşlenmesi

### Adım 1: HTML Belgesi örneğini oluşturun

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Adım 2: 'OnLoad' etkinliğine abone olun

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### Adım 3: Belirtilen Uri'de eşzamansız olarak gezinin

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Bu örnek, bir HTML belgesinin eş zamanlı olarak yüklenmesini ve tamamlandığında içeriği görüntülemek için 'OnLoad' olayının işlenmesini göstermektedir.

## Sonuç olarak

Dinamik web geliştirme dünyasında, emrinizde doğru araçlara sahip olmak çok önemlidir. Aspose.HTML for .NET, HTML ve SVG belgelerini verimli bir şekilde oluşturmanız, düzenlemeniz ve işlemeniz için gereken araçları sağlar. Bu kapsamlı kılavuz, projelerinizde Aspose.HTML for .NET'in gücünden yararlanabilmenizi sağlayarak sizi temel konularda yönlendirmiştir.

## SSS

### S1: .NET için Aspose.HTML nedir?

A1: Aspose.HTML for .NET, geliştiricilerin HTML ve SVG belgeleriyle çalışmasını sağlayan güçlü bir .NET kütüphanesidir. Sıfırdan belge oluşturmaktan mevcut HTML ve SVG dosyalarını ayrıştırmaya ve düzenlemeye kadar çok çeşitli özellikler sunar.

### S2: .NET Core ile Aspose.HTML for .NET'i kullanabilir miyim?

C2: Evet, Aspose.HTML for .NET hem .NET Framework hem de .NET Core ile uyumludur ve bu da onu modern .NET uygulamaları için çok yönlü bir seçenek haline getirir.

### S3: Aspose.HTML for .NET web kazıma ve ayrıştırma için uygun mudur?

C3: Kesinlikle! Aspose.HTML for .NET, URL'lerden ve dizelerden HTML belgeleri yükleme yeteneği sayesinde web kazıma ve ayrıştırma görevleri için mükemmel bir seçimdir. Veri çıkarabilir, analiz gerçekleştirebilir ve daha fazlasını yapabilirsiniz.

### S4: Aspose.HTML for .NET desteğine nasıl erişebilirim?

 A4: Aspose.HTML for .NET kullanırken herhangi bir sorunla karşılaşırsanız veya sorularınız varsa, şu adresi ziyaret edebilirsiniz:[Aspose Forum](https://forum.aspose.com/) Topluluktan ve Aspose uzmanlarından destek ve yardım için.

### C5: Ayrıntılı dokümantasyonu ve indirme seçeneklerini nerede bulabilirim?

C5: Kapsamlı dokümantasyon ve indirme seçeneklerine erişim için aşağıdaki bağlantılara başvurabilirsiniz:

- [Belgeleme](https://reference.aspose.com/html/net/)
- [İndirmek](https://releases.aspose.com/html/net/)
- [Satın almak](https://purchase.aspose.com/buy)
- [Ücretsiz Deneme](https://releases.aspose.com/)
- [Geçici Lisans](https://purchase.aspose.com/temporary-license/)