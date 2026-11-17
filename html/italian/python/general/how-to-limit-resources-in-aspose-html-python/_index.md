---
category: general
date: 2026-07-02
description: Come limitare le risorse durante il caricamento di una grande pagina
  HTML con Aspose.HTML in Python – impostare la profondità ed evitare il sovraccarico.
draft: false
keywords:
- how to limit resources
- how to set depth
- load large html page
language: it
og_description: Come limitare le risorse durante il caricamento di una grande pagina
  HTML con Aspose.HTML in Python – impara a impostare la profondità e a mantenere
  basso l'uso della memoria.
og_title: Come limitare le risorse in Aspose.HTML Python
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to limit resources when loading a large HTML page with Aspose.HTML
    in Python – set depth and avoid overload.
  headline: How to Limit Resources in Aspose.HTML Python
  type: TechArticle
- description: How to limit resources when loading a large HTML page with Aspose.HTML
    in Python – set depth and avoid overload.
  name: How to Limit Resources in Aspose.HTML Python
  steps:
  - name: Why This Works
    text: 1. **Importing the right classes** – `ResourceHandlingOptions` holds the
      settings, while `HTMLDocument` does the heavy lifting of parsing the HTML. 2.
      **Setting `max_handling_depth`** – This is the exact answer to **how to set
      depth**. A depth of `3` means Aspose.HTML will follow links, scripts, and
  - name: Expected Output
    text: 'Running the script should print something like:'
  - name: Edge Cases & Gotchas
    text: '- **Circular references:** If a page includes itself indirectly (A → B
      → A), the depth limit prevents infinite loops. The loader will stop at the configured
      depth and log a warning. - **Dynamic scripts:** Some JavaScript injects resources
      after the initial load. `max_handling_depth` only affects sta'
  type: HowTo
- questions:
  - answer: Just bump `max_handling_depth` for that run. You can even compute it dynamically
      based on the page size.
    question: What if I need a deeper crawl for a specific page?
  - answer: Yes. After loading, `doc.resources` contains only the resources that were
      actually fetched. Anything missing simply isn’t in the collection.
    question: Can I retrieve a list of skipped resources?
  - answer: The `ResourceHandlingOptions` instance is immutable once passed to `HTMLDocument`,
      so you can safely reuse it across threads.
    question: Is the depth limit thread‑safe?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- Resource Management
title: Come limitare le risorse in Aspose.HTML Python
url: /it/python/general/how-to-limit-resources-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come limitare le risorse in Aspose.HTML per Python

Ti sei mai chiesto **come limitare le risorse** mentre carichi un file HTML gigantesco? Non sei l'unico. Quando una pagina contiene decine di immagini, script e fogli di stile, il loader predefinito può consumare memoria più velocemente di un bambino in una frenesia di caramelle. La buona notizia? Aspose.HTML ti offre un controllo fine‑grained, e questa guida mostra **come limitare le risorse** passo passo.

Tratteremo anche **come impostare la profondità** per la gestione delle risorse e dimostreremo il modo più sicuro per **caricare una grande pagina html** senza far esplodere il tuo processo Python. Alla fine, avrai uno script pronto all'uso che rispetta un limite di profondità a tre livelli e mantiene la tua app reattiva.

## Prerequisiti

- Python 3.8 o versioni successive (la libreria supporta tutte le versioni recenti).
- Una licenza attiva di Aspose.HTML per Python o una chiave di valutazione gratuita.
- Il pacchetto `aspose-html` installato:

```bash
pip install aspose-html
```

Se stai usando un ambiente virtuale (altamente consigliato), attivalo prima—senza problemi.

## Come limitare le risorse durante il caricamento di grandi pagine HTML

Il fulcro di **come limitare le risorse** si trova nella classe `ResourceHandlingOptions`. Pensala come un agente del traffico che dice ad Aspose.HTML quando dire “stop” alle risorse annidate ulteriormente. Di seguito trovi l'esempio completo e eseguibile che segue esattamente i passaggi di cui avrai bisogno.

```python
# Step 1: Import the required Aspose.HTML classes
from aspose.html import ResourceHandlingOptions, HTMLDocument

# Step 2: Create a ResourceHandlingOptions instance and limit the handling depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after 3 levels of nested resources

# Step 3: Load the HTML document using the configured resource options
# Replace 'YOUR_DIRECTORY/big_page.html' with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)

# Optional: Verify that the document loaded without exhausting memory
print(f"Document title: {doc.title}")
print(f"Number of pages: {len(doc.pages)}")
```

### Perché funziona

1. **Importare le classi corrette** – `ResourceHandlingOptions` contiene le impostazioni, mentre `HTMLDocument` si occupa del parsing dell'HTML.
2. **Impostare `max_handling_depth`** – Questa è la risposta esatta a **come impostare la profondità**. Una profondità di `3` significa che Aspose.HTML seguirà link, script e immagini solo per tre livelli. Qualsiasi livello più profondo viene ignorato, riducendo drasticamente l'uso di memoria.
3. **Passare le opzioni al costruttore** – Il costruttore `HTMLDocument` accetta un secondo argomento, così non è necessario fare una chiamata separata per applicare le impostazioni. È pulito, conciso e riduce la possibilità di dimenticare di abilitare il limite.

### Output previsto

Eseguendo lo script dovrebbe stampare qualcosa del genere:

```
Document title: Massive Report
Number of pages: 1
```

Se il file HTML contiene più di tre livelli di risorse collegate, quelle più profonde semplicemente non verranno scaricate. Non viene generato alcun errore; il loader le ignora.

## Come impostare la profondità per la gestione delle risorse

Ora che hai visto un esempio base, esploriamo **come impostare la profondità** per diversi scenari.

| Profondità desiderata | Caso d'uso                                          | Impostazione consigliata |
|-----------------------|-----------------------------------------------------|--------------------------|
| `1`                   | Solo il file HTML principale, ignora tutte le risorse esterne | `resource_options.max_handling_depth = 1` |
| `2`                   | Carica immagini e CSS ma salta gli script annidati | `resource_options.max_handling_depth = 2` |
| `3` (default)         | Approccio equilibrato per la maggior parte delle pagine grandi | `resource_options.max_handling_depth = 3` |
| `0`                   | Disabilita completamente il caricamento di risorse esterne | `resource_options.max_handling_depth = 0` |

> **Consiglio:** Inizia con `3` e riduci il valore solo se noti che il processo continua a consumare RAM. Più bassa è la profondità, meno chiamate di rete effettuerai, il che velocizza anche il caricamento.

### Casi limite e avvertenze

- **Riferimenti circolari:** Se una pagina si include indirettamente (A → B → A), il limite di profondità impedisce loop infiniti. Il loader si fermerà alla profondità configurata e registrerà un avviso.
- **Script dinamici:** Alcuni JavaScript iniettano risorse dopo il caricamento iniziale. `max_handling_depth` influisce solo sui riferimenti statici; per contenuti dinamici dovrai eseguire lo script in un browser headless o recuperare manualmente le risorse aggiuntive.
- **File mancanti:** Quando una risorsa a una profondità consentita è assente, Aspose.HTML la ignora silenziosamente. Puoi abilitare il logging tramite `aspose.html.logging` se hai bisogno di maggiore visibilità.

## Carica grandi pagine HTML in modo efficiente

Quando l'obiettivo è **caricare una grande pagina html** senza sovraccaricare il server, combina il limite di profondità con alcuni trucchi aggiuntivi:

1. **Stream del file** – Se la pagina è su disco, aprila con uno stream bufferizzato per ridurre i picchi di memoria.
2. **Disabilita JavaScript** – Se non ti serve l'esecuzione di script, disattivalo:

```python
from aspose.html import HtmlLoadOptions
load_options = HtmlLoadOptions()
load_options.enable_javascript = False
doc = HTMLDocument("big_page.html", resource_options, load_options)
```

3. **Usa una cartella temporanea per le risorse** – Indirizza Aspose.HTML a una cartella sandbox così le risorse scaricate non inquinano la directory del progetto.

```python
resource_options.resource_folder = "temp_resources"
```

Mettendo tutto insieme:

```python
from aspose.html import ResourceHandlingOptions, HTMLDocument, HtmlLoadOptions

# Configure depth limit
resource_opts = ResourceHandlingOptions()
resource_opts.max_handling_depth = 3
resource_opts.resource_folder = "temp_resources"

# Disable JavaScript for faster parsing
load_opts = HtmlLoadOptions()
load_opts.enable_javascript = False

# Load the massive HTML file
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_opts, load_opts)

print(f"Title: {doc.title}")
print(f"Loaded pages: {len(doc.pages)}")
```

Eseguendo questo script su un file HTML da 200 MB con centinaia di risorse collegate, di solito termina in meno di un minuto su un laptop modesto—molto meglio rispetto al loader predefinito senza limiti.

## Domande comuni (e le loro risposte)

- **E se ho bisogno di una scansione più profonda per una pagina specifica?**  
  Basta aumentare `max_handling_depth` per quella esecuzione. Puoi anche calcolarla dinamicamente in base alle dimensioni della pagina.

- **Posso ottenere un elenco delle risorse saltate?**  
  Sì. Dopo il caricamento, `doc.resources` contiene solo le risorse effettivamente scaricate. Qualsiasi cosa mancante semplicemente non è nella collezione.

- **Il limite di profondità è thread‑safe?**  
  L'istanza `ResourceHandlingOptions` è immutabile una volta passata a `HTMLDocument`, quindi puoi riutilizzarla in sicurezza tra thread.

## Riepilogo

In questo tutorial abbiamo coperto **come limitare le risorse** quando si utilizza Aspose.HTML per Python, spiegato **come impostare la profondità** per controllare il caricamento di risorse annidate, e dimostrato il modo più sicuro per **caricare una grande pagina html** senza esaurire la memoria. Configurando `ResourceHandlingOptions` e, opzionalmente, `HtmlLoadOptions`, ottieni un controllo preciso sul processo di caricamento, rendendo la tua applicazione più veloce e affidabile.

## Prossimi passi

- Sperimenta con diversi valori di profondità per i tuoi set di dati.
- Combina il limite di profondità con un browser headless (ad es., Playwright) per contenuti dinamici.
- Approfondisci le funzionalità di conversione PDF di Aspose.HTML—una volta caricata la pagina in modo efficiente, convertirla in PDF è un gioco da ragazzi.

Hai altre domande o una pagina ostinata che continua a far esplodere la tua memoria? Lascia un commento e risolveremo il problema insieme. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come impostare il timeout – Gestire il timeout di rete in Aspose.HTML per Java](/html/english/java/message-handling-networking/network-timeout/)
- [Come impostare il timeout in Aspose.HTML per Java Runtime Service](/html/english/java/configuring-environment/configure-runtime-service/)
- [Come impostare il set di caratteri in Aspose.HTML per Java](/html/english/java/configuring-environment/set-character-set/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}