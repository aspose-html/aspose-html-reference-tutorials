---
category: general
date: 2026-08-09
description: Leggi rapidamente un documento HTML in Python. Scopri come analizzare
  un file HTML con Python, recuperare HTML da un sito web con Python e come caricare
  HTML in Python con esempi pronti all'uso.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- read html document python
- parse html file python
- how to read html file python
- how to load html in python
- fetch html from website python
language: it
lastmod: 2026-08-09
og_description: Leggi un documento HTML in Python per estrarre dati, analizzare file
  HTML con Python e recuperare HTML da un sito web con Python. Questo tutorial ti
  mostra come caricare HTML in Python usando una piccola classe di supporto.
og_image_alt: Screenshot of Python code loading an HTML file and printing the page
  title
og_title: Leggi documento HTML in Python – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Read HTML document in Python quickly. Learn how to parse html file
    python, fetch html from website python, and how to load html in python with ready‑to‑run
    examples.
  headline: Read HTML document in Python – complete step‑by‑step guide
  type: TechArticle
tags:
- Python
- HTML parsing
- Web scraping
title: Leggi un documento HTML in Python – guida completa passo passo
url: /it/python/general/read-html-document-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Leggi un documento HTML in Python – guida completa passo‑passo

Se hai bisogno di **leggere un documento HTML in Python**, questo tutorial ti mostra esattamente come farlo. Che tu voglia analizzare un file HTML con Python, recuperare HTML da un sito web con Python, o semplicemente caricare HTML in Python per l'estrazione dei dati, la soluzione qui sotto copre tutti gli scenari più comuni.

Concluderai questa guida con un helper `HTMLDocument` riutilizzabile che può caricare HTML da un file locale, da un URL remoto o da una stringa grezza. Non è necessaria alcuna documentazione esterna—basta copiare il codice, eseguirlo e iniziare lo scraping.

## Cosa copre questo tutorial

* Come leggere un documento HTML in Python da tre diverse fonti.  
* Un esempio completo, eseguibile, che include gestione degli errori e rilevamento della codifica.  
* Suggerimenti per analizzare HTML in modo sicuro con **BeautifulSoup** e per gestire i fallimenti di rete.  
* Estensioni come l'estrazione del titolo della pagina, la ricerca di elementi e la personalizzazione del parser.

**Prerequisiti**  
* Python 3.8 o versioni successive.  
* Pacchetti `requests` e `beautifulsoup4` (`pip install requests beautifulsoup4`).  

Ora immergiamoci nell'implementazione.

## Come leggere un documento HTML in Python

Di seguito trovi la classe principale. Determina se l'argomento fornito è un percorso file, un URL o una semplice stringa HTML, quindi crea un oggetto `BeautifulSoup` che puoi interrogare.

```python
# html_document.py
import pathlib
import requests
from bs4 import BeautifulSoup
from urllib.parse import urlparse

class HTMLDocument:
    """
    Helper to load and parse HTML from a file, a URL, or a raw string.
    The instance attribute `soup` holds a BeautifulSoup object ready for querying.
    """

    def __init__(self, source: str):
        """
        Detect the source type and load the HTML accordingly.
        :param source: file path, URL, or raw HTML string.
        """
        self.source = source
        self.html = self._load_source(source)
        # Use the built‑in html.parser for speed; switch to "lxml" if needed.
        self.soup = BeautifulSoup(self.html, "html.parser")

    def _load_source(self, src: str) -> str:
        """Return raw HTML text from the given source."""
        # 1️⃣ Is it a local file?
        if pathlib.Path(src).is_file():
            return self._load_file(src)

        # 2️⃣ Is it a well‑formed URL?
        parsed = urlparse(src)
        if parsed.scheme in ("http", "https"):
            return self._load_url(src)

        # 3️⃣ Otherwise treat it as a literal HTML string.
        return src

    def _load_file(self, path: str) -> str:
        """Read an HTML file from disk, handling common encodings."""
        try:
            with open(path, "r", encoding="utf-8") as f:
                return f.read()
        except UnicodeDecodeError:
            # Fallback to latin‑1 if UTF‑8 fails.
            with open(path, "r", encoding="latin-1") as f:
                return f.read()

    def _load_url(self, url: str) -> str:
        """Fetch HTML from a remote website, raising for HTTP errors."""
        try:
            response = requests.get(url, timeout=10)
            response.raise_for_status()
            # requests guesses the correct encoding; force utf‑8 if unsure.
            response.encoding = response.apparent_encoding or "utf-8"
            return response.text
        except requests.RequestException as exc:
            raise RuntimeError(f"Failed to fetch {url}: {exc}") from exc

    # -----------------------------------------------------------------
    # Convenience helpers ------------------------------------------------
    # -----------------------------------------------------------------
    def title(self) -> str | None:
        """Return the <title> text if present."""
        if self.soup.title:
            return self.soup.title.string.strip()
        return None

    def find(self, *args, **kwargs):
        """Proxy to BeautifulSoup.find – useful for quick queries."""
        return self.soup.find(*args, **kwargs)

    def find_all(self, *args, **kwargs):
        """Proxy to BeautifulSoup.find_all."""
        return self.soup.find_all(*args, **kwargs)
```

**Perché questa classe?**  
* Astrae il problema del *how to read html file python* in un unico oggetto riutilizzabile.  
* Centralizza la gestione degli errori (problemi di codifica del file, timeout di rete) così il tuo codice di scraping rimane pulito.  
* Espone `soup`, permettendoti di usare tutta la potenza di **BeautifulSoup** senza riscrivere boilerplate.

### Esempio di utilizzo

```python
# example.py
from html_document import HTMLDocument

# 1️⃣ Load an HTML document from a local file
doc_from_file = HTMLDocument("samples/index.html")
print("File title:", doc_from_file.title())

# 2️⃣ Load an HTML document directly from a web URL
doc_from_url = HTMLDocument("https://example.com")
print("URL title:", doc_from_url.title())

# 3️⃣ Load an HTML document from an HTML string
html_content = "<html><body><h1>Hello, world!</h1></body></html>"
doc_from_string = HTMLDocument(html_content)
print("String title:", doc_from_string.title())   # None – no <title> tag
```

**Output previsto**

```
File title: Sample Index Page
URL title: Example Domain
String title: None
```

Lo script dimostra tutti e tre i modi per **load html in python** e stampa il titolo della pagina quando disponibile.

## Analizzare un file HTML in Python

Una volta ottenuto `doc_from_file.soup`, puoi interrogare qualsiasi elemento. Di seguito una rapida illustrazione dell'estrazione di tutti i collegamenti ipertestuali:

```python
# Extract all <a> tags and their href attributes
links = doc_from_file.find_all("a")
for link in links:
    href = link.get("href")
    text = link.get_text(strip=True)
    print(f"Link text: {text} → {href}")
```

**Perché analizzare html file python?**  
L'analisi ti consente di trasformare markup non strutturato in dati strutturati che puoi memorizzare, analizzare o inviare ad altri sistemi. L'API di BeautifulSoup rende questo semplice, e il wrapper `HTMLDocument` garantisce che tu parta sempre da un oggetto soup pulito.

## Caricare HTML da un URL in Python

Recuperare una pagina remota è spesso il primo passo di una pipeline di web‑scraping. L'helper esegue automaticamente:

* Imposta un timeout (10 secondi) per evitare script bloccati.  
* Genera un'eccezione chiara se lo stato HTTP non è 200.  
* Rileva la codifica dei caratteri corretta.

Se devi personalizzare la richiesta (header, autenticazione, proxy), modifica il metodo `_load_url`:

```python
def _load_url(self, url: str) -> str:
    headers = {"User-Agent": "MyScraper/1.0 (+https://mydomain.com)"}
    response = requests.get(url, headers=headers, timeout=10)
    response.raise_for_status()
    response.encoding = response.apparent_encoding or "utf-8"
    return response.text
```

**Come recuperare html from website python in modo efficiente?**  
* Usa uno `User-Agent` realistico.  
* Rispetta `robots.txt` e limita la frequenza delle richieste.  
* Cache le risposte localmente se prevedi di visitare spesso la stessa pagina.

## Creare un HTMLDocument da una stringa

A volte hai già del markup grezzo—forse generato da un motore di template o ricevuto da un'API. Passare direttamente la stringa evita I/O non necessario:

```python
html_snippet = """
<div class="product">
    <h2>Widget</h2>
    <p class="price">$19.99</p>
</div>
"""
doc = HTMLDocument(html_snippet)
price = doc.find("p", class_="price").get_text(strip=True)
print("Extracted price:", price)   # → Extracted price: $19.99
```

**Quando usare questo pattern?**  
* Testare unitariamente i parser senza toccare la rete.  
* Analizzare corpi di email o risposte API che incorporano HTML.  

## Problemi comuni e migliori pratiche

| Problema | Perché è importante | Correzione consigliata |
|----------|---------------------|------------------------|
| **Codifica errata** | Appaiono caratteri illeggibili quando il file non è UTF‑8. | Usa un fallback (`latin-1`) o lascia che `requests` indovini la codifica (`apparent_encoding`). |
| **Manca `<title>`** | `doc.title()` restituisce `None`, il che può causare `AttributeError` se si assume una stringa. | Controlla sempre `None` prima di usare il risultato. |
| **Timeout di rete** | Gli script possono rimanere bloccati indefinitamente su server lenti. | Imposta un timeout (`requests.get(..., timeout=10)`) e cattura `requests.RequestException`. |
| **Contenuto dinamico** | HTML generato da JavaScript non sarà presente nella risposta grezza. | Usa un browser headless come Selenium o Playwright per il rendering. |
| **Pagine molto grandi** | Analizzare HTML di grandi dimensioni può consumare molta memoria. | Streamma la risposta (`requests.get(..., stream=True)`) e analizza incrementale se possibile. |

## Esempio completo funzionante

Salva i due file (`html_document.py` e `example.py`) nella stessa cartella, installa le dipendenze e avvia:

```bash
pip install requests beautifulsoup4
python example.py
```

Dovresti vedere i titoli stampati, seguiti da eventuali dati aggiuntivi che interroghi. Il codice funziona su Windows, macOS e Linux con qualsiasi interprete Python recente.

## Conclusione

Ora sai **come leggere un documento HTML in Python** usando una classe compatta `HTMLDocument` che supporta la lettura da file, URL e stringhe grezze.

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document to File in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}