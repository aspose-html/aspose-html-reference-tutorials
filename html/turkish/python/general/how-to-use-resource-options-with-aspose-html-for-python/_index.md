---
category: general
date: 2026-08-09
description: Aspose.HTML for Python'da kaynak işleme seçeneklerini nasıl kullanılır.
  Maksimum işleme derinliğini ayarlamayı ve büyük HTML sayfalarını verimli bir şekilde
  yüklemeyi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use resource
- resource handling options
- max handling depth
- Aspose.HTML for Python
- HTMLDocument loading
language: tr
lastmod: 2026-08-09
og_description: Aspose.HTML for Python'da kaynak işleme seçeneklerini nasıl kullanılır.
  Bu öğretici, maksimum işleme derinliğini yapılandırmayı ve büyük HTML dosyalarını
  güvenli bir şekilde yüklemeyi adım adım gösterir.
og_image_alt: Diagram illustrating how to use resource handling options in Aspose.HTML
  for Python
og_title: Aspose.HTML for Python ile kaynak seçeneklerini nasıl kullanılır – tam rehber
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: How to use resource handling options in Aspose.HTML for Python. Learn
    to set max handling depth and load large HTML pages efficiently.
  headline: How to use resource options with Aspose.HTML for Python
  type: TechArticle
- description: How to use resource handling options in Aspose.HTML for Python. Learn
    to set max handling depth and load large HTML pages efficiently.
  name: How to use resource options with Aspose.HTML for Python
  steps:
  - name: Import the required classes
    text: '```python from aspose.html import HTMLDocument, ResourceHandlingOptions
      ```'
  - name: Create a `ResourceHandlingOptions` object
    text: '```python # Step 2: Instantiate the options container resource_options
      = ResourceHandlingOptions() ```'
  - name: Set the maximum handling depth
    text: '```python # Step 3: Limit recursion to 5 levels of nested resources resource_options.max_handling_depth
      = 5 ```'
  - name: Load the HTML document with the configured options
    text: '```python # Step 4: Load the document using the options we just configured
      doc = HTMLDocument("YOUR_DIRECTORY/bigpage.html", resource_options) ```'
  - name: Verify that the document loaded correctly
    text: '```python # Step 5: Simple sanity check – print the document title print("Document
      title:", doc.title) ```'
  - name: Optional – handle missing resources gracefully
    text: '```python # Step 6: Attach an event handler to log missing resources def
      on_resource_not_found(sender, args): print(f"Resource not found: {args.resource_url}")'
  - name: Clean up
    text: '```python # Step 7: Release native resources when done doc.dispose() ```'
  - name: Pro tip
    text: When processing many HTML files in a batch, reuse a single `ResourceHandlingOptions`
      instance. Creating it once reduces object‑allocation overhead and guarantees
      consistent settings across all documents.
  type: HowTo
tags:
- Aspose.HTML
- Python
- HTML processing
- resource handling
title: Aspose.HTML for Python ile kaynak seçeneklerini nasıl kullanılır
url: /tr/python/general/how-to-use-resource-options-with-aspose-html-for-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML for Python ile kaynak seçeneklerini nasıl kullanılır

Aspose.HTML for Python ile **kaynakları nasıl kullanılır** işleme seçeneklerini merak ediyorsanız, bu öğretici size eksiksiz, doğrudan çalıştırılabilir bir çözüm sunar. `ResourceHandlingOptions` nasıl yapılandırılır, maksimum işleme derinliği nasıl sınırlanır ve büyük bir HTML sayfası belleği tüketmeden nasıl yüklenir öğrenebileceksiniz.

İşlemeli web sayfaları genellikle birçok iç içe kaynak çeker—stil sayfaları, görseller, betikler ve iframe'ler. Uygun sınırlamalar olmadan, yükleyici süresiz olarak yinelemeye devam edebilir ve performans sorunları ya da çöküşlere yol açabilir. Bu rehberin sonunda şunları yapabilecek durumdasınız:

* Bir `ResourceHandlingOptions` örneği oluşturun.
* `max_handling_depth` değerini güvenli bir seviyeye ayarlayın.
* Bu seçeneklerle bir `HTMLDocument` yükleyin.
* Eksik kaynaklar veya daha derin iç içe yapılar gibi yaygın kenar durumlarını yönetin.

Aspose.HTML for Python kütüphanesi ve standart bir Python 3 ortamı dışında dış araçlara ihtiyaç yoktur.

## Önkoşullar

* Python 3.8 veya daha yeni bir sürüm kurulu.
* Aspose.HTML for Python paketi (`aspose-html`) kurulu (`pip install aspose-html`).
* İç içe kaynaklar içeren bir örnek HTML dosyası (ör. `bigpage.html`).
* Python sözdizimi ve nesne‑yönelimli programlamaya temel aşinalık.

## Kaynak işleme seçeneklerini nasıl kullanılır – adım adım

### Adım 1: Gerekli sınıfları içe aktarın

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions
```

**Neden Önemli:**  
`HTMLDocument` HTML içeriğini yüklemek ve manipüle etmek için giriş noktasını oluşturur. `ResourceHandlingOptions` dış kaynakların nasıl getirileceğini, önbelleğe alınacağını veya yok sayılacağını kontrol etmenizi sağlar. Bu sınıfları dosyanın başında içe aktarmak kodu düzenli tutar ve Python en iyi uygulamalarına uyar.

### Adım 2: Bir `ResourceHandlingOptions` nesnesi oluşturun

```python
# Step 2: Instantiate the options container
resource_options = ResourceHandlingOptions()
```

**Neden Önemli:**  
Seçenek nesnesi bir yapılandırma çantası gibi davranır. Daha sonra bir `HTMLDocument` yapıcısına ekleyebilir ve böylece her kaynak isteği tanımladığınız ayarları uygular.

### Adım 3: Maksimum işleme derinliğini ayarlayın

```python
# Step 3: Limit recursion to 5 levels of nested resources
resource_options.max_handling_depth = 5
```

**Neden Önemli:**  
`max_handling_depth`, bir sayfanın kaynakları gömmesi ve bu kaynakların da başka kaynaklar gömmesi durumunda sonsuz yinelemeyi önler. Çoğu gerçek dünyadaki sayfa için **5** güvenli bir varsayılan değerdir, ancak senaryonuza göre değeri ayarlayabilirsiniz. Derinliği **0** olarak ayarlarsanız, yükleyici tüm dış kaynakları atlayacak ve bu, sadece metin çıkarımı için faydalı olabilir.

### Adım 4: HTML belgesini yapılandırılmış seçeneklerle yükleyin

```python
# Step 4: Load the document using the options we just configured
doc = HTMLDocument("YOUR_DIRECTORY/bigpage.html", resource_options)
```

**Neden Önemli:**  
`resource_options` nesnesini `HTMLDocument` yapıcısına geçirmek, kütüphaneye belirlediğiniz `max_handling_depth` değerine uymasını söyler. Belge artık tamamen ayrıştırıldı ve beşinci seviyenin üzerindeki tüm kaynaklar yok sayılarak bellek kullanımının öngörülebilir olması sağlanır.

### Adım 5: Belgenin doğru yüklendiğini doğrulayın

```python
# Step 5: Simple sanity check – print the document title
print("Document title:", doc.title)
```

**Neden Önemli:**  
Kısa bir kontrol, HTML'in ölümcül hatalar olmadan ayrıştırıldığını doğrular. Başlık `None` olarak yazdırılırsa, dosya eksik ya da hatalı olabilir ve istisnayı ele almanız gerekir (aşağıdaki “Hata yönetimi” bölümüne bakın).

### Adım 6: İsteğe Bağlı – eksik kaynakları sorunsuz şekilde yönetin

```python
# Step 6: Attach an event handler to log missing resources
def on_resource_not_found(sender, args):
    print(f"Resource not found: {args.resource_url}")

resource_options.resource_not_found += on_resource_not_found
```

**Neden Önemli:**  
Aspose.HTML, bağlı bir varlık alınamadığında `resource_not_found` olayını tetikler. Bu olayları kaydetmek, kırık bağlantıları teşhis etmenize veya alternatifler sunup sunmayacağınıza karar vermenize yardımcı olur.

### Adım 7: Temizleme

```python
# Step 7: Release native resources when done
doc.dispose()
```

**Neden Önemli:**  
`HTMLDocument` yönetilmeyen kaynakları (ör. yerel bellek tamponları) tutar. Nesneyi açıkça dispose etmek bu kaynakları hızlıca serbest bırakır; bu, uzun süre çalışan hizmetlerde veya toplu işlerde özellikle önemlidir.

## Tam çalıştırılabilir örnek

Aşağıda, yukarıdaki tüm adımları içeren tam script yer almaktadır. `"YOUR_DIRECTORY/bigpage.html"` ifadesini HTML dosyanızın gerçek yolu ile değiştirin.

```python
# ------------------------------------------------------------
# Complete example: how to use resource handling options
# with Aspose.HTML for Python
# ------------------------------------------------------------

from aspose.html import HTMLDocument, ResourceHandlingOptions

# 1️⃣ Create and configure the options
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 5  # stop after 5 levels

# 2️⃣ Optional: log missing resources
def on_resource_not_found(sender, args):
    print(f"[WARN] Missing resource: {args.resource_url}")

resource_options.resource_not_found += on_resource_not_found

# 3️⃣ Load the document using the configured options
doc_path = "YOUR_DIRECTORY/bigpage.html"
doc = HTMLDocument(doc_path, resource_options)

# 4️⃣ Verify load
print("Document title:", doc.title)

# 5️⃣ Perform any additional processing here
#    (e.g., extract text, manipulate DOM, render to PDF, etc.)

# 6️⃣ Clean up
doc.dispose()
```

**Beklenen çıktı (HTML bir `<title>` etiketi içeriyorsa):**

```
Document title: Sample Big Page
```

Eğer herhangi bir kaynak eksikse, aşağıdaki gibi uyarı satırları göreceksiniz:

```
[WARN] Missing resource: https://example.com/missing-image.png
```

## Kenar durumları ve en iyi uygulama ipuçları

| Durum | Önerilen işlem |
|-----------|----------------------|
| **Gerekli derinlik 5'ten daha derin** | `max_handling_depth` değerini gereken seviyeye artırın, ancak bir profil aracıyla bellek kullanımını izleyin. |
| **Dairesel kaynak referansları** | Derinlik sınırı otomatik olarak döngüleri keser; API sürümü destekliyorsa `resource_options.enable_circular_reference_detection = True` ayarını da yapabilirsiniz. |
| **Büyük ikili kaynaklar (ör. yüksek çözünürlüklü görüntüler)** | Her indirilen varlığın boyutunu sınırlamak için `resource_options.max_resource_size` kullanın. |
| **Ağ zaman aşımı** | Yavaş sunucularda takılmayı önlemek için `resource_options.request_timeout` (saniye cinsinden) ayarlayın. |
| **Kısıtlı bir ortamda çalışmak (internet yok)** | Tüm uzaktan çekmeleri atlamak için `resource_options.enable_external_resources = False` ayarlayın. |

### Pro ipucu

Bir toplu işlemde birçok HTML dosyasını işlerken tek bir `ResourceHandlingOptions` örneğini yeniden kullanın. Bir kez oluşturmak nesne tahsis yükünü azaltır ve tüm belgeler için tutarlı ayarları garanti eder.

## Yaygın sorular

**S: `max_handling_depth` satır içi kaynakları (ör. `<style>` etiketleri) etkiler mi?**  
C: Hayır. Satır içi kaynaklar orijinal HTML'nin bir parçasıdır ve her zaman işlenir. Derinlik sınırı yalnızca ek HTTP istekleri gerektiren dış kaynaklara uygulanır.

**

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalar içeren eksiksiz çalışan kod örnekleri sunar; böylece ek API özelliklerini öğrenebilir ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Add Handler with Aspose.HTML for Java](/html/english/java/message-handling-networking/custom-message-handler/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}