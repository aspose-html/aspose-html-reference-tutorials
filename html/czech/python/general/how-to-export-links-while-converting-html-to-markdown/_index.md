---
category: general
date: 2026-08-22
description: Jak exportovat odkazy z HTML a převést je do souboru markdown, včetně
  odstavců. Krok za krokem průvodce konverzí HTML na markdown.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export links
- convert html to markdown
- how to convert html
- how to extract paragraphs
- html to markdown file
language: cs
lastmod: 2026-08-22
og_description: Jak exportovat odkazy z HTML dokumentu a převést je do souboru markdown,
  včetně odstavců. Sledujte tento kompletní návod pro spolehlivou konverzi HTML na
  markdown.
og_image_alt: How to export links while converting HTML to Markdown
og_title: Jak exportovat odkazy při převodu HTML na Markdown – krok za krokem průvodce
schemas:
- author: GroupDocs
  dateModified: '2026-08-22'
  description: How to export links from HTML and convert it to a markdown file, including
    paragraphs. Step‑by‑step guide for HTML to markdown conversion.
  headline: How to export links while converting HTML to Markdown
  type: TechArticle
tags:
- HTML conversion
- Markdown
- Python
title: Jak exportovat odkazy při převodu HTML na Markdown
url: /cs/python/general/how-to-export-links-while-converting-html-to-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak exportovat odkazy při převodu HTML na Markdown

Pokud potřebujete **jak exportovat odkazy** z HTML stránky a převést výsledek do čistého **html to markdown souboru**, tento průvodce vám ukáže přesné kroky. Také objevíte **jak extrahovat odstavce**, aby výstup v markdownu obsahoval hlavní obsah, na který vám záleží. Na konci tutoriálu budete schopni odpovědět na otázku “**jak převést html** na markdown” pomocí připraveného skriptu.

Exportování odkazů a extrahování odstavců jsou běžné úkoly při migraci webového obsahu na statické stránky, dokumentační portály nebo back‑endy headless CMS. Níže uvedený přístup funguje s GroupDocs Conversion SDK pro Python, ale koncepty platí pro libovolnou knihovnu, která umožňuje konfigurovat exportní funkce.

---

## Co budete potřebovat

- Python 3.9 nebo novější  
- balíček `groupdocs-conversion` (nainstalujte pomocí `pip install groupdocs-conversion`)  
- HTML soubor, který chcete zpracovat (např. `input.html`)  
- Základní znalost skriptování v Pythonu  

---

## Jak exportovat odkazy při převodu HTML na Markdown

Prvním hlavním krokem je nastavení převodu tak, aby byly do **html to markdown souboru** zapsány pouze požadované funkce — odkazy a odstavce. SDK vám umožňuje nastavit bitmasku hodnot `MarkdownFeature`; kombinujeme `LINKS` a `PARAGRAPHS`, aby byl výstup zaměřený.

```python
# Import the required classes from the GroupDocs Conversion SDK
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeature, Converter

# Step 1: Load the source HTML document
html_doc = HTMLDocument("YOUR_DIRECTORY/input.html")

# Step 2: Create Markdown save options and select the features to export
markdown_options = MarkdownSaveOptions()
# Export only links and paragraphs from the HTML
markdown_options.features = MarkdownFeature.LINKS | MarkdownFeature.PARAGRAPHS

# Step 3: Convert the HTML to Markdown using the configured options
output_path = "YOUR_DIRECTORY/links_and_paragraphs.md"
Converter.convert(html_doc, markdown_options, output_path)

print(f"Conversion complete. Markdown saved to {output_path}")
```

### Proč to funguje

- **`HTMLDocument`** parsuje původní soubor a vytváří DOM, který může konvertor procházet.  
- **`MarkdownSaveOptions`** vám poskytuje jemno‑granulární kontrolu nad tím, co SDK zapisuje. Nastavení `features` na `LINKS | PARAGRAPHS` říká enginu, aby ignoroval obrázky, tabulky nebo skripty, což snižuje šum ve finálním **html to markdown souboru**.  
- **`Converter.convert`** provádí těžkou práci. Respektuje masku funkcí, extrahuje značky kotvy (`<a>`) a odstavcové značky (`<p>`) a zapisuje je pomocí standardní syntaxe Markdown.

---

## Jak převést HTML na Markdown s kompletním obsahem (volitelné)

Pokud později zjistíte, že potřebujete celou stránku — nejen odkazy a odstavce — stačí upravit masku funkcí:

```python
# Export everything the SDK supports (links, paragraphs, images, tables, etc.)
markdown_options.features = MarkdownFeature.ALL
```

Spuštěním stejného převodu nyní získáte kompletní **html to markdown soubor**, který odráží původní rozložení. To demonstruje **jak převést html** flexibilním způsobem: řídíte výstup přepínáním příznaků funkcí.

## Jak extrahovat pouze odstavce

Někdy vás zajímají jen textové těla článku, nikoli hypertextové odkazy. Odstavce můžete izolovat nastavením masky pouze na `PARAGRAPHS`:

```python
markdown_options.features = MarkdownFeature.PARAGRAPHS
output_path = "YOUR_DIRECTORY/only_paragraphs.md"
Converter.convert(html_doc, markdown_options, output_path)
```

Výsledný markdown bude obsahovat čistý, zalomený text bez jakéhokoli značkování odkazů. Tento úryvek odpovídá na otázku **jak extrahovat odstavce** z HTML zdroje.

## Časté úskalí a jak se jim vyhnout

| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| Prázdný výstupní soubor | Zdrojové HTML neobsahuje žádné `<a>` ani `<p>` značky, které odpovídají vybraným funkcím. | Ověřte strukturu HTML nebo rozšiřte masku funkcí (např. zahrňte `HEADINGS`). |
| Problémy s kódováním | HTML používá znakovou sadu, která není UTF‑8, a SDK ji načítá nesprávně. | Předávejte explicitní kódování do `HTMLDocument`, např. `HTMLDocument(path, encoding="iso-8859-1")`. |
| Přepisování existujícího markdownu | Spuštění skriptu vícekrát přepíše předchozí soubor. | Přidejte časové razítko k názvu výstupního souboru nebo před zápisem zkontrolujte `os.path.exists`. |

**Tip:** Při zpracování mnoha souborů ve složce zabalte logiku převodu do smyčky a zaznamenávejte každý výsledek. To vám poskytne jasnou auditní stopu a usnadní obnovení po selhání.

---

## Kompletní skript, který můžete zkopírovat a vložit

Níže je samostatný Python soubor (`convert_links_paragraphs.py`), který můžete spustit přímo. Obsahuje parsování argumentů, takže můžete zadat vstupní a výstupní cesty bez úpravy kódu.

```python
#!/usr/bin/env python3
"""
convert_links_paragraphs.py

A complete example that shows how to export links and extract paragraphs
when converting HTML to a markdown file using GroupDocs Conversion SDK.
"""

import argparse
import os
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeature, Converter

def convert_html_to_md(input_html: str, output_md: str, features: int) -> None:
    """Perform the conversion with the given feature mask."""
    if not os.path.isfile(input_html):
        raise FileNotFoundError(f"Input file not found: {input_html}")

    # Load the HTML document
    html_doc = HTMLDocument(input_html)

    # Configure markdown options
    md_options = MarkdownSaveOptions()
    md_options.features = features

    # Run the conversion
    Converter.convert(html_doc, md_options, output_md)
    print(f"✅ Conversion finished – markdown saved to: {output_md}")

def main() -> None:
    parser = argparse.ArgumentParser(
        description="How to export links while converting HTML to Markdown."
    )
    parser.add_argument("input", help="Path to the source HTML file.")
    parser.add_argument(
        "output",
        help="Path for the resulting markdown file (e.g., links_and_paragraphs.md).",
    )
    parser.add_argument(
        "--links",
        action="store_true",
        help="Include links in the markdown output.",
    )
    parser.add_argument(
        "--paragraphs",
        action="store_true",
        help="Include paragraphs in the markdown output.",
    )
    args = parser.parse_args()

    # Build the feature mask based on user flags
    selected_features = 0
    if args.links:
        selected_features |= MarkdownFeature.LINKS
    if args.paragraphs:
        selected_features |= MarkdownFeature.PARAGRAPHS

    # Default to both links and paragraphs if no flag is provided
    if selected_features == 0:
        selected_features = MarkdownFeature.LINKS | MarkdownFeature.PARAGRAPHS

    try:
        convert_html_to_md(args.input, args.output, selected_features)
    except Exception as exc:
        print(f"❌ Conversion failed: {exc}")

if __name__ == "__main__":
    main()
```

**Jak spustit**

```bash
python convert_links_paragraphs.py YOUR_DIRECTORY/input.html YOUR_DIRECTORY/links_and_paragraphs.md --links --paragraphs
```

Příkaz výše demonstruje **jak exportovat odkazy** a **jak extrahovat odstavce** v jediném volání. Vynechejte `--links` nebo `--paragraphs`, abyste výstup přizpůsobili svým potřebám.

## Ověření – jak výstup vypadá

Vzhledem k následujícímu jednoduchému HTML (`input.html`):

```html
<!DOCTYPE html>
<html>
<head><title>Sample page</title></head>
<body>
  <p>Welcome to the tutorial.</p>
  <p>Visit <a href="https://example.com">our site</a> for more info.</p>
</body>
</html>
```

Spuštěním skriptu s oběma přepínači vznikne `links_and_paragraphs.md`:

```markdown
Welcome to the tutorial.

Visit [our site](https://example.com) for more info.
```

Uvidíte, že jsou přítomny pouze dva odstavce a hyperodkaz — přesně to, co jste požadovali při hledání **jak exportovat odkazy** během **convert html to markdown**.

## Další kroky a související témata

- **How to convert html to markdown** s obrázky: přidejte `MarkdownFeature.IMAGES` do masky.  
- **How to extract paragraphs** a poté post‑process  

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Set Offset When Converting HTML to Markdown in Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)
- [Convert HTML to Markdown – Complete C# Guide](/html/english/java/conversion-html-to-other-formats/convert-html-to-markdown-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}