---
category: general
date: 2026-10-21
description: Python’da HTML’i nasıl ayrıştıracağınızı, bir HTML belgesini nasıl yükleyeceğinizi,
  CSS seçicilerini nasıl kullanacağınızı ve HTML’den hızlı bir şekilde bağlantıları
  nasıl çıkaracağınızı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- how to use selector
- extract hyperlinks from html
- load html document python
language: tr
lastmod: 2026-10-21
og_description: CSS seçicileri kullanarak Python’da HTML nasıl ayrıştırılır. Bir HTML
  belgesi yükleyin, bağlantıları seçin ve temiz kodla HTML’den hiperlinkleri çıkarın.
og_image_alt: Screenshot showing how to parse HTML in Python with CSS selectors
og_title: Python'da HTML nasıl ayrıştırılır – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to parse HTML in Python, load an HTML document, use CSS selectors,
    and extract hyperlinks from HTML quickly.
  headline: How to parse HTML in Python using CSS selectors
  type: TechArticle
tags:
- python
- html-parsing
- css-selectors
title: Python'da CSS seçicileri kullanarak HTML nasıl ayrıştırılır
url: /tr/python/general/how-to-parse-html-in-python-using-css-selectors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da CSS seçicileri kullanarak HTML nasıl ayrıştırılır

Eğer bir Python betiğinde **how to parse html** yapmanız gerekiyorsa, bu kılavuz tam olarak bunu gösterir. Bir HTML belgesini nasıl yükleyeceğinizi, öğeleri bulmak için seçici sözdizimini nasıl kullanacağınızı ve özel bir ayrıştırıcı yazmadan html'den hiperlinkleri nasıl çıkaracağınızı öğreneceksiniz.

HTML ayrıştırma, web kazıyıcıları, veri‑analiz boru hatları veya otomatik testler için yaygın bir görevdir. Bu öğreticinin sonunda, bir HTML belgesini yükleyen, bir CSS seçicisiyle tüm `<a>` etiketlerini seçen ve temiz bir URL listesi döndüren yeniden kullanılabilir bir fonksiyona sahip olacaksınız.

## İhtiyacınız olanlar

- Python 3.8+ (kod herhangi bir yeni sürümde çalışır)  
- **lxml** kütüphanesi (`pip install lxml`) – hızlı HTML ayrıştırma ve CSS seçici desteği sağlar  
- Analiz etmek istediğiniz bir HTML dosyası (ör. `sample.html`)  

Ek bir araç gerekmiyor; her şey standart kütüphane ve tek bir üçüncü‑taraf paketiyle çalışır.

## Adım 1: HTML nasıl ayrıştırılır – belgeyi yükleyin

Herhangi bir HTML iş akışının ilk adımı dosyayı belleğe okumaktır. **lxml.html** kullanmak, CSS seçicilerini destekleyen bir ağaç nesnesi sağlar.

```python
# step_1_load.py
from lxml import html

def load_html(path: str) -> html.HtmlElement:
    """
    Load an HTML document from the given file path.
    Returns an lxml HtmlElement that can be queried with CSS selectors.
    """
    with open(path, "r", encoding="utf-8") as f:
        content = f.read()
    # Parse the raw HTML string into a tree
    return html.fromstring(content)

# Example usage
doc = load_html("sample.html")
print("Document loaded – ready for selector queries.")
```

**Bu neden önemlidir:**  
`load_html` dosya‑okuma kalıbını soyutlar ve belgenin toleranslı bir HTML ayrıştırıcıyla işlenmesini garanti eder. Bu, hatalı işaretlemeler hakkında endişelenmeden **load html document python** yapmanın en güvenli yoludur.

## Adım 2: Seçiciyi nasıl kullanılır – tüm bağlantı öğelerini bulun

Belge yüklendikten sonra, her `<a>` etiketini bulmak için bir CSS seçicisi kullanabilirsiniz. `"a"` seçicisi tüm bağlantı öğelerini eşleştirir, ancak bunu (ör. `"a.external"` veya `"nav a"`) daha da daraltabilirsiniz.

```python
# step_2_selector.py
def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    """
    Return a list of <a> elements using a CSS selector.
    This demonstrates how to use selector syntax with lxml.
    """
    # The CSS selector "a" selects every anchor tag
    return doc.cssselect("a")

# Example usage
links = select_links(doc)
print(f"Found {len(links)} <a> elements.")
```

**Bu neden önemlidir:**  
**how to use selector** yaklaşımı, karmaşık sorguları tek, okunabilir bir dize içinde ifade etmenizi sağlar ve manuel ağaç dolaşımını önler. `lxml.cssselect` tarafından desteklenen herhangi bir CSS deseni için çalışır.

## Adım 3: HTML'den hiperlinkleri çıkarın ve işleyin

Artık bir `<a>` öğeleri listesine sahip olduğunuza göre, her birinden `href` özniteliğini alabilirsiniz. Aşağıdaki yardımcı fonksiyon ayrıca bir temel URL sağlarsanız göreli URL'leri normalleştirir.

```python
# step_3_extract.py
from urllib.parse import urljoin
from typing import Optional

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    """
    Return a list of href values from the given <a> elements.
    If base_url is supplied, relative URLs are resolved to absolute URLs.
    """
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            # Skip <a> tags without an href attribute
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

# Example usage
hyperlinks = extract_hyperlinks(links, base_url="https://example.com")
for url in hyperlinks:
    print(url)
```

**Beklenen çıktı** (`sample.html` üç bağlantı içeriyorsa):

```
https://example.com/page1.html
https://example.com/page2.html
https://external.org/resource
```

**Bu neden önemlidir:**  
`extract_hyperlinks`, **extract hyperlinks from html** işleminin çekirdeğidir. Eksik `href` özniteliklerini zarifçe ele alır, göreli bağlantıları çözer ve daha ileri işleme (ör. requests, pandas veya bir veritabanı) besleyebileceğiniz sade bir Python listesi döndürür.

## Tam uçtan‑uca örnek

Üç fonksiyonu bir araya getirmek, bir dosyayı yükleyen, tüm bağlantıları seçen ve her bir hiperlinki yazdıran tek bir betik sağlar.

```python
# parse_links.py
from lxml import html
from urllib.parse import urljoin
from typing import Optional

def load_html(path: str) -> html.HtmlElement:
    with open(path, "r", encoding="utf-8") as f:
        return html.fromstring(f.read())

def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    return doc.cssselect("a")

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

if __name__ == "__main__":
    # 1️⃣ Load the HTML document
    document = load_html("sample.html")
    # 2️⃣ Use selector to grab all <a> tags
    anchor_elements = select_links(document)
    # 3️⃣ Extract and print each hyperlink
    for url in extract_hyperlinks(anchor_elements, base_url="https://example.com"):
        print(url)
```

`python parse_links.py` komutunu çalıştırmak, her hiperlinki tam olarak çözülmüş şekilde konsola yazdırır. Bu betik **how to parse html**, **how to use selector** ve **extract hyperlinks from html** konularını tek, yeniden kullanılabilir bir akışta gösterir.

## Yaygın varyasyonlar ve kenar‑durum yönetimi

| Durum | Ne değiştirilmeli | Sebep |
|-----------|----------------|--------|
| **Yalnızca mutlak URL'ler gerekli** | `extract_hyperlinks` içinde `base_url` argümanını atlayın | Göreceli URL'leri dokunulmaz bırakır |
| **Bağlantı metnine de ihtiyacınız var** | `extract_hyperlinks`'ten bir tuple `(href, link.text_content())` döndürün | Hem URL'i hem de bağlantı metnini saklamanızı sağlar |
| **Büyük HTML dosyaları** | CSS seçici filtresiyle `lxml.etree.iterparse` kullanın | Akış sayesinde bellek kullanımını azaltır |
| **Farklı seçici** | `"a"` yerine `"nav a[href]"` veya `"div.content a.external"` kullanın | Bağlantıların bir alt kümesini hedefler, karmaşık sayfalarda **how to use selector** için faydalıdır |

**İpucu:** Ağ istekleri yapmadan önce çıkarılan URL'leri her zaman doğrulayın. Hızlı bir `urlparse` kontrolü, hatalı dizeleri filtreleyebilir ve kazıyıcınızı çöküşlerden korur.

## Sonuç

Artık Python'da **how to parse html**, **load html document python**, **how to use selector** ile öğeleri hedefleme ve **extract hyperlinks from html** işlemlerini verimli bir şekilde yapabiliyorsunuz. Yukarıdaki tam örnek, projenize kopyala‑yapıştır yapmaya hazırdır ve her fonksiyonu sayfalama, JavaScript‑oluşturulmuş içerik veya çok‑sayfalı tarama gibi daha gelişmiş kullanım senaryolarına uyarlayabilirsiniz.

İleride keşfedebileceğiniz adımlar:

- **requests‑html** veya **Playwright** kullanarak JavaScript yürütmesi gerektiren sayfaları çekmek.  
- Çıkarılan URL'leri daha sonraki analiz için bir CSV ya da SQLite veritabanında saklamak.  
- Ağ zaman aşımı ve HTTP durum kodları için hata yönetimi eklemek.

İyi ayrıştırmalar, ve farklı seçicilerle denemeler yaparak Python'da CSS‑tabanlı HTML sorgularının tam gücünü ortaya çıkarmaktan çekinmeyin!

## Bir Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım‑adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Python'da HTML kaynak yönetimini yapılandırma ve bir HTML belgesi yükleme](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)
- [Python'da HTML Ayrıştırma – Tam Kılavuz](/html/english/python/general/how-to-parse-html-in-python-complete-guide/)
- [Python'da HTML Yükleme – Adım Adım Kılavuz](/html/english/python/general/how-to-load-html-in-python-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}