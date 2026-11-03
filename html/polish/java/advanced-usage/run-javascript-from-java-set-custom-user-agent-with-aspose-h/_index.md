---
category: general
date: 2026-04-26
description: Uruchamiaj JavaScript z Javy przy użyciu Aspose.HTML i dowiedz się, jak
  ustawić niestandardowy user-agent dla symulowanego okna przeglądarki.
draft: false
keywords:
- run javascript from java
- set custom user-agent
- how to set user-agent
- configure window settings
- simulate browser java
language: pl
og_description: Uruchamiaj JavaScript z Javy przy użyciu Aspose.HTML. Dowiedz się,
  jak ustawić niestandardowy user‑agent i skonfigurować ustawienia okna dla symulowanej
  przeglądarki.
og_title: Uruchamianie JavaScript z Javy – Ustaw niestandardowy User-Agent
tags:
- Java
- Aspose.HTML
- JavaScript Execution
title: Uruchamianie JavaScript z Javy – Ustaw niestandardowy User-Agent przy użyciu
  Aspose.HTML
url: /pl/java/advanced-usage/run-javascript-from-java-set-custom-user-agent-with-aspose-h/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uruchamianie JavaScript z Javy – Ustaw niestandardowy User-Agent przy użyciu Aspose.HTML

Czy kiedykolwiek potrzebowałeś **uruchomić JavaScript z Javy**, udając, że jesteś prawdziwą przeglądarką? Może scrapujesz stronę, która blokuje nieznane agenty, albo po prostu chcesz przetestować skrypt bez otwierania Chrome. W tym poradniku pokażemy dokładnie, jak to zrobić, a także omówimy **jak ustawić user-agent**, aby zdalny serwer myślał, że ma do czynienia z zwykłą przeglądarką desktopową.

Będziemy korzystać z biblioteki Aspose.HTML, która zapewnia Javie lekkie, bezgłowe środowisko podobne do przeglądarki. Po zakończeniu tego przewodnika będziesz mógł wykonać dowolny fragment JavaScript, skonfigurować ustawienia okna i **symulować zachowanie przeglądarki Java** przy użyciu niestandardowego ciągu user‑agent. Bez zewnętrznych przeglądarek, bez Selenium, tylko czysty kod Java.

## Co będzie potrzebne

- **Java 17** (lub dowolny aktualny JDK; API działa na Java 8+)
- **Aspose.HTML for Java** 23.9 (lub najnowsza wersja w momencie pisania)
- Porządny IDE (IntelliJ IDEA, Eclipse, VS Code — Twój wybór)
- Podstawowa znajomość koncepcji Java i JavaScript

Jeśli już je masz, świetnie — przejdźmy od razu do kodu. Jeśli nie, pobierz plik JAR Aspose.HTML z oficjalnej strony i dodaj go do classpath swojego projektu; biblioteka zawiera wszystkie zależności, więc nie będziesz potrzebował nic więcej.

> **Wskazówka:** Gdy dodajesz JAR do projektu Maven, użyj następujących współrzędnych:  
> ```xml
> <dependency>
>     <groupId>com.aspose</groupId>
>     <artifactId>aspose-html</artifactId>
>     <version>23.9</version>
> </dependency>
> ```

---

## ## Uruchamianie JavaScript z Javy: Główna idea

W swojej istocie klasa `Window` z Aspose.HTML naśladuje okno przeglądarki. Możesz podać jej HTML, CSS i JavaScript, a następnie poprosić o ocenę skryptu i zwrócenie wyniku. Traktuj to jak mały Chrome, który żyje wewnątrz Twojej JVM, ale bez interfejsu UI.

Poniżej znajduje się kompletny, gotowy do uruchomienia program, który demonstruje cały przepływ:

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class JsEngineExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create window settings and define a custom User‑Agent string
        WindowSettings windowSettings = new WindowSettings();
        windowSettings.setUserAgent(
            "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"
        );

        // Step 2: Open a browser‑like window using the configured settings
        try (Window browserWindow = new Window(windowSettings)) {

            // Step 3: Execute JavaScript that reads the navigator.userAgent property
            browserWindow.evaluateScript("var ua = navigator.userAgent; ua;");

            // Step 4: Retrieve the script result (the custom User‑Agent) and display it
            String userAgent = (String) browserWindow.getLastResult();
            System.out.println("Custom user‑agent: " + userAgent);
        }
    }
}
```

**Oczekiwany wynik**

```
Custom user‑agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36
```

Uruchomienie tego programu jednocześnie dowodzi trzech rzeczy:

1. **Uruchamiasz JavaScript z Javy** (`evaluateScript`).
2. **Ustawiasz niestandardowy user-agent** (`setUserAgent` on `WindowSettings`).
3. **Konfigurujesz ustawienia okna**, aby symulować prawdziwe środowisko przeglądarki.

---

## ## Konfiguracja ustawień okna dla realistycznej przeglądarki

Po co w ogóle używać `WindowSettings`? Większość usług internetowych sprawdza nagłówek `User‑Agent`, aby zdecydować, czy dostarczyć treść mobilną, desktopową czy specyficzną dla botów. Jeśli pominiesz realistyczny ciąg, możesz otrzymać odchudzoną wersję strony lub zostać całkowicie zablokowany.

### Szczegółowy podział krok po kroku

| Krok | Co robimy | Dlaczego to ważne |
|------|------------|----------------|
| **Utwórz `WindowSettings`** | `new WindowSettings()` | Daje nam kontener dla wszystkich opcji podobnych do przeglądarki. |
| **Ustaw user‑agent** | `windowSettings.setUserAgent("…")` | Naśladuje klienta Chrome/Edge/Firefox, unikając wykrycia jako bot. |
| **Przekaż ustawienia do `Window`** | `new Window(windowSettings)` | Okno teraz dziedziczy naszą niestandardową konfigurację. |

Możesz także dostosować inne właściwości, takie jak `setLocale`, `setScreenWidth` czy `setScreenHeight`, aby jeszcze bardziej **symulować warunki przeglądarki Java**. Na przykład ustawienie szerokości ekranu na 1920 px sprawia, że responsywne strony myślą, że jesteś na monitorze desktopowym.

```java
windowSettings.setScreenWidth(1920);
windowSettings.setScreenHeight(1080);
```

---

## ## Ustaw niestandardowy User-Agent: Popularne warianty

Nie istnieje uniwersalny ciąg user‑agent. W zależności od docelowej strony, możesz potrzebować:

- **Chrome na Windows** (przykład powyżej)
- **Safari na macOS**  
  ```java
  windowSettings.setUserAgent(
      "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) " +
      "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.1 Safari/605.1.15"
  );
  ```
- **Mobile Chrome**  
  ```java
  windowSettings.setUserAgent(
      "Mozilla/5.0 (Linux; Android 11; Pixel 5) " +
      "AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.71 Mobile Safari/537.36"
  );
  ```

Gdy pytanie **jak ustawić user-agent** się pojawia, odpowiedź jest prosta: „wywołaj `setUserAgent` z dokładnym ciągiem, którego potrzebujesz”. Bez dodatkowych nagłówków, bez manipulacji na poziomie sieci. Biblioteka zajmuje się wszystkim pod maską.

---

## ## Symuluj przeglądarkę Java: Wykraczając poza User-Agent

Jeśli chcesz **symulować przeglądarkę Java** dokładniej — na przykład potrzebujesz ciasteczek, local storage lub nawet niestandardowego obiektu `navigator` — Aspose.HTML oferuje kilka dodatkowych ustawień:

```java
// Enable cookies
windowSettings.setCookiePolicy(CookiePolicy.ACCEPT_ALL);

// Pre‑populate local storage
browserWindow.getLocalStorage().setItem("token", "abc123");

// Override navigator.platform if needed
browserWindow.evaluateScript(
    "Object.defineProperty(navigator, 'platform', { get: () => 'Win32' });"
);
```

Te fragmenty kodu ilustrują, jak możesz kształtować środowisko, aby pasowało do niemal każdego scenariusza przeglądarki. Pamiętaj, że każda dodatkowa funkcja może zwiększyć zużycie pamięci, ale w większości zadań automatyzacji narzut jest pomijalny.

---

## ## Częste pułapki i jak ich unikać

1. **Zapomnienie o zamknięciu `Window`** – Blok `try‑with‑resources` w przykładzie zapewnia zwolnienie okna. Jeśli tworzysz je ręcznie, zawsze wywołaj `browserWindow.close()` w klauzuli `finally`.
2. **Używanie przestarzałego user‑agent** – Strony internetowe często aktualizują logikę wykrywania. Okresowo odświeżaj ciąg z narzędzi deweloperskich prawdziwej przeglądarki (Network → Headers → User‑Agent).
3. **Uruchamianie skryptów zależnych od DOM** – `evaluateScript` działa dobrze dla czystego JavaScript, ale jeśli potrzebujesz pełnego dokumentu HTML, najpierw go załaduj:  
   ```java
   browserWindow.navigate("about:blank");
   browserWindow.getDocument().write("<html><body></body></html>");
   ```
4. **Bezpieczeństwo wątków** – Każda instancja `Window` jest powiązana z wątkiem, który ją utworzył. Nie udostępniaj tego samego okna wielu wątkom; zamiast tego twórz nowe okno dla każdego wątku.

---

## ## Zweryfikuj wynik – szybki test

Po skompilowaniu i uruchomieniu programu powinieneś zobaczyć niestandardowy user‑agent wypisany w konsoli. Aby podwójnie sprawdzić, że biblioteka naprawdę wysyła nagłówek, możesz skierować okno na prostą usługę echo:

```java
browserWindow.navigate("https://httpbin.org/user-agent");
browserWindow.evaluateScript("document.body.textContent;");
String echoed = (String) browserWindow.getLastResult();
System.out.println("Echoed from server: " + echoed);
```

Wyjście będzie zawierało ten sam ciąg, który ustawiłeś wcześniej, potwierdzając, że krok **konfiguracji ustawień okna** zadziałał od początku do końca.

---

## ## Pełny działający przykład (wszystkie kroki połączone)

Poniżej znajduje się ostateczna, samodzielna klasa Java, którą możesz skopiować i wkleić do dowolnego IDE:

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class JsEngineFullDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create and configure window settings
        WindowSettings settings = new WindowSettings();
        settings.setUserAgent(
            "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"
        );
        settings.setScreenWidth(1920);
        settings.setScreenHeight(1080);
        settings.setCookiePolicy(CookiePolicy.ACCEPT_ALL);

        // 2️⃣ Open the headless window
        try (Window win = new Window(settings)) {

            // 3️⃣ Run a simple script that returns navigator.userAgent
            win.evaluateScript("var ua = navigator.userAgent; ua;");
            String ua = (String) win.getLastResult();
            System.out.println("Custom user‑agent: " + ua);

            // 4️⃣ Optional: Verify via an external service
            win.navigate("https://httpbin.org/user-agent");
            win.evaluateScript("document.body.textContent;");
            String echoed = (String) win.getLastResult();
            System.out.println("Echoed from server: " + echoed);
        }
    }
}
```

Uruchom ją, obserwuj konsolę i udało Ci się **uruchomić JavaScript z Javy**, ustawić **niestandardowy user-agent** oraz **skonfigurować ustawienia okna**, aby symulować prawdziwą przeglądarkę — wszystko bez opuszczania JVM.

---

## ## Ilustracja obrazkowa

![Run JavaScript from Java custom user-agent example](https://example.com/images/run-js-from-java.png "Run JavaScript from Java custom user-agent example")

*Diagram przedstawia przepływ: Java → Aspose.HTML `Window` → Wykonanie JavaScript → Wynik.*

---

## ## Kolejne kroki i powiązane tematy

- **Zaawansowana manipulacja DOM** – Załaduj pełną stronę HTML i użyj `document.querySelector` wewnątrz `evaluateScript`.
- **Testowanie headless** – Połącz Aspose.HTML z JUnit, aby automatycznie weryfikować wyniki JavaScript.
- **Obsługa proxy** – Jeśli docelowa strona blokuje Twój adres IP, skonfiguruj `WindowSettings.setProxy`, aby kierować ruch przez serwer proxy.
- **Optymalizacja wydajności** – Przy operacjach masowych, ponownie używaj jednej instancji `Window` i jedynie czyszcz dokument pomiędzy uruchomieniami.

Każdy z tych tematów opiera się na fundamentach, które tutaj przedstawiliśmy: **uruchamianie javascript z java**, **ustawianie niestandardowego user-agent**, oraz **konfiguracja ustawień okna**. Zagłęb się w dokumentację Aspose.HTML, aby uzyskać szerszy zakres API, lub eksperymentuj z powyższymi fragmentami kodu, aby dopasować je do własnych potrzeb.

---

## ## Zakończenie

Przeszliśmy przez kompletny, działający przykład, który pokazuje, jak **uruchomić JavaScript z Javy**, ustawić niestandardowy user‑agent i w pełni **skonfigurować ustawienia okna**, aby **symulować zachowanie przeglądarki Java**. Podejście jest lekkie

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}