---
category: general
date: 2026-09-29
description: Ändra bakgrundsfärg med JavaScript i en HTML‑fil med Java. Lär dig att
  ladda HTML i Java, köra JS i HTML och modifiera HTML med Java för en ny sidbakgrund.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change background color javascript
- load html in java
- run js in html
- modify html with java
- set page background
language: sv
lastmod: 2026-09-29
og_description: Ändra bakgrundsfärg med JavaScript i en HTML‑sida med Java. Denna
  handledning visar hur du laddar HTML i Java, kör JS i HTML och sätter sidans bakgrund
  programatiskt.
og_image_alt: Screenshot of Java code that changes the page background color
og_title: Ändra bakgrundsfärg i JavaScript med Java – steg‑för‑steg guide
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Change background color javascript in an HTML file using Java. Learn
    to load html in java, run js in html, and modify html with java for a new page
    background.
  headline: How to change background color javascript using Java
  type: TechArticle
tags:
- Java
- HTMLUnit
- JavaScript
- HTML manipulation
title: Hur man ändrar bakgrundsfärgen i JavaScript med Java
url: /sv/java/editing-html-documents/how-to-change-background-color-javascript-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man ändrar bakgrundsfärg med JavaScript i Java

Om du behöver **change background color javascript** i en befintlig HTML‑fil kan du göra det helt från Java utan att öppna en webbläsare. Den här handledningen visar hur du **load html in java**, kör ett litet JavaScript‑snutt, och sedan **modify html with java** så att sidans bakgrund uppdateras.  

Lösningen fungerar med det öppna källkods‑biblioteket **HTMLUnit**, som tillhandahåller en huvudlös webbläsare som kan utvärdera JavaScript exakt som en riktig webbläsare skulle göra. I slutet av den här guiden har du en återanvändbar metod som **sets page background** till vilken färg du än väljer.

## Förutsättningar

| Vad du behöver | Varför det är viktigt |
|---------------|------------------------|
| Java 8 eller nyare | HTMLUnit kräver minst Java 8. |
| Maven eller Gradle byggverktyg | För att automatiskt hämta HTMLUnit‑beroendet. |
| En HTML‑fil du vill redigera (t.ex. `input.html`) | Källdokumentet som kommer att laddas och ändras. |

Lägg till HTMLUnit i ditt projekt:

*Maven*  

```xml
<dependency>
    <groupId>net.sourceforge.htmlunit</groupId>
    <artifactId>htmlunit</artifactId>
    <version>2.71.0</version>
</dependency>
```

*Gradle*  

```gradle
implementation 'net.sourceforge.htmlunit:htmlunit:2.71.0'
```

> **Pro tip:** Använd den senaste stabila versionen av HTMLUnit för att få den mest exakta JavaScript‑motorn.

## Ändra bakgrundsfärg med JavaScript – ladda HTML i Java

Det första steget är att ladda HTML‑dokumentet i ett `HTMLPage`‑objekt. Detta ger dig ett DOM‑liknande API och en JavaScript‑exekveringskontext.

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;

public class BackgroundColorChanger {

    /**
     * Loads an HTML file from the given path.
     *
     * @param htmlPath absolute or relative path to the source HTML file
     * @return HtmlPage representing the loaded document
     * @throws IOException if the file cannot be read
     */
    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        // WebClient acts as a headless browser; disabling CSS speeds up loading.
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);

        // Convert the file path to a URL that HTMLUnit can understand.
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }
}
```

*Varför detta är viktigt*: `WebClient` skapar en sandlådemiljö där JavaScript kan köras, så du kan **run js in html** exakt som en användares webbläsare skulle göra.

## Kör js i html för att sätta sidans bakgrund

När sidan är laddad kan du utvärdera vilket JavaScript‑uttryck som helst. Snutten nedan ändrar `backgroundColor`‑stilen på `<body>`‑elementet.

```java
/**
 * Executes JavaScript that changes the page background color.
 *
 * @param page   the HtmlPage loaded earlier
 * @param color  any valid CSS color string, e.g., "lightblue" or "#ffcc00"
 */
private static void changeBackground(HtmlPage page, String color) {
    // The eval method runs JavaScript in the page's context.
    String script = "document.body.style.backgroundColor = '" + color + "';";
    page.getEnclosingWindow().getScriptableObject().eval(script);
}
```

*Förklaring*:  
- `document.body.style.backgroundColor` är den standard‑DOM‑egenskapen för sidans bakgrund.  
- Genom att anropa `eval` **run js in html** utan att behöva ett riktigt webbläsarfönster.  
- Metoden är återanvändbar för vilken färg som helst, vilket uppfyller kravet **set page background**.

## Modifiera html med java och spara resultatet

Efter att skriptet har körts reflekterar DOM den nya stilen. Du kan nu skriva den uppdaterade HTML‑filen tillbaka till disk.

```java
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Saves the modified HTML content to a new file.
 *
 * @param page          the HtmlPage that has been altered
 * @param outputPath    destination file path
 * @throws IOException  if writing fails
 */
private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
    // page.asXml() returns the current HTML markup, including the changed style.
    String updatedHtml = page.asXml();
    Files.write(Paths.get(outputPath), updatedHtml.getBytes());
}
```

När allt sätts ihop får du ett enda körbart program:

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class BackgroundColorChanger {

    public static void main(String[] args) {
        // Adjust these paths for your environment.
        String inputFile = "YOUR_DIRECTORY/input.html";
        String outputFile = "YOUR_DIRECTORY/js_modified.html";
        String newColor = "lightblue"; // Change to any CSS color you need.

        try {
            HtmlPage page = loadHtml(inputFile);
            changeBackground(page, newColor);
            saveModifiedHtml(page, outputFile);
            System.out.println("Background color changed to '" + newColor + "' and saved to " + outputFile);
        } catch (IOException e) {
            System.err.println("Error processing HTML file: " + e.getMessage());
        }
    }

    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }

    private static void changeBackground(HtmlPage page, String color) {
        String script = "document.body.style.backgroundColor = '" + color + "';";
        page.getEnclosingWindow().getScriptableObject().eval(script);
    }

    private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
        String updatedHtml = page.asXml();
        Files.write(Paths.get(outputPath), updatedHtml.getBytes());
    }
}
```

### Förväntad output

När programmet körs skrivs:

```
Background color changed to 'lightblue' and saved to YOUR_DIRECTORY/js_modified.html
```

Att öppna `js_modified.html` i en webbläsare visar sidan med en ljusblå bakgrund, vilket bekräftar att operationen **change background color javascript** lyckades.

## Vanliga variationer och kantfall

| Situation | Hur man hanterar det |
|-----------|----------------------|
| **Olika färgformat** | Skicka vilket CSS‑kompatibelt värde som helst (`"red"`, `"#ff0000"`, `"rgb(255,0,0)"`). |
| **Saknad `<body>`‑tagg** | Skriptet kommer att misslyckas tyst; du kan först säkerställa att `<body>` finns med `page.getFirstByXPath("//body")`. |
| **Stora HTML‑filer** | Inaktivera CSS (`setCssEnabled(false)`) och aktivera endast de JavaScript‑funktioner du behöver för att minska minnesanvändningen. |
| **Köra flera skript** | Anropa `changeBackground` upprepade gånger eller skapa en verktygsmetod som accepterar en lista med JavaScript‑kommandon. |

## Slutsats

Du vet nu hur du **change background color javascript** genom att ladda en HTML‑fil i Java, **run js in html**, och **modify html with java** för att **set page background** till vilken färg du än väljer. Det kompletta exemplet ovan fungerar med det senaste HTMLUnit‑biblioteket och kan integreras i större automations‑pipelines, såsom batch‑bearbetning av HTML‑rapporter eller förberedelse av e‑postmallar.

**Nästa steg**  
- Utforska andra DOM‑manipulationer (t.ex. infoga element, ta bort skript).  
- Kombinera detta tillvägagångssätt med en PDF‑renderare för att generera PDF‑filer av de stylade sidorna.  
- Prova att använda en annan huvudlös motor som Selenium WebDriver om du behöver full webbläsarnoggrannhet.

Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Get Computed Style Java – Extract Background Color from HTML](/html/english/java/css-html-form-editing/get-computed-style-java-extract-background-color-from-html/)
- [How to Load HTML, Set Device DPI & Read Background Color](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Generate HTML from JavaScript in Java – Complete Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/generate-html-from-javascript-in-java-complete-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}