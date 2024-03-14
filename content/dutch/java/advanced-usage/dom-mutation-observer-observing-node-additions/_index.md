---
title: DOM Mutation Observer met Aspose.HTML voor Java
linktitle: DOM Mutation Observer - Toevoegingen van knooppunten observeren
second_title: Java HTML-verwerking met Aspose.HTML
description: Leer in deze stapsgewijze handleiding hoe u Aspose.HTML voor Java kunt gebruiken om een DOM Mutation Observer te implementeren. Bewaak en reageer effectief op DOM-veranderingen.
type: docs
weight: 11
url: /nl/java/advanced-usage/dom-mutation-observer-observing-node-additions/
---

Bent u een Java-ontwikkelaar en wilt u veranderingen in het Document Object Model (DOM) van een HTML-document observeren en erop reageren? Aspose.HTML voor Java biedt een krachtige oplossing voor deze taak. In deze stapsgewijze handleiding onderzoeken we hoe u Aspose.HTML voor Java kunt gebruiken om een HTML-document te maken en knooppunttoevoegingen te observeren met een Mutation Observer. Deze tutorial begeleidt u door het proces, waarbij elk voorbeeld in meerdere stappen wordt opgesplitst. Uiteindelijk zult u DOM Mutation Observers gemakkelijk in uw Java-projecten kunnen implementeren.

## Vereisten

Voordat we ingaan op het gebruik van Aspose.HTML voor Java, moeten we ervoor zorgen dat u aan de noodzakelijke vereisten voldoet:

1. Java-ontwikkelomgeving: Zorg ervoor dat Java Development Kit (JDK) op uw systeem is geïnstalleerd.

2.  Aspose.HTML voor Java: U moet Aspose.HTML voor Java downloaden en installeren. Je kunt de downloadlink vinden[hier](https://releases.aspose.com/html/java/).

3. IDE (Integrated Development Environment): Gebruik uw favoriete Java IDE, zoals IntelliJ IDEA of Eclipse, voor het schrijven en uitvoeren van Java-code.

## Pakketten importeren

Om aan de slag te gaan met Aspose.HTML voor Java, moet u de vereiste pakketten in uw Java-code importeren. Hier ziet u hoe u het kunt doen:

```java
// Importeer de benodigde pakketten
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

// Maak een leeg HTML-document
HTMLDocument document = new HTMLDocument();
```

Nu u de vereiste pakketten heeft geïmporteerd, gaan we verder met de stapsgewijze handleiding voor het implementeren van een DOM Mutation Observer in Java.

## Stap 1: Maak een Mutation Observer-instantie

Eerst moet u een Mutation Observer-instantie maken. Deze waarnemer let op veranderingen in de DOM en voert een callback-functie uit wanneer er mutaties optreden.

```java
MutationObserver observer = new MutationObserver(new MutationCallback() {
    @Override
    public void invoke(IGenericList<MutationRecord> mutations, MutationObserver mutationObserver) {
        mutations.forEach(mutationRecord -> {
            mutationRecord.getAddedNodes().forEach(node -> {
                synchronized (this) {
                    System.out.println("The '" + node + "' node was added to the document.");
                    notifyAll();
                }
            });
        });
    }
});
```

In deze stap creëren we een waarnemer met een callback-functie die een bericht afdrukt wanneer knooppunten aan de DOM worden toegevoegd.

## Stap 2: Configureer de waarnemer

Laten we nu de waarnemer configureren met de gewenste opties. We willen wijzigingen in de onderliggende lijst en substructuur observeren, evenals wijzigingen in tekengegevens.

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// Geef het doelknooppunt door om te observeren met de opgegeven configuratie
observer.observe(document.getBody(), config);
```

 Hier stellen we de`config` object om het observeren van wijzigingen in de onderliggende lijst, subboom en tekengegevens mogelijk te maken. Vervolgens geven we het doelknooppunt door (in dit geval het document's`<body>`) en de configuratie voor de waarnemer.

## Stap 3: Wijzig de DOM

Nu zullen we enkele wijzigingen aanbrengen in de DOM om de waarnemer te activeren. We maken een alinea-element en voegen dit toe aan de hoofdtekst van het document.

```java
// Maak een alinea-element en voeg dit toe aan de hoofdtekst van het document
Element p = document.createElement("p");
document.getBody().appendChild(p);

// Maak een tekst en voeg deze toe aan de alinea
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

In deze stap maken we een HTML-alinea-element en voegen dit toe aan de hoofdtekst van het document. Vervolgens maken we een tekstknooppunt met de inhoud "Hallo wereld" en voegen dit toe aan de alinea.

## Stap 4: Wacht op waarnemingen (asynchroon)

Omdat mutaties asynchroon worden waargenomen, moeten we even wachten voordat de waarnemer de veranderingen kan vastleggen. We zullen gebruiken`synchronized` En`wait` voor dit doel, zoals hieronder weergegeven.

```java
// Omdat mutaties in de asynchrone modus werken, moet u een paar seconden wachten
synchronized (this) {
    wait(5000);
}
```

Hier wachten we vijf seconden om er zeker van te zijn dat de waarnemer de kans heeft om eventuele mutaties vast te leggen.

## Stap 5: Stop met observeren

Als u klaar bent met observeren, is het ten slotte van essentieel belang dat u de waarnemer loskoppelt om bronnen vrij te geven.

```java
// Houd op met observeren
observer.disconnect();
```

Met deze stap hebt u de observatie voltooid en kunt u bronnen opschonen.

## Conclusie

In deze zelfstudie hebben we het proces doorlopen van het gebruik van Aspose.HTML voor Java om een DOM Mutation Observer te implementeren. Je hebt geleerd hoe je een waarnemer maakt, configureert, wijzigingen aanbrengt in de DOM, wacht op observaties en stopt met observeren. Nu beschikt u over de vaardigheden om DOM Mutation Observers in uw Java-projecten toe te passen om veranderingen in de DOM van HTML-documenten effectief te monitoren en erop te reageren.

Als u vragen heeft of problemen ondervindt, aarzel dan niet om hulp te zoeken in de[Aspose.HTML-forum](https://forum.aspose.com/) . Bovendien heeft u toegang tot de[documentatie](https://reference.aspose.com/html/java/) voor gedetailleerde informatie over Aspose.HTML voor Java.

## Veelgestelde vragen

### Vraag 1: Wat is een DOM-mutatiewaarnemer?

A1: Een DOM Mutation Observer is een JavaScript-functie waarmee u kunt kijken naar wijzigingen in het Document Object Model (DOM) van een HTML-document. Het biedt een manier om in realtime te reageren op toevoegingen, verwijderingen of wijzigingen van DOM-knooppunten.

### V2: Kan ik Aspose.HTML voor Java gebruiken in mijn commerciële projecten?

 A2: Ja, u kunt Aspose.HTML voor Java gebruiken in commerciële projecten. U kunt licentie- en aankoopinformatie vinden[hier](https://purchase.aspose.com/buy).

### V3: Is er een gratis proefversie beschikbaar voor Aspose.HTML voor Java?

 A3: Ja, u kunt een gratis proefversie van Aspose.HTML voor Java krijgen[hier](https://releases.aspose.com/). Hierdoor kunt u de functies en mogelijkheden ervan verkennen voordat u een aankoop doet.

### Vraag 4: Wat is het voordeel van het observeren van veranderingen in karaktergegevens met de Mutation Observer?

A4: Het observeren van wijzigingen in tekengegevens is handig voor scenario's waarin u wijzigingen in de tekstinhoud van HTML-elementen wilt controleren en hierop wilt reageren. U kunt het bijvoorbeeld gebruiken om gebruikersinvoer in webformulieren bij te houden en erop te reageren.

### V5: Hoe gooi ik bronnen weg als ik Aspose.HTML voor Java gebruik?

 A5: Het is belangrijk om middelen vrij te geven als je klaar bent. In ons voorbeeld hebben we gebruikt`document.dispose()` om bronnen op te ruimen die aan het HTML-document zijn gekoppeld. Zorg ervoor dat u alle objecten en bronnen die u maakt weggooit om geheugenlekken te voorkomen.