---
title: Aspose.HTML ile .NET'te EPUB'ı XPS'e dönüştürün
linktitle: .NET'te EPUB'ı XPS'e dönüştürme
second_title: Aspose.HTML .NET HTML işleme API'si
description: .NET'te Aspose.HTML for .NET kullanarak EPUB'ı XPS'e nasıl dönüştüreceğinizi öğrenin. Zahmetsiz dönüşümler için adım adım kılavuzumuzu izleyin.
weight: 13
url: /tr/net/html-extensions-and-conversions/convert-epub-to-xps/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML ile .NET'te EPUB'ı XPS'e dönüştürün


.NET uygulamalarınızda EPUB dosyalarını XPS formatına dönüştürmenin kusursuz bir yolunu mu arıyorsunuz? Aspose.HTML for .NET bunu zahmetsizce başarmak için güçlü bir çözüm sunar. Bu adım adım kılavuzda, Aspose.HTML kullanarak EPUB'u XPS'e dönüştürme sürecinde size yol göstereceğiz. Başlayalım!

## Ön koşullar

EPUB'ı XPS'e dönüştürme işlemine başlamadan önce, aşağıdaki ön koşulların mevcut olduğundan emin olmanız gerekir:

### 1. .NET Kütüphanesi için Aspose.HTML

 Projenizde Aspose.HTML for .NET kütüphanesinin yüklü olduğundan emin olun. Eğer yüklü değilse, şuradan edinebilirsiniz:[Aspose.HTML for .NET İndirme sayfası](https://releases.aspose.com/html/net/).

### 2. EPUB Dosyasını Girin

XPS'e dönüştürmek istediğiniz bir EPUB dosyasına ihtiyacınız olacak. Dönüştürme için bir EPUB dosyanız olduğundan emin olun.

### 3. .NET Geliştirme Ortamı

Bu kılavuz, makinenizde çalışan bir .NET geliştirme ortamının kurulu olduğunu varsayar.

## Ad Alanını İçe Aktar

Başlamak için Aspose.HTML için gerekli ad alanını içe aktarmalısınız:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## EPUB'ı XPS'e dönüştür

EPUB dosyasını XPS formatına dönüştürme sürecini birden fazla adıma bölelim.

### Adım 1.1: EPUB Dosyasını Açın

Öncelikle mevcut EPUB dosyasını FileStream kullanarak okumaya açın:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Dönüştürme işlemine devam edin
}
```

### Adım 1.2: XpsSaveOptions'ı Oluşturun

XpsSaveOptions'ın bir örneğini oluşturun. Bu adım XPS çıktısını yapılandırmak için çok önemlidir:

```csharp
var options = new XpsSaveOptions();
```

### Adım 1.3: EPUB'ı XPS'e dönüştürün

Şimdi EPUB'ı XPS'e dönüştürmek için ConvertEPUB metodunu çağıralım:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Özel XPS Seçeneklerini Belirleyin

Sayfa boyutu ve arka plan rengi gibi özel seçenekleri belirleyerek XPS çıktısını daha da özelleştirebilirsiniz.

### Adım 2.1: Özel Sayfa Boyutu ve Arka Plan Rengi

Özel sayfa boyutu ve arka plan rengiyle XpsSaveOptions örneğini oluşturun:

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

### Adım 2.2: EPUB'ı Özel Seçeneklerle XPS'e Dönüştürün

Şimdi, EPUB'ı özel seçeneklerle XPS'e dönüştürmek için ConvertEPUB yöntemini çağırın:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Özel Akış Sağlayıcısını Kullan

Bu adımda, ortaya çıkan verileri düzenlemenize olanak tanıyan özel bir akış sağlayıcısı kullanarak EPUB'ı XPS'e dönüştüreceğiz.

### Adım 3.1: Bir MemoryStreamProvider Oluşturun

MemoryStreamProvider'ın bir örneğini oluşturun:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Dönüştürme işlemine devam edin
}
```

### Adım 3.2: EPUB'ı Stream Provider ile XPS'e dönüştürün

EPUB'ı MemoryStreamProvider'ı kullanarak XPS'e dönüştürün:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Adım 3.3: Sonuca Erişim ve Kaydetme

Dönüştürülen verileri içeren bellek akışını alın ve bir çıktı dosyasına kaydedin:

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
            // Belgenin işlenmesi sırasında oluşturulan MemoryStream nesnelerinin listesi
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Bu yöntem, yalnızca bir çıktı akışı gerektiğinde, örneğin XPS, PDF veya TIFF formatları için çağrılır.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Bu yöntem, birden fazla çıktı akışının oluşturulması gerektiğinde çağrılır. Örneğin, HTML'yi görüntü dosyalarının (JPG, PNG, vb.) listesine dönüştürme sırasında
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Burada, verilerle dolu akışı serbest bırakabilir ve örneğin onu sabit diske aktarabilirsiniz
            }
            public void Dispose()
            {
                // Kaynakları serbest bırakmak
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Tebrikler! Aspose.HTML for .NET kullanarak bir EPUB dosyasını XPS formatına başarıyla dönüştürdünüz.

## Çözüm

Bu kapsamlı eğitimde, çeşitli özelleştirme seçenekleriyle EPUB dosyalarını XPS formatına dönüştürmek için Aspose.HTML for .NET'i nasıl kullanacağınızı inceledik. İster deneyimli bir geliştirici olun ister yeni başlıyor olun, Aspose.HTML süreci basitleştirir ve EPUB'dan XPS'e dönüştürmeleri kolaylıkla yapmanızı sağlar.

 Herhangi bir sorunuz veya karşılaştığınız bir sorun mu var? Şuraya göz atın:[Aspose.HTML Belgeleri](https://reference.aspose.com/html/net/) daha fazla bilgi için veya yardım isteyin[Aspose.HTML Topluluk Forumu](https://forum.aspose.com/).

## Sıkça Sorulan Sorular

### .NET için Aspose.HTML nedir?
Aspose.HTML for .NET, geliştiricilerin .NET uygulamalarında HTML, EPUB ve XPS belgeleriyle çalışmasını sağlayan güçlü bir kütüphanedir.

### .NET için Aspose.HTML'i nereden indirebilirim?
 .NET için Aspose.HTML'yi şu adresten indirebilirsiniz:[indirme sayfası](https://releases.aspose.com/html/net/).

### Aspose.HTML for .NET için ücretsiz deneme sürümü mevcut mu?
 Evet, ücretsiz deneme sürümünü şu adresten alabilirsiniz:[Burada](https://releases.aspose.com/).

### Aspose.HTML for .NET için geçici lisansı nasıl alabilirim?
 Geçici bir lisans almak için şu adresi ziyaret edin:[geçici lisans sayfası](https://purchase.aspose.com/temporary-license/).

### Aspose.HTML for .NET için daha fazla öğretici ve dokümanı nerede bulabilirim?
 Konuyla ilgili geniş yelpazedeki öğreticileri ve ayrıntılı belgeleri keşfedin[Aspose.HTML Belgeleri](https://reference.aspose.com/html/net/) sayfa.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
