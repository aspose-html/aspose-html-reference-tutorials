---
category: general
date: 2026-06-10
description: Carica l'HTML da un URL per ottenere rapidamente le icone del sito web.
  Scopri come estrarre i favicon, recuperare gli URL dei favicon del sito e gestire
  i casi particolari in Python.
draft: false
keywords:
- load html from url
- get website icons
- how to extract favicons
- extract favicon urls
- fetch website favicon urls
language: it
og_description: Carica HTML da URL per estrarre le favicon e recuperare gli URL delle
  favicon del sito web. Un tutorial Python passo‑passo per sviluppatori.
og_title: Carica HTML da URL e ottieni le icone del sito – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML from URL to get website icons quickly. Learn how to extract
    favicons, fetch website favicon URLs, and handle edge cases in Python.
  headline: Load HTML from URL and Get Website Icons – Complete Guide
  type: TechArticle
tags:
- web scraping
- favicon extraction
- python
- html parsing
title: Carica HTML da URL e ottieni le icone del sito web – Guida completa
url: /it/python/general/load-html-from-url-and-get-website-icons-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Carica HTML da URL e Ottieni le Icone del Sito – Guida Completa

Ti è mai capitato di **caricare HTML da URL** solo per estrarre il piccolo logo di un sito? Non sei l'unico. Che tu stia costruendo un gestore di segnalibri, una dashboard SEO o semplicemente un progetto personale, ottenere le icone dei siti è un piccolo ma fondamentale tassello del puzzle.

In questo tutorial ti mostreremo **come estrarre i favicon** usando puro Python—senza Selenium pesante, senza magie del browser. Alla fine sarai in grado di **recuperare gli URL dei favicon dei siti**, gestire percorsi relativi e persino prendere più icone se un sito le fornisce. Pronto? Immergiamoci.

## Perché Caricare HTML da URL in Primo Luogo?

Caricare l'HTML grezzo di una pagina ti dà accesso diretto ai tag `<link>` che i browser usano per individuare i favicon. Quei tag di solito hanno questo aspetto:

```html
<link rel="icon" href="/favicon.ico">
<link rel="apple-touch-icon" href="https://example.com/apple-touch-icon.png">
```

Se riesci a estrarre quel markup, puoi leggere programmaticamente l'attributo `href` e scaricare l'immagine da solo. È più veloce che fare screenshot e funziona per qualsiasi sito che segua le convenzioni standard.

## Passo 1 – Carica il Documento HTML da un URL

La prima cosa di cui abbiamo bisogno è un modo per recuperare il sorgente della pagina. La scelta più popolare in Python è la libreria **requests** perché è semplice, affidabile e gestisce i redirect di default.

```python
import requests

def fetch_html(url: str) -> str:
    """
    Retrieve the raw HTML from the given URL.
    Raises an exception if the request fails.
    """
    response = requests.get(url, timeout=10)
    response.raise_for_status()          # Fail fast on HTTP errors
    return response.text
```

> **Suggerimento:** Se lavori dietro un proxy aziendale, passa `proxies=` a `requests.get`. Inoltre, impostare un timeout breve impedisce allo script di bloccarsi su siti inattivi.

Ora possiamo chiamare `fetch_html("https://example.com")` e ottenere una stringa contenente il markup della pagina. Questo è il nucleo del **caricamento HTML da URL**—il resto della pipeline lavora con quella stringa.

## Passo 2 – Ottieni le Icone del Sito

Una volta che abbiamo l'HTML, il passo successivo è individuare ogni elemento `<link>` il cui attributo `rel` menzioni “icon”. Il modulo integrato `html.parser` può fare il lavoro, ma **BeautifulSoup** rende il codice molto più leggibile.

```python
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def extract_icon_links(html: str, base_url: str) -> list[str]:
    """
    Parse the HTML and return a list of absolute URLs pointing to icons.
    Handles relative hrefs by joining them with the page’s base URL.
    """
    soup = BeautifulSoup(html, "html.parser")
    icons = []

    # Look for any <link> tag where rel contains "icon"
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            # Convert relative URLs to absolute ones
            absolute_url = urljoin(base_url, href)
            icons.append(absolute_url)

    return icons
```

Nota come usiamo `urljoin` per trasformare `"/favicon.ico"` in `"https://example.com/favicon.ico"`—un caso comune quando **si ottengono le icone del sito**. Alcuni siti servono icone diverse per dispositivi diversi, quindi potresti ritrovarti con una manciata di URL. Nessun problema; li raccogliamo tutti.

## Passo 3 – Estrai gli URL dei Favicon e Visualizzali

Mettere insieme i pezzi è semplice. Recupereremo l'HTML, eseguiremo l'estrattore e stamperemo la lista risultante. Lo script finale è così:

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def extract_icon_links(html: str, base_url: str) -> list[str]:
    soup = BeautifulSoup(html, "html.parser")
    icons = []
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            icons.append(urljoin(base_url, href))
    return icons

def main():
    target = "https://example.com"
    html = fetch_html(target)
    icon_urls = extract_icon_links(html, target)
    print("Found icon URLs:", icon_urls)

if __name__ == "__main__":
    main()
```

### Output Previsto

Eseguendo lo script su un sito che fornisce un favicon standard potresti ottenere:

```
Found icon URLs: ['https://example.com/favicon.ico']
```

Se il sito fornisce più icone (Apple touch icon, shortcut icon, ecc.), vedrai una lista più lunga:

```
Found icon URLs: [
    'https://example.com/favicon.ico',
    'https://example.com/apple-touch-icon.png',
    'https://example.com/favicon-32x32.png'
]
```

Questo è l’intero workflow di **estrazione degli URL dei favicon**—compatto, con poche dipendenze, e pronto per essere inserito in qualsiasi progetto.

## Gestione delle Insidie più Comuni

| Problema | Perché accade | Soluzione Rapida |
|----------|----------------|------------------|
| **`href` relativo senza tag `<base>`** | `urljoin` assume l'URL della pagina come base, il che funziona nella maggior parte dei casi. | Se esiste un tag `<base href="...">`, leggilo prima e usalo come `base_url`. |
| **Manca `rel="icon"`** | Alcuni siti usano `rel="shortcut icon"` o valori personalizzati. | Estendi la lambda: `rel=lambda r: r and ("icon" in r.lower() or "shortcut" in r.lower())`. |
| **Redirect a un dominio diverso** | Il favicon potrebbe trovarsi su un CDN. | `urljoin` risolverà correttamente il nuovo dominio perché usa l'URL finale della richiesta (`response.url`). |
| **Link interrotti (404)** | L'HTML punta a un file che non esiste più. | Dopo aver estratto gli URL, verifica ciascuno con una richiesta HEAD prima di usarli. |
| **Più tag `<link>` con la stessa icona** | Voci duplicate gonfiano la lista. | Usa `set(icon_urls)` per rimuovere i duplicati prima di restituire. |

## Approfondimento – Recupera gli URL dei Favicon di più Siti in Blocchi

Se devi **recuperare gli URL dei favicon** per un elenco di domini, avvolgi la logica `main` in un ciclo:

```python
domains = ["https://example.com", "https://python.org", "https://github.com"]
for site in domains:
    try:
        icons = extract_icon_links(fetch_html(site), site)
        print(site, "->", icons)
    except Exception as e:
        print(site, "error:", e)
```

Questo schema scala bene, e puoi aggiungere caching (ad esempio con `functools.lru_cache`) per evitare di colpire ripetutamente lo stesso sito.

## Panoramica Visiva

![Load HTML from URL diagram](load-html-url.png)

*Testo alternativo: Diagramma “Carica HTML da URL” che mostra i passaggi fetch → parse → extract.*

L'immagine sopra riassume il processo a tre step: **carica HTML da URL**, **ottieni le icone del sito**, e **estrai gli URL dei favicon**. È utile quando devi spiegare il flusso a un collega.

## Conclusione

Abbiamo percorso una soluzione completa, pronta per la produzione, su come **caricare HTML da URL** e **ottenere le icone del sito** usando solo le librerie Python `requests` e `BeautifulSoup`. Estrarre gli attributi `href` dei tag `<link rel="icon">` ti permette di **estrarre gli URL dei favicon**, gestire percorsi relativi e persino recuperare più formati di icona—tutto in poche decine di righe di codice.

Qual è il prossimo passo? Prova a scaricare le icone in una cartella locale, genera un CSV con le mappature dominio‑favicon, o integra questa logica in un'API Flask che serve i favicon su richiesta. Le possibilità per **recuperare gli URL dei favicon** sono infinite, e la tecnica di base rimane la stessa.

Hai domande su casi particolari, o vuoi condividere un trucco intelligente? Lascia un commento qui sotto—buona caccia alle icone!

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Carica documenti HTML da file in Aspose.HTML per Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Carica documenti HTML da stream con Aspose.HTML per Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Gestisci gli eventi di caricamento del documento in Aspose.HTML per Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}