---
category: general
date: 2026-02-13
description: Dowiedz się, jak zbudować własny obsługujący zasoby w C#, aby konwertować
  HTML do archiwum ZIP, tworząc zip w pamięci przy użyciu Aspose.HTML – przewodnik
  krok po kroku.
draft: false
keywords:
- custom resource handler
- convert html zip archive
- create zip from memory
- Aspose HTML
- in‑memory streaming
- C# zip compression
language: pl
og_description: Odkryj kompletny kod C# umożliwiający użycie własnego obsługiwacza
  zasobów do konwersji HTML w archiwum ZIP bezpośrednio w pamięci.
og_title: Niestandardowy obsługiwacz zasobów – konwertuj HTML do ZIP z pamięci
tags:
- C#
- Aspose.HTML
- ZipArchive
- MemoryStream
title: Niestandardowy obsługiwacz zasobów w C# – konwersja HTML do archiwum ZIP z
  pamięci
url: /pl/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-archive-fro/
---

unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obsługa zasobów niestandardowych – Konwersja HTML do archiwum ZIP z pamięci

Czy kiedykolwiek potrzebowałeś **custom resource handler**, aby pobrać każdy obraz, plik CSS lub skrypt, który strona HTML pobiera, a następnie spakować wszystko do ZIP bez zapisywania na dysku? Nie jesteś jedyny. W wielu scenariuszach automatyzacji sieciowej lub szablonów e‑mail chcesz mieć całą stronę spakowaną jako pojedynczy, przenośny pakiet i wolisz trzymać wszystko w RAM-ie dla szybkości i bezpieczeństwa.

W tym samouczku przeprowadzimy Cię przez kompletny, działający przykład, który pokazuje dokładnie, jak **convert HTML zip archive** przy użyciu **custom resource handler**, a następnie **create zip from memory** z wykorzystaniem `System.IO.Compression` w .NET. Po zakończeniu będziesz mieć samodzielną metodę, którą możesz wkleić do dowolnego projektu C# używającego Aspose.HTML.

## Czego będziesz potrzebować

- .NET 6+ (lub .NET Framework 4.7.2+)  
- Aspose.HTML for .NET (pakiet NuGet `Aspose.HTML`)  
- Podstawowa znajomość strumieni i klasy `ZipArchive`  

Bez zewnętrznych narzędzi, bez plików tymczasowych, wyłącznie czyste przetwarzanie w pamięci.

## Krok 1: Zdefiniuj obsługę zasobów niestandardowych

Serce rozwiązania to klasa dziedzicząca po `Aspose.Html.ResourceHandler`. Jej zadaniem jest dostarczenie świeżego `Stream` dla każdego zewnętrznego zasobu, którego żąda silnik HTML. Zwracając nowy `MemoryStream` za każdym razem, utrzymujemy dane odizolowane i gotowe do późniejszego pakowania.

```csharp
using System.IO;
using Aspose.Html;

// Step 1 – Custom handler that stores resources in memory
class MemoryResourceHandler : ResourceHandler
{
    // The framework calls this method for every external resource (images, CSS, etc.)
    public override Stream HandleResource(Resource resource)
    {
        // We give the engine an empty stream; later we’ll fill it with the actual bytes.
        // Using MemoryStream means everything stays in RAM.
        return new MemoryStream();
    }
}
```

**Dlaczego to ważne:**  
Jeśli pozwolisz Aspose.HTML zapisywać zasoby na dysku, będziesz musiał je później usuwać. Obsługa w pamięci eliminuje narzut I/O i sprawia, że kod jest bezpieczny w środowiskach sandboxowych (np. Azure Functions).

## Krok 2: Załaduj dokument HTML

Następnie wskaż Aspose.HTML na plik HTML, który chcesz spakować. Dokument może znajdować się na dysku, pod adresem URL lub być surowym ciągiem znaków. Tutaj używamy ścieżki pliku dla prostoty.

```csharp
using Aspose.Html;

// Step 2 – Load the source HTML
HtmlDocument document = new HtmlDocument("YOUR_DIRECTORY/input.html");
```

> **Pro tip:** Jeśli Twój HTML odwołuje się do zasobów względnych, upewnij się, że `input.html` znajduje się w tym samym folderze co te zasoby, w przeciwnym razie obsługa nie będzie w stanie ich zlokalizować.

## Krok 3: Podłącz obsługę i zapisz do MemoryStream

Teraz tworzymy instancję obsługi i informujemy Aspose.HTML, aby jej używał poprzez `HtmlSaveOptions.OutputStorage`. Wynikowy HTML (w tym przepisane URL‑e zasobów) trafia do `MemoryStream`.

```csharp
using Aspose.Html.Saving;
using System.IO;

// Step 3 – Prepare the handler and an in‑memory buffer for the final HTML
var resourceHandler = new MemoryResourceHandler();

using (MemoryStream htmlMemoryStream = new MemoryStream())
{
    document.Save(htmlMemoryStream, new HtmlSaveOptions
    {
        OutputStorage = resourceHandler // redirects all resources to the handler
    });

    // At this point htmlMemoryStream contains the full HTML file,
    // while each external resource resides in the streams returned by the handler.
```

**Co się dzieje pod maską?**  
Gdy wywoływane jest `document.Save`, Aspose.HTML pyta `MemoryResourceHandler` o strumień dla każdego zasobu. Ponieważ zwracamy puste `MemoryStream`‑y, silnik zapisuje surowe bajty bezpośrednio w pamięci. Żadne pliki tymczasowe nie są tworzone.

## Krok 4: Zbuduj archiwum ZIP całkowicie w pamięci

Teraz najciekawsza część: stworzymy `ZipArchive`, który będzie mieszkał w innym `MemoryStream`. To pozwala **create zip from memory** bez dotykania systemu plików.

```csharp
    // Step 4 – Build the ZIP archive in memory
    using (MemoryStream zipMemoryStream = new MemoryStream())
    using (var zipArchive = new ZipArchive(zipMemoryStream, ZipArchiveMode.Create, leaveOpen: true))
    {
        // 4a – Add the main HTML file
        var htmlEntry = zipArchive.CreateEntry("index.html");
        using (var entryStream = htmlEntry.Open())
        {
            // Reset the position of the HTML stream before copying
            htmlMemoryStream.Position = 0;
            htmlMemoryStream.CopyTo(entryStream);
        }

        // 4b – Add each resource that the handler captured
        // The handler stored each resource in a fresh MemoryStream, which we can enumerate.
        // For demonstration, assume we kept a list of those streams (you could store them in a dictionary).
        // Example placeholder – replace with your actual collection:
        // foreach (var kvp in capturedResources)
        // {
        //     var resourceEntry = zipArchive.CreateEntry(kvp.Key); // kvp.Key = relative path
        //     using var entry = resourceEntry.Open();
        //     kvp.Value.Position = 0;
        //     kvp.Value.CopyTo(entry);
        // }

        // When we’re done, flush everything
        zipArchive.Dispose(); // optional because of using, but makes intent clear
    }

    // At this stage zipMemoryStream holds the complete ZIP file.
    // You can return it, write it to a response stream, or save it to disk if you wish.
}
```

> **Note:** Zakomentowana sekcja pokazuje, jak można zbierać strumienie wewnątrz `MemoryResourceHandler`. W scenariuszu produkcyjnym przechowywałbyś każdy `MemoryStream` w słowniku kluczowanym oryginalnym URL‑em zasobu, a potem iterował tutaj, aby dodać je do archiwum.

**Dlaczego trzymać ZIP w pamięci?**  
Przechowywanie archiwum w `MemoryStream` ułatwia bezpośrednie wysłanie go do klienta HTTP (`FileResult` w ASP.NET Core) lub przesłanie do chmury bez pliku pośredniego.

## Krok 5: (Opcjonalnie) Zapisz ZIP na dysku

Jeśli nadal potrzebujesz fizycznego pliku — być może do debugowania — po prostu zapisz `zipMemoryStream` na dysk:

```csharp
// Optional: write the in‑memory ZIP to a file for inspection
File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipMemoryStream.ToArray());
```

## Pełny działający przykład

Łącząc wszystko razem, oto gotowy do skopiowania program, który **converts HTML to a ZIP archive** w całości w pamięci.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class MemoryResourceHandler : ResourceHandler
{
    // Capture each resource in a dictionary for later retrieval
    public static readonly System.Collections.Generic.Dictionary<string, MemoryStream> Captured = new();

    public override Stream HandleResource(Resource resource)
    {
        var ms = new MemoryStream();
        // Store the stream using the resource's absolute URL as the key
        Captured[resource.Uri.AbsoluteUri] = ms;
        return ms;
    }
}

class Program
{
    static void Main()
    {
        // Load the HTML file
        HtmlDocument doc = new HtmlDocument("YOUR_DIRECTORY/input.html");

        // Attach the custom handler
        var handler = new MemoryResourceHandler();

        // Save HTML + resources to memory
        using var htmlStream = new MemoryStream();
        doc.Save(htmlStream, new HtmlSaveOptions { OutputStorage = handler });

        // Create the ZIP archive in memory
        using var zipStream = new MemoryStream();
        using (var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            // Add the HTML file
            var htmlEntry = zip.CreateEntry("index.html");
            using (var entry = htmlEntry.Open())
            {
                htmlStream.Position = 0;
                htmlStream.CopyTo(entry);
            }

            // Add each captured resource
            foreach (var kvp in MemoryResourceHandler.Captured)
            {
                // Derive a sane relative path from the URL
                var uri = new Uri(kvp.Key);
                var relativePath = uri.AbsolutePath.TrimStart('/');
                var resEntry = zip.CreateEntry(relativePath);
                using var entry = resEntry.Open();
                kvp.Value.Position = 0;
                kvp.Value.CopyTo(entry);
            }
        }

        // The ZIP is ready – write it out or return it from a web API
        File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipStream.ToArray());

        Console.WriteLine("HTML successfully packaged into output.zip");
    }
}
```

### Oczekiwany wynik

Uruchomienie programu tworzy `output.zip` zawierający:

- `index.html` – przepisany HTML, który odwołuje się do zintegrowanych zasobów.  
- Wszystkie obrazy, pliki CSS i JavaScript, które pierwotna strona referencjonowała, zapisane przy użyciu ich oryginalnych ścieżek względnych.

Otwórz `index.html` z ZIP w dowolnej przeglądarce, a zobaczysz stronę renderowaną dokładnie tak, jak wyglądała, gdy znajdowała się w systemie plików.

## Częste pytania i przypadki brzegowe

| Question | Answer |
|----------|--------|
| **Co zrobić, gdy zasób jest bardzo duży (np. wideo)?** | Ponieważ wszystko znajduje się w pamięci, bardzo duże pliki mogą spowodować `OutOfMemoryException`. W takim wypadku strumieniuj bezpośrednio do pliku tymczasowego lub ogranicz akceptowany rozmiar. |
| **Czy muszę obsługiwać duplikujące się URL‑e zasobów?** | Słownik w obsłudze nadpisze duplikaty. Jeśli chcesz zachować tylko jedną kopię, sprawdź `Captured.ContainsKey` przed dodaniem. |
| **Czy mogę używać tego w kontrolerze ASP.NET Core?** | Oczywiście. Zwróć `File(zipStream.ToArray(), "application/zip", "page.zip")` z metody akcji. |
| **A co z zasobami HTTPS?** | Aspose.HTML pobierze je automatycznie, o ile środowisko ufa certyfikatowi SSL. W przypadku certyfikatów samopodpisanych skonfiguruj `ServicePointManager.ServerCertificateValidationCallback`. |
| **Czy obsługa jest wątkowo‑bezpieczna?** | Przykład używa statycznego słownika, który nie jest *thread‑safe*. Zabezpiecz dostęp blokadą lub użyj `ConcurrentDictionary`, jeśli planujesz przetwarzać wiele dokumentów równocześnie. |

## Porady dla produkcji

- **Reuse the handler** tylko dla jednego dokumentu; twórz nową instancję na każde żądanie, aby uniknąć krzyżowego dostępu między użytkownikami.  
- **Dispose streams** niezwłocznie. Chociaż bloki `using` obsługują większość przypadków, wszelkie strumienie przechowywane w słowniku powinny być zwolnione po zbudowaniu ZIP‑a.  
- **Validate the HTML** przed przetwarzaniem, aby wykryć niepoprawny markup, który mógłby spowodować nieoczekiwane żądania zasobów.  
- **Compress aggressively** ustawiając `ZipArchiveEntry.CompressionLevel = CompressionLevel.Optimal`, jeśli rozmiar pliku ma znaczenie.  

## Zakończenie

Omówiliśmy wszystko, co potrzebne, aby **custom resource handler** przejść przez stronę HTML, przechwycić każdy powiązany zasób i **create zip from memory** bez dotykania dysku. Pokazany wzorzec jest wystarczająco elastyczny dla scenariuszy usług webowych, zadań w tle czy nawet aplikacji desktopowych, które muszą dostarczyć samodzielny pakiet HTML.

Spróbuj — zamień `YOUR_DIRECTORY/input.html` na dowolną stronę, dostosuj obsługę do przechowywania zasobów w `ConcurrentDictionary`, a będziesz mieć solidny, w‑pamięci pipeline HTML‑to‑ZIP gotowy do produkcji.

---

*Gotowy na kolejny poziom?* Następnie odkryj, jak **convert HTML to PDF** przy użyciu Aspose.HTML, lub poeksperymentuj z szyfrowaniem ZIP‑a dla dodatkowego bezpieczeństwa. Nie ma granic, gdy opanujesz strumieniowanie w pamięci w C#. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}