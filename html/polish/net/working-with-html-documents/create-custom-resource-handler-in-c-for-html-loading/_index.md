---
category: general
date: 2026-08-15
description: Utwórz własny handler zasobów w C#, aby zarządzać zasobami HTML, takimi
  jak obrazy i CSS. Poznaj HTMLLoadOptions, strumienie pamięci oraz ładowanie HTMLDocument.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: pl
lastmod: 2026-08-15
og_description: Utwórz własny obsługujący zasoby w C#, aby kontrolować sposób strumieniowania
  zasobów HTML. Ten tutorial pokazuje konfigurację HTMLLoadOptions, obsługę strumienia
  pamięci oraz ładowanie HTMLDocument z własną logiką.
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: Utwórz własny obsługiwacz zasobów w C# – pełny przewodnik po zarządzaniu
  zasobami HTML
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: Utwórz własny handler zasobów w C# do ładowania HTML
url: /pl/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create custom resource handler in C# for HTML loading

Jeśli potrzebujesz **create custom resource handler** dla plików HTML, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Nauczysz się przechwytywać obrazy, CSS i inne zasoby podczas ładowania dokumentu HTML, używając `HTMLLoadOptions` oraz strumienia opartego na pamięci.

Tutorial obejmuje wszystko, co potrzebne do wdrożenia wielokrotnego użytku handlera, skonfigurowania opcji ładowania i weryfikacji, że zasoby są prawidłowo przechwytywane. Nie potrzebna jest żadna zewnętrzna dokumentacja — wystarczy poniższy kod i wyjaśnienia.

## Wymagania wstępne

- .NET 6.0 lub nowszy
- Podstawowa znajomość C#
- Odwołanie do biblioteki przetwarzania HTML, która udostępnia `HTMLDocument`, `HtmlLoadOptions` i `ResourceHandler` (np. GroupDocs.Viewer for .NET)

## Przegląd rozwiązania

We will:

1. **Create a custom resource handler** poprzez dziedziczenie po `ResourceHandler`.
2. Skonfiguruj `HTMLLoadOptions`, aby używał handlera.
3. Załaduj plik HTML za pomocą `HTMLDocument`, podczas gdy handler dostarcza strumień dla każdego zasobu.
4. (Opcjonalnie) Zapisz otrzymane zasoby na dysku w celu weryfikacji.

Każdy krok zawiera pełny kod źródłowy oraz wyjaśnienie.

## Krok 1: Zdefiniuj klasę własnego handlera zasobów

Utworzenie własnego handlera oznacza nadpisanie metody `HandleResource`, aby biblioteka mogła zapisywać bajty zasobu do strumienia, którym sterujesz. Użycie `MemoryStream` utrzymuje dane w pamięci, co jest idealne do testowania lub dalszego przetwarzania.

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**Dlaczego to ważne:**  
Nadpisanie `HandleResource` daje pełną kontrolę nad tym, gdzie trafiają dane zasobu. Jeśli później będziesz musiał buforować obrazy, przekształcać CSS lub rejestrować użycie zasobów, możesz zamienić `MemoryStream` na dowolną własną implementację strumienia.

## Krok 2: Skonfiguruj `HTMLLoadOptions`, aby używał handlera

`HTMLLoadOptions` pozwala podłączyć handler do potoku ładowania. Ustawienie właściwości `ResourceHandler` informuje podgląd, aby wywoływał `MyHandler` dla każdego zewnętrznego zasobu.

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**Dlaczego to ważne:**  
Bez przypisania `ResourceHandler` podgląd zapisywałby zasoby w domyślnej lokalizacji (często w folderze tymczasowym). Określając własny handler, **create custom resource handler** zachowanie, które jest zgodne ze strategią przechowywania w Twojej aplikacji.

## Krok 3: Załaduj dokument HTML z skonfigurowanymi opcjami

Teraz załaduj plik HTML. Podgląd wywoła `MyHandler.HandleResource` dla każdego napotkanego zasobu.

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

W tym momencie zawartość HTML jest parsowana, a wszystkie zewnętrzne zasoby zostały przesłane do buforów pamięci dostarczonych przez `MyHandler`.

## Krok 4 (opcjonalnie): Uzyskaj dostęp do przechwyconych zasobów

Jeśli potrzebujesz przejrzeć lub zachować zasoby, możesz zmodyfikować `MyHandler`, aby przechowywał każdy `MemoryStream` w słowniku indeksowanym nazwą zasobu.

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

Po załadowaniu możesz iterować po `handler.Resources` i zapisywać każdy na dysk:

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**Dlaczego to ważne:**  
Przechowywanie zasobów umożliwia przetwarzanie po‑załadowaniu, takie jak optymalizacja obrazów, minifikacja CSS czy archiwizacja. Daje to także namacalną weryfikację, że logika **create custom resource handler** działa zgodnie z zamierzeniami.

## Krok 5: Sprzątanie

Zarówno `HTMLDocument`, jak i wszelkie strumienie powinny być zwalniane, aby zwolnić zasoby niezarządzane.

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## Pełny przykład do uruchomienia

Poniżej znajduje się samodzielny program, który demonstruje wszystkie kroki od definicji klasy po wyodrębnianie zasobów.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**Oczekiwany wynik**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

Konsola wypisuje każdy zasób, który podgląd przesłał przez Twój własny handler, potwierdzając, że przepływ pracy **create custom resource handler** zakończył się sukcesem.

## Częste pytania i przypadki brzegowe

| Question | Answer |
|----------|--------|
| *Co zrobić, gdy zasób jest duży (np. obraz wysokiej rozdzielczości)?* | Zastąp `MemoryStream` `FileStream` wskazującym na folder tymczasowy. Zapobiega to nadmiernemu zużyciu pamięci. |
| *Czy mogę filtrować zasoby według typu?* | Wewnątrz `HandleResource` sprawdź `info.MimeType` lub `info.Extension` i zwróć `null` dla niechcianych typów. Zwrócenie `null` informuje podgląd, aby pominął zasób. |
| *Czy wymagana jest bezpieczeństwo wątkowe?* | Jeśli ta sama instancja handlera jest używana w wielu równoczesnych ładowaniach, zabezpiecz słownik `Resources` przy pomocy blokady lub użyj kolekcji współbieżnej. |
| *Jak obsługiwać względne adresy URL?* | `ResourceInfo` zawiera oryginalny URL; możesz połączyć go ze ścieżką bazową pliku HTML, aby rozwiązać względne odwołania przed zapisaniem. |

## Zakończenie

Teraz wiesz, jak **create custom resource handler** w C# dla ładowania HTML, skonfigurować `HTMLLoadOptions`, przechwycić przesyłane zasoby i odpowiednio je zwolnić. Ten wzorzec daje pełną kontrolę nad zarządzaniem zasobami, umożliwiając scenariusze takie jak przetwarzanie obrazów w locie, przepisywanie CSS czy bezpieczne przechowywanie.

Następnie, zapoznaj się z powiązanymi tematami, takimi jak **HTMLDocument loading** z różnymi opcjami renderowania, lub rozszerz handler do implementacji **C# resource handler**, które zapisują bezpośrednio w chmurze. Eksperymentuj z metodą `HandleResource` handlera, aby dopasować ją do konkretnego przepływu zasobów w Twoim projekcie.

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletny działający kod z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Utwórz HTML z ciągu znaków w C# – Przewodnik po Custom Resource Handler](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Custom Resource Handler w C# – Tutorial konwersji HTML do ZIP](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [Jak zapisać HTML w C# – Kompletny przewodnik z użyciem Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}