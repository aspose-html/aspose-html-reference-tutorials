---
category: general
date: 2026-03-02
description: Dowiedz się, jak spakować HTML przy użyciu Aspose HTML, własnego obsługiwacza
  zasobów i .NET ZipArchive. Przewodnik krok po kroku, jak utworzyć archiwum zip i
  osadzić zasoby.
draft: false
keywords:
- how to zip html
- custom resource handler
- aspose html save
- how to create zip
- how to embed resources
language: pl
og_description: Dowiedz się, jak spakować HTML przy użyciu Aspose HTML, własnego obsługiwacza
  zasobów i .NET ZipArchive. Postępuj zgodnie z krokami, aby utworzyć archiwum zip
  i osadzić zasoby.
og_title: Jak spakować HTML za pomocą Aspose HTML – Kompletny przewodnik
tags:
- Aspose.HTML
- C#
- ZIP archive
title: Jak spakować HTML przy użyciu Aspose HTML – Kompletny przewodnik
url: /pl/net/advanced-features/how-to-zip-html-with-aspose-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak spakować HTML do ZIP przy użyciu Aspose HTML – Kompletny przewodnik

Czy kiedykolwiek potrzebowałeś **spakować HTML** razem ze wszystkimi obrazami, plikami CSS i skryptami, do których się odwołuje? Być może tworzysz pakiet do pobrania dla systemu pomocy offline, albo po prostu chcesz udostępnić statyczną stronę jako pojedynczy plik. W każdym razie nauka **jak spakować HTML** to przydatna umiejętność w zestawie narzędzi programisty .NET.

W tym samouczku przeprowadzimy Cię przez praktyczne rozwiązanie wykorzystujące **Aspose.HTML**, **niestandardowy obsługiwacz zasobów** oraz wbudowaną klasę `System.IO.Compression.ZipArchive`. Po zakończeniu dokładnie będziesz wiedział, jak **zapiszyć** dokument HTML do pliku ZIP, **osadzić zasoby** i nawet dostosować proces, jeśli potrzebujesz obsługiwać nietypowe URI.

> **Pro tip:** Ten sam wzorzec działa dla PDF‑ów, SVG lub dowolnego innego formatu obciążonego zasobami webowymi — wystarczy zamienić klasę Aspose.

## Czego będziesz potrzebował

- .NET 6 lub nowszy (kod kompiluje się również z .NET Framework)
- Pakiet NuGet **Aspose.HTML for .NET** (`Aspose.Html`)
- Podstawowa znajomość strumieni C# i operacji I/O na plikach
- Strona HTML odwołująca się do zewnętrznych zasobów (obrazy, CSS, JS)

Nie są wymagane dodatkowe zewnętrzne biblioteki ZIP; standardowa przestrzeń nazw `System.IO.Compression` wykonuje całą ciężką pracę.

## Krok 1: Utwórz niestandardowy ResourceHandler (niestandardowy obsługiwacz zasobów)

Aspose.HTML wywołuje `ResourceHandler` za każdym razem, gdy podczas zapisywania napotka odwołanie zewnętrzne. Domyślnie próbuje pobrać zasób z sieci, ale my chcemy **osadzić** dokładne pliki znajdujące się na dysku. Właśnie tutaj wkracza **niestandardowy obsługiwacz zasobów**.

```csharp
using System;
using System.IO;
using Aspose.Html;

// Step 1 – custom handler that copies local files into the output stream
class MyResourceHandler : ResourceHandler
{
    public override void HandleResource(string uri, Stream outputStream)
    {
        // Assume uri is a local file path; adjust logic for URLs if needed
        using (var source = new FileStream(uri, FileMode.Open, FileAccess.Read))
        {
            source.CopyTo(outputStream);
        }
    }
}
```

**Dlaczego to ważne:**  
Jeśli pominiesz ten krok, Aspose będzie próbował wykonać żądanie HTTP dla każdego `src` lub `href`. To zwiększa opóźnienie, może nie powieść się za zaporami i podważa cel samodzielnego archiwum ZIP. Nasz obsługiwacz zapewnia, że dokładny plik znajdujący się na dysku trafi do archiwum.

## Krok 2: Załaduj dokument HTML (aspose html save)

Aspose.HTML może przyjąć URL, ścieżkę do pliku lub surowy ciąg HTML. W tej demonstracji załadujemy zdalną stronę, ale ten sam kod działa również z plikiem lokalnym.

```csharp
using Aspose.Html;

// Step 2 – load the HTML document (URL, file path, or raw string)
var htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

**Co się dzieje w tle?**  
Klasa `HTMLDocument` parsuje znacznik, buduje DOM i rozwiązuje względne URL‑e. Gdy później wywołasz `Save`, Aspose przegląda DOM, pyta Twój `ResourceHandler` o każdy zewnętrzny plik i zapisuje wszystko do docelowego strumienia.

## Krok 3: Przygotuj archiwum ZIP w pamięci (how to create zip)

Zamiast zapisywać tymczasowe pliki na dysku, zachowamy wszystko w pamięci przy użyciu `MemoryStream`. To podejście jest szybsze i zapobiega zaśmiecaniu systemu plików.

```csharp
using System.IO;
using System.IO.Compression;

// Step 3 – create a memory‑backed ZIP archive
using var archiveStream = new MemoryStream();
using var archive = new ZipArchive(archiveStream, ZipArchiveMode.Create, true);
```

**Uwaga dotycząca przypadków brzegowych:**  
Jeśli Twój HTML odwołuje się do bardzo dużych zasobów (np. obrazów wysokiej rozdzielczości), strumień w pamięci może zużywać dużo RAMu. W takiej sytuacji przełącz się na ZIP oparty na `FileStream` (`new FileStream("temp.zip", FileMode.Create)`).

## Krok 4: Zapisz dokument HTML do ZIP (aspose html save)

Teraz łączymy wszystko: dokument, nasz `MyResourceHandler` oraz archiwum ZIP.

```csharp
// Step 4 – save HTML + resources into the ZIP
var resourceHandler = new MyResourceHandler();
htmlDoc.Save(archive, resourceHandler);
```

Za kulisami Aspose tworzy wpis dla głównego pliku HTML (zwykle `index.html`) oraz dodatkowe wpisy dla każdego zasobu (np. `images/logo.png`). `resourceHandler` zapisuje dane binarne bezpośrednio do tych wpisów.

## Krok 5: Zapisz ZIP na dysku (how to embed resources)

Na koniec zapisujemy archiwum w pamięci do pliku. Możesz wybrać dowolny folder; po prostu zamień `YOUR_DIRECTORY` na swoją rzeczywistą ścieżkę.

```csharp
using System.IO;

// Step 5 – persist the ZIP file
File.WriteAllBytes(@"YOUR_DIRECTORY\sample.zip", archiveStream.ToArray());

// Optional: verify the archive size
Console.WriteLine($"ZIP created: {new FileInfo(@"YOUR_DIRECTORY\sample.zip").Length} bytes");
```

**Wskazówka weryfikacyjna:**  
Otwórz powstały `sample.zip` przy użyciu eksploratora archiwów systemu operacyjnego. Powinieneś zobaczyć `index.html` oraz strukturę folderów odzwierciedlającą oryginalne lokalizacje zasobów. Kliknij dwukrotnie `index.html` — powinien wyświetlić się offline bez brakujących obrazów czy stylów.

## Pełny działający przykład (wszystkie kroki połączone)

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Skopiuj i wklej go do nowego projektu aplikacji konsolowej, przywróć pakiet NuGet `Aspose.Html` i naciśnij **F5**.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

// Step 1: Custom ResourceHandler that copies each external resource into the ZIP entry.
class MyResourceHandler : ResourceHandler
{
    public override void HandleResource(string uri, Stream outputStream)
    {
        // Handle both absolute file paths and relative URLs.
        if (File.Exists(uri))
        {
            using var source = new FileStream(uri, FileMode.Open, FileAccess.Read);
            source.CopyTo(outputStream);
        }
        else
        {
            // Fallback: try to download from the web (rarely needed for offline ZIPs).
            using var client = new System.Net.WebClient();
            var data = client.DownloadData(uri);
            outputStream.Write(data, 0, data.Length);
        }
    }
}

class Program
{
    static void Main()
    {
        // Step 2: Load the HTML document (URL, file path, or raw HTML string).
        var htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // Step 3: Prepare an in‑memory ZIP archive.
        using var archiveStream = new MemoryStream();
        using var archive = new ZipArchive(archiveStream, ZipArchiveMode.Create, true);

        // Step 4: Save the HTML + its resources into the ZIP.
        var resourceHandler = new MyResourceHandler();
        htmlDoc.Save(archive, resourceHandler);

        // Step 5: Persist the ZIP to disk.
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "sample.zip");
        File.WriteAllBytes(outputPath, archiveStream.ToArray());

        Console.WriteLine($"✅ ZIP created at: {outputPath}");
    }
}
```

**Oczekiwany wynik:**  
Plik `sample.zip` pojawi się na pulpicie. Rozpakuj go i otwórz `index.html` — strona powinna wyglądać dokładnie tak jak wersja online, ale teraz działa całkowicie offline.

## Najczęściej zadawane pytania (FAQ)

### Czy to działa z lokalnymi plikami HTML?
Zdecydowanie tak. Zamień URL w `HTMLDocument` na ścieżkę do pliku, np. `new HTMLDocument(@"C:\site\index.html")`. Ten sam `MyResourceHandler` skopiuje lokalne zasoby.

### Co jeśli zasób jest data‑URI (zakodowany w base64)?
Aspose traktuje data‑URI jako już osadzone, więc obsługiwacz nie jest wywoływany. Nie wymaga dodatkowych działań.

### Czy mogę kontrolować strukturę folderów wewnątrz ZIP?
Tak. Przed wywołaniem `htmlDoc.Save` możesz ustawić `htmlDoc.SaveOptions` i określić ścieżkę bazową. Alternatywnie, zmodyfikuj `MyResourceHandler`, aby dodać nazwę folderu przy tworzeniu wpisów.

### Jak dodać plik README do archiwum?
Po prostu utwórz nowy wpis ręcznie:

```csharp
var readme = archive.CreateEntry("README.txt");
using var writer = new StreamWriter(readme.Open());
writer.WriteLine("This ZIP contains an offline HTML site.");
```

## Kolejne kroki i powiązane tematy

- **Jak osadzać zasoby** w innych formatach (PDF, SVG) przy użyciu podobnych API Aspose.  
- **Dostosowywanie poziomu kompresji**: `new ZipArchive(stream, ZipArchiveMode.Create, true, Encoding.UTF8)` pozwala przekazać `ZipArchiveEntry.CompressionLevel` dla szybszych lub mniejszych archiwów.  
- **Serwowanie ZIP przez ASP.NET Core**: Zwróć `MemoryStream` jako wynik pliku (`File(archiveStream, "application/zip", "site.zip")`).  

Eksperymentuj z tymi wariantami, aby dopasować je do potrzeb swojego projektu. Wzorzec, który omówiliśmy, jest wystarczająco elastyczny, aby obsłużyć większość scenariuszy „spakuj wszystko w jeden plik”.

## Podsumowanie

Właśnie pokazaliśmy **jak spakować HTML** przy użyciu Aspose.HTML, **niestandardowego obsługiwacza zasobów** oraz klasy .NET `ZipArchive`. Tworząc obsługiwacz, który strumieniuje lokalne pliki, ładując dokument, pakując wszystko w pamięci i ostatecznie zapisując ZIP, otrzymujesz w pełni samodzielne archiwum gotowe do dystrybucji.

Teraz możesz pewnie tworzyć pakiety ZIP dla statycznych stron, eksportować pakiety dokumentacji lub nawet automatyzować kopie zapasowe offline — wszystko przy użyciu kilku linii C#.

Masz własny pomysł, którym chcesz się podzielić? Dodaj komentarz i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}