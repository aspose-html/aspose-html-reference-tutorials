---
category: general
date: 2026-10-12
description: HTML'yi hızlıca markdown'a dönüştürün ve markdown'da resim eklemeyi öğrenin.
  Bu rehber, tam kodla birlikte Python kullanarak HTML'den markdown'a dönüşümü adım
  adım anlatıyor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to embed images in markdown
- html to markdown conversion python
- how to convert html page to markdown
language: tr
lastmod: 2026-10-12
og_description: HTML'yi markdown'a dönüştürün ve Python kullanarak markdown içinde
  resimleri gömün. Güvenilir HTML'den markdown'a dönüşüm için bu kapsamlı öğreticiyi
  izleyin.
og_image_alt: Screenshot showing a Python script that converts an HTML file to a markdown
  file with base64‑encoded images
og_title: HTML'yi Python'da gömülü görsellerle markdown'a dönüştürün – adım adım rehber
schemas:
- author: GroupDocs
  dateModified: '2026-10-12'
  description: convert HTML to markdown quickly and learn how to embed images in markdown.
    This guide walks through html to markdown conversion python with full code.
  headline: How to convert HTML to markdown with embedded images using Python
  type: TechArticle
tags:
- markdown
- html
- python
- document conversion
title: Python kullanarak gömülü resimlerle HTML'yi markdown'a nasıl dönüştürürüm
url: /tr/python/general/how-to-convert-html-to-markdown-with-embedded-images-using-p/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'yi gömülü resimlerle Python kullanarak markdown'a nasıl dönüştürürsünüz

Her bir resmi koruyarak **HTML'yi markdown'a dönüştürmeniz** gerekiyorsa, bu kılavuz tam olarak nasıl yapacağınızı gösterir. Dönüşüm motorunu resimleri Base64 olarak gömmek üzere yapılandırarak, her yerde çalışan tek bir, bağımsız `.md` dosyası elde edersiniz—GitHub README'larından statik site jeneratörlerine kadar.

Ayrıca **markdown içinde resimleri nasıl gömeceğinizi**, yerleşik kaynak işleme seçeneklerinin neden en güvenilir tercih olduğunu ve sadece birkaç satır kodla **html to markdown conversion python** nasıl yapılacağını öğreneceksiniz.

## Ne elde edeceksiniz

- Herhangi bir yerel HTML sayfasını temiz bir Markdown belgesine dönüştürün.  
- Her resmi doğrudan Markdown dosyasına Base64 dizesi olarak gömün, kırık bağlantıları ortadan kaldırın.  
- İşlemi Python 3.9+ ve GroupDocs Conversion kütüphanesini destekleyen herhangi bir platformda çalıştırın.

## Önkoşullar

| Gereksinim | Sebep |
|------------|-------|
| Python 3.9 or newer | GroupDocs Conversion SDK'sı tarafından gereklidir. |
| `groupdocs-conversion` package | `Converter`, `HTMLDocument`, `MarkdownSaveOptions` ve `ResourceHandlingOptions` sağlar. |
| An existing HTML file (e.g., `page.html`) | Dönüştürmek istediğiniz kaynak. |
| Write permission to the output folder | Oluşturulan `.md` dosyasını kaydetmek için. |

SDK'yı pip ile kurun:

```bash
pip install groupdocs-conversion
```

> **Pro ipucu:** Bağımlılıkları izole tutmak için bir sanal ortam (`python -m venv .venv`) kullanın.

## Adım 1: Kaynak işleme ayarını markdown içinde resimleri gömmek için yapılandırma

Dönüşüm motoru bir `<img>` etiketiyle karşılaştığında, resmi ayrı bir klasöre kopyalayabilir veya doğrudan gömebilir. Gömme, Base64 kodlu bir data URI üretir; bu da **how to embed images in markdown**'ın tam olarak gerektirdiği şeydir.

```python
from groupdocs.conversion import ResourceHandlingOptions

# Create a resource handling configuration
resource_options = ResourceHandlingOptions()
# Enable embedding of images as Base64 data URIs
resource_options.embed_images = True   # Embeds images directly in the Markdown file
```

**Neden önemli:**  
Gömme, Markdown dosyasının taşınabilir kalmasını garanti eder. `.md` dosyasını eşlik eden resim klasörü olmadan paylaşırsanız bile, resimler data URI'larını destekleyen herhangi bir platformda (GitHub, GitLab, VS Code önizleme vb.) doğru şekilde görüntülenir.

## Adım 2: Kaynak yapılandırmasını kullanarak Markdown kaydetme seçeneklerini ayarlama

`MarkdownSaveOptions` sınıfı, yukarıda oluşturulan `resource_options`'ı geçirmenizi sağlar. Ayrıca satır sonlarını, başlık stillerini ve daha fazlasını ince ayar yapmanıza imkan tanır, ancak çoğu durumda varsayılanlar yeterlidir.

```python
from groupdocs.conversion import MarkdownSaveOptions

# Attach the resource handling to the markdown save options
markdown_options = MarkdownSaveOptions(resource_handling_options=resource_options)
```

**Arka planda neler oluyor:**  
Dönüşüm sırasında motor, HTML DOM'u tarar, her öğeyi karşılık gelen Markdown'a dönüştürür ve `<img src="...">` etiketini `![alt text](data:image/...;base64,...)` ile değiştirir. `resource_options.embed_images` bayrağı bu davranışı tetikler.

## Adım 3: HTML belgesini markdown'a dönüştürme ve sonucu kaydetme

Şimdi her şeyi bir araya getiriyorsunuz: kaynak HTML'i yükleyin, kaydetme seçeneklerini uygulayın ve çıktı dosyasını yazın.

```python
from groupdocs.conversion import Converter, HTMLDocument

# Path to the source HTML file
source_path = "YOUR_DIRECTORY/page.html"
# Desired output path for the markdown file
output_path = "YOUR_DIRECTORY/page.md"

# Perform the conversion
Converter.convert_html(
    HTMLDocument(source_path),
    markdown_options,
    output_path
)

print(f"✅ Conversion complete! Markdown saved to: {output_path}")
```

**Beklenen çıktı:**  

- `page.md` Markdown metni, başlıklar, listeler ve **gömülü resimler** Base64 dizeleri içerir.  
- `page.md` bir Markdown görüntüleyicide açıldığında, tüm resimler dahil orijinal HTML düzeni dışarıdan bir varlık olmadan gösterilir.

### Hızlı kopyala‑yapıştır için tam betik

```python
# convert_html_to_markdown.py
from groupdocs.conversion import (
    Converter,
    HTMLDocument,
    MarkdownSaveOptions,
    ResourceHandlingOptions,
)

def convert_html_to_markdown(src_html: str, dst_md: str) -> None:
    """Convert an HTML file to markdown with images embedded as Base64."""
    # 1️⃣ Embed images
    resource_opts = ResourceHandlingOptions()
    resource_opts.embed_images = True

    # 2️⃣ Prepare markdown options
    md_opts = MarkdownSaveOptions(resource_handling_options=resource_opts)

    # 3️⃣ Run conversion
    Converter.convert_html(
        HTMLDocument(src_html),
        md_opts,
        dst_md
    )
    print(f"✅ Markdown file created at: {dst_md}")

if __name__ == "__main__":
    # Adjust these paths to your environment
    convert_html_to_markdown(
        src_html="YOUR_DIRECTORY/page.html",
        dst_md="YOUR_DIRECTORY/page.md"
    )
```

Betik çalıştırın:

```bash
python convert_html_to_markdown.py
```

## Yaygın kenar durumlarını ele alma

| Durum | Çözüm |
|-----------|----------|
| **Büyük resimler devasa markdown dosyalarına neden olur** | Gömmeden önce resmi yeniden boyutlandırarak veya dönüşümden önce bir görüntü‑optimizasyon kütüphanesi (ör. Pillow) kullanarak görüntü boyutunu sınırlayın. |
| **Göreli resim URL'leri projenin dışına işaret ediyor** | HTML referanslarının erişilebilir olduğundan emin olun veya dönüşümden önce bu resimleri aynı klasöre kopyalayın. |
| **Gömme yerine ayrı resim dosyalarına ihtiyacınız var** | `resource_options.embed_images = False` ayarlayın ve resimlerin kaydedileceği bir `resource_folder` yolu sağlayın. |
| **Bozuk HTML'de dönüşüm başarısız olur** | `BeautifulSoup` (`html5lib` ayrıştırıcı) ile HTML'i ön‑işlemden geçirerek bozuk etiketleri temizleyin, ardından dönüştürücüye verin. |

## Sonucu doğrulama

Oluşturulan `page.md` dosyasını herhangi bir Markdown görüntüleyicide açın:

```bash
code YOUR_DIRECTORY/page.md   # VS Code preview
```

Orijinal başlıkları, paragrafları ve resimleri doğru şekilde render edilmiş olarak görmelisiniz. Bir resim kırık bağlantı olarak görünüyorsa, `embed_images`'ın `True` olarak ayarlandığını ve kaynak HTML'nin geçerli `<img>` etiketleri içerdiğini tekrar kontrol edin.

## Sonraki adımlar ve ilgili konular

- **Export to other formats** – Aynı `Converter` sınıfı PDF, DOCX veya düz metin üretebilir. `MarkdownSaveOptions` yerine `PdfSaveOptions` veya `DocxSaveOptions` kullanın.  
- **Batch processing** – HTML dosyalarının bir dizini döngüye alarak bir Markdown belge koleksiyonu oluşturun.  
- **Custom image handling** – `ResourceHandlingOptions` aracılığıyla bir geri çağırma (callback) uygulayarak resimleri bir CDN'de depolayın ve data URI'yi bir CDN URL'siyle değiştirin.  
- **Advanced markdown features** – `markdown_options` özelliklerini ayarlayarak GitHub‑flavored markdown'ı (tablolar, görev listeleri) etkinleştirin.

**html to markdown conversion python**'ı ustalaştığınız için, artık tekrarlanabilir, üretim‑hazır bir iş akışına sahipsiniz; bu, resimlerin içerikle birlikte kalmasını garanti eder. Yukarıdaki seçeneklerle denemeler yapmaktan ve betiği kendi içerik hatlarına uyarlamaktan çekinmeyin.

---

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım‑adım açıklamalarla tam çalışan kod örnekleri içerir.

- [HTML'yi .NET'te Aspose.HTML ile Markdown'a Dönüştür](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [HTML'yi Java için Aspose.HTML ile Markdown'a Dönüştür](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Aspose HTML Converter (Java) kullanarak Markdown'tan PDF Oluştur](/html/english/java/conversion-html-to-other-formats/create-pdf-from-markdown-using-aspose-html-converter-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}