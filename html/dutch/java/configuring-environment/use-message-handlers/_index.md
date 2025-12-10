---
date: 2025-12-10
description: Leer hoe je Aspose kunt gebruiken om gebroken links in Java af te handelen,
  HTML naar PNG te converteren en een HTML‑document te laden in Java met Aspose.HTML
  voor Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Hoe Aspose.HTML-berichtverwerkers te gebruiken in Java
url: /nl/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Aspose.HTML-berichtverwerkers te gebruiken in Java

## Inleiding
In deze tutorial wordt stap‑voor‑stap gedemonstreerd **how to use aspose** voor het afhandelen van ontbrekende resources in HTML. We maken een eenvoudig HTML‑document dat naar een ontbrekende afbeelding verwijst, koppelen een aangepaste berichtverwerker, en laten zien hoe je **load html document java** kunt gebruiken terwijl je gebroken links op een nette manier afhandelt. Aan het einde zie je ook hoe je **convert html to png** kunt uitvoeren met Aspose.HTML, waardoor je een volledig beeld krijgt van HTML‑naar‑afbeelding conversie in Java.

## Snelle antwoorden
- **Wat is het primaire doel van een berichtverwerker?** Om netwerkoperaties te onderscheppen en te reageren op statuscodes zoals ontbrekende resources.  
- **Kan Aspose.HTML HTML naar PNG converteren?** Ja, met `Converter.convertHTML` kun je html‑naar‑afbeelding conversie uitvoeren.  
- **Heb ik een licentie nodig voor dit voorbeeld?** Een tijdelijke licentie verwijdert evaluatielimieten; een permanente licentie is vereist voor productie.  
- **Welke Java‑versie wordt ondersteund?** Elke JDK 8+ (de tutorial gebruikt JDK 11).  
- **Is het mogelijk om meerdere gebroken links af te handelen?** Absoluut – je kunt meerdere verwerkers schakelen om verschillende scenario's te beheren.

## Vereisten
1. Java Development Kit (JDK): Zorg ervoor dat je JDK op je systeem hebt geïnstalleerd. Je kunt het downloaden van de [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. Aspose.HTML for Java: Je moet Aspose.HTML for Java geïnstalleerd hebben. Je kunt het downloaden van de [Aspose releases page](https://releases.aspose.com/html/java/).  
3. IDE: Gebruik je favoriete Java Integrated Development Environment (IDE) zoals IntelliJ IDEA, Eclipse of NetBeans.  
4. Basiskennis van Java: Vertrouwdheid met Java‑programmeren is essentieel om deze tutorial effectief te volgen.  
5. Tijdelijke licentie: Als je de proefversie van Aspose.HTML gebruikt, overweeg dan een [temporary license](https://purchase.aspose.com/temporary-license/) aan te schaffen om beperkingen tijdens ontwikkeling te vermijden.

## Importeer pakketten
Voordat we beginnen, zorg ervoor dat je de benodigde pakketten in je Java‑project hebt geïmporteerd. Hieronder staan de essentiële imports die je nodig hebt:
```java
import java.io.IOException;
```
Deze imports geven je toegang tot de klassen en methoden die nodig zijn voor het afhandelen van netwerkoperaties, het maken van HTML‑documenten, en het uitvoeren van de HTML‑naar‑PNG conversie.

## Stap 1: Bereid de HTML‑code voor
Het eerste wat we nodig hebben is een eenvoudige HTML‑snippet die naar een afbeeldingsbestand verwijst. We zullen bewust een afbeelding refereren die niet bestaat om het foutafhandelingsmechanisme te activeren.
```java
String code = "<img src='missing.jpg'>";
```
Deze code maakt een `<img>`‑tag die wijst naar `missing.jpg`. Omdat de afbeelding ontbreekt, zal de netwerksservice een statuscode anders dan 200 teruggeven, die onze aangepaste verwerker zal opvangen.

## Stap 2: Schrijf de HTML‑code naar een bestand
Vervolgens moeten we de HTML‑snippet opslaan zodat Aspose.HTML het kan laden als een document.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
Met een `FileWriter` slaan we de HTML op naar **document.html**. Dit bestand wordt later de bron voor de **load html document java** stap.

## Stap 3: Maak een aangepaste berichtverwerker
Laten we nu een aangepaste berichtverwerker bouwen die reageert wanneer de afbeelding niet gevonden kan worden. De verwerker controleert de HTTP‑statuscode en print een vriendelijke boodschap.
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
De `invoke`‑methode onderzoekt `context.getResponse().getStatusCode()`. Als deze niet **200** is, geven we een duidelijke waarschuwing dat het bestand ontbreekt. De laatste `invoke(context);`‑aanroep geeft de controle door aan de volgende verwerker in de keten.

## Stap 4: Configureer de netwerksservice
Om Aspose.HTML op de hoogte te stellen van onze verwerker, registreren we deze bij de netwerksservice via de `Configuration`‑klasse.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Hier maken we een `Configuration`‑instantie, halen de `INetworkService` op, en voegen onze aangepaste verwerker toe aan de collectie. Dit zorgt ervoor dat de verwerker wordt uitgevoerd tijdens elk netwerkverzoek, zoals het laden van afbeeldingen.

## Stap 5: Laad het HTML‑document
Met de configuratie klaar, kunnen we nu het HTML‑bestand laden dat we eerder hebben gemaakt. Deze stap demonstreert **load html document java** terwijl de ontbrekende afbeelding onze verwerker activeert.
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
De `HTMLDocument`‑constructor ontvangt zowel het bestandspad als de aangepaste `configuration`. Wanneer het document de `<img>`‑tag parseert, probeert de netwerksservice `missing.jpg` op te halen, krijgt een 404, en onze verwerker print de waarschuwing.

## Stap 6: Converteer HTML naar PNG
Om de bredere mogelijkheden van Aspose.HTML te illustreren, converteren we het geladen document naar een PNG‑afbeelding. Dit is een klassiek **convert html to png** scenario.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` neemt het `HTMLDocument`, optionele `ImageSaveOptions` (waar je DPI, kwaliteit, enz. kunt instellen), en de output‑bestandsnaam. Het resultaat is een rasterafbeelding van de gerenderde HTML.

## Stap 7: Ruim bronnen op
Goed resource‑beheer is essentieel in elke Java‑applicatie. We ruimen zowel de `Configuration` als de `HTMLDocument` op om geheugenlekken te voorkomen.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Het omhullen van de opruiming in een `finally`‑block garandeert uitvoering zelfs als er eerder een uitzondering optreedt.

## Waarom berichtverwerkers gebruiken?
Berichtverwerkers geven je fijnmazige controle over netwerkoperaties zoals **handle broken links java**. In plaats van de bibliotheek stilzwijgend te laten falen, kun je loggen, opnieuw proberen, resources vervangen, of fallback‑content bieden—waardoor je HTML‑verwerking robuust en productie‑klaar wordt.

## Veelvoorkomende problemen en oplossingen
- **Handler‑recursie** – Zorg ervoor dat je `invoke(context);` slechts één keer aanroept om oneindige lussen te voorkomen.  
- **Ontbrekende licentie** – Zonder een geldige licentie kan de conversie een watermerk‑afbeelding opleveren.  
- **Bestandspad‑fouten** – Gebruik absolute paden of stel de werkmap correct in bij het laden van `document.html`.

## Veelgestelde vragen

**V: Kan ik meerdere berichtverwerkers schakelen?**  
A: Ja, je kunt meerdere verwerkers toevoegen aan de `network.getMessageHandlers()` collectie; ze worden uitgevoerd in de volgorde waarin ze zijn toegevoegd.

**V: Werkt de verwerker ook voor CSS‑ of script‑resources?**  
A: Absoluut—elk netwerkverzoek dat door de HTML‑engine wordt gedaan (afbeeldingen, CSS, JS, fonts) gaat door de verwerker.

**V: Hoe wijzig ik het HTTP‑verzoek voordat het wordt verzonden?**  
A: Implementeer een verwerker die `context.getRequest()` wijzigt voordat `invoke(context)` wordt aangeroepen.

**V: Is er een manier om de waarschuwing voor specifieke URL’s te onderdrukken?**  
A: Inspecteer binnen de verwerker `context.getRequest().getRequestUri()` en sla het loggen conditioneel over.

**V: Welke versie van Aspose.HTML is vereist voor deze API’s?**  
A: De code werkt met Aspose.HTML for Java 22.10 en later.

## Conclusie
En daar heb je het—een uitgebreide gids over **how to use aspose** berichtverwerkers in Java. We hebben het maken van een HTML‑bestand behandeld, het aansluiten van een aangepaste verwerker op **handle broken links java**, het laden van het document, en het uitvoeren van **convert html to png**. Met dit patroon kun je zelfverzekerd ontbrekende resources beheren, aangepaste beleidsregels afdwingen en de netwerkmogelijkheden van Aspose.HTML uitbreiden in elke Java‑applicatie.

---

**Laatst bijgewerkt:** 2025-12-10  
**Getest met:** Aspose.HTML for Java 24.11  
**Auteur:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}