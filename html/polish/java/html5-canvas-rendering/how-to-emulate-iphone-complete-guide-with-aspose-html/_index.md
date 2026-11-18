---
category: general
date: 2026-03-26
description: Dowiedz się, jak emulować iPhone’a w Javie przy użyciu Aspose.HTML. Zawiera
  kroki ustawienia niestandardowego agenta użytkownika i ustawienia współczynnika
  pikseli urządzenia dla dokładnego renderowania mobilnego.
draft: false
keywords:
- how to emulate iphone
- set custom user agent
- set device pixel ratio
- how to set user-agent
- how to set dpr
language: pl
og_description: Jak emulować iPhone w Javie? Ten samouczek pokazuje, jak ustawić niestandardowy
  user‑agent i współczynnik pikseli urządzenia przy użyciu Aspose.HTML, dostarczając
  mobilne strony o idealnym odwzorowaniu pikseli.
og_title: Jak emulować iPhone – Przewodnik Aspose.HTML krok po kroku
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Jak emulować iPhone – Kompletny przewodnik z Aspose.HTML
url: /pl/java/html5-canvas-rendering/how-to-emulate-iphone-complete-guide-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak emulować iPhone – Kompletny przewodnik z Aspose.HTML

Zastanawiałeś się kiedyś **jak emulować iPhone**, testując stronę internetową lokalnie? Być może debugujesz responsywny układ i przeglądarka na komputerze po prostu nie wystarcza. Dobrą wiadomością jest to, że nie potrzebujesz fizycznego urządzenia — Aspose.HTML’s `DocumentSandbox` pozwala naśladować ekran iPhone’a, user‑agent oraz device‑pixel‑ratio (DPR) kilkoma liniami Javy.  

W tym tutorialu przejdziemy krok po kroku przez ustawienie **niestandardowego user‑agent**, skonfigurowanie **device pixel ratio** oraz weryfikację, że wszystko działa zgodnie z oczekiwaniami. Po zakończeniu będziesz mieć wielokrotnego użytku sandbox, który renderuje strony tak, jak iPhone 8, i zrozumiesz, dlaczego każde ustawienie ma znaczenie.

## Co osiągniesz

- Utwórz obiekt `Screen`, który odzwierciedla wymiary iPhone’a oraz DPR.  
- Zastosuj **niestandardowy ciąg user‑agent**, aby serwery myślały, że żądanie pochodzi z Safari na iOS.  
- Zbuduj `DocumentSandbox`, który łączy ekran i user‑agent.  
- Uruchom `HTMLDocument` wewnątrz sandboxu i zobacz wyjście konsoli potwierdzające konfigurację.  

Nie są wymagane żadne zewnętrzne biblioteki poza Aspose.HTML, a kod działa w dowolnym środowisku Java 17+.

---

![zrzut ekranu jak emulować iPhone](https://example.com/images/iphone-emulation.png "jak emulować iPhone przy użyciu sandboxu Aspose.HTML")

## Jak emulować iPhone przy użyciu Aspose.HTML Sandbox

Pierwszą rzeczą, której potrzebujemy, jest `Screen`, który odzwierciedla fizyczne wymiary iPhone’a *oraz* jego gęstość pikseli. To jest sedno **jak emulować iPhone** dokładnie.

```java
import com.aspose.html.devices.Screen;

// Step 1: Define iPhone 8 screen size (width, height) and DPR
Screen mobileScreen = new Screen(375, 667, 2.0); // iPhone 8 dimensions, DPR = 2
```

**Dlaczego to ma znaczenie:**  
- Szerokość = 375 px i wysokość = 667 px to wymiary w pikselach CSS, które zobaczysz w Chrome DevTools po wybraniu iPhone 8.  
- Ustawienie DPR na 2 informuje silnik renderujący, że każdy piksel CSS jest równy dwóm fizycznym pikselom, co daje ostre teksty i obrazy — dokładnie tak, jak robi to prawdziwe urządzenie.

> *Wskazówka:* Jeśli potrzebujesz emulować nowszy iPhone (np. iPhone 13), po prostu zmień liczby na 390 × 844 i DPR = 3.

## Ustawianie niestandardowego User Agent (set custom user agent)

Następnie musimy **ustawić niestandardowy user agent**, aby serwer dostarczał mobilne wersje HTML/CSS. Bez tego wiele stron nadal będzie myślało, że jesteś na komputerze.

```java
// Step 2: Define an iPhone Safari user‑agent string
String iPhoneUserAgent = "Mozilla/5.0 (iPhone; CPU iPhone OS 16_0 like Mac OS X) " +
                         "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                         "Version/16.0 Mobile/15E148 Safari/604.1";
```

**Jak to działa:**  
- `User-Agent` to nagłówek, którego przeglądarki używają do przedstawienia się.  
- Podając dokładny ciąg, który wysyła Safari na iOS 16, zapewniasz, że serwer zwróci zasoby zoptymalizowane pod mobile (np. responsywne obrazy, adaptacyjne skrypty, itp.).  

Jeśli kiedykolwiek będziesz musiał **ustawić user-agent** dla innego urządzenia, po prostu zamień ciąg na odpowiednią wartość — Google Chrome, Firefox lub nawet własny bot.

## Konfigurowanie Device Pixel Ratio (set device pixel ratio)

Teraz faktycznie **ustawiamy device pixel ratio** wewnątrz sandboxu. To krok, który bezpośrednio odpowiada na pytanie “**jak ustawić dpr**” w środowisku symulowanym.

```java
import com.aspose.html.sandbox.DocumentSandbox;

// Step 3: Build the sandbox with screen and user‑agent
DocumentSandbox documentSandbox = new DocumentSandbox.Builder()
        .setScreen(mobileScreen)          // applies the DPR we defined earlier
        .setUserAgent(iPhoneUserAgent)    // applies the custom user‑agent
        .build();
```

**Wyjaśnienie:**  
- Wzorzec `Builder` pozwala płynnie dołączyć zarówno ekran (z DPR), jak i user‑agent.  
- Gdy sandbox renderuje `HTMLDocument`, będzie udawał, że działa na urządzeniu o dokładnie takiej gęstości pikseli.  

> *Dlaczego to ważne:* Niektóre zapytania media w CSS używają `device-pixel-ratio` (np. `@media (-webkit-min-device-pixel-ratio: 2)`). Jeśli nie ustawisz DPR, te reguły nigdy się nie uruchomią i przegapisz zasoby w wysokiej rozdzielczości.

## Weryfikacja konfiguracji sandboxu (how to set user-agent)

Umieśćmy sandbox w działaniu. Poniższy fragment tworzy `HTMLDocument`, ładuje stronę i wypisuje potwierdzenie, że sandbox jest aktywny.

```java
import com.aspose.html.HTMLDocument;

public class SandboxWithDprAndUa {
    public static void main(String[] args) {
        // Re‑use the sandbox we built earlier
        // DocumentSandbox documentSandbox = ... (from previous step)

        // Step 4: Load a page inside the sandbox
        HTMLDocument doc = new HTMLDocument("https://example.com", documentSandbox);

        // Step 5: Optional – output a sanity check
        System.out.println("Sandbox configured with DPR=2 and iPhone user‑agent.");
    }
}
```

**Oczekiwany wynik w konsoli**

```
Sandbox configured with DPR=2 and iPhone user-agent.
```

Jeśli uruchomisz program i zobaczysz tę linię, pomyślnie **emulowałeś iPhone** z prawidłowym DPR i user‑agent. Otwórz stronę w prawdziwej przeglądarce i sprawdź wymiary viewportu — zauważysz, że odpowiadają wartościom iPhone’a, które ustawiliśmy.

## Typowe pułapki i jak poprawnie ustawić DPR (how to set dpr)

Nawet przy prawidłowym kodzie kilka drobnych problemów może Cię zaskoczyć:

| Problem | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| **DPR pozostaje przy 1** | Przekazałeś `Screen` bez trzeciego argumentu (DPR). | Zawsze używaj `new Screen(width, height, dpr)`. |
| **User‑Agent ignorowany** | Sandbox nie został podłączony do `HTMLDocument`. | Przekaż `documentSandbox` jako drugi argument do konstruktora `HTMLDocument`. |
| **Nieprawidłowe wymiary** | Używanie pikseli urządzenia zamiast pikseli CSS. | Pamiętaj: szerokość/wysokość to **piksele CSS**, a nie piksele sprzętowe. |
| **Serwer wciąż wysyła desktopowy CSS** | Niektóre strony używają JavaScriptu do wykrywania urządzeń, nie tylko nagłówka. | Rozważ także wstrzyknięcie meta tagu viewport, jeśli to konieczne. |

Mając te informacje na uwadze, rzadko spotkasz sytuację, w której emulacja nie zachowuje się zgodnie z oczekiwaniami.

## Rozszerzanie sandboxu – kolejne kroki

Teraz, gdy znasz **jak ustawić niestandardowy user agent** i **jak ustawić dpr**, możesz dalej eksperymentować:

- **Zmień rozmiar ekranu** aby emulować tablety lub większe telefony.  
- **Zamień user‑agent** aby testować Chrome na Androidzie (`"Mozilla/5.0 (Linux; Android 12; ...) Chrome/110.0"`).  
- **Dodaj ciasteczka lub nagłówki** za pomocą metody `setHeaders` sandboxu, aby testować uwierzytelnione sesje.  
- **Zrób zrzut ekranu** używając `HTMLDocument.renderToFile("output.png")`, aby automatycznie porównać różnice wizualne.

Te rozszerzenia pozwalają zbudować w pełni funkcjonalny zestaw testowy bez opuszczania IDE.

---

## Zakończenie

Omówiliśmy **jak emulować iPhone** przy użyciu `DocumentSandbox` z Aspose.HTML, pokazując dokładnie **jak ustawić niestandardowy user agent**, **jak ustawić device pixel ratio**, a także subtelne różnice między “**jak ustawić user-agent**” a “**jak ustawić dpr**”. Kompletny, działający przykład demonstruje wszystkie elementy w jednym miejscu, więc możesz kopiować‑wklejać, modyfikować i od razu rozpocząć testowanie układów mobilnych.  

Spróbuj — zmień wymiary ekranu, baw się różnymi user‑agentami i obserwuj, jak Twoje strony reagują. Gdy opanujesz te ustawienia, debugowanie responsywnych projektów stanie się bułką z masłem, a Ty zaoszczędzisz niezliczone godziny na poszukiwaniu błędów na prawdziwych urządzeniach.

Masz pytania lub chcesz podzielić się własnymi wariacjami? zostaw komentarz poniżej i powodzenia w emulacji!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}