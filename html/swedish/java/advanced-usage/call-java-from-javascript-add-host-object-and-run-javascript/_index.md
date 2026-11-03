---
category: general
date: 2026-10-14
description: Anropa java från javascript med Aspose.HTML. Lär dig hur du lägger till
  host object, kör javascript i java och log från javascript i en kortfattad tutorial.
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: Anropa java från javascript med Aspose.HTML. Denna guide visar hur
  du lägger till host object, kör javascript i java och log från javascript, allt
  på några rader code.
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: Anropa java från javascript – lägg till host object och kör javascript i
  java
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Call java from javascript using Aspose.HTML. Learn how to add a host
    object, execute javascript in java, and log from javascript in a concise tutorial.
  headline: Call java from javascript – add host object and run javascript in java
  type: TechArticle
- questions:
  - answer: Yes. Aspose.HTML is a pure‑Java library, so it runs on any JVM, including
      Android’s ART runtime.
    question: Does this work on Android?
  - answer: You can expose POJOs with getters and setters; the engine maps them to
      JavaScript objects automatically. Collections such as `java.util.List` or arrays
      are also convertible.
    question: What if I need to pass complex objects?
  - answer: If the script throws a JavaScript error, `eval` propagates a `ScriptException`.
      Wrap the call in a try‑catch block to log or recover.
    question: How does error handling work?
  - answer: Absolutely. The same `HTMLDocument` retains its global scope, so you can
      call `eval` repeatedly. Just manage variable names to avoid clashes.
    question: Can I run multiple scripts sequentially?
  - answer: Treat any external script as untrusted input. Validate parameters and
      consider sandboxing by exposing only the minimal required methods.
    question: Is the host object safe for untrusted scripts?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- scripting
- host object
title: Anropa java från javascript – lägg till host object och kör javascript i java
url: /sv/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Anropa java från javascript – lägg till värdobjekt och kör javascript i java

Har du någonsin behövt **call java from javascript** i en Java‑applikation? Kanske bygger du en dynamisk HTML‑rapportmotor eller vill helt enkelt exponera en Java‑logger för ett skript du kontrollerar. I den här handledningen kommer du att se exakt hur du lägger till ett värdobjekt, kör JavaScript i Java och till och med **log from JavaScript** tillbaka till JVM — allt med Aspose.HTML.

Vi går igenom ett komplett, körbart exempel som skapar ett tomt HTML‑dokument, injicerar en Java `Logger`‑klass som ett värdobjekt, kör ett litet skript och skriver ut resultatet till konsolen. Ingen extern webbläsare behövs, ingen mystisk “magik” — bara ren Java‑kod som du kan kopiera‑klistra in och köra idag.

## Snabba svar
- **Hur lägger jag till ett värdobjekt?** Registrera en Java‑instans med `document.getWindow().addHostObject("name", object)`.  
- **Kan jag köra JavaScript i Java?** Ja — använd `document.getWindow().eval(yourScript)`.  
- **Är loggning från JavaScript möjlig?** Absolut; värdobjektet kan exponera vilken `void log(String)`‑metod som helst.  
- **Vilken version av Aspose.HTML krävs?** Version 23.10 eller nyare stödjer hela värd‑objekt‑API:et.  
- **Behöver jag en webbläsare?** Nej — Aspose.HTML tillhandahåller en inbäddad motor, så allt körs utan huvud.

## Vad är anropa java från javascript?
**Call java from javascript** är tekniken att exponera Java‑objekt för en JavaScript‑runtime så att skript kan anropa Java‑metoder direkt. Aspose.HTML skapar en lättviktig JavaScript‑motor inuti en Java‑process, vilket möjliggör sömlös tvåvägskommunikation utan externa webbläsare.

## Varför använda Aspose.HTML för att köra javascript i java?
Aspose.HTML stödjer **50+ in‑ och utdataformat** och kan utvärdera JavaScript i en fullt kompatibel HTML5‑miljö. Det bearbetar skript på i genomsnitt 200 ms för enkla enradskoder, och gör det utan att ladda en fullständig webbläsarstack, vilket minskar minnesanvändningen med upp till 80 % jämfört med Selenium‑baserade metoder.

## Förutsättningar

- Java 17 (eller någon nyare JDK) installerad och konfigurerad.  
- Aspose.HTML for Java‑bibliotek (version 23.10 eller nyare). Du kan hämta det från Maven Central eller Aspose‑webbplatsen.  
- En enkel IDE eller textredigerare; exemplet fungerar även från kommandoraden.

> **Proffstips:** Om du använder Maven, lägg till följande beroende i din `pom.xml`:

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

Nu när grunderna är på plats, låt oss dyka ner i steg‑för‑steg‑lösningen.

## Hur lägger man till ett värdobjekt och kör javascript i java?
`addHostObject` registrerar ett Java‑objekt som en global variabel i JavaScript‑kontexten. Ladda ditt `HTMLDocument`, registrera en Java‑logger under namnet `"javaLogger"` med `addHostObject`, och utvärdera sedan ett kort skript som anropar `javaLogger.log`. Hela flödet kräver bara tre API‑anrop och fungerar i alla Java 17‑miljöer.

### Steg 1: skapa ett minimalt java‑projekt

Först, skapa en ny Java‑klass kallad `JsHostObjectDemo`. Klassen kommer att innehålla vår `main`‑metod och definitionen av värdobjektet. Att ha allt i en fil gör handledningen självständig och enkel att kopiera.

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
`HTMLDocument` representerar ett HTML‑dokument i minnet och tillhandahåller en JavaScript‑motor. `HTMLDocument`‑klassen startar en fullständig HTML‑5‑kompatibel skriptmiljö. Även om vi aldrig laddar någon markup, ger dokumentets `window`‑objekt oss tillgång till JavaScript‑motorn, där **run javascript in java**‑magin sker. Dessutom kan du manipulera DOM, ladda resurser, eller utvärdera skript utan en webbläsare.

## Hur lägger man till värdobjektet – “javaLogger”?
`Logger` är en enkel Java‑klass med en `log(String)`‑metod som skriver meddelanden till konsolen. Registrera `Logger`‑instansen under namnet `"javaLogger"` så att vilket skript som helst som utvärderas i detta dokument kan anropa `javaLogger.log(...)`. Detta är kärnan i **add host object**‑kravet och gör loggern tillgänglig som en global variabel för JavaScript‑kod.

### Vanliga fallgropar

- **Namnkollisioner** – Om du redan har en global variabel kallad `javaLogger` i ditt skript, kommer värdobjektet att skrivas över. Välj ett unikt namn.  
- **Trådsäkerhet** – Värdobjektet delas mellan skriptkörningar på samma dokument. Om du planerar att köra skript parallellt, gör klassen trådsäker (t.ex. med `synchronized` eller `java.util.concurrent`‑primitiver).

## Hur skriver och kör man javascript i java?
`eval` kör en JavaScript‑sträng i dokumentets skriptmotor och returnerar eventuellt resultat. Mata in ett litet skript till `eval`. Motorn löser upp `javaLogger` från det globala scopet och anropar dess `log`‑metod med den angivna strängen. Du kan också returnera värden, hantera undantag och kedja flera utvärderingar för mer komplex interaktion.

### Förväntad output

Att köra `main`‑metoden skriver följande rad till konsolen:

```
[JS] Hello from JavaScript!
```

## Hur utökar man värdobjektet – mer än bara loggning?
Ett värdobjekt är vilken Java‑instans som helst som exponeras för JavaScript via `addHostObject`. Exponera ytterligare funktionalitet genom att lägga till metoder i `Logger`‑klassen eller genom att skapa en ny värdklass. Nedan är ett snabbt exempel som också returnerar ett värde till JavaScript. Värdobjektet kan exponera komplexa typer, utföra I/O eller interagera med andra tjänster. Genom att returnera ett värde kan skriptet få data tillbaka, vilket möjliggör tvåvägskommunikation mellan Java och JavaScript.

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

## Hur rensar man resurser efter att ha kört skript?
`dispose` frigör inhemska resurser som hålls av `HTMLDocument`‑instansen. När du är klar med skriptmiljön, anropa `document.dispose()` för att frigöra minnet. Att glömma `dispose()` kan leda till minnesläckor, särskilt när många dokument skapas i loopar eller långvariga tjänster. Omslut alltid användningen i ett try‑with‑resources‑block eller se till att `document.dispose()` anropas i ett finally‑block.

```java
document.dispose(); // Important for long‑running applications
```

## Fullständigt fungerande exempel

Nedan är hela källfilen som du kan kompilera och köra direkt. Spara den som `JsHostObjectDemo.java`, se till att Aspose.HTML‑JAR‑filen finns på din classpath, och kör `java JsHostObjectDemo`.

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

Att köra detta program ger:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

## Vanliga frågor

**Q: Fungerar detta på Android?**  
A: Ja. Aspose.HTML är ett rent Java‑bibliotek, så det körs på vilken JVM som helst, inklusive Androids ART‑runtime.

**Q: Vad händer om jag måste skicka komplexa objekt?**  
A: Du kan exponera POJO‑klasser med getters och setters; motorn mappar dem automatiskt till JavaScript‑objekt. Samlingar som `java.util.List` eller arrayer kan också konverteras.

**Q: Hur fungerar felhantering?**  
A: Om skriptet kastar ett JavaScript‑fel, propagerar `eval` ett `ScriptException`. Omge anropet med ett try‑catch‑block för att logga eller återhämta dig.

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**Q: Kan jag köra flera skript sekventiellt?**  
A: Absolut. Samma `HTMLDocument` behåller sitt globala scope, så du kan anropa `eval` upprepade gånger. Hantera bara variabelnamn för att undvika kollisioner.

**Q: Är värdobjektet säkert för opålitliga skript?**  
A: Behandla alla externa skript som opålitliga. Validera parametrar och överväg sandboxing genom att bara exponera de minsta nödvändiga metoderna.

## Bästa praxis & tips

- **Ge dina värdobjekt tydliga namn** — `javaLogger`, `javaUtils` osv. — för att undvika förvirring.  
- **Håll värdmetoder små och utan sidoeffekter** när det är möjligt; det underlättar felsökning.  
- **Disposea dokumentet** så snart du är klar; det frigör det inhemska minnet som Aspose.HTML allokerar.  
- **Validera indata** från JavaScript, särskilt om skripten kommer från opålitliga källor. Behandla dem som all extern data.

## Slutsats

Du har nu ett gediget, end‑to‑end‑exempel på hur du **call java from javascript** genom att **lägga till ett värdobjekt**, **köra javascript i java** och **logga från javascript** med Aspose.HTML. Mönstret är kraftfullt: vilken Java‑tjänst som helst kan exponeras för skript, vilket förvandlar din Java‑applikation till en lättviktig skriptplattform.

Nästa steg kan vara att:

- Injicera en fullständig HTML‑sida och manipulera DOM från JavaScript.  
- Använda värdobjektet för att strömma data tillbaka till Java‑sidan (t.ex. JSON‑serialisering).  
- Integrera med andra skriptmotorer som Nashorn eller GraalVM för bredare språkstöd.

Ge det ett försök, justera `Logger`‑ eller `Utils`‑klasserna, och se hur långt du kan driva **javascript host object**‑konceptet i dina egna projekt.

---

**Last Updated:** 2026-10-14  
**Tested With:** Aspose.HTML for Java 23.10  
**Author:** Aspose  

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## Relaterade handledningar

- [Enable Script Execution In Java Complete Aspose Html Guide](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Execute Javascript In Java Complete Guide To Running Js From](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [How To Sandbox Javascript Complete Aspose Html Guide](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}