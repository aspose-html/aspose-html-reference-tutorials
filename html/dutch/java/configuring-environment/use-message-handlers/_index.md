---
date: 2026-02-10
description: Leer hoe je Aspose gebruikt om gebroken links in Java af te handelen,
  HTML naar PNG te converteren en een HTML-document te laden met Aspose.HTML voor
  Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: HTML naar PNG converteren met Aspose.HTML-berichtverwerkers in Java
url: /nl/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML naar PNG converteren met Aspose.HTML Message Handlers in Java

## Inleiding
In deze tutorial ontdek je **hoe je HTML naar PNG kunt converteren** terwijl je ontbrekende bronnen op een nette manier afhandelt met Aspose.HTML voor Java. We lopen door het maken van een kleine HTML‑pagina die naar een niet‑bestaande afbeelding verwijst, het aansluiten van een **aangepaste message handler** om **netwerkverzoeken te onderscheppen**, het configureren van de **network service**, het laden van het document en tenslotte het uitvoeren van **html‑naar‑afbeelding conversie**. Aan het einde heb je een solide patroon voor zowel **broken links java** als hoogwaardige PNG‑output — perfect voor rapporten, thumbnails of e‑mail‑voorbeelden.

## Snelle antwoorden
- **Wat doet een message handler?** Hij onderschept netwerkbewerkingen (zoals afbeeldingsverzoeken) en laat je reageren op statuscodes zoals 404.  
- **Kan Aspose.HTML HTML naar PNG converteren?** Ja — `Converter.convertHTML` voert de conversie uit in één enkele aanroep.  
- **Heb ik een licentie nodig voor dit voorbeeld?** Een tijdelijke licentie verwijdert evaluatielimieten; een permanente licentie is vereist voor productiegebruik.  
- **Welke Java‑versie werkt?** Elke JDK 8+ (het voorbeeld draait op JDK 11).  
- **Kan ik de network service configureren?** Absoluut — gebruik `configuration.getService(INetworkService.class)` om je handler toe te voegen.

## Vereisten
Voordat we beginnen, zorg dat je het volgende klaar hebt staan:

1. **Java Development Kit (JDK)** – download van de [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – haal de bibliotheek van de [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse of NetBeans werkt prima.  
4. **Basiskennis van Java** – je moet vertrouwd zijn met klassen, try‑with‑resources en exception handling.  
5. **Tijdelijke licentie** – als je een proefversie gebruikt, pak een [temporary license](https://purchase.aspose.com/temporary-license/) om watermerken te vermijden.

## Pakketten importeren
Eerst importeren we de Java I/O‑klasse die we nodig hebben voor bestandsafhandeling. De overige Aspose‑klassen worden later met volledig gekwalificeerde namen aangeroepen, zodat de importlijst overzichtelijk blijft.

```java
import java.io.IOException;
```

## Stap 1: De HTML‑code voorbereiden
We maken een minimale HTML‑snippet die opzettelijk naar een ontbrekende afbeelding verwijst. Dit zal onze handler activeren wanneer de engine probeert de bron op te halen.

```java
String code = "<img src='missing.jpg'>";
```

## Stap 2: De HTML‑code naar een bestand schrijven
Vervolgens slaan we de snippet op als *document.html*. Het gebruik van een try‑with‑resources‑blok zorgt ervoor dat de `FileWriter` correct wordt gesloten.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Stap 3: Een aangepaste Message Handler schrijven
Nu bouwen we een **aangepaste message handler** die de HTTP‑status van elk netwerkverzoek controleert. Als de respons niet `200` is, loggen we een vriendelijke waarschuwing. Let op de aanroep `invoke(context);` aan het einde — dit stuurt het verzoek door naar de volgende handler in de keten en voorkomt recursie.

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

## Stap 4: De Network Service configureren
Om Aspose.HTML op de hoogte te stellen van onze handler, halen we de **network service** op uit een `Configuration`‑instantie en voegen we de handler toe aan de collectie. Dit is de stap waarin we **network service configureren** voor aangepast gedrag.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Stap 5: Het HTML‑document laden
Met de configuratie gereed, laden we *document.html*. De engine gebruikt nu onze network service, zodat het verzoek voor de ontbrekende afbeelding wordt onderschept door de handler die we zojuist hebben toegevoegd.

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

## Stap 6: HTML naar PNG converteren
Hier is het hart van het **html‑naar‑afbeelding conversie**‑proces. De methode `Converter.convertHTML` neemt het geladen `HTMLDocument`, optionele `ImageSaveOptions` (waar je DPI of kwaliteit kunt aanpassen) en de naam van het uitvoerbestand.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Stap 7: Resources opruimen
Goed Java‑gebruik vereist dat we alle native resources vrijgeven. Het `finally`‑blok zorgt ervoor dat de `Configuration` wordt verwijderd, zelfs als er een uitzondering wordt gegooid.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Waarom Message Handlers gebruiken?
Message handlers geven je **fijne controle** over elk netwerkverzoek — of het nu een afbeelding, CSS, JavaScript of lettertypebestand is. In plaats van de bibliotheek stilletjes te laten falen, kun je ontbrekende assets loggen, fallback‑inhoud bieden of zelfs het verzoek opnieuw proberen. Dit maakt je HTML‑verwerkingspipeline **robust**, **productieklaar** en makkelijker te debuggen.

## Veelvoorkomende problemen en oplossingen
- **Handler‑recursie** – Roep `invoke(context);` slechts één keer aan om oneindige lussen te voorkomen.  
- **Ontbrekende licentie** – Zonder geldige licentie bevat de gegenereerde PNG een watermerk.  
- **Onjuiste bestands‑paden** – Gebruik absolute paden of stel de werkmap correct in bij het laden van `document.html`.  
- **Niet‑ondersteunde bron‑types** – Zorg ervoor dat de bron die je wilt onderscheppen (afbeelding, CSS, enz.) daadwerkelijk wordt opgevraagd door de HTML‑engine.

## Veelgestelde vragen

**Q: Kan ik meerdere message handlers koppelen?**  
A: Ja, je kunt meerdere handlers toevoegen aan de collectie `network.getMessageHandlers()`; ze worden uitgevoerd in de volgorde waarin ze zijn toegevoegd.

**Q: Werkt de handler ook voor CSS‑ of script‑bronnen?**  
A: Absoluut — elk netwerkverzoek dat door de HTML‑engine wordt gedaan (afbeeldingen, CSS, JS, fonts) passeert de handler.

**Q: Hoe wijzig ik het HTTP‑verzoek voordat het wordt verzonden?**  
A: Implementeer een handler die `context.getRequest()` aanpast voordat je `invoke(context)` aanroept.

**Q: Is er een manier om de waarschuwing voor specifieke URL’s te onderdrukken?**  
A: Inspecteer binnen de handler `context.getRequest().getRequestUri()` en sla het loggen over op basis van een voorwaarde.

**Q: Welke versie van Aspose.HTML is vereist voor deze API’s?**  
A: De code werkt met Aspose.HTML for Java 22.10 en later.

## Conclusie
Je hebt nu een compleet, end‑to‑end voorbeeld van **hoe je HTML naar PNG kunt converteren** terwijl je een **aangepaste message handler** gebruikt om **netwerkverzoeken te onderscheppen** en **broken links java** af te handelen. Door de network service te configureren, het document te laden en de converter aan te roepen, kun je betrouwbaar PNG‑thumbnails of volledige pagina‑screenshots genereren in elke Java‑applicatie.

---

**Laatst bijgewerkt:** 2026-02-10  
**Getest met:** Aspose.HTML for Java 24.11  
**Auteur:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}