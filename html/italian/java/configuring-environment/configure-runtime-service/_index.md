---
date: 2025-12-10
description: Scopri come impostare il timeout in Aspose.HTML per Java, configurare
  il Runtime Service per convertire HTML in PNG, prevenire i loop infiniti e migliorare
  le prestazioni.
linktitle: Configure Runtime Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Come impostare il timeout nel servizio di runtime Aspose.HTML per Java
url: /it/java/configuring-environment/configure-runtime-service/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come impostare il timeout in Aspose.HTML per Java Runtime Service

## Introduzione
Se stai cercando **come impostare il timeout** per gli script quando lavori con Aspose.HTML per Java, sei nel posto giusto. Controllare l'esecuzione degli script non solo previene i loop infiniti, ma ti aiuta anche a **convertire html in png** più velocemente e a mantenere la tua applicazione reattiva. In questo tutorial vedremo passo passo come configurare il Runtime Service, limitare l'esecuzione degli script e, infine, produrre un'immagine PNG da HTML senza bloccare il programma.

## Risposte rapide
- **Che cosa fa il Runtime Service?** Consente di controllare il tempo di esecuzione degli script e gestire le risorse durante l'elaborazione dell'HTML.  
- **Come impostare il timeout per JavaScript?** Utilizzare `runtimeService.setJavaScriptTimeout(TimeSpan.fromSeconds(...))`.  
- **Posso prevenire i loop infiniti?** Sì – il timeout interrompe i loop che superano il limite definito.  
- **Questo influisce sulla conversione HTML‑to‑PNG?** No, la conversione procede una volta che lo script termina o viene interrotto dal timeout.  
- **Quale versione di Aspose.HTML è necessaria?** L'ultima release dalla pagina di download di Aspose.

## Prerequisiti
Prima di entrare nei dettagli, assicurati di avere quanto segue:

1. **Java Development Kit (JDK)** – installalo dal [sito di Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java Library** – scarica l'ultima build dalla [pagina di release di Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse o NetBeans vanno bene.  
4. **Conoscenze di base di Java e HTML** – essenziali per seguire gli esempi di codice.

## Importazione dei pacchetti
Per prima cosa, importa le classi necessarie. L'import `java.io.IOException` è richiesto per la gestione dei file.

```java
import java.io.IOException;
```

## Passo 1: Creare un file HTML con codice JavaScript
Inizieremo generando un semplice file HTML che contiene un loop JavaScript. Questo loop continuerebbe all'infinito se non imponessimo un timeout, rendendolo un demo perfetto per il Runtime Service.

```java
String code = "<h1>Runtime Service</h1>\r\n" +
        "<script> while(true) {} </script>\r\n" +
        "<p>The Runtime Service optimizes your system by helping it start apps and programs faster.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("runtime-service.html")) {
    fileWriter.write(code);
}
```

- Lo script `while(true) {}` rappresenta un potenziale loop infinito.  
- `FileWriter` scrive il contenuto HTML in **runtime-service.html**.

## Passo 2: Configurare l'oggetto Configuration
Successivamente, crea un'istanza di `Configuration`. Questo oggetto è la spina dorsale di tutti i servizi Aspose.HTML, incluso il Runtime Service.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Passo 3: Configurare il Runtime Service
Ecco dove effettivamente **impostiamo il timeout**. Recuperando l'`IRuntimeService` dalla configurazione, possiamo definire un limite di esecuzione per JavaScript.

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

- `setJavaScriptTimeout` limita l'esecuzione dello script a **5 secondi**, impedendo efficacemente i **loop infiniti**.  
- Questo **limita l'esecuzione degli script** per qualsiasi codice client‑side pesante.

## Passo 4: Caricare il documento HTML con la configurazione
Ora carica il file HTML usando la configurazione che contiene la nostra regola di timeout.

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

- Il documento rispetta il timeout definito in precedenza, quindi il loop infinito verrà interrotto dopo 5 secondi.

## Passo 5: Convertire l'HTML in PNG
Con il documento caricato in modo sicuro, possiamo **convertire html in png**. La conversione avviene solo dopo che lo script termina o viene interrotto dal timeout.

```java
    com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.ImageSaveOptions(),
        "runtime-service_out.png"
    );
```

- `ImageSaveOptions` indica ad Aspose.HTML di generare un'immagine PNG.  
- Il file risultante, **runtime-service_out.png**, mostra l'HTML renderizzato senza blocchi.

## Passo 6: Pulire le risorse
Infine, elimina gli oggetti per liberare memoria e prevenire perdite.

```java
} finally {
    if (document != null) {
        document.dispose();
    }
    if (configuration != null) {
        configuration.dispose();
    }
}
```

- Una corretta eliminazione è essenziale per applicazioni a lungo termine.

## Conclusione
Hai appena imparato **come impostare il timeout** per l'esecuzione di JavaScript in Aspose.HTML per Java, come **prevenire i loop infiniti** e come **convertire html in png** in modo sicuro. Configurando il Runtime Service ottieni un controllo fine sul comportamento degli script, il che si traduce in tempi di avvio più rapidi e conversioni più affidabili. Sperimenta con valori di timeout diversi per adattarli ai tuoi carichi di lavoro specifici e noterai un notevole miglioramento delle prestazioni.

## Domande frequenti

**D: Qual è lo scopo del Runtime Service in Aspose.HTML per Java?**  
R: Consente di controllare il tempo di esecuzione degli script, aiutando a **prevenire i loop infiniti** e a mantenere le conversioni reattive.

**D: Come posso scaricare Aspose.HTML per Java?**  
R: Ottieni l'ultima versione dalla [pagina di release](https://releases.aspose.com/html/java/).

**D: È necessario eliminare gli oggetti `document` e `configuration`?**  
R: Sì, l'eliminazione rilascia le risorse native e previene perdite di memoria.

**D: Posso impostare il timeout JavaScript a un valore diverso da 5 secondi?**  
R: Assolutamente – modifica l'argomento di `TimeSpan.fromSeconds()` con il limite che meglio si adatta al tuo scenario.

**D: Dove posso trovare aiuto se incontro problemi?**  
R: Visita il [forum Aspose.HTML](https://forum.aspose.com/c/html/29) per assistenza da parte della community e dello staff.

**Ultimo aggiornamento:** 2025-12-10  
**Testato con:** Aspose.HTML per Java 24.11 (latest)  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}