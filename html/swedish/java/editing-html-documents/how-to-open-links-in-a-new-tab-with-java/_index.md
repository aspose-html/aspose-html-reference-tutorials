---
category: general
date: 2026-10-28
description: Lär dig hur du öppnar länkar i en ny flik genom att analysera HTML i
  Java, hitta externa länkar och lägga till target="_blank".
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: sv
lastmod: 2026-10-28
og_description: 'Öppna länkar i en ny flik med Java: analysera HTML, hitta externa
  länkar, lägga till target=''_blank'' och spara den modifierade HTML‑koden.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Öppna länkar i en ny flik med Java – steg‑för‑steg guide
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: Hur man öppnar länkar i en ny flik med Java
url: /sv/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man öppnar länkar i en ny flik med Java

Om du behöver **open links in a new tab** från en statisk HTML‑fil, visar den här guiden exakt hur du gör det. Du kommer att lära dig att **parse HTML in Java**, **find external links**, **add target blank**, och **save modified HTML** utan att lämna din IDE.

Att öppna externa länkar i en ny webbläsarflik förbättrar användarupplevelsen och håller besökare på den ursprungliga sidan. Lösningen nedan fungerar med vilket HTML‑dokument som helst, kräver bara det populära jsoup‑biblioteket och körs på Java 8 eller senare.

## Förutsättningar

* JDK 8 + installerat  
* Ett byggverktyg (Maven eller Gradle) för att hämta **jsoup**‑beroendet  
* En HTML‑fil som innehåller ankare‑taggar med klassen `external`

Du behöver ingen webbserver eller ytterligare ramverk—jsoup hanterar allt lokalt.

## Steg 1: Installera jsoup i ditt projekt

Lägg till jsoup som ett beroende. Om du använder Maven, placera detta i `pom.xml`:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

För Gradle, lägg till följande rad i `build.gradle`:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Dessa koordinater hämtar den senaste stabila versionen (från och med oktober 2026). Efter synkronisering kan du importera `org.jsoup`‑klasser i dina Java‑källfiler.

## Steg 2: Parsning av HTML‑dokumentet

Att parsa filen är det första steget mot **open links new tab**. Metoden `Jsoup.parse` läser in filen till en muterbar DOM‑liknande struktur.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*Varför detta är viktigt*: `Document` ger dig CSS‑liknande selektorer, vilket gör det enkelt att hitta de element du behöver.

## Steg 3: Hitta externa länkar

Leta nu upp varje `<a>`‑element som har klassen `external`. Detta uppfyller kravet **find external links**.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` är en samling av matchande noder. Om selektorn returnerar en tom mängd, saknar din HTML antingen klassen eller använder en annan namngivningskonvention—justera selektorn därefter.

## Steg 4: Lägg till `target="_blank"` på varje länk

För varje nod som returneras av **find external links**, sätt attributet `target` till `_blank`. Detta uppfyller steget **add target blank** och säkerställer att webbläsare öppnar länken i en ny flik.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

`attr`‑metoden skriver över eventuellt befintligt `target`‑värde, vilket garanterar konsekvent beteende för alla externa ankare.

## Steg 5: Spara den modifierade HTML‑koden

Efter att ha uppdaterat DOM‑en, skriv tillbaka ändringarna till en fil. Detta slutför delen **save modified html** i handledningen.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` serialiserar hela dokumentet och bevarar indentering och formatering som jsoup ursprungligen parsade.

## Fullt fungerande exempel

Genom att sätta ihop alla steg får du ett självständigt program som du kan kopiera, klistra in och köra.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### Förväntat resultat

Anta att `sample.html` innehåller:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

Efter att programmet har körts, kommer `updated.html` att innehålla:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

Endast den externa länken fick attributet `target="_blank"`, vilket betyder att webbläsare nu kommer att öppna den i en ny flik.

## Pro‑tips och vanliga fallgropar

* **Pro tip:** Om du behöver behandla länkar som börjar med `http://` eller `https://` som externa även utan en CSS‑klass, utöka selektorn: `doc.select("a[href^=http]")`.
* **Edge case:** Vissa sidor specificerar redan `target="_self"`; `attr`‑anropet skriver över det, vilket säkerställer konsekvent beteende.
* **Performance:** För mycket stora HTML‑filer, överväg ström‑parsing (`Jsoup.parse(File, String, String, Parser.htmlParser())`) för att minska minnesanvändningen.
* **Testing:** Verifiera resultatet genom att öppna `updated.html` i en webbläsare och inspektera länken med utvecklarverktygen—let efter `target`‑attributet.

## Slutsats

Du har nu en komplett, körbar lösning för att **open links in a new tab** med Java. Handledningen täckte hur man **parse html in java**, **find external links**, **add target blank**, och **save modified html**, allt med det lätta jsoup‑biblioteket.

Från och med nu kan du:

* Utöka selektorn för att hantera andra länk‑mönster (t.ex. `rel="external"`).  
* Kombinera denna logik med ett byggsteg som bearbetar alla HTML‑filer i ett projekt.  
* Integrera koden i en större content‑management‑pipeline.

Känn dig fri att experimentera med olika selektorer eller utdataformat, och dela dina resultat med communityn!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Create new html element with Java – Full Aspose.HTML Guide](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}