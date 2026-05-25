---
category: general
date: 2026-05-25
description: HTML'yi hızlıca PDF'ye dönüştürün ve Python kullanarak bir web sayfasını
  PDF olarak kaydederken derinliği nasıl sınırlayacağınızı öğrenin. Adım adım kod
  içerir.
draft: false
keywords:
- convert html to pdf
- save webpage as pdf
- download html as pdf
- how to limit depth
- set depth limit
language: tr
og_description: HTML'yi PDF'ye dönüştürün ve bir web sayfasını PDF olarak kaydederken
  derinlik sınırını nasıl ayarlayacağınızı öğrenin. Tam Python örneği ve en iyi uygulamalar.
og_title: HTML'yi PDF'ye Dönüştür – Derinlik Kontrolüyle Adım Adım
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Convert HTML to PDF quickly and learn how to limit depth when saving
    a webpage as PDF using Python. Includes step‑by‑step code.
  headline: Convert HTML to PDF – Complete Guide with Depth Limiting
  type: TechArticle
- description: Convert HTML to PDF quickly and learn how to limit depth when saving
    a webpage as PDF using Python. Includes step‑by‑step code.
  name: Convert HTML to PDF – Complete Guide with Depth Limiting
  steps:
  - name: '## Convert HTML to PDF with Depth Control'
    text: The core of the solution lives in four concise steps. Let’s break each one
      down, explain **why** it’s needed, and show the exact code you’ll paste into
      `convert_html_to_pdf.py`.
  - name: '## Save Webpage as PDF – Verifying the Result'
    text: After the script finishes, check `YOUR_DIRECTORY/output.pdf`. You should
      see the page rendered correctly, with images and styles that fell within the
      five‑level depth you set. If the PDF looks missing a stylesheet or an image,
      increase `max_handling_depth` by one and re‑run.
  - name: '### When to Adjust the Depth Limit'
    text: '| Situation | Recommended `max_handling_depth` | |-----------|-----------------------------------|
      | Simple blog post with a few images | 2–3 | | Complex web app with nested iframes
      | 6–8 | | Documentation site that uses CSS imports | 4–5 | | Unknown third‑party
      site | Start low (2) and increase gra'
  - name: '### Handling Authentication‑Protected Pages'
    text: 'If the target page requires a login, you’ll need to fetch the HTML yourself
      (using `requests` with a session) and feed the raw string to `HTMLDocument`:'
  - name: '### Setting a Custom Base URL'
    text: 'When you pass raw HTML, you may need to tell the converter where to resolve
      relative links:'
  - name: '### Common Pitfalls'
    text: '- **Forgot to attach `resource_options`** – the converter silently ignores
      your depth setting. - **Using an invalid output folder** – you’ll get a `PermissionError`.
      Make sure the directory exists and is writable. - **Mixing HTTP and HTTPS resources**
      – some converters block insecure content by defa'
  type: HowTo
tags:
- Python
- PDF conversion
- Web scraping
title: HTML'yi PDF'ye Dönüştür – Derinlik Sınırlamasıyla Tam Rehber
url: /tr/python/general/convert-html-to-pdf-complete-guide-with-depth-limiting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML'yi PDF'ye Dönüştür – Derinlik Sınırlamalı Tam Kılavuz

Hiç **HTML'yi PDF'ye dönüştürmek** istediğinizde, sonsuz bağlı kaynakların dosya boyutunuzu şişirmesinden endişe ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici, **web sayfasını PDF olarak kaydetmeye** çalıştığında, dış CSS, JavaScript ve hatta orada olmaması gereken resimlerle dolu devasa bir belgeyle karşılaşıyor.

Aslında şu: dönüşüm motorunun ne kadar derine gideceğini bir derinlik sınırı belirleyerek tam kontrol edebilirsiniz. Bu öğreticide, **HTML'yi PDF olarak indirmek** ve **derinliği sınırlamak** için temiz, çalıştırılabilir bir Python örneği üzerinden adım adım ilerleyeceğiz. Sonunda çalıştırmaya hazır bir betiğiniz olacak, derinliğin neden önemli olduğunu anlayacaksınız ve yaygın tuzaklardan kaçınmak için birkaç profesyonel ipucu öğreneceksiniz.

---

## Gereksinimler

Başlamadan önce şunların olduğundan emin olun:

| Önkoşul | Neden Önemli |
|--------------|----------------|
| Python 3.9 ve üzeri | Kullanacağımız dönüşüm kütüphanesi yalnızca yeni çalışma zamanlarını destekler. |
| `aspose-pdf` paketi (veya benzeri bir API) | `HTMLDocument`, `ResourceHandlingOptions`, `SaveOptions` ve `Converter` sınıflarını sağlar. |
| İnternet erişimi (kaynak sayfayı çekmek için) | Betik, URL'den canlı HTML'yi alır. |
| Çıktı klasörüne yazma izni | PDF, `YOUR_DIRECTORY` içine yazılacaktır. |

Kurulum tek bir satırdır:

```bash
pip install aspose-pdf
```

*(Farklı bir kütüphane tercih ederseniz, kavramlar aynı kalır – sadece sınıf adlarını değiştirin.)*

---

## Adım‑Adım Uygulama

### ## Derinlik Kontrolü ile HTML'yi PDF'ye Dönüştürme

Çözümün özü dört kısa adımda yer alır. Her birini inceleyelim, **neden** gerekli olduğunu açıklayalım ve `convert_html_to_pdf.py` dosyasına yapıştıracağınız tam kodu gösterelim.

#### 1️⃣ HTML Belgesini Yükle

İlk olarak, dönüştürmek istediğiniz sayfayı işaret eden bir `HTMLDocument` nesnesi oluştururuz. Bu, dönüştürücüye zaten işaretlenmiş bir tuval vermek gibidir.

```python
from aspose.pdf import HTMLDocument

# Step 1: Load the HTML document you want to convert
doc = HTMLDocument("https://example.com/very-large-page.html")
```

*Neden önemli*: Kaynak yüklenmezse, dönüştürücünün işleyebileceği bir şey olmaz. URL herhangi bir herkese açık sayfa olabilir ya da HTML'yi daha önce kaydettiyseniz yerel bir dosya yolu da olabilir.

#### 2️⃣ Derinlik Sınırını Tanımla

Derinlik, motorun kaç “seviye” bağlanmış kaynağı (CSS, resimler, iframe'ler vb.) takip edeceğini belirler. `max_handling_depth = 5` olarak ayarlamak, dönüştürücünün yalnızca beş adım derinliğe kadar linkleri izleyeceği ve ardından duracağı anlamına gelir. Bu, kontrolsüz indirmeleri önler.

```python
from aspose.pdf import ResourceHandlingOptions

# Step 2: Define how deep the engine should follow linked resources
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 5   # stop after 5 levels of links
```

*Neden önemli*: Büyük siteler genellikle kaynakları başka kaynaklar içinde (ör. bir CSS dosyasının başka bir CSS'i içe aktarması) iç içe yerleştirir. Sınır olmadan tüm interneti çekiyor olabilirsiniz.

#### 3️⃣ Seçenekleri Kaydetme Yapılandırmasına Ekle

`SaveOptions`, az önce oluşturduğumuz derinlik ayarları da dahil olmak üzere tüm dönüşüm tercihlerini paketler. Bu, dönüştürücüye PDF'nin tam olarak nasıl hazırlanacağını söyleyen bir tarif kartı gibidir.

```python
from aspose.pdf import SaveOptions

# Step 3: Attach the resource handling options to the save configuration
save_options = SaveOptions()
save_options.resource_handling_options = resource_options
```

*Neden önemli*: Bu adımı atlayınca, dönüştürücü varsayılan derinliğine (genellikle sınırsız) geri döner ve **derinliği nasıl sınırlayacağınız** amacını bozar.

#### 4️⃣ Dönüşümü Gerçekleştir

Son olarak, belgeyi, çıktı yolunu ve `save_options`'ı geçirerek `Converter.convert` çağrısını yaparız. Motor derinlik sınırına uyar ve temiz bir PDF yazar.

```python
from aspose.pdf import Converter

# Step 4: Convert the document to PDF while respecting the depth limit
Converter.convert(doc, "YOUR_DIRECTORY/output.pdf", save_options)
```

*Neden önemli*: Bu tek satır, HTML'i ayrıştırma, izin verilen kaynakları çekme ve her şeyi bir PDF dosyasına render etme işini üstlenir.

---

### ## Web Sayfasını PDF Olarak Kaydet – Sonucu Doğrulama

Betik tamamlandığında `YOUR_DIRECTORY/output.pdf` dosyasını kontrol edin. Sayfanın doğru şekilde render edildiğini, beş‑seviye derinliğe giren resim ve stillerin yer aldığını görmelisiniz. PDF bir stil sayfası ya da resim eksik gösteriyorsa, `max_handling_depth` değerini bir artırıp tekrar çalıştırın.

**Pro ipucu:** Katmanları gösterebilen bir görüntüleyicide (ör. Adobe Acrobat) PDF'yi açın; gizli öğelerin çıkarılıp çıkarılmadığını kontrol edin. Bu, derinliği aşırı indirmeye yol açmadan ince ayar yapmanıza yardımcı olur.

---

## İleri Konular & Kenar Durumları

### ### Derinlik Sınırını Ne Zaman Ayarlamalısınız

| Durum | Önerilen `max_handling_depth` |
|-----------|-----------------------------------|
| Birkaç resimli basit blog gönderisi | 2–3 |
| İç içe iframe'ler içeren karmaşık web uygulaması | 6–8 |
| CSS içe aktarmaları kullanan dokümantasyon sitesi | 4–5 |
| Bilinmeyen üçüncü‑taraf sitesi | Düşük başlayın (2) ve yavaş yavaş artırın |

Sınırı çok düşük ayarlamak kritik CSS'i kırpabilir ve PDF'niz sade görünebilir. Çok yüksek ayarlamak ise bant genişliği ve bellek israfına yol açar.

### ### Kimlik Doğrulama‑Gerektiren Sayfalar

Hedef sayfa bir oturum açma gerektiriyorsa, HTML'i kendiniz çekmeniz gerekir (`requests` ile bir oturum kullanarak) ve ham dizeyi `HTMLDocument`'e beslemelisiniz:

```python
import requests
from aspose.pdf import HTMLDocument

session = requests.Session()
session.post("https://example.com/login", data={"user":"me","pass":"secret"})
html = session.get("https://example.com/secure-page.html").text

doc = HTMLDocument(html)  # Pass raw HTML instead of a URL
```

Şimdi derinlik‑sınırı mantığı hâlâ geçerlidir; çünkü dönüştürücü, sağladığınız temel URL'ye göre göreli linkleri çözer.

### ### Özel Bir Temel URL Ayarlama

Ham HTML gönderdiğinizde, göreli linklerin nereden çözüleceğini dönüştürücüye bildirmeniz gerekebilir:

```python
doc.base_url = "https://example.com/"
```

Bu küçük satır, `/assets/style.css` gibi kaynaklar için derinlik sınırının doğru çalışmasını sağlar.

### ### Yaygın Tuzaklar

- **`resource_options` eklemeyi unutmak** – dönüştürücü derinlik ayarınızı sessizce görmezden gelir.
- **Geçersiz bir çıktı klasörü kullanmak** – `PermissionError` alırsınız. Klasörün var olduğundan ve yazılabilir olduğundan emin olun.
- **HTTP ve HTTPS kaynaklarını karıştırmak** – bazı dönüştürücüler varsayılan olarak güvensiz içeriği engeller; gerekirse karışık içerik işleme özelliğini etkinleştirin.

---

## Tam Çalışan Betik

Aşağıda, yukarıdaki tüm ipuçlarını içeren, kopyala‑yapıştır‑hazır tam betik yer alıyor. `convert_html_to_pdf.py` olarak kaydedin ve `python convert_html_to_pdf.py` ile çalıştırın.

```python
# convert_html_to_pdf.py
# Complete example: convert HTML to PDF while setting a depth limit

import os
from aspose.pdf import HTMLDocument, ResourceHandlingOptions, SaveOptions, Converter

# ----------------------------------------------------------------------
# Configuration section – adjust these values for your environment
# ----------------------------------------------------------------------
SOURCE_URL = "https://example.com/very-large-page.html"
OUTPUT_DIR = "YOUR_DIRECTORY"
OUTPUT_FILE = os.path.join(OUTPUT_DIR, "output.pdf")
MAX_DEPTH = 5                     # set depth limit (how to limit depth)

# Ensure the output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document
# ----------------------------------------------------------------------
doc = HTMLDocument(SOURCE_URL)

# ----------------------------------------------------------------------
# Step 2: Define depth handling options
# ----------------------------------------------------------------------
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = MAX_DEPTH  # set depth limit

# ----------------------------------------------------------------------
# Step 3: Attach options to save configuration
# ----------------------------------------------------------------------
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# ----------------------------------------------------------------------
# Step 4: Perform the conversion
# ----------------------------------------------------------------------
Converter.convert(doc, OUTPUT_FILE, save_options)

print(f"✅ Conversion complete! PDF saved to: {OUTPUT_FILE}")
```

**Beklenen çıktı** betiği çalıştırdığınızda:

```
✅ Conversion complete! PDF saved to: YOUR_DIRECTORY/output.pdf
```

Oluşturulan PDF'yi açın – beş‑seviye derinliğe giren tüm kaynaklarla birlikte web sayfasının render edildiğini görmelisiniz.

---

## Sonuç

**HTML'yi PDF'ye dönüştürürken** **derinlik sınırı** ayarlamanın tüm inceliklerini ele aldık. Kütüphaneyi kurmaktan `ResourceHandlingOptions` yapılandırmasına, kimlik doğrulama ve özel temel URL'lere kadar, bu öğretici size sağlam, üretim‑hazır bir temel sunuyor.

Unutmayın:

- `max_handling_depth` ile **derinliği nasıl sınırlayacağınızı** kontrol edin ve PDF'leri hafif tutun.
- Derinliği, kaynak sitenin karmaşıklığına göre ayarlayın.
- Çıktıyı test edin, ardından mükemmel dengeyi yakalayana kadar ince ayar yapın.

Bir sonraki meydan okumaya hazır mısınız? **Çok sayfalı bir makaleyi PDF olarak kaydetmeyi** deneyin, `set depth limit` değerleriyle oynayın veya `PdfPage` nesneleriyle başlık/altbilgi eklemeyi keşfedin. **HTML'yi PDF olarak indirme** otomasyonu geniş bir dünya ve artık bu dünyada gezinmek için doğru araçlara sahipsiniz.

Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın – yardımcı olmaktan mutluluk duyarım. Mutlu kodlamalar ve temiz PDF'lerin tadını çıkarın!

## İlgili Öğreticiler

- [Convert HTML to PDF with Aspose.HTML – Full Manipulation Guide](/html/english/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}