---
category: general
date: 2026-01-14
description: jak ustawić DPI przy konwertowaniu adresu URL na PNG. Dowiedz się, jak
  renderować HTML do PNG, ustawiać rozmiar widoku i zapisywać HTML jako PNG przy użyciu
  Aspose.HTML w Javie.
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: pl
og_description: jak ustawić DPI przy konwertowaniu adresu URL na PNG. Przewodnik krok
  po kroku, jak renderować HTML do PNG, kontrolować rozmiar widoku i zapisywać HTML
  jako PNG przy użyciu Aspose.HTML.
og_title: jak ustawić DPI – renderowanie HTML do PNG przy użyciu AsposeHTML
tags:
- AsposeHTML
- Java
- image rendering
title: jak ustawić dpi – renderowanie HTML do PNG przy użyciu AsposeHTML
url: /pl/java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak ustawić dpi – renderowanie HTML do PNG przy użyciu AsposeHTML

Zastanawiałeś się kiedyś **jak ustawić dpi** dla obrazu w stylu zrzutu ekranu generowanego ze strony internetowej? Może potrzebujesz PNG o 300 DPI do druku lub niskiej rozdzielczości miniaturki do aplikacji mobilnej. W obu przypadkach sztuczka polega na poinformowaniu silnika renderującego, jaką logiczną wartość DPI chcesz, a następnie pozwolić mu wykonać ciężką pracę.  

W tym samouczku pobierzemy żywy URL, wyrenderujemy go do pliku PNG, **ustawimy rozmiar viewportu**, dostosujemy DPI i w końcu **zapiszemy HTML jako PNG** — wszystko przy użyciu Aspose.HTML dla Javy. Bez zewnętrznych przeglądarek, bez nieporęcznych narzędzi wiersza poleceń — po prostu czysty kod Java, który możesz wkleić do dowolnego projektu Maven lub Gradle.

> **Pro tip:** Jeśli potrzebujesz tylko szybkiej miniaturki, możesz pozostawić DPI na 96 DPI (domyślne dla większości ekranów). Dla zasobów gotowych do druku podnieś je do 300 DPI lub wyżej.

![how dpi example](https://example.com/images/how-to-set-dpi.png "how to set dpi example")

## Czego będziesz potrzebować

- **Java 17** (lub dowolny nowszy JDK).  
- **Aspose.HTML for Java** 24.10 lub nowszy. Możesz pobrać go z Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- Połączenie internetowe, aby pobrać docelową stronę (przykład używa `https://example.com/sample.html`).  
- Uprawnienia do zapisu w folderze wyjściowym.

To wszystko — bez Selenium, bez headless Chrome. Aspose.HTML wykonuje renderowanie w‑procesie, co oznacza, że pozostajesz w JVM i unikasz kosztów uruchamiania przeglądarki.

## Krok 1 – Załaduj dokument HTML z URL

Najpierw tworzymy instancję `HTMLDocument`, wskazującą na stronę, którą chcemy przechwycić. Konstruktor automatycznie pobiera HTML, parsuje go i przygotowuje DOM.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*Dlaczego to ważne:* Ładując dokument bezpośrednio, pomijasz potrzebę osobnego klienta HTTP. Aspose.HTML respektuje przekierowania, ciasteczka i nawet podstawowe uwierzytelnianie, jeśli osadzisz poświadczenia w URL.

## Krok 2 – Zbuduj sandbox z żądanym DPI i viewportem

**Sandbox** to sposób Aspose.HTML na naśladowanie środowiska przeglądarki. Tutaj instruujemy go, aby udawał ekran 1280 × 720 i, co najważniejsze, ustawiamy **device DPI**. Zmiana DPI zmienia gęstość pikseli renderowanego obrazu bez zmiany rozmiaru logicznego.

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*Dlaczego możesz chcieć dostosować te wartości:*  
- **Viewport size** kontroluje zachowanie zapytań mediów CSS (`@media (max-width: …)`).  
- **Device DPI** wpływa na fizyczny rozmiar obrazu przy drukowaniu. Obraz 96 DPI wygląda dobrze na ekranach; obraz 300 DPI zachowuje ostrość na papierze.  

Jeśli potrzebujesz kwadratowej miniaturki, po prostu zmień `setViewportSize(500, 500)` i utrzymaj niskie DPI.

## Krok  – Wybierz PNG jako format wyjściowy

Aspose.HTML obsługuje kilka formatów rastrowych (PNG, JPEG, BMP, GIF). PNG jest bezstratny, co czyni go idealnym do zrzutów ekranu, gdzie chcesz zachować każdy piksel.

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

Możesz także dostosować poziom kompresji (`pngOptions.setCompressionLevel(9)`), jeśli martwisz się rozmiarem pliku.

## Krok 4 – Renderuj i zapisz obraz

Teraz instruujemy dokument, aby **zapisał** się jako obraz. Metoda `save` przyjmuje ścieżkę pliku oraz wcześniej skonfigurowane opcje.

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

Po zakończeniu programu znajdziesz plik PNG w `YOUR_DIRECTORY/sandboxed.png`. Otwórz go — jeśli ustawiłeś DPI na 300, metadane obrazu to odzwierciedlą, mimo że wymiary w pikselach pozostaną 1280 × 720.

## Krok 5 – Zweryfikuj DPI (Opcjonalnie, ale przydatne)

Jeśli chcesz podwójnie sprawdzić, że DPI zostało naprawdę zastosowane, możesz odczytać metadane PNG przy użyciu lekkiej biblioteki takiej jak **metadata‑extractor**:

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

Powinieneś zobaczyć `300` (lub wartość, którą ustawiłeś) wydrukowaną w konsoli. Ten krok nie jest wymagany do renderowania, ale jest szybkim sprawdzeniem poprawności, szczególnie gdy generujesz zasoby do przepływu pracy drukowania.

## Częste pytania i przypadki brzegowe

### „Co jeśli strona używa JavaScript do ładowania treści?”

Aspose.HTML wykonuje **ograniczony podzbiór** JavaScript. Dla większości statycznych stron działa od razu. Jeśli strona mocno polega na frameworkach po stronie klienta (React, Angular, Vue), może być konieczne wstępne renderowanie strony lub użycie przeglądarki headless. Jednak ustawianie DPI działa tak samo, gdy DOM jest gotowy.

### „Czy mogę renderować PDF zamiast PNG?”

Oczywiście. Zamień `ImageSaveOptions` na `PdfSaveOptions` i zmień rozszerzenie wyjściowe na `.pdf`. Ustawienie DPI nadal wpływa na rastrowy wygląd wszelkich osadzonych obrazów.

### „A co z wysokiej rozdzielczości zrzutami ekranu dla wyświetlaczy Retina?”

Po prostu podwój wymiary viewportu, zachowując DPI na 96 DPI, lub zachowaj viewport i podnieś DPI do 192. Wynikowy PNG będzie zawierał dwa razy więcej pikseli, dając efekt ostrego wyświetlacza Retina.

### „Czy muszę sprzątać zasoby?”

`HTMLDocument` implementuje `AutoCloseable`. W aplikacji produkcyjnej, otocz go blokiem try‑with‑resources:

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

## Pełny działający przykład (gotowy do kopiowania i wklejenia)

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Zamień `YOUR_DIRECTORY` na rzeczywisty folder na swoim komputerze.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

Uruchom klasę, a otrzymasz PNG, który respektuje ustawienie **how to set dpi**, które określiłeś.

## Zakończenie

Przeszliśmy przez **jak ustawić dpi** przy **renderowaniu HTML do PNG**, omówiliśmy krok **set viewport size** i pokazaliśmy, jak **zapisac HTML jako PNG** przy użyciu Aspose.HTML dla Javy. Najważniejsze wnioski to:

- Użyj **sandbox** do kontrolowania DPI i viewportu.  
- Wybierz odpowiednie **ImageSaveOptions** dla wyjścia bezstratnego.  
- Zweryfikuj metadane DPI, jeśli musisz zagwarantować jakość druku.  

Od tego miejsca możesz eksperymentować z różnymi wartościami DPI, większymi viewportami lub nawet przetwarzać wsadowo listę URLi. Chcesz przekonwertować całą witrynę na miniaturki PNG? Po prostu iteruj po tablicy URLi i ponownie użyj tej samej konfiguracji sandbox.

Szczęśliwego renderowania i niech Twoje zrzuty ekranu zawsze będą perfekcyjnie pikselowe!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}