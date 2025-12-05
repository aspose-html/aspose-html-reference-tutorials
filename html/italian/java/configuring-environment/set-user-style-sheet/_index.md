---
date: 2025-12-05
description: Scopri come creare PDF da HTML impostando un foglio di stile personalizzato
  per l'utente in Aspose.HTML per Java e converti facilmente HTML in PDF con il servizio
  User Agent.
language: it
linktitle: Set User Style Sheet in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Crea PDF da HTML – Imposta foglio di stile utente in Aspose.HTML per Java
url: /java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PDF da HTML – Imposta Foglio di Stile Utente in Aspose.HTML per Java

## Introduzione
In questo tutorial imparerai a **creare PDF da HTML** usando Aspose.HTML per Java applicando un foglio di stile utente personalizzato.  
Ti è mai capitato di voler modificare l'aspetto dei tuoi documenti HTML con uno stile unico? Immagina di creare una pagina web e di aver bisogno che i titoli risaltino con un colore specifico o che i paragrafi abbiano un aspetto coerente su tutti i dispositivi. È qui che entra in gioco un *foglio di stile utente* e il **User Agent Service**. Ti guideremo passo passo—dalla scrittura di un semplice file HTML, alla configurazione dell'user agent, fino alla **conversione da HTML a PDF**—così potrai vedere subito il risultato.

## Risposte Rapide
- **Cosa significa “creare PDF da HTML”?** Significa renderizzare un documento HTML (con CSS, immagini, font, ecc.) e salvare l'output visivo come file PDF.  
- **Quale componente Aspose è necessario?** La libreria Aspose.HTML per Java fornisce il motore di conversione e il User Agent Service.  
- **Ho bisogno di una licenza per i test?** Una versione di prova gratuita è sufficiente per lo sviluppo; è necessaria una licenza commerciale per la produzione.  
- **Posso usare un file CSS esterno?** Sì – puoi collegare fogli di stile esterni proprio come in un browser normale.  
- **Quanto tempo richiede la conversione?** Per un documento semplice come quello di questa guida, la conversione avviene in meno di un secondo.

## Prerequisiti
Prima di immergerci nel codice, assicurati di avere quanto segue:

1. **Aspose.HTML for Java** – scarica l'ultimo JAR dalla [pagina di rilascio di Aspose](https://releases.aspose.com/html/java/).  
2. **Java Development Kit (JDK) 8+** – assicurati che `java -version` restituisca 8 o superiore.  
3. **IDE** – IntelliJ IDEA, Eclipse o NetBeans vanno bene.  
4. **Conoscenza di base di HTML/CSS** – utile ma non obbligatoria.

## Importa Pacchetti
Per iniziare, importa le classi Java essenziali. L'unica importazione esplicita necessaria per questo esempio è `java.io.IOException`; le classi Aspose sono referenziate con i nomi completamente qualificati più avanti.

```java
import java.io.IOException;
```

## Passo 1: Crea un Documento HTML Semplice
Per prima cosa, scriveremo un file HTML minimale (`document.html`) che servirà come sorgente per la nostra conversione in PDF.

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Consiglio:** Mantieni il file HTML nella stessa directory del tuo codice Java per evitare problemi legati ai percorsi.

## Passo 2: Configura Aspose.HTML
Crea un oggetto `Configuration`. Questo oggetto funge da contenitore per tutti i servizi (incluso il User Agent Service) che utilizzerai in seguito.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Passo 3: Accedi al User Agent Service  
Il **User Agent Service** ti consente di iniettare un foglio di stile personalizzato, impostare il set di caratteri predefinito e controllare altre opzioni di rendering.

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## Passo 4: Definisci e Applica il Foglio di Stile Utente  
Ora forniamo le regole CSS che stilizzeranno l'HTML al momento del rendering. È qui che **usiamo il servizio user agent** per impostare il foglio di stile.

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **Perché è importante:** Applicando un foglio di stile a livello di user‑agent, garantisci che gli stili vengano rispettati anche se l'HTML originale non fa riferimento a un file CSS.

## Passo 5: Carica il Documento HTML con la Configurazione Personalizzata  
Passa sia il percorso del file che l'istanza `Configuration` al costruttore `HTMLDocument`. Questo associa il foglio di stile utente al documento.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## Passo 6: Converti HTML in PDF  
Con il documento completamente stilizzato, invoca il metodo statico `convertHTML` per **convertire HTML in PDF**. L'oggetto `PdfSaveOptions` ti permette di regolare finemente l'output (ad esempio, dimensione della pagina, compressione).

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **Risultato:** `user-agent-stylesheet_out.pdf` conterrà il titolo in marrone e il paragrafo con sfondo GhostWhite, esattamente come definito nel foglio di stile.

## Passo 7: Pulisci le Risorse  
Disporre sempre degli oggetti Aspose per liberare la memoria nativa.

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

## Problemi Comuni & Soluzioni
| Problema | Causa | Correzione |
|----------|-------|------------|
| **PDF vuoto** | Nessun foglio di stile applicato o documento non caricato con la configurazione. | Verifica che `configuration` sia passato a `HTMLDocument` e che `setUserStyleSheet` sia chiamato prima del caricamento. |
| **Avviso di proprietà CSS non supportata** | Aspose.HTML non supporta alcune funzionalità CSS avanzate. | Usa solo le proprietà CSS elencate nella documentazione di Aspose.HTML o ricorri a stili più semplici. |
| **FileNotFoundException** | Percorso errato per `document.html`. | Usa un percorso assoluto o posiziona il file HTML nella radice del progetto. |

## Domande Frequenti

**D: Posso applicare stili diversi per diversi elementi HTML?**  
R: Assolutamente! Puoi definire quante regole CSS desideri all'interno del foglio di stile utente.

**D: E se devo cambiare il foglio di stile dinamicamente?**  
R: Chiama nuovamente `setUserStyleSheet` prima di creare una nuova istanza di `HTMLDocument`; i nuovi stili verranno applicati alla prossima conversione.

**D: È possibile usare file CSS esterni con Aspose.HTML per Java?**  
R: Sì – puoi collegare un foglio di stile esterno nell'HTML o caricare il suo contenuto e passarlo a `setUserStyleSheet`.

**D: Come gestisce Aspose.HTML le proprietà CSS non supportate?**  
R: Le proprietà non supportate vengono ignorate, consentendo al resto del foglio di stile di essere renderizzato senza errori.

**D: Posso convertire HTML in formati diversi da PDF?**  
R: Sì, Aspose.HTML supporta la conversione in XPS, TIFF, PNG, JPEG e altri formati usando la classe `SaveOptions` appropriata.

## Conclusione
Ora hai visto come **creare PDF da HTML** impostando un foglio di stile utente personalizzato con Aspose.HTML per Java. Questo flusso di lavoro ti offre il pieno controllo sull'aspetto visivo del PDF generato, rendendolo ideale per la generazione automatica di report, la creazione di fatture o qualsiasi scenario in cui uno stile coerente è fondamentale. Sentiti libero di sperimentare con CSS più complessi, font esterni o formati di conversione aggiuntivi per ampliare questa base.

---

**Ultimo Aggiornamento:** 2025-12-05  
**Testato Con:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}