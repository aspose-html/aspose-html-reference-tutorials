---
category: general
date: 2026-02-22
description: Ustaw współczynnik pikseli urządzenia w Javie przy użyciu piaskownicy
  Aspose.HTML. Dowiedz się, jak ustawić niestandardowy user agent, pobrać tytuł strony
  w Javie oraz konwertować HTML na PNG w jednym samouczku.
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- save html as image
- convert html to png
- get page title java
language: pl
og_description: Ustaw współczynnik pikseli urządzenia w Javie przy użyciu piaskownicy
  Aspose.HTML. Ten samouczek pokazuje, jak ustawić niestandardowy agent użytkownika,
  pobrać tytuł strony w Javie oraz konwertować HTML na PNG.
og_title: Ustaw współczynnik pikseli urządzenia w Javie – Kompletny przewodnik
tags:
- Aspose.HTML
- Java
- Web Rendering
title: Ustaw współczynnik pikseli urządzenia w Javie – kompletny przewodnik
url: /pl/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/
---

no markdown links.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ustaw współczynnik pikseli urządzenia w Javie – Kompletny przewodnik

Zastanawiałeś się kiedyś, jak **set device pixel ratio** podczas renderowania strony internetowej w Javie? Nie jesteś jedyny. Wielu programistów musi emulować ekrany mobilne o wysokiej rozdzielczości DPI, aby zrzuty ekranu były wyraźne, szczególnie gdy później **save html as image** w raportach lub materiałach marketingowych. W tym samouczku przeprowadzimy praktyczny przykład, który robi dokładnie to — a także pokażemy, jak **set custom user agent**, **get page title java** i **convert html to png** przy użyciu Aspose.HTML.

Zaczniemy od krótkiego przeglądu API sandbox, następnie przejdziemy do każdego kroku konfiguracji i w końcu wygenerujemy plik PNG, który odzwierciedla rzeczywisty wyświetlacz iPhone’a. Po zakończeniu będziesz mieć wielokrotnego użytku fragment kodu, który możesz wkleić do dowolnego projektu w Javie. Nie są potrzebne żadne zewnętrzne narzędzia, wystarczy czysta Java i Aspose.HTML 7.x (lub nowsza).

---

## Prerequisites

- Java 17 lub nowsza (kod kompiluje się również w starszych wersjach, ale zalecana jest 17).
- Biblioteka Aspose.HTML for Java (pobierz z oficjalnej strony Aspose; współrzędne Maven: `com.aspose:aspose-html:23.10`).
- IDE lub edytor tekstu według własnego wyboru (IntelliJ IDEA, VS Code, Eclipse… wszystkie działają).
- Dostęp do Internetu dla adresu demo (`https://example.com/responsive.html`), lub zamień go na dowolną publiczną stronę HTML, którą posiadasz.

> **Wskazówka:** Jeśli korzystasz z proxy, skonfiguruj właściwości systemowe JVM `http.proxyHost` i `http.proxyPort` przed uruchomieniem kodu.

---

## Krok 1: Ustaw współczynnik pikseli urządzenia i inne opcje sandbox

Pierwszą rzeczą, której potrzebujemy, jest instancja **SandboxOptions**, w której definiujemy wirtualny rozmiar ekranu oraz *device pixel ratio* (DPR). DPR to czynnik określający, ile fizycznych pikseli odpowiada jednemu pikselowi CSS. Na iPhone’ie z wyświetlaczem Retina DPR wynosi zazwyczaj **2.0**, dlatego użyjemy tej wartości.

```java
// Step 1: Create and configure SandboxOptions
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS width of an iPhone X
sandboxOptions.setScreenHeight(667);         // CSS height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
```

> **Dlaczego to ważne:** Bez ustawienia prawidłowego DPR renderowany obraz będzie wyglądał na rozmyty lub zbyt duży, ponieważ rasteryzator zakłada mapowanie 1:1 pikseli.

---

## Krok 2: Ustaw własny User Agent

Strony internetowe często dostarczają różny kod w zależności od nagłówka **User‑Agent**. Aby upewnić się, że nasza strona zachowuje się tak, jak na prawdziwym iPhone’ie, wstrzykujemy własny ciąg znaków imitujący Safari na iOS.

```java
// Step 2: Define a mobile‑specific user agent
String iphoneUA = "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                  "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                  "Version/14.0 Mobile/15E148 Safari/604.1";

sandboxOptions.setUserAgent(iphoneUA);   // <-- set custom user agent
```

> **Przypadek brzegowy:** Niektóre strony sprawdzają również nagłówek `Accept-Language`. Jeśli zauważysz brakujące tłumaczenia, dodaj `sandboxOptions.setAcceptLanguage("en-US,en;q=0.9");`.

---

## Krok 3: Załaduj stronę w sandboxie i pobierz tytuł

Teraz uruchamiamy sandbox z wcześniej zdefiniowanymi opcjami. Obiekt **Sandbox** izoluje proces renderowania, zapewniając, że nasze ustawienia DPR i user‑agent są respektowane.

```java
// Step 3: Create the sandbox and load the HTML document
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
HTMLDocument htmlDoc = new HTMLDocument(
        "https://example.com/responsive.html", mobileSandbox);
```

Gdy strona zostanie załadowana, pobranie tytułu jest tak proste, jak wywołanie `getTitle()`. Spełnia to wymóg **get page title java**.

```java
// Step 3b: Print the page title to the console
System.out.println("Title: " + htmlDoc.getTitle());   // <-- get page title java
```

**Oczekiwany wynik w konsoli**

```
Title: Responsive Demo – Mobile View
```

Jeśli tytuł jest pusty, sprawdź ponownie adres URL lub upewnij się, że strona nie jest zablokowana przez polityki CORS.

---

## Krok 4: Konwertuj HTML do PNG i zapisz HTML jako obraz

Aspose.HTML umożliwia renderowanie DOM bezpośrednio do pliku obrazu. Ponieważ już ustawiliśmy DPR na 2.0, wynikowy PNG będzie miał podwójną gęstość pikseli, co daje wyraźny zrzut ekranu.

```java
// Step 4: Render and save as PNG (convert html to png)
htmlDoc.save("mobile_view.png");   // <-- save html as image
```

Metoda `save` automatycznie wykrywa rozszerzenie pliku i wybiera odpowiedni renderer. Jeśli potrzebujesz innego formatu (JPEG, BMP), po prostu zmień nazwę pliku.

> **Co zrobić, jeśli potrzebny jest konkretny rozmiar obrazu?**  
> Użyj `ImageSaveOptions`, aby kontrolować szerokość, wysokość i kolor tła:

```java
ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
pngOptions.setWidth(750);   // 375 CSS px * DPR 2
pngOptions.setHeight(1334);
htmlDoc.save("mobile_view_custom.png", pngOptions);
```

---

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do uruchomienia program, który łączy wszystkie kroki. Skopiuj i wklej go do pliku `SandboxDemo.java`, dodaj zależność Aspose.HTML i uruchom `java SandboxDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.rendering.image.ImageSaveOptions;
import com.aspose.html.rendering.image.SaveFormat;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Configure sandbox – set device pixel ratio, screen size, and user agent
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS width (iPhone)
        sandboxOptions.setScreenHeight(667);         // CSS height
        sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                "Version/14.0 Mobile/15E148 Safari/604.1");   // <-- set custom user agent

        // 2️⃣ Create sandbox instance
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // 3️⃣ Load the target page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox);

        // 4️⃣ Retrieve and print the page title (get page title java)
        System.out.println("Title: " + htmlDoc.getTitle());

        // 5️⃣ Render the page – convert html to png and save html as image
        // Simple save (auto‑detect PNG)
        htmlDoc.save("mobile_view.png");   // <-- save html as image

        // 6️⃣ Optional: custom size rendering
        ImageSaveOptions opts = new ImageSaveOptions(SaveFormat.PNG);
        opts.setWidth(750);   // 375 * DPR 2
        opts.setHeight(1334);
        htmlDoc.save("mobile_view_custom.png", opts); // another convert html to png example
    }
}
```

Uruchomienie programu generuje dwa pliki PNG:

| Plik | Opis |
|------|------|
| `mobile_view.png` | Domyślne renderowanie przy użyciu skonfigurowanego DPR. |
| `mobile_view_custom.png` | Renderowanie z określoną szerokością/wysokością (przydatne dla zasobów o stałym rozmiarze). |

Możesz otworzyć dowolny z plików w dowolnym przeglądarce obrazów, aby zweryfikować wysoką rozdzielczość.

---

## Częste pytania i przypadki brzegowe

| Pytanie | Odpowiedź |
|----------|-----------|
| **Co zrobić, jeśli strona zawiera JavaScript, który modyfikuje DOM po załadowaniu?** | Aspose.HTML domyślnie wykonuje skrypty. Jeśli potrzebujesz statycznego zrzutu przed wykonaniem skryptów, ustaw `sandboxOptions.setEnableJavaScript(false)`. |
| **Czy mogę renderować stronę wymagającą uwierzytelnienia?** | Tak. Użyj `sandboxOptions.setCredentials(new NetworkCredential("user","pass"))` lub wstrzyknij ciasteczka poprzez `sandboxOptions.getCookies().add(...)`. |
| **Czy DPR jest ograniczone do 2.0?** | Nie. Możesz ustawić dowolną dodatnią liczbę zmiennoprzecinkową (np. 3.0 dla ultra‑wysokiej rozdzielczości DPI). Pamiętaj jednak, że większy DPR oznacza większe pliki obrazów. |
| **Jak obsłużyć strony z dużymi zasobami (obrazy, czcionki)?** | Zwiększ limit pamięci sandboxa za pomocą `sandboxOptions.setMemoryLimit(512 * 1024 * 1024)` (bajty). Zapobiega to błędom out‑of‑memory na ciężkich stronach. |
| **Czy muszę ręcznie zamykać sandbox?** | Obiekt `Sandbox` implementuje `AutoCloseable`. Umieść go w bloku try‑with‑resources, aby automatycznie zwolnić zasoby. |

---

## Zakończenie

Pokazaliśmy, jak **set device pixel ratio** w sandboxie Java, **set custom user agent**, **get page title java**, oraz **convert html to png** (efektywnie **save html as image**) przy użyciu Aspose.HTML. Pełny przykład demonstruje praktyczny przepływ pracy, który możesz dostosować do automatycznego generowania zrzutów ekranu, testów regresji wizualnej lub dowolnego scenariusza, w którym potrzebna jest piksel‑idealna reprezentacja strony internetowej.

Śmiało eksperymentuj — zmień DPR na 3.0, zamień user‑agent na ciąg Androida lub wskaż URL na lokalny plik HTML. Ten sam wzorzec działa dla PDF‑ów, SVG‑ów, a nawet renderowania wielostronicowego.

Jeśli ten przewodnik okazał się pomocny, rozważ zgłębienie powiązanych tematów, takich jak **PDF generation with Aspose.HTML**, **headless Chrome alternatives**, lub **batch rendering of multiple URLs**. Miłego kodowania i niech Twoje zrzuty ekranu zawsze będą ostra jak brzytwa!

![set device pixel ratio in Java sandbox](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}