---
category: general
date: 2026-01-01
description: Dowiedz się, jak używać stałej puli wątków w Javie do usuwania tagów script
  z plików HTML. Ten przykład ExecutorService w Javie pokazuje efektywne ładowanie
  dokumentów HTML.
draft: false
keywords:
- fixed thread pool java
- remove script tags
- remove javascript html
- executorservice example java
- load html document
language: pl
og_description: Opanuj stałą pulę wątków w Javie, aby usuwać znaczniki script z plików
  HTML. Pełny przykład ExecutorService w Javie z krokami ładowania dokumentu HTML.
og_title: Stała pula wątków w Javie – Przewodnik po równoległym czyszczeniu HTML
tags:
- Java concurrency
- HTML processing
- Aspose.HTML
title: Stała pula wątków w Javie – Równoległe czyszczenie HTML przy użyciu ExecutorService
url: /pl/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Fixed thread pool java – równoległe czyszczenie HTML przy użyciu ExecutorService

Czy kiedykolwiek potrzebowałeś **fixed thread pool java**, aby przyspieszyć przetwarzanie dużej liczby plików HTML? Nie jesteś sam. Gdy masz dziesiątki — a nawet setki — plików HTML pełnych elementów `<script>`, wykonywanie pracy kolejno może przypominać obserwowanie schnącej farby.

W tym samouczku pokażemy dokładnie, jak stworzyć **fixed thread pool java**, wczytać każdy dokument HTML, usunąć cały JavaScript (tagi `<script>`) i zapisać oczyszczone pliki — wszystko równolegle przy użyciu **executorservice example java**. Po zakończeniu będziesz mieć gotowy do uruchomienia program, który skutecznie usuwa tagi skryptów, oraz zrozumiesz, dlaczego stała pula wątków jest często optymalnym rozwiązaniem dla obciążeń CPU‑bound.

## Co osiągniesz

- Skonfiguruj `ExecutorService` z ustaloną liczbą wątków.  
- Wczytaj pliki HTML przy użyciu `HTMLDocument` z Aspose.HTML.  
- Użyj selektora CSS, aby **usunąć tagi script** (lub inne niepożądane elementy).  
- Zapisz oczyszczony wynik, stosując przejrzystą konwencję nazewnictwa.  
- Obsłuż zamknięcie i łagodne zakończenie pracy puli wątków.  

Bez zewnętrznych narzędzi budujących, bez ukrytej magii — po prostu czysty Java 8+ i Aspose.HTML.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

| Wymaganie | Dlaczego jest ważne |
|-------------|----------------|
| **Java 8 lub nowszy** | Wymagany do wyrażeń lambda i API `ExecutorService`. |
| **Aspose.HTML for Java** (pobierz z <https://products.aspose.com/html/java/>) | Udostępnia klasę `HTMLDocument` służącą do wczytywania i manipulacji HTML. |
| **Folder z przykładowymi plikami HTML** | Demo przetwarza pliki takie jak `input1.html`, `input2.html` itd. |
| **IDE lub narzędzie do budowania wiersza poleceń** (IntelliJ, Eclipse, Maven, Gradle) | Do kompilacji i uruchomienia kodu. |

Jeśli jeszcze nie dodałeś Aspose.HTML do swojego projektu, wrzuć plik JAR do folderu `libs` i dodaj go do classpath, lub zadeklaruj zależność Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

## Krok 1: Utwórz Fixed Thread Pool java

**Fixed thread pool java** zapewnia przewidywalną liczbę wątków roboczych, które pozostają aktywne przez cały czas trwania zadania. Unika to kosztów ciągłego tworzenia i niszczenia wątków, co jest szczególnie przydatne, gdy każde zadanie jest krótkotrwałe, np. wczytywanie i czyszczenie pojedynczego pliku HTML.

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;

public class ParallelProcessingDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
        // ...
    }
}
```

> **Pro tip:** Wybierz rozmiar puli w oparciu o liczbę rdzeni CPU (`Runtime.getRuntime().availableProcessors()`) plus niewielki zapas, jeśli zadania obejmują operacje I/O.

## Krok 2: Wypisz pliki HTML, które chcesz przetworzyć

Możesz skanować katalog dynamicznie, ale dla przejrzystości zakodujemy tablicę na stałe. Zastąp `"YOUR_DIRECTORY"` rzeczywistą ścieżką na swoim komputerze.

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/input1.html",
    "YOUR_DIRECTORY/input2.html",
    "YOUR_DIRECTORY/input3.html",
    "YOUR_DIRECTORY/input4.html"
};
```

Jeśli wolisz podejście dynamiczne, `Files.list(Paths.get("YOUR_DIRECTORY"))` może automatycznie wypełnić tablicę.

## Krok 3: Prześlij zadanie czyszczenia dla każdego pliku

Każdy plik otrzymuje własne zadanie **executorservice example java**. Wewnątrz wyrażenia lambda wykonujemy:

1. Otwieramy plik za pomocą `HTMLDocument`.  
2. **Usuwamy tagi script** przy użyciu selektora CSS (`"script"`).  
3. Zapisujemy oczyszczoną wersję z końcówką `_clean.html`.

```java
for (String htmlFile : htmlFiles) {
    executor.submit(() -> {
        // Load the document (each thread works with its own instance)
        try (HTMLDocument doc = new HTMLDocument(htmlFile)) {
            // Remove all <script> elements from the document
            doc.querySelectorAll("script")
               .forEach(node -> node.getParentNode().removeChild(node));

            // Save the cleaned document with a new name
            doc.save(htmlFile.replace(".html", "_clean.html"));
        } catch (Exception e) {
            System.err.println("Failed to process " + htmlFile + ": " + e.getMessage());
        }
    });
}
```

> **Dlaczego to działa:** `querySelectorAll("script")` zwraca żywą kolekcję wszystkich elementów `<script>`. Pętla `forEach` odłącza każdy węzeł od jego rodzica, skutecznie **remove javascript html** z źródła.

## Krok 4: Zakończ działanie puli i poczekaj na zakończenie

Łagodne zakończenie jest kluczowe; nie chcesz, aby niepotrzebne wątki pozostawały po zakończeniu zadania.

```java
// Step 4: Shut down the pool and wait for all tasks to finish
executor.shutdown();
if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
    System.err.println("Some tasks did not finish within the timeout.");
    executor.shutdownNow(); // Force shutdown if needed
}
System.out.println("All HTML files have been cleaned.");
```

Jeśli masz wiele plików lub duże dokumenty, zwiększ limit czasu do większej wartości.

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny program, który możesz skopiować i wkleić do `ParallelProcessingDemo.java` i uruchomić.

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelProcessingDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ List the HTML files to be processed
        String[] htmlFiles = {
            "YOUR_DIRECTORY/input1.html",
            "YOUR_DIRECTORY/input2.html",
            "YOUR_DIRECTORY/input3.html",
            "YOUR_DIRECTORY/input4.html"
        };

        // 3️⃣ Submit a cleaning task for each file
        for (String htmlFile : htmlFiles) {
            executor.submit(() -> {
                try (HTMLDocument doc = new HTMLDocument(htmlFile)) {
                    // 🌟 Remove all <script> elements (remove script tags)
                    doc.querySelectorAll("script")
                       .forEach(node -> node.getParentNode().removeChild(node));

                    // Save cleaned version
                    doc.save(htmlFile.replace(".html", "_clean.html"));
                } catch (Exception e) {
                    System.err.println("Error processing " + htmlFile + ": " + e.getMessage());
                }
            });
        }

        // 4️⃣ Shut down the pool and wait for completion
        executor.shutdown();
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            System.err.println("Timeout reached before all tasks finished.");
            executor.shutdownNow();
        } else {
            System.out.println("All files cleaned successfully!");
        }
    }
}
```

### Oczekiwany wynik

Po uruchomieniu programu zobaczysz komunikaty w konsoli, takie jak:

```
All files cleaned successfully!
```

A w Twoim katalogu znajdziesz:

- `input1_clean.html`
- `input2_clean.html`
- `input3_clean.html`
- `input4_clean.html`

Każdy plik `_clean.html` będzie identyczny z oryginalnym odpowiednikiem, z wyjątkiem wszystkich bloków `<script>`.

## Najczęściej zadawane pytania (FAQ)

**Q: Czy mogę zmienić rozmiar puli wątków w czasie działania?**  
A: Tak. Użyj `Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() + 1)` aby uzyskać dynamiczny rozmiar w zależności od maszyny hosta.

**Q: Co jeśli moje pliki HTML zawierają wbudowane obsługiwacze zdarzeń (`onclick`, `onload`)?**  
A: Obecny selektor usuwa tylko tagi `<script>`. Aby usunąć wbudowane obsługiwacze, trzeba przejść po wszystkich elementach i wyczyścić atrybuty zaczynające się od `on`. To dobre rozszerzenie na późniejszy samouczek.

**Q: Czy Aspose.HTML jest jedyną biblioteką obsługującą `querySelectorAll`?**  
A: Nie. Biblioteki takie jak jsoup również oferują selektory CSS, ale Aspose.HTML zapewnia pełne API DOM, które odzwierciedla zachowanie przeglądarki, co jest przydatne przy złożonych zadaniach czyszczenia.

**Q: Jak radzić sobie z bardzo dużymi plikami HTML, które mogą nie zmieścić się w pamięci?**  
A: Dla ogromnych plików rozważ parsery strumieniowe (np. Saxon dla XML) lub przetwarzanie pliku w kawałkach. Wzorzec stałej puli wątków nadal ma zastosowanie; wystarczy zamienić `HTMLDocument` na rozwiązanie strumieniowe.

## Kolejne kroki i powiązane tematy

- **Remove JavaScript HTML with jsoup** – lekka alternatywa, jeśli nie potrzebujesz pełnego wsparcia DOM.  
- **Dynamic thread pool sizing** – poznaj `ThreadPoolExecutor` dla bardziej szczegółowej kontroli.  
- **Batch processing with `CompletableFuture`** – łącz future’y dla bardziej rozbudowanych potoków.  
- **HTML sanitization beyond scripts** – usuń style, iframe’y lub niebezpieczne atrybuty.  

Wszystkie te tematy opierają się na tej samej podstawie **executorservice example java**, którą tutaj przedstawiliśmy.

## Zakończenie

Masz teraz solidny, gotowy do produkcji przykład, jak używać **fixed thread pool java** do **usuwania tagów script** z partii plików HTML. Dzięki wykorzystaniu `ExecutorService` każdy plik jest przetwarzany równolegle, co znacząco skraca całkowity czas wykonania. Podejście jest modularne, łatwe do rozszerzenia i działa z każdą biblioteką HTML kompatybilną z Javą, która oferuje możliwość `load html document`.

Wypróbuj go, dostosuj rozmiar puli lub dodaj dodatkowe reguły czyszczenia — twoja kolejna przygoda z przetwarzaniem HTML jest już o kilka linii kodu.

![Fixed thread pool java illustration](https://example.com/fixed-thread-pool-java.png "Fixed thread pool java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}