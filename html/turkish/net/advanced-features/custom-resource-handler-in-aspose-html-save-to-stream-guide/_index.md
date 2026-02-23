---
category: general
date: 2026-02-22
description: Özel kaynak işleyicisi, HTML çıktısını yakalamanıza olanak tanır. HTML
  belgesini nasıl yükleyeceğinizi, Aspose HTML kaydetme özelliğini nasıl kullanacağınızı
  ve basit bir C# örneğiyle HTML'yi akışa nasıl kaydedeceğinizi öğrenin.
draft: false
keywords:
- custom resource handler
- load html document
- aspose html save
- save html to stream
- capture html output
language: tr
og_description: Özel bir kaynak işleyicisinin HTML çıktısını nasıl yakaladığını, HTML
  belgesini nasıl yüklediğini ve Aspose HTML'i C#'ta kullanarak HTML'yi akışa nasıl
  kaydettiğini öğrenin.
og_title: Aspose HTML'de Özel Kaynak İşleyicisi – Akışa Kaydetme Kılavuzu
tags:
- aspose-html
- csharp
- streaming
- resource-handler
title: Aspose HTML'de Özel Kaynak İşleyicisi – Akışa Kaydetme Kılavuzu
url: /tr/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Özel Kaynak İşleyici – Aspose HTML ile HTML Çıktısını Yakalama

Hiç **custom resource handler**'a ihtiyacınız oldu mu, Aspose HTML bir dönüşüm sırasında yazdığı her dosyayı yakalamak için? Belki HTML, resimleri veya CSS'i doğrudan diske yazmak yerine belleğe yönlendirmek istediniz. Bu, durum bilgisiz kalması gereken bir web‑servis oluştururken ya da sadece **save HTML to stream** yapmak ve daha sonra işlemek istediğinizde çok yaygın bir senaryodur.

Bu öğreticide, **load HTML document** (HTML belgesini yükleme), bir **custom resource handler** ekleme ve **Aspose HTML save**'i kullanarak her çıktı parçasını bir `MemoryStream` içinde yakalama konusunda tam, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Sonunda sadece “ne”yi değil, her satırın “neden”ini de anlayacak ve herhangi bir C# projesine ekleyebileceğiniz yeniden kullanılabilir bir desen elde edeceksiniz.

> **Neden Önemli?**  
> HTML çıktısını bellekte yakalamak, dosya sistemi I/O'sundan kaçınmanızı, bulut fonksiyonlarındaki gecikmeyi azaltmanızı ve adlandırma, sıkıştırma ya da hatta anlık dönüşümler üzerinde tam kontrol sahibi olmanızı sağlar.

## Gereksinimler

- **.NET 6** veya daha yeni (kod .NET Framework 4.7+ üzerinde de çalışır).  
- **Aspose.HTML for .NET** NuGet paketi (`Aspose.Html`).  
- Referans verebileceğiniz bir klasöre yerleştirilmiş basit bir HTML dosyası (`input.html`).  
- İstediğiniz herhangi bir IDE—Visual Studio, Rider veya C# uzantılarına sahip VS Code.

Ek bir yapılandırma gerekmez; API tüm ağır işleri halleder.

## Adım 1 – Özel Kaynak İşleyicisi Oluşturma

Bu tekniğin kalbi, `Aspose.Html.Rendering.ResourceHandler` sınıfını alt sınıf olarak oluşturmakta. `HandleResource` metodunu geçersiz kılarak her kaynak akışının **where** (nerede) olacağını belirlersiniz. Bizim örneğimizde her istek için yeni bir `MemoryStream` döndürürüz, bu da her CSS, resim veya alt‑HTML parçacığının yalnızca RAM'de yaşadığı anlamına gelir.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

/// <summary>
/// Custom handler that writes every resource to a new MemoryStream.
/// </summary>
class MemoryStreamHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // The ResourceInfo gives you the original URL and MIME type.
        // You could inspect it here to decide whether to skip certain files.
        // For this tutorial we just allocate a fresh stream.
        return new MemoryStream();
    }
}
```

**Pro tip:** Akışları (örneğin daha sonra bir ZIP arşivine yazmak için) takip etmeniz gerekiyorsa, `resourceInfo.Uri` anahtarıyla `Dictionary<string, MemoryStream>` içinde saklayın.

## Adım 2 – HTML Belgesini Yükleme

Herhangi bir şey kaydetmeden önce, bir `HTMLDocument` örneğine **load HTML document** (HTML belgesini yükleme) yapmalısınız. Aspose HTML bir dosya yolu, URL ya da hatta bir dizeden okuyabilir. Burada basitlik açısından yerel bir dosya kullanıyoruz.

```csharp
// Adjust the path to point at your real HTML file.
string htmlPath = Path.Combine(Environment.CurrentDirectory, "input.html");

// Load the source HTML document.
HTMLDocument htmlDocument = new HTMLDocument(htmlPath);
```

HTML'niz dış kaynaklara (resimler, fontlar vb.) referans veriyorsa, temel URI'nın doğru olduğundan emin olun; aksi takdirde işleyici onları bulamaz.

## Adım 3 – Özel İşleyiciyi Örnekleme

Şimdi daha önce tanımladığımız işleyicinin bir örneğini oluşturuyoruz. Karmaşık bir şey yok—sadece sade bir `new`. Bu nesne bir sonraki adımda `Save` metoduna geçirilecek.

```csharp
// Step 3: Instantiate the custom handler.
MemoryStreamHandler resourceHandler = new MemoryStreamHandler();
```

İşleyici yalnızca bellek içinde bulunduğu için dosya izinleri veya disk temizliği konusunda endişelenmenize gerek yok.

## Adım 4 – Aspose HTML Save Kullanarak Belgeyi Kaydetme

**Aspose HTML save** işlemi bir `ResourceHandler` alır. Motor DOM'u dolaşırken ve her bağlı kaynağı çözerken `HandleResource` metodunu çağırır. Bizim uygulamamız bir `MemoryStream` döndürdüğü için her parça RAM'de bulunur.

```csharp
// Step 4: Save the document.
// The handler's HandleResource method will be invoked for each output stream.
htmlDocument.Save(resourceHandler);
```

Bu noktada dönüşüm tamamlanmış olur, ancak akışlar hâlâ bellek içindedir. Şimdi onları okuyabilir, bir veritabanına yazabilir ya da bir API yanıtı olarak döndürebilirsiniz.

## Adım 5 – Yakalanan Akışları Alıp Doğrulama

Her seferinde yeni bir `MemoryStream` döndürdüğümüz için referansları tutmanın bir yoluna ihtiyacımız var. Aşağıda, kaydedildikten sonra her akışı bir sözlükte saklayan önceki işleyicinin hızlı bir uzantısı yer alıyor.

```csharp
class TrackingMemoryStreamHandler : ResourceHandler
{
    public Dictionary<string, MemoryStream> Streams { get; } = new();

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var ms = new MemoryStream();
        Streams[resourceInfo.Uri] = ms;   // Remember the stream by its URI.
        return ms;
    }
}

// Usage:
var trackingHandler = new TrackingMemoryStreamHandler();
htmlDocument.Save(trackingHandler);

// Example: write the main HTML output to console (as text)
if (trackingHandler.Streams.TryGetValue(htmlPath, out var mainStream))
{
    mainStream.Position = 0; // rewind
    using var reader = new StreamReader(mainStream);
    string html = reader.ReadToEnd();
    Console.WriteLine("=== Rendered HTML ===");
    Console.WriteLine(html);
}
```

Bu kodu çalıştırmak, Aspose'un ürettiği son HTML'i yazdıracak ve **capture html output**'un beklendiği gibi çalıştığını onaylayacaktır.

## Kenar Durumları ve Sık Sorulan Sorular

### 1. Belge çok büyük olursa ne olur?

Bellek tüketimi hızla artabilir. Büyük PDF'ler veya yüksek çözünürlüklü çok sayıda resim içeren HTML için, `MemoryStream` yerine doğrudan bir `FileStream` ya da **buffered network stream**'e (tamponlu ağ akışı) akıtmayı düşünün. İşleyici, `resourceInfo.MimeType`'a göre karar verebilir.

### 2. Akışları dispose etmem gerekiyor mu?

Evet. İşlemeyi bitirdikten sonra her `MemoryStream` üzerinde `Dispose()` çağırın (ya da bir `using` bloğunun halletmesine izin verin). Takip örneğinde şu eklemeyi yapabiliriz:

```csharp
foreach (var ms in trackingHandler.Streams.Values)
    ms.Dispose();
```

### 3. Kaydetmeden önce kaynakları yeniden adlandırabilir miyim?

Kesinlikle. `HandleResource` içinde `resourceInfo.Uri`'ye erişiminiz var. Onu yeniden yazabilir, bir ön ek ekleyebilir ya da `null` döndürerek belirli dosyaları atlayabilirsiniz.

```csharp
if (resourceInfo.MimeType.StartsWith("image/"))
    return null; // Skip images completely.
```

### 4. Bu yaklaşım thread‑safe mi?

Tek bir işleyici örneği aynı anda gerçekleşen `Save` çağrıları arasında **paylaşılmamalıdır**. Her dönüşüm için yeni bir işleyici oluşturun veya yeniden kullanmanız gerekiyorsa iç sözlüğü bir kilit (lock) ile koruyun.

## Tam Çalışan Örnek

Aşağıda bir console uygulamasına yapıştırabileceğiniz tam program yer alıyor. HTML dosyasını yüklemekten yakalanan çıktıyı yazdırmaya kadar her şeyi gösteriyor.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;

class TrackingMemoryStreamHandler : ResourceHandler
{
    public Dictionary<string, MemoryStream> Streams { get; } = new();

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var ms = new MemoryStream();
        Streams[resourceInfo.Uri] = ms;
        return ms;
    }
}

class SaveToStreamTutorial
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the HTML document you want to render.
        // -------------------------------------------------
        string htmlPath = Path.Combine(Environment.CurrentDirectory, "input.html");
        if (!File.Exists(htmlPath))
        {
            Console.WriteLine($"Cannot find {htmlPath}");
            return;
        }

        HTMLDocument htmlDocument = new HTMLDocument(htmlPath);

        // -------------------------------------------------
        // Step 2: Create the custom handler that captures streams.
        // -------------------------------------------------
        var handler = new TrackingMemoryStreamHandler();

        // -------------------------------------------------
        // Step 3: Save the document – Aspose will invoke our handler.
        // -------------------------------------------------
        htmlDocument.Save(handler);

        // -------------------------------------------------
        // Step 4: Retrieve the main HTML output and display it.
        // -------------------------------------------------
        if (handler.Streams.TryGetValue(htmlPath, out var mainStream))
        {
            mainStream.Position = 0; // rewind to start
            using var reader = new StreamReader(mainStream);
            string renderedHtml = reader.ReadToEnd();
            Console.WriteLine("=== Rendered HTML Output ===");
            Console.WriteLine(renderedHtml);
        }
        else
        {
            Console.WriteLine("Main HTML stream not found.");
        }

        // -------------------------------------------------
        // Step 5: Clean up.
        // -------------------------------------------------
        foreach (var ms in handler.Streams.Values)
            ms.Dispose();

        Console.WriteLine("All streams disposed. Done.");
    }
}
```

**Beklenen çıktı:** Konsol, tam olarak render edilmiş HTML'i (Aspose'un üretebileceği satır içi CSS dahil) yazdırır ve ardından tüm akışların dispose edildiğine dair bir onay verir.

## Sonuç

Artık Aspose HTML'de **custom resource handler** (özel kaynak işleyicisi) nasıl uygulanır, **load an HTML document** (HTML belgesi nasıl yüklenir) ve **save HTML to stream** (HTML'i akışa kaydetme) yaparak **capturing the HTML output** (HTML çıktısını yakalama) işlemini öğrenmiş oldunuz. Bu desen hafif, thread‑aware (çoklu iş parçacığı farkında) ve tamamen genişletilebilir—`MemoryStream`'i birkaç satır kodla bir dosya, bir ağ soketi veya bir bulut depolama API'si ile değiştirebilirsiniz.

Sonraki adımda şunları keşfedebilirsiniz:

- **Saving to a ZIP archive** (HTML, CSS ve resimleri paketlemek için mükemmel).  
- **Applying transformations** (örneğin, CSS'i anlık olarak küçültmek).  
- **Streaming directly to an HTTP response** in ASP.NET Core (anında indirme için doğrudan HTTP yanıtına akıtma).

Bunları deneyin, ve gerçek dünyadaki senaryolarda özelleştirilmiş bir **custom resource handler**'ın ne kadar güçlü olabileceğini göreceksiniz. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}