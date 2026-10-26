---
category: general
date: 2026-02-14
description: Jak ustawić DPI przy konwersji SVG na PNG przy użyciu Javy. Eksportuj
  PNG wysokiej rozdzielczości, dowiedz się, jak konwertować SVG na PNG i używać biblioteki
  konwersji obrazów w Javie.
draft: false
keywords:
- how to set dpi
- convert svg to png
- export high resolution png
- how to convert svg
- java image conversion library
language: pl
og_description: Jak ustawić DPI przy konwersji SVG na PNG przy użyciu Javy. Ten przewodnik
  pokazuje, jak wyeksportować PNG w wysokiej rozdzielczości i używać biblioteki konwersji
  obrazów w Javie.
og_title: Jak ustawić DPI przy konwertowaniu SVG na PNG w Javie
tags:
- java
- image-conversion
- svg
- png
title: Jak ustawić DPI przy konwertowaniu SVG na PNG w Javie
url: /pl/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ustawić DPI przy konwersji SVG do PNG w Javie

Zastanawiałeś się kiedyś **jak ustawić DPI** przy konwersji SVG‑do‑PNG, aby wynik wyglądał ostro na plakacie gotowym do druku? Nie jesteś sam. W wielu projektach — myśl o ulotkach marketingowych, makietach UI czy diagramach technicznych — uzyskanie wysokiej rozdzielczości PNG z SVG jest nie do negocjacji.  

W tym tutorialu przejdziemy krok po kroku przez **konwersję SVG do PNG**, **eksport wysokiej rozdzielczości PNG**, a co najważniejsze, kontrolę DPI przy użyciu biblioteki Aspose.HTML for Java. Po zakończeniu będziesz mieć gotowy fragment kodu, który możesz wstawić do dowolnej aplikacji Java, niezależnie od tego, czy tworzysz narzędzie desktopowe, czy usługę backendową.

## Co będzie potrzebne

- **Java 8+** (kod kompiluje się na dowolnym nowoczesnym JDK)
- **Aspose.HTML for Java** JAR‑y (dostępne w Maven Central lub na stronie Aspose)
- Plik SVG, który chcesz rasteryzować  
- Odrobina ciekawości — nic więcej.

Jeśli korzystasz z Maven, po prostu dodaj zależność pokazana w następnym rozdziale; w przeciwnym razie pobierz JAR‑y ręcznie i dodaj je do classpath.

## Krok 1: Dodaj bibliotekę konwersji obrazów Java

Na początek — Twój projekt potrzebuje **biblioteki konwersji obrazów Java**, która potrafi odczytać SVG i zapisać PNG. Aspose.HTML to solidny wybór, ponieważ obsługuje CSS, czcionki i złożone funkcje wektorowe od razu.

**Użytkownicy Maven** mogą wkleić to do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- use the latest stable version -->
</dependency>
```

**Entuzjaści Gradle** mogą dodać:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

Jeśli wolisz ręczną drogę, pobierz JAR ze strony pobierania Aspose i umieść go w `libs/`, a następnie dodaj do ścieżki kompilacji w IDE.

> **Pro tip:** Zwróć uwagę na numer wersji; nowsze wydania często poprawiają obsługę DPI i naprawiają rzadkie błędy.

## Krok 2: Utwórz opcje konwersji i ustaw żądane DPI

Teraz, gdy biblioteka jest już dostępna, musimy powiedzieć jej *jak* ma wyglądać wyjściowy PNG. To właśnie tutaj wchodzi główne słowo kluczowe — **jak ustawić DPI**. Klasa `ImageConversionOptions` daje precyzyjną kontrolę nad rozdzielczością poziomą (`dpiX`) i pionową (`dpiY`).

```java
import com.aspose.html.converters.ImageConversionOptions;

// Step 2: Build the options object and set DPI
ImageConversionOptions conversionOptions = new ImageConversionOptions();
conversionOptions.setDpiX(300); // 300 DPI horizontally
conversionOptions.setDpiY(300); // 300 DPI vertically
```

Dlaczego 300 DPI? Dla większości procesów drukarskich 300 punktów na cal jest uznawane za „jakość druku”. Jeśli tworzysz zasoby wyłącznie na web, możesz obniżyć tę wartość do 72 lub 96 DPI, aby zmniejszyć rozmiar pliku.

> **Co jeśli potrzebuję innego DPI dla szerokości i wysokości?**  
> Po prostu zmień `setDpiX` i `setDpiY` niezależnie. Biblioteka respektuje wartości niejednorodne, co jest przydatne przy obrazach anamorficznych.

## Krok 3: Wykonaj konwersję SVG‑do‑PNG

Mając gotowe opcje, właściwa konwersja to jedno wywołanie statyczne. Użyjemy `java.nio.file.Paths`, aby zachować niezależność od platformy.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.Paths;

public class SvgToPng {
    public static void main(String[] args) throws Exception {
        // Paths to input SVG and output PNG
        var inputSvg  = Paths.get("YOUR_DIRECTORY/input.svg").toUri();
        var outputPng = Paths.get("YOUR_DIRECTORY/output.png").toUri();

        // Convert using the DPI settings we defined earlier
        Converter.convert(inputSvg, outputPng, conversionOptions);
    }
}
```

To wszystko — uruchom metodę `main`, a znajdziesz wyraźny PNG o 300 DPI w katalogu `YOUR_DIRECTORY`. Biblioteka automatycznie skaluje grafikę wektorową do podanego DPI, zachowując proporcje i czytelność tekstu.

## Krok 4: Zweryfikuj wynik (Opcjonalnie, ale zalecane)

Krótka kontrola może uchronić Cię przed problemami później. Otwórz wygenerowany PNG w dowolnym przeglądarce obrazów, która wyświetla metadane DPI (np. Photoshop, GIMP lub nawet zakładka „Szczegóły” w Eksploratorze Windows). Powinieneś zobaczyć **300 DPI** pod rozdzielczością poziomą i pionową.

Jeśli plik wygląda na rozmyty, sprawdź:

1. Czy oryginalny SVG nie jest niskiej rozdzielczości (pliki wektorowe są niezależne od rozdzielczości, ale osadzone w nich obrazy bitmapowe mogą ograniczać jakość).  
2. Czy naprawdę zapisałeś plik po ustawieniu DPI — IDE czasem buforują stare kompilacje.  
3. Czy opcje konwersji nie zostały nadpisane w innym miejscu kodu.

## Dlaczego DPI ma znaczenie przy eksporcie wysokiej rozdzielczości PNG

Możesz zapytać: „Po co w ogóle DPI? Czy PNG to nie tylko piksele?” Prawda jest taka, że DPI to *metadane*, które mówią aplikacjom downstream (szczególnie drukarskim) ile pikseli odpowiada jednemu calowi przestrzeni fizycznej. Jeśli przekażesz drukarce PNG 1200 × 800 bez odpowiedniego DPI, drukarka może przyjąć domyślną wartość (często 72 DPI) i powiększyć obraz, co skutkuje rozmytym wydrukiem.

Poprawne ustawienie DPI to także zysk wydajnościowy: unikasz późniejszego skalowania obrazów rastrowych, co może być kosztowne obliczeniowo i pogarszać jakość.

## Przypadki brzegowe i typowe pułapki

| Sytuacja | Na co zwrócić uwagę | Jak naprawić |
|----------|---------------------|--------------|
| **SVG zawiera osadzone obrazy bitmapowe** | Osadzona bitmapa może być niskiej rozdzielczości, co spowoduje pikselowany PNG nawet przy wysokim DPI. | Zamień bitmapę na wersję o wyższej rozdzielczości lub edytuj SVG, aby odwoływał się do zewnętrznego obrazu. |
| **Wysokie wartości DPI (np. 1200 DPI)** | Zużycie pamięci rośnie; możesz napotkać `OutOfMemoryError`. | Zwiększ rozmiar sterty JVM (`-Xmx2g`) lub ogranicz DPI do rozsądnego maksimum dla swojego przypadku użycia. |
| **Niekwadratowe piksele** | Niektóre wyświetlacze interpretują DPI inaczej, co prowadzi do rozciągniętych obrazów. | Upewnij się, że `setDpiX` równa się `setDpiY`, chyba że masz konkretny powód, by je różnić. |
| **Brakujące czcionki** | Tekst w SVG może przejść na domyślną czcionkę, zmieniając układ. | Osadź czcionki w SVG lub zainstaluj wymagane czcionki na maszynie uruchomieniowej. |

## Szybkie podsumowanie (jednym zdaniem)

Aby **jak ustawić DPI** przy konwersji SVG‑do‑PNG, utwórz obiekt `ImageConversionOptions`, ustaw `dpiX`/`dpiY` i wywołaj `Converter.convert` z biblioteki Aspose.HTML for Java.

## Kolejne kroki i tematy powiązane

- **Przetwarzanie wsadowe:** Przejdź po katalogu z plikami SVG i zastosuj te same ustawienia DPI.  
- **Dynamiczne DPI:** Odczytaj plik konfiguracyjny lub argument wiersza poleceń, aby ustawić DPI w czasie wykonywania.  
- **Alternatywne biblioteki:** Jeśli nie możesz użyć Aspose, rozważ **Batik** (Apache) lub **SVG Salamander**, choć mogą wymagać dodatkowego kodu do obsługi DPI.  
- **Eksport wysokiej rozdzielczości PNG** dla zasobów Android: połącz tę technikę z folderami Android `drawable‑hdpi`, `xhdpi` itd.

Śmiało eksperymentuj — wypróbuj 72 DPI dla miniatur internetowych, 600 DPI dla dużych wydruków lub 150 DPI jako kompromis. Kod pozostaje ten sam; zmieniają się tylko liczby.

---

![jak ustawić dpi](placeholder-image.png "Ilustracja ustawiania DPI w przepływie konwersji Java")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}