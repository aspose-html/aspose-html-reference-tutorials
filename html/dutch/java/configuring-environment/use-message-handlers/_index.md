---
date: 2026-05-04
description: Leer hoe je HTML‑naar‑PNG-conversie uitvoert, netwerkverzoeken in Java
  onderschept en gebroken links in Java afhandelt met Aspose.HTML voor Java.
keywords:
- html to png conversion
- intercept network requests java
- html to image conversion
- load html document java
- handle broken links java
linktitle: Gebruik berichtafhandelaars in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: HTML naar PNG-conversie met Aspose.HTML-berichtverwerkers in Java
url: /nl/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML naar PNG-conversie met Aspose.HTML-berichtafhandelaars in Java

## Introductie tot HTML naar PNG-conversie
In deze tutorial ontdek je **hoe je HTML naar PNG kunt converteren** terwijl je op elegante wijze ontbrekende bronnen afhandelt met Aspose.HTML voor Java. We lopen door het maken van een kleine HTML-pagina die naar een niet‑bestaande afbeelding verwijst, het aansluiten van een **aangepaste berichtafhandelaar** om **netwerkverzoeken te onderscheppen**, het configureren van de **network service**, het laden van het document, en uiteindelijk het uitvoeren van **html-naar-afbeeldingconversie**. Aan het einde heb je een solide patroon voor zowel **handle broken links java** als hoogwaardige PNG-uitvoer—perfect voor rapporten, miniaturen of e‑mailvoorbeelden.

## Snelle antwoorden
- **Wat doet een berichtafhandelaar?** Het onderschept netwerkoperaties (zoals afbeeldingsverzoeken) en laat je reageren op statuscodes zoals 404.  
- **Kan Aspose.HTML HTML naar PNG converteren?** Ja—`Converter.convertHTML` voert de conversie uit in één enkele aanroep.  
- **Heb ik een licentie nodig voor dit voorbeeld?** Een tijdelijke licentie verwijdert evaluatielimieten; een permanente licentie is vereist voor productiegebruik.  
- **Welke Java-versie werkt?** Elke JDK 8+ (het voorbeeld draait op JDK 11).  
- **Kan ik de netwerkservice configureren?** Absoluut—gebruik `configuration.getService(INetworkService.class)` om je afhandelaar toe te voegen.

## Wat is HTML naar PNG-conversie?
HTML naar PNG-conversie rendert een webpagina (of een fragment van HTML) naar een rasterafbeelding. Dit is handig wanneer je statische previews van dynamische inhoud nodig hebt, miniaturen voor e‑mailnieuwsbrieven genereert, of webpagina's archiveert als afbeeldingen.

## Waarom berichtafhandelaars gebruiken om netwerkverzoeken in Java te onderscheppen?
Berichtafhandelaars geven je **fijne controle** over elk netwerkverzoek—of het nu een afbeelding, CSS, JavaScript of lettertypebestand is. Door deze verzoeken te onderscheppen kun je **ontbrekende assets loggen**, fallback‑inhoud bieden, of zelfs mislukte downloads opnieuw proberen, waardoor je HTML‑verwerkingspipeline **robuust** en **productieklaar** wordt.

## Vereisten
1. **Java Development Kit (JDK)** – download van de [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – verkrijg de bibliotheek van de [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse of NetBeans werkt prima.  
4. **Basis Java-kennis** – je moet vertrouwd zijn met klassen, try‑with‑resources en foutafhandeling.  
5. **Tijdelijke licentie** – als je een proefversie gebruikt, neem een [temporary license](https://purchase.aspose.com/temporary-license/) om watermerken te vermijden.

## Pakketten importeren
Eerst importeren we de Java I/O‑klasse die we nodig hebben voor bestandsafhandeling. De rest van de Aspose‑klassen worden later met volledig gekwalificeerde namen verwezen, waardoor de importlijst overzichtelijk blijft.

```java
import java.io.IOException;
```

## Stap 1: HTML-code voorbereiden
We maken een minimale HTML‑snippet die opzettelijk naar een ontbrekende afbeelding verwijst. Dit zal onze afhandelaar activeren wanneer de engine probeert de bron op te halen.

```java
String code = "<img src='missing.jpg'>";
```

## Stap 2: Schrijf de HTML-code naar een bestand
Vervolgens slaan we de snippet op in *document.html*. Het gebruik van een try‑with‑resources‑blok garandeert dat de `FileWriter` correct wordt gesloten.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Stap 3: Een aangepaste berichtafhandelaar schrijven
Nu bouwen we een **aangepaste berichtafhandelaar** die de HTTP‑status van elk netwerkverzoek controleert. Als de respons niet `200` is, loggen we een vriendelijke waarschuwing. Let op de aanroep van `invoke(context);` aan het einde—dit stuurt het verzoek door naar de volgende afhandelaar in de keten, waardoor recursie wordt voorkomen.

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

## Stap 4: De netwerkservice configureren
Om Aspose.HTML op de hoogte te stellen van onze afhandelaar, halen we de **network service** op uit een `Configuration`‑instantie en voegen we de afhandelaar toe aan de collectie. Dit is de stap waarin we de **network service** configureren voor aangepast gedrag.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Stap 5: Laad het HTML-document
Met de configuratie klaar, laden we *document.html*. De engine gebruikt nu onze netwerkservice, zodat het verzoek voor de ontbrekende afbeelding wordt onderschept door de zojuist toegevoegde afhandelaar.

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

## Stap 6: Converteer HTML naar PNG
Hier is het hart van het **html-naar-afbeeldingconversie**‑proces. De `Converter.convertHTML`‑methode neemt het geladen `HTMLDocument`, optionele `ImageSaveOptions` (waar je DPI of kwaliteit kunt aanpassen), en de naam van het uitvoerbestand.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Stap 7: Resources opruimen
Goede Java‑praktijk dicteert dat we alle native resources vrijgeven. Het `finally`‑blok zorgt ervoor dat de `Configuration` wordt verwijderd, zelfs als een uitzondering zich voordoet.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Veelvoorkomende problemen en oplossingen
- **Handler-recursie** – Roep `invoke(context);` slechts één keer aan om oneindige lussen te voorkomen.  
- **Ontbrekende licentie** – Zonder een geldige licentie zal de uitvoer‑PNG een watermerk bevatten.  
- **Onjuiste bestands‑paden** – Gebruik absolute paden of stel de werkmap correct in bij het laden van `document.html`.  
- **Niet‑ondersteunde resource‑typen** – Zorg ervoor dat de resource die je wilt onderscheppen (afbeelding, CSS, enz.) daadwerkelijk wordt aangevraagd door de HTML‑engine.

## Veelgestelde vragen

**Q: Kan ik meerdere berichtafhandelaars schakelen?**  
A: Ja, je kunt meerdere afhandelaars toevoegen aan de `network.getMessageHandlers()`‑collectie; ze worden uitgevoerd in de volgorde waarin ze zijn toegevoegd.

**Q: Werkt de afhandelaar ook voor CSS‑ of script‑resources?**  
A: Absoluut—elk netwerkverzoek dat door de HTML‑engine wordt gedaan (afbeeldingen, CSS, JS, lettertypen) gaat door de afhandelaar.

**Q: Hoe wijzig ik het HTTP‑verzoek voordat het wordt verzonden?**  
A: Implementeer een afhandelaar die `context.getRequest()` wijzigt voordat `invoke(context)` wordt aangeroepen.

**Q: Is er een manier om de waarschuwing voor specifieke URL's te onderdrukken?**  
A: Binnen de afhandelaar inspecteer je `context.getRequest().getRequestUri()` en sla je het loggen conditioneel over.

**Q: Welke versie van Aspose.HTML is vereist voor deze API's?**  
A: De code werkt met Aspose.HTML for Java 22.10 en later.

---

**Last Updated:** 2026-05-04  
**Tested With:** Aspose.HTML for Java 24.11  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}