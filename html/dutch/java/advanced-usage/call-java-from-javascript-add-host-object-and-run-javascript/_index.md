---
category: general
date: 2026-03-14
description: Leer hoe je Java vanuit JavaScript kunt aanroepen met Aspose.HTML. Deze
  gids laat zien hoe je een hostobject toevoegt, JavaScript in Java uitvoert en logt
  vanuit JavaScript.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: nl
og_description: Roep Java aan vanuit JavaScript met Aspose.HTML. Voeg een hostobject
  toe, voer JavaScript uit in Java en log vanuit JavaScript in één tutorial.
og_title: Java vanuit JavaScript aanroepen – Complete gids met hostobject
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: Java aanroepen vanuit JavaScript – Hostobject toevoegen en JavaScript uitvoeren
  in Java
url: /nl/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java aanroepen vanuit JavaScript – Hostobject toevoegen en JavaScript uitvoeren in Java

Heb je ooit nodig gehad om **Java vanuit JavaScript** aan te roepen binnen een Java‑applicatie? Misschien bouw je een dynamische HTML‑rapportengine of wil je simpelweg een Java‑logger beschikbaar maken voor een script dat je beheert. In deze tutorial zie je precies hoe je een hostobject toevoegt, JavaScript uitvoert in Java, en zelfs **logt vanuit JavaScript** terug naar de JVM—allemaal met Aspose.HTML.

We lopen een compleet, uitvoerbaar voorbeeld door dat een leeg HTML‑document maakt, een Java `Logger`‑klasse injecteert als hostobject, een klein script uitvoert, en het resultaat naar de console print. Geen externe webbrowser nodig, geen mystieke “magie”—gewoon platte Java‑code die je vandaag kunt kopiëren‑plakken en uitvoeren.

## Vereisten

- Java 17 (of een recente JDK) geïnstalleerd en geconfigureerd.
- Aspose.HTML for Java‑bibliotheek (versie 23.10 of nieuwer). Je kunt deze verkrijgen via Maven Central of de Aspose‑website.
- Een eenvoudige IDE of teksteditor; het voorbeeld werkt ook vanaf de commandoregel.

> **Tip:** Als je Maven gebruikt, voeg dan de volgende afhankelijkheid toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Of, voor Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Nu we de basis hebben geregeld, duiken we in de stap‑voor‑stap oplossing.

## Stap 1: Maak een minimaal Java‑project

Eerst maak je een nieuwe Java‑klasse genaamd `JsHostObjectDemo`. Deze klasse bevat onze `main`‑methode en de definitie van het hostobject. Alles in één bestand houden maakt de tutorial zelf‑voorzienend en makkelijk te kopiëren.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### Waarom een `HTMLDocument`?

De `HTMLDocument`‑klasse van Aspose.HTML start een volledige HTML‑5‑conforme scripting‑omgeving. Hoewel we nooit markup laden, geeft het `window`‑object van het document ons toegang tot de JavaScript‑engine, waar de **run JavaScript in Java**‑magie plaatsvindt.

## Stap 2: Voeg het hostobject toe – “javaLogger”

De regel

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

doet het zware werk voor de **add host object**‑vereiste. Door de `Logger`‑instantie te registreren onder de naam `"javaLogger"`, kan elk script dat in dit document wordt geëvalueerd `javaLogger.log(...)` aanroepen. Dit is de kern van het **javascript host object**‑concept: een brug die JavaScript toegang geeft tot de JVM.

### Veelvoorkomende valkuilen

- **Naamconflicten** – Als je al een globale variabele `javaLogger` in je script hebt, wordt het hostobject overschreven. Kies een unieke naam.
- **Thread‑veiligheid** – Het hostobject wordt gedeeld tussen script‑executies op hetzelfde document. Als je scripts gelijktijdig wilt uitvoeren, maak de host‑klasse thread‑safe (bijv. gebruik `synchronized` of `java.util.concurrent`‑primitieven).

## Stap 3: Schrijf en voer JavaScript uit

Het script dat we aan `eval` geven is opzettelijk klein:

```javascript
javaLogger.log('Hello from JavaScript!');
```

Wanneer `document.getWindow().eval(script)` wordt uitgevoerd, zoekt de engine `javaLogger` op in de globale scope, vindt het Java‑object dat we hebben toegevoegd, en roept de `log`‑methode aan met de meegegeven string.

### Verwachte uitvoer

Het uitvoeren van de `main`‑methode print de volgende regel naar de console:

```
[JS] Hello from JavaScript!
```

Die kleine regel bewijst dat we succesvol **call java from javascript** hebben uitgevoerd, en dat de **log from javascript** precies verschijnt waar een normale Java `System.out`‑melding zou staan.

## Stap 4: Het hostobject uitbreiden – meer dan alleen loggen

Als je extra functionaliteit wilt blootstellen (bijv. bestands‑toegang, database‑query’s), voeg dan simpelweg meer methoden toe aan de `Logger`‑klasse — of maak een geheel nieuwe host‑klasse. Hier is een snel voorbeeld dat ook een waarde retourneert:

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

Nu toont de console:

```
[JS] 3+4=7
```

Dit demonstreert de flexibiliteit van het **javascript host object**‑patroon: je kunt elke Java‑API blootstellen die je nodig hebt, zolang de datatypes converteerbaar zijn tussen Java en JavaScript (primitieven, strings, arrays, enz.).

## Stap 5: Resources opruimen

Wanneer je klaar bent met de scripting‑omgeving, disposeer je het `HTMLDocument` om native resources vrij te geven:

```java
document.dispose(); // Important for long‑running applications
```

Het overslaan van disposen kan leiden tot geheugenlekken, vooral als je veel documenten in een lus maakt.

## Volledig werkend voorbeeld

Hieronder staat het volledige bronbestand dat je direct kunt compileren en uitvoeren. Sla het op als `JsHostObjectDemo.java`, zorg dat de Aspose.HTML‑JAR op je classpath staat, en voer `java JsHostObjectDemo` uit.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

Het uitvoeren van dit programma levert:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

Dat is de volledige **call java from javascript**‑workflow in een handvol regels.

## Veelgestelde vragen

### Werkt dit op Android?

Aspose.HTML is een pure‑Java‑bibliotheek, dus hij draait op elke JVM, inclusief Android’s Dalvik/ART. Voeg simpelweg de JAR toe en je hebt dezelfde host‑object‑mogelijkheden.

### Wat als ik complexe objecten moet doorgeven?

Je kunt POJO’s (plain old Java objects) blootstellen die velden, getters en setters bevatten. De engine zal ze automatisch naar JavaScript‑objecten mappen. Voor collecties gebruik je `java.util.List` of arrays — beide zijn converteerbaar.

### Hoe werkt foutafhandeling?

Als het script een JavaScript‑fout gooit, zal `eval` een `ScriptException` propageren. Omring de aanroep met een try‑catch‑blok om te loggen of te herstellen:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### Kan ik meerdere scripts achter elkaar uitvoeren?

Absoluut. Dezelfde `HTMLDocument`‑instantie behoudt zijn globale scope, zodat je `eval` herhaaldelijk kunt aanroepen. Let alleen op variabelen‑naamconflicten tussen scripts.

## Best practices & tips

- **Geef je hostobjecten duidelijke namen** — `javaLogger`, `javaUtils`, enz. — om verwarring te voorkomen.
- **Houd hostmethoden klein en zonder bijwerkingen** waar mogelijk; dit maakt debuggen makkelijker.
- **Disposeer het document** zodra je klaar bent; dit vrijgeeft native geheugen dat Aspose.HTML reserveert.
- **Valideer invoer** vanuit JavaScript, vooral als scripts van onbetrouwbare bronnen komen. Behandel ze als elke andere externe data.

## Conclusie

Je hebt nu een solide, end‑to‑end‑voorbeeld van hoe je **call java from javascript** kunt doen door **een hostobject toe te voegen**, **JavaScript in Java uit te voeren**, en **logt vanuit JavaScript** met behulp van Aspose.HTML. Het patroon is krachtig: elke Java‑service kan aan scripts worden blootgesteld, waardoor je Java‑applicatie een lichtgewicht scripting‑platform wordt.

Vervolgens kun je verkennen:

- Het injecteren van een volledige HTML‑pagina en het manipuleren van de DOM vanuit JavaScript.
- Het gebruik van het hostobject om gegevens terug te streamen naar de Java‑kant (bijv. JSON‑serialisatie).
- Integratie met andere scripting‑engines zoals Nashorn of GraalVM voor bredere taalondersteuning.

Probeer het, pas de `Logger`‑ of `Utils`‑klassen aan, en kijk hoe ver je het **javascript host object**‑concept in je eigen projecten kunt duwen.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}