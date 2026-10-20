---
category: general
date: 2026-07-27
description: Aspose.HTML (Python) içinde SaveOptions'ı büyük bir HTML sayfasını dönüştürmek
  ve kaynak yönetimini verimli bir şekilde uygulamak için nasıl kullanılır.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use SaveOptions
- convert large html page
- apply resource handling
- Aspose.HTML Python
- HTML resource handling
language: tr
lastmod: 2026-07-27
og_description: Aspose.HTML (Python) içinde SaveOptions kullanımını öğrenerek, büyük
  HTML sayfalarını temiz ve hızlı sonuçlar için kaynak yönetimi uygulayarak dönüştürebilirsiniz.
og_image_alt: Screenshot illustrating how to use SaveOptions in Aspose.HTML for Python
og_title: Aspose.HTML'de SaveOptions Nasıl Kullanılır – Python Rehberi
schemas:
- author: Aspose
  dateModified: '2026-07-27'
  description: How to use SaveOptions in Aspose.HTML (Python) to convert large HTML
    page and apply resource handling efficiently.
  headline: How to Use SaveOptions in Aspose.HTML (Python)
  type: TechArticle
- questions:
  - answer: Aspose.HTML follows redirects but won’t send credentials automatically.
      You can pre‑download those assets or use a custom `WebRequest` handler (beyond
      this guide’s scope).
    question: What if the page references resources over HTTPS that require authentication?
  - answer: Yes—set `resource_options.max_handling_depth = 0`. This skips external
      files but leaves any `<style>` blocks intact.
    question: Can I preserve inline CSS while stripping external files?
  - answer: After saving, you can run a secondary pass with Pillow to downscale images,
      or let Aspose.HTML’s built‑in image compression options handle it (use `save_options.image_quality`).
    question: What about very large images that still bloat the output?
  - answer: The limit is global across all resource types (images, scripts, styles).
      If you need granular control, you’d have to filter resources manually after
      loading the document.
    question: Is the depth limit applied per‑resource type?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- HTML processing
title: Aspose.HTML (Python) içinde SaveOptions Nasıl Kullanılır
url: /tr/python/general/how-to-use-saveoptions-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.HTML (Python) içinde SaveOptions Nasıl Kullanılır

Aspose.HTML for Python'da SaveOptions kullanımını büyük HTML dosyalarıyla çalışırken birçok geliştiricinin sorduğu bir konudur. Eğer **büyük HTML sayfasını dönüştürmek** ve **kaynak işleme uygulamasını** sıkı bir şekilde kontrol etmek istiyorsanız, doğru yerdesiniz.  

Bu öğreticide gerçek bir senaryoyu adım adım inceleyeceğiz: hantal bir HTML sayfasını alıp, iç içe geçmiş kaynakların ne kadar derine çekileceğini sınırlayacağız ve sonunda sonucu kristal netliğinde kontrol ederek kaydedeceğiz (veya dönüştüreceğiz). Belirsiz referanslar yok, sadece bugün projenize kopyalayıp yapıştırabileceğiniz tam, çalıştırılabilir bir örnek.

> **Pro ipucu:** Aspose.HTML’in `SaveOptions` yalnızca HTML’ye geri kaydetmek için değil, PDF, PNG veya hatta DOCX’e dönüştürmek için de çalışır. Aşağıda ele aldığımız aynı desen bu formatların tümüne uygulanabilir.

---

## Gereksinimler

- **Python 3.8+** (kod tip ipuçları kullanıyor ancak herhangi bir yeni sürümde çalışır)  
- **Aspose.HTML for Python via .NET** – `pip install aspose-html` komutuyla kurun  
- **large HTML file** dosyasını küçültmek veya dönüştürmek istiyorsanız (örnek `big_page.html` kullanır)  
- Çıktı dosyası için makul bir miktarda disk alanı  

Bu kadar—ekstra kütüphane yok, ağır yapı araçları yok.

---

## SaveOptions'ı Kaynak İşleme Seçenekleriyle Nasıl Kullanılır

Bu konuya dair asıl nokta burada. Bir `SaveOptions` örneği oluşturacağız, Aspose.HTML’e ne kadar derine kadar bağlı varlıkları takip etmesi gerektiğini söyleyen bir `ResourceHandlingOptions` nesnesi ekleyeceğiz ve ardından her şeyi belgenin `save` metoduna vereceğiz.

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Load the source HTML document
input_path = "YOUR_DIRECTORY/big_page.html"
doc = HTMLDocument(input_path)

# Define how deep nested resources should be processed (limit to 3 levels)
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # <-- controls depth of resource fetching

# Attach the resource handling configuration to the save options
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# Save the processed document (or convert to another format if desired)
output_path = "YOUR_DIRECTORY/big_page_processed.html"
doc.save(output_path, save_options)
```

**Neden bu çalışır:**  
- `HTMLDocument` orijinal dosyayı yükler, her `<img>`, `<link>`, `<script>` vb. öğeyi ayrıştırır.  
- `ResourceHandlingOptions.max_handling_depth` motoru, üç seviye iç içeleme sonrasında kaynakları takip etmeyi durdurur—başka sayfalar gömülü sayfalarda sonsuz döngüleri önlemek için mükemmeldir.  
- `SaveOptions` hem çıktı formatını (varsayılan olarak HTML) hem de kaynak işleme kurallarını taşıyan bir kaptır.  
- Son olarak, `doc.save` yeni dosyayı yazar ve az önce belirlediğimiz kuralları uygular.

Komutu çalıştırdığınızda `big_page_processed.html` adlı yeni bir dosya göreceksiniz. Tarayıcıda açın; üç seviyeye kadar derinlikteki tüm resimler, stiller ve betikler hâlâ mevcut, daha derin referanslar ise çıkarılmış olacak. Bu, sayfanın temel düzenini bozmadan dosya boyutunu büyük ölçüde azaltır—tam da **büyük HTML sayfasını** çevrim dışı kullanım veya e‑posta teslimi için **dönüştürmeniz** gerektiğinde ihtiyacınız olan şey.

---

## Büyük HTML Sayfasını Verimli Bir Şekilde Dönüştürün

Eğer amacınız *büyük HTML sayfasını* daha ince bir sürüme dönüştürmekse, yukarıdaki kod parçacığı zaten işin büyük kısmını halleder. Ancak çıktı formatını tamamen değiştirmek isteyebilirsiniz. Aspose.HTML bunu tek satırda yapmanızı sağlar:

```python
# Convert to PDF instead of HTML
pdf_save_options = SaveOptions()
pdf_save_options.resource_handling_options = resource_options
pdf_save_options.format = "PDF"   # specify desired format

doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_save_options)
```

Sadece `format` özelliğini `"PNG"`, `"JPEG"` veya `"DOCX"` ile değiştirin ve tam bir dönüşüm hattına sahip olursunuz. Aynı **kaynak işleme uygulaması** kuralları aynı kalır, böylece ortaya çıkan PDF orijinal sitedeki her harici CSS dosyasını gömmeyecek—sadece tanımladığınız üç seviyelik derinlikteki dosyalar eklenecek.

---

## İç İçe Kaynaklara Kaynak İşleme Uygulama

**kaynak işleme uygulamasını** etkili bir şekilde derinlemesine inceleyelim. HTML’nizin bir stil sayfası olduğunu ve bu stil sayfasının başka stil sayfaları içe aktardığını, her birinin de resimler çektiğini varsayalım. Derinlik sınırı olmadan Aspose.HTML zinciri sonsuza kadar takip edebilir, bellek ve CPU kullanımını şişirebilir.

```python
# Example: limit to 1 level for aggressive trimming
resource_options.max_handling_depth = 1
save_options.resource_handling_options = resource_options
doc.save("trimmed_page.html", save_options)
```

- **Depth 0** – Harici kaynaklar alınmaz; çıplak bir HTML iskeleti elde edersiniz.  
- **Depth 1** – Yalnızca birinci düzey kaynaklar (doğrudan `<img>` etiketleri, hemen ilgili CSS dosyaları) dahil edilir.  
- **Depth 2+** – Daha derin iç içeleme dikkate alınır, stillerin diğer stillere bağlı olduğu karmaşık siteler için faydalıdır.

**büyük HTML sayfasını** dönüştürme senaryonuza uygun derinliği seçin. E‑posta bültenleri için genellikle depth 1 yeterlidir. Yerel arşiv için, ana örnekteki gibi depth 3 güzel bir denge sağlar.

---

## Tam Çalışan Örnek – Baştan Sona

Aşağıda `process_html.py` adlı bir dosyaya koyabileceğiniz, bağımsız bir script bulunuyor. Hata yönetimi, günlük kaydı ve elde ettiğiniz boyut azaltımını ekrana yazdıran küçük bir yardımcı içerir.

```python
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

def process_html(
    src_path: str,
    dst_path: str,
    depth: int = 3,
    fmt: str = "HTML"
) -> None:
    """
    Loads an HTML file, applies resource handling, and saves it in the requested format.
    Returns nothing; prints size statistics for quick verification.
    """
    if not os.path.isfile(src_path):
        raise FileNotFoundError(f"Source file not found: {src_path}")

    # Load document
    doc = HTMLDocument(src_path)

    # Set up resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = depth

    # Configure save options (including format)
    save_opts = SaveOptions()
    save_opts.resource_handling_options = res_opts
    save_opts.format = fmt.upper()   # Aspose expects upper‑case format strings

    # Perform save / conversion
    doc.save(dst_path, save_opts)

    # Report size change
    original = os.path.getsize(src_path)
    final = os.path.getsize(dst_path)
    reduction = (original - final) / original * 100
    print(f"Saved {fmt.lower()} to '{dst_path}'. Size reduced by {reduction:.2f}%.")

# -------------------------------------------------------------------------
# Example usage
if __name__ == "__main__":
    input_file = "YOUR_DIRECTORY/big_page.html"
    output_file = "YOUR_DIRECTORY/big_page_processed.html"

    process_html(
        src_path=input_file,
        dst_path=output_file,
        depth=3,          # apply resource handling up to three levels
        fmt="HTML"       # change to "PDF" or "PNG" to convert format
    )
```

**Beklenen çıktı (konsol):**

```
Saved html to 'YOUR_DIRECTORY/big_page_processed.html'. Size reduced by 42.57%.
```

İşlenmiş dosyayı açın; hâlâ orijinale benzeyen daha ince bir sayfa göreceksiniz. `fmt` değerini `"PDF"` olarak değiştirirseniz, konsol bir PDF dosya boyutu raporlayacak ve dosyayı herhangi bir PDF görüntüleyicide açabileceksiniz.

---

## Sık Sorulan Sorular ve Kenar Durumları

- **Sayfa, kimlik doğrulama gerektiren HTTPS üzerinden kaynaklara referans veriyorsa ne olur?**  
  Aspose.HTML yönlendirmeleri takip eder ancak kimlik bilgilerini otomatik göndermez. Bu varlıkları önceden indirebilir veya özel bir `WebRequest` işleyicisi kullanabilirsiniz (bu kılavuzun kapsamı dışında).

- **Harici dosyaları kaldırırken satır içi CSS'i koruyabilir miyim?**  
  Evet—`resource_options.max_handling_depth = 0` ayarlayın. Bu, harici dosyaları atlar ancak `<style>` bloklarını olduğu gibi bırakır.

- **Çıktıyı şişiren çok büyük resimler ne olacak?**  
  Kaydetme işleminden sonra Pillow ile ikinci bir geçiş yaparak resimleri küçültebilir ya da Aspose.HTML’in yerleşik görüntü sıkıştırma seçeneklerini (ör. `save_options.image_quality`) kullanabilirsiniz.

- **Derinlik sınırı kaynak türüne göre uygulanıyor mu?**  
  Sınır, tüm kaynak türleri (görseller, betikler, stiller) arasında küreseldir. Daha ince kontrol gerekirse, belge yüklendikten sonra kaynakları manuel olarak filtrelemeniz gerekir.

---

## Sonuç

Artık Aspose.HTML'de **SaveOptions nasıl kullanılır** konusunda sağlam bir anlayışa sahipsiniz.

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [HTML'yi PDF'ye Dönüştürme Java – Aspose.HTML for Java Kullanarak](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [HTML'yi MHTML'ye Dönüştürme Aspose.HTML for Java ile](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [Aspose ile HTML'yi PNG'ye Render Etme – Adım Adım Kılavuz](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}