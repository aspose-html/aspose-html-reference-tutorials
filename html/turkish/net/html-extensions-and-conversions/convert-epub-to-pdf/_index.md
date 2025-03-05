---
title: Aspose.HTML ile .NET'te EPUB'ı PDF'ye dönüştürün
linktitle: .NET'te EPUB'ı PDF'ye dönüştürün
second_title: Aspose.HTML .NET HTML işleme API'si
description: Aspose.HTML for .NET kullanarak EPUB'u PDF'ye nasıl dönüştüreceğinizi öğrenin. Bu adım adım kılavuz, kusursuz belge dönüşümü için özelleştirme seçeneklerini, SSS'leri ve daha fazlasını kapsar.
type: docs
weight: 12
url: /tr/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

Bu eğitimde, EPUB dosyalarını PDF'ye dönüştürmek için Aspose.HTML for .NET'in nasıl kullanılacağını inceleyeceğiz. Aspose.HTML, HTML ve EPUB belgeleriyle çalışmak için çeşitli işlevler sağlayan güçlü bir .NET kütüphanesidir. Ön koşulları ele alacağız, gerekli ad alanlarını içe aktaracağız ve her adımı ayrıntılı olarak açıklayarak birden fazla örneği parçalara ayıracağız.

## Ön koşullar

Başlamadan önce aşağıdaki ön koşulların mevcut olduğundan emin olun:

1. .NET için Aspose.HTML: .NET projenizde .NET için Aspose.HTML'nin yüklü olduğundan emin olun. Bunu şuradan indirebilirsiniz:[Burada](https://releases.aspose.com/html/net/).

2. Veri Dizininiz: EPUB dosyalarınızın saklandığı bir veri dizinine ihtiyacınız olacak.

Şimdi Aspose.HTML for .NET kullanarak EPUB'ı PDF'ye dönüştürme sürecine adım adım bakalım.

## EPUB'ı PDF'ye dönüştür

### Adım 1: Projenizi Başlatın

Bir .NET projenizin kurulu olduğundan ve .NET için Aspose.HTML'in yüklü olduğundan emin olun.

### Adım 2: Gerekli Ad Alanlarını İçe Aktarın

C# kod dosyanıza gerekli ad alanlarını içe aktarın:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### Adım 3: EPUB Dosyasını Açın

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Bir sonraki adıma geçin...
}
```

-  Yer değiştirmek`"Your Data Directory"` EPUB dosyanızın bulunduğu gerçek dizinle.
- Bu kod EPUB dosyasını okumaya açar.

### Adım 4: PDF Seçeneklerini Ayarlayın ve Dönüştürmeyi Gerçekleştirin

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Bir örnek oluşturun`PdfSaveOptions` PDF dönüştürme ayarlarını belirtmek için.
-  Kullanın`Converter.ConvertEPUB` Verilen seçeneklerle EPUB'ı PDF'e dönüştürme yöntemi.
- Elde edilen PDF'i "output.pdf" olarak kaydedin.

## PDF Kaydetme Seçeneklerini Belirleyin

### Adım 1: Projenizi Başlatın

Bir .NET projenizin kurulu olduğundan ve .NET için Aspose.HTML'in yüklü olduğundan emin olun.

### Adım 2: Gerekli Ad Alanlarını İçe Aktarın

Gerekli ad alanlarını C# kodunuza aktarın:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### Adım 3: EPUB Dosyasını Açın

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Bir sonraki adıma geçin...
}
```

-  Yer değiştirmek`"Your Data Directory"` EPUB dosyanızın gerçek diziniyle.
- EPUB dosyasını okumak için açın.

### Adım 4: PDF Seçeneklerini Özelleştirin

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  Bir örnek oluşturun`PdfSaveOptions` ve ihtiyaçlarınıza göre özelleştirebilirsiniz.
- Bu örnekte sayfa boyutunu 3000 piksel genişliğe ve 1000 piksel yüksekliğe, arka plan rengini ise Alice Blue olarak ayarladık.

### Adım 5: Dönüştürmeyi Gerçekleştirin

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Kullanın`Converter.ConvertEPUB` EPUB'ı özel seçeneklerle PDF'e dönüştürme yöntemi.
- Elde edilen PDF'i "output.pdf" olarak kaydedin.

## Özel Akış Sağlayıcısını Kullan

### Adım 1: Projenizi Başlatın

Bir .NET projesi kurun ve .NET için Aspose.HTML'i yükleyin.

### Adım 2: Gerekli Ad Alanlarını İçe Aktarın

C# kodunuzda gerekli ad alanlarını içe aktarın:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### Adım 3: EPUB Dosyasını Açın

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Bir sonraki adıma geçin...
}
```

-  Yer değiştirmek`"Your Data Directory"` EPUB dosyanızın gerçek diziniyle.
- EPUB dosyasını okumak için açın.

### Adım 4: Özel Bir Akış Sağlayıcısı Kullanın

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // Bir sonraki adıma geçin...
}
```

-  Bir tane oluştur`MemoryStreamProvider` dönüştürme sonucunu bir bellek akışı olarak yönetmek için.
-  Kullanın`Converter.ConvertEPUB` özel akış sağlayıcısı ile yöntem.

### Adım 5: Sonucu Kaydedin

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- Dönüştürülen verileri içeren bellek akışına erişin.
- Akış konumunu başlangıca ayarlayın.
- Bir çıktı PDF dosyası oluşturun ve içeriği bellek akışından ona kopyalayın.

### Sınıf MemoryStreamProvider kaynak kodu. 

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
Artık, çeşitli seçenekler ve özelleştirme olanaklarıyla Aspose.HTML for .NET kullanarak EPUB dosyalarını PDF'ye nasıl dönüştüreceğinizi öğrendiniz. Aspose.HTML, belge dönüştürmeniz üzerinde esneklik ve kontrol sağlayarak süreci basitleştirir.

## Çözüm

Aspose.HTML for .NET, EPUB dosyalarını PDF'ye dönüştürmek için çok yönlü bir araçtır ve ortaya çıkan PDF belgesini ihtiyaçlarınıza göre uyarlamak için özelleştirme seçenekleri sunar. Basit dönüştürmeler veya gelişmiş özelleştirmeler gerektirse de, Aspose.HTML sizin için her şeyi yapar.

 Henüz yapmadıysanız, .NET için Aspose.HTML'yi şu adresten indirebilirsiniz:[web sitesi](https://releases.aspose.com/html/net/) ve bugün .NET uygulamalarınızda kullanmaya başlayın.

---

## SSS

### Aspose.HTML for .NET'i kullanmak ücretsiz mi?
    Aspose.HTML for .NET ticari bir üründür, ancak ücretsiz deneme sürümü mevcuttur[Burada](https://releases.aspose.com/).

### Dönüştürülen PDF'in görünümünü özelleştirebilir miyim?
   Evet, Örnek 2'de gösterildiği gibi sayfa boyutu ve arka plan rengi gibi seçenekleri ayarlayarak PDF görünümünü özelleştirebilirsiniz.

### .NET için Aspose.HTML desteğini nasıl alabilirim?
    Destek ve kaynakları şu adreste bulabilirsiniz:[Aspose.HTML forumu](https://forum.aspose.com/).

### Aspose.HTML for .NET ile dönüştürebileceğim başka formatlar var mı?
   Evet, Aspose.HTML for .NET HTML, EPUB ve daha fazlası dahil olmak üzere çeşitli belge biçimlerini destekler.

### Aspose.HTML for ..NET büyük ölçekli belge dönüştürme için uygun mudur?
   .NET için Aspose.HTML, geniş ölçekli belge dönüşümlerini verimli bir şekilde gerçekleştirmek üzere tasarlanmıştır ve bu sayede çok çeşitli uygulamalar için uygundur.

