---
category: general
date: 2026-09-29
description: Cambia il colore di sfondo con JavaScript in un file HTML usando Java.
  Impara a caricare HTML in Java, eseguire JS in HTML e modificare l'HTML con Java
  per un nuovo sfondo della pagina.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change background color javascript
- load html in java
- run js in html
- modify html with java
- set page background
language: it
lastmod: 2026-09-29
og_description: Cambia il colore di sfondo con JavaScript in una pagina HTML usando
  Java. Questo tutorial ti mostra come caricare HTML in Java, eseguire JS in HTML
  e impostare lo sfondo della pagina programmaticamente.
og_image_alt: Screenshot of Java code that changes the page background color
og_title: Cambia il colore di sfondo con JavaScript e Java – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Change background color javascript in an HTML file using Java. Learn
    to load html in java, run js in html, and modify html with java for a new page
    background.
  headline: How to change background color javascript using Java
  type: TechArticle
tags:
- Java
- HTMLUnit
- JavaScript
- HTML manipulation
title: Come cambiare il colore di sfondo con JavaScript usando Java
url: /it/java/editing-html-documents/how-to-change-background-color-javascript-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come cambiare il colore di sfondo con JavaScript usando Java

Se hai bisogno di **cambiare il colore di sfondo con JavaScript** in un file HTML esistente, puoi farlo interamente da Java senza aprire un browser. Questo tutorial ti mostra come **caricare html in java**, eseguire un piccolo snippet JavaScript e poi **modificare html con java** affinché lo sfondo della pagina venga aggiornato.  

La soluzione funziona con la libreria open‑source **HTMLUnit**, che fornisce un browser headless capace di valutare JavaScript esattamente come farebbe un browser reale. Alla fine di questa guida avrai a disposizione un metodo riutilizzabile che **imposta lo sfondo della pagina** su qualsiasi colore tu scelga.

## Prerequisiti

| Cosa ti serve | Perché è importante |
|---------------|---------------------|
| Java 8 o superiore | HTMLUnit richiede almeno Java 8. |
| Strumento di build Maven o Gradle | Per scaricare automaticamente la dipendenza HTMLUnit. |
| Un file HTML da modificare (ad es., `input.html`) | Il documento sorgente che verrà caricato e alterato. |

Aggiungi HTMLUnit al tuo progetto:

*Maven*  

```xml
<dependency>
    <groupId>net.sourceforge.htmlunit</groupId>
    <artifactId>htmlunit</artifactId>
    <version>2.71.0</version>
</dependency>
```

*Gradle*  

```gradle
implementation 'net.sourceforge.htmlunit:htmlunit:2.71.0'
```

> **Pro tip:** Usa l'ultima versione stabile di HTMLUnit per ottenere il motore JavaScript più accurato.

## Cambiare il colore di sfondo con JavaScript – caricare HTML in Java

Il primo passo è caricare il documento HTML in un oggetto `HTMLPage`. Questo ti fornisce un'API simile al DOM e un contesto di esecuzione JavaScript.

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;

public class BackgroundColorChanger {

    /**
     * Loads an HTML file from the given path.
     *
     * @param htmlPath absolute or relative path to the source HTML file
     * @return HtmlPage representing the loaded document
     * @throws IOException if the file cannot be read
     */
    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        // WebClient acts as a headless browser; disabling CSS speeds up loading.
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);

        // Convert the file path to a URL that HTMLUnit can understand.
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }
}
```

*Perché è importante*: `WebClient` crea un ambiente sandbox dove JavaScript può essere eseguito, così puoi **eseguire js in html** esattamente come farebbe il browser di un utente.

## Eseguire js in html per impostare lo sfondo della pagina

Una volta che la pagina è caricata, puoi valutare qualsiasi espressione JavaScript. Lo snippet qui sotto modifica lo stile `backgroundColor` dell'elemento `<body>`.

```java
/**
 * Executes JavaScript that changes the page background color.
 *
 * @param page   the HtmlPage loaded earlier
 * @param color  any valid CSS color string, e.g., "lightblue" or "#ffcc00"
 */
private static void changeBackground(HtmlPage page, String color) {
    // The eval method runs JavaScript in the page's context.
    String script = "document.body.style.backgroundColor = '" + color + "';";
    page.getEnclosingWindow().getScriptableObject().eval(script);
}
```

*Spiegazione*:  
- `document.body.style.backgroundColor` è la proprietà DOM standard per lo sfondo della pagina.  
- Chiamando `eval`, **eseguiamo js in html** senza la necessità di una finestra browser reale.  
- Il metodo è riutilizzabile per qualsiasi colore, soddisfacendo il requisito di **impostare lo sfondo della pagina**.

## Modificare html con java e salvare il risultato

Dopo l'esecuzione dello script, il DOM riflette il nuovo stile. Ora puoi scrivere l'HTML aggiornato su disco.

```java
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Saves the modified HTML content to a new file.
 *
 * @param page          the HtmlPage that has been altered
 * @param outputPath    destination file path
 * @throws IOException  if writing fails
 */
private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
    // page.asXml() returns the current HTML markup, including the changed style.
    String updatedHtml = page.asXml();
    Files.write(Paths.get(outputPath), updatedHtml.getBytes());
}
```

Unire tutti i passaggi ti fornisce un unico programma eseguibile:

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class BackgroundColorChanger {

    public static void main(String[] args) {
        // Adjust these paths for your environment.
        String inputFile = "YOUR_DIRECTORY/input.html";
        String outputFile = "YOUR_DIRECTORY/js_modified.html";
        String newColor = "lightblue"; // Change to any CSS color you need.

        try {
            HtmlPage page = loadHtml(inputFile);
            changeBackground(page, newColor);
            saveModifiedHtml(page, outputFile);
            System.out.println("Background color changed to '" + newColor + "' and saved to " + outputFile);
        } catch (IOException e) {
            System.err.println("Error processing HTML file: " + e.getMessage());
        }
    }

    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }

    private static void changeBackground(HtmlPage page, String color) {
        String script = "document.body.style.backgroundColor = '" + color + "';";
        page.getEnclosingWindow().getScriptableObject().eval(script);
    }

    private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
        String updatedHtml = page.asXml();
        Files.write(Paths.get(outputPath), updatedHtml.getBytes());
    }
}
```

### Output previsto

L'esecuzione del programma stampa:

```
Background color changed to 'lightblue' and saved to YOUR_DIRECTORY/js_modified.html
```

Aprendo `js_modified.html` in qualsiasi browser, la pagina appare con uno sfondo azzurro chiaro, confermando che l'operazione di **cambiare il colore di sfondo con JavaScript** è riuscita.

## Varianti comuni e casi limite

| Situazione | Come gestirla |
|------------|---------------|
| **Formati di colore diversi** | Passa qualsiasi valore compatibile CSS (`"red"`, `"#ff0000"`, `"rgb(255,0,0)"`). |
| **Tag `<body>` mancante** | Lo script fallirà silenziosamente; puoi prima assicurarti che `<body>` esista con `page.getFirstByXPath("//body")`. |
| **File HTML di grandi dimensioni** | Disabilita il CSS (`setCssEnabled(false)`) e attiva solo le funzionalità JavaScript necessarie per ridurre l'uso di memoria. |
| **Esecuzione di più script** | Chiama `changeBackground` più volte o crea un metodo di utilità che accetti una lista di comandi JavaScript. |

## Conclusione

Ora sai come **cambiare il colore di sfondo con JavaScript** caricando un file HTML in Java, **eseguire js in html**, e **modificare html con java** per **impostare lo sfondo della pagina** su qualsiasi colore tu desideri. L'esempio completo sopra funziona con l'ultima versione della libreria HTMLUnit e può essere integrato in pipeline di automazione più ampie, come l'elaborazione batch di report HTML o la preparazione di template email.

**Passi successivi**  
- Esplora altre manipolazioni del DOM (ad es., inserire elementi, rimuovere script).  
- Combina questo approccio con un renderer PDF per generare PDF delle pagine stilizzate.  
- Prova a usare un motore headless diverso, come Selenium WebDriver, se ti serve una fedeltà completa del browser.

Happy coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Get Computed Style Java – Extract Background Color from HTML](/html/english/java/css-html-form-editing/get-computed-style-java-extract-background-color-from-html/)
- [How to Load HTML, Set Device DPI & Read Background Color](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Generate HTML from JavaScript in Java – Complete Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/generate-html-from-javascript-in-java-complete-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}