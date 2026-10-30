---
category: general
date: 2026-02-16
description: Jak załadować HTML w Javie, ustawić DPI urządzenia, zdefiniować wirtualny
  rozmiar ekranu i odczytać obliczony kolor tła dowolnego elementu.
draft: false
keywords:
- how to load html
- read background color
- set device dpi
- set virtual screen size
- get computed background color
language: pl
og_description: Jak wczytać HTML w Javie, ustawić DPI urządzenia, zdefiniować wirtualny
  rozmiar ekranu i odczytać obliczony kolor tła dowolnego elementu.
og_title: Jak załadować HTML, ustawić DPI urządzenia i odczytać kolor tła
tags:
- Aspose.HTML
- Java
title: Jak wczytać HTML, ustawić DPI urządzenia i odczytać kolor tła
url: /pl/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak załadować HTML, ustawić DPI urządzenia i odczytać kolor tła

Zastanawiałeś się kiedyś **jak załadować html** w aplikacji Java i następnie sprawdzić style strony? Nie jesteś sam — programiści często muszą renderować stronę internetową poza ekranem, pobrać ostateczne wartości CSS i używać ich do konwersji PDF, zrzutów ekranu lub nawet testów automatycznych.  

W tym przewodniku przejdziemy dokładnie przez ten proces: załadujemy plik HTML, **ustawimy DPI urządzenia**, zdefiniujemy **wirtualny rozmiar ekranu**, a na końcu **odczytamy kolor tła** z elementu `<body>`. Po zakończeniu będziesz mieć w pełni działający fragment kodu, który wypisze **obliczony kolor tła** — bez tajemnic, po prostu czysta Java.

## Czego będziesz potrzebować

* Java 17 lub nowsza (kod działa z dowolnym aktualnym JDK).  
* Aspose.HTML for Java 23.9 lub późniejsza — pobierz plik JAR ze strony Aspose lub dodaj go przez Maven.  
* Prosty plik HTML (np. `responsive.html`), który definiuje kolor tła w CSS.

To wszystko — bez dodatkowych frameworków, bez sterowników przeglądarek. Gotowy? Zaczynajmy.

![Diagram przedstawiający, jak załadować html i wyodrębnić obliczone style](/images/load-html-diagram.png){alt="Diagram przedstawiający, jak załadować html"}

## Krok 1: Jak załadować HTML i skonfigurować opcje renderowania

Pierwszą rzeczą, którą robisz, jest stworzenie obiektu `HtmlLoadOptions`. Ten obiekt mówi Aspose.HTML **jak załadować html** — w tym wirtualne wymiary ekranu oraz DPI, które chcesz emulować.

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create load options and define the virtual screen size and DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        // setVirtualScreenSize – width × height in CSS pixels
        loadOptions.setScreenSize(new Size(1280, 800));
        // setDeviceDpi – typical desktop DPI (96 is the default for most monitors)
        loadOptions.setDeviceDpi(96);
```

**Dlaczego to ma znaczenie:**  
Ustawienie wirtualnego rozmiaru ekranu zapewnia, że zapytania medialne typu `@media (max-width: 600px)` zachowują się tak, jakby strona była renderowana na prawdziwym monitorze. DPI wpływa na to, jak jednostki CSS `px` są mapowane na fizyczne piksele — co jest kluczowe przy późniejszym generowaniu obrazów lub PDF‑ów.

## Krok 2: Załaduj plik HTML przy użyciu skonfigurowanych opcji

Teraz faktycznie ładujemy plik. Zauważ, że przekazujemy ten sam `loadOptions`, który właśnie skonfigurowaliśmy.

```java
        // 2️⃣ Load the HTML file with the options we just set.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);
```

Jeśli plik nie zostanie znaleziony, Aspose rzuca czytelny `FileNotFoundException`. W środowisku produkcyjnym warto otoczyć to wywołanie blokiem try‑catch i ewentualnie przejść do domyślnego łańcucha HTML.

## Krok 3: Ustaw wirtualny rozmiar ekranu i DPI urządzenia (jawnie)

Mimo że już wywołaliśmy `setScreenSize` i `setDeviceDpi` powyżej, warto podkreślić, że **ustawienie wirtualnego rozmiaru ekranu** oraz **ustawienie DPI urządzenia** można zmienić w dowolnym momencie przed renderowaniem. Na przykład możesz zwiększyć DPI dla wysokiej rozdzielczości zrzutów ekranu:

```java
        // 3️⃣ Adjust DPI for a high‑resolution render (optional).
        loadOptions.setDeviceDpi(300);   // 300 DPI is common for print‑ready images
        // 4️⃣ Change screen size for a mobile layout test.
        loadOptions.setScreenSize(new Size(375, 667)); // iPhone X viewport
```

Pamiętaj, aby ponownie załadować dokument, jeśli zmienisz te ustawienia po pierwszym załadowaniu — Aspose traktuje je jako niezmienne po utworzeniu obiektu `Document`.

## Krok 4: Odczytaj kolor tła i uzyskaj obliczony kolor tła

Gdy dokument znajduje się w pamięci, możesz zapytać o obliczony styl dowolnego elementu. Tutaj skupiamy się na tagu `<body>`, ale to samo podejście działa dla `<div>`, `<p>` czy nawet pseudo‑elementów.

```java
        // 5️⃣ Retrieve the <body> element.
        Element bodyElement = document.getBody();

        // 6️⃣ Output the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

**Co zobaczysz:** Jeśli `responsive.html` zawiera `body { background: #ff5722; }`, konsola wypisze coś w stylu:

```
Computed background color: rgba(255,87,34,1)
```

To jest wynik **get computed background color** — Aspose rozwiązuje wszystkie reguły kaskady CSS, zapytania medialne oraz deklaracje `!important`, zanim zwróci ostateczną wartość.

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny, gotowy do skopiowania program:

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create load options – virtual screen size + DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setScreenSize(new Size(1280, 800)); // set virtual screen size
        loadOptions.setDeviceDpi(96);                  // set device DPI (default desktop)

        // Optional: tweak for high‑resolution or mobile rendering.
        // loadOptions.setDeviceDpi(300);
        // loadOptions.setScreenSize(new Size(375, 667));

        // Step 2: Load the HTML document with the options.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);

        // Step 3: Grab the <body> element.
        Element bodyElement = document.getBody();

        // Step 4: Print the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

### Oczekiwany wynik

```
Computed background color: rgba(255,255,255,1)
```

*(Dokładne wartości RGBA zależą od CSS w Twoim pliku HTML.)*

## Częste pułapki i wskazówki profesjonalistów

* **Brak ustawienia DPI?** Aspose domyślnie używa 96 DPI, co może rozmywać zrzuty ekranu o wysokiej rozdzielczości. Zawsze ustaw je explicite, jeśli potrzebujesz wyraźnego wyniku.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}