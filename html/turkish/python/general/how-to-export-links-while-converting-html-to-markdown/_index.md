---
category: general
date: 2026-08-22
description: HTML'den bağlantıları dışa aktarma ve paragraf dahil markdown dosyasına
  dönüştürme. HTML'den markdown'a dönüşüm için adım adım kılavuz.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export links
- convert html to markdown
- how to convert html
- how to extract paragraphs
- html to markdown file
language: tr
lastmod: 2026-08-22
og_description: HTML belgesinden bağlantıları dışa aktarmayı ve paragrafları da içerecek
  şekilde bir markdown dosyasına dönüştürmeyi öğrenin. Güvenilir HTML'den markdown'a
  dönüşüm için bu kapsamlı öğreticiyi izleyin.
og_image_alt: How to export links while converting HTML to Markdown
og_title: HTML'yi Markdown'a dönüştürürken bağlantıları nasıl dışa aktarılır – adım
  adım rehber
schemas:
- author: GroupDocs
  dateModified: '2026-08-22'
  description: How to export links from HTML and convert it to a markdown file, including
    paragraphs. Step‑by‑step guide for HTML to markdown conversion.
  headline: How to export links while converting HTML to Markdown
  type: TechArticle
tags:
- HTML conversion
- Markdown
- Python
title: HTML'yi Markdown'a dönüştürürken bağlantıları nasıl dışa aktarılır?
url: /tr/python/general/how-to-export-links-while-converting-html-to-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'yi Markdown'a Dönüştürürken Bağlantıları Dışa Aktarma

Eğer bir HTML sayfasından **bağlantıları dışa aktarma** ve sonucu temiz bir **html to markdown dosyasına** dönüştürmeniz gerekiyorsa, bu kılavuz size tam adımları gösterir. Ayrıca **paragrafları çıkarmayı** keşfedecek ve markdown çıktısının sizin için önemli olan ana içeriği içermesini sağlayacaksınız. Öğreticinin sonunda “**html nasıl markdown'a dönüştürülür**” sorusuna hazır‑çalıştır bir script ile cevap verebileceksiniz.

Bağlantıları dışa aktarmak ve paragrafları çıkarmak, web içeriğini statik sitelere, dokümantasyon portallarına veya headless CMS arka uçlarına taşıdığınızda yaygın görevlerdir. Aşağıdaki yaklaşım GroupDocs Conversion SDK for Python ile çalışır, ancak kavramlar dışa aktarma özelliklerini yapılandırmanıza izin veren herhangi bir kütüphane için geçerlidir.

---

## Gereksinimler

- Python 3.9 ve üzeri  
- `groupdocs-conversion` paketi (`pip install groupdocs-conversion` ile kurulur)  
- İşlemek istediğiniz bir HTML dosyası (örnek: `input.html`)  
- Python betikleme konusunda temel bilgi  

---

## HTML'den Markdown'a Dönüştürürken Bağlantıları Dışa Aktarma

İlk büyük adım, yalnızca istenen özelliklerin—bağlantılar ve paragraflar—**html to markdown dosyasına** yazılacak şekilde dönüşümü yapılandırmaktır. SDK, `MarkdownFeature` değerlerinin bir bitmask'ını ayarlamanıza izin verir; çıktıyı odaklamak için `LINKS` ve `PARAGRAPHS` birleştiririz.

```python
# Import the required classes from the GroupDocs Conversion SDK
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeature, Converter

# Step 1: Load the source HTML document
html_doc = HTMLDocument("YOUR_DIRECTORY/input.html")

# Step 2: Create Markdown save options and select the features to export
markdown_options = MarkdownSaveOptions()
# Export only links and paragraphs from the HTML
markdown_options.features = MarkdownFeature.LINKS | MarkdownFeature.PARAGRAPHS

# Step 3: Convert the HTML to Markdown using the configured options
output_path = "YOUR_DIRECTORY/links_and_paragraphs.md"
Converter.convert(html_doc, markdown_options, output_path)

print(f"Conversion complete. Markdown saved to {output_path}")
```

### Bunun Neden Çalıştığı

- **`HTMLDocument`** orijinal dosyayı ayrıştırır ve dönüştürücünün gezebileceği bir DOM oluşturur.  
- **`MarkdownSaveOptions`** SDK'nin ne yazacağını ince ayarlarla kontrol etmenizi sağlar. `features` değerini `LINKS | PARAGRAPHS` olarak ayarlamak, motorun görselleri, tabloları veya scriptleri yok saymasını söyler; bu da son **html to markdown dosyasındaki** gürültüyü azaltır.  
- **`Converter.convert`** ağır işi yapar. Özellik maskesine uyar, bağlantı etiketlerini (`<a>`) ve paragraf etiketlerini (`<p>`) çıkarır ve bunları standart Markdown sözdizimiyle yazar.  

---

## Tam İçerikle HTML'yi Markdown'a Dönüştürme (isteğe bağlı)

Daha sonra tüm sayfaya—sadece bağlantılar ve paragraflar değil—ihtiyacınız olduğuna karar verirseniz, sadece özellik maskesini ayarlamanız yeterlidir:

```python
# Export everything the SDK supports (links, paragraphs, images, tables, etc.)
markdown_options.features = MarkdownFeature.ALL
```

Aynı dönüşümü şimdi çalıştırmak, orijinal düzeni yansıtan tam bir **html to markdown dosyası** üretir. Bu, **html nasıl markdown'a dönüştürülür** sorusuna esnek bir yanıt gösterir: çıktı, özellik bayraklarını değiştirerek kontrol edilir.

---

## Yalnızca Paragrafları Çıkarma

Bazen bir makalenin metin gövdeleriyle ilgilenirsiniz, bağlantılarla değil. Maskeyi yalnızca `PARAGRAPHS` olarak ayarlayarak paragrafları izole edebilirsiniz:

```python
markdown_options.features = MarkdownFeature.PARAGRAPHS
output_path = "YOUR_DIRECTORY/only_paragraphs.md"
Converter.convert(html_doc, markdown_options, output_path)
```

Ortaya çıkan markdown, hiçbir bağlantı işareti olmadan temiz, satır‑bölünmüş metin içerir. Bu snippet, bir HTML kaynağından **paragrafları nasıl çıkarılır** sorusuna yanıt verir.

---

## Yaygın Tuzaklar ve Nasıl Önlenir

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|-------|
| Boş çıktı dosyası | Kaynak HTML, seçilen özelliklerle eşleşen `<a>` veya `<p>` etiketine sahip değil. | HTML yapısını kontrol edin veya özellik maskesini genişletin (ör. `HEADINGS` ekleyin). |
| Kodlama sorunları | HTML, UTF-8 olmayan bir karakter seti kullanıyor ve SDK bunu yanlış okuyor. | `HTMLDocument`'e açık bir kodlama gönderin, örn. `HTMLDocument(path, encoding="iso-8859-1")`. |
| Mevcut markdown dosyasının üzerine yazma | Betik birden fazla çalıştırıldığında önceki dosyanın üzerine yazar. | Çıktı dosya adına bir zaman damgası ekleyin veya yazmadan önce `os.path.exists` kontrolü yapın. |

**Pro ipucu:** Bir klasörde birçok dosya işlenirken, dönüşüm mantığını bir döngü içinde sarın ve her sonucu kaydedin. Bu, net bir denetim izi sağlar ve bir hata sonrası devam etmeyi kolaylaştırır.

---

## Kopyalayıp Yapıştırabileceğiniz Tam Script

Aşağıda doğrudan çalıştırabileceğiniz, bağımsız bir Python dosyası (`convert_links_paragraphs.py`) yer alıyor. Kodda değişiklik yapmadan giriş ve çıkış yollarını belirtebilmeniz için argüman ayrıştırma içerir.

```python
#!/usr/bin/env python3
"""
convert_links_paragraphs.py

A complete example that shows how to export links and extract paragraphs
when converting HTML to a markdown file using GroupDocs Conversion SDK.
"""

import argparse
import os
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeature, Converter

def convert_html_to_md(input_html: str, output_md: str, features: int) -> None:
    """Perform the conversion with the given feature mask."""
    if not os.path.isfile(input_html):
        raise FileNotFoundError(f"Input file not found: {input_html}")

    # Load the HTML document
    html_doc = HTMLDocument(input_html)

    # Configure markdown options
    md_options = MarkdownSaveOptions()
    md_options.features = features

    # Run the conversion
    Converter.convert(html_doc, md_options, output_md)
    print(f"✅ Conversion finished – markdown saved to: {output_md}")

def main() -> None:
    parser = argparse.ArgumentParser(
        description="How to export links while converting HTML to Markdown."
    )
    parser.add_argument("input", help="Path to the source HTML file.")
    parser.add_argument(
        "output",
        help="Path for the resulting markdown file (e.g., links_and_paragraphs.md).",
    )
    parser.add_argument(
        "--links",
        action="store_true",
        help="Include links in the markdown output.",
    )
    parser.add_argument(
        "--paragraphs",
        action="store_true",
        help="Include paragraphs in the markdown output.",
    )
    args = parser.parse_args()

    # Build the feature mask based on user flags
    selected_features = 0
    if args.links:
        selected_features |= MarkdownFeature.LINKS
    if args.paragraphs:
        selected_features |= MarkdownFeature.PARAGRAPHS

    # Default to both links and paragraphs if no flag is provided
    if selected_features == 0:
        selected_features = MarkdownFeature.LINKS | MarkdownFeature.PARAGRAPHS

    try:
        convert_html_to_md(args.input, args.output, selected_features)
    except Exception as exc:
        print(f"❌ Conversion failed: {exc}")

if __name__ == "__main__":
    main()
```

**Nasıl Çalıştırılır**

```bash
python convert_links_paragraphs.py YOUR_DIRECTORY/input.html YOUR_DIRECTORY/links_and_paragraphs.md --links --paragraphs
```

Yukarıdaki komut, **bağlantıları dışa aktarma** ve **paragrafları çıkarma** işlemlerini tek bir çağrıda gösterir. Çıktıyı ihtiyaçlarınıza göre özelleştirmek için `--links` veya `--paragraphs` bayraklarını çıkarın.

---

## Doğrulama – Çıktının Görünümü

Aşağıdaki basit HTML (`input.html`) verildiğinde:

```html
<!DOCTYPE html>
<html>
<head><title>Sample page</title></head>
<body>
  <p>Welcome to the tutorial.</p>
  <p>Visit <a href="https://example.com">our site</a> for more info.</p>
</body>
</html>
```

Betik her iki bayrakla çalıştırıldığında `links_and_paragraphs.md` üretilir:

```markdown
Welcome to the tutorial.

Visit [our site](https://example.com) for more info.
```

Sadece iki paragraf ve hiperlinkin mevcut olduğunu görebilirsiniz—**bağlantıları dışa aktarma** araması yaparken **html'yi markdown'a dönüştür** istediğiniz tam olarak bu.

---

## Sonraki Adımlar ve İlgili Konular

- **HTML'yi markdown'a dönüştürme** görüntülerle: maskeye `MarkdownFeature.IMAGES` ekleyin.  
- **Paragrafları çıkarmak** ve ardından son işlem yapmak  

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [Java'da HTML'yi Markdown'a Dönüştürürken Ofset Ayarlama](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)
- [Markdown'tan HTML'ye Java - Aspose.HTML ile Dönüştürme](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)
- [HTML'yi Markdown'a Dönüştür – Tam C# Kılavuzu](/html/english/java/conversion-html-to-other-formats/convert-html-to-markdown-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}