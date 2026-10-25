---
category: general
date: 2026-10-25
description: Scopri come limitare la profondità delle risorse e gestire le risorse
  durante il salvataggio di file HTML di grandi dimensioni usando Python. Segui questa
  guida passo passo per ottenere risultati affidabili.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit resource depth
- apply resource handling
- HTML document processing
- save options Python
- resource handling options
language: it
lastmod: 2026-10-25
og_description: Limita la profondità delle risorse e applica la gestione delle risorse
  durante il salvataggio di HTML con Python. Questo tutorial mostra la soluzione completa
  e funzionante.
og_image_alt: Screenshot illustrating limit resource depth in a Python script
og_title: Limita la profondità delle risorse durante l'applicazione della gestione
  delle risorse – Guida Python
schemas:
- author: GroupDocs
  dateModified: '2026-10-25'
  description: Learn how to limit resource depth and apply resource handling when
    saving large HTML files using Python. Follow this step‑by‑step guide for reliable
    results.
  headline: How to limit resource depth with resource handling options
  type: TechArticle
- description: Learn how to limit resource depth and apply resource handling when
    saving large HTML files using Python. Follow this step‑by‑step guide for reliable
    results.
  name: How to limit resource depth with resource handling options
  steps:
  - name: '**Dynamic content loaded via JavaScript** – The parser only sees static
      HTML. If your page relies on scripts that inject further resources, those will
      never be counted toward the depth limit. Consider pre‑rendering the page with
      a headless browser before applying the limit.'
    text: '**Dynamic content loaded via JavaScript** – The parser only sees static
      HTML. If your page relies on scripts that inject further resources, those will
      never be counted toward the depth limit. Consider pre‑rendering the page with
      a headless browser before applying the limit.'
  - name: '**Circular references** – Some pages include iframes that point back to
      the same page. The depth counter prevents infinite loops, but you may still
      see partially rendered sections. Adjust `max_handling_depth` or manually exclude
      problematic frames.'
    text: '**Circular references** – Some pages include iframes that point back to
      the same page. The depth counter prevents infinite loops, but you may still
      see partially rendered sections. Adjust `max_handling_depth` or manually exclude
      problematic frames.'
  - name: '**Mixed protocols (http/https)** – If resources use different schemes,
      the library may treat them as separate domains. The depth limit still applies
      across protocols, but network permissions might differ. Ensure your environment
      permits both.'
    text: '**Mixed protocols (http/https)** – If resources use different schemes,
      the library may treat them as separate domains. The depth limit still applies
      across protocols, but network permissions might differ. Ensure your environment
      permits both.'
  type: HowTo
tags:
- Python
- HTML
- File handling
title: Come limitare la profondità delle risorse con le opzioni di gestione delle
  risorse
url: /it/python/general/how-to-limit-resource-depth-with-resource-handling-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come limitare la profondità delle risorse con le opzioni di gestione delle risorse

Se hai bisogno di **limitare la profondità delle risorse** durante l'elaborazione di un file HTML enorme, questa guida ti mostra esattamente come farlo. Alla fine del tutorial saprai anche come **applicare la gestione delle risorse** affinché l'operazione di salvataggio rispetti il limite di profondità e eviti elaborazioni incontrollate.

Le pagine HTML di grandi dimensioni spesso incorporano molte risorse esterne—immagini, script, fogli di stile e iframe annidati. Senza un limite di profondità il parser può seguire ogni collegamento, aumentando drasticamente l'uso di memoria e il tempo di elaborazione. La tecnica descritta qui mantiene l'operazione veloce e prevedibile.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Python 3.9+ installato.
* La libreria `groupdocs-viewer` (o una libreria di elaborazione HTML simile) disponibile tramite `pip install groupdocs-viewer`.
* Un file HTML di esempio (`big_page.html`) situato in una directory nota.
* Permessi di scrittura sulla directory di output.

Questi elementi garantiscono che il codice venga eseguito senza configurazioni aggiuntive.

## Passo 1: Caricare il documento HTML sorgente

Il primo passo è creare un'istanza `HTMLDocument` che punti al file originale. L'oggetto rappresenta l'intera struttura HTML e ti dà accesso alle opzioni di salvataggio in seguito.

```python
# Step 1: Load the source HTML document
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

*Perché è importante*: Caricare il file una sola volta fornisce alla libreria un punto di ingresso unico per tutte le operazioni successive. Inoltre verifica che il file esista, generando un errore subito se il percorso è errato.

## Passo 2: Creare le opzioni di gestione delle risorse e limitare la profondità di elaborazione

`ResourceHandlingOptions` ti consente di controllare quanto in profondità la libreria attraverserà le risorse collegate. Impostare `max_handling_depth` a un valore basso (ad es., 5) indica al motore di smettere di seguire i collegamenti dopo cinque livelli di annidamento.

```python
# Step 2: Create resource handling options and limit the processing depth
resource_opts = ResourceHandlingOptions()
resource_opts.max_handling_depth = 5  # Restricts handling to 5 levels deep
```

*Perché è importante*: **Limitando la profondità delle risorse**, impedisci al parser di scaricare ogni immagine, script o iframe che potrebbe essere referenziato indirettamente. Questo riduce il traffico di rete e la pressione sulla memoria, specialmente per pagine che incorporano contenuti di terze parti.

## Passo 3: Collegare le opzioni di risorsa alle opzioni di salvataggio

`SaveOptions` aggrega tutte le impostazioni che influenzano il file di output. Assegnando `resource_handling_options` **applichi la gestione delle risorse** all'operazione di salvataggio imminente.

```python
# Step 3: Attach the resource options to the save options
save_opts = SaveOptions()
save_opts.resource_handling_options = resource_opts
```

*Perché è importante*: L'oggetto `save_opts` funge da contenitore per più flag (compressione, formato, ecc.). Aggiungere `resource_handling_options` garantisce che il limite di profondità sia rispettato durante la fase di scrittura.

## Passo 4: Salvare il documento con la gestione delle risorse limitata

Infine, invoca `doc.save()` con le `save_opts` configurate. Il file di output conterrà solo le risorse che rientrano nella profondità definita.

```python
# Step 4: Save the document with the limited resource handling applied
doc.save("YOUR_DIRECTORY/big_page_limited.html", save_opts)
```

**Risultato atteso**:  
Un nuovo file `big_page_limited.html` appare in `YOUR_DIRECTORY`. Aprilo in un browser; vedrai il layout originale, ma tutte le risorse oltre i cinque livelli di annidamento saranno omesse. La pagina si carica più velocemente e consuma molta meno memoria.

## Verificare l'HTML salvato

Dopo il salvataggio, è buona pratica confermare che il limite di profondità sia stato rispettato.

```python
# Verify that the saved file exists and its size is reasonable
import os

output_path = "YOUR_DIRECTORY/big_page_limited.html"
if os.path.isfile(output_path):
    size_kb = os.path.getsize(output_path) / 1024
    print(f"Saved file size: {size_kb:.2f} KB")
else:
    raise FileNotFoundError("The limited HTML file was not created.")
```

Se la dimensione è drasticamente più piccola rispetto all'originale (che può essere di centinaia di kilobyte), l'impostazione **limitare la profondità delle risorse** ha funzionato come previsto.

## Problemi comuni e come evitarli

| Sintomo | Causa | Correzione |
|---------|-------|------------|
| Nessuna variazione nella dimensione del file | `max_handling_depth` lasciato al valore predefinito (illimitato) | Impostare esplicitamente `resource_opts.max_handling_depth` a un valore < ∞ |
| Immagini mancanti nella pagina | Le risorse erano più profonde del limite | Aumentare la profondità o spostare le risorse critiche a un livello più superficiale |
| `PermissionError` durante il salvataggio | La directory di output è di sola lettura | Scegliere una directory scrivibile o modificare i permessi del sistema operativo |
| Eccezione inattesa `ResourceHandlingException` | Incompatibilità della versione della libreria | Aggiornare all'ultima release di `groupdocs-viewer` (`pip install --upgrade groupdocs-viewer`) |

**Suggerimento**: Inizia con una profondità di 3 per pagine molto grandi e aumentala gradualmente finché la fedeltà visiva soddisfa le tue esigenze.

## Casi limite che potresti incontrare

1. **Contenuto dinamico caricato via JavaScript** – Il parser vede solo HTML statico. Se la tua pagina si affida a script che iniettano ulteriori risorse, queste non verranno conteggiate nel limite di profondità. Considera di pre‑renderizzare la pagina con un browser headless prima di applicare il limite.
2. **Riferimenti circolari** – Alcune pagine includono iframe che puntano alla stessa pagina. Il contatore di profondità impedisce loop infiniti, ma potresti comunque vedere sezioni parzialmente renderizzate. Regola `max_handling_depth` o escludi manualmente i frame problematici.
3. **Protocolli misti (http/https)** – Se le risorse usano schemi diversi, la libreria potrebbe trattarle come domini separati. Il limite di profondità si applica comunque tra i protocolli, ma i permessi di rete potrebbero differire. Assicurati che l'ambiente consenta entrambi.

## Prossimi passi: gestione avanzata delle risorse

Ora che sai **limitare la profondità delle risorse** e **applicare la gestione delle risorse**, potresti voler approfondire:

* **Filtri personalizzati** – Usa `resource_opts.resource_filter` per saltare tipi di file specifici (ad es., video di grandi dimensioni).
* **Impostazioni di compressione** – Combina `SaveOptions` con `compression_level` per ridurre ulteriormente l'output.
* **Elaborazione batch** – Itera su una directory di file HTML, applicando lo stesso limite di profondità a ciascuno.

Queste estensioni ti permettono di costruire una pipeline completa di ottimizzazione HTML per flussi di lavoro su larga scala.

## Conclusione

Hai imparato come **limitare la profondità delle risorse** e **applicare la gestione delle risorse** durante il salvataggio di un grande documento HTML con Python. Configurando `ResourceHandlingOptions` e collegandole a `SaveOptions`, ottieni un controllo fine su quante risorse annidate vengono elaborate, portando a salvataggi più rapidi e file di output più piccoli. Sperimenta con valori di profondità diversi e con ulteriori `SaveOptions` per adattare il comportamento alle esigenze del tuo progetto.

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci alternativi di implementazione nei tuoi progetti.

- [How to Set max_handling_depth in Aspose.HTML Python – Complete Guide](/html/english/python/general/how-to-set-max-handling-depth-in-aspose-html-python-complete/)
- [Create resource handling options and load an HTML document in Python](/html/english/python/general/create-resource-handling-options-and-load-an-html-document-i/)
- [How to Save HTML with Controlled Depth – Step‑by‑Step Python Guide](/html/english/python/general/how-to-save-html-with-controlled-depth-step-by-step-python-g/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}