---
category: general
date: 2026-02-16
description: Hur man laddar HTML i Java, sätter enhetens DPI, definierar en virtuell
  skärmstorlek och läser den beräknade bakgrundsfärgen för ett godtyckligt element.
draft: false
keywords:
- how to load html
- read background color
- set device dpi
- set virtual screen size
- get computed background color
language: sv
og_description: Hur man laddar HTML i Java, sätter enhetens DPI, definierar en virtuell
  skärmstorlek och läser den beräknade bakgrundsfärgen för ett godtyckligt element.
og_title: Hur man laddar HTML, ställer in enhetens DPI och läser bakgrundsfärgen
tags:
- Aspose.HTML
- Java
title: Hur man laddar HTML, ställer in enhetens DPI och läser bakgrundsfärgen
url: /sv/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man laddar HTML, ställer in enhetens DPI och läser bakgrundsfärg

Har du någonsin funderat **hur man laddar html** i en Java‑app och sedan inspekterar sidans stilar? Du är inte ensam—utvecklare behöver ofta rendera en webbsida off‑screen, hämta de slutgiltiga CSS‑värdena och använda dem för PDF‑konvertering, skärmdumpar eller till och med automatiserade tester.  

I den här guiden går vi igenom exakt det: vi laddar en HTML‑fil, **ställer in enhetens DPI**, definierar en **virtuell skärmstorlek** och slutligen **läser bakgrundsfärgen** från `<body>`‑elementet. När du är klar har du ett fullt körbart kodexempel som skriver ut den **beräknade bakgrundsfärgen**—ingen magi, bara ren Java.

## Vad du behöver

Innan vi dyker ner, se till att du har:

* Java 17 eller nyare (koden fungerar med vilken recent JDK som helst).  
* Aspose.HTML för Java 23.9 eller senare—ladda ner JAR‑filen från Aspose‑sidan eller lägg till den via Maven.  
* En enkel HTML‑fil (t.ex. `responsive.html`) som definierar en bakgrundsfärg i CSS.

Det är allt—inga extra ramverk, inga webbläsardrivrutiner. Klar? Låt oss börja.

![Diagram som visar hur man laddar html och extraherar beräknade stilar](/images/load-html-diagram.png){alt="Diagram som visar hur man laddar html"}

## Steg 1: Hur man laddar HTML och konfigurerar renderingsalternativ

Det första du gör är att skapa ett `HtmlLoadOptions`‑objekt. Detta objekt talar om för Aspose.HTML **hur man laddar html**—inklusive de virtuella skärm‑dimensionerna och DPI‑värdet du vill emulera.

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create load options and define the virtual screen size and DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        // setVirtualScreenSize – width × height in CSS pixels
        loadOptions.setScreenSize(new Size(1280, 800));
        // setDeviceDpi – typical desktop DPI (96 is the default for most monitors)
        loadOptions.setDeviceDpi(96);
```

**Varför detta är viktigt:**  
Att sätta en virtuell skärmstorlek säkerställer att media‑queries som `@media (max-width: 600px)` beter sig som om sidan renderades på en riktig monitor. DPI:n påverkar hur CSS‑`px`‑enheter mappas till fysiska pixlar—avgörande när du senare genererar bilder eller PDF‑filer.

## Steg 2: Ladda HTML‑filen med de konfigurerade alternativen

Nu laddar vi faktiskt filen. Observera att vi skickar med samma `loadOptions` som vi just konfigurerade.

```java
        // 2️⃣ Load the HTML file with the options we just set.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);
```

Om filen inte hittas kastar Aspose ett tydligt `FileNotFoundException`. I produktion kan du vilja omsluta detta med en try‑catch och falla tillbaka till en standard‑HTML‑sträng.

## Steg 3: Ställ in virtuell skärmstorlek och enhetens DPI (explicit)

Även om vi redan har anropat `setScreenSize` och `setDeviceDpi` ovan, är det värt att påpeka att **set virtual screen size** och **set device dpi** kan justeras när som helst före rendering. Till exempel kan du öka DPI:n för högupplösta skärmdumpar:

```java
        // 3️⃣ Adjust DPI for a high‑resolution render (optional).
        loadOptions.setDeviceDpi(300);   // 300 DPI is common for print‑ready images
        // 4️⃣ Change screen size for a mobile layout test.
        loadOptions.setScreenSize(new Size(375, 667)); // iPhone X viewport
```

Kom ihåg att ladda om dokumentet om du ändrar dessa inställningar efter den första laddningen—Aspose behandlar dem som oföränderliga när `Document`‑objektet har skapats.

## Steg 4: Läs bakgrundsfärg och hämta beräknad bakgrundsfärg

Med dokumentet i minnet kan du fråga vilken elements beräknade stil som helst. Här fokuserar vi på `<body>`‑taggen, men samma metod fungerar för `<div>`, `<p>` eller till och med pseudo‑element.

```java
        // 5️⃣ Retrieve the <body> element.
        Element bodyElement = document.getBody();

        // 6️⃣ Output the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

**Vad du kommer att se:** Om `responsive.html` innehåller `body { background: #ff5722; }`, skriver konsolen ut något i stil med:

```
Computed background color: rgba(255,87,34,1)
```

Det är resultatet av **get computed background color**—Aspose löser alla CSS‑kaskadregler, media‑queries och även `!important`‑deklarationer innan det returnerar det slutgiltiga värdet.

## Fullt fungerande exempel

Sätter vi ihop allt, så får du det kompletta, kopiera‑och‑klistra‑klara programmet:

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create load options – virtual screen size + DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setScreenSize(new Size(1280, 800)); // set virtual screen size
        loadOptions.setDeviceDpi(96);                  // set device DPI (default desktop)

        // Optional: tweak for high‑resolution or mobile rendering.
        // loadOptions.setDeviceDpi(300);
        // loadOptions.setScreenSize(new Size(375, 667));

        // Step 2: Load the HTML document with the options.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);

        // Step 3: Grab the <body> element.
        Element bodyElement = document.getBody();

        // Step 4: Print the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

### Förväntad utskrift

```
Computed background color: rgba(255,255,255,1)
```

*(De exakta RGBA‑värdena beror på CSS‑en i din HTML‑fil.)*

## Vanliga fallgropar & pro‑tips

* **Saknar du DPI‑inställning?** Aspose använder som standard 96 DPI, vilket kan göra högupplösta skärmdumpar suddiga. Ställ alltid in den explicit om du behöver skarpa resultat.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}