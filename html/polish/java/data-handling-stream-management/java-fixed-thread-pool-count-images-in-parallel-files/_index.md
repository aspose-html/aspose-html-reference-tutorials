---
category: general
date: 2026-02-10
description: Dowiedz się, jak używać stałej puli wątków w Javie do liczenia obrazów
  w plikach HTML, uruchamiać zadania równocześnie w Javie oraz prawidłowo zamykać
  usługę wykonawczą.
draft: false
keywords:
- java fixed thread pool
- how to count images
- shutdown executor service
- java parallel file processing
- run tasks concurrently java
language: pl
og_description: Opanowano użycie stałej puli wątków w Javie do liczenia obrazów, przetwarzania
  plików równolegle i bezpiecznego wyłączania usługi wykonawczej.
og_title: 'java fixed thread pool: Zliczanie obrazów w równoległych plikach'
tags:
- Java
- Concurrency
- Aspose.HTML
title: 'java fixed thread pool: liczenie obrazów w równoległych plikach'
url: /pl/java/data-handling-stream-management/java-fixed-thread-pool-count-images-in-parallel-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java fixed thread pool – Samouczek równoległego zliczania obrazów

Zastanawiałeś się kiedyś, jak **java fixed thread pool** przejść przez dziesiątki plików HTML i szybko policzyć obrazy? Być może patrzyłeś na katalog stron, pomyślałeś „muszę wiedzieć, ile znaczników `<img>` ma każdy plik”, a potem zdałeś sobie sprawę, że jednowątkowa pętla zajęłaby wieczność.  

Dobrą wiadomością jest to, że nie musisz pisać własnego menedżera wątków ani zmagać się z niskopoziomowymi obiektami `Thread`. W tym przewodniku pokażemy Ci dokładnie **jak liczyć obrazy** używając *java fixed thread pool*, **run tasks concurrently java** oraz eleganckiego **shutdown executor service**, gdy praca zostanie zakończona.  

Omówimy wszystko, od konfiguracji puli, przygotowania listy plików, zgłaszania zadań równoległych, obsługi przypadków brzegowych, po weryfikację wyniku. Po zakończeniu będziesz mieć gotowy do uruchomienia program, który demonstruje **java parallel file processing** w czysty, łatwy do utrzymania sposób.  

## Prerequisites

Before we dive in, make sure you have:

- Java 17 lub nowsza (kod używa słowa kluczowego `var` dla zwięzłości, ale w razie potrzeby możesz użyć starszej wersji).
- Aspose.HTML for Java on your classpath – you can grab it from Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- Kilka plików HTML, które chcesz przeanalizować (samouczek zakłada, że znajdują się w `YOUR_DIRECTORY/`).
- IDE lub narzędzie budujące, z którym czujesz się komfortowo – IntelliJ IDEA, VS Code lub zwykły `javac` działa bez problemu.

That’s it. No extra servers, no Docker, just plain Java and a tiny third‑party library.

## Krok 1: Utwórz java fixed thread pool

*A java fixed thread pool* zapewnia ograniczony zestaw wątków roboczych, które są ponownie wykorzystywane dla każdego zgłoszonego zadania. Zapobiega to kosztowi ciągłego tworzenia nowych wątków i ogranicza poziom współbieżności, co jest kluczowe przy odczytywaniu plików z dysku.

```java
import java.util.concurrent.*;

public class ParallelImageCounter {
    // A pool of 4 threads – adjust based on your CPU cores and I/O profile
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);
}
```

**Dlaczego 4?** Jeśli masz laptopa z czterordzeniowym procesorem, cztery wątki utrzymują każdy rdzeń zajęty bez nadmiernego obciążenia. Na serwerze z większą liczbą rdzeni możesz zwiększyć tę liczbę, ale pamiętaj, że każdy wątek otwiera uchwyt pliku, więc zbyt wiele może wyczerpać limity systemu operacyjnego.

## Krok 2: Wypisz pliki HTML, które chcesz przeanalizować

Następny element **java parallel file processing** to po prostu zbudowanie tablicy (lub `List`) ścieżek do plików. W prawdziwym projekcie możesz przeszukiwać katalog rekurencyjnie, filtrować po rozszerzeniu lub odczytywać ścieżki z bazy danych. Oto proste podejście:

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/a.html",
    "YOUR_DIRECTORY/b.html",
    "YOUR_DIRECTORY/c.html",
    "YOUR_DIRECTORY/d.html"
};
```

Jeśli potrzebujesz obsłużyć dynamiczny zestaw, zamień statyczną tablicę na coś takiego:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
String[] htmlFiles = Files.list(dir)
                         .filter(p -> p.toString().endsWith(".html"))
                         .map(Path::toString)
                         .toArray(String[]::new);
```

Ten fragment pokazuje **java parallel file processing** dla dowolnej liczby plików bez zmiany reszty kodu.

## Krok 3: Zgłoś zadania do **run tasks concurrently java**

Teraz przychodzi serce samouczka – **run tasks concurrently java** poprzez zgłoszenie lambdy dla każdego pliku. Każde zadanie ładuje dokument HTML przy użyciu Aspose.HTML, wyszukuje wszystkie elementy `<img>` i wypisuje ich liczbę.

```java
import com.aspose.html.HTMLDocument;

public static void main(String[] args) throws InterruptedException {
    for (String filePath : htmlFiles) {
        executor.submit(() -> {
            // Load the document – Aspose.HTML does the heavy lifting
            HTMLDocument document = new HTMLDocument(filePath);
            // querySelectorAll returns a NodeList; its length is the image count
            int imageCount = document.querySelectorAll("img").length;
            System.out.println(filePath + " contains " + imageCount + " images.");
        });
    }

    // Step 4 is next – gracefully shut down the pool
    shutdownAndAwaitTermination();
}
```

**Dlaczego używać lambdy?** Utrzymuje kod zwięzły i unika tworzenia osobnej klasy `Runnable`. Lambda automatycznie przechwytuje `filePath`, więc każde zadanie działa na swoim własnym pliku.

### Jak **count images** efektywnie

Aspose.HTML parsuje plik raz, buduje DOM, a następnie `querySelectorAll("img")` działa w O(n), gdzie *n* to liczba węzłów. Dla większości stron HTML jest to pomijalne. Jeśli potrzebowałbyś szybszego podejścia tylko strumieniowego (np. dla plików o rozmiarze gigabajtów), możesz przejść na parser SAX, ale poświęci to prostotę, do której dążymy.

## Krok 4: Poprawnie **shutdown executor service**

Nigdy nie zapominaj zamknąć puli, w przeciwnym razie Twoja JVM będzie działać w nieskończoność. Poniższy wzorzec to zalecany sposób na **shutdown executor service** podczas oczekiwania na zakończenie wszystkich zadań:

```java
private static void shutdownAndAwaitTermination() {
    executor.shutdown(); // Disable new tasks from being submitted
    try {
        // Wait a while for existing tasks to terminate
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            executor.shutdownNow(); // Cancel currently executing tasks
            // Wait a second for tasks to respond to being cancelled
            if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                System.err.println("Pool did not terminate");
        }
    } catch (InterruptedException ie) {
        // (Re-)Cancel if current thread also interrupted
        executor.shutdownNow();
        // Preserve interrupt status
        Thread.currentThread().interrupt();
    }
}
```

**Co jeśli zadanie się zawiesi?** Wywołanie `shutdownNow()` próbuje przerwać działające wątki. Jeśli Twoja logika zliczania obrazów respektuje przerwania (co Aspose.HTML nie blokuje przy I/O), pula zakończy się czysto. Ten wzorzec jest złotym standardem dla każdego użycia **java fixed thread pool**.

## Krok 5: Zweryfikuj wynik

Uruchom program ze swojego IDE lub z wiersza poleceń:

```bash
javac -cp "path/to/aspose-html.jar" ParallelImageCounter.java
java -cp ".:path/to/aspose-html.jar" ParallelImageCounter
```

Typowy wynik wygląda tak:

```
YOUR_DIRECTORY/a.html contains 5 images.
YOUR_DIRECTORY/b.html contains 0 images.
YOUR_DIRECTORY/c.html contains 12 images.
YOUR_DIRECTORY/d.html contains 3 images.
```

Jeśli widzisz liczniki wypisane w dowolnej kolejności, jest to oczekiwane – wątki kończą w różnym czasie. Ważne jest, aby każdy plik został uwzględniony i program zakończył się czysto po sekwencji zamknięcia.

## Pełny działający przykład (gotowy do kopiowania i wklejania)

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelImageCounter {
    // 1️⃣ Fixed thread pool – change size based on your hardware
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);

    public static void main(String[] args) throws InterruptedException {
        // 2️⃣ List of HTML files – replace with your own directory
        String[] htmlFiles = {
            "YOUR_DIRECTORY/a.html",
            "YOUR_DIRECTORY/b.html",
            "YOUR_DIRECTORY/c.html",
            "YOUR_DIRECTORY/d.html"
        };

        // 3️⃣ Submit a counting task for each file
        for (String filePath : htmlFiles) {
            executor.submit(() -> {
                HTMLDocument document = new HTMLDocument(filePath);
                int imageCount = document.querySelectorAll("img").length;
                System.out.println(filePath + " contains " + imageCount + " images.");
            });
        }

        // 4️⃣ Gracefully shut down the pool
        shutdownAndAwaitTermination();
    }

    // 5️⃣ Helper method to cleanly stop the executor
    private static void shutdownAndAwaitTermination() {
        executor.shutdown(); // Disable new tasks
        try {
            if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
                executor.shutdownNow(); // Cancel currently executing tasks
                if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                    System.err.println("Pool did not terminate");
            }
        } catch (InterruptedException ie) {
            executor.shutdownNow();
            Thread.currentThread().interrupt();
        }
    }
}
```

### Oczekiwany wynik

Uruchomienie fragmentu wypisuje każdą ścieżkę pliku wraz z liczbą znaczników `<img>`, które zawiera, a następnie JVM kończy działanie. Brak zalegających wątków, brak wycieków pamięci.

## Częste pułapki i wskazówki profesjonalne

- **Pułapka:** Używanie `newCachedThreadPool()` zamiast puli *fixed*. Tworzy to nieograniczoną liczbę wątków, co może wyczerpać deskryptory plików przy dużych partiach. Trzymaj się `newFixedThreadPool`.
- **Wskazówka:** Jeśli Twoje pliki HTML są ogromne, rozważ zwiększenie rozmiaru sterty (`-Xmx2g`) lub przejście na parser strumieniowy. Dla większości stron marketingowych domyślna sterta jest wystarczająca.
- **Pułapka:** Zapomnienie wywołania `shutdown()` – aplikacja zawiesi się po wypisaniu wyników. Metoda `shutdownAndAwaitTermination` powyżej obsługuje to solidnie.
- **Wskazówka:** Zaloguj czas rozpoczęcia i zakończenia każdego zadania, jeśli potrzebujesz metryk wydajności. Proste `System.nanoTime()` przed i po konstrukcji `HTMLDocument` pokaże, jak długo trwało parsowanie.
- **Pułapka:** Sztywne kodowanie liczby wątków. Użyj `Runtime.getRuntime().availableProcessors()`, aby wybrać rozsądny domyślny parametr:

```java
int cores = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(cores);
```

## Powiązane tematy, które możesz zbadać dalej

- **run tasks concurrently java** z `CompletableFuture` dla bardziej wyrazistych potoków.
- Trwałe przechowywanie liczby obrazów w bazie danych dla pulpitów analitycznych.
- Używanie **java parallel file processing** z API `java.nio.file.Files.walk` w połączeniu ze strumieniami.
- Implementacja własnego `ThreadFactory`, aby nadawać wątkom znaczące nazwy (pomaga w debugowaniu).

## Zakończenie

Właśnie przeszliśmy przez kompletny, samodzielny przykład, który pokazuje, jak **java fixed thread pool** może być wykorzystany do **jak liczyć obrazy** w wielu plikach HTML, jednocześnie demonstrując właściwy sposób **shutdown executor service**. Wzorzec skaluje się dobrze — zamień tablicę plików na dynamiczną listę, zwiększ rozmiar puli i masz solidne rozwiązanie dla każdego obciążenia **java parallel file processing**.  

Wypróbuj go, zmodyfikuj liczbę wątków i ewentualnie dodaj eksport wyników do CSV. Nie ma granic, gdy połączysz solidne podstawy współbieżności z przydatną biblioteką taką jak Aspose.HTML. Szczęśliwego kodowania!  

![java fixed thread pool diagram](image.png){alt="diagram java fixed thread pool"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}