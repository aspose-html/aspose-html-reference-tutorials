---
category: general
date: 2026-09-26
description: Converteer HTML naar Markdown met Python, haal links uit HTML en sla
  HTML op als Markdown. Leer hoe je HTML stap‑voor‑stap converteert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- save html as markdown
- how to convert html
- extract paragraphs from html
language: nl
lastmod: 2026-09-26
og_description: Converteer HTML naar Markdown met Python, links uit HTML extraheren
  en HTML opslaan als Markdown. Volg deze volledige gids.
og_image_alt: Screenshot of Python code converting HTML to Markdown and showing extracted
  links
og_title: HTML naar Markdown converteren in Python – links en alinea’s extraheren
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
title: HTML naar Markdown converteren in Python – links en alinea’s eenvoudig extraheren
url: /nl/python/general/convert-html-to-markdown-in-python-extract-links-and-paragra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML naar Markdown converteren in Python – links en alinea's eenvoudig extraheren

Als je **HTML naar Markdown** wilt **converteren** terwijl je alleen de nuttige delen behoudt, laat deze gids je zien hoe je dat doet met slechts een paar regels Python. Of je nu blogposts scrapt, documentatie archiveert of e‑mailinhoud opschoont, je leert een betrouwbare manier om links uit HTML te extraheren en HTML op te slaan als Markdown.

De tutorial behandelt alles, van het installeren van het benodigde pakket tot het afhandelen van randgevallen zoals lege `<a>`‑tags of geneste alinea's. Aan het einde heb je een kant‑klaar script dat **HTML naar Markdown converteert**, links uit HTML extraheert, en zelfs alinea's uit HTML haalt wanneer je die nodig hebt.

---

## Vereisten

* Python 3.8 of nieuwer geïnstalleerd  
* Toegang tot het `groupdocs-conversion` Python‑pakket (de bibliotheek die `HTMLDocument`, `MarkdownSaveOptions` en `Converter` levert)  
* Een lokaal HTML‑bestand dat je wilt verwerken (bijv. `article.html`)

Je kunt de bibliotheek installeren met pip:

```bash
pip install groupdocs-conversion
```

> **Pro tip:** Gebruik een virtuele omgeving (`python -m venv venv`) om afhankelijkheden geïsoleerd te houden.

---

## Stap 1: Laad het bron‑HTML‑document

De eerste handeling is het aanmaken van een `HTMLDocument`‑object dat naar je bronbestand wijst. Dit object abstraheert de ruwe HTML en geeft de converter een schoon ingangspunt.

```python
from groupdocs.conversion import HTMLDocument

# Load the HTML file you want to transform
html_doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

*Waarom dit belangrijk is:* Het laden van het document op deze manier laat de bibliotheek de DOM één keer parseren, zodat latere bewerkingen (zoals het extraheren van links of alinea's) snel en geheugen‑efficiënt zijn.

## Stap 2: Maak Markdown‑opslaan‑opties en selecteer de functies die je nodig hebt

`MarkdownSaveOptions` laat je bepalen welke HTML‑elementen de conversie overleven. De `features`‑vlag gebruikt een bitwise OR om opties te combineren.

```python
from groupdocs.conversion import MarkdownSaveOptions, MarkdownFeatures

# Keep only links and paragraphs in the resulting Markdown
md_options = MarkdownSaveOptions()
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS
```

*Waarom dit belangrijk is:* Door `LINKS` en `PARAGRAPHS` te specificeren **extraheer je links uit HTML** en **extraheer je alinea's uit HTML** terwijl je alles anders (stijlen, scripts, afbeeldingen) weggooit. Als je later alleen links nodig hebt, vervang je `MarkdownFeatures.PARAGRAPHS` door `0` (of laat je het weg).

## Stap 3: Converteer de HTML naar Markdown met de geconfigureerde opties

Roep nu de statische `convert_html`‑methode aan, waarbij je het bron‑document, het bestemmingspad en de opties die je zojuist hebt gebouwd doorgeeft.

```python
from groupdocs.conversion import Converter

# Perform the conversion and write the Markdown file
Converter.convert_html(html_doc, "YOUR_DIRECTORY/article_links.md", md_options)
```

*Waarom dit belangrijk is:* De conversie wordt in één enkele doorloop uitgevoerd, waarbij de door jou gedefinieerde functie‑filter wordt toegepast. Het resulterende bestand (`article_links.md`) bevat alleen Markdown‑geformatteerde links en alinea's, wat precies is wat je nodig hebt wanneer je **HTML wilt opslaan als Markdown** voor verdere verwerking.

## Volledig script – alles samen

Hieronder staat een volledig, uitvoerbaar script dat je kunt kopiëren‑en‑plakken in een bestand genaamd `html_to_md.py`. Pas de paden aan zodat ze bij jouw omgeving passen.

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

### Verwachte output

Het uitvoeren van het script genereert een bestand dat lijkt op het volgende (de exacte inhoud hangt af van de bron‑HTML):

```markdown
[OpenAI](https://openai.com)

This is the first paragraph of the article.

[GitHub](https://github.com)

Another paragraph that explains the next topic.
```

Alleen de linktekst en de alinea‑tekst verschijnen; alle andere HTML‑elementen worden verwijderd.

---

## Alleen links of alleen alinea's extraheren (geavanceerde variaties)

Soms heb je **hoe HTML te converteren** naar een Markdown‑bestand nodig dat slechts één type element bevat.

### 1. Alleen links extraheren

```python
md_options.features = MarkdownFeatures.LINKS   # No paragraphs
```

### 2. Alleen alinea's extraheren

```python
md_options.features = MarkdownFeatures.PARAGRAPHS   # No links
```

Beide variaties hergebruiken dezelfde `convert_html`‑aanroep, zodat je geen aparte conversielogica hoeft te schrijven.

## Randgevallen afhandelen

| Situation                               | Recommended fix |
|----------------------------------------|-----------------|
| HTML‑bestand bevat lege `<a>`‑tags    | De converter slaat lege links automatisch over. Als je losse `[]()`‑items ziet, stel je `md_options.removeEmptyLinks = True` in. |
| Geneste alinea's (`<p>` binnen `<div>`) | De bibliotheek vlakt geneste alinea's af, behoudt de tekstvolgorde. Geen extra code nodig. |
| Niet‑ASCII‑tekens in linktitels    | Zorg ervoor dat je Python‑bestand is opgeslagen met UTF‑8‑codering en open het uitvoerbestand met `encoding="utf-8"` als je het later leest. |
| Zeer grote HTML‑bestanden (≥ 50 MB)        | Verwerk het bestand in delen met `HTMLDocument(stream=io.BytesIO(...))` om te voorkomen dat het volledige bestand in het geheugen wordt geladen. |

## Veelgestelde vragen

**Q: Werkt dit met HTML‑fragmenten (geen `<html>`‑root‑tag)?**  
A: Ja. `HTMLDocument` accepteert elk goed gevormd fragment; de converter behandelt het fragment als de document‑body.

**Q: Kan ik afbeeldingen behouden als Markdown‑afbeeldingssyntaxis?**  
A: Voeg `MarkdownFeatures.IMAGES` toe aan de `features`‑vlag:  
```python
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
```

**Q: Hoe converteer ik veel bestanden in een map?**  
A: Plaats `convert_html_to_markdown` in een lus die de map doorloopt met `os.listdir` of `pathlib.Path.rglob("*.html")`.

## Conclusie

Je weet nu hoe je **HTML naar Markdown** kunt **converteren** in Python terwijl je selectief **links uit HTML extraheert** en **alinea's uit HTML extraheert**. Het script toont de standaard aanpak — laad het document, configureer `MarkdownSaveOptions` en voer `Converter.convert_html` uit. Met een paar aanpassingen kun je ook **HTML opslaan als Markdown** dat alleen links, alleen alinea's, of een volledige getrouwe weergave bevat.

Vervolgens kun je het volgende verkennen:

* Voeg `MarkdownFeatures.HEADINGS` toe om sectietitels te behouden.  
* Gebruik de resulterende Markdown als invoer voor statische site‑generatoren zoals MkDocs of Hugo.  
* Automatiseer bulk‑conversies voor een volledige documentatierepository.

Veel plezier met converteren!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [HTML naar Markdown converteren in .NET met Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [HTML naar Markdown converteren in Aspose.HTML voor Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Hoe offset in te stellen bij het converteren van HTML naar Markdown in Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}