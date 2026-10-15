---
category: general
date: 2026-10-15
description: Python'da Markdown kaydetme için kaynak işleme seçeneklerini nasıl oluşturacağınızı
  ve maksimum işleme derinliğini nasıl ayarlayacağınızı öğrenin. Adım adım bir kılavuzu
  izleyin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: tr
lastmod: 2026-10-15
og_description: Python'da iç içe kaynak işleme kontrolü için kaynak işleme seçenekleri
  oluşturun. Bu eğitim, güvenilir Markdown dışa aktarımları için maksimum işleme derinliğini
  nasıl ayarlayacağınızı gösterir.
og_image_alt: Screenshot showing Python code to create resource handling options and
  set max handling depth
og_title: Kaynak işleme seçenekleri oluştur – Python rehberi
schemas:
- author: Aspose
  dateModified: '2026-10-15'
  description: Learn how to create resource handling options and how to set max handling
    depth for Markdown saving in Python. Follow a step‑by‑step guide.
  headline: How to create resource handling options with Python
  type: TechArticle
tags:
- resource handling
- Markdown
- Python
- options
title: Python ile kaynak yönetimi seçenekleri nasıl oluşturulur
url: /tr/python/general/how-to-create-resource-handling-options-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python ile resource handling options nasıl oluşturulur

Markdown dışa aktarımı için **resource handling options** oluşturmanız gerekiyorsa, bu rehber size tam bir çözüm sunar. **max handling depth**'i nasıl ayarlayacağınızı tam olarak göreceksiniz, böylece iç içe kaynaklar istenen seviyeden sonra işlenmeyi durdurur.

Kaynak işleme, görüntüler, gömülü dosyalar veya diğer bağlı varlıkları içeren karmaşık belgelerden Markdown oluştururken çok önemlidir. Kontrolsüz yineleme, performans sorunlarına veya bellek yetersizliği hatalarına yol açabilir. İşleme derinliğini yapılandırarak süreci öngörülebilir ve verimli tutarsınız.

Bu öğreticide şunları yapacaksınız:

* Bir `ResourceHandlingOptions` nesnesi başlatmak.
* Maksimum işleme derinliğini yapılandırmak.
* Seçenekleri bir `MarkdownSaveOptions` örneğine eklemek.
* Projenize kopyalayabileceğiniz tam bir örnek çalıştırmak.

Standart SDK dışındaki harici kütüphaneler gerekmez ve kod, Ekim 2026 itibarıyla Python paketinin en yeni sürümüyle çalışır.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* Python 3.9 veya daha yeni bir sürüm.
* `ResourceHandlingOptions` ve `MarkdownSaveOptions` sağlayan SDK (örneğin `groupdocs-viewer` veya benzeri bir paket). Şu komutla kurun:

```bash
pip install groupdocs-viewer
```

* Python sınıfları ve nesne özellikleri konusunda temel bilgi.

## Adım 1: Resource handling options oluşturma

İlk adım **resource handling options** oluşturmak. Bu nesne, tüm kaynak‑ile ilgili ayarları tutan bir kapsayıcı görevi görür.

```python
from groupdocs.viewer import ResourceHandlingOptions, MarkdownSaveOptions

# Step 1: Instantiate the options object
resource_options = ResourceHandlingOptions()
```

`ResourceHandlingOptions` varsayılan olarak hiçbir sınırlama uygulamaz; bu, görüntüleyicinin karşılaştığı her bağlı kaynağı takip edeceği anlamına gelir. Nesneyi başlatmak, kesin kontroller uygulamak için temiz bir başlangıç sağlar.

## Adım 2: max handling depth nasıl ayarlanır

Şimdi **max handling depth**'i nasıl ayarlayacağınızı öğreneceksiniz. `max_handling_depth` özelliği, dışa aktarıcının durmadan önce işlediği iç içe seviyelerin sayısını tanımlar.

```python
# Step 2: Limit the handling depth to five levels
resource_options.max_handling_depth = 5
```

Neden derinlik sınırlanmalı? Bir Markdown belgesinin başka bir Markdown dosyasına, onun da üçüncü bir dosyaya vb. referans verdiğini hayal edin. Derinlik sınırlaması olmadan dışa aktarıcı sınırsız şekilde yineleme yapabilir, bellek ve CPU tüketebilir. `max_handling_depth` değerini `5` olarak ayarlamak, motorun beş iç içe kaynağın ardından durmasını sağlar; bu, çoğu proje için güvenli bir varsayılandır.

### Özel durum: sınırsız derinlik

Üretim ortamında nadiren ihtiyaç duyulan sınırsız yineleme istiyorsanız, değeri `None` olarak ayarlayın:

```python
resource_options.max_handling_depth = None  # No limit
```

Sınırsız derinliğin çok büyük belge ağaçlarında performans düşüşüne yol açabileceğini unutmayın.

## Adım 3: Seçenekleri MarkdownSaveOptions'a ekleme

Kaynak işleme ayarlarını yaptıktan sonra, bu seçenekleri bir `MarkdownSaveOptions` örneğine eklemelisiniz. Bu, dışa aktarıcının kaydetme sırasında ayarları kullanmasını sağlar.

```python
# Step 3: Create MarkdownSaveOptions and attach the resource handling config
markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options
```

`MarkdownSaveOptions` tüm dışa aktarma‑ile ilgili ayarları toplar. `resource_options` nesnesini `resource_handling_options` özelliğine atayarak, derinlik sınırının dönüşüm sırasında uygulanmasını garantilersiniz.

## Adım 4: Tam bir dönüşüm çalıştırma (isteğe bağlı demo)

Aşağıdaki kod parçacığı, oluşturduğunuz seçenekleri kullanarak örnek bir belgeyi Markdown'a dönüştüren tam bir örnek gösterir. Dosya yollarını ortamınıza göre ayarlayın.

```python
from groupdocs.viewer import Viewer

# Path to the source document (e.g., a DOCX with embedded images)
source_path = "sample.docx"
# Path where the Markdown output will be saved
output_path = "output.md"

# Initialize the viewer with the source file
viewer = Viewer(source_path)

# Perform the conversion using the configured options
viewer.save(output_path, markdown_options)

print(f"Conversion complete. Markdown saved to {output_path}")
```

**Beklenen çıktı**

```
Conversion complete. Markdown saved to output.md
```

Betik çalıştırıldıktan sonra `output.md` dosyasını açın. Görüntülerin ve diğer kaynakların beş seviyeye kadar referans verildiğini, daha derin bağlantıların ise atlandığını göreceksiniz; bu sayede kontrolsüz yineleme önlenir.

## Pro ipucu: İşleme derinliğini çalışma zamanında doğrulama

Derinlik sınırının uygulandığını doğrulamanız gerekiyorsa, oluşturulan Markdown dosyasındaki eksik kaynak referanslarını inceleyebilir veya SDK'da ayrıntılı günlük kaydı (verbose logging) etkinleştirebilirsiniz:

```python
viewer.set_logging(True)  # Enable detailed logs
```

Günlük, aşağıdaki gibi mesajlar gösterecektir:

```
[INFO] Resource handling stopped at depth 5 for file 'nested_image.png'
```

## Yaygın sorular

**Belgemde beşten az iç içe kaynak varsa ne olur?**  
Derinlik sınırı gerçek derinlikten daha yüksek olduğu için dışa aktarıcı mevcut tüm kaynakları işler. Hiçbir kaynak kesilmez.

**Farklı dosya türleri için farklı bir limit belirleyebilir miyim?**  
Evet. Her dışa aktarma formatı için ayrı `ResourceHandlingOptions` nesneleri oluşturup ilgili `SaveOptions` örneğine atayabilirsiniz.

**Derinlik sınırı sadece görüntülere mi uygulanır?**  
Hayır. Sınır, gömülü dosyalar, hiperlinkler ve iç içe Markdown eklemeleri dahil olmak üzere dışa aktarıcının takip edebileceği *tüm* kaynaklara uygulanır.

## Sonuç

Artık **resource handling options** oluşturmayı ve **max handling depth**'i ayarlamayı biliyorsunuz; bu sayede Python’da güvenilir Markdown dışa aktarımları yapabilirsiniz. Yinelemeyi sınırlayarak uygulamanızı aşırı bellek kullanımından korur, aynı zamanda gerekli içerik hiyerarşisini korursunuz.

İleride keşfedebileceğiniz adımlar:

* `extract_images` veya `preserve_links` gibi diğer `ResourceHandlingOptions` özelliklerini ayarlama.
* Çıkarılan dosyalar için özel adlandırma kurallarıyla kaynak işleme birleştirme.
* Belirli belge setleriniz için ideal derinlik değerini bulmak amacıyla farklı derinlik değerleriyle deneme yapma.

Kod parçacıklarını kendi iş akışınıza uyarlamaktan ve bulgularınızı toplulukla paylaşmaktan çekinmeyin. İyi kodlamalar!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla birlikte tam çalışan kod örnekleri içerir; böylece ek API özelliklerini ustalaşabilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [C# ile HTML Kaydetme – Özel Resource Handler Kullanarak Tam Kılavuz](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [C# ile HTML Sıkıştırma – Özel Resource Handler Öğreticisi](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-custom-resource-handler-tutorial/)
- [Java için Aspose.HTML ile özel şema işleyici oluşturma](/html/english/java/custom-schema-message-handling/custom-schema-message-handler/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}