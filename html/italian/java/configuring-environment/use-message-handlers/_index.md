---
date: 2026-02-10
description: Scopri come utilizzare Aspose per gestire i collegamenti interrotti in
  Java, convertire HTML in PNG e caricare documenti HTML in Java con Aspose.HTML per
  Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Converti HTML in PNG con i gestori di messaggi Aspose.HTML in Java
url: /it/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertire HTML in PNG con i Message Handler di Aspose.HTML in Java

## Introduzione
In questo tutorial scoprirai **come convertire HTML in PNG** gestendo elegantemente le risorse mancanti con Aspose.HTML per Java. Vedremo come creare una piccola pagina HTML che punta a un'immagine inesistente, collegare un **message handler personalizzato** per **intercettare le richieste di rete**, configurare il **network service**, caricare il documento e infine eseguire la **conversione da HTML a immagine**. Alla fine avrai un modello solido sia per **handle broken links java** sia per ottenere PNG di alta qualità—perfetto per report, miniature o anteprime email.

## Risposte rapide
- **Che cosa fa un message handler?** Intercetta le operazioni di rete (come le richieste di immagini) e ti consente di reagire ai codici di stato come 404.  
- **Aspose.HTML può convertire HTML in PNG?** Sì—`Converter.convertHTML` esegue la conversione in una singola chiamata.  
- **Ho bisogno di una licenza per questo esempio?** Una licenza temporanea rimuove i limiti di valutazione; è necessaria una licenza permanente per l'uso in produzione.  
- **Quale versione di Java funziona?** Qualsiasi JDK 8+ (l'esempio gira su JDK 11).  
- **Posso configurare il network service?** Assolutamente—usa `configuration.getService(INetworkService.class)` per aggiungere il tuo handler.

## Prerequisiti
Prima di iniziare, assicurati di avere quanto segue pronto:

1. **Java Development Kit (JDK)** – scarica dal [sito Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – ottieni la libreria dalla [pagina di rilascio di Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse o NetBeans vanno bene.  
4. **Conoscenza di base di Java** – dovresti sentirti a tuo agio con classi, try‑with‑resources e gestione delle eccezioni.  
5. **Licenza temporanea** – se sei in prova, procurati una [licenza temporanea](https://purchase.aspose.com/temporary-license/) per evitare filigrane.

## Importare i pacchetti
Per prima cosa includi la classe Java I/O di cui avremo bisogno per la gestione dei file. Le altre classi di Aspose sono referenziate con nomi completamente qualificati più avanti, mantenendo la lista degli import ordinata.

```java
import java.io.IOException;
```

## Passo 1: Preparare il codice HTML
Creiamo uno snippet HTML minimale che fa riferimento deliberatamente a un'immagine mancante. Questo farà scattare il nostro handler quando il motore proverà a recuperare la risorsa.

```java
String code = "<img src='missing.jpg'>";
```

## Passo 2: Scrivere il codice HTML su un file
Successivamente, salviamo lo snippet in *document.html*. L'uso di un blocco try‑with‑resources garantisce che il `FileWriter` venga chiuso correttamente.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Passo 3: Scrivere un Message Handler personalizzato
Ora costruiamo un **message handler personalizzato** che controlla lo stato HTTP di ogni richiesta di rete. Se la risposta non è `200`, registriamo un avviso amichevole. Nota la chiamata a `invoke(context);` alla fine—questa inoltra la richiesta al prossimo handler nella catena, evitando ricorsioni.

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

## Passo 4: Configurare il Network Service
Per rendere Aspose.HTML consapevole del nostro handler, recuperiamo il **network service** da un'istanza `Configuration` e aggiungiamo l'handler alla sua collezione. Questo è il passo in cui **configuriamo il network service** per un comportamento personalizzato.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Passo 5: Caricare il documento HTML
Con la configurazione pronta, carichiamo *document.html*. Il motore ora utilizza il nostro network service, così la richiesta dell'immagine mancante viene intercettata dall'handler appena aggiunto.

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
Ecco il cuore del processo di **conversione da HTML a immagine**. Il metodo `Converter.convertHTML` prende il `HTMLDocument` caricato, le opzionali `ImageSaveOptions` (dove potresti regolare DPI o qualità) e il nome del file di output.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Passo 7: Pulire le risorse
Una buona pratica Java richiede di rilasciare tutte le risorse native. Il blocco `finally` assicura che la `Configuration` venga eliminata anche se un'eccezione viene propagata.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Perché usare i Message Handler?
I message handler ti offrono **un controllo granulare** su ogni richiesta di rete—sia che si tratti di un'immagine, CSS, JavaScript o file di font. Invece di lasciare che la libreria fallisca silenziosamente, puoi registrare le risorse mancanti, fornire contenuti di fallback o persino ritentare la richiesta. Questo rende la tua pipeline di elaborazione HTML **robusta**, **pronta per la produzione** e più facile da debug.

## Problemi comuni e soluzioni
- **Recursione dell'handler** – Chiama `invoke(context);` solo una volta per evitare loop infiniti.  
- **Licenza mancante** – Senza una licenza valida il PNG di output conterrà una filigrana.  
- **Percorsi file errati** – Usa percorsi assoluti o imposta correttamente la directory di lavoro quando carichi `document.html`.  
- **Tipi di risorsa non supportati** – Assicurati che la risorsa che vuoi intercettare (immagine, CSS, ecc.) sia effettivamente richiesta dal motore HTML.

## Domande frequenti

**Q: Posso concatenare più message handler?**  
A: Sì, puoi aggiungere diversi handler alla collezione `network.getMessageHandlers()`; verranno eseguiti nell'ordine in cui sono stati aggiunti.

**Q: L'handler funziona anche per risorse CSS o script?**  
A: Assolutamente—qualsiasi richiesta di rete effettuata dal motore HTML (immagini, CSS, JS, font) passa attraverso l'handler.

**Q: Come posso modificare la richiesta HTTP prima che venga inviata?**  
A: Implementa un handler che modifica `context.getRequest()` prima di chiamare `invoke(context)`.

**Q: Esiste un modo per sopprimere l'avviso per URL specifici?**  
A: All'interno dell'handler, controlla `context.getRequest().getRequestUri()` e salta condizionalmente il log.

**Q: Quale versione di Aspose.HTML è necessaria per queste API?**  
A: Il codice funziona con Aspose.HTML for Java 22.10 e successive.

## Conclusione
Ora disponi di un esempio completo, end‑to‑end, di **come convertire HTML in PNG** utilizzando un **message handler personalizzato** per **intercettare le richieste di rete** e **gestire i broken links java**. Configurando il network service, caricando il documento e invocando il convertitore, puoi generare in modo affidabile miniature PNG o screenshot a pagina intera in qualsiasi applicazione Java.

---

**Last Updated:** 2026-02-10  
**Tested With:** Aspose.HTML for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}