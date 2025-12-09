---
date: 2025-11-29
description: Scopri come convertire HTML in XPS e regolare le dimensioni della pagina
  XPS usando Aspose.HTML per Java. Controlla facilmente le dimensioni dell'output.
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Converti HTML in XPS e regola la dimensione della pagina XPS con Aspose.HTML
  per Java
url: /it/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converti HTML in XPS e Regola le Dimensioni della Pagina XPS con Aspose.HTML per Java

In questo tutorial scoprirai **come convertire HTML in XPS** e perfezionare le dimensioni della pagina risultante utilizzando Aspose.HTML per Java. Che tu stia generando report stampabili, fatture o documenti d'archivio, controllare le dimensioni dell'XPS garantisce che l'output appaia esattamente come ti aspetti. Ti guideremo passo passo—dalla configurazione dell'ambiente al rendering del file XPS finale—così potrai integrare questa funzionalità nelle tue applicazioni Java subito.

## Risposte Rapide
- **Cosa significa “convertire HTML in XPS”?** Renderizza un documento HTML in un file XPS, preservando layout e stile.  
- **Ho bisogno di una licenza?** Una versione di prova gratuita è sufficiente per lo sviluppo; è necessaria una licenza commerciale per la produzione.  
- **Quale versione di Java è supportata?** Java 8 o superiore (consigliato JDK 11+).  
- **Posso modificare le dimensioni della pagina?** Sì – Aspose.HTML consente di specificare dimensioni personalizzate prima del rendering.  
- **Quanto tempo richiede la conversione?** Tipicamente meno di un secondo per pagine standard; documenti più grandi possono richiedere più tempo.

## Cos'è la conversione da HTML a XPS?
Convertire HTML in XPS significa prendere un file di markup orientato al web e produrre un documento XPS (XML Paper Specification) — un formato a layout fisso, pronto per la stampa, simile a PDF. È utile quando hai bisogno di documenti ad alta fedeltà e indipendenti dal dispositivo per l'archiviazione o la stampa da applicazioni Java.

## Perché regolare le dimensioni della pagina XPS?
Regolare le dimensioni della pagina ti dà il controllo sulle dimensioni fisiche del documento finale (ad es., A4, Letter, etichette personalizzate). Previene ridimensionamenti indesiderati, garantisce che il contenuto si adatti perfettamente e può ridurre la dimensione del file eliminando spazi bianchi inutili.

## Prerequisiti

Prima di iniziare, assicurati di avere i seguenti prerequisiti:

1. **Ambiente di sviluppo Java** – Java Development Kit (JDK) installato sul tuo sistema.  
2. **Libreria Aspose.HTML per Java** – Scarica e includi la libreria Aspose.HTML per Java nel tuo progetto. Puoi trovare la libreria [qui](https://releases.aspose.com/html/java/).  
3. **File HTML di input** – Prepara un file HTML che desideri renderizzare e per il quale regolare le dimensioni della pagina XPS. Puoi usare il tuo file HTML per questo tutorial.

## Importa i Pacchetti

Per prima cosa, importa le classi necessarie. Questi pacchetti ti danno accesso alla gestione dei documenti, al rendering e alle funzionalità di configurazione della pagina.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Passo 1: Imposta il Nome del File di Input

Leggi il file HTML sorgente usando un `FileInputStream`. Questo stream fornisce l'HTML grezzo al motore Aspose.HTML.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## Passo 2: Crea un Documento HTML e Imposta gli Stili

Crea un'istanza `HTMLDocument` che rappresenta il contenuto da renderizzare. In questo esempio iniettiamo anche un piccolo blocco CSS per dimostrare lo styling—sentiti libero di sostituirlo con il tuo markup.

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

## Passo 3: Crea le Opzioni di Rendering XPS

Istanzia `XpsRenderingOptions` per contenere tutte le impostazioni che influenzano la conversione da HTML a XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## Passo 4: Regola le Dimensioni della Pagina

Definisci una dimensione di pagina personalizzata (larghezza × altezza in punti) e indica al renderer se deve espandersi automaticamente alla pagina più larga. Impostare `adjustToWidestPage` su `false` preserva le dimensioni esatte specificate.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## Passo 5: Renderizza l'Output

Infine, crea un `XpsDevice` con le opzioni configurate e renderizza il documento HTML. Il risultato è un file XPS completo con le dimensioni di pagina personalizzate impostate.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Problemi Comuni e Soluzioni

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **Output XPS vuoto** | Stream di input non chiuso o HTMLDocument punta al file sbagliato. | Assicurati che il `FileInputStream` sia correttamente avvolto in un blocco try‑with‑resources e che il percorso del file sia accurato. |
| **Dimensione della pagina non applicata** | `adjustToWidestPage` lasciato su `true`. | Imposta `pageSetup.setAdjustToWidestPage(false);` come mostrato nel Passo 4. |
| **CSS non supportato** | Aspose.HTML supporta un sottoinsieme di CSS. | Attieniti a layout, font e colori di base; evita selettori avanzati o CSS Grid. |
| **LicenseException** | Esecuzione senza licenza valida in produzione. | Applica la tua licenza temporanea o acquistata prima del rendering (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Domande Frequenti

**D: Cos'è Aspose.HTML per Java?**  
R: Aspose.HTML per Java è una libreria Java che consente agli sviluppatori di manipolare e convertire documenti HTML in vari formati, come XPS, PDF e immagini.

**D: Dove posso scaricare Aspose.HTML per Java?**  
R: Puoi scaricare la libreria Aspose.HTML per Java da [questo link](https://releases.aspose.com/html/java/).

**D: È disponibile una versione di prova gratuita per Aspose.HTML per Java?**  
R: Sì, puoi ottenere una versione di prova gratuita di Aspose.HTML per Java da [qui](https://releases.aspose.com/).

**D: Come posso ottenere una licenza temporanea per Aspose.HTML per Java?**  
R: Per ottenere una licenza temporanea per Aspose.HTML per Java, visita [questa pagina](https://purchase.aspose.com/temporary-license/).

**D: Posso ottenere supporto per Aspose.HTML per Java?**  
R: Sì, puoi cercare aiuto e supporto dalla community Aspose sul [Forum Aspose](https://forum.aspose.com/).

**D: Posso convertire HTML in XPS su un server headless?**  
R: Assolutamente. Aspose.HTML funziona in ambienti senza interfaccia grafica; basta assicurarsi che il runtime Java sia configurato correttamente.

**D: La libreria supporta margini di pagina personalizzati?**  
R: Sì. Usa `PageSetup.setMarginTop()`, `setMarginBottom()`, ecc., prima di assegnare il `PageSetup` alle opzioni di rendering.

## Conclusione

Abbiamo illustrato l'intero processo di **conversione da HTML a XPS** e regolazione delle dimensioni della pagina con Aspose.HTML per Java. Seguendo questi passaggi puoi generare documenti XPS pronti per la stampa che corrispondono esattamente alle tue esigenze di layout. Sentiti libero di sperimentare con diverse dimensioni di pagina, stili o anche aggiungere intestazioni e piè di pagina per adattarli alle necessità del tuo progetto.

Se hai domande o necessiti di ulteriore assistenza, consulta la [documentazione di Aspose.HTML per Java](https://reference.aspose.com/html/java/) o partecipa alla conversazione sul [Forum Aspose](https://forum.aspose.com/).

---

**Ultimo aggiornamento:** 2025-11-29  
**Testato con:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}