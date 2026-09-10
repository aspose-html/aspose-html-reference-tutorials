---
category: general
date: 2026-02-10
description: Özel kaynak işleyicisi, C#'ta HTML'yi ZIP'e dönüştürmenizi sağlar. HTML'yi
  zip olarak kaydetmeyi ve HTML kaynaklarını verimli bir şekilde akıtmayı öğrenin.
draft: false
keywords:
- custom resource handler
- convert html to zip
- save html as zip
- create zip with html
- stream html resources
language: tr
og_description: Özel kaynak işleyicisi, HTML'yi C#'ta ZIP'e dönüştürmenizi sağlar.
  HTML'yi zip olarak kaydetmek ve HTML kaynaklarını akışa almak için bu adım adım
  kılavuzu izleyin.
og_title: C#'ta Özel Kaynak İşleyicisi – HTML'yi ZIP'e Dönüştür
tags:
- Aspose.HTML
- C#
- ZIP archive
- file streaming
title: C#'ta Özel Kaynak İşleyicisi – HTML'yi ZIP'e Dönüştürme Öğreticisi
url: /tr/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/
---

content with all translations and unchanged shortcodes.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Özel Kaynak İşleyici – HTML'yi C#'ta ZIP'e Dönüştürme

Hiç **custom resource handler** kullanarak ham HTML'den doğrudan bir ZIP dosyasına nasıl geçileceğini merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici, bir HTML sayfasını varlıklarıyla birlikte paketlemek zorunda kaldığında, geçici dosyalarla diski kirletmeden bir engelle karşılaşıyor. İyi haber? Aspose.HTML ile tüm işlemi bellekte yapabilirsiniz ve sır, özel bir kaynak işleyicide saklı.

Bu öğreticide, **convert HTML to ZIP**, **save HTML as ZIP** ve **stream HTML resources** işlemlerini gösteren tam, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Sonunda, bir HTML dizesi alıp sayfayı ve tüm bağlı kaynakları içeren hazır‑indirme `result.zip` dosyasını üreten tek bir metoda sahip olacaksınız.

> **Önkoşullar** – .NET 6+ (veya .NET Framework 4.6+), Aspose.HTML for .NET yüklü ve akışlar hakkında temel bir anlayış. Harici araç gerekmiyor.

---

## Özel Kaynak İşleyici – Temel Kavram

Aspose.HTML'de bir *resource handler*, bir belgenin her parçasının **nerede** sonlanacağını belirleyen bir nesnedir—diskte bir dosya, bir bellek tamponu ya da, göstereceğimiz gibi, bir ZIP arşivindeki bir giriş. `ResourceHandler` sınıfını alt sınıf olarak türeterek ana HTML dosyası **ve** her yardımcı kaynağın (CSS, görseller, fontlar vb.) çıktı konumu üzerinde tam kontrol elde edersiniz.

Bunu, belgenizin varlıkları için bir trafik polisiyormuş gibi düşünün: `HandleResource` yöntemi size ana HTML için bir `Stream` verirken, `ResourceSaving` olayı her bağımlı dosyayı yazılmadan hemen önce yakalamanıza olanak tanır.

## Adım 1: Özel Bir Kaynak İşleyici Uygulayın

İlk olarak, `ResourceHandler` sınıfından türeten bir sınıf oluşturun. `HandleResource` metodunu geçersiz kılarak Aspose'a birincil HTML çıktısı için yeni bir `MemoryStream` sağlarız. Bağlı varlıklar için ise daha sonra `ResourceSaving` olayına bağlanacağız.

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using System.IO;

/// <summary>
/// Supplies a stream for every resource the HTML document needs to save.
/// </summary>
class MyHandler : ResourceHandler
{
    /// <summary>
    /// Returns a new stream for the main HTML content.
    /// </summary>
    public override Stream HandleResource(ResourceInfo info)
    {
        // In real life you might return a FileStream or a ZipEntry stream.
        // Here we just hand back a clean MemoryStream.
        return new MemoryStream();
    }
}
```

**Neden önemli:** Yeni bir `MemoryStream` döndürmek, HTML'nin dosya sistemine dokunmadığı anlamına gelir. Bu, daha sonra temiz bir, bellek içi ZIP oluşturmanın temelidir.

## Adım 2: HTML'yi Tek Bir MemoryStream'e Kaydedin

Artık bir işleyicimiz olduğuna göre, bir HTML belgesi oluşturup tamamen bellekte yakalayabiliriz. Bu adım, sadece ZIP'e ihtiyacınız varsa isteğe bağlıdır, ancak işleyicinin tek başına nasıl çalıştığını gösterir.

```csharp
using Aspose.Html;

// Sample HTML – replace with your own markup or load from a file.
string htmlContent = "<html><head><title>Demo</title></head><body>Hello world!</body></html>";

// Create the document from a string.
HTMLDocument htmlDocument = new HTMLDocument(htmlContent);

// Instantiate our custom handler.
MyHandler memoryHandler = new MyHandler();

using (MemoryStream htmlStream = new MemoryStream())
{
    // Save triggers HandleResource and writes the HTML into htmlStream.
    htmlDocument.Save(htmlStream, memoryHandler);

    // Reset position for potential reading.
    htmlStream.Position = 0;

    // For demo purposes, dump the HTML to console.
    using (StreamReader reader = new StreamReader(htmlStream))
    {
        Console.WriteLine("Generated HTML:");
        Console.WriteLine(reader.ReadToEnd());
    }
}
```

**Beklenen çıktı** (okunabilirlik için biçimlendirilmiş):

```
Generated HTML:
<html><head><title>Demo</title></head><body>Hello world!</body></html>
```

Bu kodu çalıştırdığınızda, HTML'nin yalnızca RAM'de bulunduğunu—hiç geçici dosya oluşturulmadığını göreceksiniz.

## Adım 3: HTML ve Kaynakları Bir ZIP Arşivine Paketleyin

Şimdi en lezzetli kısma geliyoruz: HTML'yi **ve** başvurulan her varlığı, ara dosyalar diske yazılmadan bir ZIP dosyasına paketlemek. `System.IO.Compression.ZipArchive` ve `ResourceSaving` olayını birlikte kullanacağız.

```csharp
using Aspose.Html;
using System.IO;
using System.IO.Compression;

// Re‑use the same HTMLDocument from the previous step.
HTMLDocument htmlDocument = new HTMLDocument("<html><body>Hello world!</body></html>");

// Path where the final ZIP will be written.
string zipPath = Path.Combine(Environment.CurrentDirectory, "result.zip");

// Open a FileStream for the ZIP file.
using (FileStream zipFile = new FileStream(zipPath, FileMode.Create))
using (ZipArchive zipArchive = new ZipArchive(zipFile, ZipArchiveMode.Update))
{
    // Create a fresh handler for the ZIP operation.
    MyHandler zipHandler = new MyHandler();

    // Hook the ResourceSaving event – this fires for every resource.
    zipHandler.ResourceSaving += (sender, e) =>
    {
        // Ensure we don't create leading folder entries like "/css/style.css".
        string entryName = e.ResourceInfo.Path.TrimStart('/');

        // Create a new entry inside the ZIP.
        ZipArchiveEntry entry = zipArchive.CreateEntry(entryName);

        // Provide the stream that Aspose will write into.
        e.Stream = entry.Open();
    };

    // Save the document; the handler will fill the ZIP for us.
    htmlDocument.Save(zipHandler);
}

// Verify the ZIP exists.
Console.WriteLine($"ZIP created at: {zipPath}");
```

### Arkada Ne Oluyor?

1. **`ResourceSaving` tetiklenir** ana HTML dosyası ve her bağlı varlık için.
2. Lambda ifademiz, açık ZIP içinde eşleşen bir giriş (`CreateEntry`) oluşturur.
3. `e.Stream = entry.Open()` atayarak, Aspose'a ZIP girişine doğrudan yazan bir yazılabilir akış veriyoruz.
4. `htmlDocument.Save` tamamlandığında, ZIP içinde tam oluşmuş bir HTML sayfası ve işaretlemede referans verilen tüm CSS, görseller veya fontlar bulunur.

**Sonuç:** Tarayıcılara sunabileceğiniz, e‑postalara ekleyebileceğiniz veya blob depolamada saklayabileceğiniz tek bir `result.zip` dosyası—arkada hiçbir geçici dosya kalmaz.

## Bonus: ZIP'i Bir Web API'de Kullanma

İsteğe bağlı ZIP döndüren bir ASP.NET Core uç noktası oluşturuyorsanız, aynı mantık geçerlidir. İşte kompakt bir denetleyici eylemi:

```csharp
[ApiController]
[Route("api/[controller]")]
public class HtmlZipController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult DownloadZip()
    {
        // Build the document (could be loaded from a DB, etc.).
        var html = "<html><body><h1>Dynamic report</h1></body></html>";
        var doc = new HTMLDocument(html);
        var handler = new MyHandler();

        // Prepare an in‑memory ZIP.
        using var zipStream = new MemoryStream();
        using (var archive = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            handler.ResourceSaving += (s, e) =>
            {
                var entry = archive.CreateEntry(e.ResourceInfo.Path.TrimStart('/'));
                e.Stream = entry.Open();
            };
            doc.Save(handler);
        }

        zipStream.Position = 0;
        return File(zipStream, "application/zip", "report.zip");
    }
}
```

Artık `/api/HtmlZip/download` adresine bir GET isteği, oluşturulan zip'i doğrudan istemciye akıtıyor—anlık raporlar için mükemmel.

## Yaygın Tuzaklar & Pro İpuçları

| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| **ZIP içinde boş klasörler** | `ResourceInfo.Path` `/` ile başladığı için `/` gibi bir giriş oluşur | Olay işleyicide gösterildiği gibi `TrimStart('/')` kullanın. |
| **Eksik görseller** | Mutlak URL'lerle referans verilen görseller otomatik olarak alınmaz | `htmlDocument.Options.ResourceLoading = ResourceLoadingMode.Stream` ayarlayın ve uzaktan varlıkları indiren özel bir `ResourceHandler` sağlayın. |
| **Büyük dosyalar bellek baskısı yaratır** | ZIP kapanana kadar tüm akışlar bellekte tutulur | `ZipArchiveMode.Update` yerine `Create` kullanın ve her girişi tamponlamadan doğrudan yazın, ya da boyut RAM'i aşarsa diskte akıtın. |
| **“The stream does not support seeking” hatası** | Birden çok kaynak için yeniden kullanılmayan, arama desteklemeyen bir akışı yeniden kullanmaya çalışmak | Her kaynak için yeni bir `MemoryStream` veya `entry.Open()` sağlayın. |

## Sonuç

Şimdi bir **custom resource handler**'ın, **convert HTML to ZIP**, **save HTML as ZIP** ve **stream HTML resources** işlemlerini dosya sistemine dokunmadan nasıl mümkün kıldığını gösterdik. `HandleResource` metodunu geçersiz kılarak ve `ResourceSaving` olayına bağlanarak, Aspose.HTML'den çıkan her bayt üzerinde ayrıntılı kontrol elde edersiniz.

Bu desen ölçeklenebilir: bellek içi `MemoryStream`'i bir bulut blob akışıyla değiştirin, sıkıştırma ayarları ekleyin veya hangi varlıkların paketlendiğini denetlemek için bir günlük katmanı ekleyin. Kaynak hattına sahip olduğunuzda, sınır yoktur.

Bir sonraki adıma hazır mısınız? HTML'nize CSS ve görseller gömün, uzaktan kaynak yüklemeyi deneyin veya bu akışı, isteğe bağlı ZIP döndüren bir Azure Function'a entegre edin. İyi kodlamalar!

--- 

*Özel bir kaynak işleyicisinin HTML'yi ZIP dosyasına dönüştürme akışını gösteren görsel.*

![Özel kaynak işleyici akışı](https://example.com/placeholder-image.png "Özel kaynak işleyici akışı")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}