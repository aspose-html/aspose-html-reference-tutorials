---
category: general
date: 2026-02-11
description: Skapa HTML‑dokument i Java med Aspose.HTML. Lär dig hur du hämtar JSON‑JavaScript,
  lägger till script‑element, genererar HTML från JSON och konverterar JSON till pre.
draft: false
keywords:
- create html document
- fetch json javascript
- add script element
- generate html from json
- convert json to pre
language: sv
og_description: Skapa HTML‑dokument i Java med Aspose.HTML. Hämta JSON‑JavaScript,
  lägg till script‑element, generera HTML från JSON och konvertera JSON till pre—allt
  i en handledning.
og_title: Skapa HTML-dokument i Java – Fullständig guide
tags:
- Aspose.HTML
- Java
- Web Automation
title: Skapa HTML-dokument med Java – hämta JSON och generera innehåll
url: /sv/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa HTML-dokument – Fullständig Java‑handledning

Har du någonsin behövt **create HTML document** i farten men varit osäker på hur du hämtar fjärrdata till den? Du är inte ensam. I många projekt vill du hämta JSON med JavaScript, injicera resultatet i en sida och sedan spara den slutgiltiga markupen som en statisk fil. Den här guiden visar exakt hur du gör det med Aspose.HTML för Java.

Vi går igenom varje steg: från att skapa ett tomt dokument, till **fetch JSON JavaScript**, till **add script element**, och slutligen till **generate HTML from JSON** och **convert JSON to pre**‑taggar. I slutet har du en färdig `fetchResult.html` som innehåller den hämtade datan renderad som pretty‑printed JSON.

## Förutsättningar

- Java 17 eller nyare (koden kompileras även med JDK 11+)
- Aspose.HTML for Java‑biblioteket (tillgängligt via Maven Central)
- Grundläggande kunskap om HTML och async JavaScript
- En IDE eller vanlig `javac`/`java`‑kommandorad

Inga extra ramverk krävs—allt körs lokalt.

## Steg 1: Ställ in projektet och importera Aspose.HTML

Börja med att lägga till Aspose.HTML‑beroendet i din `pom.xml` (eller ladda ner JAR‑filen manuellt).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

> **Pro tip:** Håll versionsnumret uppdaterat; nyare releaser fixar buggar och förbättrar skriptmotorn.

## Steg 2: **Create HTML Document** – den tomma duken

Vi börjar med att skapa ett tomt `HTMLDocument`. Tänk på det som en ny sida där vi senare placerar vårt skript.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();
```

Varför behöver vi ett dokumentobjekt? Aspose.HTML:s `ScriptEngine` arbetar mot ett DOM, inte en rå sträng. Genom att bygga ett korrekt dokument ger vi motorn en riktig miljö för att köra vår **fetch JSON JavaScript**.

## Steg 3: Skriv JavaScript‑snutten – **Fetch JSON JavaScript** och **Convert JSON to pre**

Kärnan i handledningen finns i den här flerradiga strängen. Den utför en asynkron `fetch`, parsar JSON‑data och skriver sedan ett `<pre>`‑element med pretty‑printed data.

```java
        // Step 3: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;
```

Lägg märke till kommentaren *Convert JSON to <pre>* – det är exakt vad anropet `JSON.stringify(..., null, 2)` gör. Det lägger till indentering, vilket gör utskriften läsbar för människor.

## Steg 4: **Add Script Element** till dokumentet

Nu skapar vi ett `<script>`‑tagg, placerar vår kod inuti och bifogar det till body. Detta är delen **add script element**.

```java
        // Step 4: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);
```

Varför bifoga det till body? I en riktig webbläsare skulle skriptet köras så snart det har parsats. Genom att lägga till det i DOM efterliknar vi exakt detta beteende, vilket säkerställer att den asynkrona fetchen körs när vi senare anropar motorn.

## Steg 5: Kör Script Engine – låt den asynkrona fetchen slutföras

Aspose.HTML tillhandahåller en `ScriptEngine` som kan exekvera den DOM‑baserade JavaScript‑koden. Vi anropar `run()` och väntar på att promise‑kedjan ska slutföras.

```java
        // Step 5: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();
```

Motorn blockerar tills alla pågående uppgifter (vår fetch) är lösta, vilket garanterar att den genererade HTML‑en redan innehåller datan.

## Steg 6: **Generate HTML from JSON** – spara resultatet

Till sist sparar vi dokumentet till disk. Filen innehåller nu `<pre>`‑blocket med JSON‑payloaden.

```java
        // Step 6: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

När programmet körs produceras `fetchResult.html`. Öppna den i vilken webbläsare som helst så ser du något liknande:

```html
<pre>{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}</pre>
```

Det är resultatet **generate HTML from JSON** du letade efter.

## Fullständigt fungerande exempel

Nedan är den kompletta, körklara källfilen. Kopiera, klistra in, justera sökvägen för utdata och kör `java JsFetchExample`.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();

        // Step 2: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;

        // Step 3: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);

        // Step 4: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();

        // Step 5: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

## Förväntad output & verifiering

1. **Console:** Du kommer att se `HTML with fetched data saved.`  
2. **File (`fetchResult.html`):** När du öppnar den visas JSON‑innehållet i ett `<pre>`‑block, snyggt indenterat.  
3. **Validation:** Om du tittar på sidans källkod hittar du bara ett `<pre>`‑element—inga extra script‑taggar finns kvar eftersom motorn redan har exekverat dem.

## Vanliga frågor & edge‑cases

| Question | Answer |
|----------|--------|
| *Vad händer om API:et returnerar ett fel?* | Omge `fetch`‑anropet i ett `try…catch`‑block och skriv ett felmeddelande till body istället för JSON. |
| *Kan jag hämta flera resurser?* | Ja—kedja bara ytterligare `await fetch(...)`‑anrop eller använd `Promise.all`. Det slutgiltiga `innerHTML` kan concatenera flera `<pre>`‑block. |
| *Behöver jag sätta CORS‑rubriker?* | Eftersom skriptet körs i Aspose.HTML:s sandbox respekterar det samma‑origin‑policyn. Det offentliga JSONPlaceholder‑slutet tillåter redan cross‑origin‑förfrågningar. |
| *Hur ändrar jag utmatningskatalogen vid körning?* | Skicka sökvägen som ett kommandoradsargument (`args[0]`) och ersätt den hårdkodade strängen i `htmlDoc.save`. |
| *Finns det ett sätt att bädda in CSS för styling?* | Absolut. Skapa ett `<style>`‑element, sätt dess `textContent` till din CSS och lägg till det i `<head>` innan du kör motorn. |

## Tips för produktionsanvändning

- **Cache the JSON** om endpointen är långsam; du kan skriva den hämtade strängen till en fil och återanvända den.  
- **Sanitize the data** innan du injicerar den, särskilt om källan inte är betrodd. Använd `JSON.stringify` på ett säkert sätt eller escapea HTML‑entiteter.  
- **Configure the ScriptEngine timeout** (`scriptEngine.setTimeout(5000)`) för att undvika att hänga på oresponsiva tjänster.

## Visuell sammanfattning

![exempel på skapa html-dokument som visar den genererade HTML med JSON inuti ett pre‑tagg](fetchResult.png "Skärmdump av det genererade HTML‑dokumentet")

*Alt text:* *exempel på skapa html-dokument – genererad HTML‑fil som visar hämtad JSON inuti ett pre‑element.*

## Slutsats

Du vet nu hur du **create HTML document** programatiskt i Java, **fetch JSON JavaScript**, **add script element**, **generate HTML from JSON** och **convert JSON to pre** för läsbar output. Hela arbetsflödet körs offline, kräver bara Aspose.HTML och producerar en ren statisk fil som du kan servera var som helst.

Nästa steg är att utöka skriptet för att loopa över en array av objekt, lägga till CSS‑styling eller skriva flera sidor med samma teknik. Du kan också ersätta `fetch`‑URL:en med ditt eget API för att omvandla dynamisk data till statiska snapshots—perfekt för SEO‑vänlig pre‑rendering.

Lycka till med kodandet, och dela gärna dina experiment i kommentarerna!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}