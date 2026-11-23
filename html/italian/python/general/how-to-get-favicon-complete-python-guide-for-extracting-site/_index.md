---
category: general
date: 2026-06-26
description: Scopri come ottenere il favicon caricando l'HTML da un URL ed estraendo
  l'href dai tag link. Codice Python passo‑passo per ottenere rapidamente le icone
  dei siti web.
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: it
og_description: 'Come ottenere rapidamente il favicon: carica l''HTML da un URL, trova
  il link rel=''icon'' ed estrai l''href dai tag link usando Python.'
og_title: Come ottenere la favicon – Tutorial Python
schemas:
- author: Aspose
  dateModified: '2026-06-26'
  description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  headline: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  type: TechArticle
- description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  name: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  steps:
  - name: What if the site uses a `<meta>` tag instead of `<link>`?
    text: Some older pages embed the icon URL in a `<meta name="msapplication‑TileImage">`.
      You can extend `find_icon_links` to also search for those meta tags and treat
      them the same way.
  - name: How do I handle relative URLs that start with `//`?
    text: '`urljoin` automatically resolves protocol‑relative URLs (`//example.com/favicon.ico`)
      based on the scheme of the base URL, so you don’t need extra logic.'
  - name: Can I retrieve multiple sizes (e.g., 32×32, 180×180) automatically?
    text: Yes—just drop the `filter_ico_urls` step. The script will return every icon
      URL it discovers, including PNGs of various dimensions. You can then sort or
      select based on the filename pattern.
  - name: Does this work on sites that block bots?
    text: 'If a site returns a 403 or requires a custom User‑Agent, tweak the `requests.get`
      call:'
  type: HowTo
tags:
- Python
- Web Scraping
- HTML Parsing
title: Come ottenere la favicon – Guida completa in Python per estrarre le icone dei
  siti
url: /it/python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come Ottenere il Favicon – Guida Completa in Python per Estrarre le Icone dei Siti

Ti sei mai chiesto **come ottenere il favicon** da qualsiasi sito web senza dover setacciare manualmente il codice sorgente della pagina? Non sei l'unico: sviluppatori, esperti SEO e persino designer hanno spesso bisogno della piccola icona che rappresenta un sito. In questo tutorial ti mostreremo un metodo pulito, incentrato su Python, per caricare l'HTML da un URL, individuare i tag `<link rel="icon">` e estrarre gli URL delle icone. Alla fine saprai esattamente **come ottenere il favicon** per qualsiasi dominio e avrai a disposizione uno script riutilizzabile per i tuoi progetti.

Copriamo tutto, dal recupero dell'HTML alla gestione di casi particolari come URL relativi e formati di icona multipli. Nessun servizio esterno necessario—solo la libreria standard `requests` e un parser HTML leggero. Pronto a cominciare? Immergiamoci.

## Prerequisiti

- Python 3.8+ installato (il codice funziona anche su 3.10)  
- Familiarità di base con `requests` e le list comprehensions  
- Accesso a Internet per il sito di destinazione  

Se hai già questi requisiti, ottimo—passa al primo passo. Altrimenti, installa l'unica dipendenza necessaria:

```bash
pip install requests beautifulsoup4
```

> **Pro tip:** `beautifulsoup4` è un parser collaudato che rende “caricare html da url” un gioco da ragazzi.

## Passo 1: Caricare l'HTML da URL con Python  

La prima cosa da fare quando si impara **come ottenere il favicon** è scaricare il sorgente della pagina. Questa è la parte “caricare html da url” del processo.

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

Perché usare `requests`? Gestisce i redirect, la verifica HTTPS e i timeout automaticamente, il che significa meno sorprese quando in seguito proverai a **ottenere le icone del sito**.

## Passo 2: Analizzare il Documento e Trovare i Link alle Icone  

Ora che abbiamo l'HTML, dobbiamo individuare tutti gli elementi `<link>` il cui attributo `rel` indica un'icona. Questo è il cuore di **come ottenere il favicon**.

```python
def find_icon_links(html: str) -> list[BeautifulSoup]:
    """Return a list of <link> tags that declare an icon."""
    soup = BeautifulSoup(html, "html.parser")
    # Look for rel="icon" or rel="shortcut icon"
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]
```

Nota che controlliamo sia `icon` sia `shortcut icon` perché i siti più vecchi usano ancora quest'ultimo. Questa piccola sfumatura spesso confonde le persone quando cercano “come estrarre i favicon”.

## Passo 3: Estrarre l'href dagli Elementi Link  

Con i tag pertinenti in mano, il passo logico successivo—**estrarre href dal link**—è semplice.

```python
from urllib.parse import urljoin

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    """Convert each <link> tag’s href into a full absolute URL."""
    urls = []
    for tag in link_tags:
        href = tag.get("href")
        if href:
            # Resolve relative URLs against the base page
            full_url = urljoin(base_url, href)
            urls.append(full_url)
    return urls
```

Usare `urljoin` garantisce che anche se un sito fornisce un percorso relativo come `/favicon.ico`, otterrai un URL assoluto corretto—fondamentale per uno script affidabile di **come ottenere il favicon**.

## Passo 4: Opzionale – Convalidare e Filtrare gli URL delle Icone  

A volte una pagina elenca molte icone (Apple touch icons, PNG di varie dimensioni, ecc.). Se ti interessa solo il classico file `.ico`, filtra di conseguenza. Questo passo mostra **come estrarre i favicon** di un tipo specifico.

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

Sentiti libero di modificare il filtro: sostituisci `".ico"` con `".png"` o controlla `rel="apple-touch-icon"` se ti servono icone ad alta risoluzione.

## Passo 5: Scaricare i File delle Icone (Se Vuoi l'Immagine Effettiva)  

Estrarre gli URL è solo metà del lavoro; scaricarli ti fornisce un file che puoi visualizzare o archiviare. Ecco un piccolo helper:

```python
import os

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    """Save each icon to *folder*, creating it if necessary."""
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")
```

Eseguendo questo dopo i passaggi precedenti otterrai una copia locale di ogni favicon scoperto, perfetta per il caching o l'analisi offline.

## Passo 6: Mettere Tutto Insieme – Esempio Completo Funzionante  

Di seguito trovi lo script completo, pronto all'uso, che dimostra **come ottenere il favicon** da qualsiasi sito. Copia‑incolla, modifica `target_url` e osserva l'output.

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
import os

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def find_icon_links(html: str) -> list[BeautifulSoup]:
    soup = BeautifulSoup(html, "html.parser")
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    return [urljoin(base_url, tag.get("href")) for tag in link_tags if tag.get("href")]

def filter_ico_urls(urls: list[str]) -> list[str]:
    return [u for u in urls if u.lower().endswith(".ico")]

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")

def get_favicons(target_url: str) -> None:
    print(f"Fetching HTML from {target_url} …")
    html = fetch_html(target_url)

    print("Finding <link> tags that declare icons …")
    icon_tags = find_icon_links(html)

    print(f"Extracting href attributes – {len(icon_tags)} candidates found.")
    raw_urls = extract_icon_urls(target_url, icon_tags)

    # Optional filtering – keep only .ico files
    ico_urls = filter_ico_urls(raw_urls)
    print(f"Filtered to {len(ico_urls)} .ico URLs:", ico_urls)

    if ico_urls:
        download_icons(ico_urls)
    else:
        print("No .ico favicons detected; here are all discovered URLs:")
        print(raw_urls)

# Example usage – replace with any site you want to test
if __name__ == "__main__":
    target_url = "https://www.python.org"
    get_favicons(target_url)
```

**Output previsto (troncato per brevità):**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

Se il sito fornisce solo PNG o Apple touch icons, lo script elencherà quegli URL, mostrandoti esattamente **come ottenere il favicon** in ogni scenario.

## Domande Frequenti & Casi Limite  

### E se il sito usa un tag `<meta>` invece di `<link>`?  
Alcune pagine più vecchie incorporano l'URL dell'icona in un `<meta name="msapplication‑TileImage">`. Puoi estendere `find_icon_links` per cercare anche questi meta tag e trattarli allo stesso modo.

### Come gestire URL relativi che iniziano con `//`?  
`urljoin` risolve automaticamente gli URL relativi al protocollo (`//example.com/favicon.ico`) in base allo schema dell'URL di base, quindi non serve logica aggiuntiva.

### Posso recuperare più dimensioni (es. 32×32, 180×180) automaticamente?  
Sì—basta rimuovere il passo `filter_ico_urls`. Lo script restituirà tutti gli URL delle icone che scopre, inclusi PNG di varie dimensioni. Potrai poi ordinarli o selezionarli in base al pattern del nome file.

### Funziona su siti che bloccano i bot?  
Se un sito restituisce un 403 o richiede uno User‑Agent personalizzato, modifica la chiamata `requests.get`:

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

Questa piccola modifica risolve spesso il “come ottenere il favicon” su domini più restrittivi.

## Panoramica Visiva  

![Diagramma che mostra il flusso di come ottenere il favicon da un sito web – carica HTML, analizza i tag link, estrae href, download opzionale](how-to-get-favicon-diagram.png "diagramma del flusso di come ottenere il favicon")

*Il testo alternativo dell'immagine contiene la parola chiave principale, soddisfacendo la SEO per le immagini.*

## Conclusione  

Abbiamo percorso **come ottenere il favicon** passo dopo passo: caricamento dell'HTML da un URL,

## Cosa Dovresti Imparare Dopo?  

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑a‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}