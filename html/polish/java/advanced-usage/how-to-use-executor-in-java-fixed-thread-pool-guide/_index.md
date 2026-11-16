---
category: general
date: 2026-05-28
description: jak używać executor w Javie z stałą pulą wątków, wyodrębniać tekst z
  HTML i przyspieszyć przetwarzanie – kompletny przykład puli wątków w Javie.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: pl
og_description: jak używać executor w Javie z stałą pulą wątków. Poznaj kompletny
  przykład puli wątków w Javie, który wydajnie wyodrębnia tekst z plików HTML.
og_title: Jak używać Executor w Javie – Przewodnik po stałej puli wątków
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: how to use executor in Java with a fixed thread pool, extract text
    from HTML and speed up processing – a complete java thread pool example.
  headline: How to Use Executor in Java – Fixed Thread Pool Guide
  type: TechArticle
tags:
- Java
- Concurrency
- HTML Parsing
title: Jak używać Executor w Javie – Przewodnik po stałej puli wątków
url: /pl/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać Executor w Javie – Przewodnik po stałej puli wątków

Zastanawiałeś się kiedyś **jak używać executor**, aby uruchamiać wiele zadań jednocześnie bez wyczerpania pamięci? Nie jesteś sam. W wielu rzeczywistych aplikacjach będziesz musiał przeszukać folder z plikami HTML, wyciągnąć tekst z sekcji body i zrobić to szybko — dokładnie taki scenariusz rozwiązuje ten tutorial.

Przejdziemy przez implementację **fixed thread pool java**, która wyodrębnia tekst z HTML, wypisuje liczbę znaków w każdym pliku i zamyka się w sposób czysty. Po zakończeniu będziesz mieć samodzielny **java thread pool example**, który możesz wstawić do dowolnego projektu, oraz kilka wskazówek dotyczących dostosowywania rozmiaru puli i obsługi przypadków brzegowych.

> **Czego będziesz potrzebować**  
> * Java 17 (lub dowolny nowoczesny JDK)  
> * Mała biblioteka do parsowania HTML – użyjemy *jsoup*, ponieważ jest sprawdzona w boju i nie wymaga konfiguracji.  
> * Kilka przykładowych plików *.html* w wybranym przez Ciebie katalogu.

---

## Jak używać Executor z stałą pulą wątków

Sercem każdego programu Java intensywnie korzystającego z współbieżności jest `ExecutorService`. Tworząc **fixed thread pool**, informujemy JVM, aby utrzymywała dokładnie N wątków roboczych, co zapobiega narzutom związanym z tworzeniem wątków i ogranicza zużycie zasobów.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Dlaczego to ma znaczenie:*  
Gdybyś uruchamiał nowy `Thread` dla każdego pliku HTML, system operacyjny musiałby planować dziesiątki wątków na przeciętnym laptopie, co prowadziłoby do nadmiernego przełączania kontekstów. Stała pula ponownie wykorzystuje te same cztery wątki, zapewniając przewidywalne użycie CPU.

---

## Definiowanie plików HTML do przetworzenia – Fixed Thread Pool Java

Następnie wymieniamy pliki, które chcemy przekazać do puli. W prawdziwej aplikacji prawdopodobnie przeszukasz drzewo katalogów; tutaj pozostajemy przy prostym rozwiązaniu.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Wskazówka:* `List.of` zwraca niezmienną listę, którą można bezpiecznie udostępniać pomiędzy wątkami bez dodatkowej synchronizacji.

---

## Przesyłanie osobnego zadania dla każdego pliku HTML

Teraz przekazujemy każdą ścieżkę do executora. Lambda, którą przesyłamy, będzie działać **równolegle** na jednym z czterech wątków roboczych.

```java
// Step 3: Dispatch a parsing job for every file
for (String htmlFilePath : htmlFilePaths) {
    executor.submit(() -> {
        // Each lambda runs on a thread from the pool
        try {
            // Step 4: Open the document, extract its text, and display the length
            String text = extractBodyText(htmlFilePath);
            System.out.println(htmlFilePath + " → " + text.length() + " chars");
        } catch (IOException e) {
            System.err.println("Failed to read " + htmlFilePath);
            e.printStackTrace();
        }
    });
}
```

**Dlaczego opakowujemy logikę w metodę** (`extractBodyText`) stanie się jasne w następnym rozdziale — utrzymuje to lambdę schludną i pozwala nam ponownie używać kodu ekstrakcji w innych miejscach.

---

## Wyodrębnianie tekstu z HTML – Główna logika

Oto wielokrotnego użytku pomocnik, który faktycznie **wyodrębnia tekst z html** przy użyciu Jsoup. Otwiera plik, parsuje DOM i zwraca czysty tekst z sekcji body.

```java
/**
 * Reads an HTML file and returns the plain text inside the <body>.
 *
 * @param path absolute or relative path to the .html file
 * @return body text without tags
 * @throws IOException if the file cannot be read
 */
private static String extractBodyText(String path) throws IOException {
    // Jsoup parses the file into a Document object.
    org.jsoup.nodes.Document doc = org.jsoup.Jsoup.parse(new java.io.File(path), "UTF-8");
    // getBody() gives us the <body> element; text() strips all tags.
    return doc.body().text();
}
```

*Dlaczego Jsoup?* Jest lekki, radzi sobie z niepoprawnym markupem w sposób elegancki i nie wymaga pełnego silnika przeglądarki. Metoda rzuca `IOException`, dzięki czemu wywołujący może zdecydować, jak logować lub odzyskać — idealne w scenariuszu puli wątków, gdzie nie chcesz, aby pojedynczy wadliwy plik zakończył cały executor.

---

## Eleganckie zamykanie executor – Tworzenie stałej puli wątków

Po przesłaniu wszystkich zadań musimy poinformować pulę, aby przestała przyjmować nowe zadania i dokończyła te już w kolejce.

```java
// Step 5: Initiate an orderly shutdown once all tasks are queued
executor.shutdown();
try {
    // Wait up to 30 seconds for all tasks to finish
    if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
        System.err.println("Timed out waiting for tasks; forcing shutdown.");
        executor.shutdownNow();
    }
} catch (InterruptedException ie) {
    // Preserve interrupt status and force shutdown
    Thread.currentThread().interrupt();
    executor.shutdownNow();
}
```

*Wyjaśnienie:* `shutdown()` zapobiega nowym zgłoszeniom, natomiast `awaitTermination` blokuje aż wszystkie zadania parsujące zakończą się (lub upłynie limit czasu). Jeśli coś się zawiesi, `shutdownNow()` próbuje anulować uruchomione zadania. Ten wzorzec jest zalecanym sposobem na **create fixed thread pool** w bezpieczny sposób.

---

## Pełny, uruchamialny przykład

Łącząc wszystko razem, oto pojedynczy plik, który możesz skompilować i uruchomić. Zawiera niezbędne importy, metodę `main` oraz pomocnika opisanego powyżej.

```java
import java.io.IOException;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

/**
 * Demonstrates how to use executor with a fixed thread pool to
 * extract text from multiple HTML files concurrently.
 */
public class HtmlThreadPoolDemo {

    public static void main(String[] args) {
        // 1️⃣ Build a fixed‑size pool (adjust the size for your hardware)
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ Define the files we want to process
        List<String> htmlFilePaths = List.of(
                "YOUR_DIRECTORY/a.html",
                "YOUR_DIRECTORY/b.html",
                "YOUR_DIRECTORY/c.html",
                "YOUR_DIRECTORY/d.html"
        );

        // 3️⃣ Submit a parsing task for each file
        for (String htmlFilePath : htmlFilePaths) {
            executor.submit(() -> {
                try {
                    String text = extractBodyText(htmlFilePath);
                    System.out.println(htmlFilePath + " → " + text.length() + " chars");
                } catch (IOException e) {
                    System.err.println("Error processing " + htmlFilePath);
                    e.printStackTrace();
                }
            });
        }

        // 5️⃣ Shut down the pool cleanly
        executor.shutdown();
        try {
            if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("Tasks took too long; forcing shutdown.");
                executor.shutdownNow();
            }
        } catch (InterruptedException ie) {
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }

    /**
     * Reads an HTML file and returns the plain text inside the <body>.
     *
     * @param path path to the .html file
     * @return body text without markup
     * @throws IOException if file cannot be read
     */
    private static String extractBodyText(String path) throws IOException {
        Document doc = Jsoup.parse(new java.io.File(path), "UTF-8");
        return doc.body().text();
    }
}
```

**Oczekiwany wynik** (zakładając, że każdy plik zawiera około 1 200 znaków tekstu w sekcji body):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

Jeśli którykolwiek plik będzie brakował lub będzie niepoprawny, zobaczysz wydrukowany stos wywołań w `stderr`, ale pozostałe zadania będą kontynuowane bez wpływu — dokładnie to, co powinien robić dobrze zachowujący się **java thread pool example**.

---

## Częste pytania i przypadki brzegowe

| Pytanie | Odpowiedź |
|----------|--------|
| *Co jeśli mam więcej niż cztery pliki?* | Pula umieści dodatkowe zadania w kolejce i uruchomi je, gdy tylko wątek stanie się wolny. Nie potrzeba dodatkowego kodu. |
| *Czy powinienem używać `newCachedThreadPool` zamiast?* | `newCachedThreadPool` tworzy wątki na żądanie i może rosnąć nieograniczenie, co jest ryzykowne przy zadaniach intensywnych I/O. **fixed thread pool** zapewnia przewidywalne użycie pamięci i CPU. |
| *Jak zmienić rozmiar puli w zależności od rdzeni CPU?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` to powszechny wzorzec. |
| *Co jeśli parsowanie nie powiedzie się dla jednego pliku?* | `catch (IOException e)` wewnątrz lambdy izoluje błąd, loguje go i pozwala reszcie puli kontynuować pracę. |
| *Czy mogę zwrócić wyodrębniony tekst do wywołującego?* | Tak — użyj `Future<String>` zamiast `submit(Runnable)`. Kod wyglądałby tak: `Future<String> f = executor.submit(() -> extractBodyText(path));` i później `String result = f.get();`. |

---

## Zakończenie

Omówiliśmy **jak używać executor**, aby uruchomić **fixed thread pool java**, który przetwarza kolekcję plików HTML równolegle, wyodrębnia ich tekst z sekcji body i raportuje liczbę znaków. Pełny **java thread pool example** demonstruje właściwe zarządzanie zasobami, obsługę błędów i wielokrotnego użytku metodę ekstrakcji.

Kolejne kroki? Spróbuj zamienić implementację `extractBodyText` na bardziej zaawansowany scraper, poeksperymentuj z większym rozmiarem puli lub przekazuj wyniki do bazy danych. Możesz także zbadać `CompletionService`, aby pobierać wyniki natychmiast po ich gotowości, co jest przydatne, gdy rozmiary plików znacznie się różnią.

Śmiało modyfikuj ścieżkę katalogu, dodawaj więcej plików lub integruj ten fragment kodu w większym frameworku do crawlowania. Podstawowy wzorzec — tworzyć pulę, przesyłać niezależne zadania i elegancko zamykać — pozostaje taki sam, niezależnie od tego, jak skomplikowane staje się obciążenie.

Szczęśliwego kodowania i niech Twoje wątki zawsze żyją (aż je zamkniesz, oczywiście)!

## Powiązane tutoriale

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Use Aspose.HTML for Java - Mastering HTML5 Canvas Rendering](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}