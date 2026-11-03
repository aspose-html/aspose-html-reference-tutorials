---
date: 2026-05-04
description: Scopri come eseguire la conversione da HTML a PNG, intercettare le richieste
  di rete in Java e gestire i collegamenti interrotti in Java utilizzando Aspose.HTML
  per Java.
keywords:
- html to png conversion
- intercept network requests java
- html to image conversion
- load html document java
- handle broken links java
linktitle: Usa i gestori di messaggi in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Conversione da HTML a PNG con i gestori di messaggi Aspose.HTML in Java
url: /it/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Conversione da HTML a PNG con i gestori di messaggi Aspose.HTML in Java

## Introduzione alla conversione da HTML a PNG
In questo tutorial scoprirai **come convertire HTML in PNG** gestendo elegantemente le risorse mancanti usando Aspose.HTML per Java. Vedremo come creare una piccola pagina HTML che punta a un'immagine inesistente, collegare un **gestore di messaggi personalizzato** per **intercettare le richieste di rete**, configurare il **servizio di rete**, caricare il documento e infine eseguire la **conversione da HTML a immagine**. Alla fine avrai un modello solido sia per **handle broken links java** sia per ottenere un'output PNG di alta qualità—perfetto per report, miniature o anteprime email.

## Risposte rapide
- **Cosa fa un gestore di messaggi?** Intercetta le operazioni di rete (come le richieste di immagini) e ti consente di reagire a codici di stato come 404.  
- **Aspose.HTML può convertire HTML in PNG?** Sì—`Converter.convertHTML` esegue la conversione in una singola chiamata.  
- **Ho bisogno di una licenza per questo esempio?** Una licenza temporanea rimuove i limiti di valutazione; è necessaria una licenza permanente per l'uso in produzione.  
- **Quale versione di Java funziona?** Qualsiasi JDK 8+ (l'esempio gira su JDK 11).  
- **Posso configurare il servizio di rete?** Assolutamente—usa `configuration.getService(INetworkService.class)` per aggiungere il tuo gestore.

## Cos'è la conversione da HTML a PNG?
La conversione da HTML a PNG rende una pagina web (o un frammento di HTML) in un'immagine raster. È utile quando hai bisogno di anteprime statiche di contenuti dinamici, generare miniature per newsletter email o archiviare pagine web come immagini.

## Perché usare i gestori di messaggi per intercettare le richieste di rete Java?
I gestori di messaggi ti offrono **fine‑grained control** su ogni richiesta di rete—che si tratti di un'immagine, CSS, JavaScript o file di font. Intercettando queste richieste puoi **log missing assets**, fornire contenuti di fallback o persino ritentare download falliti, rendendo la tua pipeline di elaborazione HTML **robusta** e **pronta per la produzione**.

## Prerequisiti
1. **Java Development Kit (JDK)** – scarica dal [sito Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – ottieni la libreria dalla [pagina dei rilasci Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse o NetBeans vanno bene.  
4. **Conoscenza di base di Java** – dovresti sentirti a tuo agio con classi, try‑with‑resources e gestione delle eccezioni.  
5. **Licenza temporanea** – se sei in prova, procurati una [licenza temporanea](https://purchase.aspose.com/temporary-license/) per evitare filigrane.

## Importa pacchetti
Per prima cosa, importa la classe Java I/O di cui avremo bisogno per la gestione dei file. Il resto delle classi Aspose è referenziato con nomi completamente qualificati più avanti, mantenendo la lista degli import ordinata.

```java
import java.io.IOException;
```

## Passo 1: Preparare il codice HTML
Creiamo un frammento HTML minimale che fa riferimento deliberatamente a un'immagine mancante. Questo attiverà il nostro gestore quando il motore cercherà di recuperare la risorsa.

```java
String code = "<img src='missing.jpg'>";
```

## Passo 2: Scrivere il codice HTML su un file
Successivamente, salviamo il frammento in *document.html*. L'uso di un blocco try‑with‑resources garantisce che il `FileWriter` venga chiuso correttamente.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Passo 3: Scrivere un gestore di messaggi personalizzato
Ora creiamo un **gestore di messaggi personalizzato** che verifica lo stato HTTP di ogni richiesta di rete. Se la risposta non è `200`, registriamo un avviso amichevole. Nota la chiamata a `invoke(context);` alla fine—questa inoltra la richiesta al prossimo gestore nella catena, evitando la ricorsione.

```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```

## Passo 4: Configurare il servizio di rete
Per rendere Aspose.HTML consapevole del nostro gestore, recuperiamo il **servizio di rete** da un'istanza `Configuration` e aggiungiamo il gestore alla sua collezione. Questo è il passaggio in cui **configuriamo il servizio di rete** per un comportamento personalizzato.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Passo 5: Caricare il documento HTML
Con la configurazione pronta, carichiamo *document.html*. Il motore ora utilizza il nostro servizio di rete, quindi la richiesta dell'immagine mancante viene intercettata dal gestore appena aggiunto.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```

## Passo 6: Convertire HTML in PNG
Ecco il cuore del processo di **conversione da HTML a immagine**. Il metodo `Converter.convertHTML` prende il `HTMLDocument` caricato, opzionali `ImageSaveOptions` (dove puoi regolare DPI o qualità) e il nome del file di output.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Passo 7: Pulire le risorse
Una buona pratica Java prevede di rilasciare tutte le risorse native. Il blocco `finally` garantisce che la `Configuration` venga eliminata anche se un'eccezione si propaga.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Problemi comuni e soluzioni
- **Ricorsione del gestore** – Chiama `invoke(context);` solo una volta per evitare loop infiniti.  
- **Licenza mancante** – Senza una licenza valida l'output PNG conterrà una filigrana.  
- **Percorsi file errati** – Usa percorsi assoluti o imposta correttamente la directory di lavoro quando carichi `document.html`.  
- **Tipi di risorsa non supportati** – Assicurati che la risorsa che vuoi intercettare (immagine, CSS, ecc.) sia effettivamente richiesta dal motore HTML.

## Domande frequenti
**Q: Posso concatenare più gestori di messaggi?**  
**A:** Sì, puoi aggiungere diversi gestori alla collezione `network.getMessageHandlers()`; verranno eseguiti nell'ordine aggiunto.

**Q: Il gestore funziona anche per risorse CSS o script?**  
**A:** Assolutamente—qualsiasi richiesta di rete effettuata dal motore HTML (immagini, CSS, JS, font) passa attraverso il gestore.

**Q: Come modifico la richiesta HTTP prima che venga inviata?**  
**A:** Implementa un gestore che modifica `context.getRequest()` prima di chiamare `invoke(context)`.

**Q: Esiste un modo per sopprimere l'avviso per URL specifici?**  
**A:** All'interno del gestore, ispeziona `context.getRequest().getRequestUri()` e salta il log in modo condizionale.

**Q: Quale versione di Aspose.HTML è necessaria per queste API?**  
**A:** Il codice funziona con Aspose.HTML per Java 22.10 e successive.

---

**Ultimo aggiornamento:** 2026-05-04  
**Testato con:** Aspose.HTML for Java 24.11  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}