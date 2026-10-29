---
category: general
date: 2026-07-05
description: Open links in een nieuw tabblad met Python – leer hoe je target='_blank'
  toevoegt, de linkdoel verandert, een attribuut‑bevat selector gebruikt, en gemodificeerde
  HTML moeiteloos opslaat.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: nl
og_description: Open links snel in een nieuw tabblad. Deze tutorial laat zien hoe
  je target='_blank' toevoegt, het linkdoel wijzigt en de aangepaste HTML opslaat
  met Python.
og_title: Open links in nieuw tabblad – Stapsgewijze HTML‑updatengids
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: Open links in een nieuw tabblad – Complete gids voor het bijwerken van HTML‑ankers
url: /nl/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Open Links New Tab – Complete gids voor het bijwerken van HTML-ankers

Ooit nodig gehad om **open links new tab** op een statische HTML-pagina, maar wist je niet waar te beginnen? Je bent niet de enige. Veel ontwikkelaars lopen tegen dit probleem aan bij het opschonen van legacy-sites of het toevoegen van toegankelijkheidsaanpassingen. In deze tutorial lopen we een praktische oplossing door die **adds target blank**, **changes link target**, en veilig **saves modified html**—alles met een paar regels Python.

We zullen ook behandelen hoe je een **attribute contains selector** kunt gebruiken zodat je alleen de ankers aanraakt waar je echt om geeft (bijvoorbeeld elke link die naar *example.com* wijst). Aan het einde heb je een herbruikbaar script dat je in elk project kunt plaatsen, ongeacht de grootte.

## Wat je zult leren

- Laad een HTML‑bestand in een manipuleerbaar documentobject.  
- Selecteer `<a>`‑elementen waarvan het `href`‑attribuut een specifieke substring bevat.  
- **Add target blank** en stel het `rel="noopener"`‑attribuut in om de beveiliging te verbeteren.  
- **Save modified html** terug naar schijf zonder opmaak te verliezen.  

Geen externe afhankelijkheden buiten de standaardbibliotheek en **beautifulsoup4** (een kleine installatie). Als je al een andere parser gebruikt, vertalen de concepten direct.

---

## Vereisten

- Python 3.8+ geïnstalleerd op je machine.  
- Basiskennis van HTML en Python.  
- `beautifulsoup4`‑pakket (`pip install beautifulsoup4`).  

Dat is alles—geen zware frameworks nodig.

---

## Stap 1: Laad het HTML‑document

Eerst en vooral: we moeten het bronbestand lezen en het aan BeautifulSoup geven. Beschouw dit als het openen van een leeg canvas waarop je nieuwe attributen kunt tekenen.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Waarom dit belangrijk is:** Het gebruik van `Path` houdt de code OS‑agnostisch, en `html.parser` is ingebouwd, zodat je geen extra parsers nodig hebt voor eenvoudige taken.

---

## Stap 2: Gebruik een attribute contains selector om de juiste links te vinden

We willen alleen ankers aanraken die naar *example.com* wijzen. De CSS‑selector `a[href*='example.com']` doet precies dat—`*=` betekent “bevat”. De `select`‑methode van BeautifulSoup begrijpt deze syntaxis.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Pro tip:** Als je een hoofdletter‑ongevoelige overeenkomst nodig hebt, schakel dan over naar een kleine lus die controleert `if 'example.com' in a.get('href', '').lower()`.

Nu bevat `anchor_elements` elke link waar we om geven, klaar voor de volgende transformatie.

---

## Stap 3: Linkdoel wijzigen – Add Target Blank en beveilig de link

Een link in een nieuw tabblad openen is zo simpel als het instellen van `target="_blank"`. Moderne browsers raden echter aan ook `rel="noopener"` (of `noreferrer`) toe te voegen om te voorkomen dat de nieuw geopende pagina toegang krijgt tot het oorspronkelijke venster via `window.opener`. Deze kleine beveiligingsaanpassing kan phishing‑aanvallen stoppen.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Waarom we directe dictionary‑toewijzing gebruiken:** Het maakt het attribuut automatisch aan als het ontbreekt, en overschrijft het als het al bestaat—perfect voor een **change link target**‑operatie.

---

## Stap 4: Sla gewijzigde HTML op naar schijf

De laatste stap is om de bijgewerkte markup naar een nieuw bestand te schrijven. Het origineel ongemoeid laten stelt je in staat terug te gaan als er iets misgaat.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **Wat `prettify()` doet:** Het formatteert de HTML met nette inspringing, waardoor het opgeslagen bestand later makkelijker te lezen en te vergelijken is. Als je de oorspronkelijke witruimte wilt behouden, vervang dan `prettify()` door `str(soup)`.

---

## Volledig script – One‑Click‑oplossing

Hieronder staat het volledige, kant‑klaar script. Sla het op als `update_links.py` en voer `python update_links.py` uit vanuit je terminal.

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### Verwacht resultaat

Stel dat `links.html` oorspronkelijk bevatte:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Na het uitvoeren van het script zal `links-updated.html` er als volgt uitzien:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Alleen de link naar *example.com* kreeg de **add target blank**‑attributen, wat aantoont dat onze **attribute contains selector** precies werkte zoals bedoeld.

---

## Veelgestelde vragen & randgevallen

### Wat als een link al een `rel`‑attribuut heeft?

Onze lus overschrijft het met `"noopener"`. Als je bestaande waarden wilt behouden (bijv. `"nofollow"`), concateneer dan in plaats daarvan:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### Hoe meerdere domeinen afhandelen?

Breid gewoon de selector‑lijst uit:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### Verandert `prettify()` de oorspronkelijke HTML‑structuur?

Het herindenteert, maar verandert de volgorde van tags of attribuutwaarden niet. Als je de exacte oorspronkelijke witruimte moet behouden, vervang dan `prettify()` door `str(soup)` zoals eerder vermeld.

---

## Pro‑tips voor productie‑klare scripts

- **Backup before overwriting:** Voeg een kopiestap toe (`shutil.copy`) om het originele bestand veilig te houden.  
- **Logging instead of print:** Gebruik de `logging`‑module voor schaalbare projecten.  
- **Batch processing:** Loop over een map met `Path.rglob("*.html")` om veel bestanden in één keer bij te werken.  

Deze aanpassingen maken van een eenvoudig **open links new tab**‑script een robuuste tool voor elke web‑onderhouds‑workflow.

---

## Conclusie

Je hebt nu een solide, herbruikbare methode om **open links new tab** toe te passen op elke statische HTML‑collectie. Door een **attribute contains selector** te gebruiken, kun je **change link target** precies daar waar je het nodig hebt, **add target blank**, en **save modified html** zonder opmaak te verliezen.

Probeer het op een testpagina, en schaal het vervolgens op je hele site. Moet je de selector aanpassen voor PDF’s, of andere domeinen? Pas gewoon de CSS‑string aan—alles andere blijft hetzelfde.

Voel je vrij om een reactie achter te laten als je tegen eigenaardigheden aanloopt, of deel hoe je het script hebt uitgebreid voor je eigen projecten. Veel plezier met coderen, en moge al je ankers precies openen waar je ze wilt!

---

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe HTML bewerken met Aspose.HTML voor Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Hoe CSS toevoegen – Inline CSS aan HTML‑documenten in Aspose.HTML voor Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}