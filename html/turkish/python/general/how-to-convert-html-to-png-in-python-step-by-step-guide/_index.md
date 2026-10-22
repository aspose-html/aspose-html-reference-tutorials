---
category: general
date: 2026-10-21
description: HTML'yi hızlı bir şekilde PNG'ye dönüştürmeyi öğrenin. Bu öğreticide
  ayrıca web sayfasını PNG olarak dışa aktarma ve HTML dosyasını Python ile PNG'ye
  dönüştürme konuları da ele alınmaktadır.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to png
- export webpage to png
- how to convert html to image
- convert html file to png
language: tr
lastmod: 2026-10-21
og_description: Python ile HTML'yi PNG'ye dönüştürün. Web sayfasını PNG olarak dışa
  aktarmak, uç durumları ele almak ve görüntü oluşturmayı otomatikleştirmek için bu
  net rehberi izleyin.
og_image_alt: Screenshot of HTML page converted to PNG using Python
og_title: HTML'yi Python'da PNG'ye Dönüştür – Tam Programlama Rehberi
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  headline: How to convert HTML to PNG in Python – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  name: How to convert HTML to PNG in Python – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the script prints:'
  - name: Why adjust viewport size?
    text: Web pages designed for desktop screens often look cramped if rendered at
      a small width. By increasing the `width` and `height` options, you capture the
      full layout, which is especially useful for **export webpage to PNG** tasks.
  - name: 6.1 Large pages or infinite scroll
    text: 'For pages that load content lazily (e.g., infinite scroll), increase the
      JavaScript delay and optionally set a larger viewport:'
  - name: 6.2 Authentication‑protected pages
    text: 'If a page requires a session cookie, you can embed the cookie header:'
  - name: 6.3 Missing images or fonts
    text: '`wkhtmltoimage` respects the `--disable-local-file-access` flag for security.
      If your HTML references local assets, enable them explicitly:'
  type: HowTo
tags:
- python
- html conversion
- image processing
- web automation
title: Python'da HTML'yi PNG'ye Dönüştürme – Adım Adım Rehber
url: /tr/python/general/how-to-convert-html-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert HTML to PNG in Python – complete programming guide

HTML'yi **PNG'ye dönüştürmeniz** gerektiğinde, bu kılavuz size saf Python ile güvenilir bir yol gösterir. Statik bir rapor dışa aktarıyor, bir galeri için küçük resimler oluşturuyor ya da testler için ekran görüntülerini otomatikleştiriyor olun, dakikalar içinde tam, çalıştırılabilir bir çözüm elde edeceksiniz.

Ayrıca **web sayfasını PNG'ye dışa aktarma**, bir HTML dosyasını dönüştürme ile canlı bir URL'yi dönüştürme arasındaki farkı anlama ve büyük sayfalar ya da dinamik içeriklerle çalışırken en iyi uygulamaları öğrenme fırsatı bulacaksınız. Harici hizmetlere gerek yok—sadece birkaç Python paketi ve kısa bir betik yeterli.

## Prerequisites

Başlamadan önce şunların yüklü olduğundan emin olun:

- Python 3.9+ (kod Windows, macOS ve Linux'ta çalışır)
- Bir terminal ya da komut istemcisine erişim
- Python paket yöneticisi (`pip`) ile temel aşinalık

`imgkit` paketine ( `wkhtmltoimage` etrafında ince bir sarmalayıcı) ve `wkhtmltoimage` ikili dosyasına ihtiyacınız olacak. İkisi de ücretsiz ve açık kaynaklıdır.

## Step 1: Install the required tools

İlk adım `wkhtmltoimage` ve ona bağlanan Python sarmalayıcısını kurmaktır.

```bash
# Install wkhtmltoimage (Linux example)
sudo apt-get update && sudo apt-get install -y wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf

# On Windows download the installer from:
# https://wkhtmltopdf.org/downloads.html
# and add the installation folder to your PATH.

# Install the Python wrapper
pip install imgkit
```

> **Why this step matters** – `wkhtmltoimage` HTML'yi WebKit motoru ile render eder ve piksel‑tam PNG'ler üretir. `imgkit` ise seçeneklerinizi ikili dosyaya iletir, böylece bir tarayıcıdan alacağınız kaliteyi elde edersiniz.

## Step 2: Verify the installation

İkili dosyanın Python'dan erişilebilir olduğunu doğrulamak için hızlı bir kontrol çalıştırın.

```python
import imgkit

# This will raise an exception if wkhtmltoimage is not found
print("wkhtmltoimage version:", imgkit.config().wkhtmltoimage)
```

Betik `wkhtmltoimage` yolunu yazdırıyorsa, HTML'yi PNG'ye dönüştürmeye hazırsınız demektir. Bir `OSError` alırsanız, ikili dosyanın sistem `PATH`'inizde olduğundan emin olun.

## Step 3: Write a reusable conversion function

Mantığı bir fonksiyon içinde kapsüllemek, **HTML dosyasını PNG'ye dönüştürme** ya da **web sayfasını PNG'ye dışa aktarma** işlemlerini projenizin herhangi bir yerinden kolayca yapmanızı sağlar.

```python
import os
import imgkit

def convert_html_to_png(source, output_path, *, options=None):
    """
    Convert an HTML file or URL to a PNG image.

    Parameters
    ----------
    source : str
        Path to a local HTML file (e.g., "report.html") or a URL
        (e.g., "https://example.com").
    output_path : str
        Destination file path for the PNG (e.g., "report.png").
    options : dict, optional
        imgkit options such as viewport size, zoom factor, or
        JavaScript delay. If omitted, sensible defaults are used.

    Returns
    -------
    bool
        True if the conversion succeeded, False otherwise.
    """
    # Use a default set of options if none are provided
    default_options = {
        "format": "png",
        "quality": "100",
        "encoding": "UTF-8",
        "quiet": "",
        # Render at 1280×720 – adjust for your layout
        "width": 1280,
        "height": 720,
        # Wait for JavaScript to finish (ms)
        "javascript-delay": 500,
    }
    # Merge user‑supplied options over defaults
    final_options = {**default_options, **(options or {})}

    try:
        # imgkit can handle both files and URLs transparently
        imgkit.from_file(source, output_path, options=final_options) \
            if os.path.isfile(source) else \
            imgkit.from_url(source, output_path, options=final_options)
        print(f"✅ Successfully saved PNG to: {output_path}")
        return True
    except Exception as e:
        print(f"❌ Conversion failed: {e}")
        return False
```

> **Why we wrap both `from_file` and `from_url`** – Aynı fonksiyon artık yerel dosyalar ve canlı web sayfaları için **HTML'yi görüntüye nasıl dönüştürülür** konusunu destekler, kodunuzu DRY (Don’t Repeat Yourself) tutar.

## Step 4: Convert a local HTML file to PNG

`assets` adlı bir klasöre `sample.html` adlı bir HTML dosyası koyun. Ardından az önce tanımladığınız yardımcı fonksiyonu çağırın:

```python
if __name__ == "__main__":
    # Example: convert a static HTML file
    html_path = os.path.join("assets", "sample.html")
    png_path = os.path.join("output", "sample.png")

    # Ensure the output directory exists
    os.makedirs(os.path.dirname(png_path), exist_ok=True)

    # Perform the conversion
    success = convert_html_to_png(html_path, png_path)

    if success:
        # Show a tiny preview in the console (optional)
        from PIL import Image
        img = Image.open(png_path)
        img.thumbnail((200, 200))
        img.show()
```

### Expected output

Betik çalıştırıldığında şu çıktı verir:

```
✅ Successfully saved PNG to: output/sample.png
```

Yeni `output/sample.png` dosyası, `sample.html`'in piksel‑tam bir anlık görüntüsünü içerir. Herhangi bir görüntü görüntüleyicide açtığınızda sayfanın tarayıcıda göründüğü gibi olduğunu göreceksiniz.

## Step 5: Export a live webpage to PNG

Sık sık değişen bir URL (ör. bir gösterge paneli) için **web sayfasını PNG'ye dışa aktarmanız** gerekiyorsa, dosya yolu yerine URL dizesini geçmeniz yeterlidir.

```python
# Example: convert a live page
url = "https://developer.mozilla.org/en-US/docs/Web/HTML"
output_file = "output/mdn_homepage.png"

convert_html_to_png(url, output_file, options={"width": 1920, "height": 1080})
```

### Why adjust viewport size?

Masaüstü ekranları için tasarlanmış web sayfaları, dar bir genişlikte render edildiğinde sıkışık görünebilir. `width` ve `height` seçeneklerini artırarak tam düzeni yakalarsınız; bu özellikle **web sayfasını PNG'ye dışa aktarma** görevlerinde faydalıdır.

## Step 6: Handle common edge cases

### 6.1 Large pages or infinite scroll

İçeriği tembel yükleyen (ör. sonsuz kaydırma) sayfalar için JavaScript gecikmesini artırın ve isteğe bağlı olarak daha büyük bir viewport ayarlayın:

```python
options = {
    "javascript-delay": 2000,   # wait 2 seconds for JS to finish
    "width": 1440,
    "height": 3000,             # tall enough for the whole page
    "disable-smart-width": "", # forces the width we set
}
convert_html_to_png(url, "long_page.png", options=options)
```

### 6.2 Authentication‑protected pages

Bir sayfa oturum çerezi gerektiriyorsa, çerez başlığını gömebilirsiniz:

```python
options = {
    "custom-header": [
        "Cookie: sessionid=YOUR_SESSION_ID"
    ]
}
convert_html_to_png("https://internal.example.com/report", "report.png", options=options)
```

### 6.3 Missing images or fonts

`wkhtmltoimage` güvenlik için `--disable-local-file-access` bayrağını uygular. HTML'niz yerel varlıklara referans veriyorsa, bunları açıkça etkinleştirin:

```python
options = {"enable-local-file-access": ""}
convert_html_to_png("assets/complex.html", "complex.png", options=options)
```

## Step 7: Verify the result programmatically (optional)

Bazen PNG'nin doğru üretildiğini (ör. CI boru hatlarında) doğrulamanız gerekir. Aşağıdaki snippet dosya boyutunu ve boyutlarını kontrol eder:

```python
from pathlib import Path
from PIL import Image

def verify_png(path):
    p = Path(path)
    if not p.is_file():
        raise FileNotFoundError(f"{path} does not exist")
    if p.stat().st_size < 10_000:  # arbitrary minimal size
        raise ValueError("Generated PNG seems too small")
    with Image.open(p) as img:
        print(f"Image size: {img.width}×{img.height}, mode: {img.mode}")

verify_png(png_path)
```

PNG bu kontrolleri geçerse, PDF oluşturma, e‑posta ekleri veya makine‑öğrenimi boru hatları gibi sonraki süreçlerde güvenle kullanabilirsiniz.

## Conclusion

Artık Python kullanarak **HTML'yi PNG'ye dönüştürme** için eksiksiz, üretim‑hazır bir yönteme sahipsiniz. Kılavuz şunları kapsadı:

- `wkhtmltoimage` ve `imgkit` kurulumu
- Ortamın doğrulanması
- Hem yerel dosyalar hem de URL'ler için çalışan yeniden kullanılabilir `convert_html_to_png` fonksiyonu
- **Web sayfasını PNG'ye dışa aktarma**, **HTML'yi görüntüye nasıl dönüştürülür** ve **HTML dosyasını PNG'ye dönüştürme** için gerçek dünya örnekleri
- Büyük sayfalar, kimlik doğrulama ve yerel varlıklar için kenar‑durum yönetimi
- CI/CD boru hatları için isteğe bağlı doğrulama adımları

`imgkit` seçenekleriyle (ör. `zoom`, `crop-h` veya `crop-w`) çıktıyı kendi kullanım senaryonuza göre ince ayar yapmaktan çekinmeyin. İleri adımlar için şunları keşfedebilirsiniz:

- PNG'leri PDF raporuna dönüştürme (`img2pdf` kütüphanesi)
- Tüm bir HTML klasörünün toplu dönüşümünü otomatikleştirme
- Tam tarayıcı render'ı gerektiren sayfalar için Selenium kullanma (ör. ağır JavaScript çerçeveleri)

İyi kodlamalar ve piksel‑tam ekran görüntülerinin tadını çıkarın!


## What Should You Learn Next?


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım‑adım açıklamalı tam çalışan kod örnekleri içerir.

- [Convert HTML to PNG – Complete Python Guide](/html/english/python/general/convert-html-to-png-complete-python-guide/)
- [Convert HTML to PNG in Python – Complete Streaming Save Guide](/html/english/python/general/convert-html-to-png-in-python-complete-streaming-save-guide/)
- [Convert SVG to PNG in Python using Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}