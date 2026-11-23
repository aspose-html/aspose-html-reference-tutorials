---
category: general
date: 2026-07-18
description: Konvertálja a HTML-t EPUB formátumba Pythonban gyorsan. Tanulja meg,
  hogyan töltsön be HTML-fájlt Pythonban, és hogyan konvertálja a HTML-t MHTML-re
  egyszerű könyvtárak segítségével.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to epub
- load html file in python
- convert html to mhtml
language: hu
lastmod: 2026-07-18
og_description: Konvertálja a HTML-t EPUB formátumba Pythonban egy világos, futtatható
  példával. Tanulja meg, hogyan töltsön be HTML-fájlt Pythonban, és hogyan konvertálja
  a HTML-t MHTML-re percek alatt.
og_image_alt: Diagram showing convert html to epub workflow
og_title: HTML konvertálása EPUB formátumba Pythonban – Teljes útmutató
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
title: HTML konvertálása EPUB formátumba Pythonban – Teljes lépésről‑lépésre útmutató
url: /hu/python/general/convert-html-to-epub-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML konvertálása EPUB formátumba Pythonban – Teljes lépésről‑lépésre útmutató

Gondolkodtál már azon, hogyan **konvertálj HTML‑t EPUB‑ba** anélkül, hogy a hajadba ragadnál? Nem vagy egyedül – a fejlesztőknek folyamatosan szükségük van arra, hogy weboldalakat e‑könyvekké alakítsanak offline olvasáshoz, és Pythonban ez meglepően egyszerű. Ebben a tutorialban végigvezetünk a HTML‑fájl betöltésén Pythonban, a HTML‑ből EPUB‑ba történő konvertáláson, és még azt is megmutatjuk, hogyan alakítsuk ugyanazt a forrást MHTML‑dé, amely e‑mail‑barát archívumként használható.

A útmutató végére egy kész‑futású szkriptet kapsz, amely egyetlen `sample.html` fájlt vesz be, és létrehozza a `sample.epub` és a `sample.mhtml` fájlokat is. Nincs rejtély, csak tiszta kód és magyarázatok.

---

![Conversion pipeline diagram](https://example.com/images/convert-html-epub.png "Diagram showing convert html to epub workflow")

## Mit fogunk létrehozni

- **HTML‑fájl betöltése Pythonban** a beépített `pathlib` és `io` modulok segítségével.  
- **HTML konvertálása EPUB‑ba** az `ebooklib` könyvtárral, amely a EPUB konténerformátumot helyetted kezeli.  
- **HTML konvertálása MHTML‑dé** (más néven MHT) az `email` csomag használatával, egyetlen fájlból álló webarchívumot hozva létre, amelyet a böngészők közvetlenül megnyithatnak.  

Továbbá tárgyaljuk:

- A szükséges függőségek és azok telepítése.  
- Hibakezelés, hogy a szkripted elegánsan kudarcot valljon.  
- Hogyan testreszabhatod a metaadatokat, például a címet és a szerzőt az EPUB‑fájlban.  

Készen állsz? Merüljünk el benne.

---

## Előkövetelmények

Mielőtt elkezdenénk kódolni, győződj meg róla, hogy rendelkezel:

1. **Python 3.9+** – a használt szintaxis bármely friss verzión működik.  
2. **pip** – a harmadik féltől származó csomagok telepítéséhez.  
3. Egy egyszerű HTML‑fájl, például `sample.html`, egy általad kezelt mappában.  

Ha már megvannak ezek, nagyszerű – ugorj a következő szakaszra.  

> **Pro tipp:** Tartsd a HTML‑t jól formázottan (helyes `<head>` és `<body>` szekciókkal). Bár az `ebooklib` megpróbálja kijavítani a kisebb hibákat, egy tiszta forrás később sok fejfájást elkerül.

## 1. lépés – A szükséges könyvtárak telepítése

Két külső csomagra van szükségünk:

- **ebooklib** – EPUB generáláshoz.  
- **beautifulsoup4** – opcionális, de hasznos a HTML tisztításához a konvertálás előtt.

Futtasd a terminálodban:

```bash
pip install ebooklib beautifulsoup4
```

> **Miért ezek a könyvtárak?** Az `ebooklib` felépíti a ZIP‑alapú EPUB struktúrát helyetted, automatikusan kezelve a `META‑INF` mappát, a `content.opf`‑t és a `toc.ncx`‑et. A `beautifulsoup4` segít rendbe tenni a HTML‑t, biztosítva, hogy a végső e‑könyv minden olvasón megfelelően jelenjen meg.

## 2. lépés – HTML‑fájl betöltése Pythonban

A HTML‑fájl betöltése egyszerű, de egy kis segédfüggvénybe csomagoljuk, amely egy **BeautifulSoup** objektumot ad vissza a későbbi feldolgozáshoz.

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

**Magyarázat:**  
- A `Path` OS‑független fájlkezelést biztosít.  
- A `read_text` használata elkerüli a manuális `open`/`close` boilerplate‑t.  
- Egy `BeautifulSoup` objektum visszaadása lehetővé teszi, hogy később eltávolítsuk a szkripteket, javítsuk a hibás tageket, vagy stíluslapot injektáljunk, mielőtt **HTML‑t EPUB‑ba konvertálnánk**.

## 3. lépés – HTML konvertálása EPUB‑ba

Most, hogy **betöltöttük a HTML‑fájlt Pythonban**, alakítsuk át egy tiszta EPUB‑má. Az alábbi függvény egy `BeautifulSoup` objektumot, egy célútvonalat és opcionális metaadatokat fogad.

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

**Miért működik ez:**  
- Az `ebooklib.epub.EpubBook` absztrahálja a ZIP konténert és a szükséges manifest fájlokat.  
- UUID‑t generálunk az azonosítóként, hogy elkerüljük a duplikált ID‑kat, ha sok könyvet hozol létre.  
- A `spine` megmondja az olvasóknak a fejezetek sorrendjét; egy egyfejezetes könyv általában elegendő a legtöbb egyszerű HTML forráshoz.  

**A konvertálás futtatása:**

```python
if __name__ == "__main__":
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_epub(html_doc,
                 "YOUR_DIRECTORY/sample.epub",
                 title="My Sample eBook",
                 author="Jane Developer")
```

A szkript futtatásakor egy zöld pipa jelzi, hogy az EPUB‑fájl hol található.

## 4. lépés – HTML konvertálása MHTML‑dé

Az MHTML (vagy MHT) egyetlen MIME fájlba csomagolja a HTML‑t és minden erőforrását (képek, CSS). A Python `email` csomagja külső függőségek nélkül képes ezt a formátumot előállítani.

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

**Fontos pontok:**  

- A `multipart/related` MIME típus azt jelzi a böngészőknek, hogy a HTML rész és az erőforrások együtt tartoznak.  
- Végigiterálunk a `<img>` tageken, hogy beágyazzuk a képeket; ha nincs szükséged képekre, kihagyhatod ezt a blokkot.  
- A `Content-Location` egy `file://` URI‑t használ, így a böngészők belsőleg feloldják az erőforrásokat.  

**A függvény meghívása:**

```python
if __name__ == "__main__":
    # Re‑use the previously loaded soup
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_mhtml(html_doc, "YOUR_DIRECTORY/sample.mhtml", base_url="YOUR_DIRECTORY")
```

Most már mind a `sample.epub`, mind a `sample.mhtml` fájl egymás mellett áll.

## Teljes szkript – Minden lépés egy fájlban

Az alábbiakban a teljes, kész‑futású szkriptet találod, amely mindent egyesít. Mentsd `convert_html.py` néven, és cseréld le a `YOUR_DIRECTORY`‑t arra az útvonalra, ahol a `sample.html` található.



## Mit érdemes legközelebb megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódpéldákat és lépésről‑lépésre magyarázatokat tartalmaz, hogy elsajátíthasd a további API‑funkciókat, és alternatív megvalósítási megközelítéseket fedezhess fel saját projektjeidben.

- [Hogyan konvertálj HTML‑t MHTML‑dé Aspose.HTML for Java‑val](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [Hogyan konvertálj EPUB‑t PDF‑be Java‑val – Aspose.HTML használatával](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [Hogyan konvertálj EPUB‑t képekké Aspose.HTML for Java‑val](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}