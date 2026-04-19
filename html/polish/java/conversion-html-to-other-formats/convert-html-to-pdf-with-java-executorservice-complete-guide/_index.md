---
category: general
date: 2026-04-19
description: Szybko konwertuj HTML na PDF przy użyciu przykładu Java ExecutorService.
  Poznaj wzorzec stałej puli wątków w Javie do generowania PDF z HTML i bezpiecznego
  zamykania usługi executor.
draft: false
keywords:
- convert html to pdf
- java executorservice example
- fixed thread pool java
- generate pdf from html
- shutdown executor service
language: pl
og_description: Konwertuj HTML na PDF efektywnie, używając podejścia z stałą pulą
  wątków w Javie. Ten przewodnik pokazuje pełny przykład java ExecutorService, jak
  generować PDF z HTML oraz prawidłowe zamykanie usługi ExecutorService.
og_title: Konwertuj HTML na PDF przy użyciu Java ExecutorService – krok po kroku
tags:
- Java
- Concurrency
- PDF Generation
title: Konwertuj HTML do PDF przy użyciu Java ExecutorService – Kompletny przewodnik
url: /pl/java/conversion-html-to-other-formats/convert-html-to-pdf-with-java-executorservice-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertowanie HTML do PDF przy użyciu Java ExecutorService – Kompletny przewodnik

Czy kiedykolwiek potrzebowałeś **konwertować HTML do PDF**, ale martwiłeś się o szybkość przy dziesiątkach plików? Nie jesteś sam. W wielu potokach przetwarzania wsadowego podejście jednowątkowe staje się wąskim gardłem, szczególnie gdy biblioteka konwersji sama jest zależna od I/O.

Dobrą wiadomością jest to, że `ExecutorService` w Javie pozwala uruchomić **stałą pulę wątków** i wykonywać wiele konwersji równolegle, jednocześnie utrzymując kod czystym i zasoby pod kontrolą. W tym samouczku przeprowadzimy **przykład java executorservice**, który **generuje PDF z HTML**, wyjaśni dlaczego stała pula wątków jest optymalnym rozwiązaniem oraz pokaże właściwy sposób **zatrzymania executor service**, gdy wszystko zostanie zakończone.

Po zakończeniu tego przewodnika będziesz mieć gotowy do uruchomienia program, który pobiera listę plików HTML, konwertuje każdy z nich do PDF przy użyciu Aspose.HTML i kończy się elegancko — bez osieroconych wątków, bez wycieków pamięci.

---

## Co zbudujesz

- Klasa Java o nazwie `ParallelBatch`, która odczytuje tablicę ścieżek do plików HTML.  
- **Stała pula wątków** (`Executors.newFixedThreadPool`), która przetwarza każdą konwersję równolegle.  
- Czyste zarządzanie cyklem życia executor’a przy użyciu `shutdown()` i `awaitTermination`.  
- Wyjście w konsoli potwierdzające każdy wygenerowany plik PDF.

**Wymagania wstępne**

- Java 17 lub nowsza (kod używa składni lambda).  
- Biblioteka Aspose.HTML for Java w classpath (pobierz z [aspose.com/html/java](https://products.aspose.com/html/java/)).  
- Folder zawierający kilka przykładowych plików `.html`.

Nie są wymagane zewnętrzne narzędzia budujące; możesz kompilować przy użyciu `javac` i uruchamiać przy użyciu `java`. Jeśli wolisz Maven lub Gradle, po prostu dodaj zależność Aspose.HTML odpowiednio.

---

## Krok 1: Konfiguracja projektu i zależności

### Dlaczego to jest ważne

Zanim jakikolwiek kod zostanie uruchomiony, JVM musi odnaleźć klasy Aspose.HTML. Brakujące pliki JAR powodują `ClassNotFoundException`, co jest częstą pułapką dla początkujących.

### Jak to zrobić

1. **Utwórz folder** o nazwie `pdf‑converter`.  
2. **Pobierz** `aspose-html-<version>.jar` i umieść go w podfolderze `libs`.  
3. **Ułóż** swój plik źródłowy w następujący sposób:

```
pdf-converter/
├─ libs/
│  └─ aspose-html-23.10.jar
└─ src/
   └─ ParallelBatch.java
```

You can compile with:

```bash
javac -cp "libs/*" src/ParallelBatch.java -d out
```

And run with:

```bash
java -cp "out:libs/*" ParallelBatch
```

*(On Windows replace `:` with `;` in the classpath.)*

---

## Krok 2: Lista plików HTML, które chcesz skonwertować

### Uzasadnienie

Hard‑kodowanie listy plików jest w porządku dla demonstracji, ale w produkcji prawdopodobnie zeskanowałbyś katalog. Dla prostoty pozostawimy tablicę; pokazuje ona podstawową logikę bez rozpraszania Cię kodem I/O.

### Kod

```java
// Step 2: Define the source HTML files
String[] htmlFiles = {
    "YOUR_DIRECTORY/1.html",
    "YOUR_DIRECTORY/2.html",
    "YOUR_DIRECTORY/3.html"
};
```

Zastąp `YOUR_DIRECTORY` absolutną lub względną ścieżką, w której znajdują się Twoje pliki HTML.

---

## Krok 3: Utworzenie instancji stałej puli wątków w Javie

### Dlaczego stała pula?

**Stała pula wątków** (`newFixedThreadPool`) zapewnia przewidywalną liczbę wątków roboczych. Zbyt wiele wątków może wyczerpać CPU lub pamięć, podczas gdy zbyt mało nie wykorzysta systemu w pełni. Dla zadań CPU‑bound reguła kciuka to `availableProcessors()`, ale dla konwersji I/O‑bound umiarkowana pula 3‑5 wątków często daje najlepszą przepustowość.

### Kod

```java
// Step 3: Initialise a fixed‑size thread pool (3 threads in this example)
ExecutorService executor = Executors.newFixedThreadPool(3);
```

Śmiało dostosuj rozmiar puli w zależności od swojego sprzętu i rozmiaru plików HTML.

---

## Krok 4: Zgłoszenie zadania konwersji dla każdego pliku HTML

### Jak to działa

Każde zadanie to lambda, która:

1. Tworzy nazwę pliku PDF (`replace(".html", ".pdf")`).  
2. Wywołuje `Conversion.convert` z Aspose.HTML.  
3. Wypisuje linię potwierdzającą.

Użycie `executor.submit` zapewnia, że zadanie zostanie uruchomione na jednym z wątków puli.

### Kod

```java
// Step 4: Enqueue conversion jobs
for (String htmlFilePath : htmlFiles) {
    executor.submit(() -> {
        // Derive the PDF output path
        String pdfFilePath = htmlFilePath.replace(".html", ".pdf");
        // Perform the conversion
        Conversion.convert(htmlFilePath, pdfFilePath);
        // Log the result
        System.out.println(pdfFilePath + " generated.");
    });
}
```

**Wskazówka:** Jeśli konwersja się nie powiedzie, Aspose rzuca `Exception`. Możesz otoczyć ciało w try‑catch, aby logować błędy bez zabijania całej puli.

```java
executor.submit(() -> {
    try {
        String pdfFilePath = htmlFilePath.replace(".html", ".pdf");
        Conversion.convert(htmlFilePath, pdfFilePath);
        System.out.println(pdfFilePath + " generated.");
    } catch (Exception e) {
        System.err.println("Failed to convert " + htmlFilePath + ": " + e.getMessage());
    }
});
```

---

## Krok 5: Eleganckie zamknięcie Executor Service

### Dlaczego eleganckie zamknięcie?

Wywołanie `shutdown()` zapobiega przyjmowaniu nowych zadań. `awaitTermination` blokuje aż wszystkie oczekujące zadania zakończą się **lub** upłynie limit czasu. Ten wzorzec zapewnia, że aplikacja nie zakończy się, gdy wątki w tle nadal pracują, co jest częstą przyczyną obciętych PDF‑ów.

### Kod

```java
// Step 5: Shut down the pool and wait for completion
executor.shutdown();                       // No new tasks
boolean finished = executor.awaitTermination(5, TimeUnit.MINUTES);

if (finished) {
    System.out.println("All PDFs generated successfully.");
} else {
    System.err.println("Timeout reached before all tasks finished.");
}
```

Możesz zwiększyć limit czasu, jeśli spodziewasz się bardzo dużych dokumentów.

---

## Pełny działający przykład

Poniżej znajduje się kompletny, samodzielny program. Skopiuj i wklej go do `src/ParallelBatch.java`, dostosuj ścieżki plików i uruchom zgodnie z opisem w Kroku 1.

```java
import com.aspose.html.Conversion;
import java.util.concurrent.*;

public class ParallelBatch {
    public static void main(String[] args) throws Exception {
        // Step 1: List the HTML files that will be converted to PDF
        String[] htmlFiles = {
            "YOUR_DIRECTORY/1.html",
            "YOUR_DIRECTORY/2.html",
            "YOUR_DIRECTORY/3.html"
        };

        // Step 2: Create a fixed‑size thread pool to run conversions in parallel
        ExecutorService executor = Executors.newFixedThreadPool(3);

        // Step 3: For each HTML file, submit a conversion task to the pool
        for (String htmlFilePath : htmlFiles) {
            executor.submit(() -> {
                try {
                    String pdfFilePath = htmlFilePath.replace(".html", ".pdf");
                    // Convert HTML to PDF using Aspose.HTML
                    Conversion.convert(htmlFilePath, pdfFilePath);
                    System.out.println(pdfFilePath + " generated.");
                } catch (Exception e) {
                    System.err.println("Error converting " + htmlFilePath + ": " + e.getMessage());
                }
            });
        }

        // Step 4: Shut down the executor and wait for all tasks to finish
        executor.shutdown(); // stop accepting new tasks
        boolean terminated = executor.awaitTermination(5, TimeUnit.MINUTES);

        if (terminated) {
            System.out.println("All conversions completed.");
        } else {
            System.err.println("Some tasks did not finish within the timeout.");
        }
    }
}
```

**Oczekiwany output w konsoli** (kolejność może się różnić ze względu na równoległość):

```
YOUR_DIRECTORY/1.pdf generated.
YOUR_DIRECTORY/2.pdf generated.
YOUR_DIRECTORY/3.pdf generated.
All conversions completed.
```

Jeśli którykolwiek plik się nie powiedzie, zobaczysz linię błędu z przyczyną, ale pozostałe konwersje będą kontynuowane.

---

## Częste pytania i przypadki brzegowe

### 1. *Co jeśli mam setki plików HTML?*

Zwiększ rozmiar puli umiarkowanie (np. `Runtime.getRuntime().availableProcessors()`) i rozważ odczyt listy plików z katalogu:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
try (Stream<Path> stream = Files.list(dir)) {
    List<String> files = stream
        .filter(p -> p.toString().endsWith(".html"))
        .map(Path::toString)
        .collect(Collectors.toList());
    // feed `files` into the executor loop
}
```

### 2. *Czy mogę ograniczyć użycie pamięci?*

Aspose.HTML strumieniuje plik źródłowy, ale jeśli przetwarzasz bardzo duże strony HTML, możesz chcieć ustawić własne `ConversionOptions` z niższą wartością `MaxMemory`. Dokumentacja API podaje dokładne nazwy właściwości.

### 3. *Co jeśli konwersja się zawiesi?*

Otocz zadanie w `Future` i użyj `future.get(timeout, TimeUnit.SECONDS)`. Jeśli limit czasu wygaśnie, anuluj zadanie:

```java
Future<?> future = executor.submit(task);
try {
    future.get(2, TimeUnit.MINUTES);
} catch (TimeoutException te) {
    future.cancel(true);
    System.err.println("Conversion timed out for " + htmlFilePath);
}
```

### 4. *Czy to działa na Windows i Linux?*

Tak — `ExecutorService` i Aspose.HTML są niezależne od platformy. Upewnij się tylko, że natywne biblioteki (jeśli istnieją) są dostępne poprzez `java.library.path`.

---

## Profesjonalne wskazówki i pułapki

- **Pro tip:** Ponownie używaj jednej instancji `Conversion`, jeśli biblioteka to wspiera; może to zmniejszyć narzut tworzenia obiektów.  
- **Uwaga:** Hard‑kodowane ścieżki z spacjami. Umieść je w cudzysłowach lub użyj obiektów `Path`, aby uniknąć `FileNotFoundException`.  
- **Logowanie:** Zamień `System.out.println` na odpowiedni framework logujący (SLF4J, Log4j) dla widoczności na poziomie produkcyjnym.  
- **Eleganckie zamknięcie:** Zawsze wywołuj `shutdown()` *nawet* jeśli wystąpi wyjątek; blok `try‑finally` zapewnia, że pula zostanie wyczyszczona.

---

## Zakończenie

Właśnie **konwertowaliśmy HTML do PDF** używając **przykładu java executorservice**, który wykorzystuje wzorzec **stałej puli wątków w Javie**. Kod pokazuje, jak **generować PDF z HTML**, obsługiwać błędy i prawidłowo **zatrzymać executor service** po zakończeniu całej pracy.

To podejście skaluje się dobrze — od trzech plików do tysięcy — przy zachowaniu responsywności aplikacji i przyjazności zasobów. Następnie możesz rozważyć:

- Dodanie **monitorowania postępu** za pomocą `CompletionService`.  
- Użycie **dynamicznych pul wątków** (`newCachedThreadPool`) dla nieprzewidywalnych obciążeń.  
- Integrację konwertera z **REST API**, aby inne usługi mogły wywoływać generowanie PDF na żądanie.

Wypróbuj to, dostosuj rozmiar puli i zobacz, jak szybciej stają się Twoje konwersje wsadowe. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}