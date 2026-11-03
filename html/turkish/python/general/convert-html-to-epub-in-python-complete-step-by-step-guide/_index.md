---
category: general
date: 2026-07-18
description: Python’da HTML’yi hızlıca EPUB’a dönüştürün. Python’da HTML dosyasını
  nasıl yükleyeceğinizi ve basit kütüphanelerle HTML’yi MHTML’ye nasıl dönüştüreceğinizi
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to epub
- load html file in python
- convert html to mhtml
language: tr
lastmod: 2026-07-18
og_description: Python'da net, çalıştırılabilir bir örnekle HTML'yi EPUB'a dönüştürün.
  Ayrıca Python'da HTML dosyasını nasıl yükleyeceğinizi ve HTML'yi dakikalar içinde
  MHTML'ye nasıl dönüştüreceğinizi öğrenin.
og_image_alt: Diagram showing convert html to epub workflow
og_title: Python’da HTML’yi EPUB’a Dönüştür – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  headline: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  name: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Python 3.9+** – the syntax used here works on any recent version.'
    text: '**Python 3.9+** – the syntax used here works on any recent version.'
  - name: '**pip** – to install third‑party packages.'
    text: '**pip** – to install third‑party packages.'
  - name: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
    text: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
  type: HowTo
tags:
- python
- html
- epub
- mhtml
- file conversion
title: Python’da HTML’yi EPUB’a Dönüştür – Tam Adım Adım Kılavuz
url: /tr/python/general/convert-html-to-epub-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da HTML'yi EPUB'a Dönüştürme – Tam Adım‑Adım Kılavuz

Hiç **HTML'yi EPUB'a dönüştürmenin** nasıl yapılacağını merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler sürekli olarak web sayfalarını çevrim dışı okuma için e‑kitaplara dönüştürmek zorunda kalıyor ve bunu Python'da yapmak şaşırtıcı derecede sorunsuz. Bu öğreticide bir HTML dosyasını Python'da yüklemeyi, o HTML'yi EPUB'a dönüştürmeyi ve aynı kaynağı e‑posta dostu arşivler için MHTML'ye çevirmeyi adım adım göstereceğiz.

Kılavuzun sonunda, tek bir `sample.html` dosyasını alıp hem `sample.epub` hem de `sample.mhtml` üreten, çalıştırmaya hazır bir betiğiniz olacak. Gizem yok, sadece net kod ve açıklamalar.

---

![Dönüştürme boru hattı diyagramı](https://example.com/images/convert-html-epub.png "HTML'yi EPUB'a dönüştürme iş akışını gösteren diyagram")

## Oluşturacağınız Şeyler

- **Python'da bir HTML dosyasını** yerleşik `pathlib` ve `io` modüllerini kullanarak yükleyin.  
- **HTML'yi EPUB'a** `ebooklib` kütüphanesi ile dönüştürün; bu kütüphane EPUB konteyner formatını sizin için halleder.  
- **HTML'yi MHTML'ye** (MHT olarak da bilinir) `email` paketiyle dönüştürün; böylece tarayıcıların doğrudan açabileceği tek‑dosyalı bir web arşivi oluşturmuş olursunuz.  

Ayrıca şunları da ele alacağız:

- Gerekli bağımlılıklar ve nasıl kurulacağı.  
- Betiğinizin hataları nazikçe ele alması için hata yönetimi.  
- EPUB dosyası için başlık ve yazar gibi meta verileri nasıl özelleştireceğiniz.  

Hazır mısınız? Hadi başlayalım.

---

## Önkoşullar

Kodlamaya başlamadan önce şunların olduğundan emin olun:

1. **Python 3.9+** – burada kullanılan sözdizimi herhangi bir yeni sürümde çalışır.  
2. **pip** – üçüncü‑taraf paketleri kurmak için.  
3. Kontrol ettiğiniz bir klasörde bulunan basit bir HTML dosyası, ör. `sample.html`.  

Eğer bunlara sahipseniz, harika—bir sonraki bölüme geçin.  

> **Pro ipucu:** HTML'nizin iyi biçimlenmiş olmasına (doğru `<head>` ve `<body>` bölümleri) dikkat edin. `ebooklib` küçük sorunları düzeltmeye çalışsa da, temiz bir kaynak ileride baş ağrısı yaşamamanızı sağlar.

---

## Adım 1 – Gerekli Kütüphaneleri Kurun

İki dış paket ihtiyacımız var:

- **ebooklib** – EPUB oluşturma için.  
- **beautifulsoup4** – isteğe bağlı, ancak dönüşümden önce HTML'i temizlemek için kullanışlı.

Terminalinizde şu komutu çalıştırın:

```bash
pip install ebooklib beautifulsoup4
```

> **Neden bu kütüphaneler?** `ebooklib`, `META‑INF` klasörü, `content.opf` ve `toc.ncx` dosyalarını otomatik olarak yöneterek ZIP‑tabanlı EPUB yapısını sizin için oluşturur. `beautifulsoup4` ise HTML'i düzenlememizi sağlar, böylece son e‑kitap tüm okuyucularda doğru şekilde görüntülenir.

---

## Adım 2 – Python'da HTML Dosyasını Yükleyin

HTML dosyasını yüklemek oldukça basit, ancak daha sonra işlemek üzere bir **BeautifulSoup** nesnesi döndüren küçük bir yardımcı fonksiyonla sarmalayacağız.

```python
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(filepath: str) -> BeautifulSoup:
    """
    Load an HTML file from disk and return a BeautifulSoup object.
    Raises FileNotFoundError if the file does not exist.
    """
    path = Path(filepath)
    if not path.is_file():
        raise FileNotFoundError(f"HTML file not found: {filepath}")

    # Read the file using UTF‑8 encoding (most common for web content)
    html_content = path.read_text(encoding="utf-8")
    # Parse with BeautifulSoup for optional cleaning later
    soup = BeautifulSoup(html_content, "html.parser")
    return soup
```

**Açıklama:**  
- `Path`, işletim sistemi bağımsız dosya işlemleri sağlar.  
- `read_text` kullanmak, manuel `open`/`close` kodundan kurtarır.  
- Bir `BeautifulSoup` nesnesi döndürmek, daha sonra script'lerde script etiketlerini kaldırmamıza, kırık etiketleri düzeltmemize veya stil sayfası eklememize olanak tanır; ardından **HTML'yi EPUB'a dönüştürürüz**.

---

## Adım 3 – HTML'yi EPUB'a Dönüştürün

Artık **Python'da HTML dosyasını yükleyebildiğimize** göre, temiz bir EPUB oluşturabiliriz. Aşağıdaki fonksiyon bir `BeautifulSoup` nesnesi, hedef yol ve isteğe bağlı meta verileri alır.

```python
import uuid
from ebooklib import epub

def html_to_epub(soup: BeautifulSoup,
                 output_path: str,
                 title: str = "Untitled Book",
                 author: str = "Anonymous") -> None:
    """
    Convert a BeautifulSoup HTML document to an EPUB file.
    """
    # Create a new EPUB book instance
    book = epub.EpubBook()

    # Set basic metadata – this is what shows up in e‑reader libraries
    book.set_identifier(str(uuid.uuid4()))
    book.set_title(title)
    book.set_language('en')
    book.add_author(author)

    # Convert the soup back to a string; we could also clean it here
    html_str = str(soup)

    # Create a chapter (EPUB requires at least one)
    chapter = epub.EpubHtml(title=title,
                            file_name='chap_01.xhtml',
                            lang='en')
    chapter.content = html_str
    book.add_item(chapter)

    # Define the spine (reading order) and table of contents
    book.toc = (epub.Link('chap_01.xhtml', title, 'intro'),)
    book.spine = ['nav', chapter]

    # Add default navigation files
    book.add_item(epub.EpubNcx())
    book.add_item(epub.EpubNav())

    # Write the final EPUB file
    epub.write_epub(output_path, book, {})

    print(f"✅ EPUB created at: {output_path}")
```

**Bu nasıl çalışıyor:**  
- `ebooklib.epub.EpubBook`, ZIP konteyneri ve gerekli manifest dosyalarını soyutlayarak işler.  
- Tekrarlayan kimlik çakışmalarını önlemek için bir UUID oluştururuz.  
- `spine`, okuyuculara bölümlerin sırasını bildirir; tek‑bölümlü bir kitap çoğu basit HTML kaynağı için yeterlidir.  

**Dönüştürmeyi çalıştırma:**

```python
if __name__ == "__main__":
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_epub(html_doc,
                 "YOUR_DIRECTORY/sample.epub",
                 title="My Sample eBook",
                 author="Jane Developer")
```

Betik çalıştığında, EPUB dosyasının konumunu gösteren yeşil bir onay işareti göreceksiniz.

---

## Adım 4 – HTML'yi MHTML'ye Dönüştürün

MHTML (veya MHT), HTML ve tüm kaynaklarını (görseller, CSS) tek bir MIME dosyasında paketler. Python'un `email` paketi, harici bağımlılık olmadan bu formatı oluşturabilir.

```python
import mimetypes
import base64
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email import encoders

def html_to_mhtml(soup: BeautifulSoup,
                  output_path: str,
                  base_url: str = "") -> None:
    """
    Convert a BeautifulSoup HTML document to an MHTML file.
    `base_url` is used to resolve relative resource links.
    """
    # Create the multipart/related container required for MHTML
    mhtml = MIMEMultipart('related')
    mhtml['Subject'] = 'Converted MHTML document'
    mhtml['Content-Type'] = 'multipart/related; type="text/html"'

    # Main HTML part
    html_part = MIMEText(str(soup), 'html', 'utf-8')
    html_part.add_header('Content-Location', 'file://index.html')
    mhtml.attach(html_part)

    # Optional: embed images referenced in the HTML
    for img in soup.find_all('img'):
        src = img.get('src')
        if not src:
            continue

        # Resolve absolute path if needed
        img_path = Path(base_url) / src if base_url else Path(src)
        if not img_path.is_file():
            continue  # skip missing files

        # Guess MIME type; default to octet-stream
        mime_type, _ = mimetypes.guess_type(img_path)
        mime_type = mime_type or 'application/octet-stream'

        with img_path.open('rb') as f:
            img_data = f.read()

        img_part = MIMEBase(*mime_type.split('/'))
        img_part.set_payload(img_data)
        encoders.encode_base64(img_part)
        img_part.add_header('Content-Location', f'file://{src}')
        img_part.add_header('Content-Transfer-Encoding', 'base64')
        mhtml.attach(img_part)

    # Write the MHTML file
    with open(output_path, 'wb') as out_file:
        out_file.write(mhtml.as_bytes())

    print(f"✅ MHTML created at: {output_path}")
```

**Önemli noktalar:**  

- `multipart/related` MIME türü, tarayıcılara HTML kısmının ve kaynakların birlikte olduğunu söyler.  
- `<img>` etiketlerini dolaşarak görselleri gömüyoruz; görsellere ihtiyacınız yoksa bu bloğu atlayabilirsiniz.  
- `Content-Location`, tarayıcıların kaynakları dahili olarak çözümleyebilmesi için bir `file://` URI'si kullanır.  

**Fonksiyonu çağırma:**

```python
if __name__ == "__main__":
    # Re‑use the previously loaded soup
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_mhtml(html_doc, "YOUR_DIRECTORY/sample.mhtml", base_url="YOUR_DIRECTORY")
```

Artık `sample.epub` ve `sample.mhtml` yan yana duruyor.

---

## Tam Betik – Tüm Adımlar Tek Dosyada

Aşağıda her şeyi birleştiren, çalıştırmaya hazır tam betik yer alıyor. `convert_html.py` olarak kaydedin ve `YOUR_DIRECTORY` kısmını `sample.html` dosyanızın bulunduğu klasörün yolu ile değiştirin.



## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [How to Convert EPUB to PDF with Java – Using Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [How to Convert EPUB to Images with Aspose.HTML for Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}