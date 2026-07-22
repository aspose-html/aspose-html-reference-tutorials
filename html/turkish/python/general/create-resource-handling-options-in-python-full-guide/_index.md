---
category: general
date: 2026-07-21
description: Python'da kaynak işleme seçenekleri oluşturun ve HTML ayrıştırması için
  maksimum işleme derinliğini nasıl ayarlayacağınızı öğrenin. Güvenilir kaynak yönetimi
  için bu adım adım öğreticiyi izleyin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: tr
lastmod: 2026-07-21
og_description: Python'da kaynak işleme seçenekleri oluşturun ve güvenli HTML belge
  yüklemesi için maksimum işleme derinliğini nasıl ayarlayacağınızı anında görün.
  Tekniği dakikalar içinde öğrenin.
og_image_alt: Screenshot of Python code that creates resource handling options with
  max handling depth set
og_title: Python'da Kaynak İşleme Seçenekleri Oluşturun – Tam Adım Adım Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  headline: Create Resource handling options in Python – Full Guide
  type: TechArticle
- description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  name: Create Resource handling options in Python – Full Guide
  steps:
  - name: Circular References
    text: 'Some legacy sites embed an iframe that points back to the original page,
      creating a loop. With `max_handling_depth` set, the loop is automatically broken
      after the third iteration. However, you might still see a warning in the logs.
      To silence noisy logs, adjust the logger level:'
  - name: Missing Resources
    text: 'If a nested resource fails to load (404 or network timeout), the parser
      throws an exception by default. Wrap the loading call in a `try/except` block
      to keep your application alive:'
  - name: Adjusting Depth Dynamically
    text: 'Sometimes you need different depths for different parts of your pipeline.
      Because `resource_options` is a mutable object, you can change `max_handling_depth`
      on the fly:'
  type: HowTo
tags:
- Python
- HTML parsing
- resource management
title: Python'da Kaynak Yönetimi Seçenekleri Oluşturma – Tam Rehber
url: /tr/python/general/create-resource-handling-options-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da Kaynak İşleme Seçenekleri Oluşturma – Tam Kılavuz

Devasa bir HTML sayfası için **kaynak işleme seçenekleri** oluşturmanın belleğinizi tüketmeden nasıl yapılacağını hiç merak ettiniz mi? Tek başınıza değilsiniz. Devasa bir belgeyi bir ayrıştırıcıya verdiğinizde, çerçeveler, iframe'ler veya bağlanmış CSS gibi iç içe kaynaklar hızla kontrol dışına çıkabilir.  

İyi haber? Ayrıştırıcıya belirli bir iç içeleme seviyesinden sonra durmasını söyleyebilirsiniz. Bu öğreticide **max handling depth** nasıl ayarlanır ve uygulamanızın yanıt verebilir kalması gösterilecektir. Hazır mısınız? Hadi başlayalım.

## Öğrenecekleriniz

- Neden iç içeleme derinliğini sınırlamanın performans ve güvenlik açısından önemli olduğu.  
- `ResourceHandlingOptions` sınıfını kullanarak **kaynak işleme seçenekleri** oluşturmak için gereken tam kod.  
- Ayrıştırıcının üç seviyeden sonra durması için `max_handling_depth` nasıl yapılandırılır.  
- Döngüsel referanslar veya eksik kaynaklar gibi belgeler için kenar durumlarını ele alma ipuçları.  

Kütüphane ile ilgili önceden bir deneyim gerekmez—sadece çalışan bir Python 3 kurulumu ve dosya G/Ç temelleri hakkında temel bir anlayış yeterlidir.

## Önkoşullar

- Python 3.8+ (kütüphane tüm yeni sürümlerde çalışır).  
- `HTMLDocument` ve `ResourceHandlingOptions` sağlayan `htmlparser` paketi.  
- Referans alabileceğiniz bir klasöre yerleştirilmiş örnek bir HTML dosyası (`big_page.html`).  

Henüz paketi kurmadıysanız, şu komutu çalıştırın:

```bash
pip install htmlparser
```

Temel hazırlıklar tamamlandığına göre, konunun özüne geçelim.

## Kaynak İşleme Seçenekleri Oluşturma – Adım 1

İlk olarak, bir `ResourceHandlingOptions` örneğine ihtiyacınız var. Bunu, ayrıştırıcının uyması gereken sınırlamaları ve politikaları ayarlayabileceğiniz bir araç kutusu gibi düşünün.

```python
# Step 1: Create resource handling options and limit nesting depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after three levels of nested resources
```

**Neden önemli:**  
Ayrıştırıcı bir `<iframe>` içinde başka bir `<iframe>` ile karşılaştığında, normalde zinciri sonsuza kadar takip eder. Derinliği `3` ile sınırlayarak, RAM'i tüketebilecek veya yığın taşmasına neden olabilecek kontrolsüz bir yinelemeyi önlersiniz.

> **Pro ipucu:** Güvenilmeyen içerik (ör. kullanıcı‑yüklediği HTML) ayrıştırıyorsanız, olası saldırıları azaltmak için derinliği `1` veya `2`'ye düşürmeyi düşünün.

## HTML Belgesini Yükleme – Adım 2

Seçenek nesneniz hazır olduğunda, onu `HTMLDocument`'e geçirin. Yapıcı, az önce ayarladığınız `max_handling_depth` değerine saygı gösterecektir.

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
```

**Arka planda ne oluyor?**  
`HTMLDocument` dosyayı okur, bir DOM ağacı oluşturur ve ardından her dış kaynağı (stil sayfaları, betikler, görüntüler) dolaşır. İç içe bir kaynakla karşılaştığında `resource_options.max_handling_depth` değerini kontrol eder. Limit aşıldığında, ayrıştırıcı bir uyarı kaydeder ve daha fazla iç içelemeyi atlar.

Bu, ilk üç katman için tamamen kullanılabilir bir DOM elde ettiğiniz ve geri kalanının güvenli bir şekilde yok sayıldığı anlamına gelir.

## Yapılandırmayı Doğrulama – Adım 3

Ayarlarınızın etkili olduğunu doğrulamak her zaman iyi bir fikirdir. `resource_options` nesnesi mevcut durumunu ortaya koyar, böylece çıktısını alabilir veya bir testte doğrulayabilirsiniz.

```python
# Step 3: Verify that the max handling depth is set correctly
assert resource_options.max_handling_depth == 3, "Depth limit not applied!"

print(f"Resource handling options configured: max depth = {resource_options.max_handling_depth}")
```

Eğer doğrulama geçerse, ayrıştırıcının çalışmanın geri kalanında limiti uygulayacağından emin olabilirsiniz.

## Kenar Durumlarını Ele Alma

### Döngüsel Referanslar

Bazı eski siteler, orijinal sayfaya geri yönlendiren bir iframe gömer ve bir döngü oluşturur. `max_handling_depth` ayarlandığında, döngü üçüncü yinelemeden sonra otomatik olarak kırılır. Ancak, günlüklerde hâlâ bir uyarı görebilirsiniz. Gürültülü günlükleri sessize almak için logger seviyesini ayarlayın:

```python
import logging
logging.getLogger("htmlparser").setLevel(logging.ERROR)
```

### Eksik Kaynaklar

İç içe bir kaynak yüklenemezse (404 veya ağ zaman aşımı), ayrıştırıcı varsayılan olarak bir istisna fırlatır. Uygulamanızın çalışmaya devam etmesi için yükleme çağrısını bir `try/except` bloğuna sarın:

```python
try:
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
except Exception as e:
    print(f"Failed to load a nested resource: {e}")
    # Fallback: load the document without additional resources
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

### Derinliği Dinamik Olarak Ayarlama

Bazen pipeline'ınızın farklı bölümleri için farklı derinlikler gerekir. `resource_options` değiştirilebilir bir nesne olduğu için, `max_handling_depth` değerini anlık olarak değiştirebilirsiniz:

```python
resource_options.max_handling_depth = 5   # Temporarily allow deeper nesting
html_doc_deep = HTMLDocument("deep_page.html", resource_options)

resource_options.max_handling_depth = 2   # Tighten for a lightweight preview
html_doc_preview = HTMLDocument("preview.html", resource_options)
```

Sadece aynı seçenek örneğini başka bir iş parçacığında yeniden kullanmadan önce değeri sıfırlamayı unutmayın.

## Tam Çalışan Örnek

Aşağıda, kopyalayıp yapıştırabileceğiniz, dosya yollarını ayarlayabileceğiniz ve hemen çalıştırabileceğiniz tam bir betik bulunmaktadır.

```python
import logging
from htmlparser import HTMLDocument, ResourceHandlingOptions

# Optional: Reduce noisy output
logging.getLogger("htmlparser").setLevel(logging.ERROR)

def load_document(path: str, max_depth: int = 3):
    """
    Load an HTML document with a controlled resource handling depth.
    Returns the HTMLDocument instance.
    """
    opts = ResourceHandlingOptions()
    opts.max_handling_depth = max_depth    # How to set max handling depth
    try:
        doc = HTMLDocument(path, opts)
        print(f"Loaded '{path}' with max depth {max_depth}.")
        return doc
    except Exception as exc:
        print(f"Error loading '{path}': {exc}")
        # Fallback to a simple load without resource handling
        return HTMLDocument(path)

if __name__ == "__main__":
    # Example 1: Standard depth
    doc1 = load_document("YOUR_DIRECTORY/big_page.html", max_depth=3)

    # Example 2: Deeper inspection for debugging
    doc2 = load_document("YOUR_DIRECTORY/complex_page.html", max_depth=5)

    # Example 3: Very shallow preview (e.g., thumbnail generation)
    doc3 = load_document("YOUR_DIRECTORY/preview_page.html", max_depth=1)
```

**Beklenen çıktı (dosyalar mevcut ve düzgün biçimlendirilmiş olduğunda):**

```
Loaded 'YOUR_DIRECTORY/big_page.html' with max depth 3.
Loaded 'YOUR_DIRECTORY/complex_page.html' with max depth 5.
Loaded 'YOUR_DIRECTORY/preview_page.html' with max depth 1.
```

Bir dosya okunamazsa, çökme yerine bir hata mesajı göreceksiniz.

![Python'da kaynak işleme seçeneklerini oluşturma](/images/resource-options.png){alt="Python'da kaynak işleme seçeneklerini oluşturma"}

## Özet – Neden Bu Yaklaşım Harika

- **Güvenlik öncelikli:** İç içeleme derinliğini sınırlamak kontrolsüz yinelemeyi ve bellek şişmesini önler.  
- **Esneklik:** Farklı senaryolara uyacak şekilde çalışma zamanında `max_handling_depth` değerini değiştirebilirsiniz.  
- **Basitlik:** Birkaç satır kod, **kaynak işleme seçenekleri** oluşturmanıza ve hemen uygulamanıza olanak tanır.  

Kısacası, artık ayrıştırıcınızın dış kaynakları ne kadar derin takip edeceğini kontrol etmek için sağlam bir deseniniz var.

## Sıradaki Adımlar

- `ResourceHandlingOptions` sınıfını daha ayrıntılı keşfedin—önbellekleme, zaman aşımı yönetimi ve MIME‑type filtreleme için bayraklar bulunuyor.  
- Derinlik sınırlamayı özel bir `UserAgent` dizesiyle birleştirerek agresif sunucular tarafından engellenmeyi önleyin.  
- Asenkron G/Ç ile çalışıyorsanız, aynı seçenekleri saygı gösteren ancak `asyncio` ile çalışan `aiohtmlparser` varyantına bakın.  

Denemekten çekinmeyin: derinliği `0` olarak ayarlayın ve ayrıştırıcının tüm dış referansları yok saymasını izleyin. Sadece ham HTML işaretlemesi gerektiğinde kullanışlı bir kısayoldur.

Sorularınız mı var ya da hâlâ sizi zorlayan bir sayfa mı var? Aşağıya bir yorum bırakın, ayarları ince ayarlamanızda memnuniyetle yardımcı olurum. İyi ayrıştırmalar!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [C#'ta Dizeden HTML Oluşturma – Özel Kaynak İşleyici Kılavuzu](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [C#'ta HTML Kaydetme – Özel Kaynak İşleyici Kullanarak Tam Kılavuz](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Java'da HTML için Sandbox Oluşturma – Adım Adım Kılavuz](/html/english/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}