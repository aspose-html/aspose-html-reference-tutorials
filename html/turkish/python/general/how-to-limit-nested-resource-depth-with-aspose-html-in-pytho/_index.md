---
category: general
date: 2026-10-09
description: Python'da Aspose.HTML ResourceHandlingOptions kullanarak iç içe kaynak
  derinliğini sınırlamayı öğrenin. Güvenli HTML dönüşümü için max_handling_depth'i
  kontrol edin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit nested resource depth
- Aspose.HTML ResourceHandlingOptions
- Python resource handling
- max_handling_depth
- nested HTML resources
language: tr
lastmod: 2026-10-09
og_description: Aspose.HTML ResourceHandlingOptions'ı Python'da kullanarak iç içe
  kaynak derinliğini sınırlayın. HTML dönüşüm iş akışınızı korumak için max_handling_depth'i
  ayarlayın.
og_image_alt: Screenshot showing limit nested resource depth setting in Python
og_title: Python'da Aspose.HTML ile iç içe kaynak derinliğini nasıl sınırlarsınız
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Learn to limit nested resource depth using Aspose.HTML ResourceHandlingOptions
    in Python. Control max_handling_depth for safe HTML conversion.
  headline: How to limit nested resource depth with Aspose.HTML in Python
  type: TechArticle
- description: Learn to limit nested resource depth using Aspose.HTML ResourceHandlingOptions
    in Python. Control max_handling_depth for safe HTML conversion.
  name: How to limit nested resource depth with Aspose.HTML in Python
  steps:
  - name: What the setting does
    text: '- **Depth 0** – The root HTML document is processed, but no external resources
      are fetched. - **Depth 1** – Direct resources referenced by the root (e.g.,
      `<img src="...">`, `<link href="...">`) are fetched. - **Depth 2** – Resources
      referenced by the first‑level resources (e.g., CSS files that impo'
  - name: Using the options with a converter
    text: After configuring the depth limit, pass the `resource_options` object to
      the `HtmlConverter` (or any Aspose.HTML API that accepts `ResourceHandlingOptions`).
  - name: 1. Disabling depth limiting entirely
    text: Set the property to a very high number (e.g., `sys.maxsize`) or `None` if
      you want unrestricted handling. Use this only when you trust the source HTML.
  - name: 2. Handling missing resources
    text: When the depth limit stops a resource from being fetched, Aspose.HTML logs
      a warning but continues. You can capture these warnings by attaching a custom
      logger to the converter if you need audit trails.
  - name: 3. Combining with other resource options
    text: '`ResourceHandlingOptions` also offers `allow_external_resources`, `download_timeout`,
      and `max_resource_size`. Pairing a depth limit with a size limit provides a
      robust safety net.'
  - name: 4. Testing the limit
    text: Create a test HTML hierarchy with nested `<iframe>` tags or CSS `@import`
      statements to verify that your depth limit behaves as expected before deploying
      to production.
  type: HowTo
tags:
- Aspose.HTML
- Python
- HTML conversion
- Resource handling
title: Python'da Aspose.HTML ile iç içe kaynak derinliğini nasıl sınırlarsınız
url: /tr/python/general/how-to-limit-nested-resource-depth-with-aspose-html-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da Aspose.HTML ile iç içe kaynak derinliğini sınırlama

Aspose.HTML ile HTML dönüştürürken **iç içe kaynak derinliğini sınırlamanız** gerekiyorsa, bu kılavuz Python'da bunu tam olarak nasıl yapacağınızı gösterir. `max_handling_depth` özelliğini kontrol etmek, bir sayfanın çerçeveler veya bağlı stil sayfaları gibi derinlemesine iç içe kaynaklar içermesi durumunda kontrolsüz özyinelemeyi önler.

Ayrıca bir derinlik sınırı ayarlamanın neden önemli olduğunu öğrenecek, tam kod örneğini görecek ve yaygın tuzaklar ile en iyi uygulama ipuçlarını keşfedeceksiniz. Harici bir dokümantasyona ihtiyaç yok—gereken her şey burada.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

- Python 3.8 ve üzeri yüklü  
- `aspose.html` paketi (`pip install aspose-html`)  
- Aspose.HTML dönüşüm iş akışı hakkında temel bilgi  

Bu öğeler, aşağıdaki örnekler için tek bağımlılıklardır.

## Adım 1: **ResourceHandlingOptions** sınıfını içe aktarın

İlk adım, `ResourceHandlingOptions` sınıfını betiğinize dahil etmektir. Bu sınıf, dış kaynakların (görseller, CSS, scriptler vb.) nasıl alınacağı ve dönüşüm sırasında nasıl işleneceğiyle ilgili tüm seçenekleri gruplar.

```python
# Step 1: Import the ResourceHandlingOptions class
from aspose.html import ResourceHandlingOptions
```

**Neden önemli:**  
`ResourceHandlingOptions`, kaynak‑ile ilgili ayarları diğer dönüşüm seçeneklerinden izole eder; böylece iç içe kaynakların nasıl ele alınacağını, renderlama veya çıktı formatını etkilemeden ince ayar yapabilirsiniz.

## Adım 2: seçenek nesnesinin bir örneğini oluşturun

`ResourceHandlingOptions` nesnesini örnekleyin, böylece özelliklerini değiştirebilirsiniz. Varsayılan örnek sınırsız iç içe geçişe izin verir; bu da kötü niyetli sayfalarda performans sorunlarına ya da yığın taşmalarına yol açabilir.

```python
# Step 2: Create an instance of the options object
resource_options = ResourceHandlingOptions()
```

**İpucu:**  
Aynı derinlik sınırını birçok dönüşümde yeniden kullanmayı planlıyorsanız, yapılandırılmış nesneyi modül‑seviyesinde bir değişkende tutun; böylece her seferinde yeniden oluşturmak zorunda kalmazsınız.

## Adım 3: **max_handling_depth** özelliğini ayarlayarak iç içe kaynak derinliğini sınırlayın

`max_handling_depth` özelliğini, izin vermek istediğiniz en fazla iç içe seviye sayısına ayarlayın. Bu örnekte **3** seviyeden sonra duruyoruz, ancak senaryonuza uygun herhangi bir tamsayı seçebilirsiniz.

```python
# Step 3: Limit the depth of nested resource handling (stop after 3 levels)
resource_options.max_handling_depth = 3
```

### Ayarın yaptığı şey

- **Derinlik 0** – Kök HTML belgesi işlenir, ancak dış kaynaklar alınmaz.  
- **Derinlik 1** – Kök tarafından doğrudan referans verilen kaynaklar (ör. `<img src="...">`, `<link href="...">`) alınır.  
- **Derinlik 2** – Birinci seviye kaynaklar tarafından referans verilen kaynaklar (ör. diğer CSS dosyalarını içe aktaran CSS dosyaları) alınır.  
- **Derinlik 3** – Üçüncü seviye kaynaklar işlendiğinde süreç durur. Daha sonraki iç içe referanslar yok sayılır.

`max_handling_depth` ayarı uygulamanızı şunlardan korur:

| Risk | Sınırlamanın yardımı |
|------|----------------------|
| **Dairesel referanslardan kaynaklanan sonsuz özyineleme** | Dönüştürücü tanımlı derinlikten sonra durur, döngüyü kırar. |
| **Bir sayfanın onlarca zincirli stil sayfası yüklemesiyle oluşan aşırı ağ trafiği** | Yalnızca ilk birkaç seviye indirilir, bant genişliği azalır. |
| **Büyük kaynak ağaçlarının yüklenmesinden kaynaklanan bellek patlaması** | Daha az nesne oluşturulur, bellek kullanımı öngörülebilir kalır. |

### Seçenekleri bir dönüştürücü ile kullanma

Derinlik sınırını yapılandırdıktan sonra `resource_options` nesnesini `HtmlConverter`'a (veya `ResourceHandlingOptions` kabul eden herhangi bir Aspose.HTML API'sine) geçirin.

```python
from aspose.html import HtmlConverter, SaveFormat

# Create a converter with the resource handling options
converter = HtmlConverter(resource_options)

# Convert a sample HTML file to PDF while respecting the depth limit
converter.convert("sample.html", "output.pdf", SaveFormat.PDF)

print("Conversion completed with max_handling_depth =", resource_options.max_handling_depth)
```

**Beklenen çıktı**

```
Conversion completed with max_handling_depth = 3
```

Kaynak HTML üçüncü seviyenin ötesinde kaynaklar içeriyorsa, bu kaynaklar PDF'den çıkarılacak ve dönüşüm yine hızlı bir şekilde tamamlanacaktır.

## Kenar Durumları ve Yaygın Varyasyonlar

### 1. Derinlik sınırlamasını tamamen devre dışı bırakma

Özelliği çok yüksek bir sayıya (ör. `sys.maxsize`) veya sınırsız işleme istiyorsanız `None`'a ayarlayın. Bu seçeneği yalnızca kaynak HTML'e güvendiğinizde kullanın.

```python
import sys
resource_options.max_handling_depth = sys.maxsize  # effectively unlimited
```

### 2. Eksik kaynakları işleme

Derinlik sınırı bir kaynağın alınmasını engellediğinde, Aspose.HTML bir uyarı kaydeder ancak işlem devam eder. Denetim izlerine ihtiyacınız varsa, bu uyarıları dönüştürücüye özel bir logger ekleyerek yakalayabilirsiniz.

### 3. Diğer kaynak seçenekleriyle birleştirme

`ResourceHandlingOptions` ayrıca `allow_external_resources`, `download_timeout` ve `max_resource_size` seçeneklerini sunar. Derinlik sınırını bir boyut sınırıyla birleştirmek, sağlam bir güvenlik ağı sağlar.

```python
resource_options.allow_external_resources = True
resource_options.max_resource_size = 5 * 1024 * 1024  # 5 MiB per resource
```

### 4. Sınırlamayı test etme

Üretime geçmeden önce, iç içe `<iframe>` etiketleri veya CSS `@import` ifadeleri içeren bir test HTML hiyerarşisi oluşturun; böylece derinlik sınırınızın beklendiği gibi çalıştığını doğrulayabilirsiniz.

## Pratik İpuçları (E‑E‑A‑T)

- **Dönüştürmeden önce giriş URL'lerini doğrulayın** gereksiz ağ çağrılarını önlemek için.  
- **Ulaşılan gerçek derinliği kaydedin** (`converter.handling_depth_reached`) izleme için.  
- **Aynı `ResourceHandlingOptions` nesnesini** birden fazla dönüşümde yeniden kullanın, yapılandırmanın tutarlı kalması için.  
- **Derinliği değiştirirken performansı profilleyin**; daha düşük bir limit genellikle dönüşümü hızlandırır ancak gerekli varlıkları atlayabilir.

## Sonuç

Artık Python'da Aspose.HTML ile çalışırken `ResourceHandlingOptions` sınıfının `max_handling_depth` özelliğini yapılandırarak **iç içe kaynak derinliğini sınırlamayı** biliyorsunuz. Bu tek ayar, dönüşüm hattınızı kontrolsüz özyineleme, aşırı ağ kullanımı ve bellek dalgalanmalarına karşı korurken, kaynak ağaçlarının ne kadar derine işleneceği üzerinde ince ayar yapmanızı sağlar.

Daha fazlasını keşfetmeye hazır mısınız? Derinlik sınırını `max_resource_size` ile birleştirerek tamamen dayanıklı bir HTML‑to‑PDF dönüşüm iş akışı oluşturabilir veya **Aspose.HTML kaynak yönetimi** rehberimizi okuyarak `allow_external_resources` ve zaman aşımı yönetimi hakkında daha derin bilgiler edinebilirsiniz.

--- 

*Python'da iç içe kaynak derinliği ayarını gösteren ekran görüntüsü (isteğe bağlı):*  
![Python'da iç içe kaynak derinliği ayarını gösteren ekran görüntüsü](placeholder.png "iç içe kaynak derinliği sınırı")

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalar içeren tam çalışan kod örnekleri sunar; böylece ek API özelliklerini ustalaşabilir ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Aspose HTML'de Özel Kaynak İşleyicisi – Akışa Kaydetme Kılavuzu](/html/english/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/)
- [C#'ta HTML Nasıl Kaydedilir – Özel Kaynak İşleyicisi Kullanarak Tam Kılavuz](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Aspose.HTML'de Java için Mesaj İşleme ve Ağ Yönetimi](/html/english/java/message-handling-networking/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}