---
title: Aspose.HTML ile Bir Belgeyi .NET'e Kaydetmek
linktitle: .NET'te Belge Kaydetme
second_title: Aspose.HTML .NET HTML işleme API'si
description: Adım adım kılavuzumuzla Aspose.HTML for .NET'in gücünün kilidini açın. HTML ve SVG belgelerini oluşturmayı, değiştirmeyi ve dönüştürmeyi öğrenin
type: docs
weight: 16
url: /tr/net/html-document-manipulation/saving-a-document/
---

Günümüzün dijital çağında, HTML ve SVG belgelerini oluşturmak ve değiştirmek birçok yazılım geliştiricisi ve işletme için çok önemlidir. Aspose.HTML for .NET, HTML, SVG ve daha fazlasıyla çalışmak için çeşitli işlevler sunan, bu görevleri basitleştiren güçlü bir kütüphanedir. Bu kapsamlı kılavuzda Aspose.HTML for .NET'in temellerini inceleyeceğiz ve her örneği takip edilmesi kolay adımlara ayıracağız. İster deneyimli bir geliştirici olun ister yeni başlıyor olun, Aspose.HTML'nin yeteneklerinden yararlanmak için bu kılavuzun çok değerli olduğunu göreceksiniz.

## Önkoşullar

Bu yolculuğa çıkmadan önce ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım:

- Geliştirme Ortamı: Bilgisayarınızda Visual Studio'nun veya başka bir .NET geliştirme ortamının kurulu olduğundan emin olun.

- Aspose.HTML for .NET: Aspose.HTML for .NET kitaplığını edinmeniz gerekir. Şuradan indirebilirsiniz[Burada](https://releases.aspose.com/html/net/).

- C# Bilgisi: C# programlama diline aşinalık faydalıdır ancak zorunlu değildir. Bu kılavuz yeni başlayanlar için uygun olacak şekilde tasarlanmıştır.

## Ad Alanını İçe Aktar

Aspose.HTML for .NET'i kullanmaya başlamak için gerekli ad alanlarını projenize aktarmanız gerekir. C# kodunuzda aşağıdaki ad alanını ekleyin:

### Adım 1: Aspose.HTML Ad Alanını İçe Aktarın
```csharp
using Aspose.Html;
```

Bu ad alanı, çeşitli HTML ve SVG işleme yeteneklerine erişmenizi sağlayacaktır.

## HTML'yi Dosyaya Dönüştürmek

### 1. Adım: Boş bir HTML Belgesini Başlatın
```csharp
// Boş bir HTML Belgesini başlatın.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Bir metin öğesi oluşturun ve onu belgeye ekleyin
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // HTML'yi diskteki dosyaya kaydedin.
    document.Save("document.html");
}
```

Bu örnekte bir HTML belgesi oluşturup basit bir "Merhaba Dünya!" ekliyoruz. ona mesaj at. Daha sonra HTML'yi diskteki bir dosyaya kaydediyoruz.

## Bağlantılı Dosya Olmadan HTML

### Adım 1: Basit Bir HTML Dosyası Hazırlayın
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Burada, başka bir dosyaya bağlantı bağlantısı içeren temel bir HTML dosyası oluşturuyoruz.

### Adım 2: 'document.html'yi Belleğe yükleyin
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Kaydetme Seçenekleri örneği oluştur
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //Bağlantılı HTML dosyalarını kesmek için maksimum işleme derinliğini 0'a ayarlayın.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // Belgeyi kaydet
    document.Save(@".\html-to-file-example\document.html", options);
}
```

Bu örnekte, belleğe bir HTML belgesi yüklüyoruz, bağlantılı dosyaları kesmek için maksimum işleme derinliğini ayarlıyoruz ve belgeyi kaydediyoruz. 

## HTML'den MHTML'ye

### Adım 1: Basit Bir HTML Dosyası Hazırlayın
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Örnek 2'deki gibi, başka bir dosyaya bağlantı bağlantısı içeren temel bir HTML dosyası oluşturuyoruz.

### Adım 2: 'document.html'yi Belleğe yükleyin ve MHTML olarak kaydedin
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Belgeyi MHTML olarak kaydedin
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

Burada HTML belgesini belleğe yükleyip MHTML formatında kaydediyoruz.

## HTML'den Markdown'a

### Adım 1: Bir HTML Kodu Hazırlayın
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 Bu adımda, aşağıdakileri içeren bir HTML kod pasajını tanımlarız:`<H2>` eleman.

### Adım 2: Belgeyi HTML Kodundan Başlatın ve Markdown Olarak Kaydedin
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Belgeyi Markdown dosyası olarak kaydedin.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

Kod pasajından bir HTML belgesi oluşturup bunu Markdown dosyası olarak kaydediyoruz.

## Dosyaya SVG

### 1. Adım: Bir SVG Kodu Hazırlayın
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' height='80' width='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

Burada basit, renkli bir grafik çizen bir SVG kodu oluşturuyoruz.

### Adım 2: Koddan bir SVG Belgesini Başlatın ve Diske Kaydedin
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // SVG dosyasını diske kaydedin
    document.Save("document.svg");
}
```

Bu adımda koddan bir SVG belgesi oluşturup bunu SVG dosyası olarak kaydediyoruz.

## Çözüm

Aspose.HTML for .NET, .NET uygulamalarınızda HTML ve SVG belge işlemeyi kolaylaştıran çok yönlü bir kütüphanedir. Bu kılavuzda, her birini adım adım talimatlara ayırarak beş temel örneği ele aldık. Belgeleri oluşturuyor, değiştiriyor veya dönüştürüyorsanız Aspose.HTML yanınızdadır. Bu adımları izleyerek bu güçlü araçta uzmanlaşma yolunda emin adımlarla ilerliyorsunuz.

## SSS'ler

### S1: Aspose.HTML for .NET nedir?

Cevap1: Aspose.HTML for .NET, HTML ve SVG belgeleriyle çalışmak için oluşturma, değiştirme ve dönüştürme de dahil olmak üzere çok çeşitli özellikler sağlayan bir .NET kitaplığıdır.

### S2: Aspose.HTML for .NET'i nereden indirebilirim?

 Cevap2: Aspose.HTML for .NET'i şu adresten indirebilirsiniz:[Burada](https://releases.aspose.com/html/net/).

### S3: Aspose.HTML for .NET yeni başlayanlar için uygun mu?

Cevap3: Evet, Aspose.HTML for .NET hem yeni başlayanlar hem de deneyimli geliştiriciler tarafından kullanılabilir. Bu kılavuzdaki örnekler yeni başlayanlara uygun olacak şekilde tasarlanmıştır.

### S4: Aspose.HTML for .NET'i kullanarak HTML'yi diğer formatlara dönüştürebilir miyim?

Cevap4: Evet, Aspose.HTML for .NET, örneklerde gösterildiği gibi MHTML ve Markdown da dahil olmak üzere çeşitli formatlara dönüştürmeyi destekler.

### S5: Aspose.HTML for .NET desteğini nereden alabilirim?

 Cevap5: Aspose.HTML topluluk forumunda destek ve sorularınızın yanıtlarını bulabilirsiniz.[Burada](https://forum.aspose.com/).