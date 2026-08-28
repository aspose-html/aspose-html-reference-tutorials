---
category: general
date: 2026-07-27
description: Hoe SaveOptions in Aspose.HTML (Python) te gebruiken om een grote HTML‑pagina
  te converteren en efficiënt resourcebeheer toe te passen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use SaveOptions
- convert large html page
- apply resource handling
- Aspose.HTML Python
- HTML resource handling
language: nl
lastmod: 2026-07-27
og_description: Hoe je SaveOptions in Aspose.HTML (Python) gebruikt, stelt je in staat
  om grote HTML‑pagina’s te converteren terwijl je resource‑beheer toepast voor schone,
  snelle resultaten.
og_image_alt: Screenshot illustrating how to use SaveOptions in Aspose.HTML for Python
og_title: Hoe SaveOptions te gebruiken in Aspose.HTML – Python-gids
schemas:
- author: Aspose
  dateModified: '2026-07-27'
  description: How to use SaveOptions in Aspose.HTML (Python) to convert large HTML
    page and apply resource handling efficiently.
  headline: How to Use SaveOptions in Aspose.HTML (Python)
  type: TechArticle
- questions:
  - answer: Aspose.HTML follows redirects but won’t send credentials automatically.
      You can pre‑download those assets or use a custom `WebRequest` handler (beyond
      this guide’s scope).
    question: What if the page references resources over HTTPS that require authentication?
  - answer: Yes—set `resource_options.max_handling_depth = 0`. This skips external
      files but leaves any `<style>` blocks intact.
    question: Can I preserve inline CSS while stripping external files?
  - answer: After saving, you can run a secondary pass with Pillow to downscale images,
      or let Aspose.HTML’s built‑in image compression options handle it (use `save_options.image_quality`).
    question: What about very large images that still bloat the output?
  - answer: The limit is global across all resource types (images, scripts, styles).
      If you need granular control, you’d have to filter resources manually after
      loading the document.
    question: Is the depth limit applied per‑resource type?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- HTML processing
title: Hoe SaveOptions te gebruiken in Aspose.HTML (Python)
url: /nl/python/general/how-to-use-saveoptions-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe SaveOptions te gebruiken in Aspose.HTML (Python)

Hoe je SaveOptions in Aspose.HTML voor Python gebruikt, is een vraag die veel ontwikkelaars stellen bij het werken met enorme HTML‑bestanden. Als je een **grote HTML‑pagina wilt converteren** terwijl je nauwkeurig **resource handling** toepast, ben je hier op de juiste plek.  

In deze tutorial lopen we een real‑world scenario door: een omvangrijke HTML‑pagina nemen, beperken hoe diep geneste resources worden opgehaald, en uiteindelijk het resultaat opslaan (of converteren) met kristalheldere controle. Geen vage verwijzingen, maar een volledig, uitvoerbaar voorbeeld dat je vandaag nog kunt kopiëren‑plakken in je project.

> **Pro tip:** Aspose.HTML’s `SaveOptions` werkt niet alleen voor het opslaan als HTML, maar ook voor het converteren naar PDF, PNG of zelfs DOCX. Hetzelfde patroon dat we hieronder behandelen, is van toepassing op al die formaten.

---

## Wat je nodig hebt

- **Python 3.8+** (de code gebruikt type‑hints maar draait op elke recente versie)  
- **Aspose.HTML for Python via .NET** – installeer met `pip install aspose-html`  
- Een **groot HTML‑bestand** dat je wilt verkleinen of transformeren (het voorbeeld gebruikt `big_page.html`)  
- Een bescheiden hoeveelheid schijfruimte voor het uitvoerbestand  

Dat is alles—geen extra libraries, geen zware build‑tools.

---

## Hoe SaveOptions te gebruiken met Resource Handling Options

Dit is de kern van de zaak. We maken een `SaveOptions`‑instantie, koppelen een `ResourceHandlingOptions`‑object dat Aspose.HTML vertelt hoe diep het gekoppelde assets moet volgen, en geven alles door aan de `save`‑methode van het document.

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Load the source HTML document
input_path = "YOUR_DIRECTORY/big_page.html"
doc = HTMLDocument(input_path)

# Define how deep nested resources should be processed (limit to 3 levels)
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # <-- controls depth of resource fetching

# Attach the resource handling configuration to the save options
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# Save the processed document (or convert to another format if desired)
output_path = "YOUR_DIRECTORY/big_page_processed.html"
doc.save(output_path, save_options)
```

**Waarom dit werkt:**  
- `HTMLDocument` laadt het originele bestand en parseert elke `<img>`, `<link>`, `<script>`, enz.  
- `ResourceHandlingOptions.max_handling_depth` vertelt de engine om na drie niveaus van nesting te stoppen met het volgen van resources—perfect om eindeloze lussen te vermijden op pagina’s die andere pagina’s insluiten.  
- `SaveOptions` is het vat dat zowel het uitvoerformaat (standaard HTML) als de resource‑handling‑regels draagt.  
- Ten slotte schrijft `doc.save` het nieuwe bestand, waarbij de zojuist ingestelde regels worden toegepast.

Wanneer je het script uitvoert, zie je een nieuw bestand op `big_page_processed.html`. Open het in een browser; je merkt dat alle afbeeldingen, stijlen en scripts tot drie niveaus diep nog aanwezig zijn, terwijl diepere verwijzingen zijn verwijderd. Dit verkleint de bestandsgrootte drastisch zonder de kernlay-out van de pagina te breken—precies wat je nodig hebt wanneer je een **grote HTML‑pagina wilt converteren** voor offline gebruik of e‑maillevering.

---

## Grote HTML‑pagina efficiënt converteren

Als je doel is om een *grote HTML‑pagina* naar een slankere versie te *converteren*, doet het fragment hierboven al het meeste zware werk. Je wilt echter misschien het uitvoerformaat volledig wijzigen. Aspose.HTML maakt dat met één regel:

```python
# Convert to PDF instead of HTML
pdf_save_options = SaveOptions()
pdf_save_options.resource_handling_options = resource_options
pdf_save_options.format = "PDF"   # specify desired format

doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_save_options)
```

Vervang simpelweg de `format`‑eigenschap door `"PNG"`, `"JPEG"` of `"DOCX"` en je hebt een volledige conversiepijplijn. Dezelfde **apply resource handling**‑regels blijven behouden, zodat de resulterende PDF niet elke externe CSS‑file van de originele site embedt—alleen die binnen de drie‑niveau‑diepte die je hebt gedefinieerd.

---

## Resource Handling toepassen op geneste resources

Laten we iets dieper ingaan op **apply resource handling**. Stel dat je HTML een stylesheet bevat die zelf andere stylesheets importeert, die op hun beurt weer afbeeldingen binnenhalen. Zonder een diepte‑limiet zou Aspose.HTML de keten eindeloos kunnen volgen, waardoor geheugen en CPU onnodig worden belast.

```python
# Example: limit to 1 level for aggressive trimming
resource_options.max_handling_depth = 1
save_options.resource_handling_options = resource_options
doc.save("trimmed_page.html", save_options)
```

- **Diepte 0** – Er worden geen externe resources opgehaald; je krijgt een kale HTML‑skelet.  
- **Diepte 1** – Alleen resources van eerste orde (directe `<img>`‑tags, onmiddellijke CSS‑bestanden) worden meegenomen.  
- **Diepte 2+** – Diepere nesting wordt gerespecteerd, nuttig voor complexe sites waar stijlen afhankelijk zijn van andere stijlen.

Kies de diepte die past bij jouw **convert large HTML page**‑scenario. Voor e‑mailnieuwsbrieven is diepte 1 vaak voldoende. Voor een lokaal archief geeft diepte 3 (zoals in het hoofdvoorbeeld) een mooie balans.

---

## Volledig werkend voorbeeld – Van begin tot eind

Hieronder vind je een zelfstandige script dat je kunt plaatsen in een bestand genaamd `process_html.py`. Het bevat foutafhandeling, logging en een kleine helper die de verkleining van de bestandsgrootte afdrukt.

```python
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

def process_html(
    src_path: str,
    dst_path: str,
    depth: int = 3,
    fmt: str = "HTML"
) -> None:
    """
    Loads an HTML file, applies resource handling, and saves it in the requested format.
    Returns nothing; prints size statistics for quick verification.
    """
    if not os.path.isfile(src_path):
        raise FileNotFoundError(f"Source file not found: {src_path}")

    # Load document
    doc = HTMLDocument(src_path)

    # Set up resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = depth

    # Configure save options (including format)
    save_opts = SaveOptions()
    save_opts.resource_handling_options = res_opts
    save_opts.format = fmt.upper()   # Aspose expects upper‑case format strings

    # Perform save / conversion
    doc.save(dst_path, save_opts)

    # Report size change
    original = os.path.getsize(src_path)
    final = os.path.getsize(dst_path)
    reduction = (original - final) / original * 100
    print(f"Saved {fmt.lower()} to '{dst_path}'. Size reduced by {reduction:.2f}%.")

# -------------------------------------------------------------------------
# Example usage
if __name__ == "__main__":
    input_file = "YOUR_DIRECTORY/big_page.html"
    output_file = "YOUR_DIRECTORY/big_page_processed.html"

    process_html(
        src_path=input_file,
        dst_path=output_file,
        depth=3,          # apply resource handling up to three levels
        fmt="HTML"       # change to "PDF" or "PNG" to convert format
    )
```

**Verwachte output (console):**

```
Saved html to 'YOUR_DIRECTORY/big_page_processed.html'. Size reduced by 42.57%.
```

Open het verwerkte bestand; je ziet een slankere pagina die er nog steeds uitziet als het origineel. Als je `fmt` hebt gewijzigd naar `"PDF"`, zou de console een PDF‑bestandsgrootte rapporteren en kun je het openen in elke PDF‑viewer.

---

## Veelgestelde vragen & randgevallen

- **Wat als de pagina resources over HTTPS verwijst die authenticatie vereisen?**  
  Aspose.HTML volgt redirects maar stuurt geen inloggegevens automatisch. Je kunt die assets vooraf downloaden of een aangepaste `WebRequest`‑handler gebruiken (buiten de scope van deze gids).

- **Kan ik inline CSS behouden terwijl ik externe bestanden verwijder?**  
  Ja—stel `resource_options.max_handling_depth = 0`. Dit slaat externe bestanden over maar laat `<style>`‑blokken intact.

- **Wat als zeer grote afbeeldingen de uitvoer nog steeds oppompen?**  
  Na het opslaan kun je een tweede stap uitvoeren met Pillow om afbeeldingen te verkleinen, of de ingebouwde compressie‑opties van Aspose.HTML gebruiken (gebruik `save_options.image_quality`).

- **Wordt de diepte‑limiet per resource‑type toegepast?**  
  De limiet is globaal over alle resource‑types (afbeeldingen, scripts, stijlen). Als je fijnmazige controle nodig hebt, moet je resources handmatig filteren na het laden van het document.

---

## Conclusie

Je hebt nu een solide begrip van **hoe SaveOptions te gebruiken** in Aspose.HTML


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}