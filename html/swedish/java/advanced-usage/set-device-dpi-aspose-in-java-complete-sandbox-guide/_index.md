---
category: general
date: 2026-06-16
description: Lär dig hur du ställer in enhetens DPI i Aspose och sätter viewportens
  bredd och höjd när du renderar HTML med Aspose.HTML‑sandlådan i Java. Steg‑för‑steg‑kod
  inkluderad.
draft: false
keywords:
- set device dpi aspose
- set viewport width height
language: sv
og_description: Upptäck hur du ställer in enhetens DPI i Aspose och anger viewportens
  bredd och höjd med Aspose.HTML sandbox för Java. Fullständig kod och förklaring.
og_title: Ställ in enhetens DPI i Aspose med Java – Komplett Sandbox-guide
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to set device dpi aspose and set viewport width height when
    rendering HTML with Aspose.HTML sandbox in Java. Step‑by‑step code included.
  headline: set device dpi aspose in Java – Complete Sandbox Guide
  type: TechArticle
- description: Learn how to set device dpi aspose and set viewport width height when
    rendering HTML with Aspose.HTML sandbox in Java. Step‑by‑step code included.
  name: set device dpi aspose in Java – Complete Sandbox Guide
  steps:
  - name: Configure sandbox options (including DPI and viewport size).
    text: Configure sandbox options (including DPI and viewport size).
  - name: Instantiate a `DocumentSandbox` with those options.
    text: Instantiate a `DocumentSandbox` with those options.
  - name: Load an external HTML page inside the sandbox.
    text: Load an external HTML page inside the sandbox.
  - name: Perform a simple DOM operation—printing the page title.
    text: Perform a simple DOM operation—printing the page title.
  type: HowTo
tags:
- Aspose.HTML
- Java
- HTML rendering
- Sandbox
title: Ställ in enhetens DPI i Aspose med Java – Komplett Sandbox‑guide
url: /sv/java/advanced-usage/set-device-dpi-aspose-in-java-complete-sandbox-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# set device dpi aspose – Java Sandbox‑handledning

Har du någonsin undrat hur man **set device dpi aspose** när man renderar en webbsida i Java? Du är inte ensam. Många utvecklare stöter på problem när de behöver att den renderade sidan ser exakt ut som den skulle på en riktig skärm—särskilt när DPI är viktigt för layoutberäkningar.

I den här guiden går vi igenom ett praktiskt exempel som inte bara **set device dpi aspose**, utan också visar hur du **set viewport width height** så att sidan beter sig precis som i ett webbläsarfönster på 1280 × 800 pixlar. I slutet har du ett körbart kodexempel, en tydlig förklaring av varje steg och tips för att undvika vanliga fallgropar.

## Vad den här handledningen täcker

Vi börjar med att lista förutsättningarna och går sedan igenom fyra koncisa steg:

1. Konfigurera sandbox‑alternativ (inklusive DPI och viewport‑storlek).  
2. Skapa en `DocumentSandbox` med de alternativen.  
3. Ladda en extern HTML‑sida i sandboxen.  
4. Utför en enkel DOM‑operation—skriv ut sidans titel.

Du får se varför varje del är viktig, hur du justerar inställningarna för olika enheter och hur resultatet bör se ut. Ingen extern dokumentation behövs; allt du behöver finns här.

## Förutsättningar

- Java 8 eller nyare (Aspose.HTML för Java‑biblioteket stödjer JDK 8+).  
- Aspose.HTML för Java‑JAR‑filer lagda till i ditt projekts classpath.  
- En IDE eller byggverktyg (Maven/Gradle) för att kompilera och köra koden.  
- Internetåtkomst om du planerar att ladda en levande URL som `https://example.com`.

Om du har markerat alla rutor, låt oss börja.

## Steg 1: Set device DPI aspose – Definiera sandbox‑alternativ

Det första du måste göra är att berätta för sandboxen vilken “skärm” du låtsas ha. Det är här **set device dpi aspose** kommer in i bilden. DPI (dots per inch) påverkar hur CSS‑enheten `px` tolkas, vilket kan förändra teckenstorlekar, bildskalning och media queries.

```java
// Step 1: Create sandbox options and configure DPI and viewport.
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setDeviceDpi(96);               // set device dpi aspose
sandboxOptions.setViewportWidth(1280);         // set viewport width height
sandboxOptions.setViewportHeight(800);         // set viewport width height
```

> **Varför detta är viktigt:**  
> *Anropet `setDeviceDpi` talar om för Aspose.HTML att behandla en CSS‑pixel som 1/96 tum, vilket motsvarar de flesta skrivbordsmonitorer. Hoppar du över detta kan layouten bli för liten eller för stor på hög‑DPI‑skärmar.*

## Steg 2: Skapa sandboxen med de konfigurerade alternativen

Nu när alternativen är klara behöver du en sandbox‑instans som respekterar dem. Tänk på sandboxen som en liten, isolerad webbläsarmotor som inte rör ditt filsystem.

```java
// Step 2: Initialise the DocumentSandbox using the options above.
DocumentSandbox documentSandbox = new DocumentSandbox(sandboxOptions);
```

> **Proffstips:**  
> Att återanvända samma `DocumentSandbox` för flera sidor sparar minne, men kom ihåg att återställa alternativen om du behöver en annan DPI eller viewport senare.

## Steg 3: Ladda ett HTML‑dokument i sandboxen

Med sandboxen på plats är det enkelt att ladda en sida. Konstruktorn för `HTMLDocument` accepterar URL:en och sandboxen du just skapade.

```java
// Step 3: Load a remote HTML page using the sandbox.
HTMLDocument htmlDoc = new HTMLDocument("https://example.com", documentSandbox);
```

> **Edge case:**  
> Om målwebbplatsen blockerar automatiska förfrågningar kan du få ett 403‑fel. I så fall kan du antingen ladda ner HTML‑filen lokalt och läsa in den från en filsökväg, eller sätta en anpassad user‑agent‑sträng via `sandboxOptions`.

## Steg 4: Utför vanliga DOM‑operationer – Skriv ut sidans titel

På den här punkten är sidan fullständigt renderad i sandboxen, så alla DOM‑frågor fungerar exakt som i en fullfjädrad webbläsare. Vi håller det enkelt och hämtar titeln.

```java
// Step 4: Access the DOM – print the page title.
System.out.println("Title: " + htmlDoc.getTitle());
```

**Förväntad output**

```
Title: Example Domain
```

Om du ser något annat, dubbelkolla att URL:en är nåbar och att du inte av misstag ändrat DPI‑ eller viewport‑värdena.

## Varför inställning av viewport width height är avgörande

Du kanske undrar: “Varför **set viewport width height** alls?” Svaret ligger i responsiv design. Media queries som `@media (max-width: 600px)` reagerar på viewport‑dimensionerna, inte den fysiska skärmstorleken. Genom att specificera `1280` × `800` garanterar du att sidan renderas med “desktop”‑layouten, även om du kör koden på en huvudlös server utan display.

```java
sandboxOptions.setViewportWidth(1280);   // set viewport width height
sandboxOptions.setViewportHeight(800);   // set viewport width height
```

Att ändra dessa siffror låter dig simulera surfplattor, telefoner eller till och med ultrabreda monitorer utan att lämna din IDE.

## Fullt fungerande exempel

Nedan hittar du den kompletta, körklara Java‑klassen som binder ihop allt. Kopiera och klistra in den i en fil som heter `SandboxExample.java`, lägg till Aspose.HTML‑JAR‑filerna i classpath och kör `javac SandboxExample.java && java SandboxExample`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.sandbox.SandboxOptions;

public class SandboxExample {
    public static void main(String[] args) {
        // Step 1: Define sandbox options – set device DPI and viewport.
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setDeviceDpi(96);               // set device dpi aspose
        sandboxOptions.setViewportWidth(1280);         // set viewport width height
        sandboxOptions.setViewportHeight(800);         // set viewport width height

        // Step 2: Create a DocumentSandbox using the defined options.
        DocumentSandbox documentSandbox = new DocumentSandbox(sandboxOptions);

        // Step 3: Load an HTML document inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com", documentSandbox);

        // Step 4: Perform normal DOM operations – print the page title.
        System.out.println("Title: " + htmlDoc.getTitle());
    }
}
```

> **Snabb verifiering:**  
> Kör programmet. Om du ser `Title: Example Domain` är allt korrekt konfigurerat. Om inte, inspektera konsolen för undantag—de flesta problem beror på saknade JAR‑filer eller nätverksrestriktioner.

## Vanliga fallgropar & hur du undviker dem

| Symptom | Trolig orsak | Åtgärd |
|---|---|---|
| `NullPointerException` på `htmlDoc.getTitle()` | Sandboxen misslyckades med att ladda sidan | Verifiera URL:en, lägg till ett try‑catch runt `HTMLDocument`‑konstruktorn, eller aktivera loggning via `sandboxOptions.setLogLevel(...)`. |
| Layouten ser inzoomad/utzoomad ut | DPI är inte korrekt inställd | Säkerställ `sandboxOptions.setDeviceDpi(96)` (eller din mål‑DPI). |
| Media queries triggas aldrig | Viewport-dimensioner saknas | Dubbelkolla att du anropade både `setViewportWidth` **och** `setViewportHeight`. |
| Out‑of‑memory‑fel på stora sidor | Återanvända en enda sandbox för många tunga sidor | Skapa en ny `DocumentSandbox` per sida eller anropa `documentSandbox.dispose()` efter användning. |

## Utöka exemplet

Nu när du vet hur du **set device dpi aspose** och **set viewport width height**, kan du experimentera vidare:

- **Fånga en skärmdump** av den renderade sidan med `htmlDoc.renderToBitmap(...)`.  
- **Injecta anpassad CSS** före rendering för att testa mörkt läge.  
- **Kör JavaScript** i sandboxen med `htmlDoc.getWindow().eval(...)`.  

Alla dessa åtgärder respekterar den DPI och viewport du konfigurerat, vilket ger dig en pålitlig testmiljö för responsiva layouter.

## Slutsats

Vi har just gått igenom en kort, end‑to‑end‑lösning som visar hur man **set device dpi aspose** och **set viewport width height** med Aspose.HTML:s sandbox i Java. Du har nu en stabil grund för att rendera sidor exakt som de skulle visas på vilken enhet som helst, allt från en säker, isolerad miljö.

Redo för nästa steg? Prova att rendera en sida som använder CSS‑grid‑layout, eller hämta ett externt stylesheet och se hur DPI påverkar teckensnittsrenderingen. Sandboxen ger dig friheten att experimentera utan att påverka ditt värdsystem.

Om du stöter på problem, lämna en kommentar nedan eller kolla Aspose.HTML för Java‑dokumentationen—allt du behöver finns redan här. Lycka till med kodandet!  

![set device dpi aspose sandbox-diagram](https://example.com/images/set-device-dpi-aspose.png "Diagram som visar DPI- och viewport‑konfiguration i Aspose.HTML sandbox")

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Skapa PDF från HTML med Aspose.HTML för Java – Sandbox](/html/english/java/configuring-environment/implement-sandboxing/)
- [Skapa PDF från HTML – Ställ in användar‑stilmall i Aspose.HTML för Java](/html/english/java/configuring-environment/set-user-style-sheet/)
- [Hur man ställer in teckenkodning i Aspose.HTML för Java](/html/english/java/configuring-environment/set-character-set/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}