---
title: Aspose.HTML ile .NET'te EPUB'ı Görüntüye Dönüştürme
linktitle: EPUB'ı .NET'te Görüntüye Dönüştürme
second_title: Aspose.HTML .NET HTML işleme API'si
description: Aspose.HTML for .NET kullanarak EPUB'ı görsellere nasıl dönüştüreceğinizi öğrenin. Kod örnekleri ve özelleştirilebilir seçenekler içeren adım adım eğitim.
type: docs
weight: 11
url: /tr/net/html-extensions-and-conversions/convert-epub-to-image/
---

Günümüzün dijital çağında, çeşitli belge biçimlerini düzenleme ve dönüştürme yeteneği değerli bir beceridir. Aspose.HTML for .NET, geliştiricilerin HTML ve EPUB belgeleriyle zahmetsizce çalışmasına olanak tanıyan güçlü bir araçtır. Bu eğitimde, Aspose.HTML for .NET dünyasına dalacağız ve EPUB belgelerini çeşitli resim biçimlerine dönüştürme sürecinde size rehberlik edeceğiz. Her örneği birden fazla adıma bölerek her adımı açıklayacağız.

## Ön koşullar

.NET için Aspose.HTML dünyasına dalmadan önce, aşağıdaki ön koşulların mevcut olduğundan emin olmalısınız:

1. Visual Studio: Sisteminizde Visual Studio'nun yüklü olduğundan emin olun. Bunu web sitesinden indirebilirsiniz.

2.  .NET için Aspose.HTML: Kütüphaneyi Aspose web sitesinden edinebilirsiniz[Burada](https://releases.aspose.com/html/net/).

3. Veri Dizininiz: EPUB dosyalarınızı saklayacağınız ve çıktı görsellerinin kaydedileceği bir dizin hazırlayın.

4. Temel C# Bilgisi: Bu eğitimde sunulan kod örneklerini anlamak ve uygulamak için C# programlamaya aşinalık şarttır.

## Gerekli Ad Alanlarını İçe Aktarma

Aspose.HTML for .NET ile çalışmaya başlamadan önce, gerekli ad alanlarını C# kodunuza aktarmanız gerekir. Bu ad alanları, Aspose.HTML for .NET özelliklerine erişim sağlar.

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using Aspose.Html.Rendering.Image;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
using System.IO;
using System.Drawing;
using System.Collections.Generic;
```

Artık ön koşullar ve ad alanları hazır olduğuna göre, adım adım örneklere geçelim.

## EPUB'ı JPEG'e dönüştürme

```csharp
    string dataDir = "Your Data Directory";
    // Mevcut bir EPUB dosyasını okumak için açın.
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // EPUB dosyasını görüntüye dönüştürmek için ConvertEPUB metodunu çağırın.
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### Adımlar

1. dataDir değişkeninde EPUB dosyanızın yolunu belirtin.
2. EPUB dosyasını FileStream kullanarak okumak için açın.
3. EPUB akışını, çıktı formatını (JPEG) ve çıktı dosya adını ("output.jpg") belirten bir ImageSaveOptions'ı geçirerek ConvertEPUB yöntemini çağırın.
5. EPUB dosyası JPEG görüntüye dönüştürülür.

Bu örnekte bir EPUB dosyasını açıyoruz, içeriğini okuyoruz ve onu JPEG resim biçimine dönüştürüyoruz. Çıktı resmi "output.jpg" olarak kaydedilir.

## EPUB'ı PNG'ye dönüştürme

Benzer kod yapılarını kullanarak EPUB dosyalarını PNG, BMP, GIF ve TIFF gibi çeşitli resim biçimlerine kolayca dönüştürebilirsiniz. PNG'ye dönüştürmeye yönelik bir örnek şöyledir:

```csharp

    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Png);
        Converter.ConvertEPUB(stream, options, "output.png");
    }

```
### Adımlar
1. EPUB dosyasını FileStream kullanarak okumak için açın.
2. İstenilen çıktı biçimini (bu durumda PNG) kullanarak bir ImageSaveOptions nesnesi başlatın.
3. ConvertEPUB yöntemini çağırın, EPUB akışını, resim kaydetme seçeneklerini ve çıktı dosya adını geçirin.
4. EPUB dosyası belirtilen resim formatına dönüştürülür.

## Görüntü Kaydetme Seçeneklerini Belirleyin

Sayfa boyutu ve arka plan rengi gibi seçenekleri belirleyerek görüntü çıktısını özelleştirebilirsiniz. İşte bir örnek:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Jpeg)
        {
            PageSetup =
            {
                AnyPage = new Page()
                {
                    Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
                }
            },
            BackgroundColor = Color.AliceBlue,
        };
        Converter.ConvertEPUB(stream, options, "output.jpg");
    }
```
### Adımlar

1.  EPUB dosyanızın yolunu belirtin`dataDir` değişken.
2.  EPUB dosyasını okumak için açın`FileStream`.
3.  Bir tane oluştur`ImageSaveOptions` nesneyi seçin ve istediğiniz çıktı formatını (JPEG) belirtin.
4. Gerekirse sayfa boyutunu ve arka plan rengini özelleştirin.
5.  Ara`ConvertEPUB`yöntem, EPUB akışını, resim kaydetme seçeneklerini ve çıktı dosya adını geçirme.
6. EPUB dosyası belirtilen seçeneklerle görüntüye dönüştürülür.

## Özel Bir Akış Sağlayıcısı Belirleyin

Çıktı akışını düzenlemeniz gerekiyorsa, özel bir akış sağlayıcısı kullanabilirsiniz. İşte bir örnek:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        using (var streamProvider = new MemoryStreamProvider())
        {
            Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), streamProvider);
            
            for (int i = 0; i < streamProvider.Streams.Count; i++)
            {
                var memory = streamProvider.Streams[i];
                memory.Seek(0, SeekOrigin.Begin);
                
                using (FileStream fs = File.Create($"page_{i + 1}.jpg"))
                {
                    memory.CopyTo(fs);
                }
            }
        }
    }

```
MemoryStreamProvider Sınıfı Kaynak Kodu.

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

### Adımlar
1.  EPUB dosyanızın yolunu belirtin`dataDir` değişken.
2.  EPUB dosyasını okumak için açın`FileStream`.
3.  Bir tane oluştur`MemoryStreamProvider` özel çıktı akışlarını işlemek için.
4.  Ara`ConvertEPUB` yöntem, EPUB akışını, resim kaydetme seçeneklerini (JPEG) ve özel akış sağlayıcısını geçirme.
5. Özel sağlayıcıdaki bellek akışları arasında gezinin ve bunları ayrı dosyalara kaydedin.
6. Bu örnek, gerektiğinde birden fazla çıktı akışını düzenlemenize ve kaydetmenize olanak tanır.

## Çözüm

Aspose.HTML for .NET, EPUB ve HTML belgeleriyle çalışmayı basitleştiren çok yönlü bir kütüphanedir. EPUB belgelerini çeşitli resim biçimlerine dönüştürme yeteneği ve özelleştirilebilir seçeneklerle, geliştiriciler için çok çeşitli uygulamalar sunar.

---

## Sıkça Sorulan Sorular

### 1. Aspose.HTML for .NET'i nereden indirebilirim?

 .NET için Aspose.HTML'i sürümler sayfasından indirebilirsiniz[Burada](https://releases.aspose.com/html/net/).

### 2. Aspose.HTML for .NET için geçici lisansı nasıl alabilirim?

 Geçici lisans almak için geçici lisans sayfasını ziyaret edin[Burada](https://purchase.aspose.com/temporary-license/).

### 3. Aspose.HTML for .NET için ek desteği nerede bulabilirim?

 Herhangi bir soru veya sorun için destek forumunda Aspose topluluğundan yardım isteyebilirsiniz[Burada](https://forum.aspose.com/).

### 4. EPUB belgelerini PDF veya XPS gibi diğer formatlara dönüştürebilir miyim?

Evet, EPUB belgelerini PDF ve XPS dahil olmak üzere çeşitli biçimlere dönüştürmek için Aspose.HTML for .NET'i kullanabilirsiniz.

### 5. Aspose.HTML for .NET hem küçük hem de büyük ölçekli projeler için uygun mudur?

Kesinlikle! Aspose.HTML for .NET ölçeklenebilir olacak şekilde tasarlanmıştır ve bu da onu her boyuttaki proje için harika bir seçim haline getirir.
