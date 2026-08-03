---
category: general
date: 2026-08-03
description: Konvertera HTML till Markdown med Python. Lär dig hur du extraherar länkar
  från HTML och extraherar stycken från HTML i en enda, effektiv konvertering.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- extract paragraphs from html
language: sv
lastmod: 2026-08-03
og_description: Konvertera HTML till Markdown i Python med ett kort exempel som visar
  hur man extraherar länkar från HTML och extraherar stycken från HTML samtidigt som
  resultatet sparas som en Markdown‑fil.
og_image_alt: Screenshot of Python code converting an HTML file to Markdown with selected
  links and paragraphs
og_title: Konvertera HTML till Markdown i Python – fullständig extraktionsguide
schemas:
- author: GroupDocs
  dateModified: '2026-08-03'
  description: Convert HTML to Markdown using Python. Learn how to extract links from
    HTML and extract paragraphs from HTML in a single, efficient conversion.
  headline: Convert HTML to Markdown Python – extract links & paragraphs
  type: TechArticle
- description: Convert HTML to Markdown using Python. Learn how to extract links from
    HTML and extract paragraphs from HTML in a single, efficient conversion.
  name: Convert HTML to Markdown Python – extract links & paragraphs
  steps:
  - name: Load the HTML document you want to convert
    text: '```python from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions,
      Converter'
  - name: Create a feature set that includes only the elements you need
    text: '```python # Instantiate the feature collection. selected_features = MarkdownSaveOptions.Features()'
  - name: Attach the feature set to the Markdown save options
    text: '```python md_options = MarkdownSaveOptions() md_options.features = selected_features
      ```'
  - name: Perform the conversion and save the result as a Markdown file
    text: '```python output_path = "YOUR_DIRECTORY/links_and_paragraphs.md" Converter.convert_html(html_doc,
      md_options, output_path) print(f"Conversion complete. Markdown saved to {output_path}")
      ```'
  type: HowTo
tags:
- HTML conversion
- Markdown
- Python
title: Konvertera HTML till Markdown med Python – extrahera länkar och stycken
url: /sv/python/general/convert-html-to-markdown-python-extract-links-paragraphs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera HTML till Markdown med Python – extrahera länkar & stycken

Om du behöver **konvertera HTML till Markdown**, visar den här handledningen ett praktiskt sätt att göra det i Python samtidigt som du selektivt **extraherar länkar från HTML** och **extraherar stycken från HTML**. Du får se ett komplett, körbart exempel som sparar det filtrerade innehållet som en ren Markdown‑fil.

Att konvertera HTML till Markdown är ett vanligt steg när du vill ha lättviktig, versionsstyrd dokumentation, statisk‑webbplats‑innehåll eller helt enkelt en ren‑text‑representation av en webbsida. I slutet av den här guiden har du ett skript som:

1. Laddar ett HTML‑dokument från disk.  
2. Konfigurerar en funktionsuppsättning som bara behåller länkar och stycke‑element.  
3. Utför konverteringen med GroupDocs Conversion SDK för Python.  
4. Skriver resultatet till en `.md`‑fil.

## Förutsättningar

Innan du börjar, se till att du har:

| Krav | Varför det är viktigt |
|------|-----------------------|
| Python 3.9+ | SDK:n riktar sig mot moderna Python‑versioner. |
| `groupdocs-conversion`‑paketet | Tillhandahåller klasserna `HTMLDocument`, `MarkdownSaveOptions` och `Converter` som används i exemplet. |
| En HTML‑fil att testa (t.ex. `sample.html`) | Källan du kommer att konvertera. |

Installera SDK:n med pip:

```bash
pip install groupdocs-conversion
```

> **Proffstips:** Använd en virtuell miljö (`python -m venv .venv`) för att hålla beroenden isolerade.

## Konvertera HTML till Markdown med Python

Kärnan i konverteringen består av några enkla steg. Varje steg förklaras nedan, och hela skriptet visas i slutet av artikeln.

### Steg 1: Ladda HTML‑dokumentet du vill konvertera

```python
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, Converter

# Replace YOUR_DIRECTORY with the path that contains your HTML file.
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

*Varför detta steg?*  
`HTMLDocument` analyserar källfilen och bygger en intern DOM‑representation som konverteraren kan arbeta med. Utan att först ladda dokumentet har SDK:n inget att bearbeta.

### Steg 2: Skapa en funktionsuppsättning som bara innehåller de element du behöver

```python
# Instantiate the feature collection.
selected_features = MarkdownSaveOptions.Features()

# Keep only hyperlinks.
selected_features.add(MarkdownSaveOptions.Features.LINK)

# Keep only paragraph tags.
selected_features.add(MarkdownSaveOptions.Features.PARAGRAPH)
```

*Varför vi lägger till dessa funktioner*  
`MarkdownSaveOptions.Features` fungerar som ett filter. Genom att lägga till `LINK` och `PARAGRAPH` säger vi åt konverteraren att **extrahera länkar från HTML** och **extrahera stycken från HTML**, och ignorera bilder, tabeller, skript och annan markup som du kanske inte behöver i den slutliga Markdown‑filen.

### Steg 3: Koppla funktionsuppsättningen till Markdown‑spara‑alternativen

```python
md_options = MarkdownSaveOptions()
md_options.features = selected_features
```

*Varför detta steg?*  
`MarkdownSaveOptions` innehåller alla konverteringsinställningar. Genom att tilldela den tidigare byggda `selected_features` säkerställer vi att konverteringen följer vår filterkonfiguration.

### Steg 4: Utför konverteringen och spara resultatet som en Markdown‑fil

```python
output_path = "YOUR_DIRECTORY/links_and_paragraphs.md"
Converter.convert_html(html_doc, md_options, output_path)
print(f"Conversion complete. Markdown saved to {output_path}")
```

*Varför vi anropar `convert_html`*  
`Converter.convert_html` är SDK:ns ingångspunkt för HTML‑till‑Markdown‑omvandlingar. Den läser `HTMLDocument`, tillämpar `md_options` och skriver det filtrerade resultatet till `output_path`.

#### Förväntat resultat

Den resulterande `links_and_paragraphs.md` kommer endast att innehålla Markdown‑representationer av hyperlänkar och stycketext, till exempel:

```markdown
[Visit the homepage](https://example.com)

This is the first paragraph of the article, describing the main topic.

Another paragraph with more details.
```

Alla andra HTML‑element såsom `<img>`, `<table>` eller `<script>` utelämnas, vilket gör filen lättviktig och enkel att redigera.

## Extrahera länkar från HTML (valfri djupdykning)

Om ditt mål är **endast att extrahera länkar från HTML** samtidigt som du kastar bort allt annat, kan du förenkla funktionsuppsättningen:

```python
link_only_features = MarkdownSaveOptions.Features()
link_only_features.add(MarkdownSaveOptions.Features.LINK)

md_options.features = link_only_features
```

Att köra konverteringen med denna konfiguration producerar en Markdown‑fil där varje länk visas på en egen rad, t.ex.:



Den följande texten beskriver nästa steg:

De följande handledningarna täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Konvertera HTML till Markdown i Aspose.HTML för Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Konvertera HTML till Markdown i .NET med Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Hur man konverterar HTML till PDF Java – med Aspose.HTML för Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}