---
category: general
date: 2026-11-27
description: Vytvořte SVG dokument a uložte SVG soubor pomocí Pythonu. Naučte se exportovat
  vektor jako SVG a rychle generovat SVG obrázek.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: cs
lastmod: 2026-11-27
og_description: Vytvořte SVG dokument a uložte SVG soubor pomocí Pythonu. Tento návod
  vám ukáže, jak exportovat vektor jako SVG a během několika minut vytvořit SVG obrázek.
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: Vytvořte SVG dokument a uložte SVG soubor pomocí Pythonu
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: Vytvořte SVG dokument a uložte SVG soubor pomocí Pythonu
url: /cs/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření SVG dokumentu a uložení SVG souboru pomocí Pythonu

Pokud potřebujete **vytvořit SVG dokument** od nuly, tento průvodce vás provede celým procesem. Uvidíte, jak **uložit SVG soubor** na disk, exportovat vektor jako SVG, a získáte připravený SVG obrázek během několika řádků kódu.

Programatické generování škálovatelných grafik je užitečné pro zprávy, UI ikony nebo jakoukoli situaci, kde chcete obrázky nezávislé na rozlišení. Na konci tohoto tutoriálu budete schopni odpovědět na otázku „**how to create SVG**?“ pro jednoduché tvary a rozšířit vzor na složitější vektorové umění.

## Co budete potřebovat

- Python 3.8 nebo novější  
- Balíček `svgwrite` (instalovatelný pomocí `pip`)  
- Zapisovatelný adresář pro výstupní soubor  

Nejsou vyžadovány žádné externí grafické editory; vše běží z příkazové řádky.

## Krok 1: Instalace knihovny `svgwrite`

`svgwrite` poskytuje čisté, Pythonické API pro tvorbu SVG značek. Nainstalujte jej jednou pomocí:

```bash
pip install svgwrite
```

> **Tip:** Použijte virtuální prostředí (`python -m venv .venv`) k izolaci závislostí.

## Krok 2: Vytvoření SVG dokumentu

Nyní skutečně **vytvoříme SVG dokument** objekty. Třída `Drawing` představuje kořenový prvek `<svg>` a automaticky spravuje jmenné prostory.

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

Instance `Drawing` je vstupním bodem pro všechny následné SVG operace. Zadáním `size` nastavíme rozměry plátna, což ovlivňuje, jak prohlížeče vykreslují obrázek.

## Krok 3: Přidání červeného kruhu

Přidávání tvarů je jednoduché. Metoda `circle` vytvoří prvek `<circle>`; poté jej připojíme ke kořeni.

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Proč volíme kruh: kruhy jsou vektorové primitivy, které ukazují škálovatelnost bez ztráty kvality, což činí výstup ideálním pro testování workflow **export vector as SVG**.

## Krok 4: Uložení SVG souboru

Nakonec zapíšeme značky na disk. Tento krok splňuje požadavek **save SVG file** a vytvoří soubor, který můžete otevřít v libovolném prohlížeči nebo vektorovém editoru.

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

Když spustíte skript, uvidíte zprávu v konzoli potvrzující umístění vygenerovaného souboru.

### Očekávaný výstup

Výsledný soubor `circle.svg` obsahuje:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

Otevření souboru v prohlížeči zobrazí ostrý červený kruh a protože je vektorový, můžete přibližovat neomezeně bez pixelace.

## Krok 5: Běžné varianty a okrajové případy

### Export složitějších vektorů

Pokud potřebujete **export vector as SVG** pro vícestupňové ilustrace, jednoduše opakujte vzor `dwg.add()` s dalšími primitivy (`rect`, `line`, `path`, atd.). Například:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### Práce s Unicode a textem

SVG podporuje textové elementy s plnou podporou Unicode. Použijte `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` pro vložení vícejazykových popisků.

### Uložení na jiné místo

Když **save SVG image** do uživatelem určené složky, ověřte cestu, aby nedošlo k chybám oprávnění:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### Minimalizace výstupu

Pro produkční pipeline můžete chtít menší velikost souboru. Předávejte `pretty=False` do `dwg.tostring()` a výsledek zapište ručně:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## Jak vytvořit SVG s alternativními knihovnami (volitelné)

Zatímco `svgwrite` je lehký a čistě Pythonový, existují i jiné ekosystémy:

- **cairosvg** – převádí PNG, PDF nebo HTML na SVG.  
- **lxml** – umožňuje ručně vytvářet SVG značky pomocí XML API.  

Výběr knihovny závisí na složitosti vašeho projektu a existujících závislostech.

## Závěr

Nyní víte, jak **create SVG document**, přidat vektorové tvary a **save SVG file** pomocí Pythonu. Kompletní řešení ukazuje kroky k **export vector as SVG**, vytvoření **SVG image** a odpověď na častý dotaz **how to create SVG** programově.

Odtud můžete:

- Rozšířit skript pomocí smyček pro automatické generování grafů nebo ikon.  
- Integrovat SVG výstup do webových aplikací nebo e‑mailových šablon.  
- Prozkoumat animaci přidáním elementů `<animate>` pomocí `svgwrite`.

Experimentujte s různými tvary, barvami a přechody, abyste plně využili sílu škálovatelných vektorových grafik ve svých Python projektech. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vytvořit SVG dokument – Přidat kruh a uložit jako SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Vytvořit SVG dokument v Pythonu – Průvodce konverzí SVG na PNG](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Načíst SVG soubor v Pythonu – Kompletní průvodce exportem, vkládáním a konverzí](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}