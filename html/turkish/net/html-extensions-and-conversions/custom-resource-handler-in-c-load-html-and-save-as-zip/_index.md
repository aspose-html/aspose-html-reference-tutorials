---
category: general
date: 2026-03-15
description: Özel kaynak işleyicisi, URL'den HTML yüklemenizi ve HTML'yi ZIP olarak
  kaydetmenizi sağlar. Web sayfasını ZIP'e dönüştürmeyi ve kaynaklarıyla birlikte
  HTML'yi dakikalar içinde indirmeyi öğrenin.
draft: false
keywords:
- custom resource handler
- load html from url
- save html as zip
- convert webpage to zip
- download html with resources
language: tr
og_description: Özel kaynak işleyicisi, URL'den HTML yüklemenizi, web sayfasını ZIP'e
  dönüştürmenizi ve kaynaklarla birlikte HTML'yi indirmenizi sağlar. Tam adım adım
  kılavuz.
og_title: C#'ta Özel Kaynak İşleyicisi – HTML'yi Yükle ve ZIP Olarak Kaydet
tags:
- Aspose.Html
- C#
- Web Scraping
title: C#'ta Özel Kaynak İşleyicisi – HTML Yükle ve ZIP Olarak Kaydet
url: /tr/net/html-extensions-and-conversions/custom-resource-handler-in-c-load-html-and-save-as-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Özel Kaynak İşleyici – URL'den HTML Yükle ve HTML'yi ZIP Olarak Kaydet

Canlı bir sayfayı çekmek, tüm resimleri, scriptleri ve stil sayfalarını saklamak ve ardından hepsini düzenli bir ZIP dosyası olarak göndermek için **custom resource handler**'a hiç ihtiyaç duydunuz mu? Tek başınıza değilsiniz. Birçok otomasyon projesinde—örneğin çevrim dışı okuyucular, arşivleme araçları veya test paketleri—**load HTML from URL** yapmak, tüm dış kaynakları yakalamak ve ardından **save HTML as ZIP** yapmak istersiniz, diske dokunmadan.  

Bu öğreticide tam olarak bunu adım adım göstereceğiz: Aspose.HTML for .NET kullanarak bir **custom resource handler** oluşturmak, uzak bir sayfayı almak ve **convert webpage to ZIP** yapmak, böylece daha sonra **download HTML with resources** yapabilirsiniz. Gereksiz ayrıntı yok, sadece Visual Studio'ya yapıştırıp bugün çalıştırabileceğiniz çalışan bir çözüm.

## Gereksinimler

- .NET 6 SDK veya daha yeni bir sürüm (API, .NET Core ve .NET Framework'te aynı şekilde çalışır)  
- Aspose.HTML for .NET NuGet paketi (`Aspose.HTML`) – `dotnet add package Aspose.HTML` komutuyla kurun  
- Temel C# bilgisi – kodu yeni başlayanlar için yeterince basit tutacağız  
- Hedef URL için internet erişimi (örnek: `https://example.com`)  

Hepsi bu. Zaten bir projeniz varsa, kodu içine yapıştırın; aksi takdirde `dotnet new console` ile bir konsol uygulaması oluşturun.

## Adım 1: Özel Kaynak İşleyicisinin Rolünü Anlamak

Kod yazmaya başlamadan önce, **neden** özel bir işleyicinin önemli olduğunu açıklığa koyalım. Aspose.HTML, dış kaynakları (görseller, CSS, JS) talep üzerine yükler. Varsayılan olarak bunları doğrudan diske akıtır, bu yavaş olabilir ve geçici dosyalar bırakır. Bir **custom resource handler**, her isteği yakalar, size yazabileceğiniz bir `Stream` verir ve veriyi bellekte tutup tutmayacağınıza, dönüştürüp dönüştürmeyeceğinize veya tamamen atlayacağınıza karar vermenizi sağlar.

İşleyiciyi, “Hey, bu görsele ihtiyacım var—işte bir kova; doldur ve işin bittiğinde geri ver.” diyen bir aracı olarak düşünün. Her seferinde yeni bir `MemoryStream` döndürerek, her şeyi RAM'de tutarız ve daha sonra tüm içeriği ziplemek çok basit olur.

## Adım 2: Özel Kaynak İşleyicisini Uygulamak

Aşağıda tam sınıf tanımı yer alıyor. `HandleResource` metodunun `override` edildiğine dikkat edin; bu metod, istenen varlığı (URL, MIME tipi vb.) tanımlayan bir `ResourceInfo` nesnesi alır. Biz sadece yeni bir `MemoryStream` döndürürüz. Gerçek bir senaryoda `info`yu inceleyerek reklamları veya büyük videoları filtreleyebilirsiniz, ancak **download HTML with resources** demosu için basit tutuyoruz.

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Rendering.Image;
using System.IO;

/// <summary>
/// Captures every external resource (images, CSS, scripts) in memory.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Returning a fresh MemoryStream keeps the resource data in memory.
        // Aspose.HTML will write the incoming bytes into this stream.
        return new MemoryStream();
    }
}
```

> **Pro ipucu:** Bellek kullanımını sınırlamanız gerekirse, `MemoryStream`i bir boyut sınırı uygulayan özel bir akışla sarabilirsiniz.

## Adım 3: İşleyiciyi Kullanarak URL'den HTML Yüklemek

Şimdi uzak adrese işaret eden bir `HTMLDocument` oluşturuyoruz. Yapıcı otomatik olarak sayfayı almaya başlar ve işleyicimiz sayesinde, her bağlı kaynak az önce kurduğumuz bellek içi akışlara yönlendirilir.

```csharp
using Aspose.Html;
using System;

// Step 3: Load the HTML document you want to process.
var url = "https://example.com"; // <-- replace with your target page
var htmlDocument = new HTMLDocument(url);
```

URL erişilemezse, Aspose.HTML bir istisna fırlatır—bu yüzden üretim kodunda bunu bir `try/catch` bloğuna almanız iyi olur. Kısalık açısından burada bunu atlıyoruz.

## Adım 4: Paketlenmiş HTML'i (veya ZIP'i) Bellek Akışına Kaydetmek

Belge tamamen yüklendiğinde, şimdi `Save` metodunu çağırıyoruz. `MyHandler` örneğimizi geçirerek, Aspose.HTML sonraki kaydetme işlemleri için aynı bellek içi akışları kullanacağını bilir. Kullandığımız `Save` aşırı yüklemesi, temel `.html` dosyasını ve yakalanan tüm kaynakları içeren bir ZIP arşivi olan **packed HTML** formatını yazar.

```csharp
using System.IO;

// Step 4: Save the entire document, including its resources, into a memory stream.
using (var packedHtmlStream = new MemoryStream())
{
    // The handler is optional here because the document already captured resources,
    // but passing it again ensures consistency if you later switch to a different save mode.
    htmlDocument.Save(packedHtmlStream, new MyHandler());

    // At this point `packedHtmlStream` holds the packed HTML (ZIP format).
    // You can write it to disk, send it over a network, or keep it in memory.
    
    // Example: write to a file for verification
    File.WriteAllBytes("packed_page.zip", packedHtmlStream.ToArray());
    Console.WriteLine($"Saved packed HTML as ZIP – size: {packedHtmlStream.Length / 1024} KB");
}
```

**Görmeniz gereken:** Programı çalıştırdıktan sonra, proje klasörünüzde bir `packed_page.zip` dosyası oluşur. Açtığınızda `index.html` ve bir varlık klasörü (`images/`, `css/`, vb.) bulacaksınız. Bu, **convert webpage to zip** işleminin sonucudur.

## Adım 5: Çıktıyı Doğrulama – Gerçekten Tüm Kaynakları İçeriyor mu?

Hızlı bir kontrol, işleyicinin görevini yerine getirip getirmediğini doğrulamaya yardımcı olur. ZIP içindeki girdileri listeleyerek her dış dosyanın dahil edildiğini teyit edebilirsiniz.

```csharp
using System.IO.Compression;

// Verify contents
using (var zip = new ZipArchive(new MemoryStream(File.ReadAllBytes("packed_page.zip")), ZipArchiveMode.Read))
{
    Console.WriteLine("ZIP contains the following entries:");
    foreach (var entry in zip.Entries)
    {
        Console.WriteLine($"- {entry.FullName} ({entry.Length / 1024} KB)");
    }
}
```

Eksik görseller veya CSS dosyaları fark ederseniz, orijinal sayfanın ağ isteklerini tekrar kontrol edin. Bazen kaynaklar, ilk HTML ayrıştırmasından sonra JavaScript ile yüklenir; Aspose.HTML yalnızca işaretlemede doğrudan referans verilen kaynakları yakalar. Bu dinamik durumlar için bir headless tarayıcı yaklaşımına ihtiyaç duyarsınız, ancak bu **custom resource handler** rehberinin kapsamı dışındadır.

## Yaygın Sorular ve Kenar Durumları

### ZIP içinde HTML dosyasının giriş adı için özel bir ad istesem ne olur?

`HtmlSaveOptions` içeren bir `SaveOptions` nesnesi geçirin ve `DocumentFileName` özelliğini ayarlayın. Örnek:

```csharp
var options = new HtmlSaveOptions { DocumentFileName = "myPage.html" };
htmlDocument.Save(packedHtmlStream, options, new MyHandler());
```

### Hangi kaynakların kaydedileceğini sınırlayabilir miyim?

Kesinlikle. `HandleResource` içinde `info.SourceUrl` veya `info.MimeType`'ı inceleyin. Atlamak istediğiniz kaynaklar için `null` döndürün (örneğin büyük video dosyaları). Aspose.HTML bunları basitçe yok sayar.

### Büyük sayfalar için her şeyi bellekte tutmak güvenli mi?

Orta ölçekli siteler (birkaç megabayt) için sorun yok. Megabayt ölçeğinde varlıklar bekliyorsanız, doğrudan geçici bir dosyaya akıtmayı veya `OutOfMemoryException` almamak için sınırlı bir tampon kullanmayı düşünün.

## Tam Çalışan Örnek

Hepsini bir araya getirerek, yeni bir konsol projesine kopyalayıp yapıştırabileceğiniz tek bir dosya:

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using System;
using System.IO;
using System.IO.Compression;

class MyHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        return new MemoryStream(); // Keep each resource in memory
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Load the remote page
        var url = "https://example.com"; // change as needed
        var htmlDocument = new HTMLDocument(url);

        // 2️⃣ Prepare a memory stream for the packed output
        using (var packedHtmlStream = new MemoryStream())
        {
            // 3️⃣ Save as a ZIP (packed HTML) using our custom handler
            htmlDocument.Save(packedHtmlStream, new MyHandler());

            // 4️⃣ Persist to disk for inspection (optional)
            File.WriteAllBytes("packed_page.zip", packedHtmlStream.ToArray());
            Console.WriteLine($"Saved ZIP – {packedHtmlStream.Length / 1024} KB");
        }

        // 5️⃣ Quick verification of ZIP contents
        using (var zip = new ZipArchive(File.OpenRead("packed_page.zip"), ZipArchiveMode.Read))
        {
            Console.WriteLine("ZIP entries:");
            foreach (var entry in zip.Entries)
                Console.WriteLine($"- {entry.FullName}");
        }
    }
}
```

`dotnet run` komutunu çalıştırın ve tüm sayfayı içeren bir `packed_page.zip` elde edeceksiniz. Bu, tam **download HTML with resources** iş akışıdır.

## Sonuç

Bir **custom resource handler**'ın **load HTML from URL**, her bağlı varlığı yakalamak ve **save HTML as ZIP** için nasıl anahtar olabileceğini gösterdik—dolayısıyla çevrim dışı kullanım için **convert webpage to ZIP** yapabilirsiniz. Yaklaşım hafif, bellekte kalır ve hangi kaynakların tutulacağı üzerinde tam kontrol sağlar.

Sonraki adımlar? `MemoryStream`i dosya tabanlı bir akışla değiştirerek büyük siteleri işleyebilir veya `HtmlSaveOptions` ile çıktı düzenini özelleştirebilirsiniz. Ayrıca **download HTML with resources** işlemini ZIP yerine PDF olarak yapmak isterseniz Aspose.HTML'in PDF dönüşüm yeteneklerini keşfedebilirsiniz.

Kodlamaktan keyif alın ve arşivleriniz her zaman düzenli olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}