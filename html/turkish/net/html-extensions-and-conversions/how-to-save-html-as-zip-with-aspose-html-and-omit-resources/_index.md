---
category: general
date: 2026-10-21
description: Aspose.HTML kullanarak HTML'yi ZIP olarak kaydetmeyi, HTML'yi ZIP'e dönüştürmeyi
  ve temiz bir paket için kaynakları ayıklamayı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save html as zip
- convert html to zip
- how to omit resources
- how to strip resources
- create html zip
language: tr
lastmod: 2026-10-21
og_description: Aspose.HTML ile HTML'yi ZIP olarak kaydedin, HTML'yi ZIP'e nasıl dönüştüreceğinizi
  ve hafif bir arşiv için kaynakları nasıl ayıklayacağınızı öğrenin.
og_image_alt: Screenshot showing the save html as zip process with resources omitted
og_title: Aspose.HTML ile HTML'yi ZIP olarak kaydedin – kaynakları tek adımda dışarıda
  bırakın
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to save HTML as ZIP using Aspose.HTML, convert HTML to ZIP,
    and strip resources for a clean package.
  headline: How to save HTML as ZIP with Aspose.HTML and omit resources
  type: TechArticle
tags:
- Aspose.HTML
- C#
- ZIP archive
- HTML conversion
- Resource handling
title: Aspose.HTML ile HTML'yi ZIP olarak kaydetme ve kaynakları dışarıda bırakma
url: /tr/net/html-extensions-and-conversions/how-to-save-html-as-zip-with-aspose-html-and-omit-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'yi ZIP Olarak Kaydetme ve Aspose.HTML ile Kaynakları Atma

Harici dosyaları kaldırarak **HTML'yi ZIP olarak kaydetmeniz** gerekiyorsa, bu rehber eksiksiz, çalıştırmaya hazır bir çözüm sunar. Eğitim sonunda **HTML'yi ZIP'e dönüştürebilecek**, hangi kaynakların tutulacağını kontrol edebilecek ve yalnızca temel işaretlemeyi içeren temiz bir arşiv oluşturabileceksiniz.

Birçok web‑otomasyon senaryosu, bir sayfayı çevrim dışı kullanım, e‑posta eki veya arşiv depolama için paketlemeyi gerektirir. Görseller, yazı tipleri veya betikler dahil edildiğinde arşiv gereksiz yere şişebilir. Aşağıdaki adımlar **kaynakları nasıl atacağınızı** ve **kaynakları nasıl temizleyeceğinizi** açıklar, böylece ortaya çıkan ZIP hafif kalır.

## Prerequisites

Başlamadan önce şunların yüklü olduğundan emin olun:

- .NET 6.0 veya daha yeni bir sürüm  
- Aspose.HTML for .NET lisansı (veya ücretsiz deneme)  
- Temel bir C# geliştirme ortamı (Visual Studio, VS Code veya Rider)  

`Aspose.Html` dışındaki ek NuGet paketlerine ihtiyaç yoktur.

## Step 1: Create a custom resource handler

**Kaynakları atmanın** temeli, `ResourceHandler` sınıfının bir alt sınıfında yatar. Aspose.HTML, her dış varlık (görseller, CSS, betikler) için bu işleyiciyi çağırır. Boş bir akış döndürerek dönüştürücüye varlığı atlamasını söylersiniz.

```csharp
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Prevents external resources from being written to the output package.
/// </summary>
class CustomResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Returning an empty MemoryStream strips the resource from the ZIP.
        return new MemoryStream();
    }
}
```

**Neden önemli:** Varsayılan davranış, her bağlantılı dosyayı ZIP'e kopyalar ve bu dosya boyutunu iki ya da üç katına çıkarabilir. `HandleResource` metodunu geçersiz kılarak orijinal HTML'i değiştirmeden ince ayar kontrolü elde edersiniz.

## Step 2: Load the HTML document

Kaynak dosyayı `HTMLDocument` ile yükleyin. Yapıcı, bir dosya yolu, bir URL veya bir akış alabilir. Bu örnekte yerel `input.html` dosyasını okuyoruz.

```csharp
// Load the source HTML file from the local file system.
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

HTML bellekte bulunuyorsa ya da bir web isteğinden geliyorsa, bunun yerine bir `MemoryStream` ya da URL dizesi geçirebilirsiniz. API aynı şekilde çalışır.

## Step 3: Configure the save options

`HtmlSaveOptions` bir örneği oluşturun ve Step 1'de oluşturduğunuz özel işleyiciyi atayın. Bu, Aspose.HTML'in bir kaynakla karşılaştığında işleyiciyi kullanmasını sağlar.

```csharp
// Prepare save options and attach the custom resource handler.
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // The ResourceHandler property is what enables resource stripping.
    ResourceHandler = new CustomResourceHandler()
};
```

Burada ayrıca `CompressImages = false` gibi diğer seçenekleri de ayarlayabilirsiniz; bu, görüntü verisini tutarken diğer varlıkları yine de atmanızı sağlar. Örnekte varsayılan sıkıştırma ayarları korunmuştur.

## Step 4: Save the document as a ZIP archive

Son olarak, hedef yolu ve yapılandırılmış seçenekleri kullanarak `Save` metodunu çağırın. Çıktı dosyası, `index.html` (veya orijinal dosya adı) ve **hiçbir dış kaynak** içermeyen bir `.zip` olacaktır.

```csharp
// Save the HTML document as a ZIP file. The archive will contain only the HTML markup.
document.Save("YOUR_DIRECTORY/output.zip", saveOptions);
```

### Expected result

- `output.zip` → tek bir `index.html` dosyası içerir.  
- Tüm görseller, CSS dosyaları ve JavaScript referansları atılmıştır; çünkü özel işleyici her biri için boş bir akış döndürmüştür.  

Arşivi herhangi bir ZIP görüntüleyiciyle açarak doğrulayabilirsiniz. HTML sayfası hâlâ orijinal URL'lere referans verir, ancak bu dosyalar arşivde bulunmaz, paket minimal kalır.

## Full, runnable example

Aşağıda kopyalayıp yapıştırıp çalıştırabileceğiniz tam program yer alıyor. `YOUR_DIRECTORY` kısmını makinenizdeki gerçek bir klasör yolu ile değiştirin.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

class Program
{
    static void Main()
    {
        // Step 1: Define a custom resource handler to control how external resources are saved.
        class CustomResourceHandler : ResourceHandler
        {
            public override Stream HandleResource(ResourceInfo info)
            {
                // Returning an empty stream strips the resource from the ZIP output.
                return new MemoryStream();
            }
        }

        // Step 2: Load an HTML document from a file.
        string inputPath = "YOUR_DIRECTORY/input.html";
        HTMLDocument document = new HTMLDocument(inputPath);

        // Step 3: Create HTML save options and assign the custom handler.
        HtmlSaveOptions saveOptions = new HtmlSaveOptions
        {
            ResourceHandler = new CustomResourceHandler()
        };

        // Step 4: Save the document as a ZIP archive containing the HTML and (now omitted) resources.
        string outputPath = "YOUR_DIRECTORY/output.zip";
        document.Save(outputPath, saveOptions);

        Console.WriteLine($"HTML has been saved as ZIP at: {outputPath}");
    }
}
```

Bu programı çalıştırdığınızda daha önce açıklanan ZIP dosyası üretilir. Artık gereksiz varlıkları paketlemeden HTML sayfasını dağıtabileceksiniz.

## Common variations and edge cases

| Senaryo | Ayar |
|----------|------------|
| **Görselleri tut, ancak CSS/JS'i düşür** | `CustomResourceHandler` içinde `info.MimeType` kontrol edin. `text/css` ve `application/javascript` için yalnızca bir `MemoryStream` döndürün. |
| **Harici yazı tiplerini koru** | `font/woff2` MIME türleri için orijinal akışı döndürün, aksi takdirde boş bir akış döndürün. |
| **Özel bir giriş adıyla ZIP oluştur** | `HtmlSaveOptions` aşırı yüklemesi `Save(string path, SaveOptions options, string entryName)` kullanarak farklı bir kök dosya adı belirleyin. |
| **Birden çok HTML dosyasını tek ZIP içinde birleştir** | Her dosya için ayrı bir `HTMLDocument` oluşturup, her birini `System.IO.Compression` kullanarak aynı `ZipArchive` içine manuel ekleyin. |

Bu varyasyonlar, **kaynakları seçici olarak nasıl temizleyeceğinizi** gösterir ve nihai arşiv boyutu üzerinde tam kontrol sağlar.

## Pro tips

- **Sonucu doğrula**: Kaydetme işleminden sonra ZIP'i açın ve `index.html` dosyasını bir tarayıcıda yükleyin. Eksik kaynaklar kırık link olarak görünecek ve işleyicinin çalıştığını onaylayacaktır.  
- **Performans**: Boş bir `MemoryStream` döndürmek maliyet açısından düşüktür, ancak binlerce varlık varsa kararı önbelleğe almayı düşünün (ör. atlanacak MIME tiplerini tutan bir `HashSet<string>`).  
- **Lisanslama**: Aspose.HTML'in ücretsiz deneme sürümü HTML içinde bir filigran yorumu ekler. Üretim ortamında kaldırmak için lisanslı bir sürüm dağıtın.  

## Conclusion

Artık **HTML'yi ZIP olarak kaydetme**, **HTML'yi ZIP'e dönüştürme** ve Aspose.HTML for .NET kullanarak **kaynakları temizleme** konularını biliyorsunuz. Özel bir `ResourceHandler` uygulayarak istenmeyen dosyaları atabilir ve arşivi hafif tutabilirsiniz. İşleyici mantığını deneyerek yalnızca gerçekten ihtiyaç duyduğunuz kaynakları tutun ve bu deseni daha büyük otomasyon boru hatlarına entegre edin.

---

**Sonraki adımlar**

- `EmbedImages` gibi diğer `HtmlSaveOptions` özelliklerini keşfedin; böylece görselleri doğrudan HTML içine gömebilirsiniz.  
- Aynı ZIP'i oluşturduktan sonra aynı HTML'i PDF'e dönüştürmek için bu yaklaşımı `Aspose.PDF` ile birleştirin.  
- ZIP'i talep üzerine oluşturup diske yazmadan bir istemciye akış olarak gönderebileceğiniz sunucu‑tarafı senaryolarına bakın.  

İyi kodlamalar!

## What Should You Learn Next?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [ZipArchive Nasıl Kullanılır – HTML ve Kaynakları ZIP Dosyasına Kaydetme](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [C#'ta HTML Nasıl Kaydedilir – Özel Kaynak İşleyicileri ve ZIP](/html/english/net/working-with-html-documents/how-to-save-html-in-c-custom-resource-handlers-zip/)
- [C#'ta HTML'yi ZIP Olarak Kaydetme – Tam Aspose.HTML Rehberi](/html/english/net/html-extensions-and-conversions/how-to-save-html-as-zip-in-c-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}