---
category: general
date: 2026-05-06
description: Jak używać ZipArchive w C# do zapisywania HTML jako archiwum ZIP. Dowiedz
  się, jak tworzyć archiwum ZIP w C# z zasobów HTML przy użyciu Aspose.HTML.
draft: false
keywords:
- how to use ziparchive
- save html as zip
- create zip archive c#
- create zip from html
language: pl
og_description: Jak używać ZipArchive w C# do spakowania dokumentu HTML i jego zasobów
  w jeden plik ZIP. Przewodnik krok po kroku z pełnym kodem.
og_title: Jak używać ZipArchive w C# – zapisać HTML jako ZIP
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: Jak używać ZipArchive w C# – Zapisz HTML jako ZIP
url: /pl/net/html-extensions-and-conversions/how-to-use-ziparchive-in-c-save-html-as-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać ZipArchive w C# – Zapisz HTML jako ZIP

Zastanawiałeś się kiedyś, jak używać ZipArchive w C#, gdy musisz dostarczyć stronę HTML wraz z obrazami, CSS i czcionkami? Nie jesteś jedyny. W wielu scenariuszach web‑to‑desktop najprostszym sposobem przeniesienia całej strony jest spakowanie wszystkiego do pliku ZIP.  

W tym samouczku przeprowadzimy Cię przez **zapis HTML jako zip** przy użyciu Aspose.HTML i własnego `ResourceHandler`. Po zakończeniu dokładnie będziesz wiedział, jak tworzyć projekty zip archive c# automatycznie przechwytujące każdy powiązany zasób, oraz będziesz mieć kompletny, działający przykład, który możesz wstawić do własnej bazy kodu.

## Co zbudujesz

- Wczytaj istniejący plik `input.html`.
- Przechwyć każdy zewnętrzny zasób (obrazy, arkusze stylów, czcionki) podczas zapisywania dokumentu.
- Zapisz każdy zasób bezpośrednio do wpisu `ZipArchive`, tak aby końcowy plik był schludnym `output.zip`.
- Zweryfikuj, że ZIP zawiera oczekiwaną strukturę folderów.

Nie są wymagane dodatkowe zewnętrzne biblioteki zip — wystarczy wbudowana przestrzeń nazw `System.IO.Compression` oraz Aspose.HTML.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.8).
- Aspose.HTML dla .NET (wersja próbna lub licencjonowana). Zainstaluj przez NuGet: `dotnet add package Aspose.HTML`.
- Podstawowa znajomość operacji I/O i strumieni w C#.

Jeśli masz to wszystko, zanurzmy się.

![diagram użycia ziparchive](image.png "Diagram przedstawiający przepływ HTML → ZipArchive – jak używać ziparchive")

## Krok 1: Utwórz własny ResourceHandler

Aspose.HTML wywołuje `ResourceHandler.HandleResource` dla każdego zewnętrznego pliku, który musi zapisać. Nadpisując tę metodę, możemy przekazać rendererowi strumień wskazujący bezpośrednio na wpis ZIP.

```csharp
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Rendering;

/// <summary>
/// Writes each HTML resource (image, CSS, font) into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(Stream zipStream)
    {
        // Open the archive for updating; leaveOpen keeps the underlying stream alive.
        _zipArchive = new ZipArchive(zipStream, ZipArchiveMode.Update, leaveOpen: true);
    }

    public override Stream HandleResource(ResourceInfo info)
    {
        // The URI's AbsolutePath contains the file name (e.g., "/images/logo.png").
        // Trim the leading slash so the entry appears at the root of the zip.
        var entryName = info.Uri.AbsolutePath.TrimStart('/');
        var entry = _zipArchive.CreateEntry(entryName, CompressionLevel.Optimal);

        // Return the entry's stream; Aspose will write the content straight into it.
        return entry.Open();
    }
}
```

**Dlaczego własny handler?**  
Bez niego Aspose.HTML zapisywałby każdy zasób do tymczasowego pliku na dysku, a Ty musiałbyś sam skopiować wszystko do ZIP. Ten handler eliminuje pośredni krok, zmniejsza operacje I/O i utrzymuje kod w porządku.

## Krok 2: Wczytaj dokument HTML

Teraz po prostu wczytujemy plik źródłowy. Aspose.HTML obsługuje zarówno lokalne ścieżki, jak i URL‑e, więc możesz wskazać zdalną stronę, jeśli chcesz.

```csharp
// Replace with the folder where your HTML lives.
string inputPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// The HTMLDocument constructor reads the file and parses it.
var document = new HTMLDocument(inputPath);
```

**Wskazówka:** Jeśli Twój HTML odwołuje się do zasobów przy użyciu względnych URL‑ów, upewnij się, że plik `input.html` znajduje się obok tych zasobów. `ResourceHandler` otrzyma dokładne ścieżki, które rozwiązuje Aspose.

## Krok 3: Podłącz ZipResourceHandler i zapisz

Z dokumentem gotowym i zdefiniowanym handlerem otwieramy `FileStream` dla wyjściowego ZIP, tworzymy instancję handlera i wywołujemy `document.Save`. Operacja zapisu wywołuje `HandleResource` dla każdego zewnętrznego pliku.

```csharp
// The final ZIP will be placed in the same directory.
string zipPath = Path.Combine("YOUR_DIRECTORY", "output.zip");

// Open a FileStream for the zip – FileMode.Create overwrites any existing file.
using (var zipStream = new FileStream(zipPath, FileMode.Create))
{
    var zipHandler = new ZipResourceHandler(zipStream);

    // Save the HTML document; the handler captures all linked resources.
    document.Save(zipHandler);
}
```

Po zakończeniu `Save`, `output.zip` zawiera:

```
/index.html          (the original HTML file)
/styles/main.css
/images/logo.png
/fonts/open-sans.ttf
...
```

Możesz otworzyć ZIP w dowolnym menedżerze archiwów, aby zweryfikować strukturę.

## Krok 4: Zweryfikuj wynik (opcjonalnie)

Szybka kontrola poprawności chroni Cię przed tajemniczymi brakującymi obrazami w późniejszym czasie.

```csharp
using (var archive = ZipFile.OpenRead(zipPath))
{
    Console.WriteLine("Entries in the ZIP:");
    foreach (var entry in archive.Entries)
    {
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
    }
}
```

Uruchomienie tego fragmentu wypisuje każdą nazwę pliku, potwierdzając, że proces **create zip from html** zakończył się sukcesem.

## Typowe przypadki brzegowe i jak sobie z nimi radzić

| Situation | What to watch for | Suggested fix |
|-----------|-------------------|---------------|
| **Absolute URLs** (e.g., `https://example.com/img.png`) | Aspose spróbuje pobrać zasób; handler otrzyma strumień wskazujący na tymczasowy plik. | Upewnij się, że Twój komputer ma dostęp do Internetu, lub pobierz zasoby wcześniej i przepisz HTML, aby używał lokalnych ścieżek. |
| **Duplicate file names** (two images named `logo.png` in different folders) | Wpisy ZIP muszą mieć unikalne ścieżki; w przeciwnym razie drugi wpis nadpisuje pierwszy. | Zachowaj hierarchię folderów w nazwie wpisu (`info.Uri.AbsolutePath.TrimStart('/')`). |
| **Large resources** (megabyte‑size videos) | Zapisywanie bezpośrednio do wpisu zip jest w porządku, ale możesz chcieć ustawić `CompressionLevel.NoCompression` dla już skompresowanych mediów. | Dostosuj `CreateEntry(entryName, CompressionLevel.NoCompression)` dla znanych typów mediów. |
| **Unsupported formats** (e.g., SVG with external fonts) | Niektóre zasoby mogą odwoływać się do dodatkowych plików, których Aspose nie rozwiązuje automatycznie. | Ręcznie dodaj te pliki do ZIP po wywołaniu `Save`. |

## Wskazówki dla kodu gotowego do produkcji

- **Dispose prawidłowo** – Zarówno `ZipArchive`, jak i `HTMLDocument` implementują `IDisposable`. Owiń je w bloki `using`, jak pokazano, aby zwolnić zasoby natywne.
- **Bezpieczeństwo wątków** – Handler nie jest bezpieczny wątkowo; unikaj używania tej samej instancji `ZipResourceHandler` w wielu wątkach.
- **Wydajność** – Dla ogromnych pakietów HTML rozważ strumieniowanie samego HTML do ZIP (`zipArchive.CreateEntry("index.html").Open()`), a następnie wywołaj `document.Save(stream)`, gdzie `stream` jest strumieniem tego wpisu.

## Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do aplikacji konsolowej. Zawiera wszystkie dyrektywy `using`, obsługę błędów i komentarze.

```csharp
// ------------------------------------------------------------
// How to Use ZipArchive in C# – Save HTML as ZIP (Full Demo)
// ------------------------------------------------------------
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Rendering;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(Stream zipStream)
    {
        _zipArchive = new ZipArchive(zipStream, ZipArchiveMode.Update, leaveOpen: true);
    }

    public override Stream HandleResource(ResourceInfo info)
    {
        var entryName = info.Uri.AbsolutePath.TrimStart('/');
        var entry = _zipArchive.CreateEntry(entryName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Paths – adjust to your environment.
            string baseDir = Path.Combine(Environment.CurrentDirectory, "DemoFiles");
            string htmlPath = Path.Combine(baseDir, "input.html");
            string zipPath  = Path.Combine(baseDir, "output.zip");

            // 2️⃣ Load the HTML document.
            var document = new HTMLDocument(htmlPath);

            // 3️⃣ Open the ZIP stream and save.
            using (var zipStream = new FileStream(zipPath, FileMode.Create))
            {
                var zipHandler = new ZipResourceHandler(zipStream);
                document.Save(zipHandler);
            }

            // 4️⃣ Quick verification.
            Console.WriteLine($"ZIP created at: {zipPath}");
            using (var archive = ZipFile.OpenRead(zipPath))
            {
                Console.WriteLine("Contents:");
                foreach (var entry in archive.Entries)
                    Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

Skompiluj przy użyciu `dotnet run` (lub wybranego IDE) i otwórz `output.zip`. Powinieneś zobaczyć oryginalny HTML oraz wszystkie odwołane zasoby, starannie spakowane. To cały przepływ pracy **create zip archive c#** w działaniu.

## Zakończenie

Właśnie pokazaliśmy **jak używać ZipArchive** do **zapisania HTML jako zip** i zaprezentowaliśmy czysty sposób **tworzenia zip z html** przy użyciu `ResourceHandler` Aspose.HTML. Najważniejsze wnioski to:

- Nadpisz `ResourceHandler`, aby strumieniować zasoby bezpośrednio do `ZipArchive`.
- Utrzymuj ZIP otwarty przez całą operację zapisu (`leaveOpen: true`).
- Zweryfikuj wynik i obsłuż przypadki brzegowe, takie jak absolutne URL‑e czy zduplikowane nazwy.

Teraz możesz zintegrować ten wzorzec z eksporterami web‑to‑desktop, generatorami dokumentacji offline lub dowolnym scenariuszem, w którym potrzebne jest spakowanie strony HTML wraz z jej zasobami.  

Chcesz iść dalej? Spróbuj skompresować wiele stron HTML do jednego archiwum lub dodać plik manifestu, który wymienia wszystkie wpisy. Możesz także zbadać szyfrowanie the

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}