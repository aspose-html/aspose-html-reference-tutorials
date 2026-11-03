---
category: general
date: 2026-07-31
description: SVG belgesi oluşturmayı, bir daire eklemeyi ve SVG dosyasını hızlıca
  kaydetmeyi öğrenin. Grafiği birkaç satır Python kodu ile SVG olarak dışa aktarın.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: tr
lastmod: 2026-07-31
og_description: SVG belgesi oluşturun, bir daire ekleyin ve birkaç saniye içinde SVG
  dosyasını kaydedin. Bu kılavuz, grafiği SVG olarak dışa aktarmayı net, çalıştırılabilir
  kodla gösterir.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: SVG Belgesi Oluştur – Bir Daire Ekle ve SVG Olarak Kaydet
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: SVG Belgesi Oluştur – Bir Daire Ekleyin ve SVG Olarak Kaydedin
url: /tr/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SVG Belgesi Oluştur – Bir Daire Ekleyin ve SVG Olarak Kaydedin

Koddan **create SVG document** oluşturmanız gerektiğinde ama nereden başlayacağınızı bilemediğiniz oldu mu? Yalnız değilsiniz; birçok geliştirici vektör grafikleriyle ilk kez uğraştıklarında bu engelle karşılaşıyor. Bu öğreticide, **add circle to SVG** nasıl yapılır, ardından **save SVG file** nasıl yapılır gösteren küçük, bağımsız bir örnek üzerinden ilerleyeceğiz, böylece **export graphic as SVG**'yi webde veya tasarım araçlarında kullanabilirsiniz.

İşleri hafif tutacağız: sadece birkaç satır Python, popüler bir SVG yardımcı kütüphanesi ve biraz açıklama. Sonunda klasörünüzde hazır bir `circle.svg` dosyanız olacak ve her adımın neden önemli olduğunu anlayacaksınız—belirsiz “see docs” kısayolları yok.

## İhtiyacınız Olanlar

- Python 3.8+ (herhangi bir yeni sürüm çalışır)
- `svgwrite` paketi – `pip install svgwrite` ile kurun
- Bir metin editörü veya IDE (VS Code, PyCharm veya hatta Notepad iş görür)
- Dosyanın kaydedileceği dizine yazma izni

Hepsi bu. Ağır bağımlılıklar yok, harici hizmetler yok.

## Adım 1: SVG Belgesini Kurun

SVG belgesi oluşturmak, `svgwrite`'den bir `Drawing` nesnesi örneklemek kadar basittir. Bu nesneyi, her şeklin yaşadığı boş bir tuval olarak düşünün.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Bu neden önemli:** `Drawing` sınıfı XML tekrarlamasını sizin için halleder—ad alanları, başlıklar ve kök `<svg>` öğesi. Başlangıçta bir dosya adı belirterek dosyanın nereye kaydedileceğini zaten biliyoruz, bu da sonraki **save svg file** adımını basitleştirir.

### Pro ipucu
Bir döngüde birçok dosya oluşturmayı planlıyorsanız, her `Drawing`'e benzersiz bir ad verin veya `io.BytesIO` kullanarak her şeyi bellekte tutun, yazmaya hazır olana kadar.

## Adım 2: SVG'ye Bir Daire Ekleyin

Belge artık mevcut, şimdi **add circle to SVG** yapalım. `add()` yöntemi herhangi bir şekil nesnesini kabul eder; bir `Circle`, merkezde basit bir kırmızı nokta için mükemmeldir.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Neden `center` ve `radius` değişkenlerini kullanıyoruz:** Sayıları doğrudan kodlamak, kodun okunmasını ve bakımını zorlaştırır. Değerlere isim vererek amacı netleştiririz—bu daire, 200 × 200 tuvalin tam ortasında durur ve fark edilebilir kadar büyüktür.

### Kenar durumu – Şeffaf arka plan
Şeffaf bir arka plan (SVG'nin varsayılanı) gerekiyorsa, kök üzerinde `fill` ayarlamayı atlayabilirsiniz. Beyaz bir arka plan için şu kodu ekleyin:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

Bu kodu daireyi eklemeden önce yerleştirin, böylece dikdörtgen altta kalır.

## Adım 3: SVG Dosyasını Kaydedin

Şekil yerleştirildiğinde, son adım **save SVG file** işlemidir. `save()` yöntemi XML'i diske yazar ve `Drawing`'e zaten bir dosya adı verdiğimiz için tek bir çağrı işi halleder.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **Arka planda ne olur?** `svgwrite` öğe ağacını bir dizeye serileştirir, XML deklarasyonunu ekler ve UTF‑8 kodlamasıyla yazar. Hedef dizin yoksa, Python bir `FileNotFoundError` hatası verir; yolun geçerli olduğundan emin olun veya `os.makedirs()` ile oluşturun.

### Bonus: Grafiği programlı olarak SVG olarak dışa aktar
SVG içeriğine bir dize olarak ihtiyacınız varsa—örneğin bir HTML e-postasına gömmek için—`save()` yerine `dwg.tostring()` çağırabilirsiniz:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Tam Çalışan Örnek

Hepsini bir araya getirerek, işte tam, çalıştırmaya hazır bir betik:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Beklenen çıktı:** Betiği çalıştırdıktan sonra aynı klasörde bir `circle.svg` dosyası göreceksiniz. Bir tarayıcıda veya herhangi bir vektör editöründe açtığınızda beyaz bir kare üzerinde ortalanmış kırmızı bir daire görürsünüz—tam da programladığımız gibi.

## Yaygın Sorular & Tuzaklar

- **Farklı bir şekil istesem ne olur?** `dwg.circle` yerine `dwg.rect`, `dwg.ellipse` veya hatta özel bir `<path>` dizesi kullanın. API, şekiller arasında tutarlıdır.
- **SVG'yi doğrudan HTML içinde gömebilir miyim?** Kesinlikle. Az önce oluşturduğunuz dosya `<img src="circle.svg" alt="Red circle">` ile referans verilebilir veya `<svg>` etiketleriyle satır içi kullanılabilir.
- **Neden ham XML yazmıyoruz?** Yazabilirsiniz, ancak `svgwrite` gibi kütüphaneler ad alanı inceliklerini halleder ve kodu çok daha sürdürülebilir kılar—özellikle degrade veya animasyon eklemeye başladığınızda.

## Sonuç

Artık sadece birkaç Python satırıyla **create SVG document**, **add circle to SVG** ve **save SVG file** nasıl yapılacağını biliyorsunuz, böylece **export graphic as SVG** yapabilirsiniz. Bu desen ölçeklenebilir: daireyi herhangi bir vektör şekliyle değiştirin, veri üzerinden döngü kurarak grafikler oluşturun veya bir tasarım sistemi için varlıkları toplu işleyin.

Sonraki adımlar? Metin etiketleri eklemeyi, degrade ile denemeler yapmayı veya tek bir betikte tüm bir simge galerisi üretmeyi deneyin. Daha gelişmiş özellikler merak ediyorsanız, `svgwrite` belgelerinde gruplar (`<g>`), dönüşümler ve animasyon desteği konularına göz atın.

Kodlamaktan keyif alın ve vektörleriniz her zaman net kalsın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.HTML for Java'da SVG Belgesini Kaydet](/html/english/java/saving-html-documents/save-svg-document/)
- [Aspose.HTML for Java'da SVG Belgeleri Oluştur ve Yönet](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Aspose.HTML for Java ile SVG'yi Görsele Dönüştür](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}