---
title: Aspose.HTML ile EPUB'u .NET'te XPS'ye dönüştürün
linktitle: .NET'te EPUB'u XPS'ye dönüştürün
second_title: Aspose.HTML .NET HTML işleme API'si
description: Aspose.HTML for .NET kullanarak EPUB'u .NET'te XPS'ye nasıl dönüştüreceğinizi öğrenin. Zahmetsiz dönüşümler için Adım adım kılavuzumuzu izleyin.
type: docs
weight: 13
url: /tr/net/html-extensions-and-conversions/convert-epub-to-xps/
---

.NET uygulamalarınızda EPUB dosyalarını XPS formatına dönüştürmenin kusursuz bir yolunu mu arıyorsunuz? Aspose.HTML for .NET bunu zahmetsizce gerçekleştirmek için güçlü bir çözüm sunar. Bu adım adım kılavuzda, Aspose.HTML kullanarak EPUB'u XPS'ye dönüştürme sürecinde size yol göstereceğiz. Başlayalım!

## Önkoşullar

EPUB'dan XPS'ye dönüştürme sürecine dalmadan önce aşağıdaki önkoşulların yerine getirildiğinden emin olmanız gerekir:

### 1. Aspose.HTML for .NET Kütüphanesi

 Projenizde Aspose.HTML for .NET kütüphanesinin kurulu olduğundan emin olun. Eğer yapmadıysanız adresinden temin edebilirsiniz.[Aspose.HTML for .NET İndirme sayfası](https://releases.aspose.com/html/net/).

### 2. EPUB Dosyasını Girin

XPS'ye dönüştürmek istediğiniz bir EPUB dosyasına ihtiyacınız olacak. Dönüştürme için kullanılabilir bir EPUB dosyanız olduğundan emin olun.

### 3. .NET Geliştirme Ortamı

Bu kılavuz, makinenizde çalışan bir .NET geliştirme ortamının kurulu olduğunu varsaymaktadır.

## Ad Alanını İçe Aktar

Başlamak için Aspose.HTML için gerekli ad alanını içe aktarmalısınız:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## EPUB'u XPS'ye dönüştür

Bir EPUB dosyasını XPS formatına dönüştürme sürecini birden fazla adıma ayıralım.

### Adım 1.1: EPUB Dosyasını Açın

Öncelikle, FileStream kullanarak okumak için mevcut EPUB dosyasını açın:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Dönüştürme işlemine devam edin
}
```

### Adım 1.2: XpsSaveOptions'ı oluşturun

XpsSaveOptions'ın bir örneğini oluşturun. Bu adım, XPS çıkışını yapılandırmak için çok önemlidir:

```csharp
var options = new XpsSaveOptions();
```

### Adım 1.3: EPUB'u XPS'ye dönüştürün

Şimdi EPUB'u XPS'e dönüştürmek için ConvertEPUB yöntemini çağıralım:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Özel XPS Seçeneklerini Belirleyin

Sayfa boyutu ve arka plan rengi gibi özel seçenekleri belirleyerek XPS çıktısını daha da özelleştirebilirsiniz.

### Adım 2.1: Özel Sayfa Boyutu ve Arka Plan Rengi

Özel sayfa boyutuna ve arka plan rengine sahip bir XpsSaveOptions örneği oluşturun:

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### Adım 2.2: Özel Seçeneklerle EPUB'u XPS'ye dönüştürün

Şimdi EPUB'u özel seçeneklerle XPS'ye dönüştürmek için ConvertEPUB yöntemini çağırın:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Özel Akış Sağlayıcıyı Kullan

Bu adımda, özel bir akış sağlayıcı kullanarak EPUB'u XPS'ye dönüştüreceğiz ve sonuçta ortaya çıkan verileri değiştirmenize olanak sağlayacağız.

### Adım 3.1: MemoryStreamProvider Oluşturun

MemoryStreamProvider'ın bir örneğini oluşturun:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Dönüştürme işlemine devam edin
}
```

### Adım 3.2: Akış Sağlayıcı ile EPUB'u XPS'ye dönüştürün

MemoryStreamProvider'ı kullanarak EPUB'u XPS'ye dönüştürün:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Adım 3.3: Sonuca Erişin ve Kaydedin

Dönüştürülen verileri içeren bellek akışını alın ve bunu bir çıktı dosyasına kaydedin:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Sınıf MemoryStreamProvider Kaynak Kodu

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Belge oluşturma sırasında oluşturulan MemoryStream nesnelerinin listesi
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Bu yöntem, örneğin XPS, PDF veya TIFF formatları için yalnızca bir çıktı akışı gerektiğinde çağrılır.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Bu yöntem, birden fazla çıktı akışının oluşturulması gerektiğinde çağrılır. Örneğin, HTML oluşturma sırasında görüntü dosyalarının (JPG, PNG, vb.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Burada verilerle dolu akışı serbest bırakabilir ve örneğin sabit sürücüye aktarabilirsiniz.
            }
            public void Dispose()
            {
                // Kaynakları serbest bırakma
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Tebrikler! Aspose.HTML for .NET'i kullanarak bir EPUB dosyasını başarıyla XPS formatına dönüştürdünüz.

## Çözüm

Bu kapsamlı eğitimde, çeşitli özelleştirme seçenekleriyle EPUB dosyalarını XPS formatına dönüştürmek için Aspose.HTML for .NET'ten nasıl yararlanılacağını araştırdık. İster deneyimli bir geliştirici olun ister yeni başlıyor olun, Aspose.HTML süreci basitleştirerek EPUB'dan XPS'ye dönüşümleri kolaylıkla gerçekleştirmenize olanak tanır.

 Herhangi bir sorunuz veya karşılaştığınız sorunlar mı var? Kontrol et[Aspose.HTML Belgeleri](https://reference.aspose.com/html/net/) daha fazla bilgi edinmek veya yardım almak için[Aspose.HTML Topluluk Forumu](https://forum.aspose.com/).

## Sıkça Sorulan Sorular

### .NET için Aspose.HTML nedir?
Aspose.HTML for .NET, geliştiricilerin .NET uygulamalarında HTML, EPUB ve XPS belgeleriyle çalışmasına olanak tanıyan güçlü bir kitaplıktır.

### Aspose.HTML for .NET'i nereden indirebilirim?
 Aspose.HTML for .NET'i şu adresten indirebilirsiniz:[indirme sayfası](https://releases.aspose.com/html/net/).

### Aspose.HTML for .NET'in ücretsiz deneme sürümü mevcut mu?
 Evet, şu adresten ücretsiz deneme alabilirsiniz:[Burada](https://releases.aspose.com/).

### Aspose.HTML for .NET için nasıl geçici lisans alabilirim?
 Geçici lisans almak için şu adresi ziyaret edin:[geçici lisans sayfası](https://purchase.aspose.com/temporary-license/).

### Aspose.HTML for .NET için daha fazla eğitim ve belgeyi nerede bulabilirim?
Çok çeşitli eğitimleri ve ayrıntılı belgeleri keşfedin.[Aspose.HTML Belgeleri](https://reference.aspose.com/html/net/) sayfa.