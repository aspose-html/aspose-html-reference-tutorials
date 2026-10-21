---
category: general
date: 2026-05-06
description: C#'de ZipArchive'i kullanarak HTML'yi ZIP arşivi olarak kaydetme. Aspose.HTML
  ile HTML kaynaklarından C# zip arşivi oluşturmayı öğrenin.
draft: false
keywords:
- how to use ziparchive
- save html as zip
- create zip archive c#
- create zip from html
language: tr
og_description: C#'ta ZipArchive'ı kullanarak bir HTML belgesini ve kaynaklarını tek
  bir ZIP dosyasında birleştirme. Tam kodlu adım adım rehber.
og_title: C#'ta ZipArchive Nasıl Kullanılır – HTML'yi ZIP Olarak Kaydet
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: C#'de ZipArchive Nasıl Kullanılır – HTML'yi ZIP Olarak Kaydet
url: /tr/net/html-extensions-and-conversions/how-to-use-ziparchive-in-c-save-html-as-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta ZipArchive Nasıl Kullanılır – HTML'yi ZIP Olarak Kaydet

HTML sayfasını resimler, CSS ve fontlarla birlikte göndermeniz gerektiğinde C#'ta ZipArchive'i nasıl kullanacağınızı hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok web‑to‑desktop senaryosunda bir sayfayı taşımak için en kolay yol, her şeyi bir ZIP dosyasına paketlemektir.  

Bu öğreticide Aspose.HTML ve özel bir `ResourceHandler` kullanarak **HTML'yi zip olarak kaydetmeyi** adım adım göstereceğiz. Sonunda, her bağlı kaynağı otomatik olarak yakalayan zip arşiv c# projelerini nasıl oluşturacağınızı tam olarak öğrenecek ve kendi kod tabanınıza ekleyebileceğiniz eksiksiz, çalıştırılabilir bir örnek elde edeceksiniz.

## Oluşturacağınız Şey

- Mevcut bir `input.html` dosyasını yükleyin.
- Belge kaydedilirken her dış kaynağı (resimler, stil sayfaları, fontlar) yakalayın.
- Her kaynağı doğrudan bir `ZipArchive` girdisine yazın, böylece son dosya düzenli bir `output.zip` olur.
- ZIP'in beklenen klasör yapısını içerdiğini doğrulayın.

Ek bir üçüncü‑taraf zip kütüphanesine gerek yok—sadece yerleşik `System.IO.Compression` ad alanı ve Aspose.HTML yeterlidir.

## Önkoşullar

- .NET 6.0 veya daha yenisi (kod .NET Framework 4.8'de de çalışır).
- Aspose.HTML for .NET (ücretsiz deneme veya lisanslı sürüm). NuGet üzerinden kurun: `dotnet add package Aspose.HTML`.
- C# dosya I/O ve akışları konusunda temel bilgi.

Eğer bunlara sahipseniz, hemen başlayalım.

![ziparchive kullanımı diyagramı](image.png "HTML → ZipArchive akışını gösteren diyagram – ziparchive nasıl kullanılır")

## Adım 1: Özel Bir ResourceHandler Oluşturun

Aspose.HTML, yazması gereken her dış dosya için `ResourceHandler.HandleResource` metodunu çağırır. Bu metodu geçersiz kılarak, renderlayıcıya doğrudan bir ZIP girdisine işaret eden bir akış verebiliriz.

```csharp
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Rendering;

/// <summary>
/// Writes each HTML resource (image, CSS, font) into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(Stream zipStream)
    {
        // Open the archive for updating; leaveOpen keeps the underlying stream alive.
        _zipArchive = new ZipArchive(zipStream, ZipArchiveMode.Update, leaveOpen: true);
    }

    public override Stream HandleResource(ResourceInfo info)
    {
        // The URI's AbsolutePath contains the file name (e.g., "/images/logo.png").
        // Trim the leading slash so the entry appears at the root of the zip.
        var entryName = info.Uri.AbsolutePath.TrimStart('/');
        var entry = _zipArchive.CreateEntry(entryName, CompressionLevel.Optimal);

        // Return the entry's stream; Aspose will write the content straight into it.
        return entry.Open();
    }
}
```

**Neden özel bir handler?**  
Olmasaydı, Aspose.HTML her kaynağı diskte geçici bir dosyaya yazar, ardından tüm dosyaları kendiniz bir ZIP'e kopyalamanız gerekir. Bu handler ara adımı ortadan kaldırır, I/O'yu azaltır ve kodu düzenli tutar.

## Adım 2: HTML Belgesini Yükleyin

Şimdi sadece kaynak dosyayı yüklüyoruz. Aspose.HTML hem yerel yolları hem de URL'leri destekler, bu yüzden isterseniz uzak bir sayfaya da işaret edebilirsiniz.

```csharp
// Replace with the folder where your HTML lives.
string inputPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// The HTMLDocument constructor reads the file and parses it.
var document = new HTMLDocument(inputPath);
```

**Pro ipucu:** HTML'niz göreceli URL'lerle kaynaklara referans veriyorsa, `input.html` dosyasının bu varlıkların yanında bulunduğundan emin olun. `ResourceHandler`, Aspose'un çözdüğü tam yolları alacaktır.

## Adım 3: ZipResourceHandler'ı Bağlayın ve Kaydedin

Belge hazır ve handler tanımlandıktan sonra, çıktı ZIP'i için bir `FileStream` açar, handler'ı örnekler ve `document.Save` metodunu çağırırız. Kaydetme işlemi, her dış dosya için `HandleResource`'u tetikler.

```csharp
// The final ZIP will be placed in the same directory.
string zipPath = Path.Combine("YOUR_DIRECTORY", "output.zip");

// Open a FileStream for the zip – FileMode.Create overwrites any existing file.
using (var zipStream = new FileStream(zipPath, FileMode.Create))
{
    var zipHandler = new ZipResourceHandler(zipStream);

    // Save the HTML document; the handler captures all linked resources.
    document.Save(zipHandler);
}
```

`Save` tamamlandığında, `output.zip` şunları içerir:

```
/index.html          (the original HTML file)
/styles/main.css
/images/logo.png
/fonts/open-sans.ttf
...
```

ZIP'i herhangi bir arşiv yöneticisiyle açarak yapıyı doğrulayabilirsiniz.

## Adım 4: Sonucu Doğrulayın (İsteğe Bağlı)

Hızlı bir tutarlılık kontrolü, ileride ortaya çıkabilecek gizemli eksik‑resim hatalarından sizi korur.

```csharp
using (var archive = ZipFile.OpenRead(zipPath))
{
    Console.WriteLine("Entries in the ZIP:");
    foreach (var entry in archive.Entries)
    {
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
    }
}
```

Bu kod parçasını çalıştırmak her dosya adını yazdırır ve **create zip from html** sürecinin başarılı olduğunu onaylar.

## Yaygın Kenar Durumları ve Nasıl Ele Alınır

| Durum | Dikkat Edilmesi Gereken | Önerilen Çözüm |
|-----------|-------------------|---------------|
| **Mutlak URL'ler** (ör. `https://example.com/img.png`) | Aspose kaynağı indirmeye çalışır; handler geçici bir dosyaya işaret eden bir akış alır. | Makinenizin internet erişimi olduğundan emin olun veya varlıkları önceden indirin ve HTML'yi yerel yolları kullanacak şekilde yeniden yazın. |
| **Aynı Dosya Adları** (farklı klasörlerde aynı ada sahip iki `logo.png` resmi) | ZIP girdileri benzersiz yollara sahip olmalıdır; aksi takdirde ikinci giriş birincisini üzerine yazar. | Girdi adında klasör hiyerarşisini koruyun (`info.Uri.AbsolutePath.TrimStart('/')`). |
| **Büyük Kaynaklar** (megabayt‑boyutunda videolar) | Doğrudan bir zip girdisine yazmak uygundur, ancak zaten sıkıştırılmış medya için `CompressionLevel.NoCompression` ayarlamak isteyebilirsiniz. | Bilinen medya türleri için `CreateEntry(entryName, CompressionLevel.NoCompression)` ayarlamasını yapın. |
| **Desteklenmeyen Formatlar** (ör. dış fontlarla SVG) | Bazı kaynaklar, Aspose'un otomatik olarak çözmediği ek dosyalara referans verebilir. | `Save` çağrısından sonra bu dosyaları manuel olarak ZIP'e ekleyin. |

## Üretim‑Hazır Kod İçin İpuçları

- **Doğru şekilde dispose edin** – Hem `ZipArchive` hem de `HTMLDocument` `IDisposable` uygular. Gösterildiği gibi, yerel kaynakları serbest bırakmak için onları `using` blokları içinde sarın.
- **İş parçacığı güvenliği** – Handler iş parçacığı güvenli değildir; aynı `ZipResourceHandler` örneğini birden fazla iş parçacığından kullanmaktan kaçının.
- **Performans** – Büyük HTML paketleri için, HTML'i doğrudan ZIP'e akıtmayı düşünün (`zipArchive.CreateEntry("index.html").Open()`), ardından `document.Save(stream)` çağrısını yapın; burada `stream` o girdinin akışıdır.

## Tam Çalışan Örnek

Aşağıda, bir konsol uygulamasına kopyalayıp yapıştırabileceğiniz tam program bulunmaktadır. Tüm `using` yönergeleri, hata yönetimi ve yorumları içerir.

```csharp
// ------------------------------------------------------------
// How to Use ZipArchive in C# – Save HTML as ZIP (Full Demo)
// ------------------------------------------------------------
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Rendering;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(Stream zipStream)
    {
        _zipArchive = new ZipArchive(zipStream, ZipArchiveMode.Update, leaveOpen: true);
    }

    public override Stream HandleResource(ResourceInfo info)
    {
        var entryName = info.Uri.AbsolutePath.TrimStart('/');
        var entry = _zipArchive.CreateEntry(entryName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Paths – adjust to your environment.
            string baseDir = Path.Combine(Environment.CurrentDirectory, "DemoFiles");
            string htmlPath = Path.Combine(baseDir, "input.html");
            string zipPath  = Path.Combine(baseDir, "output.zip");

            // 2️⃣ Load the HTML document.
            var document = new HTMLDocument(htmlPath);

            // 3️⃣ Open the ZIP stream and save.
            using (var zipStream = new FileStream(zipPath, FileMode.Create))
            {
                var zipHandler = new ZipResourceHandler(zipStream);
                document.Save(zipHandler);
            }

            // 4️⃣ Quick verification.
            Console.WriteLine($"ZIP created at: {zipPath}");
            using (var archive = ZipFile.OpenRead(zipPath))
            {
                Console.WriteLine("Contents:");
                foreach (var entry in archive.Entries)
                    Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

`dotnet run` (veya tercih ettiğiniz IDE) ile derleyin ve `output.zip` dosyasını açın. Orijinal HTML'i ve referans verilen tüm varlıkları düzenli bir şekilde paketlenmiş olarak görmelisiniz. Bu, **create zip archive c#** iş akışının tam olarak çalışmasıdır.

## Sonuç

Şimdiye kadar **ZipArchive'i nasıl kullanacağınızı** **HTML'yi zip olarak kaydetmek** için gösterdik ve Aspose.HTML'in `ResourceHandler`'ını kullanarak **create zip from html** için temiz bir yol sunduk. Önemli çıkarımlar şunlardır:

- `ResourceHandler`'ı geçersiz kılarak kaynakları doğrudan bir `ZipArchive` içine akıtın.
- ZIP'i tüm kaydetme işlemi boyunca açık tutun (`leaveOpen: true`).
- Çıktıyı doğrulayın ve mutlak URL'ler veya yinelenen adlar gibi kenar durumlarını ele alın.

Artık bu deseni web‑to‑desktop dışa aktarıcılarına, çevrim dışı dokümantasyon oluşturucularına veya bir HTML sayfasını varlıklarıyla birlikte paketlemenin gerektiği herhangi bir senaryoya entegre edebilirsiniz.  
Daha ileri gitmek ister misiniz? Birden fazla HTML sayfasını tek bir arşive sıkıştırmayı deneyin veya tüm girdileri listeleyen bir manifest dosyası ekleyin. Ayrıca şifrelemeyi de keşfedebilirsiniz.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}