---
title: Aspose.HTML ile EPUB'u .NET'teki Görüntüye Dönüştürün
linktitle: EPUB'u .NET'te Görüntüye Dönüştürme
second_title: Aspose.HTML .NET HTML işleme API'si
description: Aspose.HTML for .NET kullanarak EPUB'u görüntülere nasıl dönüştüreceğinizi öğrenin. Kod örnekleri ve özelleştirilebilir seçenekler içeren adım adım eğitim.
type: docs
weight: 11
url: /tr/net/html-extensions-and-conversions/convert-epub-to-image/
---

Günümüzün dijital çağında, çeşitli belge formatlarını değiştirme ve dönüştürme yeteneği değerli bir beceridir. Aspose.HTML for .NET, geliştiricilerin HTML ve EPUB belgeleriyle zahmetsizce çalışmasına olanak tanıyan güçlü bir araçtır. Bu eğitimde Aspose.HTML for .NET dünyasını derinlemesine inceleyeceğiz ve EPUB belgelerini çeşitli görüntü formatlarına dönüştürme sürecinde size rehberlik edeceğiz. Her örneği birden fazla adıma ayıracağız ve yol boyunca her adımı açıklayacağız.

## Önkoşullar

Aspose.HTML for .NET dünyasına dalmadan önce aşağıdaki önkoşulların mevcut olduğundan emin olmalısınız:

1. Visual Studio: Sisteminizde Visual Studio'nun kurulu olduğundan emin olun. Web sitesinden indirebilirsiniz.

2.  Aspose.HTML for .NET: Kütüphaneyi Aspose web sitesinden edinebilirsiniz.[Burada](https://releases.aspose.com/html/net/).

3. Veri Dizininiz: EPUB dosyalarınızı saklayacağınız ve çıktı görsellerinin kaydedileceği bir dizin hazırlayın.

4. Temel C# Bilgisi: C# programlamaya aşina olmak, bu eğitimde sağlanan kod örneklerini anlamak ve uygulamak için çok önemlidir.

## Gerekli Ad Alanlarını İçe Aktarma

Aspose.HTML for .NET ile çalışmaya başlamadan önce gerekli ad alanlarını C# kodunuza aktarmanız gerekir. Bu ad alanları Aspose.HTML for .NET özelliklerine erişim sağlar.

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

Artık önkoşulları ve ad alanlarını oluşturduğumuza göre adım adım örneklere geçelim.

## EPUB'u JPEG'e dönüştürme

```csharp
    string dataDir = "Your Data Directory";
    // Okumak için mevcut bir EPUB dosyasını açın.
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // EPUB dosyasını görüntüye dönüştürmek için ConvertEPUB yöntemini çağırın.
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### Adımlar

1. dataDir değişkeninde EPUB dosyanızın yolunu belirtin.
2. FileStream kullanarak okumak için EPUB dosyasını açın.
3. EPUB akışını, çıktı biçimini (JPEG) ve çıktı dosyası adını ("output.jpg") belirten ImageSaveOptions'ı ileterek ConvertEPUB yöntemini çağırın.
5. EPUB dosyası JPEG görüntüsüne dönüştürülür.

Bu örnekte bir EPUB dosyasını açıyoruz, içeriğini okuyoruz ve onu JPEG görüntü formatına dönüştürüyoruz. Çıktı görüntüsü "output.jpg" olarak kaydedilir.

## EPUB'u PNG'ye dönüştürme

Benzer kod yapılarını kullanarak EPUB dosyalarını kolaylıkla PNG, BMP, GIF ve TIFF gibi çeşitli görüntü formatlarına dönüştürebilirsiniz. PNG'ye dönüştürmeye ilişkin bir örnek:

```csharp

    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Png);
        Converter.ConvertEPUB(stream, options, "output.png");
    }

```
### Adımlar
1. FileStream kullanarak okumak için EPUB dosyasını açın.
2. Bir ImageSaveOptions nesnesini istenen çıktı biçimiyle (bu durumda PNG) başlatın.
3. EPUB akışını, görüntü kaydetme seçeneklerini ve çıktı dosyası adını ileterek ConvertEPUB yöntemini çağırın.
4. EPUB dosyası belirtilen görüntü formatına dönüştürülür.

## Görüntü Kaydetme Seçeneklerini Belirleyin

Sayfa boyutu ve arka plan rengi gibi seçenekleri belirterek görüntü çıktısını özelleştirebilirsiniz. İşte bir örnek:

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

1.  EPUB dosyanızın yolunu şu adreste belirtin:`dataDir` değişken.
2.  EPUB dosyasını okumak için bir kullanarak açın.`FileStream`.
3.  Oluşturduğunuz bir`ImageSaveOptions` nesneyi seçin ve istenen çıktı formatını (JPEG) belirtin.
4. Gerekirse sayfa boyutunu ve arka plan rengini özelleştirin.
5.  Ara`ConvertEPUB` yöntemi, EPUB akışının, görüntü kaydetme seçeneklerinin ve çıktı dosyası adının iletilmesi.
6. EPUB dosyası belirtilen seçeneklerle bir görüntüye dönüştürülür.

## Özel Akış Sağlayıcısı Belirtin

Çıkış akışını değiştirmeniz gerekiyorsa özel bir akış sağlayıcısı kullanabilirsiniz. İşte bir örnek:

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

### Adımlar
1.  EPUB dosyanızın yolunu şu adreste belirtin:`dataDir` değişken.
2.  EPUB dosyasını okumak için bir kullanarak açın.`FileStream`.
3.  Oluşturmak`MemoryStreamProvider` özel çıktı akışlarını yönetmek için.
4.  Ara`ConvertEPUB`EPUB akışını, görüntü kaydetme seçeneklerini (JPEG) ve özel akış sağlayıcısını geçirme yöntemi.
5. Özel sağlayıcıdaki bellek akışlarını yineleyin ve bunları ayrı ayrı dosyalara kaydedin.
6. Bu örnek, birden fazla çıktı akışını gerektiği gibi değiştirmenize ve kaydetmenize olanak tanır.

## Çözüm

Aspose.HTML for .NET, EPUB ve HTML belgeleriyle çalışmayı kolaylaştıran çok yönlü bir kütüphanedir. EPUB belgelerini çeşitli görüntü formatlarına dönüştürme yeteneği ve özelleştirilebilir seçenekleriyle geliştiricilere geniş bir uygulama yelpazesi sunar.

---

## Sıkça Sorulan Sorular

### 1. Aspose.HTML for .NET'i nereden indirebilirim?

 Aspose.HTML for .NET'i sürümler sayfasından indirebilirsiniz[Burada](https://releases.aspose.com/html/net/).

### 2. Aspose.HTML for .NET için nasıl geçici lisans alabilirim?

 Geçici lisans almak için geçici lisans sayfasını ziyaret edin[Burada](https://purchase.aspose.com/temporary-license/).

### 3. Aspose.HTML for .NET için ek desteği nerede bulabilirim?

 Sorularınız veya sorunlarınız için destek forumunda Aspose topluluğundan yardım isteyebilirsiniz.[Burada](https://forum.aspose.com/).

### 4. EPUB belgelerini PDF veya XPS gibi diğer formatlara dönüştürebilir miyim?

Evet, EPUB belgelerini PDF ve XPS dahil olmak üzere çeşitli formatlara dönüştürmek için Aspose.HTML for .NET'i kullanabilirsiniz.

### 5. Aspose.HTML for .NET hem küçük hem de büyük ölçekli projeler için uygun mudur?

Kesinlikle! Aspose.HTML for .NET ölçeklenebilir olacak şekilde tasarlanmıştır, bu da onu her boyuttaki proje için mükemmel bir seçim haline getirir.
