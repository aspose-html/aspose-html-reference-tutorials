---
category: general
date: 2026-07-02
description: Come estrarre le icone da un file HTML usando Python. Impara a leggere
  un file HTML con Python, analizzare il documento HTML ed estrarre l'attributo href
  per ottenere gli URL dei favicon.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: it
og_description: Come estrarre le icone da una pagina HTML usando Python. Questo tutorial
  ti mostra come leggere un file HTML con Python, analizzare il documento e estrarre
  gli URL dei favicon.
og_title: Come estrarre icone da HTML – Guida Python
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to extract icons from an HTML file using Python. Learn to read
    HTML file python, parse HTML document, and extract href attribute to get favicon
    URLs.
  headline: How to Extract Icons from HTML with Python – Complete Guide
  type: TechArticle
- questions:
  - answer: Some sites embed icons via `<meta itemprop="image">`. Extend `is_icon_link`
      to also check for `meta` with `itemprop="image"` and pull its `content` attribute.
    question: What if the HTML uses `<meta>` tags for icons?
  - answer: Yes—just feed each URL into `requests.get(url, stream=True)` and write
      the content to a file. Remember to handle relative URLs with `urljoin`.
    question: Can I fetch the icons automatically?
  - answer: 'Absolutely. Replace the file‑reading step with `requests.get(page_url).text`
      and pass the HTML string to BeautifulSoup. Just be mindful of robots.txt and
      rate limits. --- ## Wrap‑Up We’ve covered **how to extract icons** from any
      static HTML using Python, from reading the file to printing out each f'
    question: Does this work on remote pages?
  type: FAQPage
tags:
- python
- html-parsing
- web‑scraping
- favicon
title: Come estrarre icone da HTML con Python – Guida completa
url: /it/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come estrarre le icone da HTML con Python – Guida completa

Ti sei mai chiesto **come estrarre le icone** da una pagina web senza aprire un browser? Forse stai creando un catalogo di siti, uno strumento di audit SEO, o sei semplicemente curioso delle piccole favicon che appaiono nelle schede. La buona notizia è che puoi farlo in poche righe di Python—senza Selenium, senza Chrome headless, solo con un file HTML di testo.

In questo tutorial vedremo come leggere un file HTML con Python, analizzare il documento HTML e infine **estrarre l'attributo href** dai tag `<link rel="icon">` per ottenere gli URL delle favicon. Alla fine avrai uno snippet riutilizzabile che funziona su qualsiasi HTML statico che gli fornirai, e vedrai anche come gestire casi particolari come percorsi relativi o più dichiarazioni di icona.

## Cosa imparerai

- Caricare un file HTML locale con Python (read html file python)  
- Usare un parser leggero per **parse html document** in modo sicuro  
- Individuare gli elementi `<link>` che dichiarano un'icona  
- **Estrarre i valori dell'attributo href** e trasformarli in URL assoluti  
- Raccogliere e stampare tutti gli **URL delle favicon** scoperti  

Nessun servizio esterno richiesto—solo la libreria standard e il popolare pacchetto **BeautifulSoup**.

---

![Screenshot showing Python script extracting icons – how to extract icons](https://example.com/images/extract-icons-python.png "how to extract icons")

*Image alt text: "how to extract icons using a Python script"*

## Prerequisiti

- Python 3.8+ installato  
- Libreria `beautifulsoup4` (`pip install beautifulsoup4`)  
- Un file HTML locale che vuoi analizzare (ad es., `sample.html`)  

Se hai già tutto questo, tuffiamoci subito.

## Passo 1: Leggere il file HTML con Python – Caricare il documento

Prima di tutto: dobbiamo aprire il file e passare il suo contenuto a un parser. Usare `with open(..., "r", encoding="utf‑8")` garantisce che il file venga chiuso automaticamente, e la codifica UTF‑8 gestisce la maggior parte delle pagine moderne.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**Perché è importante:** Aprire il file con la codifica corretta evita caratteri misteriosi `�` che potrebbero rompere il parser in seguito. Usare `Path` della libreria standard rende il codice cross‑platform.

## Passo 2: Analizzare il documento HTML – Trovare tutti i link alle icone

Ora passiamo l'HTML grezzo a **BeautifulSoup**, che costruisce un albero navigabile. Cercheremo ogni tag `<link>` il cui attributo `rel` contiene la parola `icon`. Nota che `rel` può essere una lista separata da spazi (`rel="shortcut icon"`), quindi serve un controllo flessibile.

```python
# Step 2: Parse the HTML and locate <link> tags that declare an icon
soup = BeautifulSoup(html_content, "html.parser")

def is_icon_link(tag):
    """Return True if a <link> tag declares an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    # BeautifulSoup may return a list or a string; handle both
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

icon_links = [tag for tag in soup.find_all(is_icon_link)]
```

**Perché questo passo è cruciale:** Un semplice `soup.find_all("link", rel="icon")` perderebbe variazioni come `rel="shortcut icon"` o `rel="apple-touch-icon"`. Il nostro helper `is_icon_link` copre questi casi, rendendo l'estrazione robusta.

## Passo 3: Estrarre l'attributo href – Ottenere gli URL

Con i tag rilevanti raccolti, ora estraiamo l'attributo `href` da ciascuno. Alcune pagine potrebbero omettere `href` (raro, ma possibile), quindi controlliamo che non sia `None`. Inoltre, le favicon sono spesso specificate con URL relativi, quindi le risolveremo rispetto all'URL base della pagina se lo conosci. Per un file locale manterremo semplicemente il percorso così com'è.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**Perché rimuoviamo gli spazi:** Gli autori HTML a volte aggiungono spazi intorno agli URL, il che romperebbe una successiva richiesta. Il trimming garantisce stringhe pulite.

## Passo 4: Estrarre gli URL delle favicon – Stampare i risultati

Infine, stampiamo (o restituiamo) la lista degli URL scoperti. In uno script reale potresti scriverli in un CSV, scaricare le icone, o passarli a un altro servizio. Ecco un semplice ciclo che mostra il risultato sulla console.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### Gestione dei casi particolari

- **Valori multipli di rel:** Il nostro controllo `is_icon_link` intercetta già `rel="shortcut icon"` e `rel="apple-touch-icon"`.  
- **Percorsi relativi:** Se in seguito ti servono URL assoluti, usa `urllib.parse.urljoin(base_url, href)`.  
- **Href mancante:** Il controllo `if href:` salta i tag malformati, evitando errori `NoneType`.  
- **Voci duplicate:** Puoi fare `icon_urls = list(dict.fromkeys(icon_urls))` per rimuovere i duplicati.

---

## Script completo – Soluzione tutto‑in‑uno

Mettendo tutto insieme, ecco il programma completo, pronto per l'esecuzione. Salvalo come `extract_icons.py` e imposta `html_path` su qualsiasi file tu voglia analizzare.

```python
#!/usr/bin/env python3
"""
How to extract icons from an HTML file using Python.

This script:
- Reads an HTML file (read html file python)
- Parses the HTML document (parse html document)
- Finds <link> tags with rel containing "icon"
- Extracts the href attribute (extract href attribute)
- Prints each favicon URL (extract favicon urls)
"""

from pathlib import Path
from bs4 import BeautifulSoup

def is_icon_link(tag):
    """Detect <link> tags that declare an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

def extract_favicon_urls(html_path: Path):
    """Return a list of favicon URLs found in the given HTML file."""
    html_content = html_path.read_text(encoding="utf-8")
    soup = BeautifulSoup(html_content, "html.parser")
    icon_links = [t for t in soup.find_all(is_icon_link)]

    urls = []
    for tag in icon_links:
        href = tag.get("href")
        if href:
            urls.append(href.strip())
    # Remove duplicates while preserving order
    return list(dict.fromkeys(urls))

if __name__ == "__main__":
    # Adjust the path to point to your HTML file
    html_file = Path("sample.html")
    favicon_urls = extract_favicon_urls(html_file)

    if not favicon_urls:
        print("No icon links found in the document.")
    else:
        for url in favicon_urls:
            print("Favicon URL:", url)
```

**Output previsto** (supponendo che `sample.html` contenga due icone):

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

Eseguilo con `python extract_icons.py` e vedrai gli URL stampati sulla console.

---

## Domande frequenti

**D: E se l'HTML usa tag `<meta>` per le icone?**  
R: Alcuni siti incorporano icone tramite `<meta itemprop="image">`. Estendi `is_icon_link` per controllare anche `meta` con `itemprop="image"` e estrarre il suo attributo `content`.

**D: Posso scaricare le icone automaticamente?**  
R: Sì—basta passare ogni URL a `requests.get(url, stream=True)` e scrivere il contenuto su file. Ricorda di gestire gli URL relativi con `urljoin`.

**D: Funziona su pagine remote?**  
R: Assolutamente. Sostituisci il passo di lettura del file con `requests.get(page_url).text` e passa la stringa HTML a BeautifulSoup. Fai solo attenzione a robots.txt e ai limiti di velocità.

---

## Conclusioni

Abbiamo coperto **come estrarre le icone** da qualsiasi HTML statico usando Python, dalla lettura del file alla stampa di ogni URL della favicon. Le idee chiave—leggere il file, analizzare il documento, individuare i tag giusti e prelevare l'attributo `href`—sono schemi riutilizzabili che incontrerai in molti compiti di web‑scraping.

Passi successivi? Prova a estendere lo script per:

- Risolvere gli URL relativi rispetto all'URL base della pagina  
- Scaricare ogni icona e salvarla localmente  
- Supportare formati aggiuntivi di icona (`rel="mask-icon"` per Safari)  

Sperimenta pure, e se incontri difficoltà lascia un commento qui sotto. Buon parsing!

## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci alternativi nei tuoi progetti.

- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document to File in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}