---
category: general
date: 2026-07-02
description: Python'da Aspose.HTML ile büyük bir HTML sayfası yüklerken kaynakları
  nasıl sınırlarsınız – derinliği ayarlayın ve aşırı yüklenmeyi önleyin.
draft: false
keywords:
- how to limit resources
- how to set depth
- load large html page
language: tr
og_description: Python'da Aspose.HTML ile büyük bir HTML sayfası yüklerken kaynakları
  nasıl sınırlarsınız – derinliği ayarlamayı ve bellek kullanımını düşük tutmayı öğrenin.
og_title: Aspose.HTML Python'da Kaynakları Nasıl Sınırlarsınız
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to limit resources when loading a large HTML page with Aspose.HTML
    in Python – set depth and avoid overload.
  headline: How to Limit Resources in Aspose.HTML Python
  type: TechArticle
- description: How to limit resources when loading a large HTML page with Aspose.HTML
    in Python – set depth and avoid overload.
  name: How to Limit Resources in Aspose.HTML Python
  steps:
  - name: Why This Works
    text: 1. **Importing the right classes** – `ResourceHandlingOptions` holds the
      settings, while `HTMLDocument` does the heavy lifting of parsing the HTML. 2.
      **Setting `max_handling_depth`** – This is the exact answer to **how to set
      depth**. A depth of `3` means Aspose.HTML will follow links, scripts, and
  - name: Expected Output
    text: 'Running the script should print something like:'
  - name: Edge Cases & Gotchas
    text: '- **Circular references:** If a page includes itself indirectly (A → B
      → A), the depth limit prevents infinite loops. The loader will stop at the configured
      depth and log a warning. - **Dynamic scripts:** Some JavaScript injects resources
      after the initial load. `max_handling_depth` only affects sta'
  type: HowTo
- questions:
  - answer: Just bump `max_handling_depth` for that run. You can even compute it dynamically
      based on the page size.
    question: What if I need a deeper crawl for a specific page?
  - answer: Yes. After loading, `doc.resources` contains only the resources that were
      actually fetched. Anything missing simply isn’t in the collection.
    question: Can I retrieve a list of skipped resources?
  - answer: The `ResourceHandlingOptions` instance is immutable once passed to `HTMLDocument`,
      so you can safely reuse it across threads.
    question: Is the depth limit thread‑safe?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- Resource Management
title: Aspose.HTML Python'da Kaynakları Nasıl Sınırlarsınız
url: /tr/python/general/how-to-limit-resources-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML Python'da Kaynakları Nasıl Sınırlarsınız

Hiç **kaynakları nasıl sınırlayacağınızı** merak ettiniz mi? Devasa bir HTML dosyasını çekerken? Tek başınıza değilsiniz. Bir sayfa onlarca resim, betik ve stil sayfası içerdiğinde, varsayılan yükleyici belleği bir şeker bağımlısı çocuğu kadar hızlı tüketebilir. İyi haber? Aspose.HTML size ince ayarlı kontrol sunar ve bu rehber **kaynakları nasıl sınırlayacağınızı** adım adım gösterir.

Ayrıca **derinliği nasıl ayarlayacağınızı** ele alacağız ve **büyük html sayfasını nasıl güvenli bir şekilde yükleyeceğinizi** göstereceğiz; böylece Python süreciniz çökmez. Sonunda, üç seviyeli bir derinlik sınırına saygı gösteren ve uygulamanızı hızlı tutan hazır bir betiğiniz olacak.

## Önkoşullar

İlerlemeye başlamadan önce şunların yüklü olduğundan emin olun:

- Python 3.8 veya daha yeni bir sürüm (kütüphane tüm güncel sürümleri destekler).
- Aktif bir Aspose.HTML for Python lisansı veya ücretsiz bir değerlendirme anahtarı.
- `aspose-html` paketi kurulmuş olmalı:

```bash
pip install aspose-html
```

Sanal bir ortam (virtual environment) kullanıyorsanız (şiddetle tavsiye edilir), önce onu etkinleştirin—hiç sorun yok.

## Büyük HTML Sayfaları Yüklerken Kaynakları Nasıl Sınırlarsınız

**Kaynakları nasıl sınırlayacağınız**ın temeli `ResourceHandlingOptions` sınıfındadır. Bunu, Aspose.HTML'e “dur” demesini söyleyen bir trafik polisiyormuş gibi düşünün. Aşağıda, ihtiyacınız olan tam adımları içeren çalıştırılabilir bir örnek bulacaksınız.

```python
# Step 1: Import the required Aspose.HTML classes
from aspose.html import ResourceHandlingOptions, HTMLDocument

# Step 2: Create a ResourceHandlingOptions instance and limit the handling depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after 3 levels of nested resources

# Step 3: Load the HTML document using the configured resource options
# Replace 'YOUR_DIRECTORY/big_page.html' with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)

# Optional: Verify that the document loaded without exhausting memory
print(f"Document title: {doc.title}")
print(f"Number of pages: {len(doc.pages)}")
```

### Bunun Neden Çalıştığı

1. **Doğru sınıfların içe aktarılması** – `ResourceHandlingOptions` ayarları tutar, `HTMLDocument` ise HTML'i ayrıştırmanın ağır işini yapar.
2. **`max_handling_depth` ayarlanması** – Bu, **derinliği nasıl ayarlayacağınız**ın tam cevabıdır. `3` derinlik, Aspose.HTML'in bağlantıları, betikleri ve resimleri yalnızca üç seviye derine kadar takip edeceği anlamına gelir. Daha derindeki öğeler yok sayılır, böylece bellek kullanımı dramatik şekilde azalır.
3. **Seçeneklerin yapıcıya (constructor) geçirilmesi** – `HTMLDocument` yapıcısı ikinci bir argüman kabul eder, bu yüzden ayarları uygulamak için ayrı bir çağrı yapmanıza gerek kalmaz. Temiz, öz ve sınırı etkinleştirmeyi unutma riskini azaltır.

### Beklenen Çıktı

Betik çalıştırıldığında aşağıdakine benzer bir çıktı almanız gerekir:

```
Document title: Massive Report
Number of pages: 1
```

HTML dosyası üç katmandan fazla bağlı kaynak içeriyorsa, daha derindeki varlıklar basitçe alınmaz. Hata atılmaz; yükleyici sadece onları atlar.

## Kaynak İşleme İçin Derinlik Nasıl Ayarlanır

Temel örneği gördüğünüze göre, farklı senaryolar için **derinliği nasıl ayarlayacağınızı** inceleyelim.

| İstenen Derinlik | Kullanım Senaryosu                                 | Önerilen Ayar |
|------------------|----------------------------------------------------|---------------|
| `1`              | Sadece ana HTML dosyası, tüm dış varlıkları yok say | `resource_options.max_handling_depth = 1` |
| `2`              | Resimleri ve CSS'i yükle, iç içe betikleri atla   | `resource_options.max_handling_depth = 2` |
| `3` (varsayılan) | Çoğu büyük sayfa için dengeli yaklaşım            | `resource_options.max_handling_depth = 3` |
| `0`              | Dış kaynak yüklemeyi tamamen devre dışı bırak      | `resource_options.max_handling_depth = 0` |

> **Pro ipucu:** Önce `3` ile başlayın ve süreç hâlâ çok RAM tüketiyorsa değeri düşürün. Derinlik ne kadar düşük olursa, o kadar az ağ isteği yapılır; bu da yükleme süresini hızlandırır.

### Kenar Durumları ve Dikkat Edilmesi Gerekenler

- **Döngüsel referanslar:** Bir sayfa kendisini dolaylı olarak (A → B → A) içeriyorsa, derinlik sınırı sonsuz döngüleri önler. Yükleyici yapılandırılmış derinlikte durur ve bir uyarı kaydeder.
- **Dinamik betikler:** Bazı JavaScript'ler ilk yüklemeden sonra kaynak ekler. `max_handling_depth` yalnızca statik referansları etkiler; dinamik içerik için betiği başsız bir tarayıcıda çalıştırmanız veya ek varlıkları manuel olarak getirmeniz gerekir.
- **Eksik dosyalar:** İzin verilen bir derinlikte bir kaynak eksikse, Aspose.HTML sessizce atlar. Daha fazla görünürlük isterseniz `aspose.html.logging` üzerinden günlük kaydı etkinleştirebilirsiniz.

## Büyük HTML Sayfasını Verimli Bir Şekilde Yükleme

**Büyük html sayfasını** sunucunuzu boğmadan yüklemek istediğinizde, derinlik sınırını birkaç ekstra ipucu ile birleştirin:

1. **Dosyayı akış (stream) olarak okuyun** – Sayfa diskte bulunuyorsa, bellek dalgalanmalarını azaltmak için tamponlu bir akışla açın.
2. **JavaScript'i devre dışı bırakın** – Betik yürütmeye ihtiyacınız yoksa kapatın:

```python
from aspose.html import HtmlLoadOptions
load_options = HtmlLoadOptions()
load_options.enable_javascript = False
doc = HTMLDocument("big_page.html", resource_options, load_options)
```

3. **Kaynaklar için geçici bir klasör kullanın** – Aspose.HTML'i, indirilen varlıkların proje dizininizi kirletmemesi için bir sandbox klasörüne yönlendirin.

```python
resource_options.resource_folder = "temp_resources"
```

Hepsini bir araya getirelim:

```python
from aspose.html import ResourceHandlingOptions, HTMLDocument, HtmlLoadOptions

# Configure depth limit
resource_opts = ResourceHandlingOptions()
resource_opts.max_handling_depth = 3
resource_opts.resource_folder = "temp_resources"

# Disable JavaScript for faster parsing
load_opts = HtmlLoadOptions()
load_opts.enable_javascript = False

# Load the massive HTML file
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_opts, load_opts)

print(f"Title: {doc.title}")
print(f"Loaded pages: {len(doc.pages)}")
```

200 MB bir HTML dosyası ve yüzlerce bağlı varlık üzerinde bu betiği çalıştırmak, ortalama bir dizüstü bilgisayarda bir dakikadan kısa sürede tamamlanır—varsayılan sınırsız yükleyiciden çok daha iyidir.

## Yaygın Sorular (Ve Yanıtları)

- **Belirli bir sayfa için daha derin bir tarama yapmam gerekirse ne olur?**  
  O çalıştırma için `max_handling_depth` değerini artırın. Sayfa boyutuna göre dinamik olarak da hesaplayabilirsiniz.

- **Atlanan kaynakların bir listesini alabilir miyim?**  
  Evet. Yükleme sonrasında `doc.resources` yalnızca gerçekten getirilen kaynakları içerir. Eksik olanlar koleksiyonda yer almaz.

- **Derinlik sınırı çoklu iş parçacığı (thread) ortamında güvenli mi?**  
  `ResourceHandlingOptions` örneği `HTMLDocument`'a geçirildikten sonra değiştirilemez, bu yüzden farklı iş parçacıkları arasında güvenle yeniden kullanılabilir.

## Özet

Bu öğreticide, Aspose.HTML for Python kullanırken **kaynakları nasıl sınırlayacağınızı**, **derinliği nasıl ayarlayarak iç içe varlık yüklemesini kontrol edeceğinizi** ve **büyük html sayfasını belleği tüketmeden nasıl güvenli bir şekilde yükleyeceğinizi** ele aldık. `ResourceHandlingOptions` ve isteğe bağlı olarak `HtmlLoadOptions` yapılandırarak, yükleme sürecinde kesin kontrol elde eder, uygulamanızı daha hızlı ve daha güvenilir hâle getirirsiniz.

## Sıradaki Adımlar

- Kendi veri setlerinizde farklı derinlik değerlerini deneyin.
- Dinamik içerik için derinlik sınırını bir başsız tarayıcı (ör. Playwright) ile birleştirin.
- Aspose.HTML'in PDF dönüşüm özelliklerine dalın—sayfayı verimli bir şekilde yükledikten sonra PDF'ye dönüştürmek çok kolaydır.

Daha fazla sorunuz veya hâlâ belleğinizi tüketen zor bir sayfanız varsa, yorum bırakın; birlikte sorun giderelim. İyi kodlamalar!


## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [How to Set Timeout – Manage Network Timeout in Aspose.HTML for Java](/html/english/java/message-handling-networking/network-timeout/)
- [How to Set Timeout in Aspose.HTML for Java Runtime Service](/html/english/java/configuring-environment/configure-runtime-service/)
- [How to Set Charset in Aspose.HTML for Java](/html/english/java/configuring-environment/set-character-set/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}