---
category: general
date: 2026-03-31
description: Utwórz strumień pamięci w C# i naucz się renderować HTML do PNG, używać
  własnego obsługiwacza zasobów, zapisywać HTML do ZIP oraz programowo ustawiać styl
  czcionki — wszystko w jednym samouczku.
draft: false
keywords:
- create memory stream
- render html to png
- custom resource handler
- save html to zip
- set font style programmatically
language: pl
og_description: Utwórz strumień pamięci w C# i natychmiast renderuj HTML do PNG, użyj
  niestandardowych obsługiwaczy zasobów, zapisz HTML do ZIP oraz ustaw styl czcionki
  programowo.
og_title: Utwórz strumień pamięci w C# – Kompletny przewodnik programistyczny
tags:
- C#
- HTML rendering
- Streams
- ZIP archives
- Image processing
title: Tworzenie strumienia pamięci w C# – Kompletny przewodnik z renderowaniem HTML
  i eksportem ZIP
url: /pl/net/rendering-html-documents/create-memory-stream-in-c-full-guide-with-html-rendering-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utworzenie strumienia pamięci w C# – Kompletny przewodnik z renderowaniem HTML i eksportem ZIP

Zastanawiałeś się kiedyś, jak **create memory stream** w C# i następnie przekształcić dokument HTML w obraz PNG, plik ZIP, a nawet zmienić styl czcionki w locie? Nie jesteś jedyny. Wielu programistów napotyka problem, gdy potrzebują reprezentacji dokumentu w pamięci, ale nie chcą korzystać z systemu plików.  

W tym samouczku przeprowadzimy Cię przez kompletną, end‑to‑end rozwiązanie: zbudujemy własny handler zasobów, przekażemy HTML do `MemoryStream`, spakujemy ten sam dokument do ZIP, a na końcu wyrenderujemy go jako obraz z antyaliasingiem. Po zakończeniu będziesz w stanie **render HTML to PNG**, **save HTML to ZIP** i **set font style programmatically** bez zapisywania tymczasowych plików na dysku.

## Wymagania wstępne

- .NET 6.0 lub nowszy (powierzchnia API jest stabilna w najnowszych wersjach).  
- Odwołanie do biblioteki HTML‑to‑image, która udostępnia `HTMLDocument`, `ImageRenderer` i powiązane typy – na przykład **HtmlRenderer.Core** (zastąp rzeczywistym pakietem, którego używasz).  
- Podstawowa znajomość strumieni, instrukcji `using` oraz wzorców obiektowych w C#.

> **Pro tip:** Jeśli używasz Visual Studio, włącz **nullable reference types** (`<Nullable>enable</Nullable>`), aby wcześnie wykrywać subtelne błędy.

## Krok 1: Utwórz strumień pamięci z własnym handlerem zasobów

Pierwszą rzeczą, której potrzebujemy, jest handler, który informuje silnik HTML, *gdzie* zapisać każdy zasób (obrazy, CSS itp.). Dziedzicząc po `ResourceHandler`, możemy kierować wszystkie wyjścia do jednego `MemoryStream`.

```csharp
using System;
using System.IO;

// Step 1: Define a handler that writes resources to an in‑memory stream
class MemoryResourceHandler : ResourceHandler
{
    // The stream lives for the whole lifetime of the handler
    public MemoryStream OutputStream = new MemoryStream();

    // The engine calls this for every resource it needs to write
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}
```

**Why this matters:**  
`MemoryStream` istnieje w całości w RAM, co oznacza brak operacji I/O na dysku, co jest idealne w scenariuszach wysokiej wydajności, takich jak usługi sieciowe czy testy jednostkowe. Handler również zadowala API, ponieważ silnik oczekuje `Stream` dla każdego zasobu.

## Krok 2: Załaduj dokument HTML i zapisz go do strumienia pamięci

Teraz ładujemy istniejący plik HTML (lub ciąg znaków) i wskazujemy, aby używał naszego `MemoryResourceHandler`. Po wywołaniu `Save` strumień `OutputStream` zawiera pełny ładunek HTML.

```csharp
using System.IO;

// Assume the HTML file lives under YOUR_DIRECTORY
HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

// Instantiate the memory handler
MemoryResourceHandler memoryHandler = new MemoryResourceHandler();

// Save the document – all resources flow into the same MemoryStream
htmlDoc.Save(memoryHandler);
```

W tym momencie pozycja strumienia znajduje się na końcu, więc musimy go przewinąć do początku, zanim będziemy mogli odczytać zawartość.

```csharp
// Reset the stream position to the beginning
memoryHandler.OutputStream.Position = 0;

// Quick verification (optional)
// string htmlContent = new StreamReader(memoryHandler.OutputStream).ReadToEnd();
// Console.WriteLine(htmlContent);
```

> **Note:** Powyższa linia `ReadToEnd` jest zakomentowana, ponieważ w scenariuszu produkcyjnym prawdopodobnie przekażesz strumień do innego komponentu zamiast go wypisywać.

## Krok 3: Spakuj ten sam HTML przy użyciu własnego handlera ZIP

Czasami trzeba dostarczyć HTML wraz z jego zasobami. Drugi własny handler może na bieżąco tworzyć wpis ZIP dla każdego zasobu.

```csharp
using System.IO.Compression;

// Step 4: Define a handler that writes each resource into a ZIP archive
class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(string zipPath)
    {
        // Open (or create) the archive in write mode
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);
    }

    // The engine calls this for each resource; we create a ZIP entry with the same name
    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    // Proper disposal of the underlying ZipArchive
    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}
```

Teraz ponownie używamy tej samej instancji `htmlDoc` i zapisujemy ją do pliku ZIP.

```csharp
// Step 5: Save the HTML document into a ZIP file
using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
{
    htmlDoc.Save(zipHandler);
}
```

**Edge case tip:** Jeśli HTML odwołuje się do tego samego obrazu wielokrotnie, handler ZIP utworzy duplikaty wpisów. Aby tego uniknąć, możesz przechowywać `HashSet<string>` już dodanych nazw i zwracać istniejący strumień wpisu.

## Krok 4: Programowo ustaw styl czcionki w domyślnym arkuszu stylów

Zmiana wyglądu dokumentu bez modyfikacji źródłowego HTML jest często przydatna — na przykład przy generowaniu podglądu PDF z pogrubionym nagłówkiem. Biblioteka udostępnia `DefaultViewStyleSheet`, który możesz dostosować.

```csharp
// Step 6: Apply bold and italic styling to the default view stylesheet
htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

Możesz połączyć dowolne flagi zdefiniowane w `WebFontStyle`. Zmiana jest natychmiastowa i wpłynie na kolejne renderowania lub zapisy.

## Krok 5: Renderuj dokument HTML do obrazu PNG

Na koniec przekształćmy HTML w obraz rastrowy. Włączając antyaliasing i hinting, uzyskujemy wyraźny tekst i gładkie krawędzie.

```csharp
using System.Drawing; // For ImageRenderingOptions if needed

// Step 7: Render the document to an image with antialiasing and hinting
var renderingOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,
    UseHinting = true
};

new ImageRenderer(renderingOptions).Render(htmlDoc, "YOUR_DIRECTORY/out.png");
```

**What you’ll see:** Plik PNG o nazwie `out.png` w katalogu `YOUR_DIRECTORY`, który wygląda dokładnie tak, jak przeglądarka renderowałaby HTML, ale z wcześniej ustawionym stylem pogrubienie‑pochylenie.

![Zrzut ekranu wyniku create memory stream](placeholder-image.png "przykład create memory stream")

*Tekst alternatywny obrazu zawiera główne słowo kluczowe w celu spełnienia wymagań SEO.*

## Częste pytania i pułapki

| Question | Answer |
|----------|--------|
| **Czy mogę ponownie użyć tego samego `HTMLDocument` po zapisaniu do ZIP?** | Tak. Obiekt dokumentu pozostaje w pamięci; możesz wywołać `Save` wielokrotnie z różnymi handlerami. |
| **Co jeśli HTML zawiera duże zasoby binarne?** | `MemoryStream` będzie odpowiednio rosnąć. W przypadku bardzo dużych plików rozważ strumieniowanie bezpośrednio do pliku lub użycie `BufferedStream`. |
| **Czy muszę wywołać `Dispose` na `MemoryResourceHandler`?** | Nie jest to ściśle konieczne, ponieważ przechowuje tylko `MemoryStream`, który jest zwalniany, gdy handler zostanie usunięty przez garbage collector. Jednak wywołanie `Dispose` jest dobrą praktyką. |
| **Jak zmienić format obrazu (np. JPEG zamiast PNG)?** | Przekaż inną rozszerzenie pliku do `ImageRenderer.Render`, lub użyj `ImageRenderer.RenderToBitmap` i następnie zapisz przy pomocy `bitmap.Save("out.jpg", ImageFormat.Jpeg)`. |
| **Czy handler ZIP jest bezpieczny wątkowo?** | Nie. `ZipArchive` nie jest bezpieczny wątkowo, więc należy serializować dostęp lub utworzyć osobny handler dla każdego wątku. |

## Pełny działający przykład

Poniżej znajduje się pojedynczy program gotowy do skopiowania i wklejenia, który demonstruje wszystkie omówione kroki. Zastąp `YOUR_DIRECTORY` rzeczywistą ścieżką na swoim komputerze.

```csharp
// FullExample.cs
using System;
using System.IO;
using System.IO.Compression;

// Assume these types come from your HTML rendering library
using HtmlRendering; // placeholder namespace

class MemoryResourceHandler : ResourceHandler
{
    public MemoryStream OutputStream = new MemoryStream();
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}

class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(string zipPath) =>
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);

    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}

class Program
{
    static void Main()
    {
        // 1️⃣ Load HTML
        var htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

        // 2️⃣ Write to a memory stream
        var memHandler = new MemoryResourceHandler();
        htmlDoc.Save(memHandler);
        memHandler.OutputStream.Position = 0;
        // Optional: verify content
        // Console.WriteLine(new StreamReader(memHandler.OutputStream).ReadToEnd());

        // 3️⃣ Zip the same document
        using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
        {
            htmlDoc.Save(zipHandler);
        }

        // 4️⃣ Change font style programmatically
        htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // 5️⃣ Render to PNG with antialiasing & hinting
        var renderOpts = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            UseHinting = true
        };
        new ImageRenderer(renderOpts).Render(htmlDoc, "YOUR_DIRECTORY/out.png");

        Console.WriteLine("All operations completed successfully.");
    }
}
```

Po uruchomieniu tego programu otrzymasz trzy artefakty:

1. **In‑memory HTML** przechowywany w `memHandler.OutputStream`.  
2. **`output.zip`** zawierający HTML oraz wszystkie powiązane zasoby.  
3. **`out.png`** – renderowany obraz, który zachowuje styl pogrubienie‑pochylenie.

## Zakończenie

Pokazaliśmy, jak **create memory stream** w C# i płynnie zintegrować go z renderowaniem HTML, archiwizacją ZIP oraz generowaniem obrazów. Najważniejszy wniosek jest taki, że pojedynczy `HTMLDocument` może być zapisywany na wiele sposobów — do `MemoryStream`, archiwum ZIP lub pliku PNG — po prostu wymieniając `ResourceHandler`.  

Jeśli jesteś gotowy, aby pójść dalej, spróbuj:

- **Render to PDF** przy użyciu renderera PDF, który akceptuje `Stream`.  
- **Compress the memory stream** przed wysłaniem go przez sieć (np. `GZipStream`).  
- **Combine multiple HTML pages** w jeden ZIP dla masowego eksportu.

Śmiało eksperymentuj i nie wahaj się zostawić komentarza, jeśli napotkasz problem. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}