---
category: general
date: 2026-09-29
description: Ställ in en anpassad användaragent i Aspose.HTML för Java och lär dig
  hur du anger virtuell skärmstorlek för korrekt HTML-rendering.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: sv
lastmod: 2026-09-29
og_description: Ställ in en anpassad användaragent i Aspose.HTML för Java och lär
  dig hur du ställer in virtuell skärmstorlek för exakt HTML-rendering.
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: Ställ in anpassad användaragent och skärmdimensioner i Aspose.HTML för Java
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: Ställ in anpassad användaragent och skärmdimensioner i Aspose.HTML för Java
url: /sv/java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ange anpassad användaragent och skärmstorlekar i Aspose.HTML för Java

Om du behöver **set custom user agent** medan du renderar HTML med Aspose.HTML för Java, visar den här guiden exakt hur du gör det. Genom att konfigurera en sandbox får du också möjlighet att **set virtual screen size**, vilket säkerställer att layouten matchar en riktig webbläsarvy.

Du avslutar den här handledningen med ett komplett, körbart program som **specifies user agent**, **sets screen width**, och **sets screen height**. Inga externa verktyg krävs—bara Aspose.HTML för Java och en Java 8+ runtime.

## Vad du kommer att lära dig

* Hur man skapar en `SandboxConfiguration` för att isolera rendering.
* Hur man **set custom user agent** och varför det är viktigt för responsiva sidor.
* Hur man **set virtual screen size** (skärmbredd och -höjd) för en exakt layout.
* Hur man laddar en HTML‑fil i sandboxen och sparar det bearbetade resultatet.
* Vanliga fallgropar och bästa‑praxis‑tips för sandbox‑rendering.

> **Förutsättningar** – Du behöver en giltig Aspose.HTML för Java‑licens, Java 8 eller nyare, och en IDE (IntelliJ IDEA, Eclipse eller VS Code). Exemplet använder en lokal `input.html`‑fil, men vilken åtkomlig URL som helst fungerar.

![Sandbox-flödesdiagram](sandbox-flow.png "exempel på anpassad användaragent i Java")

## Steg 1: Skapa en sandbox‑konfiguration (grunden)

Sandboxen isolerar renderingsmiljön från värd‑JVM:n, vilket är avgörande när du vill **set custom user agent** eller ändra viewport‑storleken.

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*Varför detta steg?*  
`SandboxConfiguration` innehåller alla renderingsalternativ, inklusive **screen dimensions** och **user‑agent**‑strängar. Genom att konfigurera den innan dokumentet laddas garanterar du att HTML‑motorn respekterar dessa inställningar redan från den första begäran.

## Steg 2: Ange skärmstorlekar för att efterlikna en riktig enhet

Responsiva webbplatser läser ofta `window.innerWidth` och `window.innerHeight`. För att få motorn att tro att den körs på en 1024 × 768‑skärm, **set virtual screen size**:

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*Varför detta är viktigt* – Om du utelämnar **set screen dimensions**, kan renderaren defaulta till en liten viewport, vilket får CSS‑media‑queries att välja mobil‑layouten. Genom att explicit **set screen width** och **set screen height**, styr du vilka CSS‑regler som tillämpas.

## Steg 3: Ange en anpassad user‑agent‑sträng

Vissa webbsidor levererar olika innehåll baserat på user‑agent‑headern. För att **specify user agent** sätter du helt enkelt den på sandbox‑konfigurationen:

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*Varför använda en anpassad user agent?*  
En anpassad sträng kan kringgå bot‑detektering, aktivera endast‑desktop‑funktioner, eller testa hur en webbplats beter sig för en specifik webbläsarversion. Aspose‑motorn vidarebefordrar detta värde med varje HTTP‑begäran som görs vid inläsning av externa resurser (CSS, bilder, skript).

## Steg 4: Ladda HTML‑dokumentet i sandboxen

Nu när sandboxen är fullt konfigurerad, ladda HTML‑filen. Konstruktorn som tar en filsökväg och en `SandboxConfiguration` tillämpar automatiskt alla inställningar vi definierat.

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

Om du behöver ladda från en fjärr‑URL, ersätt filsökvägen med URL‑strängen—Aspose.HTML kommer fortfarande att respektera **set custom user agent** och **screen dimensions**.

## Steg 5: Spara det bearbetade resultatet

När dokumentet har lästs in kan du spara det i vilket stödformat som helst. Här skriver vi en sandbox‑HTML‑fil som återspeglar eventuella DOM‑ändringar som orsakats av de anpassade inställningarna.

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

Den sparade filen kommer att innehålla samma markup, men alla skript som frågade `navigator.userAgent` eller inspekterade `window.innerWidth` kommer nu att se de värden du angav.

## Fullständigt, körbart exempel

Genom att sätta ihop alla steg får du ett självständigt program som du kan kopiera, klistra in och köra.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### Förväntat resultat

När programmet körs skapas `sandboxed_output.html`. Om du öppnar den i en webbläsare och inspekterar `navigator.userAgent` via konsolen, kommer du att se **AsposeHTML/1.0**. På samma sätt kommer `window.innerWidth` att rapportera **1024**, vilket bekräftar att **set screen dimensions** fungerade som avsett.

## Vanliga frågor & hantering av edge‑case

| Question | Answer |
|----------|--------|
| **Vad händer om sidan laddar ytterligare resurser från en annan domän?** | Sandboxen vidarebefordrar den **custom user agent** med varje begäran, men cross‑origin‑policyer gäller fortfarande. Använd `sandboxConfig.setAllowCrossDomain(true)` om du behöver lätta på dessa restriktioner. |
| **Kan jag ändra skärmstorleken efter att dokumentet har laddats?** | Nej. Skärmstorlekar läses under det initiala layout‑steget. För att rendera med en annan storlek, skapa en ny `SandboxConfiguration` och ladda om dokumentet. |
| **Behöver jag anropa `document.close()`?** | `HTMLDocument` implementerar `AutoCloseable`. Att använda ett try‑with‑resources‑block säkerställer korrekt städning, men explicit `close()` är valfritt i enkla skript. |
| **Hur skiljer detta sig från att sätta en user‑agent i en HTTP‑klient?** | Att sätta user‑agent på sandboxen påverkar **alla** resursförfrågningar som görs av HTML‑motorn, inte bara den initiala HTML‑hämtningen. Detta efterliknar en riktig webbläsare närmare. |
| **Är sandboxen säker för opålitlig HTML?** | Ja. Sandboxen isolerar filsystemstillgång och begränsar nätverksanrop enligt konfigurationen, vilket minskar risken för att skadliga skript påverkar din värd‑JVM. |

## Pro‑tips

* **Återanvänd konfigurationer** – Om du renderar många sidor med samma viewport, skapa en enda `SandboxConfiguration` och återanvänd den för att undvika overhead för objekt‑skapande.
* **Felsök med loggning** – Aktivera Aspose.HTML‑loggning (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`) för att se vilka resurser som hämtades med den custom user‑agent.
* **Kombinera med CSS‑media‑queries** – Genom att justera **set screen width** kan du testa hur din responsiva design beter sig på surfplattor, telefoner eller stora skrivbord utan att öppna en riktig webbläsare.

## Slutsats

Du vet nu hur du **set custom user agent** och **set screen dimensions** när du renderar HTML med Aspose.HTML för Java. Genom att konfigurera en sandbox isolerar du miljön, kontrollerar viewporten och säkerställer att externa resurser ser exakt de headers du anger. Denna teknik är avgörande för att testa responsiva layouter, kringgå bot‑blockeringar eller reproducera endast‑desktop‑funktioner i automatiserade pipelines.

Nästa steg kan vara att utforska **how to set custom cookies** eller **capture rendered screenshots** med Aspose.HTML:s renderings‑API—båda koncepten bygger på samma sandbox‑konfigurationsmönster som du just har lärt dig.

Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [High DPI-rendering i Java – Fånga webbsideskärmbilder med anpassad användaragent](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [Hur man laddar HTML, sätter enhetens DPI & läser bakgrundsfärg](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Skapa HTML‑fil i Java & konfigurera nätverkstjänst (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}