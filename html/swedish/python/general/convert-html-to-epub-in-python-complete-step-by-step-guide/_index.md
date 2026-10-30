---
category: general
date: 2026-07-18
description: Konvertera HTML till EPUB i Python snabbt. Lär dig hur du laddar en HTML‑fil
  i Python och även konverterar HTML till MHTML med enkla bibliotek.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to epub
- load html file in python
- convert html to mhtml
language: sv
lastmod: 2026-07-18
og_description: Konvertera HTML till EPUB i Python med ett tydligt, körbart exempel.
  Lär dig också hur du laddar en HTML‑fil i Python och konverterar HTML till MHTML
  på några minuter.
og_image_alt: Diagram showing convert html to epub workflow
og_title: Konvertera HTML till EPUB i Python – Fullständig handledning
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  headline: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  name: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Python 3.9+** – the syntax used here works on any recent version.'
    text: '**Python 3.9+** – the syntax used here works on any recent version.'
  - name: '**pip** – to install third‑party packages.'
    text: '**pip** – to install third‑party packages.'
  - name: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
    text: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
  type: HowTo
tags:
- python
- html
- epub
- mhtml
- file conversion
title: Konvertera HTML till EPUB i Python – Komplett steg‑för‑steg guide
url: /sv/python/general/convert-html-to-epub-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera HTML till EPUB i Python – Komplett steg‑för‑steg‑guide

Har du någonsin undrat hur man **convert HTML to EPUB** utan att rycka ur håret? Du är inte den enda—utvecklare måste ständigt omvandla webbsidor till e‑böcker för offline‑läsning, och att göra det i Python är förvånansvärt enkelt. I den här handledningen går vi igenom hur man laddar en HTML‑fil i Python, konverterar den HTML‑filen till EPUB, och även hur man omvandlar samma källa till MHTML för e‑post‑vänliga arkiv.

När du är klar med guiden har du ett färdigt skript som tar en enda `sample.html`‑fil och genererar både `sample.epub` och `sample.mhtml`. Inga hemligheter, bara tydlig kod och förklaringar.

---

![Diagram över konverteringspipeline](https://example.com/images/convert-html-epub.png "Diagram som visar arbetsflödet för att konvertera html till epub")

## Vad du kommer att bygga

- **Ladda en HTML‑fil i Python** using the built‑in `pathlib` and `io` modules.  
- **Konvertera HTML till EPUB** with the `ebooklib` library, which handles the EPUB container format for you.  
- **Konvertera HTML till MHTML** (also known as MHT) using the `email` package, creating a single‑file web archive that browsers can open directly.  

Vi kommer också att gå igenom:

- Nödvändiga beroenden och hur man installerar dem.  
- Felhantering så att ditt skript misslyckas på ett kontrollerat sätt.  
- Hur man anpassar metadata som titel och författare för EPUB‑filen.  

Redo? Låt oss dyka ner.

---

## Förutsättningar

Innan vi börjar koda, se till att du har:

1. **Python 3.9+** – syntaxen som används här fungerar på alla moderna versioner.  
2. **pip** – för att installera tredjepartspaket.  
3. En enkel HTML‑fil, t.ex. `sample.html`, placerad i en mapp du har kontroll över.  

Om du redan har dem, bra—hoppa till nästa avsnitt.  

> **Pro tip:** Håll din HTML välformad (korrekta `<head>` och `<body>`‑sektioner). Medan `ebooklib` försöker fixa mindre problem, sparar en ren källa dig huvudvärk senare.

## Steg 1 – Installera de nödvändiga biblioteken

Vi behöver två externa paket:

- **ebooklib** – för EPUB‑generering.  
- **beautifulsoup4** – valfritt, men praktiskt för att rensa HTML innan konvertering.

Kör detta i din terminal:

```bash
pip install ebooklib beautifulsoup4
```

> **Varför dessa bibliotek?** `ebooklib` bygger den ZIP‑baserade EPUB‑strukturen åt dig, hanterar `META‑INF`‑mappen, `content.opf` och `toc.ncx` automatiskt. `beautifulsoup4` låter oss städa upp HTML‑koden, vilket säkerställer att den färdiga e‑boken renderas korrekt i alla läsare.

## Steg 2 – Ladda HTML‑filen i Python

Att ladda en HTML‑fil är enkelt, men vi kommer att paketera det i en liten hjälpfunktion som returnerar ett **BeautifulSoup**‑objekt för senare bearbetning.

```python
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(filepath: str) -> BeautifulSoup:
    """
    Load an HTML file from disk and return a BeautifulSoup object.
    Raises FileNotFoundError if the file does not exist.
    """
    path = Path(filepath)
    if not path.is_file():
        raise FileNotFoundError(f"HTML file not found: {filepath}")

    # Read the file using UTF‑8 encoding (most common for web content)
    html_content = path.read_text(encoding="utf-8")
    # Parse with BeautifulSoup for optional cleaning later
    soup = BeautifulSoup(html_content, "html.parser")
    return soup
```

**Förklaring:**  
- `Path` ger oss OS‑oberoende filhantering.  
- Att använda `read_text` undviker manuellt `open`/`close`‑boilerplate.  
- Att returnera ett `BeautifulSoup`‑objekt betyder att vi senare kan ta bort skript, fixa trasiga taggar eller injicera en stylesheet innan vi **convert HTML to EPUB**.

## Steg 3 – Konvertera HTML till EPUB

Nu när vi kan **load HTML file in Python**, låt oss omvandla den till en ren EPUB. Funktionen nedan accepterar ett `BeautifulSoup`‑objekt, en destinationssökväg och valfri metadata.

```python
import uuid
from ebooklib import epub

def html_to_epub(soup: BeautifulSoup,
                 output_path: str,
                 title: str = "Untitled Book",
                 author: str = "Anonymous") -> None:
    """
    Convert a BeautifulSoup HTML document to an EPUB file.
    """
    # Create a new EPUB book instance
    book = epub.EpubBook()

    # Set basic metadata – this is what shows up in e‑reader libraries
    book.set_identifier(str(uuid.uuid4()))
    book.set_title(title)
    book.set_language('en')
    book.add_author(author)

    # Convert the soup back to a string; we could also clean it here
    html_str = str(soup)

    # Create a chapter (EPUB requires at least one)
    chapter = epub.EpubHtml(title=title,
                            file_name='chap_01.xhtml',
                            lang='en')
    chapter.content = html_str
    book.add_item(chapter)

    # Define the spine (reading order) and table of contents
    book.toc = (epub.Link('chap_01.xhtml', title, 'intro'),)
    book.spine = ['nav', chapter]

    # Add default navigation files
    book.add_item(epub.EpubNcx())
    book.add_item(epub.EpubNav())

    # Write the final EPUB file
    epub.write_epub(output_path, book, {})

    print(f"✅ EPUB created at: {output_path}")
```

**Varför detta fungerar:**  
- `ebooklib.epub.EpubBook` abstraherar ZIP‑behållaren och de nödvändiga manifest‑filerna.  
- Vi genererar ett UUID som identifierare för att undvika dubblett‑ID:n om du skapar många böcker.  
- `spine` talar om för läsare i vilken ordning kapitlen ska visas; en bok med ett enda kapitel räcker för de flesta enkla HTML‑källor.  

**Kör konverteringen:**

```python
if __name__ == "__main__":
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_epub(html_doc,
                 "YOUR_DIRECTORY/sample.epub",
                 title="My Sample eBook",
                 author="Jane Developer")
```

När du kör skriptet kommer du att se en grön bock som bekräftar EPUB‑filens plats.

## Steg 4 – Konvertera HTML till MHTML

MHTML (eller MHT) samlar HTML och alla dess resurser (bilder, CSS) i en enda MIME‑fil. Pythons `email`‑paket kan bygga detta format utan externa beroenden.

```python
import mimetypes
import base64
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email import encoders

def html_to_mhtml(soup: BeautifulSoup,
                  output_path: str,
                  base_url: str = "") -> None:
    """
    Convert a BeautifulSoup HTML document to an MHTML file.
    `base_url` is used to resolve relative resource links.
    """
    # Create the multipart/related container required for MHTML
    mhtml = MIMEMultipart('related')
    mhtml['Subject'] = 'Converted MHTML document'
    mhtml['Content-Type'] = 'multipart/related; type="text/html"'

    # Main HTML part
    html_part = MIMEText(str(soup), 'html', 'utf-8')
    html_part.add_header('Content-Location', 'file://index.html')
    mhtml.attach(html_part)

    # Optional: embed images referenced in the HTML
    for img in soup.find_all('img'):
        src = img.get('src')
        if not src:
            continue

        # Resolve absolute path if needed
        img_path = Path(base_url) / src if base_url else Path(src)
        if not img_path.is_file():
            continue  # skip missing files

        # Guess MIME type; default to octet-stream
        mime_type, _ = mimetypes.guess_type(img_path)
        mime_type = mime_type or 'application/octet-stream'

        with img_path.open('rb') as f:
            img_data = f.read()

        img_part = MIMEBase(*mime_type.split('/'))
        img_part.set_payload(img_data)
        encoders.encode_base64(img_part)
        img_part.add_header('Content-Location', f'file://{src}')
        img_part.add_header('Content-Transfer-Encoding', 'base64')
        mhtml.attach(img_part)

    # Write the MHTML file
    with open(output_path, 'wb') as out_file:
        out_file.write(mhtml.as_bytes())

    print(f"✅ MHTML created at: {output_path}")
```

**Viktiga punkter:**  

- `multipart/related`‑MIME‑typen talar om för webbläsare att HTML‑delen och dess resurser hör ihop.  
- Vi loopar igenom `<img>`‑taggar för att bädda in bilder; om du inte behöver bilder kan du hoppa över det blocket.  
- `Content-Location` använder en `file://`‑URI så att webbläsare kan lösa resurserna internt.  

**Anropa funktionen:**

```python
if __name__ == "__main__":
    # Re‑use the previously loaded soup
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_mhtml(html_doc, "YOUR_DIRECTORY/sample.mhtml", base_url="YOUR_DIRECTORY")
```

Nu har du både `sample.epub` och `sample.mhtml` sida vid sida.

## Fullt skript – Alla steg i en fil

Nedan är det kompletta, färdiga skriptet som kombinerar allt. Spara det som `convert_html.py` och ersätt `YOUR_DIRECTORY` med sökvägen som innehåller din `sample.html`.



## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man konverterar HTML till MHTML med Aspose.HTML för Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [Hur man konverterar EPUB till PDF med Java – med Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [Hur man konverterar EPUB till bilder med Aspose.HTML för Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}