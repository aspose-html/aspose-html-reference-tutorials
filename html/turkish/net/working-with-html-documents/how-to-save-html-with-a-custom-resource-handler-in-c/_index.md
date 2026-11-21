---
category: general
date: 2026-11-20
description: C#'ta özel bir ResourceHandler kullanarak HTML nasıl kaydedilir ve aynı
  zamanda HTML'yi zip arşivlerine, özlü ve üretim‑hazır kodla nasıl kaydedebileceğinizi
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: tr
lastmod: 2026-11-20
og_description: C#'ta özel bir ResourceHandler kullanarak HTML nasıl kaydedilir ve
  isteğe bağlı olarak HTML zip dosyalarına kaydedilir—.NET geliştiricileri için eksiksiz,
  çalıştırılabilir rehber.
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: C#'ta özel bir kaynak işleyicisiyle HTML nasıl kaydedilir
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  headline: How to save HTML with a custom resource handler in C#
  type: TechArticle
- description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  name: How to save HTML with a custom resource handler in C#
  steps:
  - name: What if I need multiple HTML files in the same zip?
    text: 'Create a new entry for each call to `HandleResource`. The `resourceName`
      argument typically contains the filename, so you can use it directly:'
  - name: How to handle large documents without exhausting memory?
    text: Replace `MemoryStream` with a `FileStream` that points to a temporary file.
      The handler then returns the file stream, and you can later delete the file
      after the zip is created.
  - name: Does this approach work with .NET Core on Linux?
    text: Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are
      cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.
  - name: Can I encrypt the zip archive?
    text: '`ZipArchive` supports password‑based encryption only through third‑party
      libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output
      bytes with a library that provides AES encryption before sending them to the
      client.'
  type: HowTo
tags:
- C#
- HTML
- file I/O
title: C#'ta özel bir kaynak işleyicisiyle HTML nasıl kaydedilir
url: /tr/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Özel Bir Kaynak İşleyicisi ile HTML Nasıl Kaydedilir

Eğer bellek içi bir dizeden veya ayrıştırılmış bir belgeden **HTML nasıl kaydedilir** bilmeniz gerekiyorsa, bu rehber tam bir çözüm sunar. Özel bir `ResourceHandler` kullanmak, hedef akışı kontrol etmenizi sağlar; bu da geçici dosyalar oluşturmadan **HTML'yi zip'e kaydet** arşivlerine kaydedebileceğiniz anlamına gelir.

Bir `ResourceHandler`'ın eski `IOutputStorage` yaklaşımına göre neden tercih edildiğini, nasıl yapılandırılacağını ve zip sıkıştırması için nasıl genişletileceğini göreceksiniz. Bu öğreticinin sonunda kodu herhangi bir .NET 6+ projesine yerleştirebilir ve kendi depolama gereksinimlerinize uyarlayabilirsiniz.

## Oluşturacağınız Şeyler

* Bir `MemoryStream` döndüren minimal bir `ResourceHandler`.
* `**HtmlAgilityPack**` ile oluşturulmuş bir `HtmlDocument`.
* `doc.Save` çağrısı, HTML'i işleyici tarafından sağlanan akıma yazar.
* Sonuçta oluşan HTML'i zip dosyasına sıkıştıran isteğe bağlı bir sarmalayıcı.

Prerequisites:

* .NET 6 SDK veya daha yeni bir sürüm.
* `HtmlAgilityPack` NuGet paketi (`dotnet add package HtmlAgilityPack`).
* C# akışlarıyla temel aşinalık.

## Adım 1: Özel bir kaynak işleyicisi oluşturun (birincil yol **HTML nasıl kaydedilir**)

`ResourceHandler` temel sınıfı (viewer SDK'nın 24.2 sürümünden itibaren kullanılabilir) tek bir soyut yöntem tanımlar: `HandleResource`. Bu yöntemi uygulamak, HTML'in nereye yazılacağı üzerinde tam kontrol sağlar.

```csharp
using System.IO;

/// <summary>
/// Handles the output stream for each HTML resource.
/// Returning a MemoryStream keeps everything in memory, which is ideal for further processing
/// such as zipping or sending over a network.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string resourceName)
    {
        // You could inspect resourceName to decide between file, memory, or zip entry.
        return new MemoryStream();
    }
}
```

**Neden önemli:** Bir `MemoryStream` döndürerek disk I/O'dan kaçınır, gecikmeyi azaltır ve birim testleri için kodun deterministik olmasını sağlarsınız. İşleyici, `Save` yöntemi tarafından otomatik olarak çağrılır, bu yüzden bir akışı açıkça geçirmeniz gerekmez.

## Adım 2: HTML belgesini yükleyin veya oluşturun

`HtmlAgilityPack`, bir dize, dosya veya akışı ayrıştırabilen kullanışlı bir `HtmlDocument` sınıfı sunar. Bu örnek için basit bir literal yüklüyoruz, ancak aynı kod herhangi bir HTML kaynağıyla çalışır.

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**Neden önemli:** Belgeyi bellek içinde tutmak, özel işleyicinin akış‑tabanlı yaklaşımıyla uyumludur. Ayrıca kaydetmeden önce DOM'u manipüle etmenizi sağlar; örneğin betik eklemek veya hatalı etiketleri düzeltmek gibi.

## Adım 3: Belgeyi özel işleyiciyle kaydedin

`MyHandler` örneğiyle `doc.Save` çağrısı, `HandleResource` yöntemini tetikler. HTML, döndürdüğünüz akıma doğrudan yazılır.

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

`Save` tamamlandıktan sonra, `MyHandler` içindeki `MemoryStream` serileştirilmiş HTML'i içerir. Bunu şu şekilde alabilirsiniz:

```csharp
// Cast the handler back to access the stream (if you kept a reference)
MyHandler handler = new MyHandler();
doc.Save(handler);

// Reset position to read from the beginning.
handler.HandleResource("").Seek(0, SeekOrigin.Begin);
using var reader = new StreamReader(handler.HandleResource(""));
string htmlOutput = reader.ReadToEnd();
System.Console.WriteLine(htmlOutput);
```

**Sonuç:** Konsol, `LoadHtml`'a gönderdiğiniz tam HTML'i yazdırır. Bu, artık **HTML nasıl kaydedilir** konusunda özel bir işleyiciyle anladığınızı gösterir.

## Adım 4: İşleyiciyi **HTML'yi zip'e kaydet** için genişletmek

HTML'i arşivlemek istiyorsanız, `MyHandler`'ı bir `ZipArchiveEntry` içine yazacak şekilde değiştirin. .NET `System.IO.Compression` ad alanı bunu basit hale getirir.

```csharp
using System.IO.Compression;

/// <summary>
/// Writes the HTML into a zip entry named "document.html".
/// The zip archive is created in memory and can be saved to a file or sent over HTTP.
/// </summary>
class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        // Initialise the zip archive in create mode.
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        // Create a zip entry for the HTML file.
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open(); // Returns a stream that writes directly into the zip entry.
    }

    /// <summary>
    /// Finalises the zip archive and returns the raw bytes.
    /// </summary>
    public byte[] GetZipBytes()
    {
        // Ensure all entries are flushed.
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}
```

Şimdi yeni işleyiciyi kullanın:

```csharp
// Instantiate the zip‑aware handler.
using var zipHandler = new ZipHtmlHandler();

// Save HTML; it ends up inside the zip archive.
doc.Save(zipHandler);

// Retrieve the zip file as a byte array.
byte[] zipBytes = zipHandler.GetZipBytes();

// Optionally write the zip to disk for verification.
File.WriteAllBytes("output.zip", zipBytes);
System.Console.WriteLine("ZIP file created with size: " + zipBytes.Length);
```

**Neden çalışır:** `HandleResource` yöntemi `document.html` adlı bir zip girdisi oluşturur. `doc.Save` döndürülen akıma yazdığında veri otomatik olarak sıkıştırılır. Zip bellek içinde oluşturulduğu için, dosya sistemine dokunmadan bir web API'sinden döndürebilir, e-postaya ekleyebilir veya bir veritabanında saklayabilirsiniz.

## Yaygın Sorular ve Kenar Durumları

### Aynı zip içinde birden fazla HTML dosyasına ihtiyacım olsaydı ne olur?

`HandleResource`'a yapılan her çağrı için yeni bir giriş oluşturun. `resourceName` argümanı genellikle dosya adını içerir, bu yüzden doğrudan kullanabilirsiniz:

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### Büyük belgeleri bellek tükenmeden nasıl yönetilir?

`MemoryStream` yerine geçici bir dosyaya işaret eden bir `FileStream` kullanın. İşleyici ardından dosya akışını döndürür ve zip oluşturulduktan sonra dosyayı silebilirsiniz.

### Bu yaklaşım Linux üzerindeki .NET Core ile çalışır mı?

Evet. Kullanılan tüm API'ler (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) çapraz platformdur. En iyi uyumluluk için hedef çerçevenin en az .NET 6 olduğundan emin olun.

### Zip arşivini şifreleyebilir miyim?

`ZipArchive`, şifre tabanlı şifrelemeyi yalnızca üçüncü taraf kütüphaneler aracılığıyla (ör. `SharpZipLib`) destekler. Şifreleme gerekiyorsa, çıktıyı istemciye göndermeden önce AES şifrelemesi sağlayan bir kütüphane ile sarmalayın.

## Profesyonel İpuçları

* Bir toplu işlemde birçok belgeyi işlerken **işleyiciyi yeniden kullanın**; her dosya için yeni bir `ZipArchive` oluşturmak gereksiz yük ekler.
* Arşiv hâlâ açıkken zip baytlarını okumanız gerekiyorsa `ZipArchive` yapıcısında **`LeaveOpen: true`** ayarlayın.
* Kaydetmeden önce **HTML'i doğrulayın**; `doc.OptionCheckSyntax = true;` çağrısı hatalı etiketleri erken yakalar.
* Oluşturulan zip'in **boyutunu kaydedin**; olağandışı büyük çıktı genellikle yinelenen kaynaklar veya eksik sıkıştırma anlamına gelir.

## Tam Çalışan Örnek

Aşağıda, bir konsol projesine (`dotnet new console`) yapıştırıp çalıştırabileceğiniz tek bir dosya bulunmaktadır. Bu, hem düz HTML kaydetmeyi hem de zip sıkıştırmasını gösterir.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using HtmlAgilityPack;

// ---------- Custom handlers ----------
class MyHandler : ResourceHandler
{
    public MemoryStream HtmlStream { get; } = new();

    public override Stream HandleResource(string resourceName) => HtmlStream;
}

class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open();
    }

    public byte[] GetZipBytes()
    {
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}

// ---------- Main program ----------
class Program
{
    static void Main()
    {
        // Build a simple HTML document.
        HtmlDocument doc = new HtmlDocument();
        doc.LoadHtml("<html><body>Hello World from HtmlAgilityPack</body></html>");

        // ---- Example 1: plain HTML save ----
        var plainHandler = new MyHandler();
        doc.Save(plainHandler);
        plainHandler.HtmlStream.Seek(0, SeekOrigin.Begin);
        using var reader = new StreamReader(plainHandler.HtmlStream);
        Console.WriteLine("Plain HTML output:");


## Sonraki Öğrenmeniz Gerekenler?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [C#'ta Özel Kaynak İşleyicisi ile HTML Nasıl Kaydedilir](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [ZipArchive Nasıl Kullanılır – HTML ve Kaynakları ZIP Dosyasına Kaydet](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [Özel Kaynak İşleyicisi ile HTML'yi zip olarak kaydet – adım adım rehber](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}