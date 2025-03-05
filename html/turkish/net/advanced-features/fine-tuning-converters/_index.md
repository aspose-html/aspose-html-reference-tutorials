---
title: Aspose.HTML ile .NET'te Dönüştürücülerin İnce Ayarı
linktitle: .NET'te Dönüştürücülerin İnce Ayarı
second_title: Aspose.HTML .NET HTML işleme API'si
description: Aspose.HTML for .NET ile HTML'yi PDF, XPS ve resimlere nasıl dönüştüreceğinizi öğrenin. Kod örnekleri ve SSS içeren adım adım eğitim.
type: docs
weight: 16
url: /tr/net/advanced-features/fine-tuning-converters/
---

## giriiş

.NET için Aspose.HTML, geliştiricilerin çeşitli formatlardaki HTML belgelerini düzenlemesine ve dönüştürmesine olanak tanıyan güçlü bir kütüphanedir. HTML'yi PDF, XPS veya resimlere dönüştürmeniz veya diğer HTML ile ilgili görevleri gerçekleştirmeniz gerekip gerekmediğine bakılmaksızın, Aspose.HTML işinizi yapmanıza yardımcı olacak sağlam bir araç seti sunar.

Bu eğitimde, .NET için Aspose.HTML'nin bazı temel özelliklerini keşfedeceğiz ve her örnek için adım adım açıklamalar sağlayacağız. Bu eğitimin sonunda, .NET uygulamalarınızda .NET için Aspose.HTML'yi nasıl kullanacağınıza dair sağlam bir anlayışa sahip olacaksınız.

## Ön koşullar

Örneklere geçmeden önce aşağıdaki ön koşulların mevcut olduğundan emin olun:

-  .NET için Aspose.HTML: .NET için Aspose.HTML kütüphanesi yüklü olmalıdır. Bunu şuradan indirebilirsiniz:[indirme bağlantısı](https://releases.aspose.com/html/net/).

-  Geçici Lisans (İsteğe bağlı): Geçerli bir lisansınız yoksa, geçici bir lisans alabilirsiniz.[Burada](https://purchase.aspose.com/temporary-license/).

Şimdi Aspose.HTML for .NET ile ilgili bazı yaygın kullanım durumlarını inceleyelim.

## Ad Alanlarını İçe Aktar

C# kodunuzda, gerekli ad alanlarını içe aktararak başlayın:

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

Bu örnek bir HTML parçacığını PDF belgesine dönüştürür. HTML kodunu ve çıktı dosyasını gerektiği gibi özelleştirebilirsiniz.

## Özel Sayfa Boyutunu Ayarla

### Adım 1: HTML Kodunu Hazırlayın

```csharp
var code = @"<span>Hello World!!</span>";
```

### Adım 2: HTML Belgesini Başlatın

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Adım 3: PDF Oluşturma Seçenekleri Oluşturun

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

Bu örnek, ortaya çıkan PDF belgesi için özel bir sayfa boyutunun nasıl ayarlanacağını göstermektedir.

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

### Adım 3: Düşük Çözünürlüklü PDF Oluşturma Seçenekleri Oluşturun

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

Bu örnek, hem düşük hem de yüksek çözünürlüklü ekranlar dikkate alınarak HTML'yi PDF'ye dönüştürürken çözünürlüğün nasıl ayarlanacağını göstermektedir.

## Arka Plan Rengini Belirle

### Adım 1: HTML Kodunu Hazırlayın ve Dosyaya Kaydedin

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Adım 2: HTML Belgesini Başlatın

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Adım 3: Arka Plan Rengiyle PDF Oluşturma Seçeneklerini Başlatın

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

Bu örnek, HTML'yi PDF'ye dönüştürürken arka plan renginin nasıl belirleneceğini göstermektedir.

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

### Adım 3: Sol ve Sağ Sayfa Boyutlarıyla PDF Oluşturma Seçenekleri Oluşturun

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

Bu örnek, HTML'yi PDF'ye dönüştürürken sol ve sağ sayfalar için farklı sayfa boyutlarının nasıl ayarlanacağını göstermektedir.

## Sayfa Boyutunu İçeriğe Göre Ayarla

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

### Adım 3: PDF Oluşturma Seçenekleri Oluşturun

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

Bu örnek, HTML'i PDF'e dönüştürürken sayfa boyutunun en geniş içeriğe göre nasıl ayarlanacağını göstermektedir.

## PDF İzinlerini Belirle

### Adım 1: HTML Kodunu Hazırlayın

```csharp
var code = @"<div>Hello World!!</div>";
```

### Adım 2: HTML Belgesini Başlatın

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Adım 3: İzinlerle PDF Oluşturma Seçenekleri Oluşturun

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

Bu örnek, HTML'yi korumalı bir PDF'ye dönüştürürken izinlerin ve şifrelemenin nasıl belirleneceğini göstermektedir.

## Görüntüye Özgü Seçenekleri Belirleyin

### Adım 1: HTML Kodunu Hazırlayın

```csharp
var code = @"<div>Hello World!!</div>";
```

### Adım 2: HTML Belgesini Başlatın

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Adım 3: Görüntü İşleme Seçenekleri Oluşturun

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

### Adım 5: HTML'yi Resme Dönüştür

```csharp
document.RenderTo(device);
```

Bu örnek, HTML'nin biçim, çözünürlük ve yumuşatma modu gibi belirli işleme seçenekleriyle bir görüntüye nasıl dönüştürüleceğini gösterir.

## XPS İşleme Seçeneklerini Belirleyin

### Adım 1: HTML Kodunu Hazırlayın

```csharp
var code = @"<span>Hello World!!</span>";
```

### Adım 2: HTML Belgesini Başlatın

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Adım 3: Sayfa Boyutuyla XPS Oluşturma Seçenekleri Oluşturun

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

### Adım 5: HTML'yi XPS'e dönüştürün

```csharp
document.RenderTo(device);
```

Bu örnek, HTML'in özel sayfa boyutu ve görüntüleme seçenekleriyle XPS'e nasıl dönüştürüleceğini gösterir.

## Birden Fazla HTML Belgesini PDF'ye Birleştirin

### Adım 1: Birden Fazla Belge İçin HTML Kodunu Hazırlayın

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

### Adım 3: HTML Oluşturucuyu Başlatın

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Adım 4: Birleştirilmiş Çıktı için PDF Aygıtı Oluşturun

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Adım 5: HTML Belgelerini PDF'ye Birleştirin

```csharp
renderer.Render(device, document1, document2, document3);
```

Bu örnek, Aspose.HTML for .NET kullanılarak birden fazla HTML belgesinin tek bir PDF dosyasında nasıl birleştirileceğini göstermektedir.

## İşleme Zaman Aşımını Ayarla

### Adım 1: JavaScript ile HTML Kodunu Hazırlayın

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

### Adım 3: HTML Oluşturucuyu Başlatın

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Adım 4: PDF Aygıtı Oluşturun ve İşleme Zaman Aşımını Ayarlayın

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Adım 5: HTML'yi Zaman Aşımıyla PDF'ye Dönüştür

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

Bu örnek, HTML'yi PDF'ye dönüştürürken, dinamik içerik veya uzun süre çalışan betiklerle uğraşırken yararlı olabilecek bir işleme zaman aşımının nasıl ayarlanacağını göstermektedir.

## Çözüm

Aspose.HTML for .NET, geliştiricilerin HTML belgeleriyle verimli bir şekilde çalışmasını sağlayan çok yönlü bir kütüphanedir. Bu eğitimde, temel HTML'den PDF'ye dönüştürmelerden özel sayfa boyutları, çözünürlükler ve izinler gibi daha gelişmiş özelliklere kadar çeşitli örnekleri ele aldık. Bu örnekleri izleyerek, .NET uygulamalarınızda Aspose.HTML for .NET'in tüm potansiyelinden yararlanabilirsiniz.

 Herhangi bir sorunuz varsa veya daha fazla yardıma ihtiyacınız varsa, lütfen şu adresi ziyaret etmekten çekinmeyin:[Aspose.HTML Forum](https://forum.aspose.com/) destek ve rehberlik için.

## SSS

### S1. .NET için Aspose.HTML nedir?
   
A1: Aspose.HTML for .NET, geliştiricilerin HTML belgelerini programatik olarak düzenlemesini ve dönüştürmesini sağlayan bir .NET kütüphanesidir. HTML'den PDF'e, XPS'e ve görüntü dönüştürmenin yanı sıra gelişmiş işleme seçenekleri de dahil olmak üzere HTML içeriğiyle çalışmak için çok çeşitli özellikler sunar.

### S2. Aspose.HTML for .NET'i nereden indirebilirim?

 A2: .NET için Aspose.HTML'yi şu adresten indirebilirsiniz:[indirme bağlantısı](https://releases.aspose.com/html/net/).

### S3. Aspose.HTML for .NET'i kullanmak için lisansa ihtiyacım var mı?

C3: Aspose.HTML for .NET'i lisansa ihtiyaç duymadan kullanabilirsiniz; ancak tüm özelliklerin kilidini açmak ve filigranları veya sınırlamaları kaldırmak için üretim amaçlı kullanım için lisans almanız önerilir.

### S4. Aspose.HTML for .NET ile oluşturulan PDF dosyalarımı nasıl koruyabilirim?

A4: Aspose.HTML for .NET kullanarak HTML'yi PDF'ye dönüştürürken PDF izinlerini ve şifreleme ayarlarını belirtebilirsiniz. Bu, ortaya çıkan PDF dosyalarına kimlerin erişebileceğini ve bunları kimlerin değiştirebileceğini kontrol etmenizi sağlar.

### S5. HTML'yi XPS veya resim gibi diğer formatlara dönüştürebilir miyim?

C5: Evet, Aspose.HTML for .NET, HTML'yi PDF, XPS ve resimler (örneğin JPEG) dahil olmak üzere çeşitli biçimlere dönüştürmeyi destekler. Dönüştürme ayarlarını özel gereksinimlerinizi karşılayacak şekilde özelleştirebilirsiniz.