---
category: general
date: 2026-03-26
description: Przykład top‑level await pokazujący await delay w JavaScript, klasę inkrementującą
  licznik oraz publiczne pola klasy w JavaScript w demonstracji na żywo.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: pl
og_description: przykład top‑level await, który demonstruje await delay w JavaScript,
  klasę inkrementującą licznik oraz publiczne pola klasy w JavaScript w zwięzłym tutorialu.
og_title: przykład top‑level await – użycie await delay w JavaScript
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: Przykład top‑level await – użycie await delay w JavaScript
url: /pl/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# przykład top level await – używanie await delay w JavaScript

Zastanawiałeś się kiedyś, jak wstrzymać wykonywanie modułu bez owijania wszystkiego w async IIFE? To właśnie to, co pozwala zrobić **top level await example**. W tym tutorialu przejdziemy przez małą stronę internetową, która używa `await delay javascript` do odroczenia pracy, a następnie tworzy `increment counter class`, które wykorzystuje **public class fields javascript**. Na końcu będziesz mieć kompletny, gotowy do skopiowania fragment kodu, który działa w każdej nowoczesnej przeglądarce.

Omówimy wszystko, od definiowania klasy z polem publicznym po podłączenie prostego pomocnika opóźnienia opartego na obietnicach. Bez zewnętrznych bibliotek, bez kroku budowania — tylko czysty HTML, `<script type="module">` i najnowsze funkcje ECMAScript. Jeśli już czujesz się pewnie w funkcjach async, zobaczysz, dlaczego top‑level await jest naturalnym rozszerzeniem. Jeśli jesteś nowy w składni **javascript class public field**, nie martw się — wyjaśniamy, dlaczego każda linijka jest taka, jaka jest.

## Czego się nauczysz

- Jak działa **top level await example** wewnątrz skryptu modułowego.
- Wzorzec pomocnika `await delay javascript`, który naśladuje `setTimeout` przy użyciu obietnic.
- Jak napisać **increment counter class**, które używa pola publicznego (`count`) oraz statycznego bloku inicjalizacyjnego.
- Oczekiwany wynik w konsoli i jak zweryfikować, że statyczny blok uruchamia się przed resztą skryptu.
- Porady dotyczące rozwiązywania typowych problemów, takich jak starsze przeglądarki nieobsługujące top‑level await.

> **Pro tip:** Nowoczesne przeglądarki (Chrome 106+, Firefox 102+, Edge 106+) już obsługują top‑level await. Jeśli musisz wspierać starsze środowiska, rozważ bundling przy użyciu narzędzia takiego jak Vite lub Babel.

## Step 1 – Define a Class with a Public Field and a Static Block

Pierwszy element naszego demo to klasa przechowująca licznik numeryczny. Zwróć uwagę na linię `count = 0;` — to składnia **public class fields javascript** wprowadzona w ES2022. Tworzy ona własność instancji bez potrzeby definiowania konstruktora.

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**Dlaczego statyczny blok?** Pozwala uruchomić jednorazową logikę inicjalizacyjną (np. logowanie) w momencie parsowania modułu, *przed* uruchomieniem jakiegokolwiek top‑level await. Gwarantuje to, że komunikat pojawi się jako pierwszy w konsoli, dowodząc, że klasa została oceniona wcześnie.

## Step 2 – Create an `await delay javascript` Helper

Następnie potrzebujemy małej funkcji opóźnienia opartej na obietnicach. To w zasadzie opakowanie wokół `setTimeout`, ale zwracanie obietnicy sprawia, że można ją `await`‑ować.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**Edge case:** Jeśli `ms` jest ujemne lub nie jest liczbą, `setTimeout` traktuje je jako `0`. Można dodać walidację, ale w demo jednowierszowy zapis utrzymuje kod czytelnym.

## Step 3 – Use Top‑Level Await to Pause Execution

Teraz przychodzi gwiazda programu: top‑level await. Ponieważ nasz skrypt jest modułem (`type="module"`), możemy umieścić `await` bezpośrednio w najwyższym zasięgu. To wstrzymuje moduł, dopóki obietnica nie zostanie rozwiązana, pozwalając kontrolować kolejność efektów ubocznych.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**Common question:** „Czy mogę używać top‑level await w normalnym znaczniku `<script>`?” Nie — obsługują go wyłącznie skrypty modułowe. Jeśli zapomnisz o `type="module"`, otrzymasz błąd składni.

## Step 4 – Instantiate the Class, Increment, and Log the Result

Na koniec łączymy wszystko: tworzymy instancję, wywołujemy `increment()` i wypisujemy ostateczną wartość licznika. To demonstracja **increment counter class** w działaniu.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### Expected Console Output

```
Counter class initialized
Final count: 1
```

Jeśli otworzysz stronę w DevTools, powinieneś zobaczyć komunikat ze statycznego bloku pojawiający się **przed** zakończeniem opóźnienia, co potwierdza, że klasa została oceniona jako pierwsza.

## Step 5 – Why Use Public Class Fields Instead of a Constructor?

Możesz się zastanawiać, dlaczego nie napisaliśmy:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

Oba podejścia działają, ale **public class fields javascript** dają czystszą, bardziej deklaratywną składnię. Pole jest definiowane raz, a nie wewnątrz każdego wywołania konstruktora, co może być łatwiejsze do odczytania, gdy klasa rośnie. Dodatkowo, statyczne bloki nie mogą być umieszczone wewnątrz konstruktora, więc oddzielenie logiki inicjalizacyjnej staje się bardziej naturalne.

## Step 6 – Adapting the Example for Real‑World Apps

W produkcji często potrzebujesz więcej niż jednego licznika. Oto kilka szybkich pomysłów:

- **Multiple counters:** Przechowuj je w `Map` kluczowanej identyfikatorem.
- **Persisted state:** Zamień `console.log` na zapisy do `localStorage`.
- **Async initialization:** Użyj statycznego bloku do pobrania konfiguracji z serwera przed utworzeniem jakiejkolwiek instancji.

Wszystkie te wzorce nadal korzystają z top‑level await, ponieważ możesz pobrać dane raz przy ładowaniu modułu i mieć pewność, że będą gotowe dla każdego konsumenta.

## Frequently Asked Questions

**Q: Czy top‑level await blokuje inne moduły?**  
A: Nie. Każdy moduł działa niezależnie. Tylko moduł zawierający await jest wstrzymany; pozostałe moduły ładują się równolegle.

**Q: Co się stanie, jeśli obietnica opóźnienia zostanie odrzucona?**  
A: Nieobsłużone odrzucenie przerwie ocenianie modułu i pojawi się jako błąd w konsoli. Owiń `await` w `try…catch`, jeśli potrzebujesz łagodnego fallbacku.

**Q: Czy słowo kluczowe `static` jest wymagane?**  
A: Nie dla samego licznika, ale statyczny blok jest przydatny, aby pokazać, że kod uruchamia się *jednorazowo* przy ładowaniu — świetny do logowania lub wykrywania funkcji.

## Conclusion

Właśnie zbudowałeś **top level await example**, które prezentuje `await delay javascript`, **increment counter class** oraz moc **public class fields javascript**. Pełny, działający fragment kodu znajduje się powyżej, a wynik w konsoli dowodzi, że statyczny blok uruchamia się przed kodem opóźnionym.  

Od tego momentu możesz eksperymentować z bardziej złożonymi przepływami async, zamienić opóźnienie na prawdziwe wywołanie API lub rozbudować klasę o dodatkowe metody. Pamiętaj, nowoczesny JavaScript pozwala traktować moduły jako pierwszorzędne jednostki async — bez dodatkowych wrapperów.

Miłego kodowania i zachęcam do dzielenia się swoimi wariacjami w komentarzach. Jeśli ten przewodnik okazał się przydatny, podziel się nim z kolegą, który wciąż zmaga się z wzorcami async!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}