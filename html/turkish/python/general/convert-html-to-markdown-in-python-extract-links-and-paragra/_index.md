---
category: general
date: 2026-09-26
description: Python ile HTML'yi Markdown'a dönüştürün, HTML'den bağlantıları çıkarın
  ve HTML'yi Markdown olarak kaydedin. HTML'yi adım adım nasıl dönüştüreceğinizi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- save html as markdown
- how to convert html
- extract paragraphs from html
language: tr
lastmod: 2026-09-26
og_description: Python ile HTML'yi Markdown'a dönüştürün, HTML'den bağlantıları çıkarın
  ve HTML'yi Markdown olarak kaydedin. Bu kapsamlı rehberi izleyin.
og_image_alt: Screenshot of Python code converting HTML to Markdown and showing extracted
  links
og_title: Python'da HTML'yi Markdown'a Dönüştür – Bağlantıları ve Paragrafları Çıkar
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  headline: Convert HTML to Markdown in Python – extract links and paragraphs easily
  type: TechArticle
- description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  name: Convert HTML to Markdown in Python – extract links and paragraphs easily
  steps:
  - name: Expected output
    text: 'Running the script generates a file similar to the following (the exact
      content depends on the source HTML):'
  - name: 1. Extract only links
    text: '```python md_options.features = MarkdownFeatures.LINKS # No paragraphs
      ```'
  - name: 2. Extract only paragraphs
    text: '```python md_options.features = MarkdownFeatures.PARAGRAPHS # No links
      ```'
  type: HowTo
- questions:
  - answer: Yes. `HTMLDocument` accepts any well‑formed fragment; the converter treats
      the fragment as the document body.
    question: Does this work with HTML fragments (no `<html>` root tag)?
  - answer: 'Add `MarkdownFeatures.IMAGES` to the `features` flag: ```python md_options.features
      = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
      ```'
    question: Can I keep images as Markdown image syntax?
  - answer: 'Wrap `convert_html_to_markdown` in a loop that walks the directory with
      `os.listdir` or `pathlib.Path.rglob("*.html")`. --- ## Conclusion You now know
      how to **convert HTML to Markdown** in Python while selectively **extracting
      links from HTML** and **extracting paragraphs from HTML**. The script de'
    question: How do I convert many files in a directory?
  type: FAQPage
tags:
- html
- markdown
- python
- data‑extraction
title: HTML'yi Python'da Markdown'a Dönüştür – Bağlantıları ve Paragrafları Kolayca
  Çıkar
url: /tr/python/general/convert-html-to-markdown-in-python-extract-links-and-paragra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'yi Python'da Markdown'e Dönüştür – Bağlantıları ve Paragrafları Kolayca Çıkar

Eğer sadece faydalı kısımları tutarak **HTML'yi Markdown'e dönüştürmeniz** gerekiyorsa, bu rehber size sadece birkaç Python satırıyla bunu nasıl yapacağınızı gösterir. Blog gönderilerini kazıyor, dokümantasyonu arşivliyor ya da e-posta gövdelerini temizliyor olun, HTML'den bağlantıları çıkarmanın ve HTML'yi Markdown olarak kaydetmenin güvenilir bir yolunu öğreneceksiniz.

Bu öğretici, gerekli paketin kurulumu ve boş `<a>` etiketleri ya da iç içe paragraflar gibi kenar durumlarının ele alınması gibi konulardan tutun, sonuna kadar her şeyi kapsar. Sonunda **HTML'yi Markdown'e dönüştüren**, HTML'den bağlantıları çıkaran ve gerektiğinde HTML'den paragrafları da çıkaran hazır‑çalıştır bir betiğe sahip olacaksınız.

---

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* Python 3.8 veya daha yeni bir sürüm  
* `groupdocs-conversion` Python paketi erişimi ( `HTMLDocument`, `MarkdownSaveOptions` ve `Converter` sınıflarını sağlayan kütüphane )  
* İşlemek istediğiniz yerel bir HTML dosyası (ör. `article.html`)

Kütüphaneyi pip ile kurabilirsiniz:

```bash
pip install groupdocs-conversion
```

> **İpucu:** Bağımlılıkları izole tutmak için sanal ortam (`python -m venv venv`) kullanın.

---

## Adım 1: Kaynak HTML belgesini yükleyin

İlk işlem, kaynak dosyanıza işaret eden bir `HTMLDocument` nesnesi oluşturmaktır. Bu nesne ham HTML'yi soyutlar ve dönüştürücüye temiz bir giriş noktası sağlar.

```python
from groupdocs.conversion import HTMLDocument

# Load the HTML file you want to transform
html_doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

*Why this matters:* Bu şekilde belgeyi yüklemek, kütüphanenin DOM'u yalnızca bir kez ayrıştırmasını sağlar; böylece sonraki işlemler (bağlantı veya paragraf çıkarma gibi) hızlı ve bellek‑verimli olur.

---

## Adım 2: Markdown kaydetme seçeneklerini oluşturun ve ihtiyacınız olan özellikleri seçin

`MarkdownSaveOptions` hangi HTML öğelerinin dönüşümden geçeceğini belirlemenizi sağlar. `features` bayrağı, seçenekleri birleştirmek için bit düzeyinde OR kullanır.

```python
from groupdocs.conversion import MarkdownSaveOptions, MarkdownFeatures

# Keep only links and paragraphs in the resulting Markdown
md_options = MarkdownSaveOptions()
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS
```

*Why this matters:* `LINKS` ve `PARAGRAPHS` belirterek **HTML'den bağlantıları çıkarır** ve **HTML'den paragrafları çıkarırsınız**, diğer her şeyi (stil, script, resim) yok sayarsınız. Daha sonra sadece bağlantılara ihtiyacınız olursa, `MarkdownFeatures.PARAGRAPHS` yerine `0` koyun (veya tamamen kaldırın).

---

## Adım 3: Yapılandırılmış seçenekleri kullanarak HTML'yi Markdown'e dönüştürün

Şimdi, kaynak belgeyi, hedef yolu ve az önce oluşturduğunuz seçenekleri parametre olarak vererek statik `convert_html` metodunu çağırın.

```python
from groupdocs.conversion import Converter

# Perform the conversion and write the Markdown file
Converter.convert_html(html_doc, "YOUR_DIRECTORY/article_links.md", md_options)
```

*Why this matters:* Dönüştürme tek bir geçişte çalışır ve tanımladığınız özellik filtresini uygular. Oluşan dosya (`article_links.md`) yalnızca Markdown‑formatlı bağlantılar ve paragraflar içerir; bu da **HTML'yi Markdown olarak kaydetmek** istediğinizde tam ihtiyacınız olan şeydir.

---

## Tam script – hepsi bir arada

Aşağıda, `html_to_md.py` adlı bir dosyaya kopyalayıp yapıştırabileceğiniz eksiksiz, çalıştırılabilir bir script bulunuyor. Ortamınıza uygun olacak şekilde yolları ayarlayın.

```python
# html_to_md.py
# -------------------------------------------------
# Convert HTML to Markdown, keeping only links and paragraphs.
# -------------------------------------------------

from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

def convert_html_to_markdown(source_path: str, target_path: str) -> None:
    """
    Convert an HTML file to Markdown, extracting only links and paragraphs.

    Args:
        source_path: Path to the source HTML file.
        target_path: Path where the Markdown file will be saved.
    """
    # Load the HTML document
    html_doc = HTMLDocument(source_path)

    # Configure conversion to keep links and paragraphs
    md_options = MarkdownSaveOptions()
    md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS

    # Run the conversion
    Converter.convert_html(html_doc, target_path, md_options)
    print(f"✅ Conversion complete – Markdown saved to: {target_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    src = "YOUR_DIRECTORY/article.html"
    dst = "YOUR_DIRECTORY/article_links.md"
    convert_html_to_markdown(src, dst)
```

### Beklenen çıktı

Betik çalıştırıldığında aşağıdakine benzer bir dosya oluşturulur (tam içerik kaynak HTML'ye bağlıdır):

```markdown
[OpenAI](https://openai.com)

This is the first paragraph of the article.

[GitHub](https://github.com)

Another paragraph that explains the next topic.
```

Yalnızca bağlantı metni ve paragraf metni görünür; diğer tüm HTML öğeleri kaldırılmıştır.

---

## Yalnızca bağlantıları veya yalnızca paragrafları çıkarın (ileri varyasyonlar)

Bazen sadece bir tür öğe içeren bir Markdown dosyasına **HTML'yi nasıl dönüştüreceğinizi** bilmeniz gerekir.

### 1. Yalnızca bağlantıları çıkar

```python
md_options.features = MarkdownFeatures.LINKS   # No paragraphs
```

### 2. Yalnızca paragrafları çıkar

```python
md_options.features = MarkdownFeatures.PARAGRAPHS   # No links
```

Her iki varyasyon da aynı `convert_html` çağrısını yeniden kullanır; böylece ayrı bir dönüşüm mantığı yazmanıza gerek kalmaz.

---

## Kenar durumlarını ele alma

| Durum                                   | Önerilen çözüm |
|----------------------------------------|-----------------|
| HTML dosyası boş `<a>` etiketleri içeriyorsa | Dönüştürücü otomatik olarak boş bağlantıları atlar. Eğer `[]()` gibi gereksiz girdiler görürseniz, `md_options.removeEmptyLinks = True` ayarlayın. |
| İç içe paragraflar (`<p>` bir `<div>` içinde) | Kütüphane iç içe paragrafları düzleştirir, metin sırasını korur. Ek bir koda gerek yoktur. |
| Bağlantı başlıklarında ASCII dışı karakterler | Python dosyanızın UTF‑8 kodlamasıyla kaydedildiğinden emin olun ve çıktıyı okurken `encoding="utf-8"` kullanın. |
| Çok büyük HTML dosyaları (≥ 50 MB)      | Belleğe tüm dosyayı yüklememek için `HTMLDocument(stream=io.BytesIO(...))` kullanarak dosyayı parçalar halinde işleyin. |

---

## Sıkça Sorulan Sorular

**S: Bu, `<html>` kök etiketi olmayan HTML parçacıklarıyla çalışır mı?**  
C: Evet. `HTMLDocument` herhangi bir iyi biçimlendirilmiş parçacığı kabul eder; dönüştürücü parçacığı belge gövdesi olarak işler.

**S: Görselleri Markdown resim sözdizimi olarak tutabilir miyim?**  
C: `features` bayrağına `MarkdownFeatures.IMAGES` ekleyin:  
```python
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
```

**S: Bir klasördeki birçok dosyayı nasıl dönüştürürüm?**  
C: `convert_html_to_markdown` fonksiyonunu, `os.listdir` ya da `pathlib.Path.rglob("*.html")` ile klasörü dolaşan bir döngü içinde kullanın.

---

## Sonuç

Artık Python'da **HTML'yi Markdown'e dönüştürürken** seçici olarak **HTML'den bağlantıları çıkarabilir** ve **HTML'den paragrafları çıkarabilirsiniz**. Script, standart yaklaşımı gösteriyor — belgeyi yükleyin, `MarkdownSaveOptions` yapılandırın ve `Converter.convert_html` çalıştırın. Birkaç ayar değişikliğiyle yalnızca bağlantılar, yalnızca paragraflar ya da tam bir temsil içeren **HTML'yi Markdown olarak kaydedebilirsiniz**.

Sonrasında şunları keşfedebilirsiniz:

* Bölüm başlıklarını korumak için `MarkdownFeatures.HEADINGS` eklemek.  
* Oluşan Markdown'ı MkDocs veya Hugo gibi statik site jeneratörlerine girdi olarak kullanmak.  
* Tüm dokümantasyon deposu için toplu dönüşümleri otomatikleştirmek.

Happy converting!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [HTML'yi .NET'te Aspose.HTML ile Markdown'e Dönüştür](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Java için Aspose.HTML ile HTML'yi Markdown'e Dönüştür](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Java'da HTML'yi Markdown'e Dönüştürürken Ofset Nasıl Ayarlanır](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}