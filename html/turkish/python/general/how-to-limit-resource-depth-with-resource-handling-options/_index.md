---
category: general
date: 2026-10-25
description: Python kullanarak büyük HTML dosyalarını kaydederken kaynak derinliğini
  sınırlamayı ve kaynak yönetimini uygulamayı öğrenin. Güvenilir sonuçlar için bu
  adım adım rehberi izleyin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit resource depth
- apply resource handling
- HTML document processing
- save options Python
- resource handling options
language: tr
lastmod: 2026-10-25
og_description: Python ile HTML kaydederken kaynak derinliğini sınırlayın ve kaynak
  işleme uygulayın. Bu öğretici, tam ve çalıştırılabilir bir çözümü gösterir.
og_image_alt: Screenshot illustrating limit resource depth in a Python script
og_title: Kaynak işleme uygularken kaynak derinliğini sınırlayın – Python rehberi
schemas:
- author: GroupDocs
  dateModified: '2026-10-25'
  description: Learn how to limit resource depth and apply resource handling when
    saving large HTML files using Python. Follow this step‑by‑step guide for reliable
    results.
  headline: How to limit resource depth with resource handling options
  type: TechArticle
- description: Learn how to limit resource depth and apply resource handling when
    saving large HTML files using Python. Follow this step‑by‑step guide for reliable
    results.
  name: How to limit resource depth with resource handling options
  steps:
  - name: '**Dynamic content loaded via JavaScript** – The parser only sees static
      HTML. If your page relies on scripts that inject further resources, those will
      never be counted toward the depth limit. Consider pre‑rendering the page with
      a headless browser before applying the limit.'
    text: '**Dynamic content loaded via JavaScript** – The parser only sees static
      HTML. If your page relies on scripts that inject further resources, those will
      never be counted toward the depth limit. Consider pre‑rendering the page with
      a headless browser before applying the limit.'
  - name: '**Circular references** – Some pages include iframes that point back to
      the same page. The depth counter prevents infinite loops, but you may still
      see partially rendered sections. Adjust `max_handling_depth` or manually exclude
      problematic frames.'
    text: '**Circular references** – Some pages include iframes that point back to
      the same page. The depth counter prevents infinite loops, but you may still
      see partially rendered sections. Adjust `max_handling_depth` or manually exclude
      problematic frames.'
  - name: '**Mixed protocols (http/https)** – If resources use different schemes,
      the library may treat them as separate domains. The depth limit still applies
      across protocols, but network permissions might differ. Ensure your environment
      permits both.'
    text: '**Mixed protocols (http/https)** – If resources use different schemes,
      the library may treat them as separate domains. The depth limit still applies
      across protocols, but network permissions might differ. Ensure your environment
      permits both.'
  type: HowTo
tags:
- Python
- HTML
- File handling
title: Kaynak işleme seçenekleriyle kaynak derinliğini sınırlama
url: /tr/python/general/how-to-limit-resource-depth-with-resource-handling-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kaynak derinliğini sınırlama ve kaynak işleme seçeneklerini uygulama

Eğer büyük bir HTML dosyasını işlerken **kaynak derinliğini sınırlamanız** gerekiyorsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. Eğitim sonunda **kaynak işleme** uygulayarak kaydetme işleminin derinlik sınırına saygı göstermesini ve kontrol dışı işleme yol açmamasını da öğreneceksiniz.

Büyük HTML sayfaları genellikle çok sayıda dış kaynak—görseller, betikler, stil sayfaları ve iç içe geçmiş iframe’ler—barındırır. Derinlik sınırı olmadan ayrıştırıcı her bağlantıyı takip edebilir, bu da bellek kullanımını ve işleme süresini dramatik şekilde artırır. Burada açıklanan teknik, işlemi hızlı ve öngörülebilir tutar.

## Önkoşullar

Başlamadan önce şunların kurulu olduğundan emin olun:

* Python 3.9+ yüklü.
* `groupdocs-viewer` (veya benzer bir HTML işleme kütüphanesi) `pip install groupdocs-viewer` ile erişilebilir.
* Bilinen bir dizinde bulunan örnek HTML dosyası (`big_page.html`).
* Çıktı dizinine yazma izni.

Bu öğeler, kodun ek yapılandırma gerektirmeden çalışmasını sağlar.

## Adım 1: Kaynak HTML belgesini yükleyin

İlk adım, orijinal dosyaya işaret eden bir `HTMLDocument` örneği oluşturmaktır. Nesne, tüm HTML yapısını temsil eder ve daha sonra kaydetme seçeneklerine erişim sağlar.

```python
# Step 1: Load the source HTML document
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

*Neden önemli*: Dosyayı bir kez yüklemek, kütüphaneye sonraki tüm işlemler için tek bir giriş noktası verir. Ayrıca dosyanın varlığını doğrular, yol hatalıysa erken bir hata fırlatır.

## Adım 2: Kaynak işleme seçeneklerini oluşturun ve işleme derinliğini sınırlayın

`ResourceHandlingOptions`, kütüphanenin bağlı kaynakları ne kadar derine kadar tarayacağını kontrol etmenizi sağlar. `max_handling_depth` değerini düşük bir sayıya (ör. 5) ayarlamak, motorun beş katmanlık iç içe geçmişlikten sonra bağlantıları takip etmeyi durdurmasını söyler.

```python
# Step 2: Create resource handling options and limit the processing depth
resource_opts = ResourceHandlingOptions()
resource_opts.max_handling_depth = 5  # Restricts handling to 5 levels deep
```

*Neden önemli*: **Kaynak derinliğini sınırlayarak**, ayrıştırıcının dolaylı olarak referans verilen her görseli, betiği veya iframe’i indirmesini engellersiniz. Bu, özellikle üçüncü‑taraf içerik barındıran sayfalarda ağ trafiğini ve bellek baskısını azaltır.

## Adım 3: Kaynak seçeneklerini kaydetme seçeneklerine ekleyin

`SaveOptions`, çıktı dosyasını etkileyen tüm ayarları toplar. `resource_handling_options` atamasıyla, yaklaşan kaydetme işlemi için **kaynak işleme** uygulanır.

```python
# Step 3: Attach the resource options to the save options
save_opts = SaveOptions()
save_opts.resource_handling_options = resource_opts
```

*Neden önemli*: `save_opts` nesnesi, birden çok bayrağı (sıkıştırma, format vb.) içeren bir kapsayıcı görevi görür. `resource_handling_options` eklemek, yazma aşamasında derinlik sınırının göz önünde bulundurulmasını sağlar.

## Adım 4: Sınırlı kaynak işleme ile belgeyi kaydedin

Son olarak, yapılandırılmış `save_opts` ile `doc.save()` metodunu çağırın. Çıktı dosyası, tanımlı derinlik içinde kalan kaynakları içerir.

```python
# Step 4: Save the document with the limited resource handling applied
doc.save("YOUR_DIRECTORY/big_page_limited.html", save_opts)
```

**Beklenen sonuç**:  
`big_page_limited.html` adlı yeni bir dosya `YOUR_DIRECTORY` içinde ortaya çıkar. Bir tarayıcıda açtığınızda orijinal düzeni görürsünüz, ancak beş seviyenin ötesindeki tüm kaynaklar atlanmıştır. Sayfa daha hızlı yüklenir ve çok daha az bellek tüketir.

## Kaydedilen HTML’yi doğrulayın

Kaydetme işleminden sonra, derinlik sınırının saygı gösterildiğini doğrulamak iyi bir uygulamadır.

```python
# Verify that the saved file exists and its size is reasonable
import os

output_path = "YOUR_DIRECTORY/big_page_limited.html"
if os.path.isfile(output_path):
    size_kb = os.path.getsize(output_path) / 1024
    print(f"Saved file size: {size_kb:.2f} KB")
else:
    raise FileNotFoundError("The limited HTML file was not created.")
```

Eğer boyut, orijinal dosyadan (yüzlerce kilobayt olabilen) belirgin şekilde daha küçükse, **kaynak derinliğini sınırlama** ayarı istenildiği gibi çalışmış demektir.

## Yaygın tuzaklar ve nasıl önlenir

| Belirti | Neden | Çözüm |
|---------|-------|-----|
| Dosya boyutunda değişiklik yok | `max_handling_depth` varsayılan (sınırsız) bırakılmış | `resource_opts.max_handling_depth` değerini < ∞ bir sayıya açıkça ayarlayın |
| Sayfada eksik görseller | Kaynaklar derinlik sınırının ötesindeydi | Derinliği artırın veya kritik kaynakları daha sığ bir seviyeye taşıyın |
| Kaydetmede `PermissionError` | Çıktı dizini salt‑okunur | Yazılabilir bir dizin seçin veya OS izinlerini düzenleyin |
| Beklenmeyen `ResourceHandlingException` | Kütüphane sürümü uyumsuzluğu | En son `groupdocs-viewer` sürümüne yükseltin (`pip install --upgrade groupdocs-viewer`) |

**İpucu**: Çok büyük sayfalar için önce derinliği 3 olarak ayarlayın ve görsel bütünlük istediğiniz seviyeye ulaşana kadar kademeli olarak artırın.

## Karşılaşabileceğiniz uç durumlar

1. **JavaScript ile dinamik içerik yüklenmesi** – Ayrıştırıcı yalnızca statik HTML’i görür. Sayfanız daha fazla kaynak ekleyen betikler kullanıyorsa, bu kaynaklar derinlik sınırına dahil edilmez. Sınırı uygulamadan önce sayfayı başsız bir tarayıcıyla ön‑renderlemeyi düşünün.
2. **Döngüsel referanslar** – Bazı sayfalar aynı sayfaya geri işaret eden iframe’ler içerir. Derinlik sayacı sonsuz döngüleri önler, ancak yine de kısmen render edilmiş bölümler görebilirsiniz. `max_handling_depth` değerini ayarlayın veya sorunlu çerçeveleri manuel olarak hariç tutun.
3. **Karışık protokoller (http/https)** – Kaynaklar farklı şemalar kullanıyorsa, kütüphane bunları ayrı domainler gibi ele alabilir. Derinlik sınırı protokoller arasında da geçerlidir, ancak ağ izinleri farklı olabilir. Ortamınızın her iki protokolü de desteklediğinden emin olun.

## İleri seviye kaynak işleme: sonraki adımlar

Artık **kaynak derinliğini sınırlayabildiğinize** ve **kaynak işleme uygulayabildiğinize** göre, aşağıdakileri keşfetmek isteyebilirsiniz:

* **Özel filtreler** – `resource_opts.resource_filter` kullanarak belirli dosya tiplerini (ör. büyük videolar) atlayın.
* **Sıkıştırma ayarları** – `SaveOptions` ile `compression_level` birleştirerek çıktıyı daha da küçültün.
* **Toplu işleme** – Bir dizindeki HTML dosyaları üzerinde döngü kurarak aynı derinlik sınırını her birine uygulayın.

Bu eklemeler, büyük ölçekli belge iş akışları için tam bir HTML optimizasyon hattı oluşturmanızı sağlar.

## Sonuç

Python ile büyük bir HTML belgesini kaydederken **kaynak derinliğini sınırlamayı** ve **kaynak işleme uygulamayı** öğrendiniz. `ResourceHandlingOptions` yapılandırıp bunları `SaveOptions`’a ekleyerek, işlenecek iç içe geçmiş kaynak sayısı üzerinde ince ayar yapabilir, daha hızlı kaydetmeler ve daha küçük çıktı dosyaları elde edebilirsiniz. Farklı derinlik değerleri ve ek `SaveOptions` ile deneyler yaparak davranışı projenizin ihtiyaçlarına göre özelleştirin.


## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki eğitimler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir; böylece ek API özelliklerini öğrenebilir ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [How to Set max_handling_depth in Aspose.HTML Python – Complete Guide](/html/english/python/general/how-to-set-max-handling-depth-in-aspose-html-python-complete/)
- [Create resource handling options and load an HTML document in Python](/html/english/python/general/create-resource-handling-options-and-load-an-html-document-i/)
- [How to Save HTML with Controlled Depth – Step‑by‑Step Python Guide](/html/english/python/general/how-to-save-html-with-controlled-depth-step-by-step-python-g/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}