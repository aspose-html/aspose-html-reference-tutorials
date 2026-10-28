---
category: general
date: 2026-10-28
description: Impara come aprire i collegamenti in una nuova scheda analizzando l'HTML
  in Java, trovando i link esterni e aggiungendo target blank.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: it
lastmod: 2026-10-28
og_description: 'Apri i collegamenti in una nuova scheda usando Java: analizza l''HTML,
  individua i link esterni, aggiungi target="_blank" e salva l''HTML modificato.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Apri i link in una nuova scheda con Java – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: Come aprire i collegamenti in una nuova scheda con Java
url: /it/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come aprire i collegamenti in una nuova scheda con Java

Se hai bisogno di **aprire i collegamenti in una nuova scheda** da un file HTML statico, questa guida ti mostra esattamente come farlo. Imparerai a **analizzare HTML in Java**, **trovare collegamenti esterni**, **aggiungere target blank** e **salvare l'HTML modificato** senza uscire dal tuo IDE.

Aprire collegamenti esterni in una nuova scheda del browser migliora l'esperienza dell'utente e mantiene i visitatori sulla pagina originale. La soluzione qui sotto funziona con qualsiasi documento HTML, richiede solo la popolare libreria jsoup e gira su Java 8 o versioni successive.

## Prerequisiti

* JDK 8 + installato  
* Uno strumento di build (Maven o Gradle) per includere la dipendenza **jsoup**  
* Un file HTML che contiene tag di ancoraggio con la classe `external`

Non è necessario un server web o framework aggiuntivi—jsoup gestisce tutto localmente.

## Passo 1: Configura jsoup nel tuo progetto

Aggiungi jsoup come dipendenza. Se usi Maven, inserisci questo in `pom.xml`:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Per Gradle, aggiungi la seguente riga a `build.gradle`:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Queste coordinate scaricano l'ultima versione stabile (a ottobre 2026). Dopo la sincronizzazione, puoi importare le classi `org.jsoup` nei tuoi file sorgente Java.

## Passo 2: Analizza il documento HTML

Analizzare il file è il primo passo verso **open links new tab**. Il metodo `Jsoup.parse` legge il file in una struttura DOM‑like mutabile.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*Perché è importante*: `Document` ti fornisce selettori in stile CSS, rendendo banale individuare gli elementi di cui hai bisogno.

## Passo 3: Trova i collegamenti esterni

Ora individua ogni elemento `<a>` che possiede la classe `external`. Questo soddisfa il requisito **find external links**.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` è una collezione di nodi corrispondenti. Se il selettore restituisce un set vuoto, il tuo HTML o non contiene la classe o utilizza una convenzione di denominazione diversa—adatta il selettore di conseguenza.

## Passo 4: Aggiungi `target="_blank"` a ogni collegamento

Per ogni nodo restituito da **find external links**, imposta l'attributo `target` a `_blank`. Questo soddisfa il passo **add target blank** e garantisce che i browser aprano il collegamento in una nuova scheda.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

Il metodo `attr` sovrascrive qualsiasi valore `target` esistente, garantendo un comportamento coerente per tutti gli ancoraggi esterni.

## Passo 5: Salva l'HTML modificato

Dopo aver aggiornato il DOM, scrivi le modifiche su un file. Questo completa la parte **save modified html** del tutorial.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` serializza l'intero documento, preservando rientri e formattazione così come jsoup lo ha originariamente analizzato.

## Esempio completo funzionante

Unendo tutti i passaggi ottieni un programma autonomo che puoi copiare, incollare ed eseguire.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### Output previsto

Supponiamo che `sample.html` contenga:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

Dopo aver eseguito il programma, `updated.html` conterrà:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

Solo il collegamento esterno ha ricevuto l'attributo `target="_blank"`, il che significa che i browser lo apriranno ora in una nuova scheda.

## Consigli professionali e problemi comuni

* **Consiglio pro:** Se devi trattare i collegamenti che iniziano con `http://` o `https://` come esterni anche senza una classe CSS, espandi il selettore: `doc.select("a[href^=http]")`.
* **Caso limite:** Alcune pagine specificano già `target="_self"`; la chiamata `attr` lo sovrascrive, garantendo un comportamento coerente.
* **Prestazioni:** Per file HTML molto grandi, considera l'analisi in streaming (`Jsoup.parse(File, String, String, Parser.htmlParser())`) per ridurre l'uso della memoria.
* **Test:** Verifica il risultato aprendo `updated.html` in un browser e ispezionando il collegamento con gli strumenti per sviluppatori—cerca l'attributo `target`.

## Conclusione

Ora hai una soluzione completa e eseguibile per **open links in a new tab** usando Java. Il tutorial ha coperto come **parse html in java**, **find external links**, **add target blank**, e **save modified html**, tutto con la leggera libreria jsoup.

Da qui puoi:

* Estendere il selettore per gestire altri pattern di collegamento (ad es., `rel="external"`).  
* Combinare questa logica con un passaggio di build che elabora tutti i file HTML in un progetto.  
* Integrare il codice in una pipeline di gestione dei contenuti più ampia.

Sentiti libero di sperimentare con diversi selettori o formati di output, e condividi i tuoi risultati con la community!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Create new html element with Java – Full Aspose.HTML Guide](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}