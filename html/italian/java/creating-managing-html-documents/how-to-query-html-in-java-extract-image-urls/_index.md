---
category: general
date: 2026-03-05
description: Come interrogare l'HTML in Java per leggere un file HTML ed estrarre
  le immagini. Impara a leggere un file HTML in Java, ottenere gli URL delle immagini
  in Java e iterare su NodeList in Java.
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: it
og_description: Come interrogare l'HTML in Java e recuperare gli URL delle immagini.
  Questa guida mostra come leggere un file HTML in Java, individuare le immagini e
  iterare su NodeList in Java.
og_title: Come interrogare l'HTML in Java – Estrarre gli URL delle immagini
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: Come interrogare l'HTML in Java – Estrarre gli URL delle immagini
url: /it/java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come interrogare HTML in Java – Estrarre gli URL delle immagini

Ti sei mai chiesto **come interrogare HTML** in Java per estrarre tutte le immagini da una pagina? Non sei l'unico: gli sviluppatori hanno spesso bisogno di leggere file HTML, fare scraping delle immagini e poi fare qualcosa di utile con gli URL. In questo tutorial vedremo un esempio pratico che mostra esattamente **come interrogare HTML**, leggere un file HTML in stile Java e ottenere gli URL delle immagini in Java.

Useremo Aspose.HTML per Java, ma i concetti—XPath, selettori CSS e iterazione su un `NodeList`—si applicano a qualsiasi libreria DOM. Alla fine di questa guida sarai a tuo agio con **come estrarre immagini**, saprai **come iterare su NodeList Java** e avrai a disposizione uno snippet di codice pronto da inserire nel tuo progetto.

![Come interrogare HTML in Java esempio](https://example.com/placeholder.png "Come interrogare HTML in Java")

---

## Cosa imparerai

- Caricare un documento HTML dal disco (read HTML file Java)
- Individuare i tag `<img>` usando sia XPath che i selettori CSS (how to extract images)
- Scorrere il `NodeList` risultante (iterate over NodeList Java)
- Stampare l'attributo `src` di ogni immagine (get image URLs Java)

Nessun servizio esterno, nessuno strumento di build complesso—solo Java puro e una singola dipendenza Maven.

---

## Prerequisiti

- Java 8 o versioni successive installate
- Maven o Gradle per la gestione delle dipendenze
- Familiarità di base con la struttura HTML
- Facoltativo ma utile: un semplice file HTML (`sample.html`) contenente alcuni elementi `<figure><img …></figure>`

Se hai tutto questo, possiamo cominciare subito.

---

## Passo 1: Read HTML File Java – Caricare il documento

Prima di tutto: dobbiamo portare l'HTML in memoria. La classe `HTMLDocument` di Aspose.HTML fa il lavoro pesante. Pensala come aprire un libro così da poter sfogliare qualsiasi pagina.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.NodeList;
import com.aspose.html.dom.Element;

/**
 * Demonstrates how to query HTML in Java and extract image URLs.
 */
public class QueryExample {
    public static void main(String[] args) throws Exception {

        // ① Load the HTML document from a local file.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

**Perché è importante:** Il caricamento del file ti fornisce un albero DOM su cui poter eseguire query. Se il percorso è errato otterrai una `FileNotFoundException`, quindi verifica la posizione prima di eseguire.

---

## Passo 2: Individuare le immagini con XPath – How to Extract Images

XPath è un linguaggio di query potente che ti permette di individuare i nodi con precisione laser. Qui chiediamo tutti i `<img>` all'interno di un `<figure>` che abbia anche un attributo `alt`.

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**Perché XPath?** È conciso e funziona anche quando l'HTML è disordinato. L'espressione `//figure/img[@alt]` si traduce in: “qualsiasi `<img>` sotto un `<figure>` che possiede un attributo `alt`.” Se devi filtrare per altri attributi, basta modificare le parentesi quadre.

---

## Passo 3: Individuare le immagini con CSS Selector – Alternative Way to Extract Images

A volte preferisci la sintassi CSS perché rispecchia ciò che scrivi nei fogli di stile. `querySelectorAll` accetta lo stesso selettore che useresti in un browser.

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**Perché entrambi?** Mostrare entrambe le opzioni ti permette di scegliere lo strumento con cui ti senti più a tuo agio. In pratica ne useresti uno solo, ma avere entrambi gli esempi rende il tutorial più completo.

---

## Passo 4: Iterate Over NodeList Java – Ottenere gli URL delle immagini Java

Ora che abbiamo una collezione, dobbiamo percorrerla. È qui che entra in gioco **iterate over NodeList Java**. Estrarremo l'attributo `src` di ogni immagine e lo stamperemo.

```java
        // ④ Loop through the NodeList returned by the CSS query.
        for (int i = 0; i < cssImages.getLength(); i++) {
            Element imageElement = (Element) cssImages.item(i);
            // Extract the "src" attribute – that’s the image URL.
            System.out.println("Image src: " + imageElement.getAttribute("src"));
        }
    }
}
```

**Perché un classico ciclo `for`?** Il `NodeList` di Aspose non implementa `Iterable`, quindi la sintassi `for‑each` migliorata non compila. Usare un ciclo con indice è il modo affidabile per **iterate over NodeList Java**.

---

## Output previsto

Eseguendo il programma su un HTML di esempio come:

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

Otterrai qualcosa di simile a:

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

Se il tuo file contiene più tag `<img>` che soddisfano i criteri, il numero aumenterà di conseguenza.

---

## Problemi comuni e consigli professionali

- **Problemi di percorso file:** Usa un percorso assoluto o posiziona `sample.html` relativo alla directory di lavoro del tuo progetto.  
- **Attributo `alt` mancante:** Le nostre query XPath/CSS filtrano su `[@alt]`. Se ti servono *tutte* le immagini, rimuovi il filtro sull'attributo (`//figure/img` o `figure img`).  
- **Performance:** Per documenti molto grandi, considera i parser in streaming, ma per la maggior parte dei compiti di web‑scraping l'approccio DOM è sufficiente.  
- **Problemi di codifica:** Aspose.HTML rispetta il charset dichiarato nell'HTML. Se vedi caratteri illeggibili, assicurati che il file sia salvato in UTF‑8.  

---

## Estendere l'esempio

Ora che sai **get image URLs Java**, potresti voler:

1. **Scaricare le immagini** usando `java.net.URL` e `Files.copy`.  
2. **Memorizzare gli URL in un database** per elaborazioni future.  
3. **Filtrare per estensione file** (`src.endsWith(".png")`).  

Tutte queste sono estensioni semplici del ciclo mostrato al Passo 4.

---

## Conclusione

In questa guida abbiamo coperto **come interrogare HTML** in Java dall'inizio alla fine: caricamento del file, individuazione delle immagini con XPath e selettori CSS, e **iterare su NodeList Java** per stampare il `src` di ogni immagine. Ora hai una solida base per **come estrarre immagini**, e sai esattamente **come leggere HTML file Java** usando Aspose.HTML.

Sentiti libero di adattare il codice alle tue esigenze di scraping—che si tratti di estrarre altri attributi, gestire tag `<a>`, o passare gli URL a un downloader. Il modello rimane lo stesso: carica, interroga, itera e agisci.

Hai domande o vuoi condividere un caso d'uso interessante? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}