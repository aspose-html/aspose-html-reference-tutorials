---
category: general
date: 2026-10-09
description: Impara a limitare la profondità delle risorse annidate usando Aspose.HTML
  ResourceHandlingOptions in Python. Controlla max_handling_depth per una conversione
  HTML sicura.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit nested resource depth
- Aspose.HTML ResourceHandlingOptions
- Python resource handling
- max_handling_depth
- nested HTML resources
language: it
lastmod: 2026-10-09
og_description: Limita la profondità delle risorse annidate usando Aspose.HTML ResourceHandlingOptions
  in Python. Imposta max_handling_depth per proteggere il tuo flusso di lavoro di
  conversione HTML.
og_image_alt: Screenshot showing limit nested resource depth setting in Python
og_title: Come limitare la profondità delle risorse annidate con Aspose.HTML in Python
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Learn to limit nested resource depth using Aspose.HTML ResourceHandlingOptions
    in Python. Control max_handling_depth for safe HTML conversion.
  headline: How to limit nested resource depth with Aspose.HTML in Python
  type: TechArticle
- description: Learn to limit nested resource depth using Aspose.HTML ResourceHandlingOptions
    in Python. Control max_handling_depth for safe HTML conversion.
  name: How to limit nested resource depth with Aspose.HTML in Python
  steps:
  - name: What the setting does
    text: '- **Depth 0** – The root HTML document is processed, but no external resources
      are fetched. - **Depth 1** – Direct resources referenced by the root (e.g.,
      `<img src="...">`, `<link href="...">`) are fetched. - **Depth 2** – Resources
      referenced by the first‑level resources (e.g., CSS files that impo'
  - name: Using the options with a converter
    text: After configuring the depth limit, pass the `resource_options` object to
      the `HtmlConverter` (or any Aspose.HTML API that accepts `ResourceHandlingOptions`).
  - name: 1. Disabling depth limiting entirely
    text: Set the property to a very high number (e.g., `sys.maxsize`) or `None` if
      you want unrestricted handling. Use this only when you trust the source HTML.
  - name: 2. Handling missing resources
    text: When the depth limit stops a resource from being fetched, Aspose.HTML logs
      a warning but continues. You can capture these warnings by attaching a custom
      logger to the converter if you need audit trails.
  - name: 3. Combining with other resource options
    text: '`ResourceHandlingOptions` also offers `allow_external_resources`, `download_timeout`,
      and `max_resource_size`. Pairing a depth limit with a size limit provides a
      robust safety net.'
  - name: 4. Testing the limit
    text: Create a test HTML hierarchy with nested `<iframe>` tags or CSS `@import`
      statements to verify that your depth limit behaves as expected before deploying
      to production.
  type: HowTo
tags:
- Aspose.HTML
- Python
- HTML conversion
- Resource handling
title: Come limitare la profondità delle risorse annidate con Aspose.HTML in Python
url: /it/python/general/how-to-limit-nested-resource-depth-with-aspose-html-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come limitare la profondità delle risorse nidificate con Aspose.HTML in Python

Se hai bisogno di **limitare la profondità delle risorse nidificate** durante la conversione di HTML con Aspose.HTML, questa guida ti mostra esattamente come farlo in Python. Controllare la proprietà `max_handling_depth` evita ricorsioni incontrollate quando una pagina include risorse profondamente nidificate come frame o fogli di stile collegati.

Imparerai anche perché impostare un limite di profondità è importante, vedrai l’esempio di codice completo e scoprirai le insidie più comuni e i consigli di best‑practice. Non è necessaria alcuna documentazione esterna—tutto ciò che ti serve è qui.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- Python 3.8 o versioni successive installate  
- Il pacchetto `aspose.html` (`pip install aspose-html`)  
- Familiarità di base con il flusso di lavoro di conversione di Aspose.HTML  

Questi sono gli unici requisiti per gli esempi seguenti.

## Passo 1: Importare la classe **ResourceHandlingOptions**

Il primo passo è importare la classe `ResourceHandlingOptions` nel tuo script. Questa classe raggruppa tutte le opzioni che influenzano come le risorse esterne (immagini, CSS, script, ecc.) vengono recuperate e elaborate durante la conversione.

```python
# Step 1: Import the ResourceHandlingOptions class
from aspose.html import ResourceHandlingOptions
```

**Perché è importante:**  
`ResourceHandlingOptions` isola le impostazioni relative alle risorse dalle altre opzioni di conversione, consentendoti di perfezionare la gestione delle risorse nidificate senza influire sul rendering o sul formato di output.

## Passo 2: Creare un'istanza dell'oggetto opzioni

Istanzia `ResourceHandlingOptions` così da poter modificare le sue proprietà. L'istanza predefinita permette un annidamento illimitato, il che può causare problemi di prestazioni o addirittura overflow dello stack su pagine appositamente costruite.

```python
# Step 2: Create an instance of the options object
resource_options = ResourceHandlingOptions()
```

**Consiglio:**  
Se prevedi di riutilizzare lo stesso limite di profondità in molte conversioni, memorizza l'oggetto configurato in una variabile a livello di modulo per evitare di ricrearlo ogni volta.

## Passo 3: Impostare **max_handling_depth** per limitare la profondità delle risorse nidificate

Assegna alla proprietà `max_handling_depth` il numero massimo di livelli nidificati che desideri consentire. In questo esempio interrompiamo dopo **3** livelli, ma puoi scegliere qualsiasi intero adatto al tuo scenario.

```python
# Step 3: Limit the depth of nested resource handling (stop after 3 levels)
resource_options.max_handling_depth = 3
```

### Cosa fa l'impostazione

- **Depth 0** – Viene elaborato il documento HTML radice, ma non vengono recuperate risorse esterne.  
- **Depth 1** – Vengono recuperate le risorse dirette referenziate dalla radice (es. `<img src="...">`, `<link href="...">`).  
- **Depth 2** – Vengono recuperate le risorse referenziate dalle risorse di primo livello (es. file CSS che importano altri CSS).  
- **Depth 3** – Il processo si ferma dopo la gestione delle risorse di terzo livello. Qualsiasi riferimento più profondo viene ignorato.

Impostare `max_handling_depth` protegge la tua applicazione da:

| Rischio | Come aiuta il limite |
|------|----------------------|
| **Ricorsione infinita** causata da riferimenti circolari | Il convertitore si interrompe dopo la profondità definita, rompendo il ciclo. |
| **Traffico di rete eccessivo** quando una pagina carica decine di fogli di stile concatenati | Vengono scaricati solo i primi livelli, riducendo la larghezza di banda. |
| **Esaurimento della memoria** dovuto al caricamento di alberi di risorse massivi | Vengono creati meno oggetti, mantenendo l'uso della memoria prevedibile. |

### Utilizzare le opzioni con un convertitore

Dopo aver configurato il limite di profondità, passa l'oggetto `resource_options` a `HtmlConverter` (o a qualsiasi API di Aspose.HTML che accetti `ResourceHandlingOptions`).

```python
from aspose.html import HtmlConverter, SaveFormat

# Create a converter with the resource handling options
converter = HtmlConverter(resource_options)

# Convert a sample HTML file to PDF while respecting the depth limit
converter.convert("sample.html", "output.pdf", SaveFormat.PDF)

print("Conversion completed with max_handling_depth =", resource_options.max_handling_depth)
```

**Output previsto**

```
Conversion completed with max_handling_depth = 3
```

Se l'HTML di origine contiene risorse oltre il terzo livello, verranno omesse dal PDF e la conversione terminerà comunque rapidamente.

## Casi limite e variazioni comuni

### 1. Disabilitare completamente il limite di profondità

Imposta la proprietà a un numero molto alto (es. `sys.maxsize`) o a `None` se desideri una gestione senza restrizioni. Usa questa opzione solo quando ti fidi dell'HTML di origine.

```python
import sys
resource_options.max_handling_depth = sys.maxsize  # effectively unlimited
```

### 2. Gestire risorse mancanti

Quando il limite di profondità impedisce il recupero di una risorsa, Aspose.HTML registra un avviso ma continua. Puoi catturare questi avvisi collegando un logger personalizzato al convertitore, se ti servono tracciature di audit.

### 3. Combinare con altre opzioni di risorsa

`ResourceHandlingOptions` offre anche `allow_external_resources`, `download_timeout` e `max_resource_size`. Accoppiare un limite di profondità con un limite di dimensione fornisce una rete di sicurezza robusta.

```python
resource_options.allow_external_resources = True
resource_options.max_resource_size = 5 * 1024 * 1024  # 5 MiB per resource
```

### 4. Testare il limite

Crea una gerarchia HTML di prova con tag `<iframe>` nidificati o dichiarazioni CSS `@import` per verificare che il tuo limite di profondità si comporti come previsto prima di distribuirlo in produzione.

## Consigli pratici (E‑E‑A‑T)

- **Convalida gli URL di input** prima della conversione per evitare chiamate di rete non necessarie.  
- **Registra la profondità effettivamente raggiunta** (`converter.handling_depth_reached`) per il monitoraggio.  
- **Riutilizza lo stesso `ResourceHandlingOptions`** in più conversioni per mantenere la configurazione coerente.  
- **Profilare le prestazioni** quando modifichi la profondità; un limite più basso di solito velocizza la conversione ma può omettere risorse necessarie.  

## Conclusione

Ora sai come **limitare la profondità delle risorse nidificate** quando lavori con Aspose.HTML in Python configurando la proprietà `max_handling_depth` di `ResourceHandlingOptions`. Questa singola impostazione protegge la tua pipeline di conversione da ricorsioni incontrollate, uso eccessivo della rete e picchi di memoria, offrendoti al contempo un controllo granulare su quanto in profondità vengano elaborate le gerarchie di risorse.

Pronto per approfondire? Prova a combinare il limite di profondità con `max_resource_size` per creare un flusso di lavoro di conversione HTML‑to‑PDF completamente rinforzato, oppure leggi la nostra guida su **Aspose.HTML resource handling** per approfondimenti su `allow_external_resources` e la gestione dei timeout.

--- 

*Immagine che illustra l'impostazione del limite di profondità (opzionale):*  
![Screenshot showing limit nested resource depth setting in Python](placeholder.png "limit nested resource depth")

## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci alternativi di implementazione nei tuoi progetti.

- [Custom Resource Handler in Aspose HTML – Save to Stream Guide](/html/english/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Message Handling and Networking in Aspose.HTML for Java](/html/english/java/message-handling-networking/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}