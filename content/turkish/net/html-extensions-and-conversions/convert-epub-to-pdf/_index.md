---
title: Aspose.HTML ile EPUB'u .NET'te PDF'ye dönüştürün
linktitle: .NET'te EPUB'u PDF'ye dönüştürün
second_title: Aspose.HTML .NET HTML işleme API'si
description: Aspose.HTML for .NET'i kullanarak EPUB'u PDF'ye nasıl dönüştüreceğinizi öğrenin. Bu adım adım kılavuz, sorunsuz belge dönüştürme için özelleştirme seçeneklerini, SSS'leri ve daha fazlasını kapsar.
type: docs
weight: 12
url: /tr/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

Bu eğitimde, EPUB dosyalarını PDF'ye dönüştürmek için Aspose.HTML for .NET'in nasıl kullanılacağını inceleyeceğiz. Aspose.HTML, HTML ve EPUB belgeleriyle çalışmak için çeşitli işlevler sağlayan güçlü bir .NET kitaplığıdır. Önkoşulları ele alacağız, gerekli ad alanlarını içe aktaracağız ve birden fazla örneği inceleyerek her adımı ayrıntılı olarak açıklayacağız.

## Önkoşullar

Başlamadan önce aşağıdaki önkoşulların mevcut olduğundan emin olun:

1. Aspose.HTML for .NET: .NET projenizde Aspose.HTML for .NET'in kurulu olduğundan emin olun. Şuradan indirebilirsiniz[Burada](https://releases.aspose.com/html/net/).

2. Veri Dizininiz: EPUB dosyalarınızın saklandığı bir veri dizinine ihtiyacınız olacak.

Şimdi Aspose.HTML for .NET kullanarak EPUB'u PDF'ye dönüştürmenin adım adım sürecine dalalım.

## EPUB'u PDF'ye dönüştür

### 1. Adım: Projenizi Başlatın

Bir .NET projenizin kurulu olduğundan ve Aspose.HTML for .NET'in kurulu olduğundan emin olun.

### 2. Adım: Gerekli Ad Alanlarını İçe Aktarın

C# kod dosyanızda gerekli ad alanlarını içe aktarın:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### 3. Adım: EPUB Dosyasını açın

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Sonraki adıma devam et...
}
```

-  Yer değiştirmek`"Your Data Directory"` EPUB dosyanızın bulunduğu gerçek dizinle.
- Bu kod EPUB dosyasını okumak için açar.

### Adım 4: PDF Seçeneklerini Ayarlayın ve Dönüştürmeyi Gerçekleştirin

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Bir örneğini oluşturun`PdfSaveOptions` PDF dönüştürme ayarlarını belirtmek için.
-  Kullan`Converter.ConvertEPUB` Verilen seçeneklerle EPUB'u PDF'ye dönüştürme yöntemi.
- Ortaya çıkan PDF'yi "output.pdf" olarak kaydedin.

## PDF Kaydetme Seçeneklerini Belirleyin

### 1. Adım: Projenizi Başlatın

Bir .NET projenizin kurulu olduğundan ve Aspose.HTML for .NET'in kurulu olduğundan emin olun.

### 2. Adım: Gerekli Ad Alanlarını İçe Aktarın

Gerekli ad alanlarını C# kodunuza aktarın:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### 3. Adım: EPUB Dosyasını açın

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Sonraki adıma devam et...
}
```

-  Yer değiştirmek`"Your Data Directory"` EPUB dosyanızın gerçek dizini ile.
- Okumak için EPUB dosyasını açın.

### 4. Adım: PDF Seçeneklerini Özelleştirin

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  Bir örneğini oluşturun`PdfSaveOptions` ve ihtiyaçlarınıza göre özelleştirin.
- Bu örnekte sayfa boyutunu 3000 piksel genişliğe ve 1000 piksel yüksekliğe, arka plan rengini ise Alice Mavisi olarak ayarladık.

### Adım 5: Dönüşümü Gerçekleştirin

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Kullan`Converter.ConvertEPUB` EPUB'u özel seçeneklerle PDF'ye dönüştürme yöntemi.
- Ortaya çıkan PDF'yi "output.pdf" olarak kaydedin.

## Özel Akış Sağlayıcıyı Kullan

### 1. Adım: Projenizi Başlatın

Bir .NET projesi oluşturun ve Aspose.HTML for .NET'i yükleyin.

### 2. Adım: Gerekli Ad Alanlarını İçe Aktarın

C# kodunuzda gerekli ad alanlarını içe aktarın:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### 3. Adım: EPUB Dosyasını açın

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Sonraki adıma devam et...
}
```

-  Yer değiştirmek`"Your Data Directory"` EPUB dosyanızın gerçek dizini ile.
- Okumak için EPUB dosyasını açın.

### 4. Adım: Özel Akış Sağlayıcısı Kullanın

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // Sonraki adıma devam et...
}
```

-  Oluşturmak`MemoryStreamProvider` Dönüşüm sonucunu bir bellek akışı olarak yönetmek için.
-  Kullan`Converter.ConvertEPUB` özel akış sağlayıcısıyla yöntem.

### Adım 5: Sonucu Kaydet

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
- Bir çıktı PDF dosyası oluşturun ve içeriği bellek akışından bu dosyaya kopyalayın.

### Sınıf MemoryStreamProvider kaynak kodu. 

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
Artık çeşitli seçenekler ve özelleştirme olanaklarıyla Aspose.HTML for .NET kullanarak EPUB dosyalarını PDF'ye nasıl dönüştüreceğinizi öğrendiniz. Aspose.HTML süreci basitleştirerek belge dönüştürme işleminiz üzerinde esneklik ve kontrol sağlar.

## Çözüm

Aspose.HTML for .NET, EPUB dosyalarını PDF'ye dönüştürmek için kullanılan çok yönlü bir araçtır ve ortaya çıkan PDF belgesini ihtiyaçlarınıza göre uyarlamak için özelleştirme seçenekleri sunar. İster basit dönüşümlere ister gelişmiş özelleştirmeye ihtiyacınız olsun, Aspose.HTML ihtiyacınızı karşılar.

 Henüz yapmadıysanız Aspose.HTML for .NET'i şu adresten indirebilirsiniz:[İnternet sitesi](https://releases.aspose.com/html/net/) ve bugün .NET uygulamalarınızda kullanmaya başlayın.

---

## SSS

### Aspose.HTML for .NET'in kullanımı ücretsiz mi?
    Aspose.HTML for .NET ticari bir üründür ancak ücretsiz deneme sürümü mevcuttur[Burada](https://releases.aspose.com/).

### Dönüştürülen PDF'nin görünümünü özelleştirebilir miyim?
   Evet, Örnek 2'de gösterildiği gibi sayfa boyutu ve arka plan rengi gibi seçenekleri ayarlayarak PDF görünümünü özelleştirebilirsiniz.

### Aspose.HTML for .NET için nasıl destek alabilirim?
    Destek ve kaynakları şu adreste bulabilirsiniz:[Aspose.HTML forumu](https://forum.aspose.com/).

### Aspose.HTML for .NET ile dönüştürebileceğim başka formatlar var mı?
   Evet, Aspose.HTML for .NET, aralarında HTML, EPUB ve daha fazlasının da bulunduğu çeşitli belge formatlarını destekler.

### Aspose.HTML for ..NET büyük ölçekli belge dönüştürmeye uygun mu?
   Aspose.HTML for .NET, büyük ölçekli belge dönüştürme işlemlerini verimli bir şekilde gerçekleştirecek şekilde tasarlanmıştır ve bu da onu çok çeşitli uygulamalar için uygun hale getirir.

