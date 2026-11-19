---
category: general
date: 2026-08-15
description: C#'ta resim ve CSS gibi HTML kaynaklarını yönetmek için özel kaynak işleyicisi
  oluşturun. HTMLLoadOptions, bellek akışları ve HTMLDocument yüklemeyi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: tr
lastmod: 2026-08-15
og_description: C#'ta HTML kaynaklarının akışını kontrol etmek için özel kaynak işleyicisi
  oluşturun. Bu öğreticide HTMLLoadOptions ayarı, bellek akışı işleme ve özel mantıkla
  HTMLDocument yükleme gösterilmektedir.
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: C#'ta Özel Kaynak İşleyicisi Oluşturma – HTML Kaynak Yönetimi İçin Tam Kılavuz
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: HTML yükleme için C#'ta özel kaynak işleyicisi oluştur
url: /tr/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML yükleme için C#'ta özel kaynak işleyicisi oluşturma

HTML dosyaları için **özel kaynak işleyicisi oluşturmanız** gerekiyorsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. `HTMLLoadOptions` ve bellek tabanlı bir akış kullanarak bir HTML belgesi yüklerken görüntüleri, CSS'i ve diğer varlıkları yakalamayı öğreneceksiniz.

Bu öğretici, yeniden kullanılabilir bir işleyici uygulamak, yükleme seçeneklerini yapılandırmak ve kaynakların doğru şekilde yakalandığını doğrulamak için gereken her şeyi kapsar. Harici bir belgeye gerek yok—yalnızca aşağıdaki kod ve açıklamalar yeterlidir.

## Önkoşullar

- .NET 6.0 veya üzeri
- C# hakkında temel bilgi
- `HTMLDocument`, `HtmlLoadOptions` ve `ResourceHandler` sağlayan HTML işleme kütüphanesine referans (ör. GroupDocs.Viewer for .NET)

## Çözümün Genel Bakışı

We will:

1. `ResourceHandler` sınıfını alt sınıf yaparak **özel bir kaynak işleyicisi oluşturma**.
2. `HTMLLoadOptions`'ı işleyiciyi kullanacak şekilde yapılandırma.
3. `HTMLDocument` ile bir HTML dosyasını yükleme; işleyici her kaynak için bir akış sağlar.
4. (İsteğe bağlı) Alınan kaynakları doğrulama amacıyla diske kaydetme.

Her adım tam kaynak kodu ve bunun arkasındaki mantığı içerir.

## Adım 1: Özel kaynak işleyici sınıfını tanımlama

Özel bir işleyici oluşturmak, kütüphanenin kaynak baytlarını kontrol ettiğiniz bir akışa yazabilmesi için `HandleResource` metodunu geçersiz kılmak anlamına gelir. `MemoryStream` kullanmak veriyi bellekte tutar; bu, test veya sonraki işleme için idealdir.

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**Neden önemlidir:**  
`HandleResource`'u geçersiz kılmak, kaynak verilerinin nereye gideceği üzerinde tam kontrol sağlar. Daha sonra görüntüleri önbelleğe almanız, CSS'i dönüştürmeniz veya kaynak kullanımını kaydetmeniz gerekirse, `MemoryStream`'i herhangi bir özel akış uygulamasıyla değiştirebilirsiniz.

## Adım 2: `HTMLLoadOptions`'ı işleyiciyi kullanacak şekilde yapılandırma

`HTMLLoadOptions`, işleyiciyi yükleme işlem hattına bağlamanızı sağlar. `ResourceHandler` özelliğini ayarlamak, görüntüleyiciye her dış varlık için `MyHandler`'ı çağırmasını söyler.

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**Neden önemlidir:**  
`ResourceHandler` atanmazsa, görüntüleyici kaynakları varsayılan konumuna (genellikle geçici bir klasör) yazar. Kendi işleyicinizi belirleyerek, uygulamanızın depolama stratejisiyle uyumlu **özel kaynak işleyicisi oluşturma** davranışı elde edersiniz.

## Adım 3: Yapılandırılmış seçeneklerle HTML belgesini yükleme

Şimdi HTML dosyasını yükleyin. Görüntüleyici, karşılaştığı her kaynak için `MyHandler.HandleResource` metodunu çağıracaktır.

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

Bu noktada HTML içeriği ayrıştırılmış ve tüm dış kaynaklar `MyHandler` tarafından sağlanan bellek tamponlarına akıtılmıştır.

## Adım 4 (isteğe bağlı): Yakalanan kaynaklara erişme

Kaynakları incelemeniz veya kalıcı hale getirmeniz gerekiyorsa, `MyHandler`'ı her `MemoryStream`'i kaynak adına göre anahtarlanan bir sözlükte saklayacak şekilde değiştirebilirsiniz.

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

Yükleme sonrasında, `handler.Resources` üzerinde döngü yaparak her birini diske yazabilirsiniz:

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**Neden önemlidir:**  
Kaynakları depolamak, görüntü optimizasyonu, CSS küçültme veya arşivleme gibi son‑işlemeleri mümkün kılar. Ayrıca **özel kaynak işleyicisi oluşturma** mantığının amaçlandığı gibi çalıştığını somut bir şekilde doğrular.

## Adım 5: Temizleme

`HTMLDocument` ve tüm akışlar, yönetilmeyen kaynakları serbest bırakmak için dispose edilmelidir.

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## Tam Çalıştırılabilir Örnek

Aşağıda, sınıf tanımından kaynak çıkarımına kadar tüm adımları gösteren bağımsız bir program bulunmaktadır.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**Beklenen çıktı**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

Konsol, görüntüleyicinin özel işleyiciniz üzerinden akıttığı her kaynağı listeler ve **özel kaynak işleyicisi oluşturma** iş akışının başarılı olduğunu doğrular.

## Yaygın sorular ve uç durumlar

| Soru | Cevap |
|----------|--------|
| *Kaynak büyük olursa (ör. yüksek çözünürlüklü görüntü)?* | `MemoryStream` yerine geçici bir klasöre işaret eden bir `FileStream` kullanın. Bu, aşırı bellek tüketimini önler. |
| *Kaynakları tipe göre filtreleyebilir miyim?* | `HandleResource` içinde `info.MimeType` veya `info.Extension` değerlerini inceleyin ve istenmeyen tipler için `null` döndürün. `null` döndürmek, görüntüleyiciye kaynağı atlamasını söyler. |
| *İş parçacığı güvenliği gerekli mi?* | Aynı işleyici örneği birden çok eşzamanlı yüklemede kullanılıyorsa, `Resources` sözlüğünü bir kilit ile koruyun veya eşzamanlı bir koleksiyon kullanın. |
| *Göreli URL'leri nasıl desteklerim?* | `ResourceInfo` orijinal URL'yi içerir; depolamadan önce göreli referansları çözmek için bunu HTML dosyasının temel yolu ile birleştirebilirsiniz. |

## Sonuç

Artık C#'ta HTML yükleme için **özel kaynak işleyicisi oluşturma**, `HTMLLoadOptions` yapılandırma, akıtılan varlıkları yakalama ve sorumlu bir şekilde temizleme konularını biliyorsunuz. Bu desen, kaynak yönetimi üzerinde tam kontrol sağlar; anlık görüntü işleme, CSS yeniden yazma veya güvenli depolama gibi senaryoları mümkün kılar.

Sonra, farklı render seçenekleriyle **HTMLDocument yükleme** gibi ilgili konuları keşfedin veya işleyiciyi doğrudan bulut depolamaya yazan **C# resource handler** uygulamalarına genişletin. İşleyicinin `HandleResource` metoduyla projenizin özel kaynak iş akışına uyacak şekilde deneyler yapın.

## Bir Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir ve ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olur.

- [C#'ta Dizeden HTML Oluşturma – Özel Kaynak İşleyici Kılavuzu](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [C#'ta Özel Kaynak İşleyici – HTML'yi ZIP'e Dönüştürme Öğreticisi](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [C#'ta HTML Kaydetme – Özel Kaynak İşleyicisi Kullanarak Tam Kılavuz](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}