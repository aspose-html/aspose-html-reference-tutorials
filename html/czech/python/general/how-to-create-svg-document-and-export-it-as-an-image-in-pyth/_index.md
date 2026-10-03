---
category: general
date: 2026-10-02
description: Naučte se, jak vytvořit SVG dokument v Pythonu, uložit SVG do souboru
  a exportovat SVG obrázek pomocí krátkého, kompletního skriptu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: cs
lastmod: 2026-10-02
og_description: Vytvořte SVG dokument v Pythonu a exportujte SVG obrázek pomocí tohoto
  praktického tutoriálu. Postupujte podle skriptu, uložte SVG do souboru a okamžitě
  znovu použijte vektorovou grafiku.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: Vytvořte SVG dokument v Pythonu – krok za krokem
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
title: Jak vytvořit SVG dokument a exportovat jej jako obrázek v Pythonu
url: /cs/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vytvořit SVG dokument a exportovat jej jako obrázek v Pythonu

Pokud potřebujete **create SVG document** programově, tento tutoriál vám přesně ukáže, jak to provést v Pythonu. Uvidíte kompletní skript, který vytvoří jednoduchý kruh, uloží SVG do souboru a vytvoří exportovatelný SVG obrázek, který můžete vložit kamkoli.

Generování škálovatelných vektorových grafik z kódu odstraňuje ruční úsilí při kreslení tvarů v GUI editoru. Na konci tohoto průvodce budete schopni integrovat tvorbu SVG do pipeline pro vizualizaci dat, automatizovaných generátorů reportů nebo jakéhokoli projektu, který vyžaduje ostrou, rozlišením nezávislou grafiku.

## Prerequisites

Než začnete, ujistěte se, že máte:

- Python 3.8 nebo novější nainstalovaný
- Knihovnu `svgwrite` (nainstalujte pomocí `pip install svgwrite`)
- Oprávnění k zápisu do adresáře, kam bude SVG uloženo

Tyto požadavky udržují příklad lehký a kompatibilní s většinou prostředí.

## Step 1: Install and import the SVG library

Prvním krokem je přidat knihovnu třetí strany, která poskytuje pohodlné API pro tvorbu SVG.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` abstrahuje XML strukturu SVG souboru, což vám umožní soustředit se na geometrii místo surového markupu.

## Step 2: Create an SVG document object

Nyní můžete **create SVG document** vytvořením instance `svgwrite.Drawing`. Tento objekt představuje kořenový element `<svg>` a obsahuje všechny následné tvary.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

Argument `size` určuje vykreslené rozměry v pixelech, zatímco `viewBox` nastavuje souřadnicový systém, který odpovídá geometrii, kterou později definujete.

## Step 3: Add a circle element

Kruh je definován svým středem (`cx`, `cy`) a poloměrem (`r`). Použijte pomocnou funkci `circle` k přiřazení těchto atributů.

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

Kruh leží uprostřed plátna 100 × 100, přičemž na každé straně zůstává okraj 10 pixelů. Upravit `fill` a `stroke` tak, aby odpovídaly vašemu designu.

## Step 4: Save the SVG to file

Po sestavení grafiky můžete **save SVG to file** pomocí metody `save`. Tím se zapíše dobře strukturované XML, které rozumí prohlížeče i vektorové editory.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

Soubor `circle.svg` se nyní nachází v aktuálním pracovním adresáři. Můžete jej otevřít ve webovém prohlížeči, Inkscape nebo v jakémkoli nástroji, který podporuje formát SVG.

## Step 5: Verify the exported SVG image

Otevřete uložený soubor v prohlížeči a ověřte výstup. Měli byste vidět centrovaný kruh se zadanými barvami. Surové XML vypadá takto:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

Protože SVG je vektorové, můžete obrázek škálovat bez ztráty kvality, což je ideální pro responzivní webové designy nebo tisk ve vysokém rozlišení.

## Pro tip: Export SVG as PNG or JPEG

Pokud potřebujete rastrovou verzi, zkombinujte SVG soubor s konverzním nástrojem, například **CairoSVG**:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Tento krok demonstruje **export SVG image** do bitmapového formátu, užitečný, když downstream systémy nedokážou SVG přímo renderovat.

## Common variations and edge cases

| Variace | Jak postupovat |
|-----------|---------------|
| Více tvarů | Zavolejte `dwg.add()` pro každý nový prvek (rect, line, path). |
| Dynamické rozměry | Vypočítejte `size` a `viewBox` z dat před vytvořením `Drawing`. |
| Textové popisky | Použijte `dwg.text("Label", insert=("10", "20"))` a stylizujte pomocí `font_size` a `fill`. |
| Opětovné použití dokumentu | Uchovejte objekt `Drawing` v paměti a zavolejte `save()`, kdykoli potřebujete aktualizovaný soubor. |
| Velké soubory | Streamujte výstup pomocí `dwg.tostring()` a zapište jej ručně do souborového objektu, abyste předešli špičkám paměti. |

Řešení těchto scénářů zajišťuje, že váš **how to generate SVG** skript škáluje od jednoduchých ikon po složité diagramy.

## Full script recap

Níže je kompletní, spustitelný příklad, který zahrnuje všechny kroky a volitelnou konverzi:

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

Spuštěním tohoto skriptu vznikne `circle.svg` a pokud je nainstalován `cairosvg`, také `circle.png`. Oba soubory jsou připravené k vložení do webových stránek, reportů nebo dalšího zpracování.

## Conclusion

Nyní víte, jak **create SVG document** v Pythonu, **save SVG to file** a **export SVG image** pro širší využití. Příklad pokrývá základní API volání, vysvětluje, proč je každý krok důležitý, a nabízí rozšíření pro složitější grafiku.

Dále prozkoumejte další témata **SVG Python tutorial**, jako je kreslení cest, aplikace gradientů a animace elementů. Integrací těchto technik budete schopni generovat dynamické, datově řízené vektorové grafiky přímo z vašich Python aplikací. Šťastné kódování!

## What Should You Learn Next?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok za krokem vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vytváření a správa SVG dokumentů v Aspose.HTML pro Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Uložení SVG dokumentu v Aspose.HTML pro Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg na png java – Převod SVG na obrázek s Aspose.HTML pro Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}