---
category: general
date: 2026-03-29
description: Dowiedz się, jak używać ZipArchive w C#, aby konwertować HTML na ZIP,
  zapisywać HTML do ZIP i kompresować obrazy HTML — wszystko w jednym przejrzystym
  tutorialu.
draft: false
keywords:
- how to use ziparchive
- convert html to zip
- save html to zip
- create zip archive c#
- compress html images
language: pl
og_description: Odkryj, jak używać ZipArchive w C#, aby konwertować HTML na ZIP, zapisywać
  HTML w ZIP oraz kompresować obrazy HTML, korzystając z pełnego, gotowego do uruchomienia
  przykładu.
og_title: Jak używać ZipArchive – Zapisz HTML i zasoby do pliku ZIP
tags:
- C#
- .NET
- Aspose.Html
- ZipArchive
title: Jak używać ZipArchive – Zapisz HTML i zasoby do pliku ZIP
url: /pl/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać ZipArchive – zapisywanie HTML i zasobów do pliku ZIP

Zastanawiałeś się kiedyś, **jak używać ZipArchive**, aby spakować stronę HTML wraz z jej obrazkami, CSS‑em i innymi zasobami? Nie jesteś sam. Wielu programistów napotyka problem, gdy muszą dostarczyć samodzielny pakiet HTML, szczególnie gdy strona odwołuje się do zewnętrznych zasobów. Dobre wieści? Kilka linii C# i Aspose.HTML pozwala **konwertować HTML do ZIP**, **zapisać HTML do ZIP**, a nawet **kompresować obrazy HTML** bez wychodzenia z IDE.

W tym tutorialu przejdziemy przez cały proces – od stworzenia prostego `HTMLDocument` po obsługę każdego powiązanego zasobu za pomocą własnego `ResourceHandler`. Na końcu będziesz mieć gotowy plik ZIP, który możesz wrzucić na dowolny serwer www lub do załącznika e‑mail. Bez zewnętrznych skryptów, bez ręcznego kopiowania – czysty .NET.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

- **.NET 6+** (lub .NET Framework 4.6+). Używane API są częścią `System.IO.Compression`.
- **Aspose.HTML for .NET** zainstalowany (pakiet NuGet `Aspose.Html`).
- Podstawową znajomość składni C#.
- IDE, takie jak Visual Studio lub VS Code.

To wszystko. Bez dodatkowych narzędzi, bez zewnętrznych programów do zipowania. Gotowy? Zaczynamy.

## Krok 1: Utwórz projekt i dodaj zależności

Utwórz nowy projekt konsolowy:

```bash
dotnet new console -n HtmlToZipDemo
cd HtmlToZipDemo
dotnet add package Aspose.Html
```

Pakiet `Aspose.Html` dostarcza klasę `HTMLDocument` oraz bazową klasę `ResourceHandler`, którą później rozszerzymy. Wbudowana przestrzeń nazw `System.IO.Compression` zapewnia `ZipArchive` i `ZipArchiveEntry`.

> **Wskazówka:** Jeśli celujesz w .NET 6, możesz używać instrukcji na najwyższym poziomie, aby utrzymać metodę `Main` w czystości. Poniższy kod używa klasy klasycznej `Program` dla przejrzystości.

## Krok 2: Stwórz własny handler zasobów

Gdy Aspose.HTML zapisuje dokument, wywołuje `ResourceHandler`, aby uzyskać `Stream` dla każdego zewnętrznego pliku (obrazy, CSS, czcionki itp.). Przez nadpisanie `HandleResource` możemy przekierować każdy zasób bezpośrednio do wpisu w archiwum ZIP.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Writes each HTML resource (image, CSS, etc.) directly into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        // Ensure a folder hierarchy inside the zip (optional but tidy)
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open(); // Aspose streams the content into this entry.
    }
}
```

**Dlaczego to ważne:** Zamiast najpierw zapisywać zasoby na dysku, a potem je zipować, handler przesyła je od razu, co zmniejsza obciążenie I/O i gwarantuje, że archiwum jest zawsze zsynchronizowane z zawartością HTML.

## Krok 3: Zbuduj dokument HTML

Dla demonstracji wstawimy mały fragment HTML, który odwołuje się do zewnętrznego obrazu `logo.png`. W prawdziwym projekcie możesz wczytać HTML z pliku lub bazy danych.

```csharp
// Create a simple HTML document with an external image reference.
HTMLDocument htmlDocument = new HTMLDocument(
    "<html><body><h1>Welcome!</h1><img src='logo.png' alt='Demo logo'></body></html>"
);
```

Jeśli chcesz **kompresować obrazy HTML**, po prostu umieść plik obrazu obok pliku wykonywalnego (lub osadź go jako zasób). `ZipResourceHandler` automatycznie doda obraz do archiwum.

## Krok 4: Otwórz (lub utwórz) plik ZIP i zapisz

Teraz łączymy wszystko. Otwieramy `FileStream` dla wyjściowego ZIP, tworzymy `ZipArchive` w trybie *Update* i przekazujemy nasz własny handler do `HTMLDocument.Save`.

```csharp
using (var fileStream = new FileStream("output.zip", FileMode.Create))
using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
{
    // Initialise the handler with the open ZipArchive.
    var zipHandler = new ZipResourceHandler(zipArchive);

    // Save the HTML document; the handler writes HTML, images, CSS, etc. into the zip.
    htmlDocument.Save(zipHandler);
}
```

Gdy bloki `using` zakończą się, archiwum zostaje sfinalizowane i zamknięte automatycznie. Powstały plik `output.zip` zawiera:

- `index.html` (zserializowany dokument HTML)
- `logo.png` (obraz odwoływany w HTML)

Możesz sprawdzić zawartość, otwierając ZIP w dowolnym eksploratorze plików.

## Krok 5: Zweryfikuj wynik (opcjonalnie)

Zawsze warto podwójnie sprawdzić, czy archiwum działa poprawnie. Oto krótki fragment, który możesz uruchomić po poprzednim kodzie, aby wypisać wpisy:

```csharp
using (var zip = ZipFile.OpenRead("output.zip"))
{
    Console.WriteLine("Contents of output.zip:");
    foreach (var entry in zip.Entries)
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
}
```

Powinieneś zobaczyć coś takiego:

```
Contents of output.zip:
- index.html (1234 bytes)
- logo.png (45678 bytes)
```

Otwórz `index.html` z wypakowanego folderu – zobaczysz poprawnie wyświetlony obraz, co potwierdza, że **zapis HTML do ZIP** zakończył się sukcesem.

## Typowe warianty i przypadki brzegowe

### 1. Użycie innej nazwy wpisu dla pliku HTML

Domyślnie Aspose zapisuje HTML jako `index.html`. Jeśli potrzebujesz własnej nazwy, ustaw `htmlDocument.FileName` przed zapisem:

```csharp
htmlDocument.FileName = "myPage.html";
htmlDocument.Save(zipHandler);
```

### 2. Ręczne dodawanie dodatkowych plików

Czasami chcesz dołączyć dodatkowe pliki (np. README). Możesz dodać je bezpośrednio do `ZipArchive` przed wywołaniem `htmlDocument.Save`:

```csharp
var readme = zipArchive.CreateEntry("README.txt", CompressionLevel.Optimal);
using (var writer = new StreamWriter(readme.Open()))
{
    writer.WriteLine("This ZIP contains an HTML page generated with Aspose.HTML.");
}
```

### 3. Efektywne obsługiwanie dużych obrazów

Jeśli HTML odwołuje się do bardzo dużych obrazów, rozważ ich zmniejszenie przed dodaniem do ZIP, aby rozmiar archiwum był rozsądny. Pakiet `System.Drawing.Common` może w tym pomóc:

```csharp
// Example: Resize logo.png to a max width of 800px before zipping.
using (var img = System.Drawing.Image.FromFile("logo.png"))
{
    int maxWidth = 800;
    if (img.Width > maxWidth)
    {
        var ratio = (double)maxWidth / img.Width;
        var newHeight = (int)(img.Height * ratio);
        using var thumb = img.GetThumbnailImage(maxWidth, newHeight, () => false, IntPtr.Zero);
        thumb.Save("logo_resized.png");
    }
}
```

Następnie w HTML użyj `<img src='logo_resized.png'>`.

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się kompletny program, który możesz skopiować do `Program.cs`. Kompiluje się i działa od razu, pod warunkiem, że zainstalowałeś pakiet NuGet Aspose.HTML.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Custom handler that streams each resource into a zip entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Create an HTML document that references an external image.
        HTMLDocument htmlDocument = new HTMLDocument(
            "<html><head><title>Demo</title></head>" +
            "<body><h2>Hello, ZipArchive!</h2>" +
            "<img src='logo.png' alt='Demo logo'></body></html>"
        );

        // 2️⃣ Open (or create) the output zip file.
        using (var fileStream = new FileStream("output.zip", FileMode.Create))
        using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
        {
            // 3️⃣ Initialise the custom handler.
            var zipHandler = new ZipResourceHandler(zipArchive);

            // 4️⃣ Save the HTML; resources get streamed into the zip.
            htmlDocument.Save(zipHandler);
        }

        Console.WriteLine("✅ HTML document and its resources have been saved to output.zip");
    }
}
```

**Oczekiwany wynik:** Konsola wypisuje komunikat sukcesu, a w folderze projektu pojawia się `output.zip` zawierający `index.html` i `logo.png`.

## Najczęściej zadawane pytania

- **Czy to działa na .NET Core?**  
  Tak. `System.IO.Compression.ZipArchive` jest częścią .NET Standard, więc ten sam kod działa na .NET 5, .NET 6 i .NET 7.

- **Co zrobić, aby **kompresować obrazy HTML** jeszcze intensywniej?**  
  Przetwórz obrazy wcześniej (zmień rozmiar, konwertuj na WebP itp.) przed ich dodaniem do ZIP. Sam handler jedynie strumieniuje otrzymane dane.

- **Czy mogę zaszyfrować ZIP?**  
  `ZipArchive` obsługuje szyfrowanie AES jedynie poprzez biblioteki firm trzecich (np. `SharpZipLib`). Jeśli potrzebujesz szyfrowania, utwórz archiwum przy użyciu takiej biblioteki, a następnie przekaż strumień do Aspose jako własny `ResourceHandler`.

- **Czy da się ustawić folder główny wewnątrz ZIP?**  
  Tak – poprzedź nazwę pliku folderem w `resourceName` w `HandleResource`, np. `var entry = _zipArchive.CreateEntry($"site/{resourceName}", ...)`.

## Podsumowanie

Teraz wiesz, **jak używać ZipArchive** w C# do **konwertowania HTML do ZIP**, **zapisywania HTML do ZIP** i **kompresowania obrazów HTML** w jednym czystym przepływie pracy. Rozszerzając `ResourceHandler` uniknęliśmy tymczasowych plików i zachowaliśmy efektywność pamięciową. Ten wzorzec skaluje się łatwo: po prostu wrzuć wygenerowany ZIP na serwer www, wyślij go mailem lub przechowuj w chmurze.

Kolejne kroki, które możesz rozważyć:

- **Tworzenie archiwów ZIP programowo** dla całych folderów witryny (`create zip archive c#`).
- **Dodawanie konwersji PDF lub DOCX** przed zipowaniem, aby uzyskać bogatsze pakiety dokumentacji.
- **Integracja z ASP.NET Core** w celu strumieniowego przesyłania ZIP bezpośrednio do przeglądarki klienta (`FileStreamResult`).

Masz więcej pytań o zipowanie HTML, obsługę czcionek lub optymalizację rozmiaru obrazów? Zostaw komentarz lub napisz do mnie na Stack Overflow. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}