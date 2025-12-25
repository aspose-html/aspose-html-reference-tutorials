---
date: 2025-12-25
description: „Dowiedz się, jak konwertować pliki EPUB na obrazy przy użyciu Aspose.HTML
  dla Javy i ustawiać niestandardowy rozmiar strony. Ten przewodnik krok po kroku
  obejmuje wymagania wstępne, importy pakietów oraz proces konwersji.”
linktitle: Specifying Image Save Options for EPUB to Image Conversion
second_title: Java HTML Processing with Aspose.HTML
title: Konwertuj EPUB na obraz przy użyciu Aspose.HTML dla Javy – ustaw niestandardowy
  rozmiar strony
url: /pl/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertowanie EPUB na Obraz przy użyciu Aspose.HTML for Java – Ustawienie Niestandardowego Rozmiaru Strony

## Quick Answers
- **Co oznacza „ustawienie niestandardowego rozmiaru strony”?** Pozwala określić szerokość i wysokość każdej wyjściowej strony obrazu.  
- **Czy mogę zmienić kolor tła obrazu?** Tak, możesz podać dowolny kolor przy użyciu `ImageSaveOptions`.  
- **Jakie formaty są obsługiwane?** JPEG, PNG, GIF i inne poprzez `ImageFormat`.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna wystarczy do testów; licencja komercyjna jest wymagana w produkcji.  
- **Jakiej wersji Javy potrzebuję?** Java 1.7 lub nowsza jest w pełni wspierana.

## Co oznacza „ustawienie niestandardowego rozmiaru strony” w konwersji EPUB na obraz?
Ustawienie niestandardowego rozmiaru strony oznacza, że kontrolujesz wymiary renderowanego obrazu (np. 3000 × 1000 pikseli). Jest to przydatne, gdy potrzebujesz wysokiej rozdzielczości zrzutów ekranu e‑booków lub gdy chcesz, aby wynik pasował do określonego układu.

## Dlaczego ustawiać niestandardowy rozmiar strony i zmieniać kolor tła obrazu?
Niestandardowe rozmiary stron dają elastyczność dla różnych docelowych wyświetlaczy — ekrany mobilne, gotowe do druku PDF‑y lub miniatury internetowe. Zmiana koloru tła pomaga dopasować się do identyfikacji wizualnej lub poprawić czytelność obrazów zawierających przezroczyste elementy.

## Prerequisites

Zanim rozpoczniesz **konwersję epub na obraz**, upewnij się, że masz następujące elementy:

1. **Java Environment** – Zestaw deweloperski Javy zainstalowany na Twoim komputerze. Jeśli nie masz jeszcze Javy, możesz ją pobrać [tutaj](https://www.java.com).
2. **Aspose.HTML for Java** – Biblioteka Aspose.HTML for Java. Pobierz najnowsze wydanie ze [strony Aspose.HTML for Java](https://releases.aspose.com/html/java/).

## Import Packages

Aby pracować z Aspose.HTML for Java, zaimportuj wymagane przestrzenie nazw:

```java
// Import the required Aspose.HTML for Java packages
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import java.io.FileInputStream;
```

## Step‑by‑Step Guide

### Step 1: Open an Existing EPUB File for Reading

```java
try (FileInputStream fileInputStream = new FileInputStream("input.epub")) {
```

Tutaj otwieramy źródłowy plik EPUB. Zamień `"input.epub"` na ścieżkę do swojego pliku e‑booka.

### Step 2: Initialize ImageSaveOptions with Custom Settings (set custom page size & change image background color)

```java
ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Jpeg);
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
Size size = new Size(
    Length.fromPixels(3000),
    Length.fromPixels(1000)
);
anyPage.setSize(size);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

W tym bloku **ustawiamy niestandardowy rozmiar strony** na 3000 × 1000 pikseli i zmieniamy tło na AliceBlue. Śmiało dostosuj `size` lub `Color` do potrzeb projektu (np. `Color.getWhite()` dla czystego białego tła).

### Step 3: Convert EPUB to Image

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    "output.jpg"
);
```

Ta linia wykonuje rzeczywistą konwersję. Plik wyjściowy (`"output.jpg"`) będzie zawierał renderowany obraz o określonych wymiarach i tle. Możesz także zmienić rozszerzenie na `.png`, jeśli wolisz **java convert epub png**.

### Step 4: Close Resources (handled automatically)

Instrukcja `try‑with‑resources` automatycznie zamyka `FileInputStream`, zapewniając, że żadne uchwyty plików nie pozostaną otwarte.

## Common Use Cases

- **Generowanie miniatur** dla bibliotek e‑booków.  
- **Tworzenie wysokiej rozdzielczości zrzutów ekranu** do dokumentacji lub materiałów marketingowych.  
- **Przetwarzanie wsadowe** dużych zbiorów EPUB‑ów na zasoby PNG/JPEG dla galerii internetowych.

## Tips & Best Practices

- **Pro tip:** Użyj `Length.fromInches()` lub `Length.fromCentimeters()`, jeśli wolisz jednostki fizyczne zamiast pikseli.  
- **Performance tip:** Dla dużych EPUB‑ów rozważ zwiększenie rozmiaru sterty JVM (`-Xmx2g`), aby uniknąć problemów z pamięcią.  
- **Error handling:** Owiń wywołanie konwersji w blok `try‑catch`, aby przechwycić `IOException` lub `AsposeException`.

## Frequently Asked Questions

**Q: Czy mogę konwertować pliki EPUB na inne formaty obrazu?**  
A: Tak, możesz określić formaty takie jak PNG lub GIF, zmieniając `ImageFormat.Jpeg` na `ImageFormat.Png` lub `ImageFormat.Gif`.

**Q: Czy Aspose.HTML for Java obsługuje EPUB3?**  
A: Absolutnie. Biblioteka w pełni wspiera EPUB3, umożliwiając pracę z najnowszymi standardami e‑booków.

**Q: Jak mogę obsłużyć błędy podczas procesu konwersji?**  
A: Zaimplementuj bloki `try‑catch` wokół kodu konwersji, aby przechwycić i zalogować wyjątki, zapewniając stabilność aplikacji.

**Q: Czy mogę dostosować rozmiar i jakość obrazu?**  
A: Tak, zmień obiekt `Size` dla wymiarów i użyj `options.setQuality(int)`, aby kontrolować jakość kompresji JPEG.

**Q: Czy Aspose.HTML for Java jest kompatybilny ze wszystkimi wersjami Javy?**  
A: Biblioteka działa z Java 1.7 i nowszymi, obejmując szeroki zakres środowisk programistycznych.

---

**Last Updated:** 2025-12-25  
**Tested With:** Aspose.HTML for Java 24.10  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}