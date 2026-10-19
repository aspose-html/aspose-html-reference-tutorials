---
category: general
date: 2026-03-25
description: Jak używać sandboxu do przechwytywania zrzutów ekranu stron internetowych
  przy użyciu Aspose.HTML dla Javy. Dowiedz się, jak zapisać HTML jako PNG, konwersję
  HTML na obraz oraz konwersję HTML na PNG w kilka minut.
draft: false
keywords:
- how to use sandbox
- capture webpage screenshot
- save html as png
- html to image conversion
- html to png conversion
language: pl
og_description: Jak używać sandboxa do przechwytywania zrzutu ekranu strony internetowej.
  Ten samouczek pokazuje, jak zapisać HTML jako PNG, obejmując konwersję HTML na obraz
  oraz konwersję HTML na PNG przy użyciu Aspose.HTML dla Javy.
og_title: Jak używać Sandbox do przechwytywania zrzutów ekranu stron internetowych
tags:
- Aspose.HTML
- Java
- Web Automation
title: Jak używać Sandbox do przechwytywania zrzutu ekranu strony internetowej
url: /pl/java/conversion-html-to-various-image-formats/how-to-use-sandbox-to-capture-webpage-screenshot/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać Sandbox do przechwytywania zrzutu ekranu strony internetowej

Używanie sandbox do przechwytywania zrzutu ekranu strony internetowej jest częstym wymaganiem, gdy potrzebny jest piksel‑idealny podgląd responsywnej strony. W tym przewodniku pokażemy także, jak **zapisać HTML jako PNG** przy użyciu Aspose.HTML for Java, obejmując wszystko od *konwersji html na obraz* po *konwersję html na png* w jednym, powtarzalnym przykładzie.

Wyobraź sobie, że testujesz stronę docelową kampanii marketingowej, która wygląda inaczej na telefonie, tablecie i komputerze stacjonarnym. Zamiast otwierać trzy przeglądarki, możesz uruchomić sandbox, skierować go na adres URL i natychmiast otrzymać PNG, który dokładnie odzwierciedla to, co wyrenderowałoby prawdziwe urządzenie. Po zakończeniu tego tutorialu będziesz mieć kompletny, uruchamialny program w Javie, który robi właśnie to, plus kilka praktycznych wskazówek, które możesz ponownie wykorzystać w swoich projektach.

## Czego będziesz potrzebować

- **Aspose.HTML for Java** (v23.9 lub nowszy). Biblioteka jest dostępna w Maven Central, więc dodanie zależności to pestka.  
- **JDK 11+** zainstalowane na Twoim komputerze.  
- IDE lub edytor tekstu według własnego wyboru (IntelliJ IDEA, VS Code, Eclipse… dowolny).  
- Dostęp do Internetu dla przykładowego adresu URL (`https://example.com/responsive.html`) lub zamień go na dowolną stronę, którą chcesz sfotografować.

Nie są wymagane dodatkowe binaria natywne ani przeglądarki headless — sandbox działa w całości w pamięci.

---

## Jak używać Sandbox – Krok 1: Zdefiniuj wirtualne urządzenie

Pierwszą rzeczą, którą robisz, jest poinformowanie sandbox, jakiego rozmiaru ekranu chcesz emulować. To właśnie tutaj główne słowo kluczowe błyszczy: *jak używać sandbox* dla konkretnego viewportu.

```java
// Step 1: Create a DeviceInfo that describes the virtual screen
DeviceInfo sandboxDevice = new DeviceInfo();
sandboxDevice.setWidth(800);               // width in pixels
sandboxDevice.setHeight(600);              // height in pixels
sandboxDevice.setDevicePixelRatio(1.0);    // 1 × for standard displays
sandboxDevice.setUserAgent("AsposeHTML/Java Sandbox");
```

**Dlaczego to ważne:**  
Ustawienie szerokości i wysokości zmusza silnik układu do traktowania strony tak, jakby była wyświetlana na monitorze 800×600. `devicePixelRatio` wpływa na to, jak zachowują się zapytania mediów oparte na CSS (`@media (min‑device‑pixel‑ratio: ...)`), zapewniając, że zrzut ekranu odpowiada rzeczywistemu doświadczeniu.

> **Wskazówka:** Jeśli potrzebujesz zrzutu ekranu w wysokiej rozdzielczości (np. wyświetlacze Retina), podnieś `devicePixelRatio` do `2.0` i odpowiednio zwiększ szerokość/wysokość.

---

## Przechwytywanie zrzutu ekranu strony – Krok 2: Załaduj stronę wewnątrz sandboxu

Teraz prosimy Aspose.HTML o pobranie zdalnego HTML i wyrenderowanie go w sandboxie, który właśnie zdefiniowaliśmy. Ten krok jest sercem **przechwytywania zrzutu ekranu strony**.

```java
// Step 2: Load the remote HTML page using the sandboxed environment
HTMLDocument document = new HTMLDocument(
        "https://example.com/responsive.html",
        new HTMLDocumentLoadOptions(new Sandbox(sandboxDevice)));
```

**Co dzieje się pod maską?**  
`HTMLDocumentLoadOptions` otrzymuje instancję `Sandbox`, która zawiera nasz `DeviceInfo`. Biblioteka tworzy następnie kontekst renderowania headless, który respektuje viewport, ciąg user‑agent oraz wszelki JavaScript, który strona może wykonać — *wszystko bez uruchamiania Chrome czy Firefox*.

Jeśli docelowa strona wymaga uwierzytelnienia, możesz wstrzyknąć ciasteczka lub niestandardowe nagłówki za pomocą `HTMLDocumentLoadOptions`. To przydatny przypadek brzegowy, gdy pracujesz z portalami intranetowymi.

---

## Zapisz HTML jako PNG – Krok 3: Konwertuj wyrenderowany dokument na obraz

Po wyrenderowaniu strony, ostatnim elementem jest **zapisanie HTML jako PNG**. To właściwy krok *konwersji html na png*.

```java
// Step 3: Convert the rendered document to PNG and write it to disk
try (FileOutputStream out = new FileOutputStream("output/responsive_page.png")) {
    Converter.convertDocument(
            document,
            new ConversionOptions(ConversionFormat.PNG),
            out);
}
```

Gdy `Converter` zakończy działanie, znajdziesz plik o nazwie `responsive_page.png` w folderze `output`. Otwórz go, a zobaczysz dokładnie to, jak strona wyglądała przy 800×600 pikselach — bez interfejsu przeglądarki, bez pasków przewijania, tylko czyste renderowanie.

**Typowe pułapki:**  
- **Błędy uprawnień do plików:** Upewnij się, że katalog istnieje (`output/` w przykładzie) i że Twój proces ma prawo do zapisu.  
- **Duże strony:** Bardzo wysokie strony mogą generować ogromne pliki PNG; możesz ograniczyć wysokość w `DeviceInfo` lub przyciąć po konwersji.  
- **Dynamiczna zawartość:** Jeśli strona ładuje dane przez AJAX po początkowym załadowaniu, może być konieczne wprowadzenie krótkiego opóźnienia (`Thread.sleep(2000)`) przed konwersją, lub użycie `HTMLDocumentLoadOptions.setWaitForResources(true)`.

---

### konwersja html na obraz – Opcje zaawansowane

Aspose.HTML oferuje kilka ustawień, które możesz dostosować, aby precyzyjnie dopasować **konwersję html na obraz**:

| Opcja | Opis | Kiedy używać |
|--------|------|--------------|
| `ConversionOptions.setQuality(int)` | Ustawia poziom kompresji PNG (0‑100). | Zmniejsz rozmiar pliku dla zasobów webowych. |
| `ConversionOptions.setBackgroundColor(Color)` | Wymusza kolor tła (domyślnie transparentny). | Przydatne, gdy strona ma przezroczyste sekcje. |
| `ConversionOptions.setPageSize(PageSize)` | Nadpisuje rozmiar sandboxu dla obrazu wyjściowego. | Tworzenie miniatur o innej rozdzielczości. |

Poniżej szybki fragment kodu, który ustawia białe tło i jakość 90 %:

```java
ConversionOptions pngOptions = new ConversionOptions(ConversionFormat.PNG);
pngOptions.setBackgroundColor(java.awt.Color.WHITE);
pngOptions.setQuality(90);

try (FileOutputStream out = new FileOutputStream("output/white_bg_page.png")) {
    Converter.convertDocument(document, pngOptions, out);
}
```

---

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny program, który możesz skopiować i wkleić do pliku `SandboxResponsiveExample.java` i uruchomić:

```java
import com.aspose.html.devices.DeviceInfo;
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.ConversionOptions;
import com.aspose.html.converters.ConversionFormat;
import com.aspose.html.render.HTMLDocument;
import com.aspose.html.render.HTMLDocumentLoadOptions;
import com.aspose.html.render.Sandbox;

import java.io.FileOutputStream;

public class SandboxResponsiveExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Define a sandbox with the desired viewport (800×600) and device pixel ratio
        DeviceInfo sandboxDevice = new DeviceInfo();
        sandboxDevice.setWidth(800);
        sandboxDevice.setHeight(600);
        sandboxDevice.setDevicePixelRatio(1.0);
        sandboxDevice.setUserAgent("AsposeHTML/Java Sandbox");

        // Step 2: Load the remote HTML page inside the sandboxed environment
        HTMLDocument document = new HTMLDocument(
                "https://example.com/responsive.html",
                new HTMLDocumentLoadOptions(new Sandbox(sandboxDevice)));

        // Step 3: Convert the document to PNG – the output reflects exactly how the page looks on the defined screen size
        try (FileOutputStream out = new FileOutputStream("output/responsive_page.png")) {
            Converter.convertDocument(
                    document,
                    new ConversionOptions(ConversionFormat.PNG),
                    out);
        }

        System.out.println("Screenshot saved to output/responsive_page.png");
    }
}
```

Uruchomienie programu wypisuje linię potwierdzającą i zapisuje PNG w folderze `output`. Otwórz plik, a zobaczysz wierne odwzorowanie zdalnej strony w dokładnie określonym rozmiarze.

---

## Najczęściej zadawane pytania

**P: Czy to działa z lokalnymi plikami HTML?**  
O: Zdecydowanie tak. Zamień URL na `file://` URI lub przekaż ścieżkę `java.io.File` do konstruktora `HTMLDocument`.

**P: Co jeśli potrzebuję PDF zamiast PNG?**  
O: Zamień `ConversionFormat.PNG` na `ConversionFormat.PDF`. Reszta kodu pozostaje bez zmian.

**P: Czy mogę zrobić zrzut całej strony (przewijanej)?**  
O: Ustaw wysokość `DeviceInfo` na wysokość przewijania strony (`document.getDocumentElement().getScrollHeight()`) przed konwersją, lub użyj `ConversionOptions.setPageSize`, aby powiększyć płótno.

---

## Podsumowanie

Teraz wiesz, **jak używać sandbox** do przechwytywania zrzutu ekranu strony internetowej, zapisywania HTML jako PNG oraz wykonywania niezawodnej konwersji html na obraz przy użyciu Aspose.HTML for Java. Podejście jest lekkie, w pełni programowalne i omija obciążenie tradycyjnych przeglądarek headless.

Co dalej? Spróbuj zamienić wyjście PNG na PDF, eksperymentuj z różnymi współczynnikami `devicePixelRatio`, aby naśladować wyświetlacze Retina, lub zautomatyzuj przetwarzanie wsadowe dziesiątek adresów URL. Ta sama technika sandbox może być również wykorzystana do **konwersji html na png** w pipeline’ach CI, testach regresji wizualnej lub generowaniu miniatur dla systemu zarządzania treścią.

Śmiało zostaw komentarz, jeśli napotkasz problemy, i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}