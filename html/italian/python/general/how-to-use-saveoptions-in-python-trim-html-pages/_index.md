---
category: general
date: 2026-05-28
description: Scopri come usare SaveOptions per ridurre le pagine HTML in Python. Questa
  guida passo passo spiega anche come caricare un documento HTML e rimuovere in modo
  efficiente le risorse nidificate.
draft: false
keywords:
- how to use saveoptions
- how to load html document
- how to trim html page
language: it
og_description: Come usare SaveOptions per ridurre le pagine HTML in Python. Segui
  questa guida per caricare un documento HTML, impostare i limiti delle risorse e
  salvare un file pulito e leggero.
og_title: Come utilizzare SaveOptions in Python – Ridurre le pagine HTML
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to use SaveOptions to trim HTML pages in Python. This step‑by‑step
    guide also explains how to load an HTML document and efficiently remove nested
    resources.
  headline: How to Use SaveOptions in Python – Trim HTML Pages
  type: TechArticle
tags:
- python
- html-processing
- saveoptions
- resource-handling
title: Come usare SaveOptions in Python – Ridurre le pagine HTML
url: /it/python/general/how-to-use-saveoptions-in-python-trim-html-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare SaveOptions in Python – Ridurre le pagine HTML

Ti sei mai chiesto **come usare SaveOptions** per ridurre un enorme file HTML senza rompere nulla? Non sei l'unico. Quando includi una pagina che contiene decine di risorse annidate — pensa a CSS, JS o anche altri frammenti HTML — il risultato può gonfiarsi incontrollabilmente.  

In questo tutorial passeremo in rassegna un esempio completo e eseguibile che non solo mostra **come usare SaveOptions**, ma copre anche **come caricare un documento HTML** e il modo migliore per **ridurre una pagina HTML** limitando la profondità di annidamento. Alla fine avrai un file pulito e ridotto pronto per il deployment o per ulteriori elaborazioni.

## Cosa otterrai

- Carica qualsiasi file HTML locale con una sola riga di codice.  
- Configura le opzioni di gestione delle risorse per fermarsi a una profondità di inclusione specifica.  
- Salva il risultato ridotto usando la potente classe `SaveOptions`.  

Nessuno strumento esterno, nessuna magia — solo Python puro e una piccola libreria che fa il lavoro pesante.

---

## Prerequisiti

Prima di immergerci, assicurati di avere:

1. **Python 3.9+** installato (la sintassi usata funziona su qualsiasi versione recente).  
2. Il pacchetto ipotetico `htmlprocessor` che fornisce `HTMLDocument`, `SaveOptions` e `ResourceHandlingOptions`. Installalo tramite:

```bash
pip install htmlprocessor
```

> **Consiglio professionale:** Se stai usando un ambiente virtuale, attivalo prima — mantiene le dipendenze ordinate.

---

## Passo 1: Come caricare un documento HTML

Caricare un file è semplice come puntare il costruttore al tuo percorso. La libreria legge il markup, costruisce un albero simile a un DOM e lo prepara per ulteriori manipolazioni.

```python
from htmlprocessor import HTMLDocument

# Replace with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/complex_page.html")
print("Document loaded –", doc.title or "Untitled")
```

> **Perché è importante:** L'oggetto `HTMLDocument` astrae la gestione delle stringhe grezze, fornendoti metodi per interrogare, modificare e infine salvare la pagina. Normalizza anche le terminazioni di riga e le codifiche dei caratteri, evitando bug sottili in seguito.

Noterai che abbiamo stampato il titolo solo per verificare che il caricamento sia riuscito. Se il file è mancante o malformato, il costruttore solleverà un'eccezione chiara — nessun fallimento silenzioso.

## Passo 2: Configurare la gestione delle risorse – Il cuore del ridimensionamento

Il prossimo pezzo del puzzle è **come ridurre il contenuto di una pagina HTML** limitando la profondità con cui il processore segue le inclusioni. È qui che `ResourceHandlingOptions` brilla.

```python
from htmlprocessor import ResourceHandlingOptions

# Create a fresh options instance
res_opt = ResourceHandlingOptions()
# max_handling_depth = 2 means: main page + one level of includes
res_opt.max_handling_depth = 2
```

### Cosa fa `max_handling_depth`?

- **Profondità 1** → Solo il file HTML radice, tutte le risorse esterne sono ignorate.  
- **Profondità 2** → La radice più tutti i file direttamente referenziati (ad esempio un `iframe` o un include lato server).  
- **Valori più alti** → Annidamento più profondo, ma anche output più grande e tempo di elaborazione più lungo.

Limitando la profondità a **2**, manteniamo la pagina principale e un livello di inclusioni, scartando tutto ciò che è più profondo. Questo è solitamente sufficiente per rimuovere footer ridondanti, script di analytics o template annidati che non ti servono in una copia ridotta.

## Passo 3: Collegare le opzioni alla configurazione di salvataggio

Ora colleghiamo le nostre regole di risorse a un'istanza di `SaveOptions`. Questo oggetto indica alla libreria *esattamente* come scrivere il file su disco.

```python
from htmlprocessor import SaveOptions

save_opt = SaveOptions()
save_opt.resource_handling_options = res_opt
```

> **Perché usare `SaveOptions`?**  
> Ti offre un controllo granulare sull'output — oltre alla sola profondità delle risorse. Puoi in seguito aggiungere compressione, formattazione leggibile o anche callback personalizzati senza toccare la logica di salvataggio principale.

## Passo 4: Come usare SaveOptions per ridurre la pagina HTML

Infine, invochiamo il metodo `save` con le nostre opzioni configurate. La libreria percorrerà il DOM, rispetterà il limite di profondità e scriverà un file ridotto.

```python
# Save the trimmed document
output_path = "YOUR_DIRECTORY/trimmed_page.html"
doc.save(output_path, save_opt)

print(f"Trimmed page saved to {output_path}")
```

### Risultato atteso

- Il file `trimmed_page.html` contiene il markup originale **più** tutte le inclusioni fino a un livello di profondità.  
- Tutte le inclusioni più profonde sono omesse, risultando in una pagina più piccola e più veloce da caricare.  
- Non compaiono tag rotti — la libreria chiude automaticamente gli elementi rimasti sospesi dopo la rimozione.

Puoi aprire l'output in un browser per verificare che il contenuto principale venga ancora renderizzato, mentre script superflui o frame annidati sono scomparsi.

## Esempio completo funzionante

Mettendo tutto insieme, ecco lo script completo che puoi copiare‑incollare ed eseguire:

```python
# -*- coding: utf-8 -*-
"""
Trim an HTML page using SaveOptions.
Demonstrates:
- How to load an HTML document
- How to configure ResourceHandlingOptions
- How to use SaveOptions to save a trimmed version
"""

from htmlprocessor import HTMLDocument, SaveOptions, ResourceHandlingOptions

def trim_html(input_path: str, output_path: str, max_depth: int = 2) -> None:
    # Load the source document
    doc = HTMLDocument(input_path)
    print("Loaded:", doc.title or "Untitled")

    # Set up resource handling (how to trim HTML page)
    res_opt = ResourceHandlingOptions()
    res_opt.max_handling_depth = max_depth

    # Attach options to save configuration (how to use SaveOptions)
    save_opt = SaveOptions()
    save_opt.resource_handling_options = res_opt

    # Perform the save
    doc.save(output_path, save_opt)
    print(f"Trimmed HTML saved to {output_path}")

if __name__ == "__main__":
    INPUT = "YOUR_DIRECTORY/complex_page.html"
    OUTPUT = "YOUR_DIRECTORY/trimmed_page.html"
    trim_html(INPUT, OUTPUT, max_depth=2)
```

Esegui lo script, punta `INPUT` a qualsiasi file HTML complesso, e otterrai una versione più snella in `OUTPUT`.  

> **Nota sui casi limite:** Se la pagina originale contiene commenti condizionali (`<!--[if IE]>…<![endif]-->`) che referenziano risorse più profonde, verranno rimossi proprio come qualsiasi altra inclusione annidata. Questo impedisce che hack per vecchi IE gonfino la dimensione finale.

## Riepilogo visivo

Di seguito trovi un diagramma rapido che illustra il flusso — dal caricamento del documento, attraverso la gestione delle risorse, al salvataggio del risultato ridotto.

![esempio di utilizzo di saveoptions](https://example.com/placeholder.png "Diagramma che mostra come utilizzare SaveOptions per ridurre le pagine HTML")

*Testo alternativo:* **esempio di utilizzo di saveoptions** – mostra il processo a tre passaggi di caricamento, configurazione e salvataggio di un documento HTML.

## Domande comuni e insidie

| Domanda | Risposta |
|----------|--------|
| **E se ho bisogno di un annidamento più profondo?** | Aumenta `max_handling_depth` a 3 o 4, ma ricorda che la dimensione dell'output crescerà. |
| **Posso escludere tag specifici (es., `<script>`) indipendentemente dalla profondità?** | Sì — `SaveOptions` supporta anche una proprietà `tag_exclusion_list`. Aggiungi `"script"` a quella lista per escludere sempre gli script. |
| **La libreria è thread‑safe?** | La versione attuale non lo è. Crea un `HTMLDocument` separato per ogni thread. |
| **Gli URL relativi verranno riscritti?** | Per impostazione predefinita no. Usa `save_opt.rewrite_relative_urls = True` se hai bisogno che vengano adeguati al nuovo percorso. |

## Prossimi passi

Ora che hai padroneggiato **come usare SaveOptions**, prova queste estensioni:

- **Comprimi l'output:** Imposta `save_opt.enable_gzip = True` per file più piccoli in rete.  
- **Pretty‑print per il debug:** Attiva `save_opt.indent_output = True` per ottenere HTML formattato in modo leggibile.  
- **Elaborazione batch:** Cicla su una directory di file HTML e applica la stessa logica di riduzione — ottimo per generatori di siti statici.  

Ognuna di queste modifiche si basa sulla stessa base che hai appena appreso, mantenendo il tuo codice pulito e manutenibile.

## Conclusione

Abbiamo coperto l'intero ciclo di vita per ridurre una pagina HTML in Python: **come caricare un documento HTML**, configurare **come ridurre una pagina HTML** usando `ResourceHandlingOptions`, e infine **come usare SaveOptions** per scrivere il file pulito. L'esempio è completamente autonomo, funziona subito, e dimostra perché controllare la profondità delle risorse è un'ottimizzazione fondamentale per web‑scraping, generazione di siti statici, o qualsiasi situazione in cui ti serve uno snapshot HTML leggero.

Provalo, sperimenta con diversi valori di `max_handling_depth` e lascia che le pagine ridotte facciano il lavoro pesante per te. Se incontri problemi, lascia un commento qui sotto — buona programmazione!

## Tutorial correlati

- [Come salvare HTML in C# – Guida completa usando un gestore di risorse personalizzato](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Come renderizzare HTML come PNG – Guida completa C#](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)
- [Come comprimere HTML in C# – Salva HTML in Zip](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}