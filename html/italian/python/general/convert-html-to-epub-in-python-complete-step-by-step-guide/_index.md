---
category: general
date: 2026-07-18
description: Converti HTML in EPUB in Python rapidamente. Scopri come caricare un
  file HTML in Python e anche convertire HTML in MHTML usando librerie semplici.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to epub
- load html file in python
- convert html to mhtml
language: it
lastmod: 2026-07-18
og_description: Converti HTML in EPUB con Python con un esempio chiaro e funzionante.
  Scopri anche come caricare un file HTML in Python e convertire HTML in MHTML in
  pochi minuti.
og_image_alt: Diagram showing convert html to epub workflow
og_title: Converti HTML in EPUB con Python – Tutorial completo
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
title: Converti HTML in EPUB con Python – Guida completa passo passo
url: /it/python/general/convert-html-to-epub-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertire HTML in EPUB con Python – Guida completa passo‑passo

Ti sei mai chiesto come **convertire HTML in EPUB** senza impazzire? Non sei l'unico: gli sviluppatori hanno costantemente bisogno di trasformare pagine web in e‑book per la lettura offline, e farlo in Python è sorprendentemente semplice. In questo tutorial vedremo come caricare un file HTML in Python, convertire quell'HTML in EPUB e persino trasformare la stessa sorgente in MHTML per archivi adatti alle email.

Alla fine della guida avrai uno script pronto all'uso che prende un unico file `sample.html` e genera sia `sample.epub` sia `sample.mhtml`. Nessun mistero, solo codice chiaro e spiegazioni.

---

![Diagramma del flusso di conversione da HTML a EPUB](https://example.com/images/convert-html-epub.png "Diagramma che mostra il flusso di lavoro per convertire html in epub")

## Cosa costruirai

- **Caricare un file HTML in Python** usando i moduli integrati `pathlib` e `io`.  
- **Convertire HTML in EPUB** con la libreria `ebooklib`, che gestisce per te il formato contenitore EPUB.  
- **Convertire HTML in MHTML** (noto anche come MHT) usando il pacchetto `email`, creando un archivio web a file singolo che i browser possono aprire direttamente.  

Tratteremo anche:

- Dipendenze richieste e come installarle.  
- Gestione degli errori affinché lo script fallisca in modo elegante.  
- Come personalizzare i metadati come titolo e autore per il file EPUB.  

Pronti? Immergiamoci.

---

## Prerequisiti

Prima di iniziare a programmare, assicurati di avere:

1. **Python 3.9+** – la sintassi usata qui funziona su qualsiasi versione recente.  
2. **pip** – per installare pacchetti di terze parti.  
3. Un semplice file HTML, ad esempio `sample.html`, posizionato in una cartella di tua scelta.  

Se li hai già, ottimo—passa alla sezione successiva.  

> **Consiglio professionale:** Mantieni il tuo HTML ben formato (sezioni `<head>` e `<body>` corrette). Anche se `ebooklib` cercherà di correggere problemi minori, una sorgente pulita ti eviterà mal di testa in seguito.

---

## Passo 1 – Installa le librerie richieste

Abbiamo bisogno di due pacchetti esterni:

- **ebooklib** – per la generazione di EPUB.  
- **beautifulsoup4** – opzionale, ma utile per pulire l'HTML prima della conversione.

Esegui questo nel terminale:

```bash
pip install ebooklib beautifulsoup4
```

> **Perché queste librerie?** `ebooklib` costruisce la struttura EPUB basata su ZIP per te, gestendo automaticamente la cartella `META‑INF`, `content.opf` e `toc.ncx`. `beautifulsoup4` ci permette di sistemare l'HTML, garantendo che l'e‑book finale venga visualizzato correttamente su tutti i lettori.

---

## Passo 2 – Carica il file HTML in Python

Caricare un file HTML è semplice, ma lo avvolgeremo in una piccola funzione di supporto che restituisce un oggetto **BeautifulSoup** per l'elaborazione successiva.

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

**Spiegazione:**  
- `Path` ci fornisce una gestione dei file indipendente dal sistema operativo.  
- L'uso di `read_text` evita il boilerplate manuale di `open`/`close`.  
- Restituire un oggetto `BeautifulSoup` significa che possiamo in seguito rimuovere script, correggere tag rotti o inserire un foglio di stile prima di **convertire HTML in EPUB**.

---

## Passo 3 – Converti HTML in EPUB

Ora che possiamo **caricare file HTML in Python**, trasformiamolo in un EPUB pulito. La funzione qui sotto accetta un oggetto `BeautifulSoup`, un percorso di destinazione e metadati opzionali.

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

**Perché funziona:**  
- `ebooklib.epub.EpubBook` astrae il contenitore ZIP e i file di manifest richiesti.  
- Generiamo un UUID come identificatore per evitare ID duplicati se crei molti libri.  
- Lo `spine` indica ai lettori l'ordine dei capitoli; un libro a capitolo unico è sufficiente per la maggior parte delle fonti HTML semplici.  

**Esecuzione della conversione:**

```python
if __name__ == "__main__":
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_epub(html_doc,
                 "YOUR_DIRECTORY/sample.epub",
                 title="My Sample eBook",
                 author="Jane Developer")
```

Quando esegui lo script, vedrai un segno di spunta verde che conferma la posizione del file EPUB.

---

## Passo 4 – Converti HTML in MHTML

MHTML (o MHT) raggruppa l'HTML e tutte le sue risorse (immagini, CSS) in un unico file MIME. Il pacchetto `email` di Python può costruire questo formato senza dipendenze esterne.

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

**Punti chiave:**  

- Il tipo MIME `multipart/related` indica ai browser che la parte HTML e le sue risorse appartengono insieme.  
- Iteriamo sui tag `<img>` per incorporare le immagini; se non ti servono le immagini, puoi saltare quel blocco.  
- `Content-Location` utilizza un URI `file://` così i browser possono risolvere le risorse internamente.  

**Chiamata della funzione:**

```python
if __name__ == "__main__":
    # Re‑use the previously loaded soup
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_mhtml(html_doc, "YOUR_DIRECTORY/sample.mhtml", base_url="YOUR_DIRECTORY")
```

Ora hai sia `sample.epub` che `sample.mhtml` affiancati.

---

## Script completo – Tutti i passaggi in un unico file

Di seguito trovi lo script completo, pronto all'uso, che combina tutto. Salvalo come `convert_html.py` e sostituisci `YOUR_DIRECTORY` con il percorso che contiene il tuo `sample.html`.



## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come convertire HTML in MHTML con Aspose.HTML per Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [Come convertire EPUB in PDF con Java – Utilizzando Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [Come convertire EPUB in immagini con Aspose.HTML per Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}