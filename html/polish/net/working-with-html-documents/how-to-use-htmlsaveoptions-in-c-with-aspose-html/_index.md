---
category: general
date: 2026-09-10
description: Dowiedz się, jak używać HtmlSaveOptions w C#, aby kontrolować style czcionek
  internetowych i zapisywać pliki HTML przy użyciu Aspose.HTML. Pełny przykład kodu
  oraz praktyczne wskazówki w zestawie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use htmlsaveoptions
- Aspose HTML library
- WebFontStyle flags
- HTMLDocument conversion
- C# save HTML
- Aspose.Html SaveOptions
language: pl
lastmod: 2026-09-10
og_description: Jak używać HtmlSaveOptions w C#, aby włączyć pogrubione i kursywne
  style czcionek internetowych przy zapisywaniu HTML przy użyciu Aspose.HTML. Zapoznaj
  się z pełnym przykładem i wskazówkami najlepszych praktyk.
og_image_alt: Screenshot showing how to use HtmlSaveOptions to save an HTML file in
  C#
og_title: Jak używać HtmlSaveOptions w C# z Aspose.HTML – przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  headline: How to use HtmlSaveOptions in C# with Aspose.HTML
  type: TechArticle
- description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  name: How to use HtmlSaveOptions in C# with Aspose.HTML
  steps:
  - name: Why configure WebFontStyle?
    text: 'When you export an HTML document, Aspose.HTML can embed web fonts that
      match the original styling. By setting `WebFontStyle`, you tell the exporter
      which font variants to include. This reduces the final file size when you only
      need specific styles and guarantees that the rendered output matches the '
  - name: 5.1 Controlling CSS embedding
    text: 'You can decide whether to embed CSS inline, keep external links, or embed
      everything:'
  - name: 5.2 Saving to a specific encoding
    text: '```csharp saveOptions.Encoding = Encoding.UTF8; ```'
  - name: 5.3 Handling large documents
    text: 'For very large HTML files, consider streaming the output to avoid high
      memory consumption:'
  - name: 5.4 Error handling best practice
    text: 'Wrap the entire workflow in a try‑catch block and log the exception details.
      This ensures that any I/O or parsing errors are captured:'
  - name: Expected console output
    text: '``` HTML saved successfully to ''YOUR_DIRECTORY/output.html''. ```'
  type: HowTo
tags:
- Aspose.HTML
- C#
- HTML processing
title: Jak używać HtmlSaveOptions w C# z Aspose.HTML
url: /pl/net/working-with-html-documents/how-to-use-htmlsaveoptions-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać HtmlSaveOptions w C# z Aspose.HTML

Jeśli potrzebujesz kontrolować sposób, w jaki Aspose.HTML zapisuje dokument HTML, **poznanie HtmlSaveOptions jest niezbędne**. Ten tutorial pokazuje krok po kroku, jak używać HtmlSaveOptions, aby włączyć pogrubione i kursywne style czcionek internetowych podczas zapisywania dokumentu.

Biblioteka Aspose HTML udostępnia rozbudowane API do ładowania, modyfikowania i eksportowania treści HTML. Po zakończeniu tego przewodnika będziesz w stanie:

* Załadować istniejący plik HTML do `HTMLDocument`.
* Skonfigurować `HtmlSaveOptions`, aby zastosować określone flagi `WebFontStyle`.
* Zapisać zmodyfikowany dokument w nowej lokalizacji lub do strumienia.
* Rozszerzyć rozwiązanie o inne style czcionek, własny CSS i obsługę błędów.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* .NET 6.0 lub nowszy zainstalowany.
* Ważną licencję na **Aspose.HTML for .NET** (bezpłatna wersja próbna wystarczy do tego przykładu).
* Visual Studio 2022 (lub dowolne IDE C#) do kompilacji i uruchomienia kodu.

Nie są wymagane dodatkowe pakiety NuGet poza `Aspose.HTML`.

## Krok 1: Utworzenie projektu i import przestrzeni nazw

Utwórz nowy projekt **Console App** i dodaj pakiet NuGet Aspose.HTML:

```bash
dotnet add package Aspose.HTML
```

Następnie, na początku pliku `Program.cs`, zaimportuj wymagane przestrzenie nazw:

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

Te przestrzenie nazw udostępniają typy `HTMLDocument`, `HtmlSaveOptions` i `WebFontStyle`, które będą używane w całym tutorialu.

## Krok 2: Załadowanie źródłowego dokumentu HTML

Pierwszym krokiem jest odczytanie HTML, który chcesz przetworzyć. Zastąp `"YOUR_DIRECTORY/input.html"` rzeczywistą ścieżką do swojego pliku.

```csharp
// Load the source HTML document from disk
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

`HTMLDocument` analizuje znacznik, buduje drzewo DOM i przygotowuje je do manipulacji. Jeśli plik nie istnieje, zostanie rzucony wyjątek, więc w kodzie produkcyjnym warto otoczyć to wywołanie blokiem try‑catch.

## Krok 3: Utworzenie i skonfigurowanie HtmlSaveOptions

`HtmlSaveOptions` pozwala precyzyjnie dostroić proces zapisu. Aby włączyć pogrubione i kursywne style czcionek internetowych, połącz odpowiednie flagi `WebFontStyle` przy użyciu operatora bitowego OR (`|`).

```csharp
// Create a new HtmlSaveOptions instance
HtmlSaveOptions saveOptions = new HtmlSaveOptions();

// Enable bold and italic web‑font styles (equivalent to the old FontStyle flags)
saveOptions.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

### Dlaczego konfigurować WebFontStyle?

Podczas eksportu dokumentu HTML, Aspose.HTML może osadzać czcionki internetowe odpowiadające oryginalnemu formatowaniu. Ustawiając `WebFontStyle`, określasz, które warianty czcionek mają zostać dołączone. Dzięki temu zmniejszasz rozmiar końcowego pliku, gdy potrzebujesz tylko wybranych stylów, i zapewniasz, że renderowany wynik będzie zgodny ze źródłem.

#### Typowe warianty

| Żądany styl | Odpowiednia flaga `WebFontStyle` |
|-------------|-----------------------------------|
| Normalny (regular) | `WebFontStyle.Regular` |
| Pogrubiony | `WebFontStyle.Bold` |
| Kursywa | `WebFontStyle.Italic` |
| Pogrubiony + Kursywa | `WebFontStyle.Bold | WebFontStyle.Italic` |
| Wszystkie warianty | `WebFontStyle.All` |

Możesz połączyć dowolną kombinację pasującą do Twojego scenariusza.

## Krok 4: Zapis dokumentu z skonfigurowanymi opcjami

Teraz zapisz dokument do nowego pliku. Metoda `Save` przyjmuje ścieżkę docelową oraz przygotowaną instancję `HtmlSaveOptions`.

```csharp
// Save the processed HTML using the configured options
document.Save("YOUR_DIRECTORY/output.html", saveOptions);
```

Jeśli potrzebujesz zapisać do strumienia pamięci (np. aby przesłać plik przez HTTP), użyj przeciążenia przyjmującego obiekt `Stream`:

```csharp
using (var stream = new MemoryStream())
{
    document.Save(stream, saveOptions);
    // Reset the position to read the content later
    stream.Position = 0;
    // Example: return the stream from a Web API endpoint
}
```

## Krok 5: Weryfikacja wyniku

Otwórz `output.html` w przeglądarce lub przejrzyj plik w edytorze tekstu. Powinieneś zobaczyć, że blok `<style>` zawiera reguły `@font-face` dla pogrubionych i kursywnych wariantów wszystkich czcionek internetowych użytych w oryginalnym dokumencie.

**Przykładowy fragment oczekiwanego wyniku:**

```html
<link rel="stylesheet" href="fonts/Roboto-Bold.woff2" type="font/woff2">
<link rel="stylesheet" href="fonts/Roboto-Italic.woff2" type="font/woff2">
```

Jeśli oryginalny HTML odwoływał się do rodziny czcionek, która posiadała jedynie wagę regularną, Aspose.HTML dołączy tylko ten plik, respektując konfigurację `WebFontStyle`.

## Zaawansowane: Użycie HtmlSaveOptions z dodatkowymi funkcjami

### 5.1 Kontrola osadzania CSS

Możesz zdecydować, czy osadzać CSS inline, pozostawić linki zewnętrzne, czy osadzić wszystko:

```csharp
saveOptions.CssSavingMode = CssSavingMode.EmbedAllCss;
```

### 5.2 Zapis z określonym kodowaniem

```csharp
saveOptions.Encoding = Encoding.UTF8;
```

### 5.3 Obsługa dużych dokumentów

W przypadku bardzo dużych plików HTML rozważ strumieniowy zapis wyjścia, aby uniknąć wysokiego zużycia pamięci:

```csharp
using (FileStream fs = new FileStream("large_output.html", FileMode.Create, FileAccess.Write))
{
    document.Save(fs, saveOptions);
}
```

### 5.4 Najlepsze praktyki obsługi błędów

Otocz cały przepływ pracy blokiem try‑catch i zaloguj szczegóły wyjątku. Dzięki temu wszelkie błędy I/O lub parsowania zostaną przechwycone:

```csharp
try
{
    // Load, configure, and save as shown earlier
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error processing HTML: {ex.Message}");
}
```

## Pro tip: Ponowne użycie HtmlSaveOptions przy wielu zapisach

Jeśli musisz zapisać kilka dokumentów z taką samą konfiguracją stylów czcionek, utwórz jedną instancję `HtmlSaveOptions` i używaj jej wielokrotnie. To zmniejsza narzut alokacji obiektów i zapewnia spójny wynik.

```csharp
HtmlSaveOptions sharedOptions = new HtmlSaveOptions
{
    WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
    CssSavingMode = CssSavingMode.EmbedAllCss
};

foreach (var file in Directory.GetFiles("input_folder", "*.html"))
{
    HTMLDocument doc = new HTMLDocument(file);
    string outputPath = Path.Combine("output_folder", Path.GetFileName(file));
    doc.Save(outputPath, sharedOptions);
}
```

## Pełny, uruchamialny przykład

Poniżej znajduje się kompletny program, który zawiera wszystkie omówione kroki. Skopiuj go do `Program.cs` i uruchom po dostosowaniu ścieżek plików.

```csharp
using System;
using System.IO;
using System.Text;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath = "YOUR_DIRECTORY/input.html";
        string outputPath = "YOUR_DIRECTORY/output.html";

        try
        {
            // Step 1: Load the source HTML document
            HTMLDocument document = new HTMLDocument(inputPath);

            // Step 2: Create HtmlSaveOptions and enable bold + italic web‑font styles
            HtmlSaveOptions saveOptions = new HtmlSaveOptions
            {
                WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
                // Optional: embed all CSS and use UTF‑8 encoding
                CssSavingMode = CssSavingMode.EmbedAllCss,
                Encoding = Encoding.UTF8
            };

            // Step 3: Save the document with the configured options
            document.Save(outputPath, saveOptions);

            Console.WriteLine($"HTML saved successfully to '{outputPath}'.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### Oczekiwany wynik w konsoli

```
HTML saved successfully to 'YOUR_DIRECTORY/output.html'.
```

Otwórz wygenerowany `output.html`, aby potwierdzić, że pogrubione i kursywne style czcionek internetowych są obecne.

## Podsumowanie

Teraz wiesz **jak używać HtmlSaveOptions**, aby kontrolować osadzanie czcionek internetowych, obsługę CSS i kodowanie przy zapisie HTML przy użyciu biblioteki Aspose HTML w C#. Konfigurując flagi `WebFontStyle`, możesz dostosować wyjście tak, aby zawierało tylko potrzebne warianty czcionek, co poprawia wydajność i zmniejsza rozmiar pliku.

Od tego momentu możesz eksplorować inne właściwości `HtmlSaveOptions`, takie jak `ImageSavingMode`, `JavaScriptSavingMode`, lub łączyć wiele opcji w złożonych pipeline’ach konwersji. Eksperymentuj z zapisem do strumieni w API webowych lub zintegrować ten przepływ pracy w większym systemie generowania dokumentów.

---


## Co powinieneś nauczyć się dalej?


Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletny, działający kod wraz z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i poznać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak zapisać HTML przy użyciu Aspose.Html – Kompletny przewodnik C#](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [Jak używać Aspose do renderowania HTML do PNG w C#](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-in-c/)
- [Jak używać Aspose do renderowania HTML do PNG – Przewodnik krok po kroku](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}