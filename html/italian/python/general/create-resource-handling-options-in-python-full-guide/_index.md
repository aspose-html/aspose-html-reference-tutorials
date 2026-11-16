---
category: general
date: 2026-07-21
description: Crea opzioni di gestione delle risorse in Python e impara come impostare
  la profondità massima di gestione per l'analisi HTML. Segui questo tutorial passo‑passo
  per una gestione affidabile delle risorse.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: it
lastmod: 2026-07-21
og_description: Crea opzioni di gestione delle risorse in Python e scopri subito come
  impostare la profondità massima di gestione per il caricamento sicuro di documenti
  HTML. Padroneggia la tecnica in pochi minuti.
og_image_alt: Screenshot of Python code that creates resource handling options with
  max handling depth set
og_title: Crea opzioni di gestione delle risorse in Python – Guida completa passo‑passo
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  headline: Create Resource handling options in Python – Full Guide
  type: TechArticle
- description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  name: Create Resource handling options in Python – Full Guide
  steps:
  - name: Circular References
    text: 'Some legacy sites embed an iframe that points back to the original page,
      creating a loop. With `max_handling_depth` set, the loop is automatically broken
      after the third iteration. However, you might still see a warning in the logs.
      To silence noisy logs, adjust the logger level:'
  - name: Missing Resources
    text: 'If a nested resource fails to load (404 or network timeout), the parser
      throws an exception by default. Wrap the loading call in a `try/except` block
      to keep your application alive:'
  - name: Adjusting Depth Dynamically
    text: 'Sometimes you need different depths for different parts of your pipeline.
      Because `resource_options` is a mutable object, you can change `max_handling_depth`
      on the fly:'
  type: HowTo
tags:
- Python
- HTML parsing
- resource management
title: Crea opzioni di gestione delle risorse in Python – Guida completa
url: /it/python/general/create-resource-handling-options-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea opzioni di gestione delle risorse in Python – Guida completa

Ti sei mai chiesto come **creare opzioni di gestione delle risorse** per una pagina HTML enorme senza esaurire la memoria? Non sei il solo. Quando inserisci un documento gigantesco in un parser, le risorse annidate come frame, iframe o CSS collegati possono rapidamente sfuggire di mano.  

La buona notizia? Puoi dire al parser di fermarsi dopo un certo numero di livelli annidati. In questo tutorial ti mostreremo **come impostare la profondità massima di gestione** e mantenere la tua applicazione reattiva. Pronto? Immergiamoci.

## Cosa imparerai

- Perché limitare la profondità di annidamento è importante per le prestazioni e la sicurezza.  
- Il codice esatto necessario per **creare opzioni di gestione delle risorse** usando la classe `ResourceHandlingOptions`.  
- Come configurare `max_handling_depth` affinché il parser si fermi dopo tre livelli.  
- Suggerimenti per gestire casi limite, come documenti con riferimenti circolari o risorse mancanti.  

Non è necessaria alcuna esperienza pregressa con la libreria—basta un'installazione funzionante di Python 3 e una comprensione di base di I/O file.

## Prerequisiti

- Python 3.8+ (la libreria funziona su tutte le versioni recenti).  
- Il pacchetto `htmlparser` che fornisce `HTMLDocument` e `ResourceHandlingOptions`.  
- Un file HTML di esempio (`big_page.html`) collocato in una cartella a cui puoi fare riferimento.  

Se non hai ancora installato il pacchetto, esegui:

```bash
pip install htmlparser
```

Ora che le basi sono coperte, passiamo al nocciolo della questione.

## Crea opzioni di gestione delle risorse – Passo 1

Prima di tutto: ti serve un'istanza di `ResourceHandlingOptions`. Pensala come una cassetta degli attrezzi dove puoi impostare i limiti e le politiche che il parser deve rispettare.

```python
# Step 1: Create resource handling options and limit nesting depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after three levels of nested resources
```

**Perché è importante:**  
Quando il parser incontra un `<iframe>` dentro un altro `<iframe>`, normalmente segue la catena all'infinito. Limitando la profondità a `3`, eviti una ricorsione incontrollata che altrimenti potrebbe esaurire la RAM o provocare un overflow dello stack.  

> **Consiglio esperto:** Se stai analizzando contenuti non attendibili (ad es., HTML caricato dagli utenti), considera di ridurre la profondità a `1` o `2` per mitigare potenziali attacchi.

## Carica il documento HTML – Passo 2

Con l'oggetto delle opzioni pronto, passalo a `HTMLDocument`. Il costruttore rispetterà il valore di `max_handling_depth` che hai appena impostato.

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
```

**Cosa succede dietro le quinte?**  
`HTMLDocument` legge il file, costruisce un albero DOM e poi percorre ogni risorsa esterna (fogli di stile, script, immagini). Ogni volta che incontra una risorsa annidata, controlla `resource_options.max_handling_depth`. Se il limite è raggiunto, il parser registra un avviso e ignora ulteriori annidamenti.  

Ciò significa che ottieni un DOM pienamente utilizzabile per i primi tre livelli, mentre il resto viene ignorato in modo sicuro.

## Verifica la configurazione – Passo 3

È sempre buona pratica confermare che le impostazioni siano effettive. L'oggetto `resource_options` espone il suo stato corrente, quindi puoi stamparlo o verificarlo in un test.

```python
# Step 3: Verify that the max handling depth is set correctly
assert resource_options.max_handling_depth == 3, "Depth limit not applied!"

print(f"Resource handling options configured: max depth = {resource_options.max_handling_depth}")
```

Se l'asserzione passa, puoi essere certo che il parser rispetterà il limite per il resto dell'esecuzione.

## Gestione dei casi limite

### Riferimenti circolari

Alcuni siti legacy incorporano un iframe che punta di nuovo alla pagina originale, creando un loop. Con `max_handling_depth` impostato, il ciclo viene interrotto automaticamente dopo la terza iterazione. Tuttavia potresti comunque vedere un avviso nei log. Per silenziare i log rumorosi, regola il livello del logger:

```python
import logging
logging.getLogger("htmlparser").setLevel(logging.ERROR)
```

### Risorse mancanti

Se una risorsa annidata non riesce a caricarsi (404 o timeout di rete), il parser lancia un'eccezione per impostazione predefinita. Avvolgi la chiamata di caricamento in un blocco `try/except` per mantenere viva l'applicazione:

```python
try:
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
except Exception as e:
    print(f"Failed to load a nested resource: {e}")
    # Fallback: load the document without additional resources
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

### Regolazione dinamica della profondità

A volte occorrono profondità diverse per parti differenti della pipeline. Poiché `resource_options` è un oggetto mutabile, puoi modificare `max_handling_depth` al volo:

```python
resource_options.max_handling_depth = 5   # Temporarily allow deeper nesting
html_doc_deep = HTMLDocument("deep_page.html", resource_options)

resource_options.max_handling_depth = 2   # Tighten for a lightweight preview
html_doc_preview = HTMLDocument("preview.html", resource_options)
```

Ricorda solo di ripristinare il valore prima di riutilizzare la stessa istanza di opzioni in un altro thread.

## Esempio completo funzionante

Di seguito trovi uno script completo che puoi copiare‑incollare, modificare i percorsi dei file e eseguire subito.

```python
import logging
from htmlparser import HTMLDocument, ResourceHandlingOptions

# Optional: Reduce noisy output
logging.getLogger("htmlparser").setLevel(logging.ERROR)

def load_document(path: str, max_depth: int = 3):
    """
    Load an HTML document with a controlled resource handling depth.
    Returns the HTMLDocument instance.
    """
    opts = ResourceHandlingOptions()
    opts.max_handling_depth = max_depth    # How to set max handling depth
    try:
        doc = HTMLDocument(path, opts)
        print(f"Loaded '{path}' with max depth {max_depth}.")
        return doc
    except Exception as exc:
        print(f"Error loading '{path}': {exc}")
        # Fallback to a simple load without resource handling
        return HTMLDocument(path)

if __name__ == "__main__":
    # Example 1: Standard depth
    doc1 = load_document("YOUR_DIRECTORY/big_page.html", max_depth=3)

    # Example 2: Deeper inspection for debugging
    doc2 = load_document("YOUR_DIRECTORY/complex_page.html", max_depth=5)

    # Example 3: Very shallow preview (e.g., thumbnail generation)
    doc3 = load_document("YOUR_DIRECTORY/preview_page.html", max_depth=1)
```

**Output previsto (quando i file esistono e sono ben formati):**

```
Loaded 'YOUR_DIRECTORY/big_page.html' with max depth 3.
Loaded 'YOUR_DIRECTORY/complex_page.html' with max depth 5.
Loaded 'YOUR_DIRECTORY/preview_page.html' with max depth 1.
```

Se un file non può essere letto, vedrai un messaggio di errore invece di un crash.

![Crea opzioni di gestione delle risorse in Python](/images/resource-options.png){alt="Crea opzioni di gestione delle risorse in Python"}

## Riepilogo – Perché questo approccio è fantastico

- **Sicurezza prima di tutto:** Limitare la profondità di annidamento impedisce ricorsioni incontrollate e gonfiamento della memoria.  
- **Flessibilità:** Puoi cambiare `max_handling_depth` a runtime per adattarlo a scenari diversi.  
- **Semplicità:** Pochi righi di codice ti permettono di **creare opzioni di gestione delle risorse** e applicarle immediatamente.  

In sintesi, ora disponi di un modello solido per controllare quanto in profondità il tuo parser segua le risorse esterne.

## Cosa c'è dopo?

- Approfondisci la classe `ResourceHandlingOptions`—ci sono flag per caching, gestione dei timeout e filtraggio dei MIME‑type.  
- Combina il limite di profondità con una stringa `UserAgent` personalizzata per evitare di essere bloccato da server aggressivi.  
- Se lavori con I/O asincrono, dai un'occhiata alla variante `aiohtmlparser` che rispetta le stesse opzioni ma funziona con `asyncio`.  

Sperimenta pure: imposta la profondità a `0` e osserva il parser ignorare ogni riferimento esterno. È un trucco utile quando ti serve solo il markup HTML grezzo.

Hai domande o una pagina ostinata che ancora ti crea problemi? Lascia un commento qui sotto, e sarò felice di aiutarti a perfezionare le impostazioni. Buon parsing!

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Create sandbox for HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}