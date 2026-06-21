---
category: general
date: 2026-05-31
description: Crea un'istanza di ResourceHandlingOptions per controllare il caricamento
  delle risorse HTML. Scopri come limitare la profondità delle risorse e caricare
  un HTMLDocument con opzioni personalizzate.
draft: false
keywords:
- create resourcehandlingoptions instance
- limit resource depth
- HTMLDocument options
- resource loading configuration
- python html parsing
language: it
og_description: Crea un'istanza di ResourceHandlingOptions per controllare il caricamento
  delle risorse HTML. Questa guida mostra come impostare la profondità massima di
  gestione e caricare un HTMLDocument con opzioni personalizzate.
og_title: Crea un'istanza di ResourceHandlingOptions per il caricamento di HTML
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create ResourceHandlingOptions instance to control HTML resource loading.
    Learn how to limit resource depth and load an HTMLDocument with custom options.
  headline: Create ResourceHandlingOptions Instance for HTML Loading
  type: TechArticle
tags:
- Python
- HTML parsing
- Resource handling
title: Crea un'istanza di ResourceHandlingOptions per il caricamento HTML
url: /it/python/general/create-resourcehandlingoptions-instance-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un'istanza di ResourceHandlingOptions per il caricamento HTML

Ti sei mai chiesto come **creare un'istanza di ResourceHandlingOptions** per evitare che una gigantesca pagina HTML faccia esplodere il tuo parser? Non sei l'unico—documenti di grandi dimensioni con script annidati, frame o includi possono trasformare rapidamente un semplice scraping in un incubo.  

In questo tutorial percorreremo i passaggi esatti per creare un oggetto `ResourceHandlingOptions`, limitare il livello di annidamento e passarne al `HTMLDocument`. Alla fine avrai un modello pulito e ripetibile per la **configurazione del caricamento delle risorse** che funziona con qualsiasi file HTML di dimensioni enormi.

## Cosa Imparerai

- Perché un'istanza di `ResourceHandlingOptions` è importante quando si analizzano pagine massive.  
- Come **limitare la profondità delle risorse** per evitare ricorsioni infinite.  
- La sintassi esatta per caricare un `HTMLDocument` con le tue opzioni personalizzate.  
- Un esempio completo e eseguibile che puoi inserire nel tuo progetto subito.  

**Prerequisiti:** Python 3.8+, la libreria `htmlparser` che fornisce `HTMLDocument` e `ResourceHandlingOptions`. Nessuna altra dipendenza richiesta.

---

## Passo 1: Crea un'istanza di ResourceHandlingOptions

La prima cosa di cui hai bisogno è un nuovo oggetto `ResourceHandlingOptions`. Pensalo come il pannello di controllo per ogni risorsa esterna che il parser potrebbe incontrare—script, immagini, iframe, quello che vuoi.

```python
# Step 1: Initialize the options object
options = ResourceHandlingOptions()
```

> **Perché è importante:** Senza un'istanza esplicita il parser ricade sui valori predefiniti, il che spesso significa “caricare tutto”. Per pagine enormi questo valore predefinito può consumare gigabyte di memoria e bloccare il tuo script.

---

## Passo 2: Limita la profondità delle risorse

Successivamente, indichiamo alle opzioni quanto in profondità vogliamo andare. Impostare `max_handling_depth` a 5, per esempio, ferma il parser dopo cinque livelli di risorse annidate. Regola il numero in base al tuo caso d'uso.

```python
# Step 2: Cap the nesting depth (e.g., stop after 5 levels)
options.max_handling_depth = 5
```

> **Consiglio professionale:** Se ti interessa solo il contenuto di livello superiore, una profondità di 1 o 2 è solitamente sufficiente e velocizza notevolmente il processo.

---

## Passo 3: Carica il documento HTML con le opzioni

Ora passiamo le `options` configurate a `HTMLDocument`. Il costruttore accetta il percorso del file (o l'URL) e l'oggetto delle opzioni, fornendoti un controllo dettagliato su ciò che viene caricato.

```python
# Step 3: Parse the HTML file using the configured options
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
```

> **Ciò che vedrai:** Il parser leggerà `big_page.html`, ma qualsiasi risorsa che farebbe superare la profondità di 5 verrà silenziosamente ignorata. Questo previene ricorsioni incontrollate e mantiene prevedibile l'uso della memoria.

---

## Passo 4: Verifica il risultato (Opzionale ma utile)

È una buona abitudine verificare che il documento sia stato caricato come previsto. Di seguito un rapido controllo di coerenza che stampa il numero di risorse gestite con successo.

```python
# Step 4: Quick verification
print(f"Handled resources: {len(doc.resources)}")
print(f"Document title: {doc.title}")
```

**Output previsto** (i tuoi numeri differiranno in base al file di input):

```
Handled resources: 12
Document title: Example Large Page
```

Se il conteggio è molto più basso di quanto ti aspettassi, potresti dover aumentare `max_handling_depth` o regolare altre proprietà di `ResourceHandlingOptions`.

---

## Variazioni comuni e casi limite

| Situazione | Regolazione |
|-----------|------------|
| **Devi ignorare solo le immagini** | Set `options.ignore_images = True`. |
| **Gli script causano timeout** | Use `options.max_script_execution_time = 2` (seconds). |
| **Analizzare un URL remoto invece di un file** | Pass the URL string to `HTMLDocument` just like a file path. |
| **Vuoi un logger personalizzato** | Assign `options.logger = my_logger` before loading. |

Queste modifiche fanno parte del toolkit delle **opzioni di HTMLDocument** e ti permettono di affinare la **configurazione del caricamento delle risorse** senza riscrivere il tuo parser.

---

## Esempio completo funzionante

Mettendo tutto insieme, ecco uno script autonomo che puoi eseguire subito. Salvalo come `parse_big_page.py` ed eseguilo con `python parse_big_page.py`.

```python
# parse_big_page.py
from htmlparser import HTMLDocument, ResourceHandlingOptions

def main():
    # 1️⃣ Create the options instance
    options = ResourceHandlingOptions()
    
    # 2️⃣ Limit how deep we go into nested resources
    options.max_handling_depth = 5
    
    # Optional: ignore images to speed things up
    # options.ignore_images = True
    
    # 3️⃣ Load the document with our custom options
    doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
    
    # 4️⃣ Verify the load
    print(f"Handled resources: {len(doc.resources)}")
    print(f"Document title: {doc.title}")

if __name__ == "__main__":
    main()
```

Eseguilo e dovresti vedere stampati il conteggio delle risorse e il titolo, confermando che hai creato con successo **un'istanza di ResourceHandlingOptions** e l'hai applicata.

---

## Conclusione

Ti abbiamo appena mostrato come **creare un'istanza di ResourceHandlingOptions**, limitare il livello di annidamento e passarla a un `HTMLDocument`. Questo modello ti fornisce una **configurazione del caricamento delle risorse** affidabile per qualsiasi file HTML di grandi dimensioni, mantenendo il parsing HTML in Python veloce e a consumo di memoria contenuto.

Pronto per il passo successivo? Prova a modificare il limite di profondità, attivare/disattivare `ignore_images` o integrare un logger personalizzato—ogni modifica ti insegnerà di più sulle **opzioni di HTMLDocument** e su come interagiscono con il tuo flusso di dati.

Se hai trovato utile questa guida, sentiti libero di condividerla, mettere una stella al repository o lasciare un commento con i tuoi consigli. Buon parsing!

## Cosa dovresti imparare dopo?

- [Crea HTML da stringa in C# – Guida al gestore di risorse personalizzato](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Come salvare HTML in C# – Guida completa usando un gestore di risorse personalizzato](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Crea Stream Provider in .NET con Aspose.HTML](/html/english/net/advanced-features/create-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}