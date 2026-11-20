---
category: general
date: 2026-06-19
description: Hur man startar en tråd i Java med en återanvändbar Runnable, startar
  flera trådar, skriver ut trådens namn och parsar HTML med Java. Steg‑för‑steg‑exempel.
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: sv
og_description: Hur man startar en tråd i Java med Runnable, kör flera trådar, skriver
  ut trådens namn och parsar HTML med Java i ett enda körbart exempel.
og_title: Hur man startar en tråd i Java – Komplett guide
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to start thread in Java with a reusable Runnable, start multiple
    threads, print thread name, and parse HTML with Java. Step‑by‑step example.
  headline: How to start thread in Java – Complete Guide
  type: TechArticle
tags:
- java
- multithreading
- html-parsing
- runnable
title: Hur man startar en tråd i Java – Komplett guide
url: /sv/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man startar tråd i Java – Komplett guide

Har du någonsin funderat på **how to start thread** i Java utan att drunkna i boilerplate‑kod? Du är inte ensam. Oavsett om du bygger en webb‑crawler, en UI‑uppdaterare, eller bara behöver avlasta en tung beräkning, är det ett måste att behärska trådskapande för alla Java‑utvecklare.

I den här handledningen går vi igenom ett praktiskt scenario: **parse HTML with Java**, skriva ut den aktuella trådens namn, och **start multiple threads** som delar samma logik. I slutet kommer du att veta **how to use Runnable**, starta flera arbetare och se den förväntade utskriften — allt i ett självständigt exempel som du kan kopiera och klistra in direkt.

## Vad du kommer att lära dig

- De exakta stegen **how to start thread** med `Thread`‑klassen och en `Runnable`.
- Hur man **start multiple threads** som kör samma uppgift utan att duplicera kod.
- Det enklaste sättet att **print thread name** tillsammans med dina bearbetningsresultat.
- En ren metod för att **parse HTML with Java** med en lättviktig `HTMLDocument`‑hjälpare (eller någon parser du föredrar).
- Varför **how to use runnable** är viktigt för återanvändbar, testbar kod.

Inga externa bibliotek krävs för kärnexemplet, men vi kommer att notera var du kan byta till Jsoup eller en annan parser om du behöver mer kraft.

---

## Steg 1: Definiera en återanvändbar uppgift – **how to use runnable**

Det första du behöver veta **how to use runnable** är att kapsla in det arbete du vill att varje tråd ska utföra. En `Runnable` är bara ett funktionellt gränssnitt med en enda `run()`‑metod, vilket gör den perfekt för lambda‑uttryck.

```java
// Define the reusable task
Runnable extractTextLength = () -> {
    // Open the HTML file inside a try‑with‑resources block
    try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
        // Get the length of the body text
        int textLength = doc.getBody().getTextContent().length();

        // Print the thread name and the length
        System.out.println(Thread.currentThread().getName() + ": " + textLength);
    } catch (Exception e) {
        e.printStackTrace();
    }
};
```

**Varför detta är viktigt:** Genom att hålla logiken i en `Runnable` kan du ge den till hur många `Thread`‑objekt som helst, en trådpool eller till och med en executor‑service senare. Detta gör din kod DRY och testbar.

---

## Steg 2: **How to start thread** – skapa den första arbetaren

Nu när vi har en `Runnable` är det lika enkelt att starta en tråd som att anropa `Thread`‑konstruktorn. Frågan **how to start thread** besvaras i en enda rad:

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

Observera det andra argumentet, `"Worker-1"`. Det namnet kommer att visas när vi senare **print thread name**, vilket gör felsökning mycket mindre kryptisk.

---

## Steg 3: **Start multiple threads** – återanvänd samma `Runnable`

Vill du bearbeta flera HTML‑filer samtidigt? Starta bara en ny `Thread` med samma `Runnable`. Detta visar **start multiple threads** utan att kopiera uppgiftskoden:

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

Både `Worker-1` och `Worker-2` kommer att köra blocket som definieras i `extractTextLength` samtidigt. Eftersom uppgiften är stateless (den läser bara en fil) finns det ingen race‑condition att oroa sig för.

---

## Steg 4: **Print thread name** medan du parser HTML

Inuti `Runnable` har vi redan anropat `Thread.currentThread().getName()`. Det är det kanoniska sättet att **print thread name**. Utdata kommer att se ut ungefär så här (förutsatt att HTML‑kroppen innehåller 1 234 tecken):

```
Worker-1: 1234
Worker-2: 1234
```

Om du kör programmet på en större fil kommer varje rad att visa samma längd eftersom båda trådarna läser samma fil. Ändra sökvägen eller skicka filnamnet som en parameter för att se olika resultat.

---

## Steg 5: Fullt, körbart exempel – från import till körning

Nedan är det kompletta, **self‑contained**‑programmet som du kan lägga i en fil med namnet `HtmlThreadDemo.java`. Det inkluderar en liten `HTMLDocument`‑stub så att koden kompilerar även om du inte har en riktig parser tillgänglig. Ersätt stubben med Jsoup eller något bibliotek du föredrar för produktionsbruk.

```java
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Minimal HTMLDocument helper.
 * In a real project you would use Jsoup or another robust parser.
 */
class HTMLDocument implements AutoCloseable {
    private final String content;

    private HTMLDocument(String html) {
        this.content = html;
    }

    public static HTMLDocument load(String path) throws IOException {
        String html = new String(Files.readAllBytes(Paths.get(path)));
        return new HTMLDocument(html);
    }

    public Body getBody() {
        // Very naive extraction of <body>...</body>
        int start = content.indexOf("<body");
        if (start == -1) return new Body("");
        start = content.indexOf('>', start) + 1;
        int end = content.indexOf("</body>", start);
        if (end == -1) end = content.length();
        return new Body(content.substring(start, end));
    }

    @Override
    public void close() {
        // No resources to free in this stub
    }

    /** Simple wrapper for body text */
    static class Body {
        private final String text;
        Body(String text) { this.text = text; }
        public String getTextContent() { return text; }
    }
}

public class HtmlThreadDemo {

    public static void main(String[] args) {
        // Step 1: Define a reusable task (how to use runnable)
        Runnable extractTextLength = () -> {
            try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
                int textLength = doc.getBody().getTextContent().length();
                // Step 4: Print thread name and length
                System.out.println(Thread.currentThread().getName() + ": " + textLength);
            } catch (Exception e) {
                e.printStackTrace();
            }
        };

        // Step 2 & 3: How to start thread and start multiple threads
        new Thread(extractTextLength, "Worker-1").start();
        new Thread(extractTextLength, "Worker-2").start();
    }
}
```

### Förväntad utskrift

Om vi antar att `page.html` innehåller 2 567 tecken i sin `<body>`‑tagg, kommer du att se något liknande:

```
Worker-1: 2567
Worker-2: 2567
```

Om filen inte kan läsas kommer stack‑trace att skrivas ut — tack vare `catch`‑blocket.

---

## Vanliga fallgropar & pro‑tips

| Problem | Varför det händer | Lösning |
|---------|-------------------|--------|
| **Fil ej hittad** | Sökvägen `"YOUR_DIRECTORY/page.html"` är relativ till där du startar JVM:n. | Använd en absolut sökväg eller `Paths.get("").toAbsolutePath()` för felsökning. |
| **Race‑condition** | Om `Runnable` muterar delat tillstånd kan trådar kollidera. | Håll uppgiften stateless, eller synkronisera åtkomst till delade objekt. |
| **För många trådar** | Att skapa dussintals `Thread`s kan tömma OS‑resurser. | Byt till en `ExecutorService` med en begränsad pool när du behärskar grunderna. |
| **Felaktig HTML‑parsing** | Stubben `HTMLDocument` är förenklad; komplexa sidor går sönder. | Ersätt den med Jsoup: `Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

---

## Utöka exemplet

Nu när du vet **how to start thread**, kanske du vill:

- **Parse different files** genom att skicka filnamnet till `Runnable` (använd en konstruktor eller en lambda som fångar en variabel).
- **Collect results** med en `ConcurrentLinkedQueue<Integer>` istället för att bara skriva ut.
- **Leverage a thread pool** (`Executors.newFixedThreadPool(4)`) för bättre skalbarhet.
- **Swap the parser** till Jsoup, HtmlUnit eller något bibliotek som passar ditt projekts behov.

Alla dessa steg bygger fortfarande på den grundidé vi gick igenom: definiera en återanvändbar uppgift, ge den till en eller flera trådar, och observera vilken tråd som utför arbetet genom att **print thread name**.

## Slutsats

Vi har gått igenom **how to start thread** i Java, demonstrerat **how to use runnable** för återanvändbart arbete, visat hur man **start multiple threads**, och illustrerat ett enkelt sätt att **parse HTML with Java** samtidigt som vi **print thread name** för varje arbetare. Kodsnutten ovan är klar att köra, och koncepten kan skalas till mer komplexa, produktionsklara applikationer.

Känn dig fri att experimentera: ändra filsökvägen, öka antalet arbetare, eller anslut en riktig HTML‑parser. Grunderna förblir desamma, och du har nu en solid grund för alla multitrådade Java‑projekt.

Har du frågor om trådsäkerhet, executor‑services eller HTML‑parsersbibliotek? Lämna en kommentar nedan, och lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}