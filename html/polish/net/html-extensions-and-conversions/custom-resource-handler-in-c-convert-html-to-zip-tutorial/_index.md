---
category: general
date: 2026-02-10
description: Niestandardowy handler zasobów umożliwia konwersję HTML do ZIP w C#.
  Dowiedz się, jak zapisać HTML jako zip i efektywnie strumieniować zasoby HTML.
draft: false
keywords:
- custom resource handler
- convert html to zip
- save html as zip
- create zip with html
- stream html resources
language: pl
og_description: Obsługa niestandardowych zasobów umożliwia konwersję HTML do ZIP w
  C#. Skorzystaj z tego przewodnika krok po kroku, aby zapisać HTML jako zip i strumieniować
  zasoby HTML.
og_title: Niestandardowy obsługiwacz zasobów w C# – konwersja HTML do ZIP
tags:
- Aspose.HTML
- C#
- ZIP archive
- file streaming
title: Niestandardowy obsługiwacz zasobów w C# – Samouczek konwersji HTML do ZIP
url: /pl/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Niestandardowy obsługiwacz zasobów – Konwersja HTML do ZIP w C#

Zastanawiałeś się kiedyś, jak **custom resource handler** przekształcić surowy HTML bezpośrednio w plik ZIP? Nie jesteś sam. Wielu programistów napotyka problem, gdy muszą spakować stronę HTML wraz z jej zasobami, nie zapełniając dysku plikami tymczasowymi. Dobra wiadomość? Dzięki Aspose.HTML możesz zrobić to wszystko w pamięci, a sztuczka polega na niestandardowym obsługiwaczu zasobów.

W tym samouczku przeprowadzimy Cię przez kompletny, działający przykład, który pokaże, jak **convert HTML to ZIP**, **save HTML as ZIP** i **stream HTML resources** w locie. Po zakończeniu będziesz mieć jedną metodę, która przyjmuje ciąg HTML i generuje gotowy do pobrania `result.zip` zawierający stronę oraz wszystkie powiązane zasoby.

> **Wymagania wstępne** – .NET 6+ (lub .NET Framework 4.6+), zainstalowany Aspose.HTML dla .NET oraz podstawowa znajomość strumieni. Nie są wymagane żadne zewnętrzne narzędzia.

---

## Niestandardowy obsługiwacz zasobów – podstawowa koncepcja

*resource handler* w Aspose.HTML jest obiektem, który decyduje **gdzie** trafia każda część dokumentu — czy to plik na dysku, bufor pamięci, czy, jak pokażemy, wpis w archiwum ZIP. Dziedzicząc po `ResourceHandler`, uzyskujesz pełną kontrolę nad miejscem docelowym dla głównego pliku HTML **oraz** każdego pomocniczego zasobu (CSS, obrazy, czcionki itp.).

Pomyśl o nim jak o policjancie ruchu drogowego dla zasobów Twojego dokumentu: metoda `HandleResource` przekazuje Ci `Stream` dla głównego HTML, a zdarzenie `ResourceSaving` pozwala przechwycić każdy zależny plik tuż przed jego zapisaniem.

## Krok 1: Implementacja niestandardowego obsługiwacza zasobów

Najpierw utwórz klasę dziedziczącą po `ResourceHandler`. Nadpiszemy `HandleResource`, aby przekazać Aspose nowy `MemoryStream` dla głównego wyjścia HTML. Dla powiązanych zasobów podłączymy się później do `ResourceSaving`.

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using System.IO;

/// <summary>
/// Supplies a stream for every resource the HTML document needs to save.
/// </summary>
class MyHandler : ResourceHandler
{
    /// <summary>
    /// Returns a new stream for the main HTML content.
    /// </summary>
    public override Stream HandleResource(ResourceInfo info)
    {
        // In real life you might return a FileStream or a ZipEntry stream.
        // Here we just hand back a clean MemoryStream.
        return new MemoryStream();
    }
}
```

**Dlaczego to ważne:** Zwrócenie nowego `MemoryStream` oznacza, że HTML nigdy nie trafia do systemu plików. To podstawa czystego, w‑pamięci tworzenia ZIP później.

## Krok 2: Zapisz HTML w pojedynczym MemoryStream

Teraz, gdy mamy obsługiwacz, możemy wygenerować dokument HTML i przechwycić go w całości w pamięci. Ten krok jest opcjonalny, jeśli potrzebujesz tylko ZIP, ale ilustruje, jak działa obsługiwacz w izolacji.

```csharp
using Aspose.Html;

// Sample HTML – replace with your own markup or load from a file.
string htmlContent = "<html><head><title>Demo</title></head><body>Hello world!</body></html>";

// Create the document from a string.
HTMLDocument htmlDocument = new HTMLDocument(htmlContent);

// Instantiate our custom handler.
MyHandler memoryHandler = new MyHandler();

using (MemoryStream htmlStream = new MemoryStream())
{
    // Save triggers HandleResource and writes the HTML into htmlStream.
    htmlDocument.Save(htmlStream, memoryHandler);

    // Reset position for potential reading.
    htmlStream.Position = 0;

    // For demo purposes, dump the HTML to console.
    using (StreamReader reader = new StreamReader(htmlStream))
    {
        Console.WriteLine("Generated HTML:");
        Console.WriteLine(reader.ReadToEnd());
    }
}
```

**Oczekiwany wynik** (sformatowany dla czytelności):

```
Generated HTML:
<html><head><title>Demo</title></head><body>Hello world!</body></html>
```

Jeśli uruchomisz ten fragment, zobaczysz, że HTML istnieje wyłącznie w RAM — nie zostaną utworzone żadne pliki tymczasowe.

## Krok 3: Pakowanie HTML i zasobów w archiwum ZIP

Teraz nadchodzi najciekawsza część: pakowanie HTML **i** każdego odwołanego zasobu w plik ZIP bez zapisywania pośrednich plików na dysku. Użyjemy `System.IO.Compression.ZipArchive` wraz ze zdarzeniem `ResourceSaving`.

```csharp
using Aspose.Html;
using System.IO;
using System.IO.Compression;

// Re‑use the same HTMLDocument from the previous step.
HTMLDocument htmlDocument = new HTMLDocument("<html><body>Hello world!</body></html>");

// Path where the final ZIP will be written.
string zipPath = Path.Combine(Environment.CurrentDirectory, "result.zip");

// Open a FileStream for the ZIP file.
using (FileStream zipFile = new FileStream(zipPath, FileMode.Create))
using (ZipArchive zipArchive = new ZipArchive(zipFile, ZipArchiveMode.Update))
{
    // Create a fresh handler for the ZIP operation.
    MyHandler zipHandler = new MyHandler();

    // Hook the ResourceSaving event – this fires for every resource.
    zipHandler.ResourceSaving += (sender, e) =>
    {
        // Ensure we don't create leading folder entries like "/css/style.css".
        string entryName = e.ResourceInfo.Path.TrimStart('/');

        // Create a new entry inside the ZIP.
        ZipArchiveEntry entry = zipArchive.CreateEntry(entryName);

        // Provide the stream that Aspose will write into.
        e.Stream = entry.Open();
    };

    // Save the document; the handler will fill the ZIP for us.
    htmlDocument.Save(zipHandler);
}

// Verify the ZIP exists.
Console.WriteLine($"ZIP created at: {zipPath}");
```

### Co dzieje się w tle?

1. **`ResourceSaving` jest wywoływane** dla głównego pliku HTML oraz każdego powiązanego zasobu.  
2. Nasza lambda tworzy pasujący wpis (`CreateEntry`) w otwartym ZIP.  
3. Przypisując `e.Stream = entry.Open()`, przekazujemy Aspose strumień zapisu, który zapisuje bezpośrednio do wpisu ZIP.  
4. Gdy `htmlDocument.Save` zakończy się, ZIP zawiera w pełni sformatowaną stronę HTML oraz wszystkie CSS, obrazy lub czcionki odwołane w znacznikach.

**Wynik:** pojedynczy plik `result.zip`, który możesz udostępnić przeglądarkom, załączyć do e‑maili lub przechowywać w blob storage — bez pozostawionych plików tymczasowych.

## Bonus: Użycie ZIP w Web API

Jeśli tworzysz punkt końcowy ASP.NET Core, który zwraca ZIP na żądanie, obowiązuje ta sama logika. Oto zwięzła akcja kontrolera:

```csharp
[ApiController]
[Route("api/[controller]")]
public class HtmlZipController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult DownloadZip()
    {
        // Build the document (could be loaded from a DB, etc.).
        var html = "<html><body><h1>Dynamic report</h1></body></html>";
        var doc = new HTMLDocument(html);
        var handler = new MyHandler();

        // Prepare an in‑memory ZIP.
        using var zipStream = new MemoryStream();
        using (var archive = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            handler.ResourceSaving += (s, e) =>
            {
                var entry = archive.CreateEntry(e.ResourceInfo.Path.TrimStart('/'));
                e.Stream = entry.Open();
            };
            doc.Save(handler);
        }

        zipStream.Position = 0;
        return File(zipStream, "application/zip", "report.zip");
    }
}
```

Teraz żądanie GET do `/api/HtmlZip/download` strumieniu generowany ZIP bezpośrednio do klienta — idealne dla raportów generowanych w locie.

## Częste problemy i wskazówki

| Problem | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| **Puste foldery w ZIP** | `ResourceInfo.Path` zaczyna się od `/` powodując wpis taki jak `/` | Użyj `TrimStart('/')` jak pokazano w obsłudze zdarzenia. |
| **Brakujące obrazy** | Obrazy odwołujące się do bezwzględnych adresów URL nie są pobierane automatycznie | Ustaw `htmlDocument.Options.ResourceLoading = ResourceLoadingMode.Stream` i dostarcz niestandardowy `ResourceHandler`, który pobiera zdalne zasoby. |
| **Duże pliki powodują obciążenie pamięci** | Wszystkie strumienie są przechowywane w pamięci aż do zamknięcia ZIP | Zmień `ZipArchiveMode.Update` na `Create` i zapisuj każdy wpis bezpośrednio bez buforowania, lub strumieniuj z dysku, jeśli rozmiar przekracza RAM. |
| **Wyjątek „The stream does not support seeking”** | Próba ponownego użycia nie‑poszukującego strumienia dla wielu zasobów | Zawsze dostarczaj nowy `MemoryStream` lub `entry.Open()` dla każdego zasobu. |

## Zakończenie

Właśnie pokazaliśmy, jak **custom resource handler** umożliwia **convert HTML to ZIP**, **save HTML as ZIP** i **stream HTML resources** bez dotykania systemu plików. Nadpisując `HandleResource` i korzystając z `ResourceSaving`, uzyskujesz precyzyjną kontrolę nad każdym bajtem wychodzącym z Aspose.HTML.

Wzorzec skaluje się: zamień pamięciowy `MemoryStream` na strumień chmury (blob), dodaj ustawienia kompresji lub podłącz warstwę logowania, aby audytować, które zasoby są pakowane. Nie ma ograniczeń, gdy kontrolujesz pipeline zasobów.

Gotowy na kolejny krok? Spróbuj osadzić CSS i obrazy w HTML, eksperymentuj z ładowaniem zdalnych zasobów lub zintegrować ten przepływ w Azure Function, która zwraca ZIP na żądanie. Szczęśliwego kodowania!

*Obraz ilustrujący przepływ pracy niestandardowego obsługiwacza zasobów, zamieniającego HTML w plik ZIP.*

![przepływ pracy niestandardowego obsługiwacza zasobów](https://example.com/placeholder-image.png "przepływ pracy niestandardowego obsługiwacza zasobów")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}