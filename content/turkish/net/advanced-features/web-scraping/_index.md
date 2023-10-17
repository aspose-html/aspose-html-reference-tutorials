---
title: Aspose.HTML ile .NET'te Web Scraping
linktitle: .NET'te Web Kazıma
second_title: Aspose.HTML .NET HTML işleme API'si
description: Aspose.HTML ile .NET'te HTML belgelerini yönetmeyi öğrenin. Gelişmiş web geliştirme için öğeleri etkili bir şekilde gezinin, filtreleyin, sorgulayın ve seçin.
type: docs
weight: 13
url: /tr/net/advanced-features/web-scraping/
---

Günümüzün dijital çağında, HTML belgelerinden bilgi çıkarmak ve değiştirmek geliştiricilerin ortak bir görevidir. Aspose.HTML for .NET, .NET uygulamalarında HTML işlemeyi ve değiştirmeyi kolaylaştıran güçlü bir araçtır. Bu eğitimde Aspose.HTML for .NET'in önkoşullar, ad alanları ve tüm potansiyelinden yararlanmanıza yardımcı olacak adım adım örnekler de dahil olmak üzere çeşitli yönlerini inceleyeceğiz.

## Önkoşullar

Aspose.HTML for .NET dünyasına dalmadan önce birkaç ön koşula ihtiyacınız olacak:

1. Geliştirme Ortamı: Visual Studio veya herhangi bir uyumlu .NET geliştirme için IDE ile ayarlanmış, çalışan bir geliştirme ortamına sahip olduğunuzdan emin olun.

2.  Aspose.HTML for .NET: Aspose.HTML for .NET kitaplığını aşağıdaki adresten indirip yükleyin:[İndirme: {link](https://releases.aspose.com/html/net/). İhtiyaçlarınıza göre ücretsiz deneme sürümü veya lisanslı sürüm arasında seçim yapabilirsiniz.

3. Temel HTML Bilgisi: Aspose.HTML for .NET'i etkili bir şekilde kullanmak için HTML yapısına ve öğelerine aşina olmak çok önemlidir.

## Ad Alanlarını İçe Aktarma

Başlamak için gerekli ad alanlarını C# projenize aktarmanız gerekir. Bu ad alanları Aspose.HTML for .NET sınıflarına ve işlevlerine erişim sağlar:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

Önkoşullar mevcut ve ad alanları içe aktarıldıktan sonra, Aspose.HTML for .NET'in etkili bir şekilde nasıl kullanılacağını göstermek için bazı önemli örnekleri adım adım inceleyelim.

## HTML'de Gezinmek

Bu örnekte, bir HTML belgesinde gezineceğiz ve öğelerine adım adım erişeceğiz.

```csharp
public static void NavigateThroughHTML()
{
    // Bir HTML kodu hazırlayın
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    // Hazırlanan koddan bir belgeyi başlat
    using (var document = new HTMLDocument(html_code, "."))
    {
        // BODY'nin ilk çocuğuna (ilk SPAN) referansı alın
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // Çıktı: Merhaba

        //HTML öğeleri arasındaki boşluklara referans alın
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Çıktı: ' '

        // İkinci SPAN öğesinin referansını alın
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Çıktı: Dünya!
    }
}
```

 Bu örnekte, bir HTML belgesi oluşturuyoruz, onun ilk çocuğuna (a) erişiyoruz.`SPAN` eleman), elemanlar arasındaki boşluk ve ikinci`SPAN` temel gezinmeyi gösteren öğe.

## Düğüm Filtrelerini Kullanma

Düğüm filtreleri, bir HTML belgesindeki belirli öğeleri seçerek işlemenize olanak tanır.

```csharp
public static void NodeFilterUsageExample()
{
    // Bir HTML kodu hazırlayın
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    // Hazırlanan koda göre bir belgeyi başlatın
    using (var document = new HTMLDocument(code, "."))
    {
        // Görüntü öğeleri için özel filtreli bir TreeWalker oluşturun
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

 Bu örnek, belirli öğeleri ayıklamak için özel bir düğüm filtresinin nasıl kullanılacağını gösterir (bu durumda,`IMG` öğeleri) HTML belgesinden.

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
    
    // Hazırlanan koda göre bir belgeyi başlatın
    using (var document = new HTMLDocument(code, "."))
    {
        // Belirli öğeleri seçmek için bir XPath ifadesini değerlendirin
        var result = document.Evaluate("//*[@class='mutlu']//span",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // Ortaya çıkan düğümler üzerinde yineleme
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // Çıktı: Merhaba
            // Çıktı: Dünya!
        }
    }
}
```

Bu örnek, HTML belgesindeki öğeleri niteliklerine ve yapılarına göre bulmak için XPath sorgularının kullanımını gösterir.

## CSS Seçiciler

CSS seçicileri, CSS stil sayfalarının öğeleri hedeflemesine benzer şekilde, bir HTML belgesindeki öğeleri seçmek için alternatif bir yol sağlar.

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
    
    // Hazırlanan koda göre bir belgeyi başlatın
    using (var document = new HTMLDocument(code, "."))
    {
        // Sınıf ve hiyerarşiye dayalı öğeleri çıkarmak için bir CSS seçici kullanın
        var elements = document.QuerySelectorAll(".happy span");
        
        // Sonuçta ortaya çıkan öğe listesi üzerinde yineleme yapın
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // Çıktı: Merhaba
            // Çıktı: Dünya!
        }
    }
}
```

Burada, HTML belgesindeki belirli öğeleri hedeflemek için CSS seçicilerin nasıl kullanılacağını gösteriyoruz.

Bu örneklerle Aspose.HTML for .NET kullanarak HTML belgelerindeki öğelerin nasıl gezinileceği, filtreleneceği, sorgulanacağı ve seçileceği konusunda temel bir anlayış elde ettiniz.

## Çözüm

Aspose.HTML for .NET, .NET geliştiricilerinin HTML belgeleriyle verimli bir şekilde çalışmasını sağlayan çok yönlü bir kitaplıktır. Gezinme, filtreleme, sorgulama ve öğeleri seçmeye yönelik güçlü özellikleri sayesinde çeşitli HTML işleme görevlerini sorunsuz bir şekilde gerçekleştirebilirsiniz. Bu öğreticiyi takip ederek ve adresindeki belgeleri inceleyerek[Aspose.HTML for .NET Belgeleri](https://reference.aspose.com/html/net/).NET uygulamalarınız için bu aracın tüm potansiyelini ortaya çıkarabilirsiniz.

## SSS'ler

### S1. Aspose.HTML for .NET'in kullanımı ücretsiz mi?

 Cevap1: Aspose.HTML for .NET ücretsiz deneme sürümü sunuyor ancak üretim kullanımı için bir lisans satın almanız gerekecek. Lisanslama ayrıntılarını ve seçeneklerini şu adreste bulabilirsiniz:[Aspose.HTML Satın Alma](https://purchase.aspose.com/buy).

### Q2. Aspose.HTML for .NET için nasıl geçici lisans alabilirim?

 Cevap2: Test amaçlı olarak geçici bir lisans alabilirsiniz.[Aspose.HTML Geçici Lisans](https://purchase.aspose.com/temporary-license/).

### S3. Aspose.HTML for .NET için nereden yardım veya destek alabilirim?

 A3: Herhangi bir sorunla karşılaşırsanız veya sorularınız varsa, şu adresi ziyaret edebilirsiniz:[Aspose.HTML Forumu](https://forum.aspose.com/) yardım ve topluluk desteği için.

### S4. Aspose.HTML for .NET'i öğrenmek için ek kaynaklar var mı?

 Cevap4: Bu eğitimin yanı sıra, konuyla ilgili daha fazla eğitim ve belgeyi keşfedebilirsiniz.[Aspose.HTML for .NET dokümantasyon sayfası](https://reference.aspose.com/html/net/).

### S5. Aspose.HTML for .NET en son .NET sürümleriyle uyumlu mu?

Cevap5: Aspose.HTML for .NET, en yeni .NET sürümleri ve teknolojileriyle uyumluluğun sağlanması amacıyla düzenli olarak güncellenmektedir.