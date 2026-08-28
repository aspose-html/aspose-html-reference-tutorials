---
category: general
date: 2026-07-05
description: Python kullanarak bağlantıları yeni sekmede aç – target blank eklemeyi,
  link hedefini değiştirmeyi, attribute contains seçicisini kullanmayı ve değiştirilmiş
  HTML'yi zahmetsizce kaydetmeyi öğrenin.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: tr
og_description: Bağlantıları yeni sekmede hızlıca açın. Bu öğreticide `target="_blank"`
  ekleme, bağlantı hedefini değiştirme ve Python ile değiştirilmiş HTML'yi kaydetme
  gösteriliyor.
og_title: Bağlantıları Yeni Sekmede Aç – Adım Adım HTML Güncelleme Rehberi
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: Bağlantıları Yeni Sekmede Aç – HTML Bağlantılarını Güncelleme Tam Kılavuzu
url: /tr/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bağlantıları Yeni Sekmede Aç – HTML Bağlantılarını Güncelleme Tam Kılavuzu

Statik bir HTML sayfasında **open links new tab** yapmanız gerektiğinde ama nereden başlayacağınızı bilemediğiniz oldu mu? Yalnız değilsiniz. Birçok geliştirici, eski siteleri temizlerken veya erişilebilirlik iyileştirmeleri eklerken bu soruna takılıyor. Bu öğreticide **adds target blank**, **changes link target** ve güvenli bir şekilde **saves modified html** yapan pratik bir çözümü birkaç satır Python ile göstereceğiz.

Ayrıca **attribute contains selector** kullanımını da ele alacağız, böylece yalnızca gerçekten ilgilendiğiniz bağlantılara dokunursunuz (örneğin, *example.com* adresine yönelen tüm linkler). Sonunda, büyük ya da küçük fark etmeksizin herhangi bir projeye ekleyebileceğiniz yeniden kullanılabilir bir betiğiniz olacak.

## Öğrenecekleriniz

- HTML dosyasını manipüle edilebilir bir belge nesnesine yükleyin.  
- `href` özniteliği belirli bir alt dize içeren `<a>` öğelerini seçin.  
- **Add target blank** ve güvenliği artırmak için `rel="noopener"` özniteliğini ayarlayın.  
- **Save modified html**'i biçimlendirmeyi kaybetmeden diske kaydedin.  

Standart kütüphane ve **beautifulsoup4** (çok hafif bir kurulum) dışındaki harici bağımlılık yok. Farklı bir ayrıştırıcı kullanıyorsanız, kavramlar doğrudan uygulanabilir.

---

## Önkoşullar

- Makinenizde Python 3.8+ yüklü.  
- HTML ve Python hakkında temel bilgi.  
- `beautifulsoup4` paketi (`pip install beautifulsoup4`).  

Hepsi bu—ağır çerçevelere gerek yok.

---

## Adım 1: HTML Belgesini Yükleyin

İlk olarak, kaynak dosyayı okumamız ve BeautifulSoup'a vermemiz gerekiyor. Bunu, yeni öznitelikler çizebileceğiniz boş bir tuval açmak gibi düşünün.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Why this matters:** `Path` kullanmak kodu OS‑bağımsız tutar ve `html.parser` yerleşik olduğundan basit görevler için ekstra ayrıştırıcıya ihtiyaç duymazsınız.

---

## Adım 2: Doğru Bağlantıları Bulmak İçin Attribute Contains Selector Kullanımı

Yalnızca *example.com* adresine yönelen bağlantılara dokunmak istiyoruz. CSS seçicisi `a[href*='example.com']` tam olarak bunu yapar—`*=` “içerir” anlamına gelir. BeautifulSoup’un `select` metodu bu sözdizimini anlar.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Pro tip:** Büyük/küçük harfe duyarsız bir eşleşme gerekiyorsa, `if 'example.com' in a.get('href', '').lower()` kontrol eden küçük bir döngüye geçin.

Şimdi `anchor_elements` ilgilendiğimiz her linki tutuyor ve bir sonraki dönüşüm için hazır.

---

## Adım 3: Bağlantı Hedefini Değiştir – Add Target Blank ve Bağlantıyı Güvenceye Al

Bir linki yeni sekmede açmak sadece `target="_blank"` ayarlamak kadar basittir. Ancak modern tarayıcılar, yeni açılan sayfanın `window.opener` üzerinden orijinal pencereye erişimini önlemek için `rel="noopener"` (veya `noreferrer`) eklenmesini de önerir. Bu küçük güvenlik ayarı phishing saldırılarını önleyebilir.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Why we use direct dictionary assignment:** Öznitelik yoksa otomatik olarak oluşturur, varsa üzerine yazar—**change link target** işlemi için mükemmeldir.

---

## Adım 4: Değiştirilmiş HTML'i Diske Kaydedin

Son adım, güncellenmiş işaretlemeyi yeni bir dosyaya yazmaktır. Orijinali dokunulmamış bırakmak, bir şeyler ters giderse geri dönmenizi sağlar.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **What `prettify()` does:** HTML'i güzel girintilerle biçimlendirir, kaydedilen dosyanın daha okunabilir ve daha sonra fark edilmesini (diff) kolaylaştırır. Orijinal boşlukları tercih ediyorsanız, `prettify()` yerine `str(soup)` kullanın.

---

## Tam Script – Tek‑Tık Çözüm

Aşağıda, çalıştırmaya hazır tam script yer alıyor. `update_links.py` olarak kaydedin ve terminalinizden `python update_links.py` komutunu çalıştırın.

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### Beklenen Sonuç

Diyelim ki `links.html` başlangıçta şöyleydi:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Script'i çalıştırdıktan sonra `links-updated.html` şöyle görünecek:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Yalnızca *example.com* adresine giden link, **add target blank** özniteliklerini aldı; bu da **attribute contains selector**'ün tam olarak istediğimiz gibi çalıştığını gösteriyor.

---

## Yaygın Sorular & Kenar Durumları

### Bir bağlantının zaten bir `rel` özniteliği varsa ne olur?

Döngümüz `"noopener"` ile üzerine yazar. Mevcut değerleri (ör. `"nofollow"`) korumanız gerekiyorsa, şu şekilde birleştirin:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### Birden fazla alan adı nasıl ele alınır?

Sadece seçici listesini genişletin:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### `prettify()` orijinal HTML yapısını değiştirir mi?

Yeniden girintiler ekler ancak etiket sırasını veya öznitelik değerlerini değiştirmez. Tam orijinal boşlukları tutmanız gerekiyorsa, daha önce belirtildiği gibi `prettify()` yerine `str(soup)` kullanın.

---

## Üretim‑Hazır Scriptler İçin Pro İpuçları

- **Backup before overwriting:** Orijinal dosyayı güvenli tutmak için bir kopya adımı (`shutil.copy`) ekleyin.  
- **Logging instead of print:** Ölçeklenebilir projeler için `logging` modülünü kullanın.  
- **Batch processing:** Tek bir çalıştırmada birden fazla dosyayı güncellemek için `Path.rglob("*.html")` ile bir dizini döngüye alın.  

Bu ince ayarlar, basit bir **open links new tab** betiğini herhangi bir web‑bakım akışı için sağlam bir yardımcı programa dönüştürür.

---

## Sonuç

Artık herhangi bir statik HTML koleksiyonunda **open links new tab** yapabilen sağlam, yeniden kullanılabilir bir yönteme sahipsiniz. **Attribute contains selector**'ü kullanarak **change link target**'ı tam istediğiniz yerde uygulayabilir, **add target blank** ekleyebilir ve **save modified html**'i biçimlendirmeyi kaybetmeden kaydedebilirsiniz.  

Bir test sayfasında deneyin, ardından tüm sitenize ölçeklendirin. PDF'ler, diğer alan adları vb. için seçiciyi ayarlamanız mı gerekiyor? CSS dizesini sadece değiştirin—diğer her şey aynı kalır.

Herhangi bir tuhaflıkla karşılaşırsanız yorum bırakmaktan çekinmeyin ya da betiği kendi projelerinizde nasıl genişlettiğinizi paylaşın. İyi kodlamalar, ve tüm bağlayıcılarınız tam istediğiniz yerde açılsın!

## Sonra Ne Öğrenmelisin?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}