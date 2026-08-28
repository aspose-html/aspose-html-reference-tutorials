---
category: general
date: 2026-07-02
description: Python kullanarak bir HTML dosyasından simgeleri nasıl çıkarılır. HTML
  dosyasını Python ile okuma, HTML belgesini ayrıştırma ve favicon URL'lerini elde
  etmek için href özniteliğini çıkarma öğrenin.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: tr
og_description: Python kullanarak bir HTML sayfasından simgeleri nasıl çıkarabilirsiniz.
  Bu öğretici, HTML dosyasını Python ile nasıl okuyacağınızı, belgeyi nasıl ayrıştıracağınızı
  ve favicon URL'lerini nasıl elde edeceğinizi gösterir.
og_title: HTML'den Simgeleri Nasıl Çıkarabilirsiniz – Python Rehberi
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to extract icons from an HTML file using Python. Learn to read
    HTML file python, parse HTML document, and extract href attribute to get favicon
    URLs.
  headline: How to Extract Icons from HTML with Python – Complete Guide
  type: TechArticle
- questions:
  - answer: Some sites embed icons via `<meta itemprop="image">`. Extend `is_icon_link`
      to also check for `meta` with `itemprop="image"` and pull its `content` attribute.
    question: What if the HTML uses `<meta>` tags for icons?
  - answer: Yes—just feed each URL into `requests.get(url, stream=True)` and write
      the content to a file. Remember to handle relative URLs with `urljoin`.
    question: Can I fetch the icons automatically?
  - answer: 'Absolutely. Replace the file‑reading step with `requests.get(page_url).text`
      and pass the HTML string to BeautifulSoup. Just be mindful of robots.txt and
      rate limits. --- ## Wrap‑Up We’ve covered **how to extract icons** from any
      static HTML using Python, from reading the file to printing out each f'
    question: Does this work on remote pages?
  type: FAQPage
tags:
- python
- html-parsing
- web‑scraping
- favicon
title: Python ile HTML'den Simge Çıkarma – Tam Kılavuz
url: /tr/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'den Python ile Simge Çıkarma – Tam Kılavuz

Hiç bir web sayfasından **simge nasıl çıkarılır** diye merak ettiniz mi, tarayıcı açmadan? Belki bir site‑katalogu, bir SEO denetim aracı oluşturuyorsunuz ya da sekmelerde görülen küçük favikonlarla sadece merak ediyorsunuz. İyi haber şu ki, bunu birkaç satır Python ile yapabilirsiniz—Selenium, headless Chrome gerekmez, sadece düz‑metin bir HTML dosyası yeter.

Bu öğreticide bir HTML dosyasını python ile okuma, HTML belgesini ayrıştırma ve sonunda `<link rel="icon">` etiketlerinden **href özniteliğini çıkarma** sürecini adım adım göstereceğiz. Sonunda, herhangi bir statik HTML dosyasında çalışacak yeniden kullanılabilir bir kod parçacığına sahip olacaksınız ve ayrıca göreli yollar ya da birden fazla simge bildirimi gibi uç durumları nasıl ele alacağınızı göreceksiniz.

## Öğrenecekleriniz

- Python ile yerel bir HTML dosyasını yükleme (read html file python)  
- Hafif bir ayrıştırıcı kullanarak **HTML belgesini ayrıştırma** güvenli bir şekilde  
- `<link>` öğelerini bulma ve bir simge tanımlayanları tespit etme  
- **href özniteliği** değerlerini çıkarma ve bunları mutlak URL'lere dönüştürme  
- Keşfedilen tüm **favicon URL'lerini** toplama ve yazdırma  

Harici hizmetlere gerek yok—sadece standart kütüphane ve popüler **BeautifulSoup** paketini kullanarak.

---

![Python betiği kullanarak simge çıkarma](https://example.com/images/extract-icons-python.png "simge çıkarma")

*Image alt text: "Python betiği kullanarak simge çıkarma"*

## Ön Koşullar

- Python 3.8+ yüklü  
- `beautifulsoup4` kütüphanesi (`pip install beautifulsoup4`)  
- Tarama yapmak istediğiniz yerel bir HTML dosyası (ör. `sample.html`)  

Eğer bunlar zaten yüklüyse, hemen başlayalım.

## Adım 1: HTML Dosyasını Python ile Oku – Belgeyi Yükle

İlk olarak: dosyayı açmamız ve içeriğini bir ayrıştırıcıya vermemiz gerekiyor. `with open(..., "r", encoding="utf‑8")` kullanmak, dosyanın otomatik olarak kapanmasını garanti eder ve UTF‑8 kodlaması çoğu modern sayfayı işler.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**Neden önemli:** Dosyayı doğru kodlamayla açmak, daha sonra ayrıştırıcıyı bozabilecek gizemli `�` karakterlerinin oluşmasını önler. Standart kütüphaneden `Path` kullanmak da kodun platformlar arası çalışmasını sağlar.

## Adım 2: HTML Belgesini Ayrıştır – Tüm Simge Bağlantılarını Bul

Şimdi ham HTML'i **BeautifulSoup**'a veriyoruz; bu, gezilebilir bir ağaç oluşturur. `rel` özniteliği içinde `icon` kelimesi geçen her `<link>` etiketine bakacağız. `rel` bir boşlukla ayrılmış liste (`rel="shortcut icon"`) olabilir, bu yüzden esnek bir kontrol yapmamız gerekir.

```python
# Step 2: Parse the HTML and locate <link> tags that declare an icon
soup = BeautifulSoup(html_content, "html.parser")

def is_icon_link(tag):
    """Return True if a <link> tag declares an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    # BeautifulSoup may return a list or a string; handle both
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

icon_links = [tag for tag in soup.find_all(is_icon_link)]
```

**Neden bu adım kritik:** Naif bir `soup.find_all("link", rel="icon")` ifadesi, `rel="shortcut icon"` ya da `rel="apple-touch-icon"` gibi varyasyonları kaçırır. Yardımcı fonksiyonumuz `is_icon_link` bu durumları kapsar ve çıkarımı sağlamlaştırır.

## Adım 3: href Özniteliğini Çıkar – URL'leri Al

İlgili etiketleri topladıktan sonra, her birinden `href` özniteliğini alıyoruz. Bazı sayfalar `href`'i atlayabilir (nadir ama mümkün), bu yüzden `None` kontrolü yapıyoruz. Ayrıca, favikonlar genellikle göreli URL'lerle belirtilir; bu yüzden sayfanın temel URL'si biliniyorsa ona göre çözümleyeceğiz. Yerel bir dosya için yolu olduğu gibi tutacağız.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**Neden boşlukları temizliyoruz:** HTML yazarları bazen URL'lerin etrafına yanlışlıkla boşluk ekler, bu da sonraki isteği bozar. Kesme (trim) işlemi temiz stringler elde etmemizi sağlar.

## Adım 4: Favicon URL'lerini Çıkar – Sonuçları Görüntüle

Son olarak, keşfedilen URL listesini yazdırıyoruz (veya döndürüyoruz). Gerçek bir senaryoda bunları bir CSV'ye yazabilir, simgeleri indirebilir ya da başka bir servise besleyebilirsiniz. İşte konsolda sonucu gösteren basit bir döngü.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### Kenar Durumlarını Ele Alma

- **Birden fazla rel değeri:** `is_icon_link` kontrolümüz zaten `rel="shortcut icon"` ve `rel="apple-touch-icon"` durumlarını yakalar.  
- **Göreli yollar:** Daha sonra mutlak URL'lere ihtiyacınız olursa `urllib.parse.urljoin(base_url, href)` kullanın.  
- **Eksik href:** `if href:` koruması hatalı etiketleri atlar, `NoneType` hatalarını önler.  
- **Çift kayıtlar:** `icon_urls = list(dict.fromkeys(icon_urls))` ile tekrarları kaldırabilirsiniz.

---

## Tam Script – Tek Çözüm

Hepsini bir araya getirerek, tam ve çalıştırılabilir programı aşağıda bulabilirsiniz. `extract_icons.py` olarak kaydedin ve `html_path` değişkenini istediğiniz dosyaya yönlendirin.

```python
#!/usr/bin/env python3
"""
How to extract icons from an HTML file using Python.

This script:
- Reads an HTML file (read html file python)
- Parses the HTML document (parse html document)
- Finds <link> tags with rel containing "icon"
- Extracts the href attribute (extract href attribute)
- Prints each favicon URL (extract favicon urls)
"""

from pathlib import Path
from bs4 import BeautifulSoup

def is_icon_link(tag):
    """Detect <link> tags that declare an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

def extract_favicon_urls(html_path: Path):
    """Return a list of favicon URLs found in the given HTML file."""
    html_content = html_path.read_text(encoding="utf-8")
    soup = BeautifulSoup(html_content, "html.parser")
    icon_links = [t for t in soup.find_all(is_icon_link)]

    urls = []
    for tag in icon_links:
        href = tag.get("href")
        if href:
            urls.append(href.strip())
    # Remove duplicates while preserving order
    return list(dict.fromkeys(urls))

if __name__ == "__main__":
    # Adjust the path to point to your HTML file
    html_file = Path("sample.html")
    favicon_urls = extract_favicon_urls(html_file)

    if not favicon_urls:
        print("No icon links found in the document.")
    else:
        for url in favicon_urls:
            print("Favicon URL:", url)
```

**Beklenen çıktı** (örnek `sample.html` iki simge içeriyorsa):

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

`python extract_icons.py` komutuyla çalıştırın ve URL'lerin konsola yazdırıldığını göreceksiniz.

---

## Sık Sorulan Sorular

**S: HTML `<meta>` etiketlerini simge için kullanırsa ne olur?**  
**C:** Bazı siteler simgeleri `<meta itemprop="image">` ile gömer. `is_icon_link` fonksiyonunu `meta` etiketinde `itemprop="image"` kontrolü ekleyerek ve `content` özniteliğini çekerek genişletebilirsiniz.

**S: Simge dosyalarını otomatik olarak indirebilir miyim?**  
**C:** Evet—her URL'yi `requests.get(url, stream=True)` ile alıp içeriği bir dosyaya yazabilirsiniz. Göreli URL'leri `urljoin` ile ele almayı unutmayın.

**S: Bu uzaktan sayfalarda çalışır mı?**  
**C:** Kesinlikle. Dosya‑okuma adımını `requests.get(page_url).text` ile değiştirip HTML string'ini BeautifulSoup'a geçirin. Robots.txt ve istek oranı limitlerine dikkat edin.

---

## Özet

Herhangi bir statik HTML'den **simge nasıl çıkarılır** konusunu Python ile ele aldık; dosyayı okumaktan her favicon URL'sini yazdırmaya kadar. Dosyayı okuma, belgeyi ayrıştırma, doğru etiketleri bulma ve `href` özniteliğini çekme temelleri, birçok web‑kazıma görevinde tekrar kullanılabilecek kalıplardır.

Sonraki adımlar? Scripti şu şekilde genişletmeyi deneyin:

- Göreli URL'leri sayfanın temel URL'sine göre çözümleme  
- Her simgeyi indirip yerel olarak kaydetme  
- Ek simge formatlarını destekleme (`rel="mask-icon"` Safari için)  

Deney yapmaktan çekinmeyin, ve bir sorunla karşılaşırsanız aşağıya yorum bırakın. İyi kazımalar!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayalı olarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document to File in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}