---
category: general
date: 2026-09-26
description: Konvertera HTML till Markdown med Python, extrahera länkar från HTML
  och spara HTML som Markdown. Lär dig hur du konverterar HTML steg för steg.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- save html as markdown
- how to convert html
- extract paragraphs from html
language: sv
lastmod: 2026-09-26
og_description: Konvertera HTML till Markdown med Python, extrahera länkar från HTML
  och spara HTML som Markdown. Följ den kompletta guiden.
og_image_alt: Screenshot of Python code converting HTML to Markdown and showing extracted
  links
og_title: Konvertera HTML till Markdown i Python – extrahera länkar och stycken
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  headline: Convert HTML to Markdown in Python – extract links and paragraphs easily
  type: TechArticle
- description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  name: Convert HTML to Markdown in Python – extract links and paragraphs easily
  steps:
  - name: Expected output
    text: 'Running the script generates a file similar to the following (the exact
      content depends on the source HTML):'
  - name: 1. Extract only links
    text: '```python md_options.features = MarkdownFeatures.LINKS # No paragraphs
      ```'
  - name: 2. Extract only paragraphs
    text: '```python md_options.features = MarkdownFeatures.PARAGRAPHS # No links
      ```'
  type: HowTo
- questions:
  - answer: Yes. `HTMLDocument` accepts any well‑formed fragment; the converter treats
      the fragment as the document body.
    question: Does this work with HTML fragments (no `<html>` root tag)?
  - answer: 'Add `MarkdownFeatures.IMAGES` to the `features` flag: ```python md_options.features
      = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
      ```'
    question: Can I keep images as Markdown image syntax?
  - answer: 'Wrap `convert_html_to_markdown` in a loop that walks the directory with
      `os.listdir` or `pathlib.Path.rglob("*.html")`. --- ## Conclusion You now know
      how to **convert HTML to Markdown** in Python while selectively **extracting
      links from HTML** and **extracting paragraphs from HTML**. The script de'
    question: How do I convert many files in a directory?
  type: FAQPage
tags:
- html
- markdown
- python
- data‑extraction
title: Konvertera HTML till Markdown i Python – extrahera länkar och stycken enkelt
url: /sv/python/general/convert-html-to-markdown-in-python-extract-links-and-paragra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera HTML till Markdown i Python – extrahera länkar och stycken enkelt

Om du behöver **konvertera HTML till Markdown** och bara behålla de användbara delarna visar den här guiden hur du gör det med bara några rader Python. Oavsett om du skrapar blogginlägg, arkiverar dokumentation eller rensar e‑postmeddelanden, får du lära dig ett pålitligt sätt att extrahera länkar från HTML och spara HTML som Markdown.

Tutorialen täcker allt från att installera det nödvändiga paketet till att hantera kantfall som tomma `<a>`‑taggar eller nästlade stycken. I slutet har du ett färdigt skript som **konverterar HTML till Markdown**, extraherar länkar från HTML och till och med extraherar stycken från HTML när du behöver dem.

---

## Förutsättningar

Innan du börjar, se till att du har:

* Python 3.8 eller nyare installerat  
* Tillgång till `groupdocs-conversion`‑Python‑paketet (biblioteket som tillhandahåller `HTMLDocument`, `MarkdownSaveOptions` och `Converter`)  
* En lokal HTML‑fil som du vill bearbeta (t.ex. `article.html`)

Du kan installera biblioteket med pip:

```bash
pip install groupdocs-conversion
```

> **Pro tip:** Använd ett virtuellt miljö (`python -m venv venv`) för att hålla beroenden isolerade.

---

## Steg 1: Läs in käll‑HTML‑dokumentet

Den första operationen är att skapa ett `HTMLDocument`‑objekt som pekar på din källfil. Detta objekt abstraherar den råa HTML‑koden och ger konverteraren en ren ingångspunkt.

```python
from groupdocs.conversion import HTMLDocument

# Load the HTML file you want to transform
html_doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

*Varför detta är viktigt:* Att läsa in dokumentet på detta sätt låter biblioteket parsra DOM‑en en gång, så efterföljande operationer (som att extrahera länkar eller stycken) blir snabba och minnes‑effektiva.

---

## Steg 2: Skapa Markdown‑spara‑alternativ och välj de funktioner du behöver

`MarkdownSaveOptions` låter dig bestämma vilka HTML‑element som överlever konverteringen. `features`‑flaggan använder en bitvis OR för att kombinera alternativ.

```python
from groupdocs.conversion import MarkdownSaveOptions, MarkdownFeatures

# Keep only links and paragraphs in the resulting Markdown
md_options = MarkdownSaveOptions()
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS
```

*Varför detta är viktigt:* Genom att specificera `LINKS` och `PARAGRAPHS` **extraherar du länkar från HTML** och **extraherar stycken från HTML** samtidigt som allt annat (stilar, skript, bilder) tas bort. Om du senare bara behöver länkar, ersätt `MarkdownFeatures.PARAGRAPHS` med `0` (eller utelämna det).

---

## Steg 3: Konvertera HTML till Markdown med de konfigurerade alternativen

Anropa nu den statiska `convert_html`‑metoden, skicka in källdokumentet, destinationssökvägen och de alternativ du just byggt.

```python
from groupdocs.conversion import Converter

# Perform the conversion and write the Markdown file
Converter.convert_html(html_doc, "YOUR_DIRECTORY/article_links.md", md_options)
```

*Varför detta är viktigt:* Konverteringen körs i ett enda pass och tillämpar det filter du definierat. Den resulterande filen (`article_links.md`) innehåller bara Markdown‑formaterade länkar och stycken, vilket är exakt vad du behöver när du vill **spara HTML som Markdown** för vidare bearbetning.

---

## Fullt skript – allt tillsammans

Nedan är ett komplett, körbart skript som du kan kopiera‑klistra in i en fil med namnet `html_to_md.py`. Anpassa sökvägarna så att de matchar din miljö.

```python
# html_to_md.py
# -------------------------------------------------
# Convert HTML to Markdown, keeping only links and paragraphs.
# -------------------------------------------------

from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

def convert_html_to_markdown(source_path: str, target_path: str) -> None:
    """
    Convert an HTML file to Markdown, extracting only links and paragraphs.

    Args:
        source_path: Path to the source HTML file.
        target_path: Path where the Markdown file will be saved.
    """
    # Load the HTML document
    html_doc = HTMLDocument(source_path)

    # Configure conversion to keep links and paragraphs
    md_options = MarkdownSaveOptions()
    md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS

    # Run the conversion
    Converter.convert_html(html_doc, target_path, md_options)
    print(f"✅ Conversion complete – Markdown saved to: {target_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    src = "YOUR_DIRECTORY/article.html"
    dst = "YOUR_DIRECTORY/article_links.md"
    convert_html_to_markdown(src, dst)
```

### Förväntad utdata

När du kör skriptet genereras en fil som liknar följande (det exakta innehållet beror på käll‑HTML‑en):

```markdown
[OpenAI](https://openai.com)

This is the first paragraph of the article.

[GitHub](https://github.com)

Another paragraph that explains the next topic.
```

Endast länktexten och stycke­texten visas; alla andra HTML‑element har tagits bort.

---

## Extrahera bara länkar eller bara stycken (avancerade varianter)

Ibland behöver du **hur man konverterar HTML** till en Markdown‑fil som bara innehåller en typ av element.

### 1. Extrahera bara länkar

```python
md_options.features = MarkdownFeatures.LINKS   # No paragraphs
```

### 2. Extrahera bara stycken

```python
md_options.features = MarkdownFeatures.PARAGRAPHS   # No links
```

Båda varianterna återanvänder samma `convert_html`‑anrop, så du behöver inte skriva separat konverteringslogik.

---

## Hantera kantfall

| Situation                               | Rekommenderad åtgärd |
|----------------------------------------|----------------------|
| HTML‑fil innehåller tomma `<a>`‑taggar | Konverteraren hoppar automatiskt över tomma länkar. Om du ser stray `[]()`‑poster, sätt `md_options.removeEmptyLinks = True`. |
| Nästlade stycken (`<p>` inuti `<div>`) | Biblioteket plattar ut nästlade stycken och bevarar textordningen. Ingen extra kod behövs. |
| Icke‑ASCII‑tecken i länk‑titlar        | Se till att din Python‑fil sparas med UTF‑8‑kodning och öppna utdatafilen med `encoding="utf-8"` om du läser den senare. |
| Mycket stora HTML‑filer (≥ 50 MB)       | Processa filen i bitar med `HTMLDocument(stream=io.BytesIO(...))` för att undvika att ladda hela filen i minnet. |

---

## Vanliga frågor

**Q: Fungerar detta med HTML‑fragment (utan `<html>`‑rottag)?**  
A: Ja. `HTMLDocument` accepterar vilket väl‑format fragment som helst; konverteraren behandlar fragmentet som dokumentets kropp.

**Q: Kan jag behålla bilder som Markdown‑bildsyntax?**  
A: Lägg till `MarkdownFeatures.IMAGES` i `features`‑flaggan:  
```python
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
```

**Q: Hur konverterar jag många filer i en katalog?**  
A: Wrappa `convert_html_to_markdown` i en loop som går igenom katalogen med `os.listdir` eller `pathlib.Path.rglob("*.html")`.

---

## Slutsats

Du vet nu hur du **konverterar HTML till Markdown** i Python samtidigt som du selektivt **extraherar länkar från HTML** och **extraherar stycken från HTML**. Skriptet demonstrerar den standardiserade metoden – läs in dokumentet, konfigurera `MarkdownSaveOptions` och kör `Converter.convert_html`. Med några justeringar kan du också **spara HTML som Markdown** som bara innehåller länkar, bara stycken eller en fullständig trogen representation.

Nästa steg kan vara att utforska:

* Att lägga till `MarkdownFeatures.HEADINGS` för att bevara avsnittsrubriker.  
* Använda den resulterande Markdown‑filen som indata till statiska webbplatsgeneratorer som MkDocs eller Hugo.  
* Automatisera masskonverteringar för ett helt dokumentationsarkiv.

Lycka till med konverteringen!

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närbesläktade ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [How to Set Offset When Converting HTML to Markdown in Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}