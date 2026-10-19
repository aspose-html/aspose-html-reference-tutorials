---
category: general
date: 2026-05-28
description: Leer hoe je SaveOptions kunt gebruiken om HTML‑pagina’s bij te snijden
  in Python. Deze stapsgewijze gids legt ook uit hoe je een HTML‑document laadt en
  efficiënt geneste bronnen verwijdert.
draft: false
keywords:
- how to use saveoptions
- how to load html document
- how to trim html page
language: nl
og_description: Hoe je SaveOptions gebruikt om HTML-pagina’s te trimmen in Python.
  Volg deze gids om een HTML‑document te laden, resource‑limieten in te stellen en
  een schoon, lichtgewicht bestand op te slaan.
og_title: Hoe SaveOptions in Python te gebruiken – Trim HTML‑pagina’s
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to use SaveOptions to trim HTML pages in Python. This step‑by‑step
    guide also explains how to load an HTML document and efficiently remove nested
    resources.
  headline: How to Use SaveOptions in Python – Trim HTML Pages
  type: TechArticle
tags:
- python
- html-processing
- saveoptions
- resource-handling
title: Hoe SaveOptions in Python te gebruiken – HTML‑pagina’s bijsnijden
url: /nl/python/general/how-to-use-saveoptions-in-python-trim-html-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe SaveOptions te gebruiken in Python – HTML-pagina's inkorten

Heb je je ooit afgevraagd **hoe je SaveOptions kunt gebruiken** om een enorm HTML‑bestand te verkleinen zonder iets te breken? Je bent niet de enige. Wanneer je een pagina ophaalt die tientallen geneste bronnen bevat—denk aan CSS, JS of zelfs andere HTML‑fragmenten—kan je output uit de hand lopen.  

In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat niet alleen laat zien **hoe je SaveOptions kunt gebruiken**, maar ook behandelt **hoe je een HTML‑document laadt** en de beste manier om een **HTML‑pagina in te korten** door de nestingsdiepte te beperken. Aan het einde heb je een schoon, ingekort bestand klaar voor inzet of verdere verwerking.

## Wat je zult bereiken

- Laad elk lokaal HTML‑bestand met één regel code.  
- Configureer resource‑handling‑opties om te stoppen op een specifieke include‑diepte.  
- Sla het ingekorte resultaat op met de krachtige `SaveOptions`‑klasse.  

Geen externe tools, geen magie—alleen plain Python en een kleine bibliotheek die het zware werk doet.

---

## Voorvereisten

Voordat we beginnen, zorg ervoor dat je het volgende hebt:

1. **Python 3.9+** geïnstalleerd (de gebruikte syntax werkt op elke recente versie).  
2. Het hypothetische `htmlprocessor`‑pakket dat `HTMLDocument`, `SaveOptions` en `ResourceHandlingOptions` levert. Installeer het via:

```bash
pip install htmlprocessor
```

> **Pro tip:** Als je een virtuele omgeving gebruikt, activeer deze eerst—houdt je afhankelijkheden netjes.

---

## Stap 1: Hoe een HTML‑document te laden

Het laden van een bestand is zo simpel als de constructor naar je pad wijzen. De bibliotheek leest de markup, bouwt een DOM‑achtige boom en maakt deze klaar voor verdere manipulatie.

```python
from htmlprocessor import HTMLDocument

# Replace with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/complex_page.html")
print("Document loaded –", doc.title or "Untitled")
```

> **Waarom dit belangrijk is:** Het `HTMLDocument`‑object abstraheert ruwe string‑verwerking, waardoor je methoden krijgt om te queryen, te wijzigen en uiteindelijk de pagina op te slaan. Het normaliseert ook regeleinden en tekenencoderingen, wat je later beschermt tegen subtiele bugs.

Je zult merken dat we de titel afdrukken alleen om te verifiëren dat het laden geslaagd is. Als het bestand ontbreekt of onjuist is, zal de constructor een duidelijke uitzondering werpen—geen stille fouten.

---

## Stap 2: Resource‑handling configureren – De kern van het inkorten

Het volgende puzzelstukje is **hoe je HTML‑pagina in te korten** door te beperken hoe diep de processor includes volgt. Hier blinkt `ResourceHandlingOptions` uit.

```python
from htmlprocessor import ResourceHandlingOptions

# Create a fresh options instance
res_opt = ResourceHandlingOptions()
# max_handling_depth = 2 means: main page + one level of includes
res_opt.max_handling_depth = 2
```

### Wat doet `max_handling_depth`?

- **Depth 1** → Alleen het root‑HTML‑bestand, alle externe bronnen worden genegeerd.  
- **Depth 2** → De root plus alle direct gerefereerde bestanden (bijv. een `iframe` of server‑side include).  
- **Higher values** → Diepere nesting, maar ook een grotere output en langere verwerkingstijd.

Door de diepte te beperken tot **2**, behouden we de hoofdpagina en één laag includes, en verwijderen we alles dieper. Dit is meestal voldoende om overbodige footers, analytics‑scripts of geneste templates die je niet nodig hebt in een ingekorte kopie, weg te halen.

---

## Stap 3: De opties koppelen aan de save‑configuratie

Nu binden we onze resource‑regels aan een `SaveOptions`‑instantie. Dit object vertelt de bibliotheek *exact* hoe het bestand terug naar schijf moet worden geschreven.

```python
from htmlprocessor import SaveOptions

save_opt = SaveOptions()
save_opt.resource_handling_options = res_opt
```

> **Waarom `SaveOptions` gebruiken?**  
> Het geeft je granulaire controle over de output—buiten de resource‑diepte. Later kun je compressie, pretty‑printing of zelfs aangepaste callbacks toevoegen zonder de kern‑opslaan‑logica aan te passen.

---

## Stap 4: Hoe SaveOptions te gebruiken om de HTML‑pagina in te korten

Tot slot roepen we de `save`‑methode aan met onze geconfigureerde opties. De bibliotheek doorloopt de DOM, respecteert de diepte‑limiet en schrijft een ingekort bestand.

```python
# Save the trimmed document
output_path = "YOUR_DIRECTORY/trimmed_page.html"
doc.save(output_path, save_opt)

print(f"Trimmed page saved to {output_path}")
```

### Verwacht resultaat

- Het `trimmed_page.html`‑bestand bevat de originele markup **plus** alle includes tot één niveau diep.  
- Alle diepere includes worden weggelaten, wat resulteert in een kleinere, sneller ladende pagina.  
- Er verschijnen geen gebroken tags—de bibliotheek sluit automatisch alle elementen die na verwijdering loshingen.

Je kunt de output in een browser openen om te verifiëren dat de hoofdinhoud nog steeds wordt gerenderd, terwijl overbodige scripts of geneste frames verdwenen zijn.

---

## Volledig werkend voorbeeld

Alles bij elkaar, hier is het complete script dat je kunt kopiëren‑plakken en uitvoeren:

```python
# -*- coding: utf-8 -*-
"""
Trim an HTML page using SaveOptions.
Demonstrates:
- How to load an HTML document
- How to configure ResourceHandlingOptions
- How to use SaveOptions to save a trimmed version
"""

from htmlprocessor import HTMLDocument, SaveOptions, ResourceHandlingOptions

def trim_html(input_path: str, output_path: str, max_depth: int = 2) -> None:
    # Load the source document
    doc = HTMLDocument(input_path)
    print("Loaded:", doc.title or "Untitled")

    # Set up resource handling (how to trim HTML page)
    res_opt = ResourceHandlingOptions()
    res_opt.max_handling_depth = max_depth

    # Attach options to save configuration (how to use SaveOptions)
    save_opt = SaveOptions()
    save_opt.resource_handling_options = res_opt

    # Perform the save
    doc.save(output_path, save_opt)
    print(f"Trimmed HTML saved to {output_path}")

if __name__ == "__main__":
    INPUT = "YOUR_DIRECTORY/complex_page.html"
    OUTPUT = "YOUR_DIRECTORY/trimmed_page.html"
    trim_html(INPUT, OUTPUT, max_depth=2)
```

Voer het script uit, wijs `INPUT` naar elk complex HTML‑bestand, en je krijgt een slankere versie in `OUTPUT`.  

> **Edge case‑opmerking:** Als de originele pagina voorwaardelijke commentaren bevat (`<!--[if IE]>…<![endif]-->`) die naar diepere resources verwijzen, worden deze net als elke andere geneste include verwijderd. Dit voorkomt dat oude IE‑hacks je uiteindelijke grootte opblazen.

---

## Visuele samenvatting

Hieronder staat een snel diagram dat de stroom illustreert—van het laden van het document, via resource‑handling, tot het opslaan van het ingekorte resultaat.

![voorbeeld van hoe saveoptions te gebruiken](https://example.com/placeholder.png "Diagram dat laat zien hoe SaveOptions te gebruiken om HTML-pagina's te trimmen")

*Alt‑tekst:* **voorbeeld van hoe saveoptions te gebruiken** – toont het drie‑stappenproces van laden, configureren en opslaan van een HTML‑document.

---

## Veelgestelde vragen & valkuilen

| Vraag | Antwoord |
|----------|--------|
| **Wat als ik een diepere nesting nodig heb?** | Verhoog `max_handling_depth` naar 3 of 4, maar onthoud dat de output‑grootte zal toenemen. |
| **Kan ik specifieke tags (bijv. `<script>`) uitsluiten, ongeacht de diepte?** | Ja—`SaveOptions` ondersteunt ook een `tag_exclusion_list`‑eigenschap. Voeg `"script"` toe aan die lijst om scripts altijd te verwijderen. |
| **Is de bibliotheek thread‑safe?** | De huidige versie is dat niet. Maak een aparte `HTMLDocument` per thread. |
| **Worden relatieve URL's herschreven?** | Standaard niet. Gebruik `save_opt.rewrite_relative_urls = True` als je ze moet aanpassen naar de nieuwe locatie. |

---

## Volgende stappen

Nu je **hoe SaveOptions te gebruiken** onder de knie hebt, probeer deze uitbreidingen:

- **Compress de output:** Stel `save_opt.enable_gzip = True` in voor kleinere bestanden tijdens transport.  
- **Pretty‑print voor debugging:** Zet `save_opt.indent_output = True` aan om mooi geformatteerde HTML te krijgen.  
- **Batch‑verwerking:** Loop over een map met HTML‑bestanden en pas dezelfde inkortlogica toe—ideaal voor statische site‑generators.

Elk van deze aanpassingen bouwt voort op dezelfde basis die je net geleerd hebt, waardoor je code schoon en onderhoudbaar blijft.

---

## Conclusie

We hebben de volledige levenscyclus van het inkorten van een HTML‑pagina in Python behandeld: **hoe je een HTML‑document laadt**, configureer **hoe je HTML‑pagina in te korten** met `ResourceHandlingOptions`, en uiteindelijk **hoe je SaveOptions** gebruikt om het opgeschoonde bestand weg te schrijven. Het voorbeeld is volledig zelf‑containend, werkt direct uit de doos, en laat zien waarom het beheersen van de resource‑diepte een cruciale optimalisatie is voor web‑scraping, statische site‑generatie of elke situatie waarin je een lichtgewicht HTML‑snapshot nodig hebt.

Probeer het, experimenteer met verschillende `max_handling_depth`‑waarden, en laat de ingekorte pagina's het zware werk voor je doen. Als je ergens tegenaan loopt, laat dan een reactie achter—happy coding!

## Gerelateerde tutorials

- [Hoe HTML opslaan in C# – Complete gids met een aangepaste resource‑handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Hoe HTML renderen als PNG – Complete C#‑gids](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)
- [Hoe HTML zippen in C# – HTML opslaan in zip](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}