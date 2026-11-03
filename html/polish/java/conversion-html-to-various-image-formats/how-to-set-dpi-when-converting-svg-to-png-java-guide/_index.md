---
category: general
date: 2026-05-06
description: Jak ustawić DPI przy konwersji SVG do PNG w wysokiej rozdzielczości w
  Javie przy użyciu Aspose.HTML. Dowiedz się, jak konwertować SVG na PNG, eksportować
  SVG jako PNG oraz przekształcać wektor w raster.
draft: false
keywords:
- how to set dpi
- convert svg to png
- how to convert svg
- export svg as png
- convert vector to raster
language: pl
og_description: Jak ustawić DPI przy konwersji SVG do PNG w wysokiej rozdzielczości
  w Javie przy użyciu Aspose.HTML. Uzyskaj kod krok po kroku oraz wskazówki ekspertów.
og_title: Jak ustawić DPI przy konwertowaniu SVG na PNG – Poradnik Java
tags:
- Java
- Aspose.HTML
- Image Conversion
title: Jak ustawić DPI przy konwertowaniu SVG na PNG – przewodnik Java
url: /pl/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ustawić DPI przy konwersji SVG do PNG – Przewodnik Java

Zastanawiałeś się kiedyś **jak ustawić DPI** przy konwersji SVG‑do‑PNG i uzyskać wyraźny, gotowy do druku obraz? Nie jesteś sam. Wielu programistów napotyka problem, gdy wyeksportowany PNG jest rozmyty, ponieważ domyślne DPI (zwykle 96) po prostu nie wystarcza do profesjonalnego wydruku.

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokazuje **jak ustawić DPI** przy użyciu Aspose.HTML dla Javy. Po zakończeniu będziesz w stanie **konwertować SVG do PNG**, **eksportować SVG jako PNG**, a nawet **konwertować wektor na raster** z dowolnym DPI, którego potrzebujesz — bez tajemnic, po prostu przejrzysty kod.

## Czego się nauczysz

- Dokładne kroki konfigurowania DPI przed konwersją.
- Dlaczego DPI ma znaczenie, gdy **konwertujesz wektor na raster**.
- Jak **konwertować SVG do PNG** w jednej linii kodu.
- Wskazówki dotyczące obsługi dużych plików SVG i przetwarzania wsadowego.
- Pełny, kompilowalny program, który możesz od razu wkleić do swojego projektu.

## Wymagania wstępne

- Java 17 lub nowsza (najlepiej najnowsza wersja LTS).
- Maven lub Gradle do pobrania biblioteki Aspose.HTML.
- Prosty plik SVG, który chcesz rasteryzować (np. `logo.svg`).
- IDE lub edytor tekstu — IntelliJ IDEA, VS Code, a nawet zwykły Notatnik się sprawdzi.

Nie są wymagane żadne dodatkowe narzędzia; biblioteka wykonuje całą ciężką pracę.

## Krok 1: Dodaj Aspose.HTML do swojego projektu

Na początek potrzebujesz pliku JAR Aspose.HTML. Jeśli używasz Maven, dodaj ten fragment do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Dla Gradle wygląda to tak:

```groovy
implementation 'com.aspose:aspose-html:23.10'
```

> **Pro tip:** Zawsze używaj najnowszej stabilnej wersji; nowsze wydania zawierają poprawki wydajności dla renderowania w wysokim DPI.

## Krok 2: Jak ustawić DPI dla konwersji

Teraz przechodzimy do sedna sprawy — **jak ustawić DPI**. Aspose.HTML udostępnia `ImageConversionOptions`, w którym możesz określić zarówno poziomą (`dpiX`), jak i pionową (`dpiY`) rozdzielczość. Ustawienie obu na `300` daje klasyczną gęstość druku.

```java
import com.aspose.html.converters.ImageConversionOptions;
import com.aspose.html.rendering.Converter;

public class SvgHighRes {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create conversion options
        ImageConversionOptions conversionOptions = new ImageConversionOptions();

        // 2️⃣ Set target DPI for high‑resolution output (300 dpi → crisp print quality)
        conversionOptions.setDpiX(300);
        conversionOptions.setDpiY(300);

        // 3️⃣ Convert the SVG file to a PNG using the configured options
        Converter.convertSvgToPng(
                "YOUR_DIRECTORY/logo.svg",        // source SVG
                "YOUR_DIRECTORY/logo_300dpi.png", // destination PNG
                conversionOptions);
    }
}
```

> **Dlaczego 300 dpi?** To de‑facto standard w profesjonalnym druku. Jeśli potrzebujesz obrazu gotowego do internetu, 72 dpi wystarczy, ale do ulotek lub broszur warto mieć przynajmniej 300 dpi.

### Podgląd obrazu

![Jak ustawić DPI przy konwersji SVG do PNG](https://example.com/placeholder.png "Jak ustawić DPI przy konwersji SVG do PNG")

*Powyższy obraz ilustruje różnicę między PNG o niskim DPI (po lewej) a wynikiem 300 dpi (po prawej).*

## Krok 3: Konwertuj SVG do PNG – Jedna linijka

Jeśli potrzebujesz szybkiego **konwertowania svg do png** bez manipulacji DPI, możesz całkowicie pominąć obiekt opcji:

```java
Converter.convertSvgToPng("logo.svg", "logo_default.png", null);
```

Przekazanie `null` mówi Aspose.HTML, aby użyło domyślnego DPI (zwykle 96). Jest to przydatne przy miniaturkach lub gdy nie zależy Ci na jakości druku.

## Krok 4: Zweryfikuj wynik – Eksportuj SVG jako PNG

Po zakończeniu konwersji otwórz wygenerowany PNG w dowolnym przeglądarce obrazów. Powinieneś zobaczyć obraz rastrowy, który odpowiada wymiarom oryginalnego wektora, ale teraz posiada ustawione DPI. Większość przeglądarek wyświetla DPI w właściwościach obrazu; w Windows kliknij prawym przyciskiem → Właściwości → Szczegóły.

Jeśli potrzebujesz programowo zweryfikować DPI, `ImageIO` w Javie może je odczytać:

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File("logo_300dpi.png"));
int dpi = (int) img.getProperty("dpi");
System.out.println("Exported PNG DPI: " + dpi);
```

> **Uwaga:** Nie wszystkie formaty obrazów przechowują metadane DPI; PNG tak, ale JPEG może wymagać dodatkowej obsługi.

## Przypadki brzegowe i warianty

### 1️⃣ Różne wartości DPI

Możesz się zastanawiać, „Co jeśli potrzebuję 600 dpi dla dużego plakatu?” Po prostu zmień liczby:

```java
conversionOptions.setDpiX(600);
conversionOptions.setDpiY(600);
```

Wyższe DPI oznacza większy rozmiar pliku, więc pamiętaj o ograniczeniach pamięci przy przetwarzaniu wielu plików.

### 2️⃣ Konwersja wsadowa folderu

Gdy masz dziesiątki plików SVG, otocz konwersję prostą pętlą:

```java
File dir = new File("YOUR_DIRECTORY");
for (File svg : dir.listFiles((d, name) -> name.endsWith(".svg"))) {
    String pngName = svg.getName().replace(".svg", "_300dpi.png");
    Converter.convertSvgToPng(svg.getAbsolutePath(),
                              new File(dir, pngName).getAbsolutePath(),
                              conversionOptions);
}
```

Ten wzorzec **konwertuje wektor na raster** masowo, oszczędzając godziny ręcznej pracy.

### 3️⃣ Obsługa przezroczystego tła

Jeśli Twój SVG zawiera przezroczystość i chcesz białe tło, najpierw wyrenderuj do `BufferedImage`, a następnie wypełnij tło:

```java
// Render SVG to BufferedImage with DPI
BufferedImage raster = Converter.convertSvgToImage(
        "logo.svg", conversionOptions);

// Fill background (optional)
Graphics2D g = raster.createGraphics();
g.setComposite(AlphaComposite.SrcOver);
g.setColor(Color.WHITE);
g.fillRect(0, 0, raster.getWidth(), raster.getHeight());
g.dispose();

// Write out PNG
ImageIO.write(raster, "png", new File("logo_whitebg.png"));
```

## Często zadawane pytania

**Q: Czy to działa na Linuxie?**  
A: Absolutnie. Aspose.HTML jest niezależny od platformy; po prostu upewnij się, że masz odpowiednie środowisko Java.

**Q: Co jeśli mój SVG odwołuje się do zewnętrznych obrazów?**  
A: Upewnij się, że te zasoby są dostępne poprzez ścieżki bezwzględne lub URL‑e; w przeciwnym razie renderer je pominie.

**Q: Czy mogę konwertować SVG do innych formatów rastrowych, takich jak JPEG lub BMP?**  
A: Tak. Użyj `Converter.convertSvgToJpeg` lub `Converter.convertSvgToBmp` z tym samym `ImageConversionOptions`.

## Porady profesjonalne dla wysokiej jakości rasteryzacji

- **Dopasuj DPI do końcowego rozmiaru wyjściowego.** Logo o szerokości 2 cali drukowane w 300 dpi wymaga szerokości 600 px (2 in × 300 dpi). Skaluj SVG odpowiednio przed konwersją, jeśli potrzebujesz konkretnego wymiaru w pikselach.
- **Zwróć uwagę na profil kolorów.** PNG‑y nie osadzają domyślnie profili ICC; jeśli zależy Ci na wierności kolorów, konwertuj do TIFF lub użyj biblioteki obsługującej osadzanie profili.
- **Ponownie używaj obiektu `ImageConversionOptions`** przy konwersji wielu plików — unika to niepotrzebnego tworzenia obiektów i może poprawić wydajność.

## Zakończenie

Teraz wiesz **jak ustawić DPI** dla konwersji SVG‑do‑PNG w Javie i widziałeś, jak to samo podejście pozwala **konwertować svg do png**, **eksportować svg jako png**, oraz ogólnie **konwertować wektor na raster** z pełną kontrolą nad rozdzielczością. Pełny przykład powyżej działa od razu, a dodatkowe wskazówki dają plan działania przy skalowaniu rozwiązania do projektów produkcyjnych.

Co dalej? Spróbuj zamienić wartość 300 dpi na 600 dpi, eksperymentuj z przetwarzaniem wsadowym lub odkryj inne formaty rastrowe. Te same zasady obowiązują — wystarczy zmienić metodę wyjścia i gotowe.

Masz trudny SVG lub pytanie dotyczące wydajności? Zostaw komentarz i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}