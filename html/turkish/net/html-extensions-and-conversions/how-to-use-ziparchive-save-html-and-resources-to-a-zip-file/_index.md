---
category: general
date: 2026-03-29
description: 'C#''ta ZipArchive''i nasıl kullanacağınızı öğrenin: HTML''yi ZIP''e
  dönüştürme, HTML''yi ZIP''e kaydetme ve HTML görüntülerini sıkıştırma—hepsi tek
  bir net öğreticide.'
draft: false
keywords:
- how to use ziparchive
- convert html to zip
- save html to zip
- create zip archive c#
- compress html images
language: tr
og_description: C#'ta ZipArchive'ı kullanarak HTML'yi ZIP'e dönüştürmeyi, HTML'yi
  ZIP'e kaydetmeyi ve HTML resimlerini sıkıştırmayı, eksiksiz ve çalıştırılabilir
  bir örnekle keşfedin.
og_title: ZipArchive Nasıl Kullanılır – HTML ve Kaynakları ZIP Dosyasına Kaydet
tags:
- C#
- .NET
- Aspose.Html
- ZipArchive
title: ZipArchive Nasıl Kullanılır – HTML ve Kaynakları ZIP Dosyasına Kaydet
url: /tr/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ZipArchive Nasıl Kullanılır – HTML ve Kaynakları ZIP Dosyasına Kaydetme

Hiç **ZipArchive nasıl kullanılır** diye merak ettiniz mi, bir HTML sayfasını resimleri, CSS'i ve diğer varlıklarıyla birlikte bir ZIP dosyasına paketlemek için? Tek başınıza değilsiniz. Birçok geliştirici, özellikle sayfa dış kaynaklara referans verdiğinde, kendine özgü bir HTML paketini dağıtmak zorunda kaldığında bir duvara çarpar. İyi haber? Birkaç C# satırı ve Aspose.HTML ile **HTML'yi ZIP'e dönüştürebilir**, **HTML'yi ZIP'e kaydedebilir** ve hatta **HTML resimlerini sıkıştırabilirsiniz** IDE'nizden çıkmadan.

Bu öğreticide, basit bir `HTMLDocument` oluşturulmasından özel bir `ResourceHandler` aracılığıyla her bağlı kaynağın işlenmesine kadar tüm süreci adım adım inceleyeceğiz. Sonunda, herhangi bir web sunucusuna ya da e‑posta ekine sürükleyebileceğiniz kullanıma hazır bir ZIP dosyanız olacak. Harici betikler yok, manuel kopyalama yok—sadece saf .NET.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

- **.NET 6+** (veya .NET Framework 4.6+). Kullanılan API'ler `System.IO.Compression` içinde.
- **Aspose.HTML for .NET** yüklü (NuGet paketi `Aspose.Html`).
- C# sözdizimi hakkında temel bir anlayış.
- Visual Studio ya da VS Code gibi bir IDE.

Hepsi bu. Ek bir araç, üçüncü‑taraf zip programı gerekmez. Hazır mısınız? Başlayalım.

## Adım 1: Projeyi Kurun ve Bağımlılıkları Ekleyin

Yeni bir konsol projesi oluşturun:

```bash
dotnet new console -n HtmlToZipDemo
cd HtmlToZipDemo
dotnet add package Aspose.Html
```

`Aspose.Html` paketi, daha sonra genişleteceğimiz `HTMLDocument` sınıfını ve `ResourceHandler` temel sınıfını sağlar. Yerleşik `System.IO.Compression` ad alanı ise `ZipArchive` ve `ZipArchiveEntry` öğelerini sunar.

> **Pro tip:** .NET 6 hedefliyorsanız, `Main` metodunu sade tutmak için üst‑seviye ifadeler kullanabilirsiniz. Aşağıdaki kod, açıklık açısından klasik bir `Program` sınıfı kullanıyor.

## Adım 2: Özel Bir Resource Handler Oluşturun

Aspose.HTML bir belgeyi kaydederken, her dış dosya (resimler, CSS, fontlar vb.) için bir `Stream` sağlamasını bir `ResourceHandler` üzerinden ister. `HandleResource` metodunu geçersiz kılarak, her kaynağı doğrudan bir zip girdisine yönlendirebiliriz.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Writes each HTML resource (image, CSS, etc.) directly into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        // Ensure a folder hierarchy inside the zip (optional but tidy)
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open(); // Aspose streams the content into this entry.
    }
}
```

**Neden önemli:** Kaynakları önce diske yazıp ardından zip'lemek yerine, handler bunları doğrudan zip girdisine akıtarak I/O yükünü azaltır ve zip'in HTML içeriğiyle senkron kalmasını garantiler.

## Adım 3: HTML Belgesini Oluşturun

Gösterim amaçlı, `logo.png` adlı harici bir resme referans veren küçük bir HTML parçacığı gömeceğiz. Gerçek bir projede HTML'i bir dosyadan ya da veritabanından okuyabilirsiniz.

```csharp
// Create a simple HTML document with an external image reference.
HTMLDocument htmlDocument = new HTMLDocument(
    "<html><body><h1>Welcome!</h1><img src='logo.png' alt='Demo logo'></body></html>"
);
```

**HTML resimlerini sıkıştırmak** istiyorsanız, resim dosyasının çalıştırılabilir dosyanın yanına (ya da bir kaynak olarak) yerleştirildiğinden emin olun. `ZipResourceHandler` resmi otomatik olarak arşive ekleyecektir.

## Adım 4: ZIP Dosyasını Açın (veya Oluşturun) ve Kaydedin

Şimdi her şeyi birleştirelim. Çıktı zip'i için bir `FileStream` açıyoruz, *Update* modunda bir `ZipArchive` örneği oluşturuyoruz ve özel handler'ımızı `HTMLDocument.Save` metoduna iletiyoruz.

```csharp
using (var fileStream = new FileStream("output.zip", FileMode.Create))
using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
{
    // Initialise the handler with the open ZipArchive.
    var zipHandler = new ZipResourceHandler(zipArchive);

    // Save the HTML document; the handler writes HTML, images, CSS, etc. into the zip.
    htmlDocument.Save(zipHandler);
}
```

`using` blokları sona erdiğinde zip otomatik olarak sonlandırılır ve kapanır. Oluşan `output.zip` şunları içerir:

- `index.html` (serileştirilmiş HTML belgesi)
- `logo.png` (HTML içinde referans verilen resim)

İçeriği herhangi bir dosya gezginiyle zip'i açarak doğrulayabilirsiniz.

## Adım 5: Sonucu Doğrulayın (İsteğe Bağlı)

ZIP'in gerçekten çalıştığını iki kez kontrol etmek her zaman iyidir. Önceki kodun ardından çalıştırabileceğiniz hızlı bir snippet aşağıdadır; girdileri listeler:

```csharp
using (var zip = ZipFile.OpenRead("output.zip"))
{
    Console.WriteLine("Contents of output.zip:");
    foreach (var entry in zip.Entries)
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
}
```

Şuna benzer bir çıktı görmelisiniz:

```
Contents of output.zip:
- index.html (1234 bytes)
- logo.png (45678 bytes)
```

Çıkarılan klasörden `index.html` dosyasını açın; resmin doğru şekilde render edildiğini göreceksiniz—**HTML'yi ZIP'e kaydetme** işleminin başarıyla gerçekleştiğinin kanıtı.

## Ortak Varyasyonlar ve Kenar Durumları

### 1. HTML Dosyası için Farklı Bir Giriş Adı Kullanma

Varsayılan olarak Aspose HTML'i `index.html` olarak yazar. Özel bir ad istiyorsanız, kaydetmeden önce `htmlDocument.FileName` özelliğini ayarlayabilirsiniz:

```csharp
htmlDocument.FileName = "myPage.html";
htmlDocument.Save(zipHandler);
```

### 2. Ek Dosyaları Manuel Olarak Ekleme

Bazen ekstra dosyalar (ör. bir README) eklemek isteyebilirsiniz. `htmlDocument.Save` çağrısından önce bu dosyaları doğrudan `ZipArchive`'e ekleyebilirsiniz:

```csharp
var readme = zipArchive.CreateEntry("README.txt", CompressionLevel.Optimal);
using (var writer = new StreamWriter(readme.Open()))
{
    writer.WriteLine("This ZIP contains an HTML page generated with Aspose.HTML.");
}
```

### 3. Büyük Resimleri Verimli Bir Şekilde İşleme

HTML'iniz çok büyük resimler referans veriyorsa, zip boyutunu makul tutmak için önceden yeniden boyutlandırmayı düşünün. `System.Drawing.Common` paketi bu konuda yardımcı olur:

```csharp
// Example: Resize logo.png to a max width of 800px before zipping.
using (var img = System.Drawing.Image.FromFile("logo.png"))
{
    int maxWidth = 800;
    if (img.Width > maxWidth)
    {
        var ratio = (double)maxWidth / img.Width;
        var newHeight = (int)(img.Height * ratio);
        using var thumb = img.GetThumbnailImage(maxWidth, newHeight, () => false, IntPtr.Zero);
        thumb.Save("logo_resized.png");
    }
}
```

Ardından HTML içinde `<img src='logo_resized.png'>` kullanın.

## Tam, Çalıştırılabilir Örnek

Aşağıda `Program.cs` dosyasına kopyalayıp yapıştırabileceğiniz eksiksiz bir program yer alıyor. Aspose.HTML NuGet paketi yüklü olduğu sürece olduğu gibi derlenip çalışır.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Custom handler that streams each resource into a zip entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Create an HTML document that references an external image.
        HTMLDocument htmlDocument = new HTMLDocument(
            "<html><head><title>Demo</title></head>" +
            "<body><h2>Hello, ZipArchive!</h2>" +
            "<img src='logo.png' alt='Demo logo'></body></html>"
        );

        // 2️⃣ Open (or create) the output zip file.
        using (var fileStream = new FileStream("output.zip", FileMode.Create))
        using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
        {
            // 3️⃣ Initialise the custom handler.
            var zipHandler = new ZipResourceHandler(zipArchive);

            // 4️⃣ Save the HTML; resources get streamed into the zip.
            htmlDocument.Save(zipHandler);
        }

        Console.WriteLine("✅ HTML document and its resources have been saved to output.zip");
    }
}
```

**Beklenen çıktı:** Konsol bir başarı mesajı verir ve proje klasöründe `output.zip` oluşur; içinde `index.html` ve `logo.png` bulunur.

## Sıkça Sorulan Sorular

- **Bu .NET Core'da çalışır mı?**  
  Evet. `System.IO.Compression.ZipArchive` .NET Standard'ın bir parçasıdır, bu yüzden aynı kod .NET 5, .NET 6 ve .NET 7'de çalışır.

- **HTML resimlerini daha agresif bir şekilde **sıkıştırmam** gerekirse ne olur?**  
  Resimleri ZIP'e eklenmeden önce ön işleme tabi tutabilirsiniz (boyutlandırma, formatı WebP'ye değiştirme vb.). Handler sadece aldığı veriyi akış olarak gönderir.

- **ZIP'i şifreleyebilir miyim?**  
  `ZipArchive` yalnızca üçüncü‑taraf kütüphaneler aracılığıyla AES şifrelemeyi destekler (ör. `SharpZipLib`). Şifreleme gerekiyorsa, ZIP'i bu kütüphane ile oluşturup ardından akışı Aspose'a özel bir `ResourceHandler` olarak sağlayabilirsiniz.

- **ZIP içinde kök klasörü ayarlamanın bir yolu var mı?**  
  Evet—`HandleResource` içinde `resourceName`'in önüne bir klasör adı ekleyin, ör. `var entry = _zipArchive.CreateEntry($"site/{resourceName}", ...)`.

## Sonuç

Artık **ZipArchive**'i C# içinde **HTML'yi ZIP'e dönüştürmek**, **HTML'yi ZIP'e kaydetmek** ve **HTML resimlerini sıkıştırmak** için tek bir, temiz iş akışıyla nasıl kullanacağınızı biliyorsunuz. `ResourceHandler`'ı genişleterek geçici dosyalardan kaçındık ve süreç bellek‑verimli oldu. Bu desen ölçeklenebilir: oluşturduğunuz zip'i bir web sunucusuna, e‑posta eki olarak gönderin ya da bulut depolamaya kaydedin.

İleride keşfedebileceğiniz adımlar:

- **Tam site klasörleri için programatik olarak ZIP arşivleri oluşturma** (`create zip archive c#`).
- **ZIP öncesi PDF veya DOCX dönüşümleri** ekleyerek daha zengin dokümantasyon paketleri oluşturma.
- **ASP.NET Core ile bütünleştirme**; zip'i doğrudan istemci tarayıcısına akıtma (`FileStreamResult`).

HTML zipleme, font yönetimi veya resim boyutu optimizasyonu hakkında daha fazla sorunuz mu var? Yorum bırakın ya da Stack Overflow'da bana ulaşın. Mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}