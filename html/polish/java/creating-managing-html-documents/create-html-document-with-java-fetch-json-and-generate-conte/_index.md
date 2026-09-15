---
category: general
date: 2026-02-11
description: Utwórz dokument HTML w Javie przy użyciu Aspose.HTML. Dowiedz się, jak
  pobrać JSON w JavaScript, dodać element skryptu, wygenerować HTML z JSON oraz przekonwertować
  JSON na pre.
draft: false
keywords:
- create html document
- fetch json javascript
- add script element
- generate html from json
- convert json to pre
language: pl
og_description: Utwórz dokument HTML w Javie przy użyciu Aspose.HTML. Pobierz JSON
  w JavaScript, dodaj element script, wygeneruj HTML z JSON i przekształć JSON w pre
  — wszystko w jednym samouczku.
og_title: Tworzenie dokumentu HTML w Javie – pełny przewodnik
tags:
- Aspose.HTML
- Java
- Web Automation
title: Utwórz dokument HTML w Javie – pobierz JSON i wygeneruj treść
url: /pl/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz dokument HTML – Pełny samouczek Java

Czy kiedykolwiek potrzebowałeś **create HTML document** w locie, ale nie byłeś pewien, jak pobrać zdalne dane? Nie jesteś sam. W wielu projektach będziesz chciał pobrać JSON przy użyciu JavaScript, wstrzyknąć wynik do strony, a następnie zapisać ostateczny znacznik jako plik statyczny. Ten przewodnik pokazuje dokładnie, jak to zrobić przy użyciu Aspose.HTML dla Javy.

Przejdziemy przez każdy krok: od utworzenia pustego dokumentu, przez **fetch JSON JavaScript**, po **add script element**, a na końcu **generate HTML from JSON** i **convert JSON to pre**. Na końcu będziesz mieć gotowy do użycia plik `fetchResult.html`, który zawiera pobrane dane wyświetlone jako ładnie sformatowany JSON.

## Wymagania wstępne

- Java 17 lub nowszy (kod kompiluje się również z JDK 11+)
- Biblioteka Aspose.HTML for Java (dostępna przez Maven Central)
- Podstawowa znajomość HTML i asynchronicznego JavaScript
- IDE lub zwykła linia poleceń `javac`/`java`

Nie są wymagane dodatkowe frameworki — wszystko działa lokalnie.

## Krok 1: Skonfiguruj projekt i zaimportuj Aspose.HTML

Najpierw dodaj zależność Aspose.HTML do swojego `pom.xml` (lub pobierz plik JAR ręcznie).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

> **Pro tip:** Utrzymuj numer wersji aktualny; nowsze wydania naprawiają błędy i ulepszają silnik skryptów.

## Krok 2: **Create HTML Document** – pusty płótno

Zaczynamy od stworzenia pustego `HTMLDocument`. Traktuj go jak nową stronę, na którą później wstawimy nasz skrypt.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();
```

Dlaczego potrzebujemy obiektu dokumentu? `ScriptEngine` Aspose.HTML działa na DOM, a nie na surowym ciągu znaków. Tworząc odpowiedni dokument, dajemy silnikowi rzeczywiste środowisko do wykonania naszego **fetch JSON JavaScript**.

## Krok 3: Napisz fragment JavaScript – **Fetch JSON JavaScript** i **Convert JSON to pre**

Sedno samouczka znajduje się w tym wieloliniowym ciągu. Wykonuje asynchroniczny `fetch`, parsuje JSON, a następnie zapisuje element `<pre>` z ładnie sformatowanymi danymi.

```java
        // Step 3: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;
```

Zauważ komentarz *Convert JSON to <pre>* — to dokładnie to, co robi wywołanie `JSON.stringify(..., null, 2)`. Dodaje wcięcia, czyniąc wyjście czytelnym dla człowieka.

## Krok 4: **Add Script Element** do dokumentu

Teraz tworzymy znacznik `<script>`, wstawiamy nasz kod i dołączamy go do elementu body. To jest część **add script element**.

```java
        // Step 4: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);
```

Dlaczego dołączamy go do body? W prawdziwej przeglądarce skrypt uruchomiłby się natychmiast po parsowaniu. Dodając go do DOM, naśladujemy dokładnie to zachowanie, zapewniając, że asynchroniczny fetch wykona się, gdy później wywołamy silnik.

## Krok 5: Uruchom Script Engine – pozwól asynchronicznemu fetch zakończyć się

Aspose.HTML udostępnia `ScriptEngine`, który może wykonywać JavaScript oparty na DOM. Wywołujemy `run()` i czekamy, aż łańcuch obietnic się rozwiąże.

```java
        // Step 5: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();
```

Silnik blokuje się, dopóki wszystkie oczekujące zadania (nasz fetch) nie zostaną rozwiązane, co gwarantuje, że wygenerowany HTML już zawiera dane.

## Krok 6: **Generate HTML from JSON** – zapisz wynik

Na koniec zapisujemy dokument na dysku. Plik teraz zawiera blok `<pre>` z ładunkiem JSON.

```java
        // Step 6: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

Uruchomienie programu tworzy `fetchResult.html`. Otwórz go w dowolnej przeglądarce, a zobaczysz coś podobnego:

```html
<pre>{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}</pre>
```

To jest wynik **generate HTML from JSON**, którego szukałeś.

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do uruchomienia plik źródłowy. Skopiuj, wklej, dostosuj ścieżkę wyjścia i uruchom `java JsFetchExample`.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();

        // Step 2: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;

        // Step 3: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);

        // Step 4: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();

        // Step 5: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

## Oczekiwany wynik i weryfikacja

1. **Konsola:** Zobaczysz `HTML with fetched data saved.`  
2. **Plik (`fetchResult.html`):** Po otwarciu wyświetli JSON wewnątrz bloku `<pre>`, ładnie wcięty.  
3. **Walidacja:** Jeśli zobaczysz źródło strony, znajdziesz tylko element `<pre>` — żadne dodatkowe znaczniki skryptu nie pozostaną, ponieważ silnik już je wykonał.

## Częste pytania i przypadki brzegowe

| Pytanie | Odpowiedź |
|----------|--------|
| *Co jeśli API zwróci błąd?* | Umieść wywołanie `fetch` w bloku `try…catch` i zapisz komunikat o błędzie do elementu body zamiast JSON. |
| *Czy mogę pobrać wiele zasobów?* | Tak — po prostu łańcuchuj dodatkowe wywołania `await fetch(...)` lub użyj `Promise.all`. Końcowy `innerHTML` może połączyć kilka bloków `<pre>`. |
| *Czy muszę ustawiać nagłówki CORS?* | Ponieważ skrypt działa w sandboxie Aspose.HTML, respektuje politykę samego pochodzenia. Publiczny endpoint JSONPlaceholder już zezwala na żądania cross‑origin. |
| *Jak zmienić katalog wyjściowy w czasie działania?* | Przekaż ścieżkę jako argument wiersza poleceń (`args[0]`) i zamień sztywno zakodowany ciąg w `htmlDoc.save`. |
| *Czy istnieje sposób na osadzenie CSS dla stylizacji?* | Oczywiście. Utwórz element `<style>`, ustaw jego `textContent` na swój CSS i dołącz go do `<head>` przed uruchomieniem silnika. |

## Wskazówki dla produkcji

- **Cache the JSON** jeśli endpoint jest wolny; możesz zapisać pobrany ciąg do pliku i ponownie go używać.
- **Sanitize the data** przed wstrzyknięciem, szczególnie jeśli źródło nie jest zaufane. Używaj `JSON.stringify` bezpiecznie lub escapuj encje HTML.
- **Configure the ScriptEngine timeout** (`scriptEngine.setTimeout(5000)`) aby uniknąć zawieszania się przy nieodpowiadających usługach.

## Podsumowanie wizualne

![przykład create html document pokazujący wygenerowany HTML z JSON wewnątrz tagu pre](fetchResult.png "Zrzut ekranu wygenerowanego dokumentu HTML")

*Alt text:* *przykład create html document – wygenerowany plik HTML wyświetlający pobrany JSON wewnątrz elementu pre.*

## Zakończenie

Teraz wiesz, jak programowo **create HTML document** w Javie, **fetch JSON JavaScript**, **add script element**, **generate HTML from JSON** i **convert JSON to pre** dla czytelnego wyjścia. Cały przepływ działa offline, wymaga jedynie Aspose.HTML i generuje czysty plik statyczny, który możesz udostępnić gdziekolwiek.

Następnie spróbuj rozszerzyć skrypt, aby iterował po tablicy obiektów, dodał stylizację CSS lub zapisał wiele stron przy użyciu tej samej techniki. Możesz także zamienić URL `fetch` na własne API, aby przekształcić dynamiczne dane w statyczne migawki — idealne do SEO‑przyjaznego pre‑renderingu.

Miłego kodowania i zachęcam do dzielenia się swoimi eksperymentami w komentarzach!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}