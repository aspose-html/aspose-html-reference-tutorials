---
category: general
date: 2026-02-22
description: Niestandardowy obsługiwacz zasobów pozwala przechwytywać wyjście HTML.
  Dowiedz się, jak załadować dokument HTML, użyć funkcji zapisu Aspose HTML oraz zapisać
  HTML do strumienia w prostym przykładzie C#.
draft: false
keywords:
- custom resource handler
- load html document
- aspose html save
- save html to stream
- capture html output
language: pl
og_description: Dowiedz się, jak niestandardowy obsługiwacz zasobów przechwytuje wyjście
  HTML, ładuje dokument HTML i zapisuje HTML do strumienia przy użyciu Aspose HTML
  w języku C#.
og_title: Niestandardowy obsługiwacz zasobów w Aspose HTML – Przewodnik zapisu do
  strumienia
tags:
- aspose-html
- csharp
- streaming
- resource-handler
title: Niestandardowy obsługiwacz zasobów w Aspose HTML – Przewodnik zapisu do strumienia
url: /pl/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Niestandardowy Obsługujący Zasoby – Przechwytywanie Wyjścia HTML przy użyciu Aspose HTML

Zdarzyło Ci się potrzebować **niestandardowego obsługującego zasoby**, aby przechwycić każdy plik, który Aspose HTML zapisuje podczas konwersji? Być może chciałeś przekierować HTML, obrazy lub CSS bezpośrednio do pamięci zamiast na dysk. To bardzo częsty scenariusz, gdy budujesz usługę web‑ową, która musi pozostać bezstanowa lub gdy po prostu chcesz **zapisać HTML do strumienia** w celu dalszego przetwarzania.

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokazuje, jak **załadować dokument HTML**, podłączyć **niestandardowy obsługujący zasoby** oraz użyć **Aspose HTML save**, aby przechwycić każdy element wyjścia w `MemoryStream`. Po zakończeniu zrozumiesz nie tylko „co”, ale także „dlaczego” stojące za każdą linią i będziesz mieć wielokrotnego użytku wzorzec, który możesz wstawić do dowolnego projektu C#.

> **Dlaczego to ważne?**  
> Przechwytywanie wyjścia HTML w pamięci pozwala uniknąć operacji I/O na systemie plików, zmniejsza opóźnienia w funkcjach chmurowych i daje pełną kontrolę nad nazewnictwem, kompresją lub nawet transformacjami w locie.

---

## Czego będziesz potrzebować

- **.NET 6** lub nowszy (kod działa również na .NET Framework 4.7+).  
- Pakiet NuGet **Aspose.HTML for .NET** (`Aspose.Html`).  
- Prosty plik HTML (`input.html`) umieszczony w folderze, do którego możesz odwołać się.  
- Dowolne IDE, które lubisz — Visual Studio, Rider lub VS Code z rozszerzeniami C#.

Nie wymaga dodatkowej konfiguracji; API wykonuje całą ciężką pracę.

---

## Krok 1 – Utwórz Niestandardowy Obsługujący Zasoby

Sednem tej techniki jest dziedziczenie po `Aspose.Html.Rendering.ResourceHandler`. Przez nadpisanie `HandleResource` decydujesz, **gdzie** trafia każdy strumień zasobu. W naszym przypadku zwracamy nowy `MemoryStream` dla każdego żądania, co oznacza, że każdy CSS, obraz lub pod‑fragment HTML istnieje wyłącznie w pamięci RAM.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

/// <summary>
/// Custom handler that writes every resource to a new MemoryStream.
/// </summary>
class MemoryStreamHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // The ResourceInfo gives you the original URL and MIME type.
        // You could inspect it here to decide whether to skip certain files.
        // For this tutorial we just allocate a fresh stream.
        return new MemoryStream();
    }
}
```

**Wskazówka:** Jeśli musisz śledzić strumienie (np. aby później zapisać je do archiwum ZIP), przechowuj je w `Dictionary<string, MemoryStream>` kluczowanym według `resourceInfo.Uri`.

## Krok 2 – Załaduj Dokument HTML

Zanim będziesz mógł cokolwiek zapisać, musisz **załadować dokument HTML** do instancji `HTMLDocument`. Aspose HTML może odczytywać z ścieżki pliku, URL lub nawet z łańcucha znaków. Tutaj używamy lokalnego pliku dla prostoty.

```csharp
// Adjust the path to point at your real HTML file.
string htmlPath = Path.Combine(Environment.CurrentDirectory, "input.html");

// Load the source HTML document.
HTMLDocument htmlDocument = new HTMLDocument(htmlPath);
```

Jeśli Twój HTML odwołuje się do zewnętrznych zasobów (obrazy, czcionki itp.), upewnij się, że bazowy URI jest prawidłowy; w przeciwnym razie obsługujący nie będzie w stanie ich znaleźć.

## Krok 3 – Utwórz Instancję Niestandardowego Obsługującego

Teraz tworzymy instancję obsługującego, którą zdefiniowaliśmy wcześniej. Nic skomplikowanego — po prostu zwykłe `new`. Ten obiekt zostanie przekazany do metody `Save` w następnym kroku.

```csharp
// Step 3: Instantiate the custom handler.
MemoryStreamHandler resourceHandler = new MemoryStreamHandler();
```

Ponieważ obsługujący istnieje wyłącznie w pamięci, nie musisz martwić się o uprawnienia do plików ani o sprzątanie na dysku.

## Krok 4 – Zapisz Dokument przy użyciu Aspose HTML Save

Operacja **Aspose HTML save** przyjmuje `ResourceHandler`. Gdy silnik przegląda DOM i rozwiązuje każdy powiązany zasób, wywołuje `HandleResource`. Nasza implementacja zwraca `MemoryStream`, więc każdy element trafia do RAM.

```csharp
// Step 4: Save the document.
// The handler's HandleResource method will be invoked for each output stream.
htmlDocument.Save(resourceHandler);
```

W tym momencie konwersja jest zakończona, ale strumienie nadal znajdują się w pamięci. Możesz je teraz odczytać, zapisać do bazy danych lub zwrócić w odpowiedzi API.

## Krok 5 – Pobierz i Zweryfikuj Przechwycone Strumienie

Ponieważ przy każdym wywołaniu zwracaliśmy nowy `MemoryStream`, potrzebujemy sposobu na zachowanie referencji. Poniżej znajduje się szybkie rozszerzenie poprzedniego obsługującego, które przechowuje każdy strumień w słowniku, abyś mógł je przejrzeć po zapisaniu.

```csharp
class TrackingMemoryStreamHandler : ResourceHandler
{
    public Dictionary<string, MemoryStream> Streams { get; } = new();

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var ms = new MemoryStream();
        Streams[resourceInfo.Uri] = ms;   // Remember the stream by its URI.
        return ms;
    }
}

// Usage:
var trackingHandler = new TrackingMemoryStreamHandler();
htmlDocument.Save(trackingHandler);

// Example: write the main HTML output to console (as text)
if (trackingHandler.Streams.TryGetValue(htmlPath, out var mainStream))
{
    mainStream.Position = 0; // rewind
    using var reader = new StreamReader(mainStream);
    string html = reader.ReadToEnd();
    Console.WriteLine("=== Rendered HTML ===");
    Console.WriteLine(html);
}
```

Uruchomienie tego kodu wypisze finalny HTML wygenerowany przez Aspose, potwierdzając, że **przechwytywanie wyjścia HTML** działa zgodnie z oczekiwaniami.

## Przypadki Brzegowe i Częste Pytania

### 1. Co zrobić, gdy dokument jest bardzo duży?

Zużycie pamięci może rosnąć szybko. W przypadku dużych PDF‑ów lub HTML‑a z wieloma obrazami wysokiej rozdzielczości rozważ strumieniowanie bezpośrednio do `FileStream` lub **buforowanego strumienia sieciowego** zamiast `MemoryStream`. Obsługujący może podjąć decyzję na podstawie `resourceInfo.MimeType`.

### 2. Czy muszę zwalniać strumienie?

Tak. Po zakończeniu przetwarzania wywołaj `Dispose()` na każdym `MemoryStream` (lub pozwól, aby blok `using` to zrobił). W przykładzie śledzenia moglibyśmy dodać:

```csharp
foreach (var ms in trackingHandler.Streams.Values)
    ms.Dispose();
```

### 3. Czy mogę zmienić nazwę zasobów przed zapisem?

Oczywiście. Wewnątrz `HandleResource` masz dostęp do `resourceInfo.Uri`. Możesz go przekształcić, dodać prefiks lub nawet pominąć niektóre pliki, zwracając `null`.

```csharp
if (resourceInfo.MimeType.StartsWith("image/"))
    return null; // Skip images completely.
```

### 4. Czy to podejście jest bezpieczne wątkowo?

Pojedyncza instancja obsługującego nie powinna być **współdzielona** pomiędzy równoczesnymi wywołaniami `Save`. Utwórz nowy obsługujący dla każdej konwersji lub zabezpiecz wewnętrzny słownik blokadą, jeśli musisz go ponownie używać.

## Pełny Działający Przykład

Poniżej znajduje się kompletny program, który możesz wkleić do aplikacji konsolowej. Demonstruje wszystko — od załadowania pliku HTML po wypisanie przechwyconego wyjścia.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;

class TrackingMemoryStreamHandler : ResourceHandler
{
    public Dictionary<string, MemoryStream> Streams { get; } = new();

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var ms = new MemoryStream();
        Streams[resourceInfo.Uri] = ms;
        return ms;
    }
}

class SaveToStreamTutorial
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the HTML document you want to render.
        // -------------------------------------------------
        string htmlPath = Path.Combine(Environment.CurrentDirectory, "input.html");
        if (!File.Exists(htmlPath))
        {
            Console.WriteLine($"Cannot find {htmlPath}");
            return;
        }

        HTMLDocument htmlDocument = new HTMLDocument(htmlPath);

        // -------------------------------------------------
        // Step 2: Create the custom handler that captures streams.
        // -------------------------------------------------
        var handler = new TrackingMemoryStreamHandler();

        // -------------------------------------------------
        // Step 3: Save the document – Aspose will invoke our handler.
        // -------------------------------------------------
        htmlDocument.Save(handler);

        // -------------------------------------------------
        // Step 4: Retrieve the main HTML output and display it.
        // -------------------------------------------------
        if (handler.Streams.TryGetValue(htmlPath, out var mainStream))
        {
            mainStream.Position = 0; // rewind to start
            using var reader = new StreamReader(mainStream);
            string renderedHtml = reader.ReadToEnd();
            Console.WriteLine("=== Rendered HTML Output ===");
            Console.WriteLine(renderedHtml);
        }
        else
        {
            Console.WriteLine("Main HTML stream not found.");
        }

        // -------------------------------------------------
        // Step 5: Clean up.
        // -------------------------------------------------
        foreach (var ms in handler.Streams.Values)
            ms.Dispose();

        Console.WriteLine("All streams disposed. Done.");
    }
}
```

**Oczekiwany wynik:** Konsola wypisuje w pełni wyrenderowany HTML (w tym wszelki w‑linii CSS, który Aspose mógł wygenerować) oraz potwierdzenie, że wszystkie strumienie zostały zwolnione.

## Zakończenie

Właśnie nauczyłeś się, jak zaimplementować **niestandardowy obsługujący zasoby** w Aspose HTML, **załadować dokument HTML** oraz **zapisać HTML do strumienia**, jednocześnie **przechwycając wyjście HTML** do dalszego przetwarzania. Wzorzec jest lekki, świadomy wątków i w pełni rozszerzalny — możesz zamienić `MemoryStream` na plik, gniazdo sieciowe lub API przechowywania w chmurze kilkoma liniami kodu.

Następnie możesz zbadać:

- **Zapisywanie do archiwum ZIP** (idealne do pakowania HTML, CSS i obrazów).  
- **Stosowanie transformacji** (np. minifikacja CSS w locie).  
- **Strumieniowanie bezpośrednio do odpowiedzi HTTP** w ASP.NET Core w celu natychmiastowego pobrania.

Spróbuj ich, a zobaczysz, jak potężny może być dopasowany **niestandardowy obsługujący zasoby** w rzeczywistych scenariuszach. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}