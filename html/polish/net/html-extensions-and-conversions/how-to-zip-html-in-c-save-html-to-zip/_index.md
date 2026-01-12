---
category: general
date: 2025-12-29
description: Jak szybko spakować HTML w C# przy użyciu Aspose.HTML – zapisz HTML do
  pliku zip za pomocą własnego ZipResourceHandler. Dowiedz się krok po kroku.
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: pl
og_description: Jak szybko spakować HTML w C# przy użyciu Aspose.HTML. Postępuj zgodnie
  z tym przewodnikiem, aby zapisać HTML do pliku zip i utworzyć archiwum zip z niestandardowym
  obsługiwaniem zasobów.
og_title: Jak spakować HTML w formacie ZIP w C# – Zapisz HTML do pliku ZIP
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: Jak spakować HTML w C# – Zapisz HTML do pliku ZIP
url: /pl/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak spakować HTML do ZIP w C# – Zapis HTML w ZIP

Spakowanie HTML do ZIP w C# to częsta potrzeba, gdy chcesz udostępnić strony internetowe do użytku offline. Niezależnie od tego, czy pakujesz jedną stronę wraz z jej obrazkami, czy eksportujesz całą witrynę, **zapis HTML w zip** utrzymuje wszystko w porządku i przenośne. W tym samouczku przeprowadzimy Cię przez kompletną, gotową do uruchomienia rozwiązanie, które nie tylko pakuje znacznik HTML, ale także strumieniuje wszystkie odwoływane zasoby bezpośrednio do archiwum.

Nauczysz się, jak:

* Programowo tworzyć archiwum zip przy użyciu `System.IO.Compression` w .NET.
* Podłączyć własny `ResourceHandler` do Aspose.HTML, aby zasoby trafiały bezpośrednio do zip.
* Obsługiwać przypadki brzegowe, takie jak istniejące pliki zip i duże zasoby binarne.

Nie są potrzebne żadne zewnętrzne narzędzia — wystarczy C#, Aspose.HTML i kilka linijek kodu.

## Czego będziesz potrzebować

Zanim zaczniemy, upewnij się, że masz:

* **.NET 6+** (kod działa także na .NET Framework 4.6.2 i nowszych).
* **Aspose.HTML for .NET** – możesz pobrać darmową wersję próbną ze strony Aspose lub użyć licencjonowanej kopii.
* Środowisko programistyczne (Visual Studio, VS Code, Rider — cokolwiek wolisz).

To wszystko. Nie potrzebujesz dodatkowych pakietów NuGet poza `System.IO.Compression` (dołączonym do .NET) i `Aspose.HTML`.

## Krok 1: Konfiguracja projektu i importy

Utwórz nowy projekt konsolowy (lub wstaw kod do istniejącego). Dodaj wymagane dyrektywy `using` na początku pliku:

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **Pro tip:** Jeśli używasz Visual Studio, IDE zasugeruje dodanie brakującego pakietu NuGet dla `Aspose.Html`. Zaakceptuj je i jesteś gotowy do działania.

## Krok 2: Implementacja własnego ZipResourceHandler

Aspose.HTML wywołuje `ResourceHandler` za każdym razem, gdy musi zapisać zasób (np. obraz, plik CSS lub skrypt). Nadpisując metodę `HandleResource`, możemy zdecydować, gdzie każdy zasób trafi. Poniższy handler tworzy wpis zip, który odzwierciedla logiczną ścieżkę zasobu, a następnie zwraca strumień zapisu skierowany bezpośrednio do tego wpisu.

```csharp
/// <summary>
/// Streams each HTML resource straight into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Ensure the entry's directory structure exists inside the zip.
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        // The returned stream writes directly into the zip entry.
        return entry.Open();
    }
}
```

**Dlaczego to ważne:**  
Zamiast zapisywać zasoby w tymczasowym folderze, a potem pakować folder, ten handler strumieniuje dane w locie, oszczędzając operacje dyskowe i utrzymując niskie zużycie pamięci. Zapewnia także, że wewnętrzna hierarchia folderów w zipie odpowiada względnym ścieżkom HTML, co przeglądarki oczekują po rozpakowaniu i otwarciu strony.

## Krok 3: Przygotowanie archiwum ZIP

Teraz otworzymy (lub utworzymy) docelowy plik zip. Flaga `FileMode.Create` nadpisuje istniejący plik — idealna do powtarzalnych buildów. Jeśli wolisz zachować istniejące archiwum, przełącz się na `FileMode.OpenOrCreate` i odpowiednio obsłuż duplikaty wpisów.

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **Przypadek brzegowy:** Jeśli proces zakończy się awarią przed zakończeniem bloku `using`, możesz skończyć z uszkodzonym zipem. Uruchomienie kodu w `try/catch` i usunięcie częściowo utworzonego pliku w razie niepowodzenia to prosta ochrona.

## Krok 4: Budowa dokumentu HTML z osadzonym zasobem

Dla demonstracji stworzymy małą stronę HTML, która odwołuje się do obrazu o nazwie `image.png`. W rzeczywistym scenariuszu wczytywałbyś HTML z pliku lub łańcucha pochodzącego z bazy danych.

```csharp
// Sample HTML containing an <img> tag.
// Aspose.HTML will ask the ResourceHandler for "image.png".
string htmlContent = @"
<html>
<head><title>Sample Zip</title></head>
<body>
    <h1>Hello, zipped world!</h1>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

// Create the document from the string.
var html = new HTMLDocument(htmlContent);
```

Jeśli masz rzeczywiste pliki obrazów na dysku, możesz dodać je do zipa ręcznie przed zapisaniem HTML, albo pozwolić Aspose.HTML pobrać je przez handler (np. z URL). Nasz handler działa zarówno dla lokalnych ścieżek, jak i zdalnych adresów URL.

## Krok 5: Konfiguracja opcji zapisu, aby używać ZipResourceHandler

Teraz informujemy Aspose.HTML, aby używał naszego własnego handlera przy zapisie zasobów. Klasa `HTMLSaveOptions` pozwala także określić nazwę pliku wyjściowego wewnątrz zip (domyślnie jest to `index.html`).

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## Krok 6: Zapis dokumentu – wszystko strumieniuje do ZIP

Na koniec wywołujemy `Save`. Aspose.HTML parsuje znacznik, znajduje tag `<img>`, wywołuje `HandleResource` dla `image.png` i zapisuje zarówno plik HTML, jak i obraz do tego samego archiwum zip.

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

Gdy bloki `using` zakończą się, `ZipArchive` finalizuje plik, czyniąc go gotowym do dystrybucji.

### Pełny działający przykład

Poniżej znajduje się cały program złożony razem. Skopiuj‑wklej go do `Program.cs` i uruchom — nie są potrzebne żadne dalsze modyfikacje.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare the zip file.
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);
        using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);

        // 2️⃣ Build a simple HTML document with an image reference.
        string htmlContent = @"
        <html>
        <head><title>Sample Zip</title></head>
        <body>
            <h1>Hello, zipped world!</h1>
            <img src='image.png' alt='Demo image'>
        </body>
        </html>";
        var html = new HTMLDocument(htmlContent);

        // 3️⃣ Set save options to stream resources into the zip.
        var saveOptions = new HTMLSaveOptions
        {
            OutputFileName = "index.html",
            OutputStorage = new ZipResourceHandler(zip)
        };

        // 4️⃣ Save – everything ends up in output.zip.
        html.Save(saveOptions);
        Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
    }
}
```

**Oczekiwany rezultat:** Po wykonaniu, `output.zip` zawiera dwa wpisy:

```
index.html
image.png
```

Jeśli rozpakujesz plik i otworzysz `index.html` w przeglądarce, obraz wyświetli się poprawnie, ponieważ względna ścieżka została zachowana.

## Frequently Asked

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}