---
category: general
date: 2026-06-04
description: Haal snel tekst uit EPUB en leer hoe je EPUB‑bestanden kunt lezen, EPUB
  naar tekst kunt converteren en hoofdstukken kunt extraheren met Python.
draft: false
keywords:
- get text from epub
- convert epub to text
- how to read epub
language: nl
og_description: Haal tekst uit EPUB met Python in enkele minuten. Deze tutorial laat
  zien hoe je EPUB‑bestanden leest, EPUB naar tekst converteert en veelvoorkomende
  randgevallen afhandelt.
og_title: Tekst uit EPUB halen in Python – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-06-04'
  description: Get text from EPUB quickly and learn how to read EPUB files, convert
    EPUB to text, and extract chapters using Python.
  headline: Get Text from EPUB in Python – Complete Guide
  type: TechArticle
- description: Get text from EPUB quickly and learn how to read EPUB files, convert
    EPUB to text, and extract chapters using Python.
  name: Get Text from EPUB in Python – Complete Guide
  steps:
  - name: Import Libraries and Load the EPUB
    text: '```python from pathlib import Path from ebooklib import epub from bs4 import
      BeautifulSoup'
  - name: Grab the First Chapter (First <section> Element)
    text: '```python # Find the first HTML document inside the EPUB first_item = None
      for item in book.get_items(): if item.get_type() == epub.ITEM_DOCUMENT: first_item
      = item break'
  - name: Strip Tags and Output Plain Text
    text: '```python # .get_text() removes all HTML tags and returns clean text chapter_text
      = first_chapter.get_text(separator="

      ", strip=True)'
  - name: Full Script – Ready to Run
    text: '```python #!/usr/bin/env python3 """ Get text from EPUB – extract the first
      chapter and print it as plain text. """'
  type: HowTo
- questions:
  - answer: Not directly. `.mobi` uses a different container format. Convert it to
      EPUB first (Calibre does a solid job), then apply the same script.
    question: Can I use this with a .mobi file?
  - answer: The fallback to `<body>` (shown in the code) covers that case. You can
      also look for `<div class="chapter">` if the publisher uses custom markup.
    question: What if the EPUB has no `<section>` tags?
  - answer: 'No. Alternatives include `zipfile` + manual HTML parsing, or `pypub`
      for a higher‑level API. `ebooklib` is popular because it abstracts the ZIP handling
      and gives you item types out of the box. --- ## Conclusion You now know how
      to **get text from EPUB** files using Python, whether you need just the'
    question: Is `ebooklib` the only library?
  type: FAQPage
tags:
- python
- epub
- text‑extraction
title: Tekst uit EPUB halen in Python – Complete gids
url: /nl/python/general/get-text-from-epub-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit EPUB halen met Python – Complete Gids

Heb je je ooit afgevraagd **hoe je EPUB‑bestanden** kunt lezen zonder een logische lezer te openen? Misschien moet je het eerste hoofdstuk voor analyse ophalen, of je wilt gewoon **EPUB naar tekst converteren** voor een snelle zoekopdracht. Hoe dan ook, je bent op de juiste plek. In deze tutorial laten we je zien hoe je **tekst uit EPUB haalt** met een paar regels Python, en we leggen ook uit waarom elke stap nodig is zodat je de oplossing kunt aanpassen aan elk boek.

We lopen door het installeren van de juiste bibliotheek, het laden van de EPUB, het extraheren van het eerste `<section>`‑element, en het afdrukken van de platte‑tekstinhoud. Aan het einde heb je een herbruikbaar script dat werkt op elke EPUB die je in een map plaatst.

## Vereisten

- Python 3.8+ (de code gebruikt f‑strings en pathlib)
- Een moderne IDE of gewoon een terminal
- De pakketten `ebooklib` en `beautifulsoup4` (installeren met `pip install ebooklib beautifulsoup4`)

Geen andere externe tools zijn nodig, en het script draait op Windows, macOS en Linux.

---

## Tekst uit EPUB halen – Stap‑voor‑stap

Hieronder staat de kernlogica die precies doet wat de titel belooft: het **halen van tekst uit EPUB** en het afdrukken van het eerste hoofdstuk. We splitsen het op zodat je elke regel begrijpt.

### Stap 1: Bibliotheken importeren en de EPUB laden

```python
from pathlib import Path
from ebooklib import epub
from bs4 import BeautifulSoup

# Path to the .epub file – change this to your own location
EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")

# Load the EPUB container
book = epub.read_epub(EPUB_PATH)
```

*Waarom deze stap?*  
`ebooklib` kent de ZIP‑gebaseerde structuur van EPUB‑bestanden, terwijl `BeautifulSoup` het gemakkelijk maakt om de ingebedde HTML te parseren. Het gebruik van `Path` houdt de code OS‑onafhankelijk.

### Stap 2: Het eerste hoofdstuk pakken (Eerste <section>‑element)

```python
# Find the first HTML document inside the EPUB
first_item = None
for item in book.get_items():
    if item.get_type() == epub.ITEM_DOCUMENT:
        first_item = item
        break

if not first_item:
    raise ValueError("No HTML content found in the EPUB.")

# Parse the HTML with BeautifulSoup
soup = BeautifulSoup(first_item.get_content(), "html.parser")

# Retrieve the first <section> element – this usually holds a chapter
first_chapter = soup.find("section")
if not first_chapter:
    # Fallback: use the first <body> if no <section> exists
    first_chapter = soup.body
```

*Waarom deze stap?*  
EPUB‑bestanden slaan elk hoofdstuk op als een HTML‑bestand. De lus stopt bij het eerste document, dat vaak de omslag of introductie is. Door te richten op de eerste `<section>` gaan we direct naar het eerste echte hoofdstuk, maar we bieden ook een fallback naar het `<body>`‑element voor boeken die geen secties gebruiken.

### Stap 3: Tags verwijderen en platte tekst weergeven

```python
# .get_text() removes all HTML tags and returns clean text
chapter_text = first_chapter.get_text(separator="\n", strip=True)

print(chapter_text)
```

*Waarom deze stap?*  
`get_text()` is de eenvoudigste manier om **EPUB naar tekst te converteren**. Het argument `separator` zorgt ervoor dat elk blok‑element op een nieuwe regel begint, waardoor de output leesbaar is.

### Volledig script – Klaar om uit te voeren

```python
#!/usr/bin/env python3
"""
Get text from EPUB – extract the first chapter and print it as plain text.
"""

from pathlib import Path
from ebooklib import epub
from bs4 import BeautifulSoup

def extract_first_chapter(epub_path: Path) -> str:
    """Return the plain‑text of the first chapter in an EPUB file."""
    book = epub.read_epub(epub_path)

    # Locate the first HTML document
    first_item = next(
        (i for i in book.get_items() if i.get_type() == epub.ITEM_DOCUMENT),
        None,
    )
    if not first_item:
        raise ValueError("The EPUB does not contain any HTML documents.")

    soup = BeautifulSoup(first_item.get_content(), "html.parser")

    # Try to find a <section>; otherwise fall back to <body>
    chapter_tag = soup.find("section") or soup.body
    if not chapter_tag:
        raise ValueError("No readable content found in the first HTML document.")

    # Clean the text
    return chapter_tag.get_text(separator="\n", strip=True)


if __name__ == "__main__":
    # Replace with the actual path to your EPUB file
    EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")
    try:
        text = extract_first_chapter(EPUB_PATH)
        print(text)
    except Exception as e:
        print(f"Error: {e}")
```

Sla dit op als `extract_epub.py` en voer `python extract_epub.py` uit. Als alles correct is ingesteld, zie je de tekst van het eerste hoofdstuk in de console.

![Schermafbeelding van terminaloutput met geëxtraheerde EPUB‑tekst](get-text-from-epub.png "Voorbeeldoutput van tekst uit EPUB")

---

## EPUB naar Tekst Converteren – Opschalen

Het fragment hierboven behandelt één hoofdstuk, maar de meeste projecten hebben het volledige boek als één grote string nodig. Hier is een snelle uitbreiding die door **alle** documentitems loopt, hun opgeschoonde tekst samenvoegt en naar een `.txt`‑bestand schrijft.

```python
def convert_epub_to_text(epub_path: Path, output_path: Path) -> None:
    """Convert an entire EPUB into a plain‑text file."""
    book = epub.read_epub(epub_path)
    all_text = []

    for item in book.get_items():
        if item.get_type() == epub.ITEM_DOCUMENT:
            soup = BeautifulSoup(item.get_content(), "html.parser")
            # Grab everything inside <body> – safe for most EPUBs
            body = soup.body
            if body:
                all_text.append(body.get_text(separator="\n", strip=True))

    output_path.write_text("\n\n".join(all_text), encoding="utf-8")
    print(f"✅ EPUB converted – saved to {output_path}")

# Example usage
if __name__ == "__main__":
    EPUB_PATH = Path("YOUR_DIRECTORY/book.epub")
    TXT_PATH = Path("YOUR_DIRECTORY/book.txt")
    convert_epub_to_text(EPUB_PATH, TXT_PATH)
```

**Pro‑tip:** Sommige EPUB‑bestanden bevatten scripts of style‑tags die `BeautifulSoup` kunnen verwarren. Als je vreemde tekens ziet, voeg dan `soup = BeautifulSoup(item.get_content(), "lxml")` toe en installeer `lxml` voor een strengere parser.

---

## EPUB‑bestanden efficiënt lezen – Veelvoorkomende valkuilen

1. **Verrassende encodering** – EPUB‑bestanden zijn ZIP‑bestanden met UTF‑8 HTML. Als je een `UnicodeDecodeError` krijgt, forceer dan UTF‑8 bij het lezen: `item.get_content().decode("utf-8", errors="ignore")`.
2. **Meerdere talen** – Boeken met gemengde talen kunnen aparte `<section>`‑tags per taal bevatten. Gebruik `soup.find_all("section")` en filter op het `lang`‑attribuut indien nodig.
3. **Afbeeldingen en voetnoten** – Het script verwijdert tags, waardoor alt‑tekst van afbeeldingen verdwijnt. Als je die nodig hebt, extraheer dan de `alt`‑attributen van `<img>` of de voetnoot‑`<a>`‑links vóór het opschonen.
4. **Grote boeken** – Het in het geheugen opslaan van elk hoofdstuk kan RAM doen opraken. Schrijf elk opgeschoond hoofdstuk direct naar een bestand in append‑modus om het geheugen licht te houden.

---

## FAQ – Snelle antwoorden op veelgestelde vragen

**V: Kan ik dit gebruiken met een .mobi‑bestand?**  
A: Niet direct. `.mobi` gebruikt een ander containerformaat. Converteer het eerst naar EPUB (Calibre doet dat prima), en gebruik daarna hetzelfde script.

**V: Wat als de EPUB geen `<section>`‑tags heeft?**  
A: De fallback naar `<body>` (zoals in de code te zien) dekt dat geval. Je kunt ook zoeken naar `<div class="chapter">` als de uitgever aangepaste markup gebruikt.

**V: Is `ebooklib` de enige bibliotheek?**  
A: Nee. Alternatieven zijn `zipfile` + handmatige HTML‑parsing, of `pypub` voor een hoger‑niveau API. `ebooklib` is populair omdat het het ZIP‑beheer abstraheert en je direct item‑types geeft.

---

## Conclusie

Je weet nu hoe je **tekst uit EPUB‑bestanden** kunt halen met Python, of je nu alleen het eerste hoofdstuk nodig hebt of het hele boek. De tutorial behandelde de essentiële stappen om **EPUB naar tekst te converteren**, legde de reden achter elke regel uit, en belichtte randgevallen die je kunt tegenkomen.  

Probeer nu het script uit te breiden om metadata (titel, auteur) te extraheren met `book.get_metadata('DC', 'title')`, of experimenteer met outputformaten zoals Markdown of JSON. Dezelfde principes gelden, zodat je elke vergelijkbare bestands‑parsing‑uitdaging aankunt.

Veel programmeerplezier, en laat gerust een reactie achter als je ergens vastloopt!

## Wat kun je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe EPUB naar PDF converteren met Java – Met Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [EPUB naar afbeeldingen converteren met Aspose HTML voor Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [EPUB naar PDF en afbeeldingen converteren met Aspose.HTML voor Java](/html/english/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}