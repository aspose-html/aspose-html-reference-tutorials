---
category: general
date: 2026-02-22
description: Ställ in enhetens pixelratio i Java med Aspose.HTML sandbox. Lär dig
  hur du ställer in en anpassad user agent, hämtar sidans titel i Java och konverterar
  HTML till PNG i en handledning.
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- save html as image
- convert html to png
- get page title java
language: sv
og_description: Ställ in enhetens pixelförhållande i Java med Aspose.HTML sandbox.
  Denna handledning visar hur man ställer in en anpassad användaragent, hämtar sidtitel
  i Java och konverterar HTML till PNG.
og_title: Ställ in enhetens pixelförhållande i Java – Komplett guide
tags:
- Aspose.HTML
- Java
- Web Rendering
title: Ställ in enhetens pixelförhållande i Java – Komplett guide
url: /sv/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ställ in enhetens pixelförhållande i Java – Komplett guide

Har du någonsin undrat hur man **set device pixel ratio** när man renderar en webbsida från Java? Du är inte ensam. Många utvecklare behöver emulera hög‑DPI‑mobilskärmar så att skärmbilder blir skarpa, särskilt när de senare **save html as image** för rapporter eller marknadsföringsmaterial. I den här handledningen går vi igenom ett praktiskt exempel som gör exakt det—samt visar hur du **set custom user agent**, **get page title java**, och **convert html to png** med Aspose.HTML.

Vi börjar med en kort översikt av sandbox‑API:et, går sedan igenom varje konfigurationssteg och slutligen skapar en PNG‑fil som speglar en riktig iPhone‑display. När du är klar har du ett återanvändbart kodsnutt som du kan lägga in i vilket Java‑projekt som helst. Inga externa verktyg behövs, bara ren Java och Aspose.HTML 7.x (eller nyare).

---

## Förutsättningar

- Java 17 eller senare (koden kompileras med tidigare versioner men 17 rekommenderas).
- Aspose.HTML för Java‑biblioteket (ladda ner från den officiella Aspose‑sidan; Maven‑koordinater: `com.aspose:aspose-html:23.10`).
- En IDE eller textredigerare du föredrar (IntelliJ IDEA, VS Code, Eclipse… alla fungerar).
- Internetåtkomst för demo‑URL:en (`https://example.com/responsive.html`), eller ersätt den med någon offentlig HTML‑sida du äger.

> **Pro tip:** Om du sitter bakom en proxy, konfigurera JVM:s `http.proxyHost` och `http.proxyPort` systemegenskaper innan du kör koden.

---

## Steg 1: Ställ in enhetens pixelförhållande och andra sandbox‑alternativ

Det första vi behöver är en **SandboxOptions**‑instans där vi definierar den virtuella skärmstorleken och *device pixel ratio* (DPR). Tänk på DPR som faktorn som talar om för webbläsaren hur många fysiska pixlar som motsvarar en CSS‑pixel. På en Retina‑iPhone är DPR vanligtvis **2.0**, vilket är varför vi använder det värdet.

```java
// Step 1: Create and configure SandboxOptions
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS width of an iPhone X
sandboxOptions.setScreenHeight(667);         // CSS height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
```

> **Varför detta är viktigt:** Utan att sätta rätt DPR kommer den renderade bilden att se suddig eller för stor ut eftersom rasteriseraren antar en 1:1‑pixelmappning.

---

## Steg 2: Ställ in anpassad User Agent

Webbplatser levererar ofta olika markup baserat på **User‑Agent**‑headern. För att säkerställa att vår sida beter sig som på en riktig iPhone injicerar vi en anpassad sträng som efterliknar Safari på iOS.

```java
// Step 2: Define a mobile‑specific user agent
String iphoneUA = "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                  "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                  "Version/14.0 Mobile/15E148 Safari/604.1";

sandboxOptions.setUserAgent(iphoneUA);   // <-- set custom user agent
```

> **Edge case:** Vissa webbplatser inspekterar även `Accept-Language`‑headern. Om du märker att översättningar saknas, lägg till `sandboxOptions.setAcceptLanguage("en-US,en;q=0.9");`.

---

## Steg 3: Ladda sidan i sandboxen och hämta titeln

Nu startar vi sandboxen med de alternativ vi just definierade. **Sandbox**‑objektet isolerar renderingsprocessen och säkerställer att våra DPR‑ och user‑agent‑inställningar respekteras.

```java
// Step 3: Create the sandbox and load the HTML document
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
HTMLDocument htmlDoc = new HTMLDocument(
        "https://example.com/responsive.html", mobileSandbox);
```

När sidan har laddats är det lika enkelt som att anropa `getTitle()` för att hämta titeln. Detta uppfyller kravet **get page title java**.

```java
// Step 3b: Print the page title to the console
System.out.println("Title: " + htmlDoc.getTitle());   // <-- get page title java
```

**Förväntad konsolutskrift**

```
Title: Responsive Demo – Mobile View
```

Om titeln är tom, dubbelkolla URL:en eller se till att sidan inte blockeras av CORS‑policyer.

---

## Steg 4: Konvertera HTML till PNG och spara HTML som bild

Aspose.HTML låter dig rendera DOM‑en direkt till en bildfil. Eftersom vi redan har satt DPR till 2.0 kommer den resulterande PNG‑filen att ha dubbel pixeldensitet, vilket ger en skarp skärmbild.

```java
// Step 4: Render and save as PNG (convert html to png)
htmlDoc.save("mobile_view.png");   // <-- save html as image
```

`save`‑metoden upptäcker automatiskt filändelsen och väljer rätt renderare. Om du behöver ett annat format (JPEG, BMP) ändrar du bara filnamnet därefter.

> **Vad händer om du behöver en specifik bildstorlek?**  
> Använd `ImageSaveOptions` för att styra bredd, höjd och bakgrundsfärg:

```java
ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
pngOptions.setWidth(750);   // 375 CSS px * DPR 2
pngOptions.setHeight(1334);
htmlDoc.save("mobile_view_custom.png", pngOptions);
```

---

## Fullt fungerande exempel

Nedan är det kompletta, färdiga programmet som binder ihop alla stegen. Kopiera och klistra in det i en `SandboxDemo.java`‑fil, lägg till Aspose.HTML‑beroendet och kör `java SandboxDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.rendering.image.ImageSaveOptions;
import com.aspose.html.rendering.image.SaveFormat;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Configure sandbox – set device pixel ratio, screen size, and user agent
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS width (iPhone)
        sandboxOptions.setScreenHeight(667);         // CSS height
        sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                "Version/14.0 Mobile/15E148 Safari/604.1");   // <-- set custom user agent

        // 2️⃣ Create sandbox instance
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // 3️⃣ Load the target page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox);

        // 4️⃣ Retrieve and print the page title (get page title java)
        System.out.println("Title: " + htmlDoc.getTitle());

        // 5️⃣ Render the page – convert html to png and save html as image
        // Simple save (auto‑detect PNG)
        htmlDoc.save("mobile_view.png");   // <-- save html as image

        // 6️⃣ Optional: custom size rendering
        ImageSaveOptions opts = new ImageSaveOptions(SaveFormat.PNG);
        opts.setWidth(750);   // 375 * DPR 2
        opts.setHeight(1334);
        htmlDoc.save("mobile_view_custom.png", opts); // another convert html to png example
    }
}
```

När programmet körs skapas två PNG‑filer:

| Fil | Beskrivning |
|------|-------------|
| `mobile_view.png` | Standardrendering med den konfigurerade DPR:n. |
| `mobile_view_custom.png` | Rendering med explicit bredd/höjd (användbart för fasta tillgångar). |

Du kan öppna någon av filerna i vilken bildvisare som helst för att verifiera den högupplösta utskriften.

---

## Vanliga frågor & edge‑cases

| Fråga | Svar |
|----------|--------|
| **Vad händer om sidan innehåller JavaScript som modifierar DOM efter laddning?** | Aspose.HTML kör skript som standard. Om du behöver en statisk ögonblicksbild innan skript körs, sätt `sandboxOptions.setEnableJavaScript(false)`. |
| **Kan jag rendera en sida som kräver autentisering?** | Ja. Använd `sandboxOptions.setCredentials(new NetworkCredential("user","pass"))` eller injicera cookies via `sandboxOptions.getCookies().add(...)`. |
| **Är DPR begränsad till 2.0?** | Nej. Du kan sätta vilket positivt double‑värde som helst (t.ex. 3.0 för ultra‑höga DPI‑enheter). Kom bara ihåg att högre DPR innebär större bildfiler. |
| **Hur hanterar jag sidor med stora resurser (bilder, typsnitt)?** | Öka sandboxens minnesgräns med `sandboxOptions.setMemoryLimit(512 * 1024 * 1024)` (bytes). Detta förhindrar out‑of‑memory‑fel på tunga sidor. |
| **Behöver jag stänga sandboxen manuellt?** | `Sandbox` implementerar `AutoCloseable`. Omge den i ett try‑with‑resources‑block för automatisk städning. |

---

## Slutsats

Vi har visat hur man **set device pixel ratio** i en Java‑sandbox, **set custom user agent**, **get page title java**, och **convert html to png** (effektivt **save html as image**) med Aspose.HTML. Det kompletta exemplet demonstrerar ett praktiskt arbetsflöde som du kan anpassa för automatiserad skärmbildsgenerering, visuell regressions‑testning eller vilket scenario som helst där en pixel‑perfekt representation av en webbsida krävs.

Känn dig fri att experimentera—ändra DPR till 3.0, byt user‑agent mot en Android‑sträng, eller peka URL:en mot en lokal HTML‑fil. Samma mönster fungerar för PDF‑filer, SVG‑filer eller till och med flersidiga renderingar.

Om du fann den här guiden hjälpsam, överväg att utforska relaterade ämnen som **PDF generation with Aspose.HTML**, **headless Chrome alternatives**, eller **batch rendering of multiple URLs**. Lycka till med kodandet, och må dina skärmbilder alltid vara knivskarpa! 

![ställ in enhetens pixelförhållande i Java sandbox](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}