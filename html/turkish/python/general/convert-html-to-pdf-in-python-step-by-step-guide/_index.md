---
category: general
date: 2026-08-06
description: Python’da HTML’yi PDF’ye dönüştürün, tam bir örnekle. HTML’den PDF oluşturmayı,
  HTML’yi PDF olarak kaydetmeyi ve yaygın kenar durumlarını ele almayı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: tr
lastmod: 2026-08-06
og_description: Python'da HTML'yi PDF'ye dönüştürün ve belge oluşturmayı otomatikleştirin.
  Bu kılavuzu izleyerek HTML'den PDF oluşturun, HTML'yi PDF olarak kaydedin ve çıktıyı
  özelleştirin.
og_image_alt: Example of convert html to pdf script in Python
og_title: Python'da HTML'yi PDF'ye dönüştürme – kapsamlı öğretici
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  headline: Convert HTML to PDF in Python – step‑by‑step guide
  type: TechArticle
- description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  name: Convert HTML to PDF in Python – step‑by‑step guide
  steps:
  - name: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
    text: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
  - name: '**Input handling** – read the HTML file or build the markup programmatically.'
    text: '**Input handling** – read the HTML file or build the markup programmatically.'
  - name: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
    text: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
  type: HowTo
tags:
- HTML to PDF
- Python
- Document conversion
title: Python’da HTML’yi PDF’ye Dönüştür – adım adım rehber
url: /tr/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da HTML’yi PDF’ye Dönüştürme – adım adım rehber

HTML’yi **PDF’ye hızlıca dönüştürmeniz** gerektiğinde, bu öğretici Python’da eksiksiz bir çözüm sunar. HTML’den PDF oluşturmayı, HTML’yi PDF olarak kaydetmeyi ve dönüşüm sürecini kodunuzdan çıkmadan kontrol etmeyi öğreneceksiniz.

Kılavuz, güvenilir bir kütüphanenin kurulumu, bir HTML belgesinin yüklenmesi, dönüşümün gerçekleştirilmesi ve sonucun doğrulanması adımlarını size gösterir. Sonunda, kaynak statik bir sayfa ya da dinamik olarak üretilen işaretleme olsun, herhangi bir Python projesinde HTML dosyasından PDF oluşturabilirsiniz.

## Öğrenecekleriniz

* HTML‑to‑PDF dönüşümü için gerekli `pdfkit` ve `wkhtmltopdf` bağımlılıklarını kurun.  
* Diskten ya da bir dizeden HTML belgesi yükleyin.  
* Özel sayfa boyutu, kenar boşlukları ve kodlama seçenekleriyle HTML’den PDF oluşturun.  
* Tek bir fonksiyon çağrısıyla HTML’yi PDF olarak kaydedin.  
* Eksik varlıklar, Unicode karakterler ve büyük dosyalar gibi tipik kenar durumlarını yönetin.  

**Önkoşullar** – Python 3.8+ ve temel dosya I/O bilgisi. Harici hizmetlere ihtiyaç yoktur.

## HTML’yi PDF’ye Dönüştürme – genel iş akışı

Dönüşüm süreci üç mantıksal aşamadan oluşur:

1. **Hazırlık** – dönüştürücüyü kurun ve `wkhtmltopdf` ikili dosyasının erişilebilir olduğundan emin olun.  
2. **Girdi işleme** – HTML dosyasını okuyun veya işaretlemeyi programlı olarak oluşturun.  
3. **Çıktı üretimi** – dönüştürücüyü çalıştırın, PDF dosyasını yazın ve sonucu doğrulayın.

Her aşama aşağıdaki adımlarda ayrıntılı olarak ele alınmıştır.

## Adım 1: Gerekli kütüphaneleri kurun

`pdfkit`, yaygın olarak kullanılan `wkhtmltopdf` motoru etrafında ince bir Python sarmalayıcısı sağlar. İkisini de `pip` ile kurun ve ikili dosya yolunu doğrulayın.

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

Taşınabilir bir ikili dosya tercih ediyorsanız, uygun sürümü [wkhtmltopdf GitHub sayfasından](https://github.com/wkhtmltopdf/wkhtmltopdf/releases) indirip `PATH`’inize eklenen bir klasöre yerleştirin. Betik daha sonra yolu otomatik olarak kontrol eder.

## Adım 2: HTML belgesini yükleyin

Statik bir dosya okuyabilir, uzaktan içerik çekebilir ya da HTML’yi anında oluşturabilirsiniz. Aşağıdaki örnek, tanımladığınız bir klasörde bulunan `sample.html` adlı yerel dosyayı yükler.

```python
import pathlib
import pdfkit

# Define the directory that holds the HTML source
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")

# Resolve the full path to the HTML file
html_path = BASE_DIR / "sample.html"

# Read the file content as a UTF‑8 string
with html_path.open(encoding="utf-8") as f:
    html_content = f.read()
```

Dosyayı Unicode dizesi olarak okumak, “é”, “ß” gibi karakterlerin ya da Asya gliflerinin dönüşüm sırasında korunmasını sağlar. Bu adım, **generate PDF from HTML** içeren uluslararası metinler için kritiktir.

## Adım 3: HTML’den PDF oluşturun

`pdfkit.from_string`, HTML işaretlemesi içeren bir dizeyi PDF dosyasına dönüştürür. Sayfa boyutu, kenar boşlukları ve başlık/altbilgi davranışını kontrol etmek için bir seçenek sözlüğü geçirebilirsiniz.

```python
# Define the output PDF path
pdf_path = BASE_DIR / "sample.pdf"

# Conversion options – adjust as needed
options = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left": "0.75in",
    "encoding": "UTF-8",
    "enable-local-file-access": None,  # Allows loading local images/CSS
}

# Perform the conversion
pdfkit.from_string(html_content, str(pdf_path), options=options)
```

Yukarıdaki çağrı, `sample.pdf` içinde **creates PDF from HTML file** oluşturur. Kaynak HTML yerel CSS veya görseller referans veriyorsa, `enable‑local‑file‑access` bayrağı `wkhtmltopdf`’nin bu kaynakları çözümlemesini sağlar.

### Bu yaklaşım neden çalışır?

* `pdfkit`, ağır işi `wkhtmltopdf`’ye devrederek HTML’yi WebKit motoruyla render eder; bu da orijinal tasarıma yüksek sadakat sağlar.  
* Bir seçenek sözlüğü sağlamak, HTML’i değiştirmeden çıktıyı ince ayar yapmanıza imkan tanır.  
* `from_string` kullanmak, HTML anlık olarak üretildiğinde bellekte kalmasını sağlar ve iş akışını basitleştirir.

## Adım 4: HTML’yi PDF olarak kaydedin ve çıktıyı doğrulayın

Dönüşümden sonra PDF’nin var olduğunu ve okunabilir olduğunu doğrulamak isteyebilirsiniz. Aşağıdaki kod parçası dosya boyutunu kontrol eder ve PDF’yi varsayılan sistem görüntüleyicisiyle (platform‑spesifik) açar.

```python
import os
import subprocess
import sys

# Verify that the PDF file was created
if pdf_path.is_file() and pdf_path.stat().st_size > 0:
    print(f"✅ PDF generated successfully: {pdf_path}")

    # Open the PDF for visual verification (optional)
    if sys.platform.startswith("darwin"):      # macOS
        subprocess.run(["open", str(pdf_path)])
    elif os.name == "nt":                      # Windows
        os.startfile(str(pdf_path))
    else:                                      # Linux and others
        subprocess.run(["xdg-open", str(pdf_path)])
else:
    raise FileNotFoundError("PDF generation failed – file not found or empty.")
```

Betik çalıştırıldığında bir başarı mesajı yazdırır ve PDF görüntüleyiciyi başlatarak düzenin orijinal HTML ile eşleştiğini anında onaylamanızı sağlar. Bu adım **save html as pdf** döngüsünü tamamlar.

## Adım 5: Gelişmiş seçenekler – HTML dosyasından özel ayarlarla PDF oluşturma

Bazen diskte fiziksel bir HTML dosyanız olur ve içeriği kendiniz yüklemek yerine `pdfkit.from_file` tercih edersiniz. Bu yöntem, HTML zaten karmaşık göreli yollar içerdiğinde kullanışlıdır.

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Ayrıca `options` sözlüğünü genişleterek bir kapak sayfası, içindekiler tablosu veya JavaScript yürütme bayrakları ekleyebilirsiniz. Örneğin bir kapak sayfası eklemek için:

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Bu ince ayarlar, daha sofistike yayınlama hatları için **how to convert HTML to PDF** gösterimini ortaya koyar.

## Yaygın hatalar ve nasıl önlenir

| Sorun | Neden | Çözüm |
|-------|-------|--------|
| Görseller veya CSS görünmüyor | `wkhtmltopdf` varsayılan olarak yerel dosya erişimini engeller | Seçenekler sözlüğüne `"enable-local-file-access": None` ekleyin |
| Unicode karakterler bozuluyor | `encoding` seçeneği eksik veya dosya yanlış karakter setiyle okunuyor | Her zaman `"encoding": "UTF-8"` ayarlayın ve HTML dosyasını UTF‑8 ile okuyun |
| PDF boş | `wkhtmltopdf` ikili dosyasının yolu hatalı | Yolu açıkça belirtin: `pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| Büyük HTML dosyaları zaman aşımına sebep oluyor | Varsayılan zaman aşımı çok kısa | `"javascript-delay": "2000"` ayarlayın veya `"timeout": "60"` ile zaman aşımını artırın |

Bu sorunları çözmek, farklı ortamlar arasında güvenilir bir **generate pdf from html** süreci sağlar.

## Tam betik – uçtan uca örnek

Aşağıdakini `html_to_pdf.py` olarak kaydedin ve `python html_to_pdf.py` ile çalıştırın. `YOUR_DIRECTORY` değerini projenizin klasörüne göre ayarlayın.

```python
#!/usr/bin/env python3
"""
Convert HTML to PDF in Python – complete, runnable example.
"""

import pathlib
import pdfkit
import os
import subprocess
import sys

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")          # <-- change this
HTML_FILE = BASE_DIR / "sample.html"
PDF_FILE = BASE_DIR / "sample.pdf"

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## Sonraki Öğrenilecek Konular

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [HTML'yi PDF'ye Dönüştürme Java – Aspose.HTML for Java Kullanarak](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [HTML'yi PDF'ye Dönüştürme .NET'te Aspose.HTML ile](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [HTML'yi PDF'ye Dönüştürme Java – Aspose.HTML ile Sayfa Kenar Boşluklarını Ayarlama](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}