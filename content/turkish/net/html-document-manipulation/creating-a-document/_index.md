---
title: Aspose.HTML ile .NET'te Belge Oluşturma
linktitle: .NET'te Belge Oluşturma
second_title: Aspose.HTML .NET HTML işleme API'si
description: .NET için Aspose.HTML'nin gücünü açığa çıkarın. HTML ve SVG Belgelerini Kolaylıkla Oluşturmayı, Düzenlemeyi ve Optimize Etmeyi Öğrenin. Adım Adım Örnekleri ve SSS'leri keşfedin.
type: docs
weight: 14
url: /tr/net/html-document-manipulation/creating-a-document/
---

Sürekli gelişen web geliştirme dünyasında, diğerlerinden önde olmak çok önemlidir. Aspose.HTML for .NET, geliştiricilere HTML belgeleriyle çalışmak için güçlü bir araç seti sağlar. İster sıfırdan başlıyor olun, ister bir dosyadan yükleme yapıyor, ister bir URL'den çekiyor veya SVG belgelerini kullanıyor olun, bu kitaplık ihtiyacınız olan çok yönlülüğü sunar.

Bu adım adım kılavuzda, Aspose.HTML for .NET kullanımının temellerini inceleyerek, bu güçlü aracı web geliştirme projelerinizde kullanmak için iyi bir donanıma sahip olmanızı sağlayacağız. Ayrıntılara dalmadan önce yolculuğunuzu başlatmak için önkoşulları ve gerekli ad alanlarını gözden geçirelim.

## Önkoşullar

Bu eğitimi başarıyla takip etmek ve Aspose.HTML for .NET'in gücünden yararlanmak için aşağıdaki önkoşullara ihtiyacınız olacak:

- .NET Framework veya .NET Core yüklü bir Windows makinesi.
- Visual Studio gibi bir kod düzenleyici.
- Temel C# programlama bilgisi.

Artık önkoşullarınızı yerine getirdiğinize göre başlayalım.

## Ad Alanlarını İçe Aktarma

Aspose.HTML for .NET'i kullanmaya başlamadan önce gerekli ad alanlarını içe aktarmanız gerekir. Bu ad alanları, HTML belgeleriyle çalışmak için hayati önem taşıyan sınıfları ve yöntemleri içerir. Aşağıda içe aktarmanız gereken ad alanlarının listesi verilmiştir:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Bu ad alanlarının içe aktarılmasıyla artık adım adım örneklere dalmaya hazırsınız.

## Sıfırdan HTML Belgesi Oluşturma

### 1. Adım: Boş bir HTML Belgesini Başlatın

```csharp
// Boş bir HTML Belgesini başlatın.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Bir metin öğesi oluşturun ve onu belgeye ekleyin
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Belgeyi diske kaydedin.
    document.Save("document.html");
}
```

Bu örnekte boş bir HTML belgesi oluşturup bir "Merhaba Dünya!" ekleyerek başlıyoruz. ona mesaj at. Daha sonra belgeyi bir dosyaya kaydediyoruz.

## Dosyadan HTML Belgesi Oluşturma

### 1. Adım: Bir 'document.html' dosyası hazırlayın

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### 2. Adım: 'document.html' dosyasından yükleyin

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Belge içeriğini çıktı akışına yazın.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Burada "Merhaba Dünya!" başlıklı bir dosya hazırlıyoruz. içeriği oluşturun ve ardından onu bir HTML belgesi olarak yükleyin. Belgenin içeriğini konsola yazdırıyoruz.

## URL'den HTML Belgesi Oluşturma

### 1. Adım: Bir web sayfasından belge yükleyin

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // Belge içeriğini çıktı akışına yazın.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Bu örnekte, bir HTML belgesini doğrudan bir web sayfasından yüklüyoruz ve içeriğini görüntülüyoruz.

## Bir Dizeden HTML Belgesi Oluşturma

### 1. Adım: Bir HTML kodu hazırlayın

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

Burada bir string değişkeninden bir HTML belgesi oluşturup bunu bir dosyaya kaydediyoruz.

## MemoryStream'den HTML Belgesi Oluşturma

### 1. Adım: Bir bellek akışı nesnesi oluşturun

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // HTML Kodunu bellek nesnesine yazın
    sw.Write("<p>Hello World!</p>");
    // Konumu başlangıca ayarla
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

## SVG Belgeleriyle Çalışmak

### 1. Adım: SVG Belgesini bir dizeden başlatın

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // Belge içeriğini çıktı akışına yazın.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Burada bir dizeden bir SVG belgesi oluşturup görüntülüyoruz.

## Bir HTML Belgesini Eşzamansız Olarak Yükleme

### Adım 1: HTML Belgesi örneğini oluşturun

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### 2. Adım: 'ReadyStateChange' etkinliğine abone olun

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    //'ReadyState' özelliğinin değerini kontrol edin.
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

Bu örnekte, bir HTML belgesini eşzamansız olarak yüklüyoruz ve yükleme tamamlandığında içeriği görüntülemek için 'ReadyStateChange' olayını işliyoruz.

## 'Yükte' Olayını Yönetme

### Adım 1: HTML Belgesi örneğini oluşturun

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### 2. Adım: 'Yükte' etkinliğine abone olun

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

Bu örnek, bir HTML belgesinin eşzamansız olarak yüklenmesini ve tamamlandığında içeriğin görüntülenmesi için 'Yüklendiğinde' olayının işlenmesini gösterir.

## Sonuç olarak

Web geliştirmenin dinamik dünyasında, doğru araçların elinizin altında olması çok önemlidir. Aspose.HTML for .NET, sizi HTML ve SVG belgelerini verimli bir şekilde oluşturma, değiştirme ve işleme araçlarıyla donatır. Bu kapsamlı kılavuz, projelerinizde Aspose.HTML for .NET'in gücünden yararlanabilmenizi sağlayacak temel bilgiler konusunda size yol gösterdi.

## SSS'ler

### S1: Aspose.HTML for .NET nedir?

Cevap1: Aspose.HTML for .NET, geliştiricilerin HTML ve SVG belgeleriyle çalışmasına olanak tanıyan güçlü bir .NET kitaplığıdır. Sıfırdan belge oluşturmaktan mevcut HTML ve SVG dosyalarını ayrıştırmaya ve değiştirmeye kadar çok çeşitli özellikler sunar.

### S2: Aspose.HTML for .NET'i .NET Core ile kullanabilir miyim?

C2: Evet, Aspose.HTML for .NET hem .NET Framework hem de .NET Core ile uyumludur, bu da onu modern .NET uygulamaları için çok yönlü bir seçim haline getiriyor.

### S3: Aspose.HTML for .NET web kazıma ve ayrıştırma için uygun mudur?

A3: Kesinlikle! Aspose.HTML for .NET, HTML belgelerini URL'lerden ve dizelerden yükleme yeteneği sayesinde web kazıma ve ayrıştırma görevleri için mükemmel bir seçimdir. Verileri çıkarabilir, analiz gerçekleştirebilir ve daha fazlasını yapabilirsiniz.

### S4: Aspose.HTML for .NET desteğine nasıl erişebilirim?

 Cevap4: Aspose.HTML for .NET'i kullanırken herhangi bir sorunla karşılaşırsanız veya sorularınız olursa şu adresi ziyaret edebilirsiniz:[Aspose Forumu](https://forum.aspose.com/) Topluluktan ve Aspose uzmanlarından destek ve yardım için.

### Cevap5: Ayrıntılı belgeleri ve indirme seçeneklerini nerede bulabilirim?

Cevap5: Kapsamlı belgeler ve indirme seçeneklerine erişim için aşağıdaki bağlantılara başvurabilirsiniz:

- [Dokümantasyon](https://reference.aspose.com/html/net/)
- [İndirmek](https://releases.aspose.com/html/net/)
- [Satın almak](https://purchase.aspose.com/buy)
- [Ücretsiz deneme](https://releases.aspose.com/)
- [Geçici Lisans](https://purchase.aspose.com/temporary-license/)