---
category: general
date: 2026-05-28
description: Python’da HTML’i hızlıca nasıl ayrıştırılır—HTML dosyasını yükle, CSS
  seçicisini kullan ve bir XPath contains örneğiyle href özniteliklerini çıkar.
draft: false
keywords:
- how to parse html
- get href attribute
- load html file
- use css selector
- xpath contains example
language: tr
og_description: 'Python''da HTML nasıl ayrıştırılır: bir HTML dosyasını nasıl yükleyeceğinizi
  öğrenin, CSS seçicilerini kullanın ve XPath contains örneğiyle href özniteliklerini
  alın.'
og_title: Python'da HTML Nasıl Ayrıştırılır – Adım Adım
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  headline: How to Parse HTML in Python – Complete Guide
  type: TechArticle
- description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  name: How to Parse HTML in Python – Complete Guide
  steps:
  - name: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
    text: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
  - name: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
    text: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
  - name: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
    text: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
  - name: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
    text: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
  type: HowTo
tags:
- html parsing
- python
- web scraping
title: Python'da HTML Nasıl Ayrıştırılır – Tam Kılavuz
url: /tr/python/general/how-to-parse-html-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da HTML Nasıl Ayrıştırılır – Tam Kılavuz

Hiç **HTML nasıl ayrıştırılır** diye bir Python betiğinde ağır bir tarayıcı kullanmadan merak ettiniz mi? Yalnız değilsiniz. Çoğumuz sadece **HTML dosyasını yüklemek**, birkaç başlık kazımak ve belki bir iki indirme bağlantısı çekmek istiyoruz. Bu öğreticide tam olarak bunu göstereceğim—küçük bir kütüphane, bir CSS seçici ve bir XPath contains örneği kullanarak **href özniteliğini almak**.

Yerel bir HTML belgesini okumaktan, ilgilendiğiniz verileri yazdırmaya kadar tüm süreci adım adım göstereceğiz. Gereksiz ayrıntı yok, sadece bugün kendi projenize ekleyebileceğiniz pratik, çalıştırılabilir bir örnek.

## Öğrenecekleriniz

- Hafif bir ayrıştırıcıyla **HTML dosyasını yüklemeyi** nasıl yapacağınızı.
- Makale başlıkları gibi öğeleri çekmek için **CSS seçicisi** sözdizimini nasıl **kullanacağınızı**.
- Bağlantıları filtreleyen bir **XPath contains örneği** nasıl oluşturacağınızı.
- Eşleşen düğümlerdeki **href özniteliği** değerlerini güvenli bir şekilde **almayı**.
- Bozuk işaretlemeyi ele alma ve betiği genişletme ipuçları.

Sadece Python 3.8+ ve `lxml` ile `cssselect` paketlerine ihtiyacınız var—her ikisi de tek bir `pip` komutuyla kurulabilir.

---

## Adım 1: HTML Dosyasını Yükleyin

Her şeyden önce, HTML içeriğini belleğe almanız gerekir. `lxml.html` modülü kullanışlı bir `fromstring` yardımcı işlevi sağlar, ancak diskte bir dosyanız olduğunda `parse` işlevi daha da temizdir.

```python
# Step 1: Load the HTML file
from lxml import html

# Replace the path with the location of your HTML document
html_path = "YOUR_DIRECTORY/news.html"
doc = html.parse(html_path)

# The root element gives us access to CSS and XPath methods
root = doc.getroot()
```

> **Neden önemli:** Dosyayı bir kez yüklemek bellek kullanımını düşük tutar ve hem CSS seçicilerini hem de XPath sorgularını destekleyen tek bir `root` nesnesi sağlar. Dosya eksik ya da okunamazsa, `html.parse` net bir `OSError` yükseltecek, bunu daha sonra yakalayabilirsiniz.

### Pro ipucu
Bir dosya yerine bir dizeyle çalışıyorsanız, `html.parse` yerine `html.fromstring(your_html_string)` kullanın.

---

## Adım 2: Başlıkları Almak İçin CSS Seçicisini Kullanma

CSS seçicileri özlüdür ve stil sayfası yazmış herkes için tanıdıktır. `<article>` içinde bulunan her `<h2>` öğesini alalım—haber başlıkları için mükemmel.

```python
# Step 2: Find all article headlines using a CSS selector
headline_nodes = root.cssselect("article h2")

# Print each headline's text content
for node in headline_nodes:
    print(node.text_content().strip())
```

**Beklenen çıktı** (örnek HTML iki makale içeriyorsa):

```
Breaking News: Python Takes Over the World
Local Developer Solves HTML Parsing Puzzle
```

> **Neden CSS?** Okunabilir, hızlıdır ve `lxml` ile kutudan çıkar çıkmaz çalışır. `cssselect` yöntemi seçiciyi gizli bir şekilde bir XPath ifadesine dönüştürür, böylece her iki dünyanın da en iyisini elde edersiniz.

---

## Adım 3: XPath Contains Örneği – “download” Bağlantılarını Bulma

Bazen CSS'in sunduğundan daha ince bir kontrol gerekir. XPath'in `contains()` işlevi, bir öznitelik içinde bir alt dize eşleştirmek istediğinizde, örneğin bir indirmeye işaret eden tüm bağlantılar gibi, parlıyor.

```python
# Step 3: Find all links that contain the word "download" using XPath
download_link_nodes = root.xpath("//a[contains(@href, 'download')]")

# Extract and print the href attribute from each matching node
for node in download_link_nodes:
    href = node.get("href")
    print(href)
```

**Örnek çıktı**:

```
/files/report_download.pdf
https://example.com/downloads/setup.exe
```

> **Neden XPath contains?** Ek Python döngüleri olmadan doğrudan öznitelik değerlerine göre filtreleme yapmanızı sağlar. Bu, öğreticilerde sıkça gördüğünüz klasik **xpath contains örneği**; ancak burada gerçek dünya kullanım senaryosu ile eşleştirilmiştir.

---

## Adım 4: Hepsini Yeniden Kullanılabilir Bir Fonksiyona Sarmak

Yolları ve çıktıları sabit kodlamak hızlı bir test için uygundur, ancak üretim kodu fonksiyonları tercih eder. Aşağıda hem başlıkları hem de indirme bağlantılarını döndüren kompakt bir yardımcı fonksiyon var.

```python
def parse_news_html(file_path):
    """
    Parse a news HTML file and return headlines plus download URLs.

    Parameters
    ----------
    file_path : str
        Path to the local HTML document.

    Returns
    -------
    dict
        {
            "headlines": list of strings,
            "download_links": list of href strings
        }
    """
    doc = html.parse(file_path)
    root = doc.getroot()

    # Headlines via CSS selector
    headlines = [
        node.text_content().strip()
        for node in root.cssselect("article h2")
    ]

    # Download links via XPath contains
    download_links = [
        node.get("href")
        for node in root.xpath("//a[contains(@href, 'download')]")
    ]

    return {"headlines": headlines, "download_links": download_links}
```

Artık fonksiyonu çağırabilir ve sonuçları güzel bir şekilde yazdırabilirsiniz:

```python
if __name__ == "__main__":
    results = parse_news_html("YOUR_DIRECTORY/news.html")
    print("Headlines:")
    for h in results["headlines"]:
        print(f"- {h}")

    print("\nDownload Links:")
    for link in results["download_links"]:
        print(f"- {link}")
```

Betik çalıştırıldığında öncekiyle aynı çıktı elde edilir, ancak şimdi yeniden kullanım için düzenli bir şekilde paketlenmiştir.

---

## Adım 5: Kenar Durumlarını ve Yaygın Tuzakları Ele Alma

1. **Eksik `href` özniteliği** – XPath, `href` bulunmasa bile `<a>` düğümünü döndürür. `None` durumuna karşı önlem alın:

   ```python
   href = node.get("href")
   if href:
       download_links.append(href)
   ```

2. **Göreceli vs. mutlak URL'ler** – Bağlantılarınız göreceli ise, temel URL'ye göre çözümlemek isteyebilirsiniz:

   ```python
   from urllib.parse import urljoin
   base_url = "https://example.com"
   absolute = urljoin(base_url, href)
   ```

3. **Bozuk HTML** – `lxml` hoşgörülüdür, ancak aşırı bozuk işaretleme `html.parse`'in `XMLSyntaxError` yükseltmesine neden olabilir. Parse çağrısını bir `try/except` bloğuna sararak hatayı kaydedin ve sorunlu dosyaları atlayın.

4. **Büyük dosyalarla performans** – Çok megabaytlık sayfalar için, tüm DOM'u belleğe yüklemek yerine `iterparse` ile akış olarak işlemeyi düşünün.

---

## Görsel Genel Bakış (isteğe bağlı)

![HTML nasıl ayrıştırılır akış diyagramı, dosya yükleme → CSS seçici → XPath contains → href özniteliğini alma](how-to-parse-html-flow.png "HTML nasıl ayrıştırılır akış diyagramı")

*Alt metin, SEO'yu karşılamak için birincil anahtar kelimeyi içerir.*

---

## Sonuç

Python’da **HTML nasıl ayrıştırılır** konusunu baştan sona ele aldık: bir HTML dosyasını yüklemek, makale başlıklarını çekmek için bir CSS seçicisi kullanmak, indirme bağlantılarını bulmak için bir XPath contains örneği oluşturmak ve sonunda **href özniteliğini** güvenli bir şekilde almak. Yeniden kullanılabilir `parse_news_html` fonksiyonu, herhangi bir kazıma görevine uyarlayabileceğiniz temiz, sürdürülebilir bir yaklaşımı gösterir.

Bir sonraki zorluğa hazır mısınız? Betiği şu şekilde genişletmeyi deneyin:

- `//table//tr` XPath sorgularıyla tabloları ayrıştırın.
- Başka bir **xpath contains örneği** kullanarak görüntü `src` özniteliklerini çıkarın.
- Canlı web sayfaları için `aiohttp` ile eşzamansız çekmeye geçin.

Keyifli ayrıştırmalar, ve unutmayın—bu temelleri öğrendikten sonra HTML kazıma geri kalan kısmı çocuk oyuncağı olur. Herhangi bir sorunla karşılaşırsanız, aşağıya bir yorum bırakın—birlikte sorun giderelim!

## İlgili Öğreticiler

- [Aspose.HTML for Java’da Dosyadan HTML Belgelerini Yükleme](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Aspose.HTML for Java’da HTML Belge Ağacını Düzenleme](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Aspose.HTML for Java’da HTML Belgelerine CSS – Satır İçi CSS Ekleme](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}