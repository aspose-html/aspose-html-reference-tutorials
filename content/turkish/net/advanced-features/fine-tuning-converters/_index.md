---
title: Aspose.HTML ile .NET'te Dönüştürücülerin İnce Ayarı
linktitle: .NET'te Dönüştürücülerin İnce Ayarı
second_title: Aspose.HTML .NET HTML işleme API'si
description: Aspose.HTML for .NET ile HTML'yi PDF'ye, XPS'ye ve görsellere nasıl dönüştüreceğinizi öğrenin. Kod örnekleri ve SSS içeren adım adım eğitim.
type: docs
weight: 16
url: /tr/net/advanced-features/fine-tuning-converters/
---

## giriiş

Aspose.HTML for .NET, geliştiricilerin çeşitli formatlardaki HTML belgelerini değiştirmesine ve dönüştürmesine olanak tanıyan güçlü bir kütüphanedir. HTML'yi PDF'ye, XPS'ye veya görüntülere dönüştürmeniz veya HTML ile ilgili diğer görevleri gerçekleştirmeniz gerekiyorsa, Aspose.HTML işinizi tamamlamanıza yardımcı olacak güçlü bir araç seti sunar.

Bu eğitimde Aspose.HTML for .NET'in bazı temel özelliklerini inceleyeceğiz ve her örnek için adım adım açıklamalar sunacağız. Bu eğitimin sonunda Aspose.HTML for .NET'i .NET uygulamalarınızda nasıl kullanacağınız konusunda sağlam bir anlayışa sahip olacaksınız.

## Önkoşullar

Örneklere dalmadan önce aşağıdaki önkoşulların mevcut olduğundan emin olun:

-  Aspose.HTML for .NET: Aspose.HTML for .NET kütüphanesinin kurulu olması gerekir. adresinden indirebilirsiniz.[İndirme: {link](https://releases.aspose.com/html/net/).

- Geçici Lisans (İsteğe Bağlı): Geçerli bir lisansınız yoksa, geçici lisansı adresinden alabilirsiniz.[Burada](https://purchase.aspose.com/temporary-license/).

Şimdi Aspose.HTML for .NET'in bazı yaygın kullanım örneklerini inceleyelim.

## Ad Alanlarını İçe Aktar

C# kodunuzda gerekli ad alanlarını içe aktararak başlayın:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## HTML'yi PDF'ye dönüştür

### Adım 1: HTML Kodunu Hazırlayın

```csharp
var code = @"<span>Hello World!!</span>";
```

### Adım 2: HTML Belgesini Başlatın

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Adım 3: PDF Aygıtı Oluşturun ve Çıktı Dosyasını Belirleyin

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Adım 4: HTML'yi PDF'ye dönüştürün

```csharp
document.RenderTo(device);
```

Bu örnek, bir HTML pasajını PDF belgesine dönüştürür. HTML kodunu ve çıktı dosyasını gerektiği gibi özelleştirebilirsiniz.

## Özel Sayfa Boyutunu Ayarla

### Adım 1: HTML Kodunu Hazırlayın

```csharp
var code = @"<span>Hello World!!</span>";
```

### Adım 2: HTML Belgesini Başlatın

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 3. Adım: PDF Oluşturma Seçenekleri Oluşturun

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### Adım 4: PDF Aygıtı Oluşturun ve Seçenekleri ve Çıktı Dosyasını Belirleyin

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Adım 5: HTML'yi PDF'ye dönüştürün

```csharp
document.RenderTo(device);
```

Bu örnek, ortaya çıkan PDF belgesi için özel sayfa boyutunun nasıl ayarlanacağını gösterir.

## Çözünürlüğü Ayarla

### Adım 1: HTML Kodunu Hazırlayın ve Dosyaya Kaydedin

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Adım 2: HTML Belgesini Başlatın

```csharp
using (var document = new HTMLDocument("document.html"))
```

### 3. Adım: Düşük Çözünürlük için PDF Oluşturma Seçenekleri Oluşturun

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### Adım 4: PDF Aygıtı Oluşturun ve Düşük Çözünürlük için Seçenekleri ve Çıktı Dosyasını Belirleyin

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Adım 5: Düşük Çözünürlük için HTML'yi PDF'ye Dönüştürün

```csharp
document.RenderTo(device);
```

### Adım 6: Yüksek Çözünürlük için PDF Oluşturma Seçenekleri Oluşturun

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### Adım 7: PDF Aygıtı Oluşturun ve Yüksek Çözünürlük için Seçenekleri ve Çıktı Dosyasını Belirleyin

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Adım 8: Yüksek Çözünürlük için HTML'yi PDF'ye Dönüştürün

```csharp
document.RenderTo(device);
```

Bu örnek, hem düşük hem de yüksek çözünürlüklü ekranlar dikkate alınarak HTML'yi PDF'ye dönüştürürken çözünürlüğün nasıl ayarlanacağını gösterir.

## Arka Plan Rengini Belirtin

### Adım 1: HTML Kodunu Hazırlayın ve Dosyaya Kaydedin

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Adım 2: HTML Belgesini Başlatın

```csharp
using (var document = new HTMLDocument("document.html"))
```

### 3. Adım: PDF Oluşturma Seçeneklerini Arka Plan Rengiyle Başlatın

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### Adım 4: PDF Aygıtı Oluşturun ve Seçenekleri ve Çıktı Dosyasını Belirleyin

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Adım 5: HTML'yi PDF'ye dönüştürün

```csharp
document.RenderTo(device);
```

Bu örnek, HTML'yi PDF'ye dönüştürürken arka plan renginin nasıl belirleneceğini gösterir.

## Sol ve Sağ Sayfa Boyutlarını Ayarla

### Adım 1: HTML Kodunu Hazırlayın

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### Adım 2: HTML Belgesini Başlatın

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 3. Adım: Sol ve Sağ Sayfa Boyutlarıyla PDF Oluşturma Seçenekleri Oluşturun

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### Adım 4: PDF Aygıtı Oluşturun ve Seçenekleri ve Çıktı Dosyasını Belirleyin

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Adım 5: HTML'yi PDF'ye dönüştürün

```csharp
document.RenderTo(device);
```

Bu örnek, HTML'yi PDF'ye dönüştürürken sol ve sağ sayfalar için farklı sayfa boyutlarının nasıl ayarlanacağını gösterir.

## Sayfa Boyutunu İçeriğe Göre Ayarlayın

### Adım 1: HTML Kodunu Hazırlayın

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### Adım 2: HTML Belgesini Başlatın

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 3. Adım: PDF Oluşturma Seçenekleri Oluşturun

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Adım 4: PDF Aygıtı Oluşturun ve Seçenekleri ve Çıktı Dosyasını Belirleyin

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Adım 5: HTML'yi PDF'ye dönüştürün

```csharp
document.RenderTo(device);
```

Bu örnek, HTML'yi PDF'ye dönüştürürken sayfa boyutunun en geniş içeriğe nasıl ayarlanacağını gösterir.

## PDF İzinlerini Belirleyin

### Adım 1: HTML Kodunu Hazırlayın

```csharp
var code = @"<div>Hello World!!</div>";
```

### Adım 2: HTML Belgesini Başlatın

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 3. Adım: İzinlerle PDF Oluşturma Seçenekleri Oluşturun

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### Adım 4: PDF Aygıtı Oluşturun ve Seçenekleri ve Çıktı Dosyasını Belirleyin

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Adım 5: HTML'yi PDF'ye dönüştürün

```csharp
document.RenderTo(device);
```

Bu örnek, HTML'yi korumalı bir PDF'ye dönüştürürken izinlerin ve şifrelemenin nasıl belirleneceğini gösterir.

## Resme Özel Seçenekleri Belirleyin

### Adım 1: HTML Kodunu Hazırlayın

```csharp
var code = @"<div>Hello World!!</div>";
```

### Adım 2: HTML Belgesini Başlatın

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 3. Adım: Görüntü Oluşturma Seçenekleri Oluşturun

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Adım 4: Görüntü Aygıtı Oluşturun ve Seçenekleri ve Çıktı Dosyasını Belirleyin

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Adım 5: HTML'yi Resme Dönüştürün

```csharp
document.RenderTo(device);
```

Bu örnek, HTML'nin format, çözünürlük ve yumuşatma modu gibi belirli işleme seçenekleriyle bir görüntüye nasıl dönüştürüleceğini gösterir.

## XPS İşleme Seçeneklerini Belirtin

### Adım 1: HTML Kodunu Hazırlayın

```csharp
var code = @"<span>Hello World!!</span>";
```

### Adım 2: HTML Belgesini Başlatın

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 3. Adım: Sayfa Boyutuyla XPS İşleme Seçenekleri Oluşturun

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### Adım 4: XPS Aygıtı Oluşturun ve Seçenekleri ve Çıktı Dosyasını Belirleyin

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### Adım 5: HTML'yi XPS'ye dönüştürün

```csharp
document.RenderTo(device);
```

Bu örnek, özel sayfa boyutu ve işleme seçenekleriyle HTML'nin XPS'ye nasıl dönüştürüleceğini gösterir.

## Birden Çok HTML Belgesini PDF'de Birleştirin

### Adım 1: Birden Çok Belge için HTML Kodunu Hazırlayın

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### Adım 2: Birleştirilecek HTML Belgeleri Oluşturun

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### 3. Adım: HTML Oluşturucuyu Başlatın

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### 4. Adım: Birleştirilmiş Çıktı için PDF Aygıtı Oluşturun

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Adım 5: HTML Belgelerini PDF'ye Birleştirin

```csharp
renderer.Render(device, document1, document2, document3);
```

Bu örnek, Aspose.HTML for .NET kullanılarak birden fazla HTML belgesinin tek bir PDF dosyasında nasıl birleştirileceğini gösterir.

## İşleme Zaman Aşımını Ayarla

### Adım 1: HTML Kodunu JavaScript ile Hazırlayın

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### Adım 2: HTML Belgesini Başlatın

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 3. Adım: HTML Oluşturucuyu Başlatın

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### 4. Adım: PDF Aygıtı Oluşturun ve İşleme Zaman Aşımını Ayarlayın

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Adım 5: HTML'yi Zaman Aşımı ile PDF'ye Dönüştürün

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

Bu örnek, HTML'yi PDF'ye dönüştürürken oluşturma zaman aşımının nasıl ayarlanacağını gösterir; bu, dinamik içerikle veya uzun süre çalışan komut dosyalarıyla çalışırken yararlı olabilir.

## Çözüm

Aspose.HTML for .NET, geliştiricilerin HTML belgeleriyle verimli bir şekilde çalışmasını sağlayan çok yönlü bir kitaplıktır. Bu eğitimde, temel HTML'den PDF dönüştürmelerine, özel sayfa boyutları, çözünürlükler ve izinler gibi daha gelişmiş özelliklere kadar çeşitli örnekleri ele aldık. Bu örnekleri takip ederek .NET uygulamalarınızda Aspose.HTML for .NET'in tüm potansiyelinden yararlanabilirsiniz.

 Herhangi bir sorunuz varsa veya daha fazla yardıma ihtiyacınız varsa, şu adresi ziyaret etmekten çekinmeyin:[Aspose.HTML Forumu](https://forum.aspose.com/) destek ve rehberlik için.

## SSS'ler

### S1. .NET için Aspose.HTML nedir?
   
Cevap1: Aspose.HTML for .NET, geliştiricilerin HTML belgelerini programlı olarak değiştirmesine ve dönüştürmesine olanak tanıyan bir .NET kitaplığıdır. HTML'den PDF'ye, XPS'ye ve görüntü dönüştürmenin yanı sıra gelişmiş oluşturma seçenekleri de dahil olmak üzere HTML içeriğiyle çalışmak için çok çeşitli özellikler sunar.

### Q2. Aspose.HTML for .NET'i nereden indirebilirim?

 Cevap2: Aspose.HTML for .NET'i şu adresten indirebilirsiniz:[İndirme: {link](https://releases.aspose.com/html/net/).

### S3. Aspose.HTML for .NET'i kullanmak için lisansa ihtiyacım var mı?

Cevap3: Aspose.HTML for .NET'i lisans olmadan kullanabilirsiniz ancak tüm özelliklerin kilidini açmak ve filigranları veya sınırlamaları kaldırmak için üretimde kullanım için bir lisans almanız önerilir.

### S4. Aspose.HTML for .NET ile oluşturulan PDF dosyalarımı nasıl koruyabilirim?

Cevap4: Aspose.HTML for .NET kullanarak HTML'yi PDF'ye dönüştürürken PDF izinlerini ve şifreleme ayarlarını belirleyebilirsiniz. Bu, ortaya çıkan PDF dosyalarına kimlerin erişebileceğini ve bunları değiştirebileceğini kontrol etmenize olanak tanır.

### S5. HTML'yi XPS veya görseller gibi diğer formatlara dönüştürebilir miyim?

Cevap5: Evet, Aspose.HTML for .NET, HTML'yi PDF, XPS ve görseller (örn. JPEG) dahil olmak üzere çeşitli formatlara dönüştürmeyi destekler. Özel gereksinimlerinizi karşılamak için dönüştürme ayarlarını özelleştirebilirsiniz.