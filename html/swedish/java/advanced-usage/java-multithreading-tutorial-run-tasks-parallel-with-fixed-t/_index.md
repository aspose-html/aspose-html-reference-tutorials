---
category: general
date: 2026-04-05
description: Java-multitrådningshandledning som visar hur man kör uppgifter parallellt
  med en fast trådpool i Java och stänger ner ExecutorService på ett säkert sätt.
draft: false
keywords:
- java multithreading tutorial
- fixed thread pool java
- shutdown executorservice
- print thread name
- run tasks parallel
language: sv
og_description: Java‑multitrådningshandledning som guidar dig genom att köra uppgifter
  parallellt, skapa en fast trådpool i Java, skriva ut trådnamen och städa ner ExecutorService
  på ett korrekt sätt.
og_title: java-multitrådad handledning – Parallell körning med fast trådpool
tags:
- Java
- Concurrency
- ExecutorService
title: 'java-multitrådningshandledning: Kör uppgifter parallellt med en fast trådpool'
url: /sv/java/advanced-usage/java-multithreading-tutorial-run-tasks-parallel-with-fixed-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java multithreading tutorial – Parallell exekvering gjort enkelt

Har du någonsin undrat hur man **run tasks parallel** i Java utan att drunkna i låg‑nivå trådhante­ring? I den här **java multithreading tutorial** går vi igenom exakt det: att använda en **fixed thread pool java**, skriva ut varje tråds namn, och på ett rent sätt **shutdown executorservice** när arbetet är klart.  

Om du någonsin har skrivit en loop som blockerar på nätverks‑I/O eller du behöver skrapa flera webbsidor samtidigt, kommer mönstret vi täcker nedan att spara både tid och huvudvärk.  

Vi kommer att täcka allt du behöver—inga externa dokument, bara ren Java‑kod som du kan kopiera‑klistra, köra och se resultat. I slutet förstår du varför en fixed thread pool ofta är den bästa lösningen för begränsad parallellism, hur du säkert avslutar den, och hur du gör dina loggar mer läsbara genom att skriva ut trådens namn.  

> **Prerequisites**: Java 8+ (paketet `java.util.concurrent` har varit stabilt i åratal), en IDE eller enkel `javac`/`java` kommandorad, och en grundläggande förståelse för OOP. Inga extra bibliotek krävs utöver Aspose HTML for Java‑jar‑filen du redan har.

---

![java multithreading tutorial-diagram som visar en trådpool som matar upp uppgifter](https://example.com/images/java-multithreading-tutorial.png "java multithreading tutorial diagram")

## java multithreading tutorial – Skapa en Fixed Thread Pool

En **fixed thread pool** begränsar antalet samtidigt körande trådar, vilket förhindrar att din applikation skapar för många OS‑trådar och uttömmer resurser. Här skapar vi en pool med fyra arbetare:

```java
import java.util.concurrent.*;

public class ParallelProcessingTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Varför fyra?* Det matchar antalet URL:er vi kommer att hämta, men du kan justera detta antal baserat på CPU‑kärnor, I/O‑intensitet eller minnesgränser. `Executors`‑fabriken skyddar dig från den lågnivå `Thread`‑konstruktorn och ger dig en ren `ExecutorService`‑referens som du senare **shutdown executorservice**.

## Förbered URL:er och definiera parallella uppgifter

Nästa steg är att lista de sidor vi vill bearbeta. I en riktig skrapare skulle du förmodligen läsa dessa från en fil eller databas, men en statisk array håller exemplet självständigt:

```java
        // Step 2: List the web pages to process
        String[] pageUrls = {
            "https://example.com/a.html",
            "https://example.com/b.html",
            "https://example.com/c.html",
            "https://example.com/d.html"
        };
```

Nu kommer delen **run tasks parallel**. För varje URL skickar vi in en lambda som laddar dokumentet och skriver ut dess titel. Lägg märke till användningen av `Thread.currentThread().getName()` – det är vårt **print thread name**‑knep som gör felsökning mycket enklare:

```java
        // Step 3: Submit a task for each URL that loads the document and prints its title
        for (String url : pageUrls) {
            executor.submit(() -> {
                try (HTMLDocument doc = new HTMLDocument(url)) {
                    String title = doc.getTitle();
                    // Print the thread name alongside the title
                    System.out.println(Thread.currentThread().getName() + " – " + title);
                } catch (Exception e) {
                    System.err.println(Thread.currentThread().getName() + " failed: " + e.getMessage());
                }
            });
        }
```

> **Pro tip**: Att omsluta `HTMLDocument` i ett try‑with‑resources‑block garanterar att den underliggande strömmen stängs, även om sidan misslyckas med att laddas.

## Avsluta ExecutorService på ett graciöst sätt

Att låta en trådpool vara aktiv efter att dess arbete är klart kan få din JVM att hänga. Det korrekta sättet är att **shutdown executorservice**, och sedan vänta på avslut:

```java
        // Step 4: Shut down the pool and wait for all tasks to finish
        executor.shutdown();                         // No new tasks will be accepted
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            // Force shutdown if tasks exceed the timeout
            executor.shutdownNow();
        }
    }
}
```

*Varför timeouten?* Den skyddar dig från en lömsk uppgift som aldrig returnerar (t.ex. ett nätverksanrop som hänger). Om poolen inte avslutas inom en minut anropar vi `shutdownNow()` för att avbryta eventuella kvarvarande trådar.

### Förväntad output

Att köra programmet skriver ut något liknande:

```
pool-1-thread-1 – Example A
pool-1-thread-3 – Example C
pool-1-thread-2 – Example B
pool-1-thread-4 – Example D
```

Den exakta ordningen kan variera—uppgifterna är ju faktiskt parallella. Vad som förblir konstant är **print thread name**‑prefixet, som exakt visar vilken arbetare som hanterade varje URL.

---

## Vanliga variationer & kantfall

| Situation | Vad att ändra | Orsak |
|-----------|----------------|--------|
| **Fler URL:er än trådar** | Behåll samma pool‑storlek; extra uppgifter köas automatiskt. | Fixed‑poolen hanterar back‑pressure åt dig. |
| **CPU‑bindad arbetsbelastning** | Sätt pool‑storleken till `Runtime.getRuntime().availableProcessors()` istället för ett hårdkodat 4. | Maximerar CPU‑utnyttjande utan att överskrida. |
| **Behöver avbryta en specifik uppgift** | Behåll en `Future<?>`‑referens från `executor.submit()` och anropa `future.cancel(true)`. | Ger fin‑granulerad kontroll över enskilda jobb. |
| **Bearbetning av stora filer** | Öka pool‑storleken måttligt *eller* byt till `newCachedThreadPool()` om du förväntar dig spikar. | Cachade pooler skapar trådar vid behov, men var försiktig med obegränsad tillväxt. |

---

## Slutsats

Du har nu en solid **java multithreading tutorial** som demonstrerar hur man **run tasks parallel** med en **fixed thread pool java**, **print thread name** för tydlig loggning, och **shutdown executorservice** på ett rent sätt. Den kompletta, körbara koden finns i en enda klass, så du kan slänga in den i vilket projekt som helst och omedelbart börja skala ditt I/O‑bindade arbete.

Vad blir nästa steg? Prova att byta ut `HTMLDocument` mot din egen HTTP‑klient, experimentera med olika pool‑storlekar, eller integrera en `CompletionService` för att samla resultat när de blir klara. Du kan också utforska `java.util.concurrent.Flow` för reaktiva strömmar om du behöver back‑pressure‑hantering utöver en enkel kö.

Lycka till med kodandet, och kom ihåg: med rätt tråd‑pool‑strategi blir samtidighet en *bit av en kaka*, inte en källa till buggar. Om du har frågor, tveka inte att lämna en kommentar—jag är alltid redo för ett samtal om Java‑konkurrens!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}