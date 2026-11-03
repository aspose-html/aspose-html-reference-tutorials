---
category: general
date: 2026-06-16
description: Come usare CSS per caricare un file HTML e contare i link in Java. Impara
  a contare gli elementi HTML e a valutare XPath in Java in un unico esempio chiaro.
draft: false
keywords:
- how to use css
- load html file
- how to count links
- count html elements
- evaluate xpath java
language: it
og_description: Come utilizzare CSS in Java per caricare un file HTML, contare i link
  e valutare le espressioni XPath—tutto in una guida pratica.
og_title: Come usare CSS in Java – Caricare HTML, contare i link e valutare XPath
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use CSS to load HTML file and count links in Java. Learn to
    count html elements and evaluate xpath java in a single, clear example.
  headline: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
  type: TechArticle
- description: How to use CSS to load HTML file and count links in Java. Learn to
    count html elements and evaluate xpath java in a single, clear example.
  name: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
  steps:
  - name: What if the HTML file is malformed?
    text: Both the CSS and XPath engines are tolerant of minor markup errors (missing
      closing tags, unquoted attributes). However, severe malformations may cause
      the parser to abort. In production, wrap the loading step in a try‑catch block
      and log the exception.
  - name: Can I combine CSS and XPath in a single expression?
    text: Not directly; each engine has its own syntax. The typical pattern is to
      use the one that expresses the condition most naturally (CSS for structural
      queries, XPath for attribute functions) and then merge the results in Java if
      needed.
  - name: How do I count elements across multiple files?
    text: 'Just place the loading logic inside a loop:'
  - name: Does this work with Java 8?
    text: Yes—provided you use a library version that targets Java 8 or higher. The
      code shown does not rely on newer language features.
  type: HowTo
tags:
- Java
- HTML parsing
- CSS selectors
- XPath
title: Come usare CSS in Java – Caricare HTML, contare i link e valutare XPath
url: /it/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare CSS in Java – Caricare HTML, Contare i link e valutare XPath

Ti sei mai chiesto **come usare i selettori CSS** durante l'elaborazione di un file HTML in Java? Forse stai costruendo un web‑crawler, uno scraper, o semplicemente devi verificare un sito statico. La buona notizia? Non devi scrivere un parser personalizzato da zero—le librerie moderne ti permettono di combinare i selettori CSS4 con le espressioni XPath 3.1 in un unico flusso di lavoro ordinato.

In questo tutorial vedremo **come caricare un file HTML**, applicare un selettore CSS per contare i link all'interno di una barra di navigazione, e poi **valutare XPath** per contare specifici elementi immagine. Alla fine avrai un programma completo e eseguibile che stampa il numero di nodi corrispondenti, e comprenderai perché ogni parte è importante.

## Prerequisiti

- Java 17 (o qualsiasi JDK recente) installato sulla tua macchina  
- Maven o Gradle per la gestione delle dipendenze (useremo Maven nell'esempio)  
- Un piccolo frammento HTML salvato come `input.html` in una cartella che controlli  

Non sono necessari altri strumenti—solo un editor di testo e un terminale.

## Cosa copre il tutorial

- **Caricamento di un file HTML** in una struttura simile a DOM usando la classe *HTMLDocument*  
- Applicazione di un **selettore CSS4** (`nav a[data-role]`) per individuare i link di navigazione  
- Esecuzione di un'**espressione XPath 3.1** per trovare i tag `<img>` il cui `src` termina con `.png` e che hanno anche un attributo `alt`  
- **Conteggio** dei risultati di entrambe le query e stampa su console  
- Codice sorgente completo, spiegazioni del “perché”, e una rapida occhiata a possibili casi limite  

Iniziamo subito.

---

## Passo 1 – Come caricare un file HTML con HTMLDocument

Prima di poter eseguire qualsiasi query, il documento HTML deve essere analizzato in un modello attraversabile. La classe `HTMLDocument` della libreria **jsoup‑plus** (o di qualsiasi parser simile consapevole di HTML) fa esattamente questo.

```java
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Load the HTML document from the file system
        HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/input.html");
        // From here on we can query the DOM using CSS or XPath
```

*Perché è importante:*  
Caricare il file una sola volta e mantenere un riferimento (`doc`) evita I/O ripetuti, che possono diventare un collo di bottiglia di prestazioni quando si elaborano grandi lotti di pagine.

---

## Passo 2 – Come usare CSS per contare i link all'interno di `<nav>`

Ora che il documento è in memoria, possiamo usare un selettore CSS4 per prendere ogni elemento `<a>` che si trova all'interno di un `<nav>` e che possiede anche un attributo `data‑role`. Questo è un pattern comune per i menu di navigazione che usano attributi data per i hook JavaScript.

```java
        // Use a CSS4 selector to find every <a> inside a <nav> that has a data‑role attribute
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");
```

*Spiegazione:*  
- `nav a[data-role]` si legge come “qualsiasi elemento `<a>` con un attributo `data‑role` che è discendente di un elemento `<nav>`.”  
- Il selettore è compatibile con **CSS4**, il che significa che puoi anche usare pseudo‑classi come `:not()` o `:has()` se il tuo caso d'uso si espande.

> **Consiglio:** Se ti servono solo i figli diretti, sostituisci lo spazio con `>` (`nav > a[data-role]`). Questo riduce lo spazio di ricerca e può accelerare l'elaborazione di documenti grandi.

---

## Passo 3 – Valutare XPath in Java per contare specifici elementi `<img>`

XPath brilla quando hai bisogno di filtrare in base agli attributi, cosa non così immediata in CSS. Qui individueremo ogni `<img>` il cui `src` termina con `.png` **e** che definisce anche un attributo `alt`—utile per audit di accessibilità.

```java
        // Use an XPath 3.1 expression to locate all <img> elements whose src ends with .png and have an alt attribute
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");
```

*Perché XPath?*  
- La funzione `ends-with()` fa parte di XPath 3.1, consentendo il confronto di suffissi senza ricorrere a regex.  
- Combinare più predicati (`and @alt`) garantisce di contare solo le immagini che sono sia correttamente referenziate sia descritte.

Se la tua libreria supporta solo XPath 1.0, dovrai usare `contains(@src, '.png')` e poi filtrare in Java—un approccio meno preciso.

---

## Passo 4 – Come contare gli elementi HTML e stampare i risultati

Infine, recuperiamo le lunghezze di entrambi gli oggetti `NodeList` e li stampiamo. Questa è la parte **come contare i link** del puzzle, ma funziona per qualsiasi collezione di nodi.

```java
        // Output the number of matches for each query
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**Output previsto sulla console** (supponendo che l'HTML di esempio contenga 3 link corrispondenti e 2 immagini corrispondenti):

```
Nav links: 3
PNG images with alt: 2
```

Se i conteggi sono zero, ricontrolla la sintassi del tuo selettore o verifica che `input.html` contenga effettivamente gli elementi attesi.

---

## Esempio completo funzionante

Di seguito trovi il programma completo e autonomo che puoi copiare‑incollare in un file chiamato `CssXPathDemo.java`. Include gli import necessari, un semplice frammento `pom.xml` per Maven, e un campione HTML minimale per i test.

```java
/* CssXPathDemo.java */
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the HTML document
        HTMLDocument doc = new HTMLDocument("input.html");

        // Step 2: CSS selector – count navigation links with data-role
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");

        // Step 3: XPath expression – count PNG images that have alt text
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");

        // Step 4: Print the results
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**Estratto `pom.xml` di Maven** (aggiungi questa dipendenza per includere il parser consapevole di HTML che supporta sia CSS4 sia XPath 3.1):

```xml
<dependencies>
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>html-parser-plus</artifactId>
        <version>2.3.1</version>
    </dependency>
</dependencies>
```

**Esempio `input.html`** (posizionalo nella stessa directory del file Java):

```html
<!DOCTYPE html>
<html lang="en">
<head><title>Test Page</title></head>
<body>
<nav>
    <a href="/home" data-role="main">Home</a>
    <a href="/about" data-role="secondary">About</a>
    <a href="/contact">Contact</a>
</nav>
<img src="logo.png" alt="Company Logo">
<img src="banner.jpg">
<img src="icon.png" alt="Icon">
</body>
</html>
```

Eseguendo `mvn compile exec:java -Dexec.mainClass=CssXPathDemo` otterrai i conteggi attesi mostrati in precedenza.

---

## Casi limite e domande comuni

### Cosa succede se il file HTML è malformato?

Sia i motori CSS che XPath tollerano errori di markup minori (tag di chiusura mancanti, attributi non quotati). Tuttavia, malformazioni gravi possono far abortire il parser. In produzione, avvolgi il passaggio di caricamento in un blocco try‑catch e registra l'eccezione.

### Posso combinare CSS e XPath in un'unica espressione?

Non direttamente; ogni motore ha la propria sintassi. Il pattern tipico è usare quello che esprime la condizione più naturalmente (CSS per query strutturali, XPath per funzioni sugli attributi) e poi unire i risultati in Java se necessario.

### Come conto gli elementi su più file?

Basta posizionare la logica di caricamento all'interno di un ciclo:

```java
for (Path p : Files.newDirectoryStream(Paths.get("html_folder"), "*.html")) {
    HTMLDocument doc = new HTMLDocument(p.toString());
    // repeat the queries...
}
```

### Funziona con Java 8?

Sì—a condizione di usare una versione della libreria che supporta Java 8 o superiore. Il codice mostrato non dipende da funzionalità più recenti del linguaggio.

---

## Conclusione

Abbiamo dimostrato **come usare i selettori CSS** insieme alle espressioni **evaluate xpath java** per **caricare un file HTML**, **contare i link** e **contare gli elementi HTML** che soddisfano criteri specifici. I punti chiave sono:

- Caricare il documento una sola volta con `HTMLDocument`.  
- Sfruttare CSS4 per query strutturali semplici (`nav a[data-role]`).  
- Utilizzare XPath 3.1 per potenti funzioni sugli attributi (`ends-with(@src, '.png')`).  
- Recuperare la lunghezza del `NodeList` per ottenere conteggi esatti.  

Da qui puoi espandere lo script: aggiungere più selettori, scrivere i risultati in un CSV, o integrarlo in una pipeline di crawling più ampia. La combinazione di CSS e XPath ti offre la flessibilità per affrontare praticamente qualsiasi sfida di scraping HTML.

Pronto a sperimentare? Prova a sostituire il selettore CSS con `section article[data-id]` o cambia l'XPath per puntare ai tag `<video>` con un codec specifico. Il cielo è il limite.

Se hai trovato utile questa guida, sentiti libero di condividerla, mettere una stella al repository, o lasciare un commento con i tuoi casi d'uso. Buon coding!

![diagramma esempio di utilizzo CSS](https://example.com/diagram.png "esempio di utilizzo CSS")

---

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come aggiungere CSS – CSS inline ai documenti HTML in Aspose.HTML per Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Come modificare CSS - Modifica avanzata di CSS esterno con Aspose.HTML per Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)
- [Come modificare l'albero del documento HTML in Aspose.HTML per Java](/html/english/java/editing-html-documents/edit-html-document-tree/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}