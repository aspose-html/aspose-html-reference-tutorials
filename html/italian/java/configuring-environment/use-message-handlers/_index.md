---
date: 2025-12-10
description: Impara come usare Aspose per gestire i collegamenti interrotti in Java,
  convertire HTML in PNG e caricare documenti HTML in Java con Aspose.HTML per Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Come utilizzare i gestori di messaggi Aspose.HTML in Java
url: /it/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare i Message Handler di Aspose.HTML in Java

## Introduzione
In questo tutorial viene mostrato **come usare aspose** per gestire le risorse mancanti in HTML passo‑per‑passo. Creeremo un semplice documento HTML che fa riferimento a un’immagine mancante, allegheremo un message handler personalizzato e vi mostreremo come **caricare un documento html java** gestendo elegantemente i collegamenti interrotti. Alla fine, vedrete anche come **convertire html in png** usando Aspose.HTML, ottenendo una panoramica completa della conversione da HTML a immagine in Java.

## Risposte rapide
- **Qual è lo scopo principale di un message handler?** Intercettare le operazioni di rete e reagire a codici di stato come le risorse mancanti.  
- **Aspose.HTML può convertire HTML in PNG?** Sì, usando `Converter.convertHTML` è possibile eseguire la conversione da html a immagine.  
- **È necessaria una licenza per questo esempio?** Una licenza temporanea rimuove i limiti di valutazione; una licenza permanente è richiesta per la produzione.  
- **Quale versione di Java è supportata?** Qualsiasi JDK 8+ (il tutorial utilizza JDK 11).  
- **È possibile gestire più collegamenti interrotti?** Assolutamente – è possibile concatenare diversi handler per gestire scenari differenti.

## Prerequisiti
Prima di immergerci nella guida passo‑per‑passo, assicuriamoci di avere tutto il necessario:
1. Java Development Kit (JDK): Verificate di avere il JDK installato sul vostro sistema. Potete scaricarlo dal [sito di Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
2. Aspose.HTML for Java: È necessario avere Aspose.HTML for Java installato. Potete scaricarlo dalla [pagina dei rilasci di Aspose](https://releases.aspose.com/html/java/).
3. IDE: Utilizzate il vostro IDE Java preferito, come IntelliJ IDEA, Eclipse o NetBeans.
4. Conoscenze di base di Java: Familiarità con la programmazione Java è essenziale per seguire efficacemente questo tutorial.
5. Licenza temporanea: Se state usando la versione di prova di Aspose.HTML, considerate l’ottenimento di una [licenza temporanea](https://purchase.aspose.com/temporary-license/) per evitare limitazioni durante lo sviluppo.

## Importare i pacchetti
Prima di iniziare, assicuratevi di aver importato i pacchetti necessari nel vostro progetto Java. Di seguito sono elencate le importazioni essenziali:
```java
import java.io.IOException;
```
Queste importazioni vi daranno accesso alle classi e ai metodi richiesti per gestire le operazioni di rete, creare documenti HTML e eseguire la conversione da HTML a PNG.

## Passo 1: Preparare il codice HTML
La prima cosa di cui abbiamo bisogno è un semplice frammento HTML che faccia riferimento a un file immagine. Faremo riferimento deliberatamente a un’immagine che non esiste per attivare il meccanismo di gestione degli errori.
```java
String code = "<img src='missing.jpg'>";
```
Questo codice crea un tag `<img>` che punta a `missing.jpg`. Poiché l’immagine è mancante, il servizio di rete restituirà un codice di stato diverso da 200, che il nostro handler personalizzato intercetterà.

## Passo 2: Scrivere il codice HTML su file
Successivamente, dobbiamo persistere il frammento HTML affinché Aspose.HTML possa caricarlo come documento.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
Utilizzando un `FileWriter` salviamo l’HTML in **document.html**. Questo file diventa la sorgente per il passo **load html document java** successivo.

## Passo 3: Creare un Message Handler personalizzato
Ora costruiamo un message handler personalizzato che reagisce quando l’immagine non viene trovata. L’handler controlla il codice di stato HTTP e stampa un messaggio amichevole.
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
Il metodo `invoke` esamina `context.getResponse().getStatusCode()`. Se non è **200**, stampiamo un avviso chiaro che il file è mancante. La chiamata finale `invoke(context);` passa il controllo al prossimo handler nella catena.

## Passo 4: Configurare il servizio di rete
Per rendere Aspose.HTML consapevole del nostro handler, lo registriamo con il servizio di rete tramite la classe `Configuration`.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Qui creiamo un’istanza di `Configuration`, recuperiamo l’`INetworkService` e aggiungiamo il nostro handler personalizzato alla sua collezione. Questo garantisce che l’handler venga eseguito durante qualsiasi richiesta di rete, ad esempio il caricamento di immagini.

## Passo 5: Caricare il documento HTML
Con la configurazione pronta, possiamo ora caricare il file HTML creato in precedenza. Questo passo dimostra **load html document java** mentre l’immagine mancante attiva il nostro handler.
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
Il costruttore `HTMLDocument` riceve sia il percorso del file sia la `configuration` personalizzata. Quando il documento analizza il tag `<img>`, il servizio di rete tenta di recuperare `missing.jpg`, riceve un 404 e il nostro handler stampa l’avviso.

## Passo 6: Convertire HTML in PNG
Per illustrare le capacità più ampie di Aspose.HTML, convertiremo il documento caricato in un’immagine PNG. Si tratta di uno scenario classico di **convert html to png**.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` accetta l’`HTMLDocument`, eventuali `ImageSaveOptions` (dove è possibile impostare DPI, qualità, ecc.) e il nome del file di output. Il risultato è un’immagine raster dell’HTML renderizzato.

## Passo 7: Pulire le risorse
Una corretta gestione delle risorse è fondamentale in qualsiasi applicazione Java. Disporremo sia della `Configuration` sia dell’`HTMLDocument` per evitare perdite di memoria.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Raccogliere la pulizia in un blocco `finally` garantisce l’esecuzione anche se si verifica un’eccezione in precedenza.

## Perché usare i Message Handler?
I message handler offrono un controllo fine sulle operazioni di rete, come **handle broken links java**. Invece di lasciare che la libreria fallisca silenziosamente, potete registrare, riprovare, sostituire risorse o fornire contenuti di fallback—rendendo il vostro processamento HTML robusto e pronto per la produzione.

## Problemi comuni e soluzioni
- **Recursione dell’handler** – Assicuratevi di chiamare `invoke(context);` una sola volta per evitare loop infiniti.  
- **Licenza mancante** – Senza una licenza valida, la conversione potrebbe produrre un’immagine con watermark.  
- **Errori di percorso file** – Utilizzate percorsi assoluti o impostate correttamente la directory di lavoro quando caricate `document.html`.

## Domande frequenti

**D: Posso concatenare più message handler?**  
R: Sì, potete aggiungere diversi handler alla collezione `network.getMessageHandlers()`; verranno eseguiti nell’ordine di aggiunta.

**D: L’handler funziona anche per risorse CSS o script?**  
R: Assolutamente—qualsiasi richiesta di rete effettuata dal motore HTML (immagini, CSS, JS, font) passa attraverso l’handler.

**D: Come modifico la richiesta HTTP prima che venga inviata?**  
R: Implementate un handler che modifica `context.getRequest()` prima di chiamare `invoke(context)`.

**D: È possibile sopprimere l’avviso per URL specifici?**  
R: All’interno dell’handler, ispezionate `context.getRequest().getRequestUri()` e saltate condizionatamente il log.

**D: Quale versione di Aspose.HTML è necessaria per queste API?**  
R: Il codice funziona con Aspose.HTML for Java 22.10 e successive.

## Conclusione
Ecco a voi una guida completa su **come usare aspose** message handler in Java. Abbiamo coperto la creazione di un file HTML, il collegamento di un handler personalizzato per **handle broken links java**, il caricamento del documento e l’esecuzione di **convert html to png**. Con questo approccio potete gestire con sicurezza le risorse mancanti, applicare politiche personalizzate ed estendere le capacità di rete di Aspose.HTML in qualsiasi applicazione Java.

---

**Ultimo aggiornamento:** 2025-12-10  
**Testato con:** Aspose.HTML for Java 24.11  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}