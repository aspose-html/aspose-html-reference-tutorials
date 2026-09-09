---
category: general
date: 2025-12-29
description: Aspose.HTML kullanarak C#'ta HTML'yi hızlıca zip'leme – HTML'yi özel
  bir ZipResourceHandler ile zip'e kaydedin. Adım adım öğrenin.
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: tr
og_description: Aspose.HTML kullanarak C#'ta HTML'yi hızlıca zip'lemek nasıl yapılır.
  HTML'yi zip'e kaydetmek ve özel kaynak yönetimiyle bir zip arşivi oluşturmak için
  bu rehberi izleyin.
og_title: C#'ta HTML Nasıl Sıkıştırılır – HTML'yi Zip Dosyasına Kaydet
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: C#'ta HTML Nasıl Zip'lenir – HTML'yi Zip'e Kaydet
url: /tr/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta HTML Nasıl Zip'lenir – HTML'yi Zip'e Kaydet

C#'ta HTML zip'leme, web sayfalarını çevrim dışı kullanım için paketlemek istediğinizde sıkça karşılaşılan bir ihtiyaçtır. Tek bir sayfayı görselleriyle birlikte paketlemek ya da tüm bir siteyi dışa aktarmak isterken, **HTML'yi zip'e kaydetmek** her şeyi düzenli ve taşınabilir tutar. Bu öğreticide, HTML işaretlemesini zip'lemenin yanı sıra, her başvurulan kaynağı doğrudan arşive akıtacak tam, çalıştırılabilir bir çözümü adım adım inceleyeceğiz.

Şunları öğreneceksiniz:

* .NET’in `System.IO.Compression` sınıfı ile programatik olarak zip arşivi oluşturmayı.
* Aspose.HTML’e özel bir `ResourceHandler` ekleyerek kaynakların doğrudan zip içine akmasını.
* Mevcut zip dosyaları ve büyük ikili varlıklar gibi kenar durumlarını yönetmeyi.

Harici bir araç gerektirmez—sadece C#, Aspose.HTML ve birkaç satır kod yeterlidir.

## Gereksinimler

Başlamadan önce şunların kurulu olduğundan emin olun:

* **.NET 6+** (kod .NET Framework 4.6.2 ve üzeri sürümlerde de çalışır).
* **Aspose.HTML for .NET** – Aspose web sitesinden ücretsiz deneme sürümünü alabilir veya lisanslı bir kopya kullanabilirsiniz.
* Bir geliştirme ortamı (Visual Studio, VS Code, Rider—hangisini tercih ederseniz).

Hepsi bu. `System.IO.Compression` (.NET ile birlikte gelir) ve `Aspose.HTML` dışındaki ekstra NuGet paketine ihtiyacınız yok.

## Adım 1: Projeyi ve Kullanım Alanlarını (Imports) Ayarlama

Yeni bir konsol projesi oluşturun (veya kodu mevcut bir projeye ekleyin). Dosyanızın en üstüne gerekli `using` yönergelerini ekleyin:

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **İpucu:** Visual Studio kullanıyorsanız, IDE `Aspose.Html` için eksik NuGet paketini eklemenizi önerecektir. Onayı verin, ardından hazırsınız.

## Adım 2: Özel Bir ZipResourceHandler Uygulama

Aspose.HTML, bir kaynak (görsel, CSS dosyası veya script gibi) yazması gerektiğinde bir `ResourceHandler` çağırır. `HandleResource` metodunu geçersiz kılarak her kaynağın tam olarak nereye konulacağını belirleyebiliriz. Aşağıdaki handler, kaynağın mantıksal yolunu yansıtan bir zip girdisi oluşturur ve bu girdiye doğrudan yazılabilecek bir akış döndürür.

```csharp
/// <summary>
/// Streams each HTML resource straight into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Ensure the entry's directory structure exists inside the zip.
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        // The returned stream writes directly into the zip entry.
        return entry.Open();
    }
}
```

**Neden önemli:**  
Kaynakları geçici bir klasöre yazıp ardından klasörü zip'lemek yerine, bu handler veriyi anında akıtarak disk I/O’sunu azaltır ve bellek kullanımını düşük tutar. Ayrıca zip içindeki klasör hiyerarşisinin HTML’nin göreli yollarıyla aynı olmasını sağlar; bu da sayfayı unzip edip açtığınızda tarayıcının doğru dosyaları bulmasını garantiler.

## Adım 3: Zip Arşivini Hazırlama

Şimdi hedef zip dosyasını açacağız (veya oluşturacağız). `FileMode.Create` bayrağı mevcut dosyayı üzerine yazar—tekrarlanabilir derlemeler için idealdir. Mevcut bir arşivi korumak isterseniz `FileMode.OpenOrCreate` kullanıp yinelenen girdileri ayrı şekilde ele alabilirsiniz.

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **Kenar durumu:** `using` bloğu arşivi dispose etmeden süreç çökerse, bozuk bir zip dosyası oluşabilir. Kodu bir try/catch içinde çalıştırıp hata durumunda kısmen oluşturulmuş dosyayı silmek basit bir önlemdir.

## Adım 4: Gömülü Kaynaklu HTML Belgesi Oluşturma

Örnek olarak, `image.png` adlı bir görsele başvuran küçük bir HTML sayfası oluşturacağız. Gerçek bir senaryoda HTML’i bir dosyadan ya da veritabanından gelen bir stringden yüklerdiniz.

```csharp
// Sample HTML containing an <img> tag.
// Aspose.HTML will ask the ResourceHandler for "image.png".
string htmlContent = @"
<html>
<head><title>Sample Zip</title></head>
<body>
    <h1>Hello, zipped world!</h1>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

// Create the document from the string.
var html = new HTMLDocument(htmlContent);
```

Diskte gerçek görsel dosyalarınız varsa, HTML’i kaydetmeden önce bunları zip’e manuel olarak ekleyebilir ya da Aspose.HTML’in handler aracılığıyla (ör. bir URL’den) almasını sağlayabilirsiniz. Yazdığımız handler hem yerel yollar hem de uzak URL’ler için çalışır.

## Adım 5: ZipResourceHandler Kullanacak Şekilde Kaydetme Seçeneklerini Yapılandırma

Artık Aspose.HTML’in kaynakları yazarken bizim özel handler’ımızı kullanmasını söyleyeceğiz. `HTMLSaveOptions` sınıfı aynı zamanda zip içindeki çıktı dosya adını da belirlemenize izin verir (varsayılan `index.html`’dir).

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## Adım 6: Belgeyi Kaydet – Tüm Veri Zip’e Akıyor

Son olarak `Save` metodunu çağırın. Aspose.HTML işaretlemeyi çözümler, `<img>` etiketini bulur, `image.png` için `HandleResource`’ı çalıştırır ve hem HTML dosyasını hem de görseli aynı zip arşivine yazar.

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

`using` blokları sona erdiğinde `ZipArchive` dosyayı sonlandırır ve dağıtıma hazır hâle getirir.

### Tam Çalışan Örnek

Aşağıda tüm program bir arada verilmiştir. `Program.cs` dosyasına kopyalayıp çalıştırın—başka bir değişiklik yapmanıza gerek yok.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare the zip file.
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);
        using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);

        // 2️⃣ Build a simple HTML document with an image reference.
        string htmlContent = @"
        <html>
        <head><title>Sample Zip</title></head>
        <body>
            <h1>Hello, zipped world!</h1>
            <img src='image.png' alt='Demo image'>
        </body>
        </html>";
        var html = new HTMLDocument(htmlContent);

        // 3️⃣ Set save options to stream resources into the zip.
        var saveOptions = new HTMLSaveOptions
        {
            OutputFileName = "index.html",
            OutputStorage = new ZipResourceHandler(zip)
        };

        // 4️⃣ Save – everything ends up in output.zip.
        html.Save(saveOptions);
        Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
    }
}
```

**Beklenen sonuç:** Çalıştırdıktan sonra `output.zip` içinde iki giriş bulunur:

```
index.html
image.png
```

Dosyayı unzip edip `index.html` dosyasını bir tarayıcıda açtığınızda, göreli yol korunduğu için görsel doğru şekilde görüntülenir.

## Sık Sorulan Sorular

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}