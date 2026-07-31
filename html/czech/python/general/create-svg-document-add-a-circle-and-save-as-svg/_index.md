---
category: general
date: 2026-07-31
description: Naučte se, jak vytvořit SVG dokument, přidat kruh a rychle uložit SVG
  soubor. Exportujte grafiku jako SVG pomocí několika řádků kódu v Pythonu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: cs
lastmod: 2026-07-31
og_description: Vytvořte SVG dokument, přidejte kruh a uložte SVG soubor během několika
  sekund. Tento návod vám ukáže, jak exportovat grafiku jako SVG s jasným, spustitelným
  kódem.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: Vytvořit SVG dokument – přidat kruh a uložit jako SVG
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
title: Vytvořte SVG dokument – přidejte kruh a uložte jako SVG
url: /cs/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření SVG dokumentu – Přidání kruhu a uložení jako SVG

Už jste někdy potřebovali **create SVG document** z kódu, ale nevedeli ste, kde začít? Nejste v tom sami; mnoho vývojářů narazí na tuto překážku, když poprvé experimentují s vektorovou grafikou. V tomto tutoriálu projdeme malý, samostatný příklad, který vám ukáže, jak **add circle to SVG**, poté **save SVG file**, abyste mohli **export graphic as SVG** pro použití na webu nebo v designových nástrojích.

Budeme držet věci lehké: jen několik řádků Pythonu, populární knihovnu pro SVG a špetku vysvětlení. Na konci budete mít připravený `circle.svg` ve své složce a pochopíte, proč je každý krok důležitý—žádné vágní zkratky typu „viz dokumentaci“.

## Co budete potřebovat

- Python 3.8+ (jakákoli recent verze funguje)
- Balíček `svgwrite` – nainstalujte jej pomocí `pip install svgwrite`
- Textový editor nebo IDE (VS Code, PyCharm nebo i Notepad stačí)
- Oprávnění k zápisu do adresáře, kam chcete soubor uložit

To je vše. Žádné těžkopádné závislosti, žádné externí služby.

## Krok 1: Nastavení SVG dokumentu

Vytvoření SVG dokumentu je tak jednoduché, jako vytvořit objekt `Drawing` z `svgwrite`. Představte si tento objekt jako prázdné plátno, kde žije každý tvar.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Proč je to důležité:** Třída `Drawing` za vás řeší veškerý XML boilerplate—jmenné prostory, hlavičky a kořenový prvek `<svg>`. Tím, že hned na začátku zadáte název souboru, už víme, kam soubor skončí, což pozdější krok **save svg file** učiní triviálním.

### Tip
Pokud plánujete generovat mnoho souborů ve smyčce, dejte každému `Drawing` unikátní název nebo použijte `io.BytesIO`, abyste vše drželi v paměti, dokud nebudete připraveni zapisovat.

## Krok 2: Přidání kruhu do SVG

Nyní, když dokument existuje, pojďme **add circle to SVG**. Metoda `add()` přijímá jakýkoli objekt tvaru; `Circle` je ideální pro jednoduchou červenou tečku uprostřed.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Proč používáme proměnné `center` a `radius`:** Vkládání čísel přímo do kódu ztěžuje čtení a údržbu. Pojmenováním hodnot objasňujeme záměr—tento kruh leží přesně uprostřed plátna 200 × 200 a je dostatečně velký, aby byl vidět.

### Okrajový případ – Průhledné pozadí
Pokud potřebujete průhledné pozadí (výchozí pro SVG), můžete vynechat nastavení `fill` na kořeni. Pro bílé pozadí přidejte:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

Umístěte to před přidáním kruhu, aby obdélník byl pod ním.

## Krok 3: Uložení SVG souboru

S tvarem na místě je posledním krokem **save SVG file**. Metoda `save()` zapíše XML na disk a protože jsme už `Drawing`u zadali název souboru, stačí jedno volání.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **Co se děje pod kapotou?** `svgwrite` serializuje strom elementů do řetězce, přidá XML deklaraci a zapíše ho pomocí kódování UTF‑8. Pokud cílový adresář neexistuje, Python vyvolá `FileNotFoundError`; ujistěte se, že cesta je platná nebo ji vytvořte pomocí `os.makedirs()`.

### Bonus: Programatické exportování grafiky jako SVG
Pokud potřebujete obsah SVG jako řetězec—například pro vložení do HTML e‑mailu—můžete zavolat `dwg.tostring()` místo `save()`:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Kompletní funkční příklad

Spojením všeho dohromady získáte kompletní, připravený ke spuštění skript:

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

**Očekávaný výstup:** Po spuštění skriptu uvidíte soubor `circle.svg` ve stejné složce. Otevřením v prohlížeči nebo jakémkoli vektorovém editoru se zobrazí červený kruh uprostřed bílého čtverce—přesně to, co jsme naprogramovali.

## Časté otázky a úskalí

- **Co když chci jiný tvar?** Vyměňte `dwg.circle` za `dwg.rect`, `dwg.ellipse` nebo dokonce za vlastní řetězec `<path>`. API je napříč tvary konzistentní.
- **Mohu SVG vložit přímo do HTML?** Ano. Soubor, který jste právě vytvořili, můžete odkazovat pomocí `<img src="circle.svg" alt="Red circle">` nebo vložit přímo pomocí značek `<svg>`.
- **Proč nepíšeme čisté XML?** Můžete, ale knihovny jako `svgwrite` řeší zvláštnosti jmenných prostorů a činí kód mnohem udržitelnějším—obzvláště když začnete přidávat gradienty nebo animace.

## Závěr

Nyní už víte, jak **create SVG document**, **add circle to SVG** a **save SVG file**, abyste mohli **export graphic as SVG** pomocí několika řádků Pythonu. Tento vzor je škálovatelný: nahraďte kruh libovolným vektorovým tvarem, iterujte přes data pro generování grafů nebo hromadně zpracovávejte assety pro designový systém.

Další kroky? Zkuste přidat textové popisky, experimentovat s gradienty nebo vygenerovat celou galerii ikon v jednom skriptu. Pokud vás zajímají pokročilejší funkce, podívejte se do dokumentace `svgwrite` na skupiny (`<g>`), transformace a podporu animací.

Šťastné kódování a ať jsou vaše vektory vždy ostré!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Uložit SVG dokument v Aspose.HTML pro Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Vytvořit a spravovat SVG dokumenty v Aspose.HTML pro Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Převod SVG na obrázek s Aspose.HTML pro Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}