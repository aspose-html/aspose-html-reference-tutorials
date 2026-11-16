---
category: general
date: 2026-07-05
description: Apri i link in una nuova scheda usando Python – impara come aggiungere
  target blank, modificare il target del link, utilizzare il selettore con attributo
  contains e salvare l'HTML modificato senza sforzo.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: it
og_description: Apri i link in una nuova scheda rapidamente. Questo tutorial mostra
  come aggiungere target="_blank", cambiare il target del link e salvare l'HTML modificato
  con Python.
og_title: Apri i collegamenti in una nuova scheda – Guida passo‑passo per l'aggiornamento
  HTML
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: Apri i link in una nuova scheda – Guida completa all'aggiornamento delle ancore
  HTML
url: /it/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Open Links New Tab – Complete Guide to Updating HTML Anchors

Ti è mai capitato di dover **open links new tab** su una pagina HTML statica ma non sapevi da dove cominciare? Non sei solo. Molti sviluppatori incontrano questo ostacolo quando puliscono siti legacy o aggiungono miglioramenti di accessibilità. In questo tutorial vedremo una soluzione pratica che **adds target blank**, **changes link target**, e salva in modo sicuro **saves modified html**—tutto con poche righe di Python.

Tratteremo anche come usare un **attribute contains selector** così da intervenire solo sugli ancoraggi che ti interessano davvero (ad esempio, tutti i link che puntano a *example.com*). Alla fine avrai uno script riutilizzabile che potrai inserire in qualsiasi progetto, grande o piccolo.

## Cosa imparerai

- Carica un file HTML in un oggetto documento manipolabile.  
- Seleziona gli elementi `<a>` il cui attributo `href` contiene una sottostringa specifica.  
- **Add target blank** e imposta l'attributo `rel="noopener"` per migliorare la sicurezza.  
- **Save modified html** di nuovo su disco senza perdere la formattazione.  

Nessuna dipendenza esterna oltre alla libreria standard e **beautifulsoup4** (una piccola installazione). Se stai già usando un parser diverso, i concetti si traducono direttamente.

---

## Prerequisiti

- Python 3.8+ installato sulla tua macchina.  
- Familiarità di base con HTML e Python.  
- Pacchetto `beautifulsoup4` (`pip install beautifulsoup4`).  

È tutto—non sono richiesti framework pesanti.

---

## Passo 1: Carica il documento HTML

Prima di tutto: dobbiamo leggere il file sorgente e passarne il contenuto a BeautifulSoup. Pensalo come aprire una tela vuota dove puoi aggiungere nuovi attributi.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Perché è importante:** Usare `Path` mantiene il codice indipendente dal sistema operativo, e `html.parser` è integrato, così non hai bisogno di parser aggiuntivi per compiti semplici.

---

## Passo 2: Usa un Attribute Contains Selector per trovare i link giusti

Vogliamo intervenire solo sugli ancoraggi che puntano a *example.com*. Il selettore CSS `a[href*='example.com']` fa esattamente questo—`*=` significa “contiene”. Il metodo `select` di BeautifulSoup comprende questa sintassi.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Consiglio professionale:** Se ti serve una corrispondenza case‑insensitive, passa a un piccolo ciclo che verifica `if 'example.com' in a.get('href', '').lower()`.

Ora `anchor_elements` contiene tutti i link di cui ci interessa, pronti per la trasformazione successiva.

---

## Passo 3: Cambia il target del link – Aggiungi Target Blank e rendi il link sicuro

Aprire un link in una nuova scheda è semplice come impostare `target="_blank"`. Tuttavia, i browser moderni raccomandano di aggiungere anche `rel="noopener"` (o `noreferrer`) per impedire alla pagina appena aperta di accedere alla finestra originale tramite `window.opener`. Questa piccola modifica di sicurezza può fermare attacchi di phishing.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Perché usiamo l'assegnazione diretta del dizionario:** Crea automaticamente l'attributo se manca, e lo sovrascrive se esiste già—perfetto per un'operazione di **change link target**.

---

## Passo 4: Salva l'HTML modificato su disco

L'ultimo passo è scrivere il markup aggiornato in un nuovo file. Mantenere intatto l'originale ti permette di tornare indietro se qualcosa va storto.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **Cosa fa `prettify()`:** Formatta l'HTML con una buona indentazione, rendendo il file salvato più facile da leggere e confrontare in seguito. Se preferisci gli spazi originali, sostituisci `prettify()` con `str(soup)`.

---

## Script completo – Soluzione a un click

Di seguito trovi lo script completo, pronto da eseguire. Salvalo come `update_links.py` ed esegui `python update_links.py` dal tuo terminale.

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### Risultato atteso

Supponiamo che `links.html` contenesse originariamente:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Dopo aver eseguito lo script, `links-updated.html` avrà l'aspetto seguente:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Solo il link a *example.com* ha ricevuto gli attributi **add target blank**, dimostrando che il nostro **attribute contains selector** ha funzionato esattamente come previsto.

---

## Domande comuni e casi particolari

### E se un link ha già un attributo `rel`?

Il nostro ciclo lo sovrascrive con `"noopener"`. Se devi preservare i valori esistenti (ad esempio, `"nofollow"`), concatenali invece:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### Come gestire più domini?

Basta espandere la lista dei selettori:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### `prettify()` modifica la struttura originale dell'HTML?

Riformatta l'indentazione ma non altera l'ordine dei tag o i valori degli attributi. Se devi mantenere esattamente gli spazi originali, sostituisci `prettify()` con `str(soup)` come menzionato prima.

---

## Consigli professionali per script pronti alla produzione

- **Backup prima di sovrascrivere:** Aggiungi un passaggio di copia (`shutil.copy`) per mantenere il file originale al sicuro.  
- **Logging invece di print:** Usa il modulo `logging` per progetti scalabili.  
- **Elaborazione batch:** Esegui un ciclo su una directory con `Path.rglob("*.html")` per aggiornare molti file in un'unica esecuzione.  

Queste modifiche trasformano un semplice script **open links new tab** in un'utilità robusta per qualsiasi flusso di lavoro di manutenzione web.

---

## Conclusione

Ora hai un metodo solido e riutilizzabile per **open links new tab** su qualsiasi collezione di HTML statici. Sfruttando un **attribute contains selector**, puoi **change link target** esattamente dove ti serve, **add target blank**, e **save modified html** senza perdere la formattazione.

Provalo su una pagina di test, poi scala all'intero sito. Hai bisogno di modificare il selettore per PDF, PDF o altri domini? Basta regolare la stringa CSS—tutto il resto rimane invariato.

Sentiti libero di lasciare un commento se incontri problemi, o condividi come hai esteso lo script per i tuoi progetti. Buon coding, e che tutti i tuoi ancoraggi si aprano esattamente dove desideri!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}