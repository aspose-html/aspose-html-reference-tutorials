---
category: general
date: 2026-06-03
description: Seleziona l'elemento HTML per classe in Java, impara come caricare un
  file HTML in Java, analizza un documento HTML in Java e estrai il valore di una
  proprietà CSS come il colore dell'elemento.
draft: false
keywords:
- select html element by class
- load html file java
- how to get element color
- parse html document java
- extract css property value
language: it
og_description: Seleziona l'elemento HTML per classe in Java, carica il file HTML
  in Java ed estrai i valori delle proprietà CSS, come il colore dell'elemento, con
  codice passo‑passo.
og_title: Seleziona elemento HTML per classe in Java – Tutorial completo di programmazione
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Select HTML element by class in Java, learn how to load HTML file Java,
    parse HTML document Java, and extract CSS property value like element color.
  headline: Select HTML Element by Class in Java – Complete Guide
  type: TechArticle
- description: Select HTML element by class in Java, learn how to load HTML file Java,
    parse HTML document Java, and extract CSS property value like element color.
  name: Select HTML Element by Class in Java – Complete Guide
  steps:
  - name: Add jsoup Dependency
    text: 'If you’re using Maven, pop this into your `pom.xml`:'
  - name: Load the Document
    text: '```java import org.jsoup.Jsoup; import org.jsoup.nodes.Document; import
      java.io.File; import java.io.IOException;'
  - name: 3A. Inline Styles (Fast Path)
    text: 'If the element defines `color` directly:'
  - name: 3B. External Stylesheets (Full‑Featured)
    text: 'If the color comes from an external CSS file, you’ll need to load that
      stylesheet and apply the cascade rules yourself. Below is a **simplified** approach
      that works for most static pages:'
  type: HowTo
tags:
- Java
- HTML Parsing
- CSS Extraction
title: Seleziona l'elemento HTML per classe in Java – Guida completa
url: /it/java/css-html-form-editing/select-html-element-by-class-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Selezionare un elemento HTML per classe in Java – Guida completa

Ti è mai capitato di dover **selezionare un elemento HTML per classe in Java** ma non sapevi da dove cominciare? Non sei l’unico: molti sviluppatori incontrano questo ostacolo quando costruiscono scraper, testano componenti UI o generano report da pagine statiche. In questo tutorial caricheremo un file HTML, analizzeremo il documento e **estrarremo la proprietà CSS color** di un elemento target, il tutto usando puro codice Java.

Copriamo tutto, dall’impostare la libreria giusta alla gestione di casi limite come stili mancanti o sovrascritture inline. Alla fine potrai rispondere a domande come *“come ottenere il colore di un elemento”* senza sudare, e avrai uno snippet riutilizzabile da inserire in qualsiasi progetto. Niente superfluo, solo una soluzione pratica e pronta all’uso.

## Prerequisiti

Prima di immergerci, assicurati di avere:

- **Java 11+** (il codice funziona con qualsiasi JDK recente)
- **Maven** o **Gradle** per gestire le dipendenze (nei esempi useremo Maven)
- Familiarità di base con i concetti di HTML e CSS
- Un semplice file HTML (lo chiameremo `sample.html`) posizionato in una directory nota

Se qualcosa ti è poco familiare, fermati qui e sistemalo—ti ringrazierà più tardi quando il codice girerà senza intoppi.

## Passo 1: Caricare il file HTML in Java

La prima cosa di cui abbiamo bisogno è **caricare il file HTML in stile Java**, cioè leggere il file in memoria e passarne il contenuto a un parser. La libreria de‑facto per questo compito è **jsoup**, un parser HTML leggero, con licenza MIT, che gestisce markup malformato in modo elegante.

### Aggiungere la dipendenza jsoup

Se usi Maven, inserisci questo nel tuo `pom.xml`:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Per Gradle, aggiungi:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

### Caricare il documento

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class HtmlColorExtractor {

    public static void main(String[] args) {
        // Adjust the path to point to your actual sample.html location
        File input = new File("YOUR_DIRECTORY/sample.html");
        try {
            // Parse the file using UTF-8 encoding
            Document doc = Jsoup.parse(input, "UTF-8");
            // Proceed to element selection...
            extractColor(doc);
        } catch (IOException e) {
            System.err.println("Failed to load HTML file: " + e.getMessage());
        }
    }
```

**Perché è importante:** `Jsoup.parse(File, String)` legge il file e costruisce un oggetto `Document` simile a un DOM, che è la base per qualsiasi operazione **parse html document java**. Normalizza anche l’HTML, così non devi preoccuparti di tag erranti che rompano la tua logica.

## Passo 2: Selezionare un elemento HTML per classe

Ora che abbiamo un `Document`, possiamo **selezionare un elemento HTML per classe** usando un selettore di tipo CSS. Questo rispecchia il modo in cui i browser ti permettono di interrogare il DOM, rendendo il codice intuitivo.

```java
import org.jsoup.nodes.Element;

private static void extractColor(Document doc) {
    // Example: pick the first <p> with class "intro"
    Element para = doc.selectFirst("p.intro");
    if (para == null) {
        System.out.println("No <p class=\"intro\"> element found.");
        return;
    }
    // Continue to CSS extraction...
    getComputedColor(para);
}
```

**Spiegazione:**  
- `doc.selectFirst("p.intro")` si traduce direttamente in “trova un elemento `<p>` il cui attributo class contiene `intro`”.  
- Se il selettore restituisce `null`, abortiamo in modo elegante—si tratta di un caso limite comune quando la struttura HTML cambia.

## Passo 3: Ottenere il colore dell'elemento (estrarre il valore della proprietà CSS)

La libreria jsoup di Java non calcola gli stili per te perché non è un motore di rendering. Tuttavia, possiamo comunque **come ottenere il colore di un elemento** leggendo l’attributo `style` o consultando un foglio di stile esterno se lo carichi manualmente.

### 3A. Stili inline (percorso veloce)

Se l’elemento definisce `color` direttamente:

```java
private static void getComputedColor(Element element) {
    // Check for an inline style first
    String inlineStyle = element.attr("style"); // e.g., "color: #222; font-weight: bold;"
    String color = extractColorFromStyle(inlineStyle);
    if (color != null) {
        System.out.println("Computed color (inline): " + color);
        return;
    }
    // Fallback to external stylesheet parsing...
    System.out.println("No inline color found; attempting stylesheet lookup.");
}
```

Helper per estrarre la dichiarazione `color` da una stringa di stile grezza:

```java
private static String extractColorFromStyle(String style) {
    if (style == null || style.isEmpty()) return null;
    // Split by semicolon, then look for "color:"
    for (String part : style.split(";")) {
        String trimmed = part.trim().toLowerCase();
        if (trimmed.startsWith("color:")) {
            return trimmed.substring(6).trim(); // Return everything after "color:"
        }
    }
    return null;
}
```

### 3B. Fogli di stile esterni (funzionalità completa)

Se il colore proviene da un file CSS esterno, dovrai caricare quel foglio di stile e applicare le regole di cascata da solo. Di seguito trovi un approccio **semplificato** che funziona per la maggior parte delle pagine statiche:

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;
import java.util.HashMap;
import java.util.Map;

private static void getComputedColor(Element element) {
    // Inline check as before...
    String inlineColor = extractColorFromStyle(element.attr("style"));
    if (inlineColor != null) {
        System.out.println("Computed color (inline): " + inlineColor);
        return;
    }

    // Load all linked CSS files (naïve approach)
    Document doc = element.ownerDocument();
    Elements links = doc.select("link[rel=stylesheet]");
    Map<String, String> cssRules = new HashMap<>();

    for (Element link : links) {
        String href = link.absUrl("href");
        try {
            String css = Jsoup.connect(href).ignoreContentType(true).execute().body();
            parseCssRules(css, cssRules);
        } catch (IOException e) {
            System.err.println("Failed to load stylesheet: " + href);
        }
    }

    // Resolve the most specific rule for the element’s class
    String className = element.className(); // e.g., "intro"
    String selector = "." + className; // ".intro"
    String color = cssRules.get(selector);
    if (color != null) {
        System.out.println("Computed color (external): " + color);
    } else {
        System.out.println("Color not found in inline style or linked stylesheets.");
    }
}
```

**Parsing CSS – un piccolo helper (non un parser completo):**

```java
private static void parseCssRules(String css, Map<String, String> map) {
    // Very basic: split on '}' then on '{' to get selector and declarations
    String[] blocks = css.split("}");
    for (String block : blocks) {
        String[] parts = block.split("\\{");
        if (parts.length != 2) continue;
        String selector = parts[0].trim(); // e.g., ".intro"
        String declarations = parts[1].trim(); // e.g., "color: rgb(34,34,34);"
        String color = extractColorFromStyle(declarations);
        if (color != null) {
            map.put(selector, color);
        }
    }
}
```

**Perché funziona:**  
- Recuperiamo ogni foglio di stile collegato tramite `Jsoup.connect(...).ignoreContentType(true)`, che tratta il CSS come testo semplice.  
- `parseCssRules` costruisce una mappa di selettori ai loro valori `color`.  
- Infine, cerchiamo il selettore di classe dell’elemento (`.intro`) in quella mappa. Questo imita la cascata per casi semplici; per selettori complessi servirebbe un motore CSS completo, ma è oltre lo scopo di questa demo rapida.

## Passo 4: Stampare il colore calcolato sulla console

Mettendo tutto insieme, il metodo `main` finale stampa il colore scoperto:

```java
    public static void main(String[] args) {
        File input = new File("YOUR_DIRECTORY/sample.html");
        try {
            Document doc = Jsoup.parse(input, "UTF-8");
            Element para = doc.selectFirst("p.intro");
            if (para == null) {
                System.out.println("Target element not found.");
                return;
            }
            // Try inline first, then external CSS
            String color = extractColorFromStyle(para.attr("style"));
            if (color != null) {
                System.out.println("Computed color: " + color);
                return;
            }
            // Load external stylesheets (simplified)
            Map<String, String> cssMap = new HashMap<>();
            for (Element link : doc.select("link[rel=stylesheet]")) {
                String href = link.absUrl("href");
                String css = Jsoup.connect(href).ignoreContentType(true).execute().body();
                parseCssRules(css, cssMap);
            }
            String classSelector = "." + para.className();
            String externalColor = cssMap.get(classSelector);
            System.out.println("Computed color: " + (externalColor != null ? externalColor : "unknown"));
        } catch (IOException e) {
            System.err.println("Error: " + e.getMessage());
        }
    }
}
```

**Output previsto** (supponendo che `sample.html` contenga `<p class="intro" style="color: #222;">`):

```
Computed color: #222
```

Oppure, se il colore è definito in un foglio di stile esterno:

```
Computed color: rgb(34, 34, 34)
```

## Consigli pratici e ostacoli comuni

- **URL relativi:** `link.absUrl("href")` risolve automaticamente i percorsi relativi in base alla posizione del documento—non dimenticarlo, altrimenti potresti recuperare il file sbagliato.


## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Caricare documenti HTML da file in Aspose.HTML per Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Come modificare l’albero di un documento HTML in Aspose.HTML per Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Come aggiungere CSS – CSS inline a documenti HTML in Aspose.HTML per Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}