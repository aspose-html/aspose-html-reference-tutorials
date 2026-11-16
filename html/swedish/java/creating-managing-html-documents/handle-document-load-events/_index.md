---
date: 2026-04-23
description: Lär dig hur du får outer HTML och väntar på att dokumentet laddas med
  Aspose.HTML för Java i den här steg‑för‑steg‑guiden.
keywords:
- get outer html
- wait for document load
- java html processing
- navigate html document
- aspose html example
linktitle: Hantera dokumentladdningshändelser i Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Hämta Outer HTML och hantera laddningshändelser i Aspose.HTML för Java
url: /sv/java/creating-managing-html-documents/handle-document-load-events/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hämta yttre HTML och hantera laddningshändelser i Aspose.HTML för Java

## Introduktion
När du behöver **hämta yttre html** från en fjärrsida och reagera så snart dokumentet har laddats färdigt blir hantering av dokumentets laddningshändelser avgörande. I Java erbjuder Aspose.HTML ett rent API för både att navigera till en URL och lyssna på `OnLoad`‑händelsen, så att du säkert kan komma åt HTML‑koden när den är klar. Denna handledning guidar dig genom hela processen – från att sätta upp miljön till att skriva ut den yttre HTML‑koden för en laddad sida – så att du kan integrera den i vilken web‑centrerad Java‑applikation som helst.

## Snabba svar
- **Vad betyder “get outer html”?** Det returnerar hela HTML‑markupen för dokumentets rot‑element.  
- **Vilket bibliotek hanterar laddningshändelser?** Aspose.HTML för Java tillhandahåller `OnLoad`‑händelsen.  
- **Behöver jag en licens för testning?** En gratis provversion finns tillgänglig; en kommersiell licens krävs för produktion.  
- **Hur kan jag vänta på att dokumentet ska laddas?** Använd `OnLoad`‑hanteraren eller en enkel sleep för demonstrationsändamål.  
- **Är detta tillvägagångssätt asynkront säkert?** Ja, händelsen avfyras efter att dokumentet har laddats färdigt, vilket säkerställer att HTML‑koden är redo.

## Vad är “get outer html”?
`document.getDocumentElement().getOuterHTML()` returnerar den kompletta HTML‑strängen för dokumentets rot‑element, inklusive öppnings‑ och stängningstaggarna. Detta är användbart när du behöver den råa markupen för vidare bearbetning, lagring eller transformation.

## Varför använda Aspose.HTML för Java?
- **Robust HTML‑parsing** utan att behöva en webbläsarmotor.  
- **Händelsedriven modell** låter dig reagera exakt när dokumentet är klart.  
- **Plattformsoberoende** stöd för Windows, Linux och macOS.  
- **Rik API** för navigering, manipulation och konvertering till PDF, bild osv.

## Förutsättningar
Innan vi dyker ner i koden, se till att du har följande:

1. **Java Development Kit (JDK)** – Installera från [Oracle's website](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html).  
2. **Aspose.HTML för Java** – Ladda ner den senaste JAR‑filen från [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse eller någon annan editor du föredrar.  
4. **Grundläggande Java‑kunskaper** – Förståelse för klasser, metoder och händelsehantering.  
5. **Internetanslutning** – Exemplet laddar en online‑HTML‑sida.

När allt är klart är du redo att börja koda!

## Steg‑för‑steg‑guide

### Steg 1: Initiera ett HTML‑dokument
Först skapar du en `HTMLDocument`‑instans. Vi sätter också upp en `AtomicBoolean` för att hålla reda på laddningsstatusen.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument();
java.util.concurrent.atomic.AtomicBoolean isLoading = new java.util.concurrent.atomic.AtomicBoolean(false);
```

### Steg 2: Prenumerera på **OnLoad**‑händelsen
Fäst en hanterare som sätter `isLoading`‑flaggan när dokumentet har laddats färdigt. Här vet vi att det är säkert att anropa **get outer html**.

```java
document.OnLoad.add(new DOMEventHandler() {
    @Override
    public void invoke(Object o, Event event) {
        isLoading.set(true);
    }
});
```

### Steg 3: Navigera till dokumentet (ladda html från url)
Berätta för `HTMLDocument` vilken sida som ska hämtas. I detta exempel laddar vi en offentlig Aspose‑dokumentationssida.

```java
document.navigate("https://docs.aspose.com/html/net/creating-a-document/document.html");
```

### Steg 4: Vänta på att dokumentet ska laddas
Att ladda en fjärrsida är asynkront. För demonstration pausar vi tråden i några sekunder; i produktion skulle du förlita dig på `OnLoad`‑flaggan eller en mer sofistikerad synkroniseringsmetod.

```java
Thread.sleep(5000);
```

### Steg 5: Åtkomst till det laddade dokumentet och **Get Outer HTML**
Nu när `isLoading` är true, hämta den fullständiga markupen för dokumentets rot‑element.

```java
System.out.println("outerHTML = " + document.getDocumentElement().getOuterHTML());
```

Du bör se den kompletta HTML‑koden för den laddade sidan skriven till konsolen.

## Vanliga problem och lösningar
| Problem | Orsak | Lösning |
|-------|--------|-----|
| **`isLoading` blir aldrig true** | `OnLoad`‑hanteraren var inte fäst innan `navigate()` | Fäst hanteraren **innan** du anropar `navigate()`. |
| **`NullPointerException` på `getDocumentElement()`** | Dokumentet är inte helt laddat när det nås | Använd en korrekt väntemetod (t.ex. loopa på `isLoading.get()` eller en `CountDownLatch`). |
| **SSLHandshakeException** när HTTPS‑URL:er laddas | Saknade betrodda certifikat | Lägg till rätt certifikat i din Java‑keystore eller använd `-Djsse.enableSNIExtension=false`. |
| **Långsam laddning orsakar timeout** | Stor sida eller nätverkslatens | Öka sömnperioden eller implementera en timeout‑medveten lyssnare. |

## Vanliga frågor

**Q: Vad är Aspose.HTML för Java?**  
A: Aspose.HTML för Java är ett bibliotek som låter utvecklare skapa, manipulera och konvertera HTML‑dokument i Java‑applikationer.

**Q: Hur laddar jag ner Aspose.HTML för Java?**  
A: Du kan ladda ner det från [Aspose releases page](https://releases.aspose.com/html/java/).

**Q: Kan jag använda Aspose.HTML gratis?**  
A: Ja, du kan prova Aspose.HTML gratis genom att ladda ner en provversion från [Aspose website](https://releases.aspose.com/).

**Q: Finns det support för Aspose.HTML?**  
A: Ja, du kan hitta support och ställa frågor på [Aspose forum](https://forum.aspose.com/c/html/29).

**Q: Hur får jag en tillfällig licens för Aspose.HTML?**  
A: Du kan begära en tillfällig licens genom att besöka [Aspose temporary license page](https://purchase.aspose.com/temporary-license/).

---

**Senast uppdaterad:** 2026-04-23  
**Testat med:** Aspose.HTML för Java 24.11  
**Författare:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}