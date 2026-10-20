---
category: general
date: 2026-04-05
description: Szybko twórz archiwum zip w C# — dowiedz się, jak konwertować HTML do
  ZIP, renderować HTML jako obraz oraz osadzać obrazy przy użyciu System.IO.Compression
  zip.
draft: false
keywords:
- create zip archive
- convert html to zip
- render html as image
- html with embedded images
- system.io compression zip
language: pl
og_description: Utwórz archiwum zip w C# poprzez konwersję HTML do ZIP, renderowanie
  HTML jako obrazu oraz obsługę osadzonych obrazów — wszystko za pomocą Aspose.HTML.
og_title: Tworzenie archiwum ZIP w C# – pełny przewodnik
tags:
- C#
- Aspose.HTML
- ZIP
- Image Rendering
title: Tworzenie archiwum ZIP w C# – Konwersja HTML do ZIP z osadzonymi obrazami
url: /pl/net/html-extensions-and-conversions/create-zip-archive-in-c-convert-html-to-zip-with-embedded-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie archiwum ZIP w C# – konwersja HTML do ZIP z osadzonymi obrazami

Kiedykolwiek potrzebowałeś **utworzyć archiwum zip** z strony HTML, ale nie wiedziałeś, jak spakować HTML, jego style i wygenerowany podgląd w jednym pliku? Nie jesteś sam. W wielu scenariuszach web‑to‑desktop chcesz dostarczyć samodzielny pakiet, który zawiera oryginalny znacznik **i** obraz podglądu — pomyśl o dokumentacji offline, załącznikach e‑mail czy przenośnych demo.

Dobra wiadomość? Kilka linii C# i Aspose.HTML pozwoli Ci **przekształcić HTML do ZIP**, wyrenderować stronę jako obraz i upewnić się, że każdy zasób trafi dokładnie tam, gdzie powinien w archiwum. Poniżej znajdziesz kompletną, gotową do uruchomienia implementację, a także wskazówki, dlaczego każdy element ma znaczenie.

> **Szybki efekt:** Po zakończeniu tego przewodnika będziesz mieć plik `result.zip` zawierający `input.html`, wszystkie pliki CSS lub JS oraz `preview.png` pokazujący stronę tak, jak wyglądałaby w przeglądarce.

## Czego będziesz potrzebować

- **.NET 6+** (dowolny aktualny runtime)
- **Aspose.HTML for .NET** – biblioteka, która wykonuje ciężką pracę przy parsowaniu HTML i renderowaniu obrazów.
- Mały plik HTML (`input.html`), który chcesz spakować.
- Środowisko deweloperskie — Visual Studio, VS Code lub Rider wystarczą.

Nie są wymagane dodatkowe pakiety NuGet poza Aspose.HTML; obsługa ZIP korzysta z wbudowanego namespace `System.IO.Compression`.

## Krok 1: Załaduj dokument HTML – podstawa Twojego archiwum

Pierwszą rzeczą, którą robimy, jest odczytanie pliku źródłowego HTML do obiektu `HTMLDocument`. Daje nam to manipulowalny DOM, więc możemy wstrzykiwać style, dostosowywać zasoby lub nawet zmienić znacznik przed zapisaniem.

```csharp
using Aspose.Html;
using System.IO.Compression;

// Step 1 – Load the source HTML file
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

> **Dlaczego to ważne:** Ładowanie pliku przez Aspose.HTML zapewnia prawidłowe rozwiązywanie względnych URL‑ów później, gdy osadzamy zasoby w ZIP. Daje nam także miejsce na dodanie dodatkowego CSS bez modyfikowania oryginalnego pliku na dysku.

## Krok 2: Dodaj regułę CSS – połączenie pogrubienia i podkreślenia

Czasami trzeba zagwarantować określony styl wizualny dla obrazu podglądu. Tutaj wstrzykujemy regułę CSS, która sprawia, że każdy `<h1>` jest pogrubiony **i** podkreślony. Dodanie reguły programowo oznacza, że ZIP zawsze zawiera dokładnie taki styl, jaki zamierzyłeś, niezależnie od pierwotnej strony.

```csharp
// Step 2 – Add a CSS rule that combines bold and underline styling
string style = @"
    h1 {
        font-family: 'Times New Roman';
        font-size: 36px;
        font-weight: bold;          /* bold */
        text-decoration: underline;/* underline */
    }";
document.StyleSheets.Add(style);
```

> **Pro tip:** Jeśli masz wiele bloków stylów, po prostu wywołaj `document.StyleSheets.Add(...)` dla każdego. Aspose.HTML scala je w kolejności, w jakiej zostaną dodane, tak jak przeglądarki stosują arkusze stylów.

## Krok 3: Konfiguracja renderowania obrazu – uchwycenie wysokiej jakości migawki

Chcemy, aby ZIP zawierał wyrenderowany PNG strony. Klasa `ImageRenderingOptions` pozwala kontrolować wymiary i antyaliasing, co jest niezbędne do wyraźnego podglądu.

```csharp
using Aspose.Html.Rendering.Image;

// Step 3 – Configure image rendering options (enable antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    Width = 1200,
    Height = 800,
    UseAntialiasing = true
};
```

> **Dlaczego antyaliasing?** Bez niego ukośne linie i krawędzie tekstu mogą wyglądać ząbkowanie, zwłaszcza po późniejszym skalowaniu obrazu. Włączenie antyaliasingu daje profesjonalny zrzut ekranu.

## Krok 4: Przygotuj archiwum ZIP i własny obsługujący zasoby handler

`System.IO.Compression.ZipArchive` zajmuje się niskopoziomowym tworzeniem zip, natomiast **handler zasobów** informuje Aspose.HTML, gdzie każdy plik ma zostać zapisany. Handler, którego używamy (`ZipHandler`), to cienka warstwa wokół `ZipArchive`, respektująca strukturę folderów (np. `assets/style.css` trafia do folderu `assets/` w zip).

```csharp
using System.IO;
using Aspose.Html.Saving;

// Step 4 – Create a ZIP archive and a resource handler that writes each resource into it
using (FileStream zipFileStream = new FileStream("YOUR_DIRECTORY/result.zip", FileMode.Create))
using (ZipArchive zipArchive = new ZipArchive(zipFileStream, ZipArchiveMode.Update))
{
    // ZipHandler is defined below – it knows where to place each resource
    var resourceHandler = new ZipHandler(zipArchive);
```

### Implementacja `ZipHandler`

Poniżej znajduje się minimalny, ale w pełni funkcjonalny handler. Zapisuje HTML, CSS, obrazy oraz wyrenderowany PNG do odpowiednich wpisów.

```csharp
using Aspose.Html;
using Aspose.Html.Saving;
using System.IO.Compression;

public class ZipHandler : IResourceHandler
{
    private readonly ZipArchive _archive;

    public ZipHandler(ZipArchive archive) => _archive = archive;

    public void HandleResource(ResourceSavingArgs args)
    {
        // Determine the entry name – preserve folder hierarchy if present
        string entryName = args.ResourcePath.TrimStart('/'); // e.g., "assets/style.css"
        var entry = _archive.CreateEntry(entryName, CompressionLevel.Optimal);
        using (var entryStream = entry.Open())
        {
            args.DataStream.CopyTo(entryStream);
        }

        // Let Aspose know the resource has been saved
        args.Handled = true;
    }

    // Required by the interface but not used for our simple case
    public void Dispose() { }
}
```

> **Uwaga o przypadkach brzegowych:** Jeśli Twój HTML odwołuje się do zewnętrznych URL‑ów (np. czcionek z CDN), nie zostaną one zapisane automatycznie. Musisz je najpierw pobrać lub zmienić znacznik, aby używać lokalnych kopii.

## Krok 5: Zapisz dokument – niech handler wykona ciężką pracę

Teraz łączymy wszystko. `HtmlSaveOptions` pozwala podpiąć `ResourceHandler` oraz `ImageRenderingOptions`. Gdy wywołasz `document.Save`, Aspose.HTML zapisze HTML, wszystkie powiązane zasoby **i** `preview.png` (wyrenderowany obraz) do zip.

```csharp
    // Step 5 – Configure save options
    HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions
    {
        ResourceHandler = resourceHandler,
        ImageRenderingOptions = imageOptions   // render the main page as an image inside the ZIP
    };

    // Save the document – the handler decides the location of every file
    document.Save(htmlSaveOptions);
}
```

### Jak wygląda ZIP

Po zakończeniu działania kodu, `result.zip` zawiera mniej‑więcej:

```
/input.html
/assets/style.css          (added by our custom CSS rule)
/preview.png               (1200×800 PNG of the page)
/assets/image1.jpg         (any original images referenced)
```

![Diagram procesu tworzenia archiwum zip](image.png "Diagram pokazujący przepływ od pliku HTML do archiwum zip z wyrenderowanym obrazem")

*Alt text: „diagram procesu tworzenia archiwum zip ilustrujący konwersję HTML do ZIP z osadzonymi obrazami i podglądem.”*

## Weryfikacja wyniku

1. **Otwórz ZIP** dowolnym menedżerem archiwów. Powinieneś zobaczyć `input.html`, wstrzyknięty CSS oraz `preview.png`.
2. **Kliknij dwukrotnie `preview.png`** – zauważysz, że `<h1>` jest teraz pogrubiony i podkreślony, co potwierdza, że wstrzyknięcie CSS zadziałało.
3. **Wyodrębnij `input.html`** i otwórz go w przeglądarce. Wszystkie powiązane zasoby (style, obrazy) powinny się załadować poprawnie, ponieważ znajdują się w tych samych względnych ścieżkach wewnątrz zip.

Jeśli coś wydaje się brakować, sprawdź, czy ścieżki w oryginalnym HTML są względne (np. `src="assets/logo.png"`). Absolutne URL‑e nie zostaną automatycznie przechwycone.

## Często zadawane pytania i przypadki brzegowe

### Czy mogę użyć tego do **konwersji HTML do ZIP** bez obrazu?

Tak. Po prostu pomiń przypisanie `ImageRenderingOptions` lub ustaw `htmlSaveOptions.ImageRenderingOptions = null;`. ZIP nadal będzie zawierał HTML i jego zasoby.

### Co zrobić, jeśli potrzebuję **wielu obrazów** (np. miniatury i pełnowymiarowego zrzutu)?

Utwórz kolejną instancję `ImageRenderingOptions`, dostosuj `Width`/`Height` i wywołaj `document.RenderToImage` ręcznie przed zapisem. Następnie dodaj dodatkowy PNG do zip za pomocą metody `resourceHandler.HandleResource`.

### Czy to działa na **Linux/macOS**?

Oczywiście. `System.IO.Compression` jest wieloplatformowy, a Aspose.HTML obsługuje .NET Core na wszystkich głównych systemach operacyjnych. Upewnij się jedynie, że ścieżki plików używają ukośników (`/`) lub `Path.Combine` dla przenośności.

### Jak radzić sobie z **dużymi plikami HTML**, które mogą przekraczać limity pamięci?

Aspose.HTML strumieniuje proces renderowania, ale możesz także ustawić `imageOptions.UseMemoryCache = false`, aby wymusić użycie plików tymczasowych, zmniejszając obciążenie RAM.

## Pełny kod źródłowy – gotowy do wklejenia

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Saving;

public class ZipArchiveDemo
{
    public static void Main()
    {
        // 1️⃣ Load the source HTML file
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // 2️⃣ Add a CSS rule that combines bold and underline styling
        string style = @"
            h1 {
                font-family: 'Times New Roman';
                font-size: 36px;
                font-weight: bold;          /* bold */
                text-decoration: underline;/* underline */
            }";
        document.StyleSheets.Add(style);

        // 3️⃣ Configure image rendering options (enable antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 1200,
            Height = 800,
            UseAntialiasing = true
        };

        // 4️⃣ Create a ZIP archive and a resource handler that writes each resource into it
        using (FileStream zipFileStream = new FileStream("YOUR_DIRECTORY/result.zip", FileMode.Create))
        using (ZipArchive zipArchive = new ZipArchive(zipFileStream, ZipArchiveMode.Update))
        {
            var resourceHandler = new ZipHandler(zipArchive);

            HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions
            {
                ResourceHandler = resourceHandler,
                ImageRenderingOptions = imageOptions // render the main page as an image inside the ZIP
            };

            // 5️⃣ Save the document – the handler decides the location of every file
            document.Save(htmlSaveOptions);
        }

        Console.WriteLine("✅ ZIP archive created successfully!");
    }
}

// ---------------------------------------------------------------------
// Helper class that streams each resource into the ZipArchive.
// ---------------------------------------------------------------------
public class ZipHandler : IResourceHandler, IDisposable
{
    private readonly ZipArchive _archive;

    public ZipHandler(ZipArchive archive) => _archive = archive;

    public void HandleResource(ResourceSavingArgs args)
    {
        // Preserve folder hierarchy inside the ZIP
        string entryName = args.ResourcePath.TrimStart('/');
        var entry = _archive.CreateEntry(entryName, CompressionLevel.Optimal);
        using (var entryStream = entry.Open())
        {
            args.DataStream.CopyTo(entryStream);
        }
        args.Handled = true;
    }

    public void Dispose() { }
}
```

### Oczekiwany wynik

Uruchomienie programu wypisuje:

```
✅ ZIP archive created successfully!
```

A `result.zip` zawiera plik HTML, wstrzyknięty CSS, wszystkie oryginalne zasoby oraz `preview.png`, który odzwierciedla pogrubiony i podkreślony `<h1>`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}