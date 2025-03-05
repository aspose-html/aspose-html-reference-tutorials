---
title: Aspose.HTML ile .NET'te Bir Belgeyi Kaydetme
linktitle: .NET'te Bir Belgeyi Kaydetme
second_title: Aspose.HTML .NET HTML işleme API'si
description: Adım adım kılavuzumuzla .NET için Aspose.HTML'nin gücünü açığa çıkarın. HTML ve SVG belgeleri oluşturmayı, düzenlemeyi ve dönüştürmeyi öğrenin
type: docs
weight: 16
url: /tr/net/html-document-manipulation/saving-a-document/
---

Günümüzün dijital çağında, HTML ve SVG belgeleri oluşturmak ve düzenlemek birçok yazılım geliştiricisi ve işletmesi için olmazsa olmazdır. Aspose.HTML for .NET, bu görevleri basitleştiren, HTML, SVG ve daha fazlasıyla çalışmak için çeşitli işlevler sunan güçlü bir kütüphanedir. Bu kapsamlı kılavuzda, Aspose.HTML for .NET'in temellerine dalacağız ve her örneği kolayca takip edilebilen adımlara ayıracağız. İster deneyimli bir geliştirici olun, ister yeni başlıyor olun, bu kılavuzu Aspose.HTML'in yeteneklerinden yararlanmak için paha biçilmez bulacaksınız.

## Ön koşullar

Bu yolculuğa çıkmadan önce ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım:

- Geliştirme Ortamı: Bilgisayarınızda Visual Studio veya başka bir .NET geliştirme ortamının yüklü olduğundan emin olun.

- .NET için Aspose.HTML: .NET için Aspose.HTML kütüphanesini edinmeniz gerekir. Bunu şuradan indirebilirsiniz:[Burada](https://releases.aspose.com/html/net/).

- C# Bilgisi: C# programlama diline aşinalık faydalıdır ancak zorunlu değildir. Bu kılavuz yeni başlayanlar için uygundur.

## Ad Alanını İçe Aktar

.NET için Aspose.HTML kullanmaya başlamak için, gerekli ad alanlarını projenize aktarmanız gerekir. C# kodunuzda, aşağıdaki ad alanını ekleyin:

### Adım 1: Aspose.HTML Ad Alanını İçe Aktar
```csharp
using Aspose.Html;
```

Bu ad alanı size çeşitli HTML ve SVG düzenleme yeteneklerine erişim imkanı verecektir.

## HTML'den Dosyaya

### Adım 1: Boş bir HTML Belgesi Başlatın
```csharp
// Boş bir HTML Belgesi başlatın.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Bir metin öğesi oluşturun ve bunu belgeye ekleyin
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // HTML'yi diskteki dosyaya kaydedin.
    document.Save("document.html");
}
```

Bu örnekte, bir HTML belgesi oluşturuyoruz ve ona basit bir "Hello World!" metni ekliyoruz. Daha sonra HTML'yi diskteki bir dosyaya kaydediyoruz.

## Bağlantılı Dosya Olmadan HTML

### Adım 1: Basit bir HTML Dosyası Hazırlayın
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Burada, başka bir dosyaya bağlantı veren basit bir HTML dosyası oluşturuyoruz.

### Adım 2: 'document.html'yi Belleğe Yükleyin
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Kaydetme Seçenekleri örneğini oluştur
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //Bağlantılı HTML dosyalarını kesmek için maksimum işleme derinliğini 0 olarak ayarlayın.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // Belgeyi kaydet
    document.Save(@".\html-to-file-example\document.html", options);
}
```

Bu örnekte, bir HTML belgesini belleğe yüklüyoruz, bağlantılı dosyaları kesmek için maksimum işleme derinliğini ayarlıyoruz ve belgeyi kaydediyoruz. 

## HTML'den MHTML'e

### Adım 1: Basit bir HTML Dosyası Hazırlayın
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Örnek 2'deki gibi, başka bir dosyaya bağlantı veren basit bir HTML dosyası oluşturuyoruz.

### Adım 2: 'document.html' dosyasını Belleğe yükleyin ve MHTML olarak kaydedin
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Belgeyi MHTML olarak kaydedin
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

Burada HTML dokümanını belleğe yükleyip MHTML formatında kaydediyoruz.

## HTML'den Markdown'a

### Adım 1: Bir HTML Kodu Hazırlayın
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 Bu adımda, bir HTML kod parçacığı tanımlıyoruz.`<H2>` öğe.

### Adım 2: Belgeyi HTML Kodundan Başlatın ve Markdown Olarak Kaydedin
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Belgeyi Markdown dosyası olarak kaydedin.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

Kod parçacığından bir HTML belgesi oluşturup bunu Markdown dosyası olarak kaydediyoruz.

## SVG'yi Dosyaya Dönüştür

### Adım 1: Bir SVG Kodu Hazırlayın
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' yükseklik='80' genişlik='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

Burada basit ve renkli bir grafik çizen bir SVG kodu oluşturuyoruz.

### Adım 2: Koddan bir SVG Belgesi Başlatın ve Diske Kaydedin
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // SVG dosyasını diske kaydedin
    document.Save("document.svg");
}
```

Bu adımda koddan bir SVG belgesi oluşturup bunu SVG dosyası olarak kaydediyoruz.

## Çözüm

.NET için Aspose.HTML, .NET uygulamalarınızda HTML ve SVG belge işlemeyi basitleştiren çok yönlü bir kütüphanedir. Bu kılavuzda, her birini adım adım talimatlara ayırarak beş temel örneği ele aldık. Belgeleri oluşturuyor, işliyor veya dönüştürüyor olun, Aspose.HTML sizi korur. Bu adımları izleyerek, bu güçlü aracı ustalıkla kullanma yolunda iyi bir mesafe kat etmiş olursunuz.

## SSS

### S1: .NET için Aspose.HTML nedir?

A1: Aspose.HTML for .NET, HTML ve SVG belgeleriyle çalışmak için oluşturma, düzenleme ve dönüştürme dahil olmak üzere çok çeşitli özellikler sağlayan bir .NET kütüphanesidir.

### S2: Aspose.HTML for .NET'i nereden indirebilirim?

 A2: .NET için Aspose.HTML'yi şu adresten indirebilirsiniz:[Burada](https://releases.aspose.com/html/net/).

### S3: Aspose.HTML for .NET yeni başlayanlar için uygun mudur?

C3: Evet, Aspose.HTML for .NET hem yeni başlayanlar hem de deneyimli geliştiriciler tarafından kullanılabilir. Bu kılavuzdaki örnekler yeni başlayanlar için uygun olacak şekilde tasarlanmıştır.

### S4: Aspose.HTML for .NET kullanarak HTML'yi diğer formatlara dönüştürebilir miyim?

C4: Evet, Aspose.HTML for .NET, örneklerde gösterildiği gibi MHTML ve Markdown dahil olmak üzere çeşitli biçimlere dönüştürmeyi destekler.

### S5: Aspose.HTML for .NET için desteği nereden alabilirim?

 A5: Aspose.HTML topluluk forumunda destek ve sorularınızın yanıtlarını bulabilirsiniz[Burada](https://forum.aspose.com/).