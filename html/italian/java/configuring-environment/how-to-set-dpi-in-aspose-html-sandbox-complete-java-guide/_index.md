---
category: general
date: 2026-04-02
description: Scopri come impostare DPI, dimensione della viewport e user agent in
  Aspose.HTML Sandbox. Esempio Java passo‑passo con codice completo e consigli.
draft: false
keywords:
- how to set dpi
- set viewport size
- set user agent
- Aspose.HTML sandbox
- Java rendering settings
language: it
og_description: Padroneggia come impostare DPI, la dimensione della viewport e l'user
  agent in Aspose.HTML Sandbox con un esempio Java completo.
og_title: Come impostare DPI nella Sandbox di Aspose.HTML – Tutorial Java
tags:
- Aspose.HTML
- Java
- Rendering
- Sandbox
title: Come impostare DPI in Aspose.HTML Sandbox – Guida completa Java
url: /it/java/configuring-environment/how-to-set-dpi-in-aspose-html-sandbox-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come impostare DPI in Aspose.HTML Sandbox – Guida completa Java

Ti sei mai chiesto **come impostare DPI** durante il rendering di una pagina web con Aspose.HTML? Non sei l’unico. In molti scenari di test è necessario che il layout corrisponda a una densità di schermo specifica—pensa a PDF pronti per la stampa o screenshot ad alta risoluzione. La buona notizia è che il sandbox di Aspose.HTML ti consente di controllare DPI, dimensione del viewport e persino la stringa user‑agent, tutto in un unico pacchetto ordinato.

In questo tutorial percorreremo un esempio pratico in Java che **imposta DPI**, **imposta la dimensione del viewport** e **imposta lo user agent** contemporaneamente. Alla fine avrai un programma eseguibile, saprai perché ogni impostazione è importante e sarai pronto a personalizzare il sandbox per i tuoi progetti.

---

## Cosa ti servirà

- **Java 17** (o qualsiasi JDK recente; l’API è compatibile con Java 8+)
- Libreria **Aspose.HTML for Java** (versione 23.12 o successiva)
- Un IDE o un semplice editor di testo + compilazione da riga di comando
- Accesso a Internet per l’URL di esempio (`https://example.com`)

Non sono necessari strumenti di build esterni; il codice si compila con `javac` e si esegue con `java`. Se preferisci Maven o Gradle, aggiungi semplicemente la dipendenza Aspose.HTML—nulla di complicato.

---

## Step 1: Crea un Sandbox che definisce l’Ambiente di Rendering

Il sandbox è dove dici ad Aspose.HTML quale “schermo” stai simulando. Qui impostiamo un **viewport di 1024 × 768**, un **DPI di 96** e una stringa **user‑agent personalizzata**.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Define the sandbox – this is the core of how to set dpi, viewport, and user agent.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent
```

**Perché è importante:**  
- **DPI** influisce su come le unità CSS `pt` vengono tradotte in pixel; un DPI più alto produce un rendering più nitido.  
- **Dimensione del viewport** determina i breakpoint di layout che il CSS responsive attiverà.  
- **User‑agent** può attivare variazioni di contenuto lato server (mobile vs desktop).

> **Pro tip:** Se in seguito genererai PDF, abbina il DPI alla risoluzione di stampa desiderata (ad es., 300 dpi per stampe di alta qualità).

---

## Step 2: Carica una Pagina Web all’interno del Sandbox

Ora puntiamo il sandbox a un URL. Il costruttore `HTMLDocument` accetta il sandbox, così il motore di layout rispetta le impostazioni appena definite.

```java
        // Load the page using the sandbox we just configured.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {
```

**Cosa succede dietro le quinte?**  
Aspose.HTML crea un contesto di rendering isolato, simile a un browser headless, ma senza l’onere di un’intera istanza Chromium. Questo rende l’operazione veloce e leggera in termini di memoria—perfetta per l’elaborazione batch.

---

## Step 3: Interagisci con il DOM – Leggi il Titolo della Pagina

Per dimostrazione estrarremo il titolo e lo stamperemo. In uno scenario reale potresti fare uno screenshot, esportare in PDF o estrarre dati.

```java
            // Simple DOM interaction – fetch and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());
        }
    }
}
```

**Output previsto** (quando `https://example.com` è raggiungibile):

```
Title inside sandbox: Example Domain
```

Se il sito restituisce un titolo diverso, vedrai quello al posto di questo—non è necessario modificare altro.

---

## Step 4: Verifica le Impostazioni (Debug Opzionale)

A volte vuoi ricontrollare che il sandbox rispetti davvero DPI e viewport. Aspose.HTML non espone direttamente questi valori, ma puoi dedurli misurando le dimensioni degli elementi.

```java
        // Example: measure a known element's width in pixels.
        int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
        System.out.println("Measured width (px): " + elementWidth);
```

Se sai che il CSS dichiara l’elemento come `width: 200pt;`, a **96 dpi** dovresti vedere `200pt * (96/72) ≈ 267px`. Modifica il DPI e riesegui per vedere il numero cambiare—prova che **come impostare DPI** funziona davvero.

---

## Codice Completo in Un Unico Blocco

Copia‑incolla il seguente codice in `SandboxExample.java`. Si compila così com’è; assicurati solo che il JAR di Aspose.HTML sia nel classpath.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox that defines the rendering environment
        // (viewport size 1024×768 and 96 dpi) and a custom user‑agent string.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent

        // Step 2: Load a web page inside the sandbox so layout respects the settings.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {

            // Step 3: Interact with the DOM – here we simply read and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());

            // Optional: verify DPI effect by measuring an element (if you know its CSS size).
            // int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
            // System.out.println("Measured width (px): " + elementWidth);
        }
    }
}
```

Compila ed esegui:

```bash
javac -cp "aspose-html-23.12.jar" SandboxExample.java
java -cp ".:aspose-html-23.12.jar" SandboxExample
```

Dovresti vedere il titolo stampato, confermando che il sandbox funziona con il **DPI impostato**, la **dimensione del viewport impostata** e lo **user agent impostato** che hai fornito.

---

## Domande Frequenti & Casi Limite

### E se avessi bisogno di un DPI diverso?

Basta cambiare il secondo argomento di `DocumentSandbox`. Per PDF pronti per la stampa potresti usare `300`:

```java
new DocumentSandbox(new Size(1024, 768), 300, "MyCustomUserAgent/1.0");
```

Un DPI più alto genera dimensioni pixel maggiori per gli stessi punti CSS, migliorando la qualità raster ma consumando più memoria.

### Posso caricare un file HTML locale invece di un URL?

Assolutamente. Sostituisci l’URL con un percorso file:

```java
HTMLDocument webDoc = new HTMLDocument("file:///C:/myfolder/page.html", renderingSandbox);
```

Assicurati che il percorso sia assoluto e utilizzi lo schema `file:///`.

### Come cambio lo user‑agent dopo aver creato il sandbox?

Il sandbox è immutabile—una volta passato a `HTMLDocument`, le impostazioni sono bloccate. Per usare uno user‑agent diverso, crea un nuovo `DocumentSandbox` con la stringa desiderata.

### Aspose.HTML supporta l’esecuzione di JavaScript?

Sì, il motore esegue la maggior parte degli script client‑side. Se uno script modifica il DOM dopo il caricamento, puoi attendere un po’:

```java
webDoc.waitForLoad();
```

Oppure usare una logica simile a `setTimeout` all’interno della pagina prima di interrogare gli elementi.

---

## Conferma Visiva (Immagine)

Di seguito è mostrato uno screenshot della console che evidenzia l’esecuzione riuscita. Nota come l’output del titolo corrisponda alla pagina, confermando che il sandbox ha rispettato le nostre impostazioni.

![Console output showing how to set dpi in Aspose.HTML Sandbox](/images/console-output.png)

*Alt text:* *Output della console che dimostra come impostare DPI, dimensione del viewport e user agent in Aspose.HTML Sandbox.*

---

## Riepilogo & Prossimi Passi

Abbiamo coperto **come impostare DPI** (96 dpi nell’esempio), **come impostare la dimensione del viewport** (1024 × 768) e **come impostare lo user agent** (stringa personalizzata) usando l’API sandbox di Aspose.HTML. Il programma Java completo e funzionante dimostra che queste impostazioni non sono solo teoriche—affectano direttamente il rendering e l’interazione con il DOM.

Pronto per andare oltre?

- **Esporta in PDF:** Dopo aver caricato la pagina, chiama `webDoc.save("output.pdf", SaveFormat.PDF);` per generare un PDF ad alta risoluzione che rispecchia il DPI impostato.  
- **Cattura uno Screenshot:** Usa `webDoc.renderToBitmap("screenshot.png");` per immagini pixel‑perfect.  
- **Gioca con Layout Responsive:** Cambia le dimensioni del viewport per testare i breakpoint mobile senza un dispositivo reale.  

Sperimenta con valori DPI diversi, combinazioni di viewport e user‑agent per vedere come server e CSS reagiscono. Il sandbox è un playground leggero che ti evita di avviare browser completi.

---

### Continua a Esplorare

- **Documentazione Aspose.HTML** – approfondisci le opzioni di `DocumentSandbox`.  
- **Media Queries CSS Avanzate** – scopri come la dimensione del viewport attiva stili diversi.  
- **User‑Agent Spoofing** – scopri come alcuni siti forniscono markup alternativo in base alla stringa agent.

Hai domande o un caso difficile? Lascia un commento e risolviamo insieme. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}