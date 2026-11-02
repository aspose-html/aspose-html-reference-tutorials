---
category: general
date: 2026-03-14
description: Lär dig hur du anropar Java från JavaScript med Aspose.HTML. Den här
  guiden visar hur du lägger till ett värdobjekt, kör JavaScript i Java och loggar
  från JavaScript.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: sv
og_description: Anropa Java från JavaScript med Aspose.HTML. Lägg till ett värdobjekt,
  kör JavaScript i Java och logga från JavaScript i en enda handledning.
og_title: Anropa Java från JavaScript – Komplett guide med värdobjekt
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: Anropa Java från JavaScript – Lägg till värdobjekt och kör JavaScript i Java
url: /sv/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Anropa Java från JavaScript – Lägg till värdobjekt och kör JavaScript i Java

Har du någonsin behövt **call Java from JavaScript** i en Java‑applikation? Kanske bygger du en dynamisk HTML‑rapportmotor eller vill helt enkelt exponera en Java‑logger för ett skript du kontrollerar. I den här handledningen kommer du att se exakt hur du lägger till ett värdobjekt, kör JavaScript i Java och till och med **log from JavaScript** tillbaka till JVM‑en — allt med Aspose.HTML.

Vi går igenom ett komplett, körbart exempel som skapar ett tomt HTML‑dokument, injicerar en Java `Logger`‑klass som ett värdobjekt, kör ett litet skript och skriver ut resultatet till konsolen. Ingen extern webbläsare behövs, ingen mystisk “magik” — bara ren Java‑kod som du kan kopiera‑klistra in och köra idag.

## Förutsättningar

- Java 17 (eller någon nyare JDK) installerad och konfigurerad.
- Aspose.HTML för Java‑biblioteket (version 23.10 eller senare). Du kan hämta det från Maven Central eller Aspose‑webbplatsen.
- En enkel IDE eller textredigerare; exemplet fungerar även från kommandoraden.

> **Pro tip:** Om du använder Maven, lägg till följande beroende i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Eller, för Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Nu när vi har grunderna på plats, låt oss dyka ner i steg‑för‑steg‑lösningen.

## Steg 1: Skapa ett minimalt Java‑projekt

Först, skapa en ny Java‑klass som heter `JsHostObjectDemo`. Klassen kommer att innehålla vår `main`‑metod och definitionen av värdobjektet. Att hålla allt i en fil gör handledningen självständig och enkel att kopiera.

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

### Varför ett `HTMLDocument`?

Aspose.HTML:s `HTMLDocument`‑klass startar upp en fullständig HTML‑5‑kompatibel skriptmiljö. Även om vi aldrig laddar någon markup, ger dokumentets `window`‑objekt oss åtkomst till JavaScript‑motorn, vilket är där magin med **run JavaScript in Java** sker.

## Steg 2: Lägg till värdobjektet – “javaLogger”

Raden

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

utför det tunga arbetet för kravet **add host object**. Genom att registrera `Logger`‑instansen under namnet `"javaLogger"` kan vilket skript som helst som evalueras i detta dokument anropa `javaLogger.log(...)`. Detta är kärnan i konceptet **javascript host object**: en brygga som låter JavaScript nå in i JVM.

### Vanliga fallgropar

- **Naming collisions** – Om du redan har en global variabel som heter `javaLogger` i ditt skript, kommer värdobjektet att skrivas över. Välj ett unikt namn.
- **Thread safety** – Värdobjektet delas mellan skriptkörningar på samma dokument. Om du planerar att köra skript samtidigt, gör värdklassen trådsäker (t.ex. använd `synchronized` eller `java.util.concurrent`‑primitiver).

## Steg 3: Skriv och kör JavaScript

Skriptet som vi matar in i `eval` är avsiktligt litet:

```javascript
javaLogger.log('Hello from JavaScript!');
```

När `document.getWindow().eval(script)` körs, letar motorn upp `javaLogger` i sitt globala omfång, hittar Java‑objektet vi lade till och anropar dess `log`‑metod med den angivna strängen.

### Förväntad utskrift

Kör du `main`‑metoden skrivs följande rad ut till konsolen:

```
[JS] Hello from JavaScript!
```

## Steg 4: Utöka värdobjektet – mer än bara loggning

Om du behöver exponera ytterligare funktionalitet (t.ex. filåtkomst, databasfrågor), lägg bara till fler metoder i `Logger`‑klassen — eller skapa en helt ny värdklass. Här är ett snabbt exempel som också returnerar ett värde:

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

Nu visar konsolen:

```
[JS] 3+4=7
```

## Steg 5: Rensa upp resurser

När du är klar med skriptmiljön, avlossa `HTMLDocument` för att frigöra inhemska resurser:

```java
document.dispose(); // Important for long‑running applications
```

Att hoppa över avlopp kan leda till minnesläckor, särskilt om du skapar många dokument i en loop.

## Fullt fungerande exempel

Nedan är den kompletta källfilen som du kan kompilera och köra omedelbart. Spara den som `JsHostObjectDemo.java`, se till att Aspose.HTML‑JAR‑filen finns på din classpath, och kör `java JsHostObjectDemo`.

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

Kör du detta program får du:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

## Vanliga frågor

### Fungerar detta på Android?

Aspose.HTML är ett rent Java‑bibliotek, så det körs på vilken JVM som helst, inklusive Androids Dalvik/ART. Bara paketera JAR‑filen så har du samma värdobjekt‑funktionalitet.

### Vad händer om jag behöver skicka komplexa objekt?

Du kan exponera POJO:n (plain old Java objects) som innehåller fält, getters och setters. Motorn mappar dem automatiskt till JavaScript‑objekt. För samlingar, använd `java.util.List` eller arrayer — båda är konverterbara.

### Hur fungerar felhantering?

Om skriptet kastar ett JavaScript‑fel, kommer `eval` att propagera ett `ScriptException`. Omslut anropet i ett try‑catch‑block för att logga eller återhämta:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### Kan jag köra flera skript sekventiellt?

Absolut. Samma `HTMLDocument`‑instans behåller sitt globala omfång, så du kan anropa `eval` upprepade gånger. Var bara medveten om variabelnamnskrockar mellan skript.

## Bästa praxis & tips

- **Namnge dina värdobjekt tydligt** — `javaLogger`, `javaUtils` osv. — för att undvika förvirring.
- **Håll värdmetoder små och utan sidoeffekter** när det är möjligt; det underlättar felsökning.
- **Avlossa dokumentet** så snart du är klar; det frigör inhemskt minne som Aspose.HTML allokerar.
- **Validera indata** från JavaScript, särskilt om skript kommer från opålitliga källor. Behandla dem som all extern data.

## Slutsats

Du har nu ett gediget, end‑to‑end‑exempel på hur du **call java from javascript** genom att **add a host object**, **run JavaScript in Java**, och **log from JavaScript** med Aspose.HTML. Mönstret är kraftfullt: vilken Java‑tjänst som helst kan exponeras för skript, vilket förvandlar din Java‑applikation till en lättviktig skriptplattform.

Nästa steg kan du utforska:

- Att injicera en fullständig HTML‑sida och manipulera DOM från JavaScript.
- Att använda värdobjektet för att strömma data tillbaka till Java‑sidan (t.ex. JSON‑serialisering).
- Att integrera med andra skriptmotorer som Nashorn eller GraalVM för bredare språkstöd.

Prova det, justera `Logger`‑ eller `Utils`‑klasserna, och se hur långt du kan driva **javascript host object**‑konceptet i dina egna projekt

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}