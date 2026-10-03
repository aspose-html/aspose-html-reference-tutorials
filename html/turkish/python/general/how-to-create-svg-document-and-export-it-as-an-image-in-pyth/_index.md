---
category: general
date: 2026-10-02
description: Python'da SVG belgesi oluşturmayı, SVG'yi dosyaya kaydetmeyi ve kısa,
  eksiksiz bir betikle SVG görüntüsünü dışa aktarmayı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: tr
lastmod: 2026-10-02
og_description: Python'da SVG belgesi oluşturun ve bu pratik öğreticiyle SVG görüntüsünü
  dışa aktarın. Komut dosyasını izleyin, SVG'yi dosyaya kaydedin ve vektör grafiğini
  anında yeniden kullanın.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: Python'da SVG belgesi oluşturma – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: Python'da SVG belgesi oluşturma ve görüntü olarak dışa aktarma
url: /tr/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da SVG belgesi oluşturma ve görüntü olarak dışa aktarma

Programlı olarak **SVG belgesi oluşturmanız** gerekiyorsa, bu öğretici Python ile bunu tam olarak nasıl yapacağınızı gösterir. Basit bir daire oluşturan, SVG'yi dosyaya kaydeden ve istediğiniz yere yerleştirebileceğiniz dışa aktarılabilir bir SVG görüntüsü üreten tam bir betik göreceksiniz.

Koddan ölçeklenebilir vektör grafikleri üretmek, bir GUI editöründe şekil çizmeye harcanan manuel çabayı ortadan kaldırır. Bu rehberin sonunda SVG oluşturmayı veri görselleştirme boru hatlarına, otomatik rapor oluşturuculara veya keskin, çözünürlük‑bağımsız grafikler gerektiren herhangi bir projeye entegre edebilirsiniz.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

- Python 3.8 veya daha yeni bir sürüm
- `svgwrite` kütüphanesi (`pip install svgwrite` ile kurulur)
- SVG'nin kaydedileceği dizine yazma izni

Bu gereksinimler örneği hafif tutar ve çoğu ortamla uyumludur.

## Adım 1: SVG kütüphanesini kurun ve içe aktarın

İlk adım, SVG oluşturma için kullanışlı bir API sağlayan üçüncü‑taraf kütüphaneyi eklemektir.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite`, bir SVG dosyasının XML yapısını soyutlayarak ham işaretlemeden ziyade geometriye odaklanmanızı sağlar.

## Adım 2: Bir SVG belge nesnesi oluşturun

Şimdi `svgwrite.Drawing` örneği oluşturarak **SVG belgesi oluşturabilirsiniz**. Bu nesne kök `<svg>` öğesini temsil eder ve sonraki tüm şekilleri içinde tutar.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

`size` argümanı oluşturulan piksel boyutlarını tanımlarken, `viewBox` daha sonra tanımlayacağınız geometriyle eşleşen bir koordinat sistemi kurar.

## Adım 3: Bir daire öğesi ekleyin

Bir daire, merkez koordinatları (`cx`, `cy`) ve yarıçapı (`r`) ile tanımlanır. Bu öznitelikleri eklemek için `circle` yardımcı metodunu kullanın.

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Daire, 100 × 100 tuvalin ortasında yer alır ve her iki tarafta 10 piksel boşluk bırakır. `fill` ve `stroke` değerlerini tasarım dilinize göre ayarlayın.

## Adım 4: SVG'yi dosyaya kaydedin

Grafik bir araya geldiğinde, `save` yöntemiyle **SVG'yi dosyaya kaydedebilirsiniz**. Bu, tarayıcıların ve vektör editörlerinin anlayabileceği iyi biçimlendirilmiş XML yazar.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

`circle.svg` dosyası artık geçerli çalışma dizininde bulunur. Bir web tarayıcısında, Inkscape'de veya SVG formatını destekleyen herhangi bir araçta açabilirsiniz.

## Adım 5: Dışa aktarılan SVG görüntüsünü doğrulayın

Kaydedilen dosyayı bir tarayıcıda açarak çıktıyı kontrol edin. Belirttiğiniz renklerle ortalanmış bir daire görmelisiniz. Ham XML şu şekildedir:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

SVG vektör tabanlı olduğundan, kalite kaybı olmadan ölçeklendirebilirsiniz; bu da duyarlı web tasarımları veya yüksek çözünürlüklü baskılar için idealdir.

## Pro ipucu: SVG'yi PNG veya JPEG olarak dışa aktarın

Raster bir sürüme ihtiyacınız varsa, **CairoSVG** gibi bir dönüşüm aracıyla SVG dosyasını birleştirin:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Bu adım, **SVG görüntüsünü** bir bitmap formatına dışa aktarmayı gösterir; alt sistemler doğrudan SVG render edemediğinde kullanışlıdır.

## Yaygın varyasyonlar ve kenar durumları

| Varyasyon | Nasıl ele alınır |
|-----------|-------------------|
| Birden fazla şekil | Her yeni öğe (rect, line, path) için `dwg.add()` çağırın. |
| Dinamik boyutlar | `Drawing` oluşturulmadan önce `size` ve `viewBox` değerlerini veriden hesaplayın. |
| Metin etiketleri | `dwg.text("Label", insert=("10", "20"))` kullanın ve `font_size` ile `fill` ile stil verin. |
| Belgeyi yeniden kullanma | `Drawing` nesnesini bellekte tutun ve gerektiğinde `save()` çağırarak güncellenmiş dosya oluşturun. |
| Büyük dosyalar | Bellek dalgalanmalarını önlemek için çıktıyı `dwg.tostring()` ile akışa alın ve manuel olarak bir dosya nesnesine yazın. |

Bu senaryoları ele almak, **SVG oluşturma** betiğinizin basit ikonlardan karmaşık diyagramlara kadar ölçeklenmesini sağlar.

## Tam betik özeti

Aşağıda, tüm adımları ve isteğe bağlı dönüşümü içeren çalıştırılabilir tam örnek yer alıyor:

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Bu betiği çalıştırdığınızda `circle.svg` ve `cairosvg` kuruluysa `circle.png` oluşturulur. Her iki dosya da web sayfalarına, raporlara veya daha ileri işleme dahil edilmeye hazırdır.

## Sonuç

Artık Python'da **SVG belgesi oluşturma**, **SVG'yi dosyaya kaydetme** ve **SVG görüntüsünü dışa aktarma** konularını biliyorsunuz. Örnek, temel API çağrılarını kapsar, her adımın neden önemli olduğunu açıklar ve daha karmaşık grafikler için genişletmeler sunar.

Sonraki adımda, yollar çizmeyi, degrade uygulamayı ve öğeleri animasyonlu hale getirmeyi içeren ek **SVG Python öğreticileri** keşfedin. Bu teknikleri entegre ederek Python uygulamalarınızdan doğrudan dinamik, veri‑odaklı vektör grafikler üretebileceksiniz. İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımları keşfetmeniz için adım‑adım açıklamalı tam çalışan kod örnekleri içerir.

- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}