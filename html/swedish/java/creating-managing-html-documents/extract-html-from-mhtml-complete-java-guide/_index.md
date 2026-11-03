---
category: general
date: 2026-04-19
description: Extrahera HTML från MHTML snabbt med Java. Lär dig hur du konverterar
  MHTML till HTML, extraherar e‑postkroppen, skriver en sträng till fil och hanterar
  MHT‑konvertering.
draft: false
keywords:
- extract html from mhtml
- convert mhtml to html
- extract email body
- write string to file
- convert mht to html
language: sv
og_description: Extrahera HTML från MHTML i Java. Denna guide visar hur man konverterar
  MHTML till HTML, extraherar e‑postmeddelandets kropp och skriver strängen till en
  fil.
og_title: Extrahera HTML från MHTML – Java steg för steg
tags:
- Java
- Aspose.HTML
- Email Processing
title: Extrahera HTML från MHTML – Komplett Java‑guide
url: /sv/java/creating-managing-html-documents/extract-html-from-mhtml-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera HTML från MHTML – Komplett Java‑guide

Har du någonsin behövt **extrahera HTML från MHTML** men varit osäker på var du ska börja? Kanske har du fått ett arkiverat e‑postmeddelande (`.mht`) och vill ha den rena kroppen för en webb‑förhandsgranskning, eller så bygger du ett migrationsskript som omvandlar äldre arkiv till moderna HTML‑sidor. I båda fallen är problemet detsamma: du har ett en‑fil‑webbarkiv och du behöver den råa HTML‑markupen från det.

Den goda nyheten? Med några rader Java och Aspose.HTML‑biblioteket kan du **konvertera MHTML till HTML**, hämta e‑postkroppen och till och med skriva den strängen till en fil – allt utan att lämna din IDE. I den här handledningen går vi igenom hela processen, förklarar varför varje steg är viktigt och visar hur du hanterar vanliga kantfall som saknade resurser eller icke‑UTF‑8‑kodningar.

> **Snabb sammanfattning:** I slutet av den här guiden kommer du att kunna **extrahera e‑postkropp**, **konvertera MHTML till HTML** och **skriva sträng till fil** med ett rent, återanvändbart kodexempel som fungerar för alla `.mht` eller `.mhtml` du kastar på det.

---

## Vad du behöver

- **Java 17+** (koden använder try‑with‑resources‑mönstret, som finns sedan Java 7, men Java 17 är den nuvarande LTS‑versionen).
- **Aspose.HTML for Java** JARs on your classpath. You can grab them from the [Aspose website](https://products.aspose.com/html/java/) or via Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- En exempel **`.mht` eller `.mhtml`**‑fil som du vill bearbeta. För demonstrationen kallar vi den `email.mht` och placerar den i `YOUR_DIRECTORY`.

Det är allt – inga extra ramverk, inga tunga parserar. Bara ren Java och ett enda, väl‑dokumenterat bibliotek.

## Steg 1 – Öppna MHTML‑filen som en ström

Det första vi gör är att öppna det arkiverade e‑postmeddelandet som en `InputStream`. Att använda en ström håller minnesanvändningen låg, särskilt för stora `.mht`‑filer som kan innehålla inbäddade bilder eller CSS.

```java
// Step 1: Open the MHTML file as a stream
try (InputStream mhtmlStream = new FileInputStream("YOUR_DIRECTORY/email.mht")) {
    // Subsequent steps go inside this block
}
```

**Varför en ström?**  
En ström låter `MhtmlDocument` läsa data i farten, vilket betyder att du inte får `OutOfMemoryError` även om arkivet är flera megabyte. Den ger dig också flexibiliteten att läsa från andra källor senare (t.ex. en `ByteArrayInputStream` från en databas).

## Steg 2 – Läs in MHTML‑dokumentet från strömmen

Nu överlämnar vi strömmen till Asposes `MhtmlDocument`‑klass. Denna klass parsar det MIME‑kodade arkivet och bygger en DOM‑liknande representation av den inbäddade HTML‑koden.

```java
// Step 2: Load the MHTML document from the stream
MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);
```

**Bakom kulisserna:**  
Aspose extraherar varje MIME‑del (HTML, bilder, CSS) och sätter ihop dem internt. Därför kan du senare begära bara HTML‑delen utan att behöva oroa dig för de inbäddade resurserna.

## Steg 3 – Hämta huvud‑HTML‑innehållet

När dokumentet är laddat är hämtning av den råa HTML‑koden en enradare. Metoden `getHtmlContent()` returnerar kroppen som en `String`, och bevarar den ursprungliga markupen.

```java
// Step 3: Retrieve the main HTML content as a string
String htmlContent = mhtmlDoc.getHtmlContent();
```

**Vad du får:**  
`htmlContent` innehåller hela HTML‑sidan – inklusive `<head>`‑ och `<body>`‑taggar – exakt som den såg ut när e‑posten sparades. Om du bara behöver den synliga delen kan du senare parsra den med Jsoup och ta bort `<head>`.

## Steg 4 – Skriv den extraherade HTML‑koden till en separat fil

Att spara strängen till disk är enkelt med `java.nio.file`‑API:t. Detta steg demonstrerar mönstret **write string to file** som fungerar på alla plattformar.

```java
// Step 4: Save the extracted HTML to a separate file
Files.writeString(Path.of("YOUR_DIRECTORY/email_body.html"), htmlContent);
```

**Tips:**  
Om du behöver ett specifikt teckensnitt, använd `Files.writeString(Path, CharSequence, Charset)`. Standard är UTF‑8, vilket fungerar för de flesta moderna e‑postmeddelanden.

## Steg 5 – Bekräfta extraktionen

En snabb `System.out.println` låter dig verifiera att allt kördes utan undantag. I ett produktionsjobb skulle du ersätta detta med korrekt loggning.

```java
// Step 5: Indicate successful extraction
System.out.println("HTML extracted.");
```

När du kör programmet bör du se `HTML extracted.` i konsolen, och filen `email_body.html` kommer att dyka upp i `YOUR_DIRECTORY`.

## Fullt, kör‑klart exempel

Sätter vi ihop allt får du den kompletta, fristående Java‑klassen. Kopiera och klistra in den i din IDE och tryck på **Run**.

```java
import com.aspose.html.MhtmlDocument;
import java.io.FileInputStream;
import java.io.InputStream;
import java.nio.file.Files;
import java.nio.file.Path;

public class MhtmlToHtmlConverter {

    public static void main(String[] args) {
        // Adjust the path to point to your .mht/.mhtml file
        String sourcePath = "YOUR_DIRECTORY/email.mht";
        String targetPath = "YOUR_DIRECTORY/email_body.html";

        // Try-with-resources ensures the stream is closed automatically
        try (InputStream mhtmlStream = new FileInputStream(sourcePath)) {

            // Load the MHTML document
            MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);

            // Extract the HTML content
            String htmlContent = mhtmlDoc.getHtmlContent();

            // Write the HTML string to a new file
            Files.writeString(Path.of(targetPath), htmlContent);

            // Simple confirmation output
            System.out.println("HTML extracted to " + targetPath);
        } catch (Exception e) {
            // In real code you might want to log this instead of printing
            System.err.println("Failed to extract HTML: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Förväntad utskrift

Running the program prints something like:

```
HTML extracted to YOUR_DIRECTORY/email_body.html
```

Och `email_body.html` kommer att innehålla hela HTML‑källkoden för det ursprungliga e‑postmeddelandet. Öppna den i en webbläsare – du bör se samma visuella rendering som det ursprungliga arkiverade meddelandet (förutom eventuella externa resurser som inte var inbäddade).

## Hantera vanliga kantfall

### 1. Saknade inbäddade resurser

Ibland refererar MHTML‑filen till externa bilder som inte sparades i arkivet. I sådana fall returnerar `getHtmlContent()` fortfarande `<img src="...">`‑markupen, men URL:erna pekar på den ursprungliga webbplatsen. Om du behöver en helt fristående HTML‑fil kan du:

- Använd `MhtmlDocument.save(Path, SaveFormat.HTML)` för att låta Aspose extrahera alla resurser till en mapp.
- Eller efterbehandla HTML med ett bibliotek som **Jsoup** för att ersätta fjärr‑URL:er med base64‑kodade data‑URI:er.

### 2. Icke‑UTF‑8‑kodningar

Om ditt e‑postmeddelande sparades med ett annat teckensnitt (t.ex. `windows-1252`), kan den returnerade strängen innehålla felaktiga tecken. Du kan tvinga ett specifikt teckensnitt vid skrivning:

```java
Files.writeString(
    Path.of(targetPath),
    htmlContent,
    StandardCharsets.ISO_8859_1
);
```

### 3. Stora filer

För arkiv som är större än några hundra megabyte, överväg att streama HTML‑utdata direkt till en `BufferedWriter` istället för att ladda hela strängen i minnet. Aspose erbjuder också en **`save`**‑metod som skriver direkt till en fil, och kringgår den mellanstegande `String`.

## Pro‑tips & bästa praxis

- **Återanvänd `MhtmlDocument`‑objektet** om du behöver extrahera flera delar (t.ex. CSS, bilder). Det parsar arkivet bara en gång.
- **Validera utdata** med en HTML‑validator (W3C‑validatorn eller `jsoup.isValid()`) om du planerar att skicka HTML till ett annat system.
- **Logga, skriv inte ut** i produktion. Ersätt `System.out.println` med ett loggningsramverk som SLF4J för att fånga tidsstämplar och allvarlighetsnivåer.
- **Versionshantera dina beroenden.** Aspose släpper frekventa uppdateringar; lås versionen i din `pom.xml` för att undvika oväntade brytande förändringar.

## Slutsats

Vi har just gått igenom en praktisk, helhetslösning för **extrahering av HTML från MHTML** med Java. Genom att öppna arkivet som en ström, ladda det med Aspose.HTML, hämta HTML‑strängen och **skriva strängen till fil** har du nu ett pålitligt sätt att **konvertera MHTML till HTML**, **extrahera e‑postkropp** och till och med **konvertera MHT till HTML** för efterföljande bearbetning.

Känn dig fri att anpassa kodexemplet: byt `FileInputStream` mot en `ByteArrayInputStream` om dina arkiv finns i en databas, eller integrera koden i ett större batch‑jobb som bearbetar dussintals e‑postmeddelanden åt gången. Grundidén förblir densamma – låt ett dedikerat bibliotek göra det tunga arbetet, och hantera sedan ren text på det sätt du behöver.

**Nästa steg** du kan utforska:

- Använd Jsoup för att **rensa den extraherade HTML‑koden** (ta bort spårningspixelar, inline‑CSS, osv.).
- Automatisera **masskonvertering** genom att loopa över en katalog med `.mht`‑filer.
- Kombinera detta med **Apache POI** för att bädda in den rensade HTML‑koden i Word‑ eller PDF‑dokument.

Har du frågor om ett specifikt kantfall eller vill dela hur du utökade skriptet? Lämna en kommentar nedan – glad kodning!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}