---
category: general
date: 2026-11-17
description: Python’da HTML’yi görsellerle birlikte markdown’a dönüştür – HTML’yi
  hızlıca nasıl dönüştüreceğinizi ve görselleri bozulmadan dışa aktaracağınızı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to convert html
- export html with images
- markdown conversion with images
language: tr
lastmod: 2026-11-17
og_description: HTML'yi Python'da resimlerle markdown'a dönüştürün. Bu eğitim, HTML'yi
  dönüştürürken resimleri dışa aktarmayı gösterir ve size eksiksiz, hemen çalıştırılabilir
  bir çözüm sunar.
og_image_alt: Diagram showing convert html to markdown workflow with image extraction
og_title: Python'da Görsellerle HTML'yi Markdown'a Dönüştürme – Hızlı Rehber
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Convert HTML to markdown with images in Python – learn how to convert
    HTML quickly while exporting images intact.
  headline: Convert HTML to markdown with images in Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
- Image extraction
title: Python'da Görsellerle HTML'yi Markdown'a Dönüştür
url: /tr/python/general/convert-html-to-markdown-with-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'yi Python'da Görsellerle Markdown'a Dönüştürme

HTML'yi **markdown'a dönüştürürken** görselleri ayrı dosyalar olarak tutmanız gerekiyorsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. Dış kaynakları işleyen, markdown çıktısının orijinal görsellere doğru şekilde referans verdiği eksiksiz, çalıştırılabilir bir örnek alacaksınız.

Görselleri içeren HTML'yi dışa aktarmak, basit dönüştürücülerde genellikle görsellerin ya atılması ya da base64 dizgeleri olarak gömülmesi nedeniyle sorun çıkarır. Kaynak işleme seçeneklerini yapılandırarak orijinal görsel dosyalarını korur ve daha sonra sürüm kontrolüne ya da düzenlemeye uygun temiz bir markdown üretirsiniz.

Bu öğreticide şunları yapacaksınız:

* Diskten bir HTML belgesi yükleme.  
* Dönüştürücüyü **görselleri ayrı dosyalar olarak dışa aktarma** şeklinde yapılandırma.  
* **Görsellerle markdown dönüşümü** seçeneklerini kullanarak sonucu markdown olarak kaydetme.  

Tek gereksinim, `HTMLDocument`, `ResourceHandlingOptions`, `MarkdownSaveOptions` ve `Converter` sağlayan Aspose.HTML for Python kütüphanesinin (veya uyumlu bir API'nin) güncel bir sürümüdür. Ayrıca Python 3.8+ ve çıktı klasörüne yazma iznine ihtiyacınız var.

---

## Önkoşullar ve kurulum

1. Aspose.HTML paketini yükleyin:

   ```bash
   pip install aspose-html
   ```

2. Kurulumu doğrulayın:

   ```python
   import aspose.html as ah
   print(ah.__version__)   # should print the installed version, e.g., 22.9
   ```

> **İpucu:** Diğer projelerle sürüm çakışmalarını önlemek için bir sanal ortam (virtual environment) kullanın.

---

## Adım 1: Kaynak HTML belgesini yükleyin

İlk adım, kaynak dosyayı temsil eden bir `HTMLDocument` nesnesi oluşturmaktır. Bu nesne işaretlemi (markup) ayrıştırır ve dönüştürücünün gezebileceği bir DOM ağacı oluşturur.

```python
from aspose.html import HTMLDocument

# Load the HTML file you want to convert
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

*Neden önemli* – Belgeyi yüklemek, kütüphanenin işaretlemeyi tam kontrol etmesini sağlar; böylece göreli URL'leri çözümleyebilir ve daha sonra kaynak işleme uygulayabilir.

---

## Adım 2: Dış kaynak işleme ayarlarını yapılandırın

**Görselleri ayrı dosyalar olarak dışa aktarmak** istediğinizde, genellikle görsellerin markdown dosyasının yanında kaydedilmesini istersiniz, gömülü olmalarını değil. `ResourceHandlingOptions` sınıfı bu davranışı belirlemenize olanak tanır.

```python
from aspose.html import ResourceHandlingOptions

resource_options = ResourceHandlingOptions()
resource_options.save_external_resources = True   # keep images as separate files
```

`save_external_resources` özelliğini `True` olarak ayarlamak, dönüştürücünün her dış kaynağı (görseller, CSS, fontlar) markdown çıktısının yanındaki bir klasöre kopyalamasını sağlar. Markdown dosyası, bu kopyalara göreli bağlantılar içerir.

---

## Adım 3: Kaynak işleme yapılandırmasını markdown seçeneklerine ekleyin

`MarkdownSaveOptions`, markdown dönüşümünün nasıl gerçekleşeceğini kontrol eder. `resource_handling_options` özelliğini atayarak **görsellerle markdown dönüşümü** özelliğini etkinleştirirsiniz.

```python
from aspose.html import MarkdownSaveOptions

markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options
```

Bu adımı atlamanız durumunda, dönüştürücü görsel referanslarını kaldırır ya da onları veri URI'ları olarak gömer; bu da görselleri dışa aktarma amacını boşa çıkarır.

---

## Adım 4: Dönüşümü gerçekleştirin

Son olarak, `Converter.convert` metodunu kaynak belge, hedef yol ve hazırladığınız seçeneklerle çağırın.

```python
from aspose.html import Converter

output_path = "YOUR_DIRECTORY/sample.md"
Converter.convert(html_doc, output_path, markdown_options)
```

Çağrı tamamlandığında şunları bulacaksınız:

* `sample.md` – orijinal HTML'nin markdown sürümü.  
* `sample_files` (veya benzeri) adlı bir alt klasör, HTML'de referans verilen tüm görselleri içerir.

---

## Tam çalışan betik

Tüm parçaları bir araya getirdiğinizde komut satırından çalıştırabileceğiniz tek bir betik elde edersiniz:

```python
# convert_html_to_markdown.py
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, MarkdownSaveOptions, Converter

def convert_html_to_markdown(html_file: str, markdown_file: str):
    """
    Convert an HTML file to markdown while exporting images as separate files.
    """
    # 1. Load the HTML document
    html_doc = HTMLDocument(html_file)

    # 2. Set up resource handling to keep images external
    res_opts = ResourceHandlingOptions()
    res_opts.save_external_resources = True

    # 3. Attach resource handling to markdown options
    md_opts = MarkdownSaveOptions()
    md_opts.resource_handling_options = res_opts

    # 4. Convert and save
    Converter.convert(html_doc, markdown_file, md_opts)
    print(f"Conversion complete: {markdown_file}")

if __name__ == "__main__":
    # Adjust these paths to your environment
    src_html = os.path.abspath("YOUR_DIRECTORY/sample.html")
    dst_md   = os.path.abspath("YOUR_DIRECTORY/sample.md")

    convert_html_to_markdown(src_html, dst_md)
```

**Beklenen çıktı**

```
Conversion complete: /absolute/path/YOUR_DIRECTORY/sample.md
```

Çalıştırdıktan sonra `sample.md` dosyasını herhangi bir markdown editöründe açın. Görsel bağlantıları şu şekilde görünecektir:

```markdown
![Alt text](sample_files/image1.png)
```

Görseller kendileri `sample_files` klasöründe bulunur; sürüm kontrolüne ya da sonraki işlemlere hazırdır.

---

## Yaygın kenar durumlarının ele alınması

| Durum                                   | Önerilen yaklaşım |
|----------------------------------------|-------------------|
| **Eksik görsel dosyaları**               | Dönüştürücü bir uyarı verir ve kırık bir bağlantı bırakır. Dönüştürmeden önce tüm `<img src>` özniteliklerinin ulaşılabilir kaynaklara işaret ettiğinden emin olun. |
| **Projeye dışarıda kalan göreli URL'ler** | `ResourceHandlingOptions.base_url` kullanarak temel bir URL sağlayın; böylece dönüştürücü yolları doğru şekilde çözümleyebilir. |
| **Çok sayıda görsel içeren büyük HTML dosyaları** | (Varsa) `resource_options.max_resource_size` ayarını kullanarak kopyalanan kaynakların boyutunu sınırlayın. |
| **PNG/JPEG dışındaki görsel formatları** | Kütüphane orijinal formatı otomatik olarak kopyalar. Hedef markdown görüntüleyicisinin formatı desteklediğinden emin olun (ör. SVG). |
| **Yazma izni hataları**                 | Betiği uygun izinlerle çalıştırın veya yazma izniniz olan bir çıktı dizini seçin. |

---

## **Görsellerle markdown dönüşümü** için ipuçları

* Çıktı klasörünü temiz tutun: her çalıştırmadan önce `*_files` dizinini silin, böylece yeni bir görsel seti elde edersiniz.  
* Orijinal HTML'de anlamlı `alt` öznitelikleri kullanın; bunlar otomatik olarak markdown görsel alt metinlerine dönüşür.  
* Görselleri base64 olarak gömmeniz gerekiyorsa (tek dosyalı markdown için), `resource_options.save_external_resources = False` olarak ayarlayın. Bu, **görselleri ayrı dosyalar olarak dışa aktarma** işleminin tersidir, ancak e‑posta ya da dokümantasyon gömmeleri için faydalıdır.  
* Birden fazla dosyayı dönüştürürken, betiği bir döngü içinde çalıştırın ve `resource_options.resource_folder` ayarını isim çakışmalarını önleyecek şekilde değiştirin.

---

## Sıkça Sorulan Sorular

**S: Tam bir `<html>` sarmalayıcısı olmayan HTML parçacıklarıyla da çalışır mı?**  
C: Evet. `HTMLDocument` parçacıkları ayrıştırabilir; dönüştürücü bunları aynı şekilde işler.

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri içerir; böylece ek API özelliklerini ustalaşabilir ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [How to embed images in HTML to Markdown conversion using Python](/html/english/python/general/how-to-embed-images-in-html-to-markdown-conversion-using-pyt/)
- [Convert HTML to Markdown – Complete Guide with CSS & Images](/html/english/python/general/convert-html-to-markdown-complete-guide-with-css-images/)
- [Convert HTML to Markdown with Aspose – Complete Python Guide](/html/english/python/general/convert-html-to-markdown-with-aspose-complete-python-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}