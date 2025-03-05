---
title: Aspose.HTML ile .NET'te HTML Şablonlarını Kullanma
linktitle: .NET'te HTML Şablonlarını Kullanma
second_title: Aspose.HTML .NET HTML işleme API'si
description: JSON verilerinden HTML belgelerini dinamik olarak oluşturmak için Aspose.HTML for .NET'i nasıl kullanacağınızı öğrenin. .NET uygulamalarınızda HTML manipülasyonunun gücünden yararlanın.
type: docs
weight: 17
url: /tr/net/advanced-features/using-html-templates/
---

.NET uygulamalarınızda HTML belgeleri ve şablonlarıyla çalışmak istiyorsanız doğru yerdesiniz! Aspose.HTML for .NET, geliştiricilerin HTML belgelerini ve şablonlarını zahmetsizce düzenlemesini sağlayan çok yönlü bir kütüphanedir. Bu eğitimde, Aspose.HTML for .NET'i kullanmanın temellerini ele alacağız, her adımı parçalara ayıracağız ve yol boyunca net bir açıklama sunacağız.

## Ön koşullar

Aspose.HTML for .NET'in ayrıntılarına dalmadan önce, aşağıdaki ön koşulların mevcut olduğundan emin olun:

1. Visual Studio: Makinenizde Visual Studio'nun yüklü olduğundan emin olun. Zaten yüklü değilse web sitesinden indirebilirsiniz.

2.  .NET için Aspose.HTML: Visual Studio projenizde .NET için Aspose.HTML'in yüklü olması gerekir. Bunu şuradan edinebilirsiniz:[belgeleme](https://reference.aspose.com/html/net/).

3. JSON Verileri: HTML şablonunuzu doldurmak için kullanmak istediğiniz bir JSON veri kaynağı hazırlayın. Bu eğitim için aşağıdaki JSON verilerini kullanacağız:

```json
{
    'FirstName': 'John',
    'LastName': 'Smith',
    'Address': {
        'City': 'Dallas',
        'Street': 'Austin rd.',
        'Number': '200'
    }
}
```

4. HTML Şablonu: JSON verileriyle doldurmak istediğiniz bir HTML şablonu oluşturun. İşte basit bir örnek:

```html
<table border=1>
    <tr>
        <th>Person</th>
        <th>Address</th>
    </tr>
    <tr>
        <td>{{FirstName}} {{LastName}}</td>
        <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
    </tr>
</table>
```

## Ad Alanlarını İçe Aktarma

Öncelikle .NET projenize gerekli ad alanlarını aktaralım:

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Loading;
```

Artık ön koşulları ele aldığımıza ve gerekli ad alanlarını içe aktardığımıza göre, her adımı ayrıntılı olarak inceleyelim.

## Adım 1: Bir JSON Veri Kaynağı Hazırlayın

HTML şablonunuza eklemek istediğiniz bilgileri tutan bir JSON veri kaynağı oluşturarak başlayın. Bu örnekte, ön koşullarda belirtildiği gibi bir JSON veri kaynağı hazırladık. Bunu bir dosyaya kaydedin, örneğin, "data-source.json."

```csharp
var data = @"{
    'FirstName': 'John',
    'LastName': 'Smith',
    'Address': {
        'City': 'Dallas',
        'Street': 'Austin rd.',
        'Number': '200'
    }
}";
System.IO.File.WriteAllText("data-source.json", data);
```

Bu kod parçacığı JSON verilerini okur ve "data-source.json" adlı bir dosyaya yazar.

## Adım 2: Bir HTML Şablonu Hazırlayın

Şimdi, JSON verileriyle doldurmak istediğiniz bir HTML şablonu oluşturalım. Bu şablonu "template.html" gibi bir dosyaya kaydedin.

```csharp
var template = @"
<table border=1>
    <tr>
        <th>Person</th>
        <th>Address</th>
    </tr>
    <tr>
        <td>{{FirstName}} {{LastName}}</td>
        <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
    </tr>
</table>
";
System.IO.File.WriteAllText("template.html", template);
```

 Bu HTML şablonu şu gibi yer tutucuları içerir:`{{FirstName}}`, `{{LastName}}`, `{{Address.Street}}`, `{{Address.Number}}` Ve`{{Address.City}}`Bunu gerçek verilerle değiştireceğiz.

## Adım 3: HTML Şablonunu Doldurun

 Son olarak, şunu çağırın:`Converter.ConvertTemplate` HTML şablonunuzu JSON kaynağındaki verilerle doldurma yöntemi.

```csharp
Aspose.Html.Converters.Converter.ConvertTemplate(
"template.html", new Aspose.Html.Converters.TemplateData("data-source.json"), new Aspose.Html.Loading.TemplateLoadOptions(), "document.html"
);
```

Bu kod "template.html" dosyasını alır, yer tutucuları karşılık gelen JSON değerleriyle değiştirir ve sonucu "document.html" dosyasına kaydeder.

Tebrikler! Aspose.HTML for .NET'in gücünden yararlanarak JSON verilerinden dinamik olarak HTML belgeleri ürettiniz.

## Çözüm

Bu eğitimde, HTML belgelerini dinamik olarak oluşturmak için .NET için Aspose.HTML kullanmanın temellerini inceledik. Ön koşulları, ad alanlarını içe aktarmayı ve her adımı ayrıntılı olarak ele aldık. Bu adımları izleyerek, HTML belge oluşturmayı .NET uygulamalarınıza sorunsuz bir şekilde entegre edebilirsiniz.

## SSS

### S1. .NET için Aspose.HTML nedir?

A1: Aspose.HTML for .NET, .NET geliştiricilerinin HTML belgeleri ve şablonlarıyla programatik olarak çalışmasını sağlayan güçlü bir kütüphanedir. HTML oluşturma, dönüştürme ve düzenleme gibi görevleri basitleştirir.

### S2. Aspose.HTML for .NET'in belgelerini nerede bulabilirim?

 A2: .NET için Aspose.HTML belgelerine erişebilirsiniz[Burada](https://reference.aspose.com/html/net/)API referansları ve kod örnekleri de dahil olmak üzere kapsamlı bilgiler sağlar.

### S3. Aspose.HTML for .NET'i nasıl indirebilirim?

A3: .NET için Aspose.HTML'yi indirme sayfasından indirebilirsiniz[Burada](https://releases.aspose.com/html/net/).

### S4. Aspose.HTML for .NET için ücretsiz deneme sürümü mevcut mu?

 C4: Evet, Aspose.HTML for .NET'i ücretsiz deneme sürümünü indirerek deneyebilirsiniz.[Burada](https://releases.aspose.com/).

### S5. Aspose.HTML for .NET için geçici bir lisansa ihtiyacım var mı?

 A5: Değerlendirme amaçlı geçici bir lisansa ihtiyacınız varsa, bunu şu adresten alabilirsiniz:[Burada](https://purchase.aspose.com/temporary-license/).