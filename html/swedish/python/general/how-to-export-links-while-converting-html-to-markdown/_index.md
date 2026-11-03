---
category: general
date: 2026-08-22
description: Hur man exporterar länkar från HTML och konverterar dem till en markdown‑fil,
  inklusive stycken. Steg‑för‑steg‑guide för HTML‑till‑markdown‑konvertering.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export links
- convert html to markdown
- how to convert html
- how to extract paragraphs
- html to markdown file
language: sv
lastmod: 2026-08-22
og_description: Hur man exporterar länkar från ett HTML‑dokument och konverterar det
  till en markdown‑fil, inklusive stycken. Följ den här kompletta handledningen för
  pålitlig HTML‑till‑markdown‑konvertering.
og_image_alt: How to export links while converting HTML to Markdown
og_title: Hur man exporterar länkar när man konverterar HTML till Markdown – steg‑för‑steg‑guide
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
title: Hur man exporterar länkar när man konverterar HTML till Markdown
url: /sv/python/general/how-to-export-links-while-converting-html-to-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man exporterar länkar när man konverterar HTML till Markdown

Om du behöver **how to export links** från en HTML‑sida och omvandla resultatet till en ren **html to markdown file**, visar den här guiden de exakta stegen. Du kommer också att upptäcka **how to extract paragraphs** så att markdown‑utdata innehåller huvudinnehållet du bryr dig om. I slutet av handledningen kan du besvara frågan “**how to convert html** to markdown” med ett färdigt skript.

Att exportera länkar och extrahera stycken är vanliga uppgifter när du migrerar webbcontent till statiska webbplatser, dokumentationsportaler eller headless CMS‑back‑ends. Metoden nedan fungerar med GroupDocs Conversion SDK för Python, men koncepten gäller för alla bibliotek som låter dig konfigurera exportfunktioner.

---

## Vad du behöver

- Python 3.9 eller nyare  
- `groupdocs-conversion`‑paketet (installera med `pip install groupdocs-conversion`)  
- En HTML‑fil du vill bearbeta (t.ex. `input.html`)  
- Grundläggande kunskap om Python‑skriptning  

---

## Hur man exporterar länkar med HTML‑till‑Markdown‑konvertering

Det första stora steget är att konfigurera konverteringen så att endast de önskade funktionerna—länkar och stycken—skrivs till **html to markdown file**. SDK:n låter dig ange en bitmask av `MarkdownFeature`‑värden; vi kombinerar `LINKS` och `PARAGRAPHS` för att hålla utdata fokuserad.

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

### Varför detta fungerar

- **`HTMLDocument`** analyserar den ursprungliga filen och bygger ett DOM‑träd som konverteraren kan gå igenom.  
- **`MarkdownSaveOptions`** ger dig fin‑granulär kontroll över vad SDK:n skriver. Att sätta `features` till `LINKS | PARAGRAPHS` instruerar motorn att ignorera bilder, tabeller eller skript, vilket minskar brus i den slutliga **html to markdown file**.  
- **`Converter.convert`** utför det tunga arbetet. Den respekterar funktionsmasken, extraherar ankartaggar (`<a>`) och stycketaggar (`<p>`), och skriver dem med standard‑Markdown‑syntax.

---

## Hur man konverterar HTML till Markdown med fullständigt innehåll (valfritt)

Om du senare bestämmer dig för att du behöver hela sidan—inte bara länkar och stycken—justera helt enkelt funktionsmasken:

```python
# Export everything the SDK supports (links, paragraphs, images, tables, etc.)
markdown_options.features = MarkdownFeature.ALL
```

Att köra samma konvertering nu producerar en komplett **html to markdown file** som speglar den ursprungliga layouten. Detta demonstrerar **how to convert html** på ett flexibelt sätt: du styr utdata genom att växla funktionsflaggor.

---

## Hur man extraherar endast stycken

Ibland bryr du dig bara om den textuella kroppen i en artikel, inte om hyperlänkarna. Du kan isolera stycken genom att sätta masken till enbart `PARAGRAPHS`:

```python
markdown_options.features = MarkdownFeature.PARAGRAPHS
output_path = "YOUR_DIRECTORY/only_paragraphs.md"
Converter.convert(html_doc, markdown_options, output_path)
```

Den resulterande markdown‑filen kommer att innehålla ren, rad‑bryten text utan någon länk‑markup. Detta kodsnutt svarar på frågan **how to extract paragraphs** från en HTML‑källa.

---

## Vanliga fallgropar och hur man undviker dem

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| Tom utdatafil | Käll‑HTML‑filen innehåller inga `<a>`‑ eller `<p>`‑taggar som matchar de valda funktionerna. | Verifiera HTML‑strukturen eller bredda funktionsmasken (t.ex. inkludera `HEADINGS`). |
| Kodningsproblem | HTML‑filen använder en teckenkodning som inte är UTF‑8 och SDK:n läser den felaktigt. | Skicka en explicit kodning till `HTMLDocument`, t.ex. `HTMLDocument(path, encoding="iso-8859-1")`. |
| Skriver över befintlig markdown | Att köra skriptet flera gånger ersätter den tidigare filen. | Lägg till en tidsstämpel i utdatafilens namn eller kontrollera `os.path.exists` innan du skriver. |

**Pro tip:** När du bearbetar många filer i en mapp, omslut konverteringslogiken i en loop och logga varje resultat. Detta ger dig en tydlig revisionsspår och gör det enkelt att återuppta efter ett fel.

---

## Fullt skript du kan kopiera‑och‑klistra

Nedan är en fristående Python‑fil (`convert_links_paragraphs.py`) som du kan köra direkt. Den innehåller argument‑parsing så att du kan ange in‑ och utdata‑sökvägar utan att redigera koden.

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

**Hur man kör**

```bash
python convert_links_paragraphs.py YOUR_DIRECTORY/input.html YOUR_DIRECTORY/links_and_paragraphs.md --links --paragraphs
```

Kommandot ovan demonstrerar **how to export links** och **how to extract paragraphs** i ett enda anrop. Utelämna `--links` eller `--paragraphs` för att anpassa utdata efter dina behov.

---

## Verifiering – hur utdata ser ut

Givet följande enkla HTML (`input.html`):

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

Att köra skriptet med båda flaggorna producerar `links_and_paragraphs.md`:

```markdown
Welcome to the tutorial.

Visit [our site](https://example.com) for more info.
```

Du kan se att endast de två styckena och hyperlänken finns—precis vad du bad om när du sökte **how to export links** medan du utförde **convert html to markdown**.

---

## Nästa steg och relaterade ämnen

- **How to convert html to markdown** med bilder: lägg till `MarkdownFeature.IMAGES` till masken.  
- **How to extract paragraphs** och sedan efter‑processa  

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Set Offset When Converting HTML to Markdown in Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)
- [Convert HTML to Markdown – Complete C# Guide](/html/english/java/conversion-html-to-other-formats/convert-html-to-markdown-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}