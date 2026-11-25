---
category: general
date: 2026-08-19
description: Aspose.HTML ve özel bir kaynak işleyicisi kullanarak C#'ta HTML'yi ZIP
  olarak kaydedin. Kaynakları gömmek ve taşınabilir bir arşiv oluşturmak için bu adım
  adım kılavuzu izleyin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save HTML as ZIP
- custom resource handler
- Aspose.HTML C#
- HTML archive generation
- resource streaming C#
language: tr
lastmod: 2026-08-19
og_description: Aspose.HTML ve özel bir kaynak işleyicisi kullanarak C#'ta HTML'yi
  ZIP olarak kaydedin. Bu öğreticide tam kod gösterilir, her adımın neden önemli olduğu
  açıklanır ve yaygın hatalar ele alınır.
og_image_alt: Screenshot of C# code that saves an HTML document as a ZIP archive
og_title: C#'ta Özel Kaynak İşleyicisiyle HTML'yi ZIP Olarak Kaydet – Tam Rehber
schemas:
- author: Aspose
  dateModified: '2026-08-19'
  description: Save HTML as ZIP in C# using Aspose.HTML and a custom resource handler.
    Follow this step‑by‑step guide to embed resources and generate a portable archive.
  headline: Save HTML as ZIP with a custom resource handler in C#
  type: TechArticle
- description: Save HTML as ZIP in C# using Aspose.HTML and a custom resource handler.
    Follow this step‑by‑step guide to embed resources and generate a portable archive.
  name: Save HTML as ZIP with a custom resource handler in C#
  steps:
  - name: Saving to a specific folder inside the ZIP
    text: 'If you want all resources to reside under a subfolder (e.g., `assets/`),
      modify the handler to prepend the folder name to each file name:'
  - name: Streaming directly to a network location
    text: 'When the ZIP must be sent over HTTP without touching the local file system,
      use a `MemoryStream` for the final archive:'
  - name: Handling large resources
    text: 'Large images or videos can exhaust memory if you keep everything in `MemoryStream`.
      Switch to a file‑based stream inside the handler:'
  - name: Preserving original URLs
    text: 'Aspose.HTML rewrites the `src`/`href` attributes to point to the new locations
      inside the ZIP. If you need to keep the original URLs for later processing,
      capture them before saving:'
  type: HowTo
tags:
- C#
- Aspose.HTML
- ZIP archive
- resource handling
title: C#'ta özel bir kaynak işleyicisiyle HTML'yi ZIP olarak kaydet
url: /tr/net/advanced-features/save-html-as-zip-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'yi ZIP Olarak Kaydetmek için C#'ta Özel Bir Kaynak İşleyicisi Kullanma

Bağlantılı kaynakların nasıl depolanacağını kontrol ederken **HTML'yi ZIP olarak kaydetmeniz** gerekiyorsa, bu kılavuz eksiksiz bir çözüm sunar. Özel bir kaynak işleyicisi oluşturmayı, Aspose.HTML kaydetme seçeneklerini yapılandırmayı ve HTML dosyasını ve varlıklarını içeren taşınabilir bir ZIP arşivi oluşturmayı öğreneceksiniz.

Kaynakları doğru şekilde gömmek, kendine yeten bir web sayfası dağıtmak, uyumluluk için bir raporu arşivlemek veya çevrim dışı kullanım için bir anlık görüntüyü önbelleğe almak istediğinizde önemlidir. Aşağıdaki adımlar Aspose.HTML 23.10 veya daha yeni sürümlerle çalışır ve yalnızca bir .NET geliştirme ortamı gerektirir.

## Oluşturacağınız Şey

* Her kaynak için bir akış döndüren `ResourceHandler`'ı uygulayan bir C# sınıfı.
* Diskten mevcut bir HTML dosyasını yükleyen kod.
* Özel işleyiciyi kullanmak için `HTMLSaveOptions` yapılandırması.
* `HTMLDocument.Save` çağrısı, HTML belgesini ve tüm başvurulan kaynakları içeren bir ZIP arşivi `output.zip` üretir.

## Önkoşullar

* .NET 6.0 SDK veya daha yeni bir sürüm (örnek .NET Framework 4.7.2'de de çalışır).
* Visual Studio 2022 veya C# projelerini destekleyen herhangi bir IDE.
* .NET için Aspose.HTML NuGet paketi (`Aspose.Html`).
* En az bir dış kaynak (görsel, CSS, script) içeren bir HTML dosyası (`example.html`) böylece işleyicinin çalışmasını görebilirsiniz.

## Adım 1: Özel bir kaynak işleyicisi oluşturma

**Özel kaynak işleyicisi**, her dış varlığın nereye yazılacağını belirler. `ResourceHandler`'ı uygulamak, çıktı akışı üzerinde tam kontrol sağlar.

```csharp
using Aspose.Html;
using System.IO;

/// <summary>
/// Provides a stream for each resource referenced by the HTML document.
/// </summary>
class MyResourceHandler : ResourceHandler
{
    /// <summary>
    /// Returns a writable stream for the given resource.
    /// </summary>
    /// <param name="resource">Metadata about the resource being saved.</param>
    /// <returns>A stream that Aspose.HTML will write the resource to.</returns>
    public override Stream HandleResource(Resource resource)
    {
        // Create a memory stream for the resource.
        // In production you might write to a file on disk, a cloud blob, or a database.
        return new MemoryStream();
    }
}
```

**Neden Önemli:**  
`HandleResource`, her dış dosya (görseller, stil sayfaları, scriptler) için çağrılır. Yeni bir `MemoryStream` döndürerek, Aspose.HTML'nin verileri bellekte toplamasını sağlarsınız; kaydetme rutini daha sonra bu verileri ZIP arşivine paketler. Kaynakları diske kaydetmeniz gerekiyorsa, `new MemoryStream()` ifadesini `File.Create(Path.Combine(outputFolder, resource.FileName))` ile değiştirin.

## Adım 2: HTML belgesini yükleme

Kaynak dosyayı `HTMLDocument` ile yükleyin. Yapıcı, bir dosya yolu, bir URL veya bir akış alabilir.

```csharp
using Aspose.Html;

// Adjust the path to point to your HTML file.
string htmlPath = Path.Combine("YOUR_DIRECTORY", "example.html");

// Load the document into memory.
HTMLDocument doc = new HTMLDocument(htmlPath);
```

**Neden Önemli:**  
Belgeyi önce yüklemek, Aspose.HTML'nin DOM'u ayrıştırmasını ve tüm bağlantılı kaynakları keşfetmesini sağlar. Kütüphane, keşfedilen her kaynağı önceki adımda tanımladığınız işleyiciye gönderir.

## Adım 3: Kaydetme seçeneklerini özel işleyiciyle yapılandırma

`HTMLSaveOptions`, çıktı formatını ve kaynak işleyicisini belirlemenizi sağlar.

```csharp
using Aspose.Html.Saving;

// Create default save options.
HTMLSaveOptions saveOptions = new HTMLSaveOptions();

// Attach the custom resource handler.
saveOptions.ResourceHandler = new MyResourceHandler();
```

**Neden Önemli:**  
`ResourceHandler` atanmazsa, Aspose.HTML kaynakları diskte geçici bir klasöre yazar ve bu kontrol edilemez. `MyResourceHandler`'ınızı bağlayarak, ZIP arşivi oluşturulmadan önce her kaynağın tam olarak nasıl depolanacağını belirlemiş olursunuz.

## Adım 4: Belgeyi ZIP arşivi olarak kaydetme

Son olarak, `HTMLDocument.Save` metodunu `SaveFormat.Zip` ile çağırın. Bu yöntem HTML dosyasını ve işleyici tarafından sağlanan tüm akışları sıkıştırır.

```csharp
// Define the output ZIP path.
string zipPath = Path.Combine("YOUR_DIRECTORY", "output.zip");

// Save the document as a ZIP archive.
doc.Save(zipPath, SaveFormat.Zip, saveOptions);
```

Çağrı tamamlandığında, `output.zip` şunları içerir:

* `example.html` – güncellenmiş kaynak bağlantılarına sahip orijinal HTML dosyası.
* Tüm dış varlıklar (görseller, CSS, JS) ayrı girişler olarak depolanır; her biri özel işleyici tarafından oluşturulur.

## Sonucu Doğrulama

Oluşturulan ZIP'i herhangi bir arşiv görüntüleyiciyle açın. Aşağıdakine benzer bir klasör yapısı görmelisiniz:

```
output.zip
│─ example.html
│─ images/
│   └─ logo.png
│─ styles/
│   └─ main.css
│─ scripts/
│   └─ app.js
```

Çıkarılan klasörden `example.html` dosyasını bir tarayıcıda açın; sayfa orijinaliyle aynı şekilde render edilmelidir, bu da kaynakların doğru şekilde gömüldüğünü doğrular.

## Yaygın varyasyonlar ve kenar durumları

### ZIP içinde belirli bir klasöre kaydetme

Tüm kaynakların bir alt klasör altında (ör. `assets/`) bulunmasını istiyorsanız, işleyiciyi her dosya adına klasör adını ekleyecek şekilde değiştirin:

```csharp
public override Stream HandleResource(Resource resource)
{
    string folder = "assets";
    string entryName = Path.Combine(folder, resource.FileName);
    // Aspose.HTML uses the entry name when packing the ZIP.
    resource.FileName = entryName;
    return new MemoryStream();
}
```

### Doğrudan bir ağ konumuna akış gönderme

ZIP'in yerel dosya sistemine dokunmadan HTTP üzerinden gönderilmesi gerektiğinde, son arşiv için bir `MemoryStream` kullanın:

```csharp
using (var zipStream = new MemoryStream())
{
    doc.Save(zipStream, SaveFormat.Zip, saveOptions);
    zipStream.Position = 0; // Reset for reading.
    // Send zipStream to a web API, store in Azure Blob, etc.
}
```

### Büyük kaynakları işleme

Büyük görseller veya videolar, her şeyi `MemoryStream` içinde tutarsanız belleği tüketebilir. İşleyicinin içinde dosya tabanlı bir akışa geçiş yapın:

```csharp
public override Stream HandleResource(Resource resource)
{
    string tempPath = Path.GetTempFileName();
    return new FileStream(tempPath, FileMode.Create, FileAccess.Write);
}
```

`doc.Save` tamamlandıktan sonra geçici dosyaları silebilirsiniz.

### Orijinal URL'leri koruma

Aspose.HTML, `src`/`href` özniteliklerini ZIP içindeki yeni konumlara işaret edecek şekilde yeniden yazar. Daha sonra işlemek üzere orijinal URL'leri tutmanız gerekiyorsa, kaydetmeden önce yakalayın:

```csharp
foreach (var img in doc.Images)
{
    Console.WriteLine($"Original src: {img.Source}");
}
```

## Profesyonel ipuçları

* **İşleyiciyi yeniden kullanın** – `MyResourceHandler`'ın tek bir örneğini oluşturun ve birden fazla kaydetme işlemi arasında yeniden kullanarak tekrar tekrar tahsisatı önleyin.
* **Kaynakları doğrulayın** – `HandleResource` içinde `resource.MimeType` veya `resource.FileName`'i inceleyerek istenmeyen dosyaları filtreleyebilirsiniz (ör. analiz scriptlerini atlayın).
* **Sıkıştırma seviyesini ayarlayın** – `HTMLSaveOptions`, `CompressionLevel` (0–9) özelliğini sunar. Daha yüksek değerler CPU süresi karşılığında daha küçük ZIP'ler üretir.

## Tam, çalıştırılabilir örnek

Aşağıda, yeni bir konsol projesine (`dotnet new console`) kopyalayabileceğiniz tam program yer alıyor. HTML dosyasını yüklemekten `output.zip` üretmeye kadar her adımı gösterir.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Saving;

class MyResourceHandler : ResourceHandler
{
    public override Stream HandleResource(Resource resource)
    {
        // Return a memory stream for each resource.
        // Replace with FileStream if you need disk persistence.
        return new MemoryStream();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Define paths.
        string baseDir = Path.Combine(Environment.CurrentDirectory, "YOUR_DIRECTORY");
        string htmlPath = Path.Combine(baseDir, "example.html");
        string zipPath = Path.Combine(baseDir, "output.zip");

        // 2️⃣ Load the HTML document.
        HTMLDocument doc = new HTMLDocument(htmlPath);

        // 3️⃣ Configure save options with the custom handler.
        HTMLSaveOptions saveOptions = new HTMLSaveOptions
        {
            ResourceHandler = new MyResourceHandler()
        };

        // 4️⃣ Save as a ZIP archive.
        doc.Save(zipPath, SaveFormat.Zip, saveOptions);

        Console.WriteLine($"HTML saved as ZIP at: {zipPath}");
    }
}
```

**Beklenen çıktı**

```
HTML saved as ZIP at: C:\path\to\YOUR_DIRECTORY\output.zip
```

ZIP'i çıkararak önceki bölümde açıklanan yapıyı doğrulayın.

## Sonuç

Artık Aspose.HTML for .NET kullanarak **HTML'yi ZIP olarak kaydetmeyi** ve her varlığın nereye yazılacağını kontrol eden **özel bir kaynak işleyicisi** kullanmayı biliyorsunuz. Bu yaklaşım, kaynak depolama üzerinde tam esneklik sağlar, bellek içi işleme olanak tanır ve bulut ya da şirket içi iş akışlarıyla kolayca bütünleşir.

Buradan devam edebilirsiniz:

* İşleyiciyi, kaynakları Azure Blob Storage'a yazacak şekilde genişletmek (ikincil anahtar kelime: custom resource handler).
* ZIP'i, güvenli belge teslimi için dijital imza ile birleştirmek.
* `HTMLSaveOptions` kullanarak diğer formatları (ör. MHTML) üretmek ve yine kaynakları programlı olarak yönetmek.

Projenizin gereksinimlerine uygun farklı akış tipleri, sıkıştırma seviyeleri ve klasör yapılarıyla denemeler yapın. İyi kodlamalar!

## What Should You Learn Next?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [C#'ta HTML'yi Kaydetme – Özel Kaynak İşleyicisi Kullanarak Tam Kılavuz](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [C#'ta Özel Kaynak İşleyicisi – HTML'yi ZIP'e Dönüştürme Öğreticisi](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [HTML'yi Render Etme – Özel Kaynak İşleyicisi ile Tam Kılavuz](/html/english/net/rendering-html-documents/how-to-render-html-complete-guide-with-custom-resource-handl/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}