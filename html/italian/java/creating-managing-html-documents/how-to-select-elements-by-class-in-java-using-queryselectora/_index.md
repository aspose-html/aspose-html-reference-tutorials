---
category: general
date: 2026-09-29
description: Impara a selezionare gli elementi per classe, leggere l'HTML da un file
  e trovare i link esterni in Java. Questa guida passo‑passo copre l'iterazione efficiente
  di una NodeList.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: it
lastmod: 2026-09-29
og_description: Seleziona gli elementi per classe in Java, leggi l'HTML da un file
  e trova i collegamenti esterni usando querySelectorAll. Segui l'esempio completo
  per iterare un NodeList.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Seleziona gli elementi per classe in Java – guida completa con querySelectorAll
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: Come selezionare gli elementi per classe in Java usando querySelectorAll
url: /it/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come selezionare gli elementi per classe in Java usando querySelectorAll

Se hai bisogno di **selezionare gli elementi per classe** durante l'elaborazione di un file HTML in Java, questa guida ti mostra esattamente come farlo. Imparerai a leggere l'HTML da un file, usare `querySelectorAll` per trovare i link esterni e iterare in modo sicuro il `NodeList` risultante.

Lavorare con HTML in Java spesso sembra pesante, ma le librerie moderne ti offrono un'API concisa basata sui selettori CSS. L'esempio qui sotto utilizza **jsoup** (versione 1.17.2) perché implementa selettori in stile `querySelectorAll` e restituisce una collezione `Elements` che si comporta come un `NodeList`. Puoi adattare la stessa logica ad altre implementazioni DOM se necessario.

## Prerequisiti

* JDK 17 o versioni successive installato.
* Maven o Gradle per la gestione delle dipendenze.
* Familiarità di base con gli stream Java e il modello DOM.

Add jsoup to your project:

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## Passo 1: Leggere l'HTML da file

Il primo compito è caricare il documento HTML dal disco. `Jsoup.parse(Path, Charset)` legge il file e costruisce un albero DOM su cui puoi eseguire query.

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*Perché è importante*: Caricare il file una sola volta evita I/O ripetuti mentre itera sugli elementi in seguito. L'oggetto `Document` contiene l'intero DOM, consentendo query di selettori rapide.

## Passo 2: Usare `querySelectorAll` per selezionare gli elementi per classe

Ora che il documento è in memoria, puoi **selezionare gli elementi per classe** usando un selettore CSS. Il selettore `"a.external"` corrisponde ai tag `<a>` che possiedono la classe `external`—esattamente ciò che ti serve per **trovare i link esterni**.

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*Perché è importante*: Usare un selettore di classe è sia espressivo che performante. La libreria traduce il selettore in un attraversamento ottimizzato, così non è necessario scrivere loop manuali su ogni nodo.

## Passo 3: Iterare il NodeList (Elements) in Java

`Elements` implementa `Iterable<Element>`, il che significa che puoi usare un normale ciclo `for‑each` per **iterare NodeList Java**. Il ciclo qui sotto stampa l'attributo `href` di ogni link.

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*Perché è importante*: L'iterazione diretta mantiene il codice leggibile ed evita l'overhead di convertire la collezione in uno stream quando ti serve solo un output semplice.

## Esempio completo funzionante

Unendo i tre passaggi ottieni un programma autonomo che puoi eseguire dalla riga di comando.

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### Output previsto

Assuming `input.html` contains:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

Running the program prints:

```
External link: https://example.com
External link: https://openai.com
```

## Consigli professionali e problemi comuni

* **L'encoding è importante** – Leggi sempre il file con UTF‑8 (o il charset che corrisponde alla tua sorgente). Un encoding errato può corrompere i caratteri nei valori degli attributi.
* **Classi multiple** – Se un elemento ha diverse classi (ad esempio `class="btn external"`), il selettore `"a.external"` corrisponde comunque perché i selettori di classe CSS verificano la presenza del token, non la stringa esatta.
* **Suggerimento di performance** – Se ti serve solo l'attributo `href`, puoi richiederlo direttamente con `doc.select("a.external[href]").eachAttr("href")`. Questo evita di creare oggetti `Element` completi per ogni corrispondenza.
* **Sicurezza contro i null** – `link.attr("href")` restituisce una stringa vuota se l'attributo è mancante, quindi non è necessario un controllo null prima di stampare.

## Domande frequenti

**Q: Funziona con frammenti HTML che non hanno una radice `<html>`?**  
A: Sì. `Jsoup.parse` tratta l'input come un frammento e aggiunge automaticamente gli elementi radice mancanti, consentendo ai selettori di operare sul body del frammento.

**Q: Posso usare `querySelectorAll` senza jsoup?**  
A: L'API DOM standard di Java (`org.w3c.dom`) non include `querySelectorAll`. Librerie come **HTMLUnit** o **jodd-lagarto** forniscono metodi simili. Il pattern mostrato qui—caricare, selezionare con CSS, iterare—rimane lo stesso.

**Q: E se devo modificare i link invece di stamparli?**  
A: Dopo aver ottenuto ogni `Element`, puoi chiamare `link.attr("href", "newUrl")` e poi scrivere il documento su disco con `Files.writeString`.

## Conclusione

Ora sai come **selezionare gli elementi per classe**, **leggere l'HTML da file**, **trovare i link esterni** e **iterare un NodeList in Java** usando selettori in stile `querySelectorAll`. L'esempio completo dimostra un flusso di lavoro pulito e pronto per la produzione che puoi integrare in pipeline di scraping o trasformazione più ampie.

Successivamente, esplora argomenti correlati come **analizzare contenuti dinamici con HTMLUnit**, **scrivere HTML modificato su disco**, o **usare gli stream Java per raccogliere gli URL dei link in una lista**. Ognuno di questi si basa sulla tecnica fondamentale di selezione basata su classi mostrata qui. Buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come interrogare HTML in Java – Selezionare elementi, filtrare per attributo e ottenere il testo](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [Iterare NodeList Java – Leggere HTML e ottenere src dell'immagine](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Caricare documenti HTML da file in Aspose.HTML per Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}