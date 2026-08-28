---
category: general
date: 2026-06-04
description: Estrai SVG da HTML ed esporta il file SVG con opzioni di salvataggio
  SVG personalizzate, mantenendo intatto il CSS esterno. Segui questo tutorial passo‑passo.
draft: false
keywords:
- extract svg from html
- export svg file
- svg save options
- svg external css
- inline svg markup
language: it
og_description: Estrai rapidamente SVG da HTML. Questo tutorial mostra come esportare
  un file SVG usando le opzioni di salvataggio SVG mantenendo il CSS esterno.
og_title: Estrai SVG da HTML – Guida all'esportazione di file SVG
schemas:
- author: Aspose
  dateModified: '2026-06-04'
  description: Extract SVG from HTML and export SVG file with custom SVG save options,
    keeping external CSS intact. Follow this step‑by‑step tutorial.
  headline: Extract SVG from HTML – Full Guide to Export SVG File
  type: TechArticle
tags:
- SVG
- HTML
- Export
- Scripting
title: Estrai SVG da HTML – Guida completa per esportare file SVG
url: /it/python/general/extract-svg-from-html-full-guide-to-export-svg-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai SVG da HTML – Guida completa per esportare file SVG

Ti è mai capitato di dover **estrarre svg da html** ma non eri sicuro di quali chiamate API ti forniscano un file pulito e autonomo? Non sei l'unico. In molti progetti di automazione web l'SVG è nascosto all'interno di una pagina, e estrarlo mantenendo lo stile originale è un vero grattacapo.  

In questa guida ti accompagneremo passo passo in una soluzione completa che non solo **estrae l'SVG**, ma ti mostra anche come **esportare file svg** con precise **svg save options**, garantendo che il tuo **svg external css** rimanga esterno e che il **inline svg markup** rimanga intatto.

## Cosa imparerai

- Come caricare un documento HTML dal disco.
- Come individuare il primo elemento `<svg>` (o qualsiasi altro di cui hai bisogno).
- Come creare un `SVGDocument` dal **inline svg markup**.
- Quali **svg save options** disabilitano l'incorporamento del CSS in modo che gli stili rimangano in file esterni.
- I passaggi esatti per **esportare file svg** nella cartella desiderata.
- Suggerimenti per gestire più SVG, preservare gli ID e risolvere problemi comuni.

Nessuna dipendenza pesante, solo gli oggetti di scripting integrati che ottieni con Adobe InDesign (o qualsiasi ambiente che fornisca `HTMLDocument`, `SVGDocument` e `SVGSaveOptions`). Prendi un editor di testo, copia il codice e sei pronto a partire.

![Extract SVG from HTML workflow](extract-svg-workflow.png){alt="Flusso di lavoro per estrarre SVG da HTML"}

## Prerequisiti

- Adobe InDesign (o un host ExtendScript compatibile) versione 2022 o successiva.
- Familiarità di base con la sintassi JavaScript/ExtendScript.
- Un file HTML che contenga almeno un elemento `<svg>` che desideri estrarre.

Se soddisfi questi tre requisiti, puoi saltare la sezione “setup” e passare direttamente al codice.

---

## Estrai SVG da HTML – Passo 1: Carica il documento HTML

Prima di tutto: ti serve un riferimento alla pagina HTML che contiene l'SVG. Il costruttore `HTMLDocument` accetta un percorso file e analizza il markup per te.

```javascript
// Step 1: Load the HTML document
var htmlPath = File("YOUR_DIRECTORY/page.html"); // adjust the path
var htmlDoc = new HTMLDocument(htmlPath);
```

> **Perché è importante:** Caricare il documento ti fornisce un modello di oggetti simile al DOM, così puoi interrogare gli elementi proprio come faresti in un browser. Senza questo, saresti costretto a utilizzare ricerche di stringhe fragili.

---

## Estrai SVG da HTML – Passo 2: Individua il primo elemento `<svg>`

Ora che il DOM è pronto, prendiamo il primo nodo SVG. Se ti serve un altro, basta cambiare l'indice o usare un selettore più specifico.

```javascript
// Step 2: Locate the first <svg> element
var svgElements = htmlDoc.getElementsByTagName("svg");
if (svgElements.length === 0) {
    throw new Error("No <svg> elements found in the HTML file.");
}
var svgElement = svgElements[0]; // you could loop through all if needed
```

> **Consiglio:** `svgElements` è una collezione simile a un array, quindi puoi iterarla per **esportare più file svg** in una successiva iterazione.

---

## Markup SVG inline – Passo 3: Crea un SVGDocument

La proprietà `outerHTML` restituisce il markup completo dell'elemento `<svg>`, includendo tutti gli attributi inline. Passare quella stringa a `SVGDocument` ti fornisce un oggetto SVG completo che puoi manipolare o salvare.

```javascript
// Step 3: Create an SVGDocument from the extracted markup
var svgMarkup = svgElement.outerHTML; // this is the inline svg markup
var svgDoc = new SVGDocument(svgMarkup);
```

> **Perché usiamo `outerHTML`:** Cattura l'elemento *e* i suoi figli, preservando gradienti, filtri e qualsiasi blocco `<style>` incorporato che possa far parte del **inline svg markup**.

---

## Opzioni di salvataggio SVG – Passo 4: Configura le impostazioni di esportazione

Per impostazione predefinita, InDesign incorpora il CSS direttamente nell'SVG, il che può gonfiare il file e rompere i flussi di lavoro con stili esterni. Per mantenere il foglio di stile separato, attiva/disattiva il flag `embedCSS`.

```javascript
// Step 4: Configure SVG save options (disable CSS embedding)
var svgOptions = new SVGSaveOptions();
svgOptions.embedCSS = false;      // ensures svg external css stays external
svgOptions.embedImages = false;   // optional: keep images as links
svgOptions.fontType = SVGFontType.OUTLINE; // optional: outline fonts
```

> **Cosa significa “svg external css”:** Quando `embedCSS` è `false`, tutti i tag `<style>` vengono rimossi e l'SVG fa riferimento a un file CSS separato (se esiste). Questo è perfetto per i flussi di lavoro che si basano su un foglio di stile condiviso tra molti asset SVG.

---

## Esporta file SVG – Passo 5: Salva l'SVG estratto

Infine, scrivi l'SVG su disco. Il metodo `save` rispetta le opzioni impostate sopra, producendo un file pulito pronto per il web o per ulteriori elaborazioni.

```javascript
// Step 5: Save the extracted SVG to a separate file
var outputPath = File("YOUR_DIRECTORY/extracted.svg");
svgDoc.save(outputPath, svgOptions);
```

**Risultato atteso:** Un file chiamato `extracted.svg` appare in `YOUR_DIRECTORY`. Aprilo in un browser – dovresti vedere il grafico renderizzato esattamente come appariva nell'HTML originale, ma con tutto il CSS ora caricato da fonti esterne.

---

## Gestione di più SVG (Opzionale)

Se la tua pagina HTML contiene diversi SVG, avvolgi la logica di individuazione‑e‑salvataggio in un ciclo:

```javascript
for (var i = 0; i < svgElements.length; i++) {
    var element = svgElements[i];
    var doc = new SVGDocument(element.outerHTML);
    var outFile = File("YOUR_DIRECTORY/svg_" + i + ".svg");
    doc.save(outFile, svgOptions);
}
```

Questa piccola modifica ti consente di **esportare file svg** in massa senza riscrivere alcun codice.

---

## Problemi comuni e come evitarli

| Sintomo | Causa probabile | Soluzione |
|---------|-----------------|-----------|
| L'SVG appare vuoto nel browser | Il CSS è stato incorporato e poi rimosso, perdendo le regole di stile | Assicurati che `svgOptions.embedCSS = false` solo quando hai un foglio di stile esterno pronto. |
| Il testo appare seghettato | I font non sono stati convertiti in contorni | Imposta `svgOptions.fontType = SVGFontType.OUTLINE`. |
| Le immagini mancano | `embedImages` è rimasto true ma le immagini sono esterne | Imposta `svgOptions.embedImages = false` e mantieni i file immagine accanto all'SVG. |
| Gli ID collidono quando si uniscono più SVG | Ogni SVG ha mantenuto i suoi ID originali | Esegui un post‑processo con uno script di rinomina semplice o usa l'opzione “unique IDs” di InDesign, se disponibile. |

---

## Script completo – Pronto per copia‑incolla

Di seguito trovi l'intero script, pronto da incollare in una finestra di ExtendScript Toolkit ed eseguire. Sostituisci `YOUR_DIRECTORY` con la cartella che contiene il tuo file HTML.



## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Salva documento SVG in Aspose.HTML per Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Come convertire SVG in XPS con Aspose.HTML per Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Crea PDF da SVG con Aspose.HTML per Java](/html/hindi/java/conversion-html-to-other-formats/convert-svg-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}