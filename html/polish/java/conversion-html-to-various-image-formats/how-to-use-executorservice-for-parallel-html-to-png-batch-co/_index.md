---
category: general
date: 2026-02-21
description: Jak używać ExecutorService do szybkiego konwertowania HTML na PNG. Dowiedz
  się, jak konwertować pliki HTML w partiach przy użyciu równoległych zadań w Javie.
draft: false
keywords:
- how to use executorservice
- convert html to png
- how to run parallel tasks
- how to convert html to png
- batch convert html files
language: pl
og_description: Jak używać ExecutorService do konwertowania plików HTML na PNG w partiach.
  Przewodnik krok po kroku z kompletnym przykładem w Javie.
og_title: Jak używać ExecutorService do równoległej konwersji HTML na PNG
tags:
- Java
- concurrency
- Aspose.HTML
- image‑conversion
title: Jak używać ExecutorService do równoległej konwersji wsadowej HTML‑do‑PNG
url: /pl/java/conversion-html-to-various-image-formats/how-to-use-executorservice-for-parallel-html-to-png-batch-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać ExecutorService do równoległej konwersji wsadowej HTML‑to‑PNG

Zastanawiałeś się kiedyś **how to use ExecutorService**, gdy masz folder pełen stron HTML, które muszą zostać przekształcone w obrazy PNG? Nie jesteś jedyny — wielu programistów napotyka ten problem, gdy ich pipeline raportowania webowego zacinają się w jednowątkowej pętli konwersji.  

Dobre wieści? Dzięki kilku liniom Javy i potężnemu Aspose.HTML `Converter` możesz uruchomić pulę wątków pracowników, podać każdy plik HTML do konwertera i obserwować, jak obrazy pojawiają się równolegle. W tym samouczku dotkniemy również podstaw **convert html to png**, pokażemy, jak **run parallel tasks**, i dostarczymy gotowy do uruchomienia skrypt **batch convert html files**.

## Wymagania wstępne

- Java 17 lub nowsza (kod używa nowoczesnego API `java.nio.file`).  
- Biblioteka Aspose.HTML for Java w classpath. Możesz ją pobrać z Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

- Katalog zawierający pliki źródłowe `.html` oraz pusty folder wyjściowy.  
- Umiarkowana ilość RAM — każda konwersja działa w swoim własnym wątku, więc rozmiar puli powinien odpowiadać liczbie rdzeni CPU, które posiadasz.

> **Pro tip:** Jeśli pracujesz na maszynie z hyper‑threadingiem, `Runtime.getRuntime().availableProcessors()` zazwyczaj zwraca optymalną liczbę rdzeni.

## Krok 1 – Definiowanie ścieżek wejściowych i wyjściowych

Najpierw musimy powiedzieć Javie, gdzie znajdują się pliki HTML i gdzie mają trafić pliki PNG. Użycie obiektów `Path` zapewnia niezależność kodu od platformy.

```java
import java.nio.file.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Input folder containing .html files
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        // Output folder for the generated .png files
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");

        // Ensure the output folder exists
        Files.createDirectories(outputDir);
```

> **Dlaczego to ważne:** Tworzenie katalogu wyjściowego z wyprzedzeniem zapobiega `FileNotFoundException`, gdy pierwszy wątek pracownika próbuje zapisać plik.

## Krok 2 – Tworzenie puli wątków o stałym rozmiarze

Sednem **how to use ExecutorService** jest stworzenie puli dopasowanej do Twojego sprzętu. *Stała* pula gwarantuje, że nie uruchomimy więcej wątków niż możemy faktycznie wykonać.

```java
        // Create a thread pool sized to the number of available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());
```

> **Wyjaśnienie:** `ExecutorService` ukrywa niskopoziomowe zarządzanie wątkami. Używając `newFixedThreadPool`, pozwalamy JVM ponownie wykorzystywać wątki, co zmniejsza narzut związany z ciągłym tworzeniem i niszczeniem ich.

## Krok 3 – Dodawanie jednego zadania konwersji na każdy plik HTML

Teraz przechodzimy przez katalog wejściowy, wybieramy każdy plik `*.html` i przekazujemy go do puli. Każde zadanie to mała lambda wywołująca `Converter.convert`.

```java
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        // Build the output filename by swapping .html for .png
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();

                        // Perform the actual conversion
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }
```

### Co dzieje się pod maską?

1. **DirectoryStream** leniwie odczytuje nazwy plików, więc zużycie pamięci pozostaje niskie nawet przy tysiącach plików.  
2. Lambda przechwytuje `htmlFile` i `outputDir` — nie ma potrzeby osobnej klasy `Runnable`.  
3. `Converter.convert` jest wywołaniem blokującym, które odczytuje HTML, renderuje go i zapisuje PNG. Ponieważ każde wywołanie działa w swoim własnym wątku, wiele plików jest przetwarzanych jednocześnie — dokładnie tak, jak oczekujesz przy **run parallel tasks**.

## Krok 4 – Eleganckie zamykanie puli

Po zakolejkowaniu wszystkich zadań informujemy pulę, aby przestała przyjmować nowe zadania i czekała, aż wszystko się zakończy. Jeśli coś się zawiesi, limit czasu przerwie po godzinie, co jest hojnie wystarczające dla większości zadań wsadowych.

```java
        // No more tasks will be submitted
        pool.shutdown();

        // Wait up to 1 hour for all conversions to complete
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }

        System.out.println("All conversions completed.");
    }
}
```

> **Edge case:** Jeśli masz wyjątkowo duże pliki HTML, możesz chcieć zwiększyć limit czasu lub monitorować zużycie pamięci. Dodanie `pool.setRejectedExecutionHandler(new ThreadPoolExecutor.CallerRunsPolicy())` zmusza wątek wywołujący do wykonania nadmiarowych zadań, zapobiegając `RejectedExecutionException`.

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się cały program, gotowy do skopiowania i wklejenia do jednego pliku `ParallelBatchConversion.java`.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.*;
import java.util.concurrent.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Step 1: Define source and destination folders
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");
        Files.createDirectories(outputDir);

        // Step 2: Create a thread pool sized to the available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());

        // Step 3: Submit a conversion task for each HTML file found
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }

        // Step 4: Shut down the pool and wait for all conversions to finish
        pool.shutdown();
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }
        System.out.println("All conversions completed.");
    }
}
```

### Oczekiwany wynik

Uruchomienie programu wypisuje linię dla każdej udanej konwersji:

```
Converted: report1.html
Converted: dashboard.html
Converted: summary.html
All conversions completed.
```

Jeśli plik się nie uda, zobaczysz linię błędu z komunikatem wyjątku, co ułatwia debugowanie.

## Jak rozszerzyć ten wzorzec

- **Different image formats:** Zamień rozszerzenie `.png` na `.jpg` lub `.bmp` i odpowiednio dostosuj opcje konwersji Aspose.  
- **Dynamic thread count:** Dla obciążeń I/O‑bound możesz zwiększyć rozmiar puli (`availableProcessors() * 2`).  
- **Progress monitoring:** Zastąp `System.out.println` biblioteką wątkowo‑bezpiecznego paska postępu, taką jak `jline`, lub loguj do pliku.  
- **Error handling:** Zbierz nieudane ścieżki do `List<Path>` i spróbuj ponownie po zakończeniu głównej pętli.

## Najczęściej zadawane pytania

**Q: Czy to działa na Windows i Linux?**  
A: Tak. `java.nio.file` abstrahuje podległy system plików, więc ten sam kod działa niezmieniony na każdym systemie operacyjnym obsługującym Javę.

**Q: Co jeśli mam ponad 10 000 plików HTML?**  
A: Iterator `DirectoryStream` odczytuje wpisy leniwie, więc pamięć pozostaje niska. Upewnij się tylko, że dysk ma wystarczająco wolnego miejsca na wyjściowe pliki PNG.

**Q: Czy mogę ograniczyć pamięć używaną przez każdą konwersję?**  
A: Aspose.HTML pozwala skonfigurować silnik renderujący za pomocą `HtmlLoadOptions` i `ImageSaveOptions`. Możesz ustawić maksymalny rozmiar bitmapy lub włączyć renderowanie niskiej jakości, aby kontrolować zużycie RAM.

## Podsumowanie

Przeszliśmy przez **how to use ExecutorService**, aby **batch convert html files** do obrazów PNG, wyjaśniliśmy, dlaczego stała wielkość puli jest optymalna dla renderowania obciążonego CPU, i dostarczyliśmy kompletny, gotowy do skopiowania program w Javie. Postępując zgodnie z powyższymi krokami, zamienisz wolną, jednowątkową pętlę w szybką, skalowalną linię przetwarzania, zdolną obsłużyć tysiące plików jednym poleceniem.

Gotowy na kolejne wyzwanie? Spróbuj zamienić `Converter.convert` na eksport PDF Aspose, aby **convert html to pdf**, lub zintegrować tę logikę z mikrousługą Spring Boot przyjmującą żądania upload‑and‑convert. Główna idea — użycie `ExecutorService` do **run parallel tasks** — pozostaje taka sama i okaże się przydatna w niezliczonych scenariuszach przetwarzania wsadowego.

Szczęśliwego kodowania i niech Twoje wątki zawsze pozostają żywe! 

![how to use executorservice diagram](placeholder.png "Diagram illustrating the thread pool workflow for parallel HTML‑to‑PNG conversion")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}