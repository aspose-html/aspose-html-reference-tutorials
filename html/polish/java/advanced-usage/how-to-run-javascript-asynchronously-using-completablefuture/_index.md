---
category: general
date: 2026-02-16
description: Dowiedz się, jak uruchamiać JavaScript w Javie przy użyciu CompletableFuture,
  opóźniać JS i oceniać kod asynchroniczny. Kompletny przewodnik krok po kroku poświęcony
  asynchronicznej ocenie JavaScript.
draft: false
keywords:
- how to run javascript
- how to use completablefuture
- how to delay js
- how to evaluate async
- evaluate javascript asynchronously
language: pl
og_description: Opanuj, jak uruchamiać JavaScript z Javy, opóźniać JS i oceniać kod
  asynchroniczny przy użyciu CompletableFuture w tym kompletnym poradniku.
og_title: Jak uruchomić JavaScript asynchronicznie przy użyciu CompletableFuture
tags:
- javascript
- java
- asynchronous
- completablefuture
title: Jak uruchomić JavaScript asynchronicznie przy użyciu CompletableFuture
url: /pl/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uruchomić JavaScript asynchronicznie przy użyciu CompletableFuture

Zastanawiałeś się kiedyś, **jak uruchomić JavaScript** wewnątrz aplikacji Java bez blokowania głównego wątku? Być może potrzebujesz wywołać mały skrypt pobierający dane, ale nie chcesz, aby interfejs użytkownika zamarzał. Dobra wiadomość jest taka, że nowoczesne biblioteki Java pozwalają oceniać JavaScript **asynchronicznie**, a nawet możesz wprowadzić opóźnienia tak, jak w przeglądarce. W tym przewodniku pokażemy kompletny, gotowy do uruchomienia przykład, który wykorzystuje `ScriptEngine` z Aspose HTML razem z `CompletableFuture`, aby **jak uruchomić javascript** i otrzymać wynik z powrotem w Javie.

Omówimy także **jak używać CompletableFuture**, **jak opóźnić JS**, oraz **jak ocenić kod async**, abyś mógł **oceniać JavaScript asynchronicznie** w dowolnym projekcie Java. Po zakończeniu będziesz mieć solidny szablon, który możesz kopiować‑wklejać, modyfikować i wbudowywać w większe systemy.

---

## Czego się nauczysz

- Skonfigurować `ScriptEngine` w Javie, który potrafi wykonywać nowoczesny JavaScript ES2022.  
- Napisać funkcję `async` zawierającą opóźnienie (`jak opóźnić js`).  
- Wywołać `evaluateAsync` i otrzymać `CompletableFuture` (`jak używać completablefuture`).  
- Pobrać wynik po rozwiązaniu obietnicy JavaScript (`jak ocenić async`).  
- Wskazówki dotyczące obsługi błędów, zarządzania wątkami i rozszerzania wzorca.

Nie są wymagane żadne zewnętrzne narzędzia budujące poza plikiem JAR Aspose HTML for Java, który możesz po prostu dodać do classpath. Zanurzmy się.

---

## Krok 1: Jak uruchomić JavaScript – Inicjalizacja silnika skryptowego

Na początek. Biblioteka Aspose HTML udostępnia klasę `ScriptEngine`, która może wykonywać kod JavaScript. Pomyśl o niej jak o małym silniku Chromium działającym wewnątrz Twojej JVM.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Dlaczego to ważne:** Tworząc instancję `ScriptEngine`, otrzymujemy środowisko sandbox, w którym nowoczesny JavaScript (w tym `async/await`) działa od razu. Nie musisz uruchamiać zewnętrznego procesu Node.

---

## Krok 2: Jak opóźnić JS – Napisz funkcję async z timerem opartym na Promise

`setTimeout` w JavaScript to klasyczny sposób na wstrzymanie wykonania. W nowoczesnym kodzie opakowujemy go w `Promise`, aby móc `await`‑ować. Dokładnie to zrobimy w łańcuchu skryptu.

```java
        // ES2022 async function that resolves after a short delay
        String asyncScript = """
            async function fetchMessage() {
                const delay = ms => new Promise(r => setTimeout(r, ms));
                await delay(500); // 500 ms pause
                return "Hello from async JS!";
            }
            fetchMessage(); // Return the promise to Java
            """;
```

> **Jak opóźnić js:** Pomocnicza funkcja `delay` tworzy obietnicę, która rozwiązuje się po `ms` milisekundach. Dzięki `await`‑owi funkcja pauzuje bez blokowania wątku Java.

---

## Krok 3: Jak ocenić async – Uruchom skrypt i uzyskaj CompletableFuture

Zamiast synchronicznej metody `evaluate`, wywołujemy `evaluateAsync`. Natychmiast zwraca ona `CompletableFuture<Object>`, które zostanie zakończone, gdy obietnica JavaScript się rozwiąże.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **Jak ocenić async:** `evaluateAsync` łączy pętlę zdarzeń JavaScript z `CompletableFuture` w Javie. To jest sedno **oceniania javascript asynchronicznie**.

---

## Krok 4: Jak używać CompletableFuture – Dołącz callback i zablokuj wątek dla demonstracji

Teraz dołączamy callback przy pomocy `thenAccept`, aby wypisać wynik, i blokujemy główny wątek na tyle długo, aby demo mogło się zakończyć.

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **Dlaczego wywołujemy `get()`:** W prawdziwej aplikacji prawdopodobnie kontynuowałbyś przetwarzanie gdzie indziej. Tutaj blokujemy, aby przykład był samodzielny.

---

## Przegląd wizualny

![Diagram pokazujący, jak uruchomić JavaScript asynchronicznie przy użyciu CompletableFuture](https://example.com/diagram.png "Jak uruchomić JavaScript – przepływ async")

*Alt text:* **Diagram pokazujący, jak uruchomić JavaScript asynchronicznie przy użyciu CompletableFuture** – obraz ilustruje przepływ od Javy do silnika skryptowego, asynchroniczne opóźnienie i zakończenie CompletableFuture.

---

## Typowe pułapki i dobre praktyki (Jak ocenić async bezpiecznie)

| Pułapka | Co się dzieje | Rozwiązanie |
|---------|---------------|-------------|
| Zapomnienie zwrócenia obietnicy | `evaluateAsync` rozwiązuje się od razu z `undefined` | Upewnij się, że ostatnia linia skryptu to obietnica (`fetchMessage();`) |
| Użycie blokującego `Thread.sleep` w JS | Blokuje pętlę zdarzeń silnika, niszczy asynchroniczność | Użyj wzorca `delay` opartego na Promise (jak pokazano) |
| Ignorowanie wyjątków | Future kończy się wyjątkowo, ale go nie widzisz | Dołącz `.exceptionally(e -> { e.printStackTrace(); return null; })` |
| Nie zamknięcie silnika | Wycieki zasobów w aplikacjach długotrwałych | Wywołaj `scriptEngine.dispose()` po zakończeniu |

---

## Rozszerzanie wzorca (Jak używać CompletableFuture w prawdziwych projektach)

Możesz łączyć wiele asynchronicznych wywołań JavaScript, łączyć je z innymi futures lub uruchamiać je na własnym `Executor`. Oto szybki szkic:

```java
ExecutorService jsPool = Executors.newFixedThreadPool(4);
CompletableFuture<Object> future = scriptEngine.evaluateAsync(asyncScript, jsPool)
    .thenApply(result -> {
        // Post‑process the JS string result
        return ((String) result).toUpperCase();
    })
    .exceptionally(ex -> {
        System.err.println("JS error: " + ex);
        return "fallback";
    });
```

> **Jak używać CompletableFuture:** Przekazując `Executor`, kontrolujesz pulę wątków, utrzymując UI responsywnym i unikając wyczerpania wątków.

---

## Oczekiwany wynik

Uruchom klasę `JsAsyncDemo`, a zobaczysz:

```
JS result: Hello from async JS!
```

Pauza 500 ms nie jest widoczna w konsoli, ale możesz dodać znaczniki czasu, aby zweryfikować opóźnienie, jeśli chcesz.

---

## Podsumowanie – Jak uruchomić JavaScript z CompletableFuture

Zaczęliśmy od **jak uruchomić javascript** w Javie, napisaliśmy funkcję `async`, która **jak opóźnić js**, uruchomiliśmy ją przy pomocy `evaluateAsync` (**jak ocenić async**) i przechwyciliśmy wynik używając **jak używać completablefuture**. Cały przepływ demonstruje **ocenianie javascript asynchronicznie** w czystym, wielokrotnego użytku wzorcu.

---

## Co dalej?

- **Integracja z klientami HTTP:** Pobieraj dane z endpointu REST wewnątrz asynchronicznego JS i zwracaj je do Javy.  
- **Wiele skryptów:** Łącz kilka wywołań `evaluateAsync` w złożone pipeline’y.  
- **Zamiana silnika:** Ten sam wzorzec działa z Nashorn, GraalVM lub innymi środowiskami JavaScript – wystarczy podmienić `ScriptEngine`.

Śmiało eksperymentuj z dłuższymi opóźnieniami, skryptami rzucającymi błędy lub nawet modułami WebAssembly. Nie ma granic, gdy połączysz prymitywy współbieżności Javy z nowoczesnym JavaScriptem.

---

### Masz pytania?

Jeśli coś nie jest jasne – może zastanawiasz się, jak obsłużyć odrzuconą obietnicę lub jak przekazać zmienne z Javy do skryptu – zostaw komentarz poniżej. Powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}