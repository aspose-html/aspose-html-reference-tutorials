---
title: Aspose.HTML ile .NET'te Web Kazıma
linktitle: .NET'te Web Kazıma
second_title: Aspose.HTML .NET HTML işleme API'si
description: Aspose.HTML ile .NET'te HTML belgelerini düzenlemeyi öğrenin. Gelişmiş web geliştirme için öğeleri etkili bir şekilde gezinin, filtreleyin, sorgulayın ve seçin.
weight: 13
url: /tr/net/advanced-features/web-scraping/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML ile .NET'te Web Kazıma


Günümüzün dijital çağında, HTML belgelerinden bilgi işlemek ve çıkarmak geliştiriciler için yaygın bir görevdir. .NET için Aspose.HTML, .NET uygulamalarında HTML işleme ve işlemeyi basitleştiren güçlü bir araçtır. Bu eğitimde, .NET için Aspose.HTML'nin ön koşullar, ad alanları ve tüm potansiyelinden yararlanmanıza yardımcı olacak adım adım örnekler dahil olmak üzere çeşitli yönlerini keşfedeceğiz.

## Ön koşullar

.NET için Aspose.HTML dünyasına dalmadan önce birkaç ön koşula ihtiyacınız olacak:

1. Geliştirme Ortamı: .NET geliştirme için Visual Studio veya uyumlu herhangi bir IDE ile çalışan bir geliştirme ortamı kurduğunuzdan emin olun.

2.  .NET için Aspose.HTML: .NET için Aspose.HTML kitaplığını indirin ve yükleyin.[indirme bağlantısı](https://releases.aspose.com/html/net/)İhtiyaçlarınıza göre ücretsiz deneme sürümü veya lisanslı sürüm arasında seçim yapabilirsiniz.

3. Temel HTML Bilgisi: Aspose.HTML for .NET'i etkili bir şekilde kullanmak için HTML yapısı ve öğelerine aşina olmak önemlidir.

## Ad Alanlarını İçe Aktarma

Başlamak için, C# projenize gerekli ad alanlarını içe aktarmanız gerekir. Bu ad alanları, .NET sınıfları ve işlevleri için Aspose.HTML'ye erişim sağlar:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

Ön koşullar sağlandıktan ve ad alanları içe aktarıldıktan sonra, Aspose.HTML for .NET'in etkili bir şekilde nasıl kullanılacağını göstermek için bazı önemli örnekleri adım adım ele alalım.

## HTML'de Gezinme

Bu örnekte bir HTML belgesinde gezinip, adım adım öğelerine erişeceğiz.

```csharp
public static void NavigateThroughHTML()
{
    // Bir HTML kodu hazırlayın
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    // Hazırlanan koddan bir belge başlatın
    using (var document = new HTMLDocument(html_code, "."))
    {
        // BODY'nin ilk çocuğuna (ilk SPAN) ait referansı alın
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // Çıktı: Merhaba

        // HTML öğeleri arasındaki boşluklara referans alın
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Çıktı: ' '

        // İkinci SPAN öğesinin referansını alın
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Çıktı: Dünya!
    }
}
```

 Bu örnekte bir HTML belgesi oluşturuyoruz, ilk çocuğuna (bir`SPAN` eleman), elemanlar arasındaki boşluk ve ikinci`SPAN` Temel gezinmeyi gösteren öğe.

## Düğüm Filtrelerini Kullanma

Düğüm filtreleri, bir HTML belgesindeki belirli öğeleri seçici bir şekilde işlemenize olanak tanır.

```csharp
public static void NodeFilterUsageExample()
{
    // Bir HTML kodu hazırlayın
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    // Hazırlanan koda dayalı bir belge başlatın
    using (var document = new HTMLDocument(code, "."))
    {
        // Görüntü öğeleri için özel bir filtreye sahip bir TreeWalker oluşturun
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                // Çıktı: image1.png
                // Çıktı: image2.png
            }
        }
    }
}
```

 Bu örnek, belirli öğeleri (bu durumda,`IMG` HTML belgesinden öğeler) silinir.

## XPath Sorguları

XPath sorguları, bir HTML belgesindeki öğeleri belirli ölçütlere göre aramanıza olanak tanır.

```csharp
public static void XPathQueryUsageExample()
{
    // Bir HTML kodu hazırlayın
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello!</span>
            </div>
        </div>
        <p class='happy'>
            <span>World</span>
        </p>
    ";
    
    // Hazırlanan koda dayalı bir belge başlatın
    using (var document = new HTMLDocument(code, "."))
    {
        // Belirli öğeleri seçmek için bir XPath ifadesini değerlendirin
        var result = document.Evaluate("//*[@class='happy']//genişlik",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // Sonuçlanan düğümler üzerinde yineleme yapın
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // Çıktı: Merhaba
            // Çıktı: Dünya!
        }
    }
}
```

Bu örnek, HTML belgesindeki öğeleri niteliklerine ve yapılarına göre bulmak için XPath sorgularının kullanımını göstermektedir.

## CSS Seçicileri

CSS seçicileri, CSS stil sayfalarının öğeleri hedefleme biçimine benzer şekilde, bir HTML belgesindeki öğeleri seçmek için alternatif bir yol sağlar.

```csharp
public static void CSSSelectorUsageExample()
{
    // Bir HTML kodu hazırlayın
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello</span>
            </div>
        </div>
        <p class='happy'>
            <span>World!</span>
        </p>
    ";
    
    // Hazırlanan koda dayalı bir belge başlatın
    using (var document = new HTMLDocument(code, "."))
    {
        //Sınıf ve hiyerarşiye göre öğeleri çıkarmak için bir CSS seçici kullanın
        var elements = document.QuerySelectorAll(".happy span");
        
        // Sonuçlanan elemanlar listesi üzerinde yineleme yapın
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // Çıktı: Merhaba
            // Çıktı: Dünya!
        }
    }
}
```

Burada, HTML belgesindeki belirli öğeleri hedeflemek için CSS seçicilerinin nasıl kullanılacağını gösteriyoruz.

Bu örneklerle, Aspose.HTML for .NET kullanarak HTML belgelerindeki öğelerde gezinme, filtreleme, sorgulama ve seçme konusunda temel bir anlayış kazandınız.

## Çözüm

 .NET için Aspose.HTML, .NET geliştiricilerinin HTML belgeleriyle verimli bir şekilde çalışmasını sağlayan çok yönlü bir kütüphanedir. Gezinme, filtreleme, sorgulama ve öğeleri seçme için güçlü özellikleriyle çeşitli HTML işleme görevlerini sorunsuz bir şekilde halledebilirsiniz. Bu öğreticiyi takip ederek ve şu adresteki belgeleri inceleyerek:[.NET için Aspose.HTML Belgeleri](https://reference.aspose.com/html/net/), .NET uygulamalarınız için bu aracın tüm potansiyelini ortaya çıkarabilirsiniz.

## SSS

### S1. Aspose.HTML for .NET'i kullanmak ücretsiz mi?

A1: Aspose.HTML for .NET ücretsiz deneme sürümü sunar, ancak üretim kullanımı için bir lisans satın almanız gerekir. Lisanslama ayrıntılarını ve seçeneklerini şu adreste bulabilirsiniz:[Aspose.HTML Satın Al](https://purchase.aspose.com/buy).

### S2. Aspose.HTML for .NET için geçici lisansı nasıl alabilirim?

 A2: Test amaçlı geçici lisansı şu adresten alabilirsiniz:[Aspose.HTML Geçici Lisansı](https://purchase.aspose.com/temporary-license/).

### S3. Aspose.HTML for .NET için yardım veya desteği nereden alabilirim?

 A3: Herhangi bir sorunla karşılaşırsanız veya sorularınız varsa, şu adresi ziyaret edebilirsiniz:[Aspose.HTML Forum](https://forum.aspose.com/) yardım ve toplum desteği için.

### S4. .NET için Aspose.HTML öğrenmek için ek kaynaklar var mı?

 A4: Bu eğitimle birlikte, daha fazla eğitim ve belgeyi inceleyebilirsiniz.[Aspose.HTML for .NET dokümantasyon sayfası](https://reference.aspose.com/html/net/).

### S5. Aspose.HTML for .NET en son .NET sürümleriyle uyumlu mudur?

C5: Aspose.HTML for .NET, en son .NET sürümleri ve teknolojileriyle uyumluluğun sağlanması amacıyla düzenli olarak güncellenmektedir.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
