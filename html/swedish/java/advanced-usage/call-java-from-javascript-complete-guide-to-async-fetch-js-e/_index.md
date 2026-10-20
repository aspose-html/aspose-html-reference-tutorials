---
category: general
date: 2026-03-04
description: Anropa Java från JavaScript med Aspose.HTML, kör asynkron JavaScript
  och hämta JSON i Java med ett enkelt exempel. Lär dig att köra JavaScript-motorn
  effektivt.
draft: false
keywords:
- call java from javascript
- run async javascript
- fetch json in java
- asynchronous fetch api
- execute javascript engine
language: sv
og_description: Anropa Java från JavaScript med Aspose.HTML, kör asynkron JavaScript
  och hämta JSON i Java. Fullständig kod, förklaringar och tips inkluderade.
og_title: Anropa Java från JavaScript – Steg‑för‑steg asynkron hämtning‑handledning
tags:
- Java
- JavaScript
- Aspose.HTML
- Async Programming
title: Anropa Java från JavaScript – Komplett guide till asynkron hämtning och JS‑motorns
  exekvering
url: /sv/java/advanced-usage/call-java-from-javascript-complete-guide-to-async-fetch-js-e/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Anropa Java från JavaScript – Fullständig handledning med Async Fetch API

Har du någonsin undrat hur man **anropa Java från JavaScript** utan att lämna din Java‑applikation? Kanske bygger du en server‑side HTML‑renderare, eller så behöver du exponera någon Java‑logik för ett skript som körs i ett dokument. Den goda nyheten är att Aspose.HTML gör detta till en barnlek. I den här guiden kommer vi inte bara att visa dig hur du *köra async JavaScript* i ett Java‑stödd dokument, utan också hur du **hämta JSON i Java** med den moderna **asynchronous fetch API** och slutligen **exekvera JavaScript engine**‑anrop på ett säkert sätt.

Kort sagt får du ett komplett, körbart exempel som hämtar en JSON‑payload från en publik endpoint, överlämnar den till ett Java‑host‑objekt och skriver ut resultatet i konsolen. Inga externa webbservrar, inga extra bibliotek – bara ren Java och Aspose.HTML.

## Vad du kommer att lära dig

- Hur du skapar ett tomt HTML‑dokument med Aspose.HTML.  
- Hur du får tag på och **execute JavaScript engine** från Java.  
- Hur du registrerar ett Java‑host‑objekt som JavaScript kan anropa.  
- Hur du skriver en **asynchronous JavaScript**‑funktion som använder **asynchronous fetch API**.  
- Hur du hanterar den hämtade datan tillbaka i Java med en ren callback.  
- Förväntad output och felsökningstips.

### Förutsättningar

- Java 17 eller nyare (koden kompileras även med JDK 11).  
- Aspose.HTML for Java 23.7 (eller den senaste versionen vid skrivtillfället).  
- Grundläggande kunskap om Java och JavaScript‑promises.  
- Internetåtkomst för demo‑förfrågan till `jsonplaceholder`.

Om någon av dessa punkter känns obekant, panik inte – varje steg förklaras på enkel engelska, och du kommer att se exakt varför vi gör som vi gör.

---

## Steg 1 – Skapa ett tomt HTML-dokument och hämta dess JavaScript-motor

Det första vi behöver är ett tomt dokument som ger oss en sandboxad JavaScript‑miljö. Aspose.HTML:s `Document`‑klass gör exakt det.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Create an empty HTML document
        Document document = new Document();

        // Obtain the JavaScript engine associated with the document's window
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();
```

**Varför detta är viktigt:** `Document`‑objektet efterliknar ett webbläsarfönster, och dess `JavaScriptEngine` låter oss köra skript precis som en webbläsare skulle. Detta är grunden för **anropa Java från JavaScript** – motorn fungerar som bron.

---

## Steg 2 – Registrera ett host‑objekt så att JavaScript kan anropa tillbaka Java

Aspose.HTML låter dig exponera vilket Java‑objekt som helst för skriptvärlden. Vi skapar en anonym klass med en enda `onResult`‑metod som helt enkelt skriver ut den JSON vi får.

```java
        // Register a Java host object that the script can invoke
        jsEngine.addHostObject("javaCallback", new Object() {
            // This method will be called from JavaScript with the fetched JSON string
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });
```

**Förklaring:**  
- `addHostObject` binder namnet `javaCallback` till det anonyma Java‑objektet.  
- Inuti JavaScript kommer vi att anropa `javaCallback.onResult(...)`.  
- Detta är kärnan i **anropa Java från JavaScript** – skriptet når in i Java‑världen, och Java reagerar.

> **Pro tip:** Håll host‑objektets metoder `public` och enkla; komplexa objekt kan orsaka serialiseringsproblem.

---

## Steg 3 – Skriv en Asynchronous JavaScript‑funktion med det Asynchronous Fetch API

Nu kommer den roliga delen: ett litet skript som hämtar JSON från en fjärrendpoint. Vi använder `async/await`, vilket är det moderna sättet att **run async JavaScript**.

```java
        // Asynchronous script that fetches JSON and passes it to the Java host object
        String asyncScript =
            "async function fetchData() {" +
            "  const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "  const json = await response.json();" +
            "  javaCallback.onResult(JSON.stringify(json));" +
            "}" +
            "fetchData();";
```

**Varför vi väljer `fetch` framför äldre XHR:**  
- `fetch` returnerar ett `Promise`, vilket gör koden renare.  
- Det fungerar nativt med `await`, så flödet läses top‑to‑bottom – perfekt för **asynchronous fetch api**‑demoer.  
- API‑et är framtidssäkert; de flesta webbläsare och motorer (inklusive Aspose’s) stödjer det direkt.

---

## Steg 4 – Exekvera skriptet i dokumentets JavaScript‑motor

Till sist överlämnar vi skriptet till motorn. Motorn startar en liten event‑loop, löser `fetch`‑promiset och anropar tillbaka till Java när det är klart.

```java
        // Execute the async script
        jsEngine.execute(asyncScript);
    }
}
```

När du kör klassen `AsyncJsTutorial` bör du se något liknande:

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

Den outputen bekräftar tre saker:

1. **asynchronous fetch API** hämtade data framgångsrikt.  
2. JSON‑en serialiserades och överlämnades till Java.  
3. Vårt **execute javascript engine**‑anrop slutfördes utan deadlocks.

---

## Steg 5 – Hantera fel och kantfall (valfria förbättringar)

Verklig kod fungerar sällan perfekt varje gång. Nedan följer några vanliga fallgropar och hur du skyddar dig mot dem.

### 5.1 Nätverksfel

Om fjärrservern är nere kastar `fetch` ett undantag. Lägg in anropet i ett `try/catch`‑block:

```java
String asyncScript =
    "async function fetchData() {" +
    "  try {" +
    "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
    "    if (!response.ok) throw new Error('Network response was not ok');" +
    "    const json = await response.json();" +
    "    javaCallback.onResult(JSON.stringify(json));" +
    "  } catch (e) {" +
    "    javaCallback.onResult('Error: ' + e.message);" +
    "  }" +
    "}" +
    "fetchData();";
```

Nu får Java‑sidan ett felmeddelande istället för att hänga.

### 5.2 Tidsgränser

Aspose‑motorn exponerar ingen inbyggd timeout för `fetch`, men du kan implementera en i JavaScript:

```javascript
const controller = new AbortController();
setTimeout(() => controller.abort(), 5000); // 5‑second timeout
const response = await fetch(url, { signal: controller.signal });
```

### 5.3 Flera anrop

Om du behöver hämta flera resurser, loopa eller mappa över en array med URL:er. Host‑objektet kan utökas för att ta emot en identifierare, så att du kan korrelera svaren.

---

## Komplett fungerande exempel

Nedan är **full source file** som du kan kopiera‑klistra in i din IDE. Inga dolda beroenden, bara Aspose.HTML‑JAR‑filen på classpath.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an empty HTML document and obtain its JavaScript engine
        Document document = new Document();
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();

        // Step 2: Register a host object that JavaScript can call back into Java
        jsEngine.addHostObject("javaCallback", new Object() {
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });

        // Step 3: Write an async function that uses the asynchronous fetch API
        String asyncScript =
            "async function fetchData() {" +
            "  try {" +
            "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "    if (!response.ok) throw new Error('Network error');" +
            "    const json = await response.json();" +
            "    javaCallback.onResult(JSON.stringify(json));" +
            "  } catch (e) {" +
            "    javaCallback.onResult('Error: ' + e.message);" +
            "  }" +
            "}" +
            "fetchData();";

        // Step 4: Execute the script inside the document's JavaScript engine
        jsEngine.execute(asyncScript);
    }
}
```

**Förväntad konsoloutput**

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

Om du ser en felrad som börjar med `Error:` så har något gått fel – troligen ett nätverksavbrott.

---

## Visuell översikt

![Diagram som visar hur Java anropar JavaScript och tar emot async fetch-resultat – call java from javascript](/images/java-js-async.png)

*Bilden visar flödet: Java → JavaScriptEngine → async fetch → JavaCallback.*

---

## Vanliga frågor

**Kan jag använda detta tillvägagångssätt med andra JavaScript‑motorer?**  
Ja, vilken motor som helst som exponerar en host‑object‑mekanism (t.ex. Nashorn, GraalVM) kan fungera, men Aspose.HTML ger dig en fullständigt utrustad browser‑liknande miljö med inbyggd `fetch`.

**Vad händer om jag behöver returnera ett komplext Java‑objekt istället för en sträng?**  
Du kan serialisera objektet till JSON på Java‑sidan och låta JavaScript parsa det, eller så kan du exponera flera metoder på host‑objektet för att ta emot separata fält.

**Är `fetch`‑implementationen helt standard‑kompatibel?**  
Aspose.HTML implementerar WHATWG Fetch‑standarden, så du får korrekt hantering av omdirigeringar, CORS och streaming.

**Blockerar detta Java‑tråden medan nätverket väntar?**  
Nej. `execute`‑anropet returnerar omedelbart, och den interna motorn bearbetar promiset asynkront. Huvudtråden lever dock kvar tills skriptet är färdigt eller du explicit stänger ner motorn.

---

## Slutsats

Vi har just gått igenom ett praktiskt scenario som låter dig **anropa Java från JavaScript**, **run async JavaScript** och **fetch JSON i Java** med hjälp av **asynchronous fetch API**. Genom att skapa ett host‑objekt, skriva en snygg `async`‑funktion och exekvera den med Aspose.HTML:s **JavaScript engine** får du en ren, icke‑blockerande brygga mellan de två runtime‑miljöerna.

Ge det ett försök, ändra URL:en eller lägg till fler callbacks – din fantasi är gränsen. Nästa steg kan vara att utforska:

- **Executing JavaScript engine** med flera samtidiga skript.  
- Använda **run async javascript** för att bearbeta stora datamängder parallellt.  
- Integrera detta mönster i en webbtjänst som renderar dynamisk HTML i farten.

Känn dig fri att experimentera, och tveka inte att lämna en kommentar om du stöter på ett oväntat problem. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}