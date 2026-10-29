---
category: general
date: 2026-08-09
description: HTML'yi PDF veya Markdown'a dönüştürürken kaynakları nasıl sınırlarsınız.
  PDF dışa aktarmayı, HTML'den bağlantı çıkarmayı ve kaynak derinliğini kontrol etmeyi
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to limit resources
- convert html to pdf
- convert html to markdown
- extract links from html
- how to export pdf
language: tr
lastmod: 2026-08-09
og_description: HTML'yi PDF veya Markdown'a dönüştürürken kaynakları nasıl sınırlayacağınızı
  öğrenin. Bu rehber, PDF dışa aktarmayı, HTML'den bağlantı çıkarmayı ve kaynak işleme
  sürecini yüzeysel tutmayı gösterir.
og_image_alt: Screenshot showing how to limit resources in HTML conversion script
og_title: HTML‑to‑PDF ve HTML‑to‑Markdown dönüşümü için kaynakları nasıl sınırlarsınız
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: How to limit resources while converting HTML to PDF or Markdown. Learn
    to export PDF, extract links from HTML, and control resource depth.
  headline: How to limit resources for HTML to PDF and Markdown
  type: TechArticle
tags:
- HTML conversion
- PDF export
- Markdown generation
- Resource handling
title: HTML'den PDF ve Markdown'a kaynakları nasıl sınırlarsınız
url: /tr/python/general/how-to-limit-resources-for-html-to-pdf-and-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'den PDF ve Markdown'e Kaynakları Sınırlama

Büyük ölçekli bir HTML dönüşümü sırasında **kaynakları nasıl sınırlayacağınızı** öğrenmeniz gerekiyorsa, bu kılavuz size tam çözümü gösterir. Kaynak‑işleme seçeneklerini yapılandırarak derin dış çağrıları önler, bellek kullanımını düşük tutar ve yine de doğru PDF ve Markdown çıktısı elde edersiniz.

Ayrıca **html'yi pdf'ye dönüştürmeyi**, **html'yi markdown'a dönüştürmeyi**, **html'den bağlantıları çıkarmayı** ve aynı kaynak belgeden **pdf'yi dışa aktarmanın** en iyi yolunu öğreneceksiniz. GroupDocs.Conversion SDK dışındaki herhangi bir harici araç gerekmemektedir.

## Ne Başaracaksınız

* Harici kaynak işleme derinliğini güvenli bir seviyeye sınırlayın.  
* Büyük bir HTML raporundan PDF dosyası oluşturun.  
* Sadece bağlantılar ve paragraflar içeren Git‑flavoured Markdown dosyası üretin.  
* PDF dışa aktarımının başarılı olduğunu ve Markdown dosyasının beklenen bağlantıları içerdiğini doğrulayın.

### Önkoşullar

* Python 3.8+ (kod tip‑annotated Python kullanır).  
* `groupdocs-conversion` paketinin yüklü olması (`pip install groupdocs-conversion`).  
* Yazılabilir bir dizinde bulunan büyük bir HTML dosyası (ör. `big_report.html`).  

---

## HTML Dönüştürürken Kaynakları Nasıl Sınırlarsınız

Dönüştürücünün dış kaynakları (görseller, CSS, betikler) kaç seviyeye kadar takip edeceğini kontrol etmek, performans ve güvenlik açısından kritiktir. `ResourceHandlingOptions` sınıfı, maksimum işleme derinliğini ayarlamanıza olanak tanır. Derinlik **3** olduğunda, dönüştürücü üç seviyeye kadar bağlantıları takip eder ve ardından durur, böylece kontrol dışı ağ çağrıları önlenir.

```python
from groupdocs.conversion import ResourceHandlingOptions, HTMLDocument, Converter, MarkdownSaveOptions

# Step 1: Create a ResourceHandlingOptions instance and cap the depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3  # limit external resource traversal
```

*Neden önemli*: Büyük raporlar genellikle birçok dış varlığa referans verir. Derinlik sınırı olmadan, dönüştürücü her bağlantılı betiği veya görseli indirmeye çalışabilir, bant genişliğini ve belleği tüketir. `max_handling_depth` değerini 3 olarak ayarlamak, tamlık ile güvenliği dengeler.

---

## Kontrol Edilen Kaynak Derinliğiyle HTML'yi PDF'ye Dönüştürme

Kaynak seçenekleri hazır olduğunda, HTML belgesini bu seçeneklerle yükleyin ve PDF dönüşümünü başlatın. `Converter.convert_html` yöntemi, dosya uzantısından çıktı formatını algılar.

```python
# Step 2: Load the HTML document with the resource options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_report.html", resource_options)

# Step 3: Convert the HTML document to PDF
Converter.convert_html(html_doc, "YOUR_DIRECTORY/big_report.pdf")
```

*Neden işe yarıyor*: `HTMLDocument` yapıcı, bir `ResourceHandlingOptions` argümanı alır, böylece PDF oluşturma sırasında aynı derinlik sınırı uygulanır. SDK, sayfa düzenini otomatik olarak render eder, izin verilen görselleri gömer ve yüksek‑doğruluklu bir PDF üretir.

**Beklenen çıktı**: `big_report.pdf`, `YOUR_DIRECTORY` içinde görünür. Görsellerin, tabloların ve metnin doğru render edildiğini, derinlik 3'ün ötesindeki dış kaynakların ise dışarıda bırakıldığını doğrulamak için herhangi bir PDF görüntüleyicide açın.

---

## Bağlantı Çıkarma İçin Markdown Kaydetme Seçeneklerini Hazırlama

HTML'nin hafif bir temsiline ihtiyacınız olduğunda, Markdown'a dönüştürmek idealdir. `MarkdownSaveOptions` sınıfı, bir biçimlendirici (Git‑flavoured) seçmenize ve hangi içerik özelliklerini tutacağınıza olanak tanır. Bu öğreticide yalnızca **bağlantıları** ve **paragrafları** tutuyoruz; bu, **html'den bağlantıları çıkarmak** gereksinimini karşılar.

```python
# Step 4: Configure MarkdownSaveOptions for link‑only output
markdown_options = MarkdownSaveOptions()
markdown_options.formatter = MarkdownSaveOptions.Formatter.GIT
markdown_options.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)
```

*Neden bu bayraklar*:  
* `Formatter.GIT`, GitHub ve GitLab ile sorunsuz çalışan bir Markdown üretir.  
* `Features.LINK | Features.PARAGRAPH`, görselleri, tabloları ve betikleri kaldırır, temiz bir hiperlink listesi ve okunabilir metin blokları bırakır.

## Yapılandırılmış Seçenekleri Kullanarak HTML'yi Markdown'a Dönüştürme

Şimdi aynı `HTMLDocument` örneğiyle dönüşümü çalıştırın. aşırı yüklenmiş `convert_html` yöntemi, bir `MarkdownSaveOptions` nesnesi ve ardından hedef dosya yolunu kabul eder.

```python
# Step 5: Convert the same HTML document to Markdown
Converter.convert_html(html_doc, markdown_options, "YOUR_DIRECTORY/big_report.md")
```

**Sonuç**: `big_report.md` yalnızca Markdown‑formatlı bağlantılar ve paragraflar içerir. Orijinal HTML'den çıkarılan URL'lerin öz bir listesini görmek için dosyayı herhangi bir editörde açın.

## PDF'yi Dışa Aktarma ve Sonuçları Doğrulama

PDF dışa aktarma zaten Adım 3'te ele alındı, ancak dosyanın doğru yazıldığını ve kaynak sınırının beklendiği gibi davrandığını doğrulamakta fayda var.

```python
import os

pdf_path = "YOUR_DIRECTORY/big_report.pdf"
md_path = "YOUR_DIRECTORY/big_report.md"

# Verify PDF existence and size
if os.path.isfile(pdf_path):
    print(f"PDF exported successfully – size: {os.path.getsize(pdf_path)} bytes")
else:
    raise FileNotFoundError("PDF export failed")

# Verify Markdown existence and preview first 5 lines
if os.path.isfile(md_path):
    print("Markdown export successful. First lines:")
    with open(md_path, "r", encoding="utf-8") as f:
        for _ in range(5):
            print(f.readline().strip())
else:
    raise FileNotFoundError("Markdown export failed")
```

*Neden bu kontrol*: Dosya‑boyutu kontrolü, eksik kaynakları işaret edebilecek olağandışı küçük PDF'leri fark etmenize yardımcı olur. Markdown önizlemesi, yalnızca bağlantıların ve paragrafların korunduğunu doğrular, **html'den bağlantıları çıkarmak** hedefini karşılar.

## Yaygın Varyasyonlar ve Kenar‑Durum İşleme

| Situation | Recommended tweak |
|-----------|-------------------|
| **HTML, 3 seviyeden daha derin referanslar içeriyor** | `max_handling_depth` değerini 5 veya 7'ye artırın, ancak bellek kullanımını izleyin. |
| **Markdown'da görselleri tutma ihtiyacı** | `features` bayrağına `MarkdownSaveOptions.Features.IMAGE` ekleyin. |
| **Tek sayfalık PDF oluşturma** | `PDFSaveOptions.page_width` ve `page_height` değerlerini içeriğe uyacak şekilde ayarlayın veya `pdf_options.split_into_pages = False` kullanın. |
| **Başsız (headless) sunucuda çalıştırma** | SDK'nın yerel bağımlılıklarının (`libcairo`, `libpango`) yüklü olduğundan emin olun, böylece render hataları önlenir. |
| **Büyük dosyalar zaman aşımına neden oluyor** | `HTMLDocument.load_range(start, end)` ile bölümleri yükleyerek HTML'yi parçalara ayırıp işleyin. |

**Pro ipucu**: Birden fazla dönüşüm için aynı `HTMLDocument` örneğini yeniden kullanın. SDK, ayrıştırılmış DOM'u önbelleğe alır, bu da sonraki PDF veya Markdown dışa aktarımları için CPU süresini azaltır.

## Sonuç

Artık **kaynakları nasıl sınırlayacağınızı** **html'yi pdf'ye dönüştürürken** ve **html'yi markdown'a dönüştürürken**, **html'den bağlantıları nasıl çıkaracağınızı** ve **pdf'yi güvenli bir şekilde nasıl dışa aktaracağınızı** biliyorsunuz. `ResourceHandlingOptions` ve `MarkdownSaveOptions` yapılandırarak dış çağrı derinliğini kontrol eder, çıktıyı hafif tutar ve sonraki işlemler için güvenilir artefaktlar üretirsiniz.

Sonra, **özel CSS enjeksiyonu**, **PDF'lere filigran ekleme** veya **birden fazla HTML dosyasını toplu dönüştürme** gibi gelişmiş özellikleri keşfedin. Bu konular burada ele alınan aynı prensiplere dayanır ve belge‑işleme hattınızı daha da genişletir.

---

## Sonra Ne Öğrenmelisin?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [HTML'yi PDF'ye Dönüştürme Java – Aspose.HTML for Java Kullanarak](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Aspose.HTML'yi Kullanarak HTML‑to‑PDF Java için Yazı Tiplerini Yapılandırma](/html/english/java/configuring-environment/configure-fonts/)
- [Aspose.HTML for Java ile HTML'yi MHTML'ye Dönüştürme](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}