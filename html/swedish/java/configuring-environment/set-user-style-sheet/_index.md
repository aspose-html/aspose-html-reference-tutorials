---
date: 2026-04-05
description: Lär dig hur du skapar PDF från HTML genom att ange en anpassad användar‑stilmall
  i Aspose.HTML för Java och enkelt konvertera HTML till PDF med User Agent Service.
keywords:
- create pdf from html
- convert html to pdf
- java html to pdf
- generate pdf with css
- configure user agent
linktitle: Ange användarstilmall i Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Skapa PDF från HTML – Ställ in användarens stilmall i Aspose.HTML för Java
url: /sv/java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PDF från HTML – Ange användarformatmall i Aspose.HTML för Java

## Introduktion
I den här handledningen kommer du att lära dig hur du **skapar PDF från HTML** med Aspose.HTML för Java samtidigt som du använder en anpassad användarformatmall. Har du någonsin velat finjustera utseendet på dina HTML-dokument med din egen unika stil? Föreställ dig att du skapar en webbsida och du behöver rubriker som sticker ut med en specifik färg eller stycken som ser enhetliga ut på alla enheter. Det är här en *användarformatmall* och **User Agent Service** kommer in i bilden. Vi går igenom varje steg—från att skriva en enkel HTML-fil, konfigurera användaragenter, till slut att **konvertera HTML till PDF**—så att du kan se resultatet omedelbart.

## Snabba svar
- **Vad betyder “create PDF from HTML”?** Det betyder att rendera ett HTML-dokument (med CSS, bilder, teckensnitt osv.) och spara den visuella utskriften som en PDF-fil.  
- **Vilken Aspose-komponent krävs?** Aspose.HTML för Java-biblioteket tillhandahåller konverteringsmotorn och User Agent Service.  
- **Behöver jag en licens för testning?** En gratis provversion fungerar för utveckling; en kommersiell licens krävs för produktion.  
- **Kan jag använda en extern CSS-fil?** Ja – du kan länka externa formatmallar precis som i en vanlig webbläsare.  
- **Hur lång tid tar konverteringen?** För ett enkelt dokument som det i den här guiden slutförs konverteringen på under en sekund.  
- **Varför konfigurera User Agent Service?** Det låter dig injicera en anpassad formatmall, ange standardteckenkodningar och kontrollera renderingsalternativ, vilket säkerställer enhetlig PDF-utdata.  

## Vad är “create PDF from HTML”?
Att skapa en PDF från HTML är processen att ta ett webb‑orienterat dokument (HTML + CSS) och rendera det till en PDF-fil med fast layout. Detta är användbart för att generera rapporter, fakturor eller annat utskriftsbart material direkt från webbcontent.

## Varför använda Aspose.HTML:s User Agent Service?
**User Agent Service** ger dig låg‑nivå kontroll över renderingsalternativ såsom standardteckenkodning, språk, teckensnitt, och—mest viktigt för den här handledningen—en anpassad användarformatmall. Genom att tillämpa stilar på den här nivån garanterar du enhetlig visuell utskrift även när den ursprungliga HTML‑koden saknar egen CSS.

## Förutsättningar
1. **Aspose.HTML for Java** – ladda ner den senaste JAR‑filen från [Aspose releases page](https://releases.aspose.com/html/java/).  
2. **Java Development Kit (JDK) 8+** – säkerställ att `java -version` rapporterar 8 eller högre.  
3. **IDE** – IntelliJ IDEA, Eclipse eller NetBeans fungerar bra.  
4. **Grundläggande kunskap i HTML/CSS** – användbart men inte obligatoriskt.

## Importera paket
För att börja, importera de nödvändiga Java‑klasserna. Den enda explicita importen du behöver för detta exempel är `java.io.IOException`; Aspose‑klasserna refereras med fullständiga namn senare.

```java
import java.io.IOException;
```

## Steg 1: Skapa ett enkelt HTML-dokument
Först skriver vi en minimal HTML‑fil (`document.html`) som kommer att fungera som källa för vår PDF‑konvertering.

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Proffstips:** Behåll HTML‑filen i samma katalog som din Java‑källa för att undvika sökvägsrelaterade problem.

## Steg 2: Ställ in Aspose.HTML‑konfiguration
Skapa ett `Configuration`‑objekt. Detta objekt fungerar som en behållare för alla tjänster (inklusive User Agent Service) som du kommer att använda senare.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Steg 3: Åtkomst till User Agent Service  
**User Agent Service** låter dig injicera en anpassad formatmall, ange standardteckenkodning och kontrollera andra renderingsalternativ.

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## Steg 4: Definiera och tillämpa användarformatmallen  
Nu tillhandahåller vi CSS‑reglerna som kommer att formatera HTML‑dokumentet när det renderas. Det är här vi **använder user agent service** för att ange formatmallen.

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **Varför detta är viktigt:** Genom att tillämpa en formatmall på användaragentsnivå säkerställer du att stilarna respekteras även om den ursprungliga HTML‑koden inte refererar till en CSS‑fil.

## Steg 5: Ladda HTML‑dokumentet med den anpassade konfigurationen  
Skicka både filsökvägen och `Configuration`‑instansen till `HTMLDocument`‑konstruktorn. Detta binder användarformatmallen till dokumentet.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## Steg 6: Konvertera HTML till PDF  
När dokumentet är fullt stylat, anropa den statiska `convertHTML`‑metoden för att **konvertera HTML till PDF**. `PdfSaveOptions`‑objektet låter dig finjustera utdata (t.ex. sidstorlek, komprimering).

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **Resultat:** `user-agent-stylesheet_out.pdf` kommer att innehålla rubriken i brunt och stycket med en GhostWhite‑bakgrund, exakt som definierat i formatmallen.

## Steg 7: Rensa resurser  
Disposera alltid Aspose‑objekt för att frigöra inbyggt minne.

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

## Vanliga problem & lösningar
| Issue | Cause | Fix |
|-------|-------|-----|
| **Tom PDF‑utdata** | Ingen formatmall tillämpad eller dokumentet inte laddat med konfiguration. | Verifiera att `configuration` skickas till `HTMLDocument` och att `setUserStyleSheet` anropas innan laddning. |
| **Varning för ej stödd CSS‑egenskap** | Aspose.HTML stödjer inte vissa avancerade CSS‑funktioner. | Använd endast CSS‑egenskaper som listas i Aspose.HTML‑dokumentationen eller falla tillbaka på enklare stilar. |
| **FileNotFoundException** | Fel sökväg till `document.html`. | Använd en absolut sökväg eller placera HTML‑filen i projektets rot. |

## Vanliga frågor

**Q: Kan jag tillämpa olika stilar för olika HTML‑element?**  
A: Absolut! Du kan definiera så många CSS‑regler du behöver i användarformatmallen.

**Q: Vad händer om jag behöver ändra formatmallen dynamiskt?**  
A: Anropa `setUserStyleSheet` igen innan du skapar en ny `HTMLDocument`‑instans; de nya stilarna kommer att tillämpas vid nästa konvertering.

**Q: Är det möjligt att använda externa CSS‑filer med Aspose.HTML för Java?**  
A: Ja, du kan antingen länka en extern formatmall i HTML‑koden eller ladda dess innehåll och skicka det till `setUserStyleSheet`.

**Q: Hur hanterar Aspose.HTML ej stödda CSS‑egenskaper?**  
A: Ej stödda egenskaper ignoreras, vilket gör att resten av formatmallen renderas utan fel.

**Q: Kan jag konvertera HTML till andra format än PDF?**  
A: Ja, Aspose.HTML stödjer konvertering till XPS, TIFF, PNG, JPEG och fler med hjälp av lämplig `SaveOptions`‑klass.

---

**Senast uppdaterad:** 2026-04-05  
**Testad med:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}