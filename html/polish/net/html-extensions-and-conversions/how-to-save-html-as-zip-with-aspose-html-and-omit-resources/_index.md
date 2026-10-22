---
category: general
date: 2026-10-21
description: Dowiedz się, jak zapisać HTML jako ZIP przy użyciu Aspose.HTML, konwertować
  HTML na ZIP oraz usuwać zasoby, aby uzyskać czysty pakiet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save html as zip
- convert html to zip
- how to omit resources
- how to strip resources
- create html zip
language: pl
lastmod: 2026-10-21
og_description: Zapisz HTML jako ZIP przy użyciu Aspose.HTML, dowiedz się, jak konwertować
  HTML na ZIP i usuwać zasoby, aby uzyskać lekki archiwum.
og_image_alt: Screenshot showing the save html as zip process with resources omitted
og_title: Zapisz HTML jako ZIP przy użyciu Aspose.HTML – pomiń zasoby w jednym kroku
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to save HTML as ZIP using Aspose.HTML, convert HTML to ZIP,
    and strip resources for a clean package.
  headline: How to save HTML as ZIP with Aspose.HTML and omit resources
  type: TechArticle
tags:
- Aspose.HTML
- C#
- ZIP archive
- HTML conversion
- Resource handling
title: Jak zapisać HTML jako ZIP przy użyciu Aspose.HTML i pominąć zasoby
url: /pl/net/html-extensions-and-conversions/how-to-save-html-as-zip-with-aspose-html-and-omit-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zapisać HTML jako ZIP przy użyciu Aspose.HTML i pominąć zasoby

Jeśli potrzebujesz **zapisać HTML jako ZIP**, jednocześnie usuwając pliki zewnętrzne, ten przewodnik pokazuje kompletną, gotową do uruchomienia rozwiązanie. Po zakończeniu tutorialu będziesz w stanie **przekształcić HTML do ZIP**, kontrolować, które zasoby są zachowywane, oraz wygenerować czysty archiwum zawierające wyłącznie podstawowy kod.

Wiele scenariuszy automatyzacji sieciowej wymaga spakowania strony do użytku offline, jako załącznika e‑mail lub do archiwizacji. Dołączanie obrazów, czcionek czy skryptów często niepotrzebnie zwiększa rozmiar archiwum. Poniższe kroki wyjaśniają **jak pominąć zasoby** i **jak usuwać zasoby** z wyniku, tak aby powstały lekki plik ZIP.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

- .NET 6.0 lub nowszy zainstalowany  
- Licencję Aspose.HTML for .NET (lub darmową wersję ewaluacyjną)  
- Podstawowe środowisko programistyczne C# (Visual Studio, VS Code lub Rider)  

Nie są wymagane dodatkowe pakiety NuGet poza `Aspose.Html`.

## Krok 1: Utwórz własny obsługujący zasoby handler

Sednem **sposobu pomijania zasobów** jest podklasa `ResourceHandler`. Aspose.HTML wywołuje ten handler dla każdego zewnętrznego zasobu (obrazów, CSS, skryptów). Zwracając pusty strumień, skutecznie informujesz konwerter, aby pominął dany zasób.

```csharp
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Prevents external resources from being written to the output package.
/// </summary>
class CustomResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Returning an empty MemoryStream strips the resource from the ZIP.
        return new MemoryStream();
    }
}
```

**Dlaczego to ważne:** Domyślne zachowanie kopiuje każdy powiązany plik do ZIP, co może podwoić lub potroić rozmiar pliku. Nadpisanie `HandleResource` daje precyzyjną kontrolę bez modyfikacji oryginalnego HTML.

## Krok 2: Wczytaj dokument HTML

Wczytaj plik źródłowy przy pomocy `HTMLDocument`. Konstruktor akceptuje ścieżkę do pliku, URL lub strumień. W tym przykładzie odczytujemy lokalny plik o nazwie `input.html`.

```csharp
// Load the source HTML file from the local file system.
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

Jeśli Twój HTML znajduje się w pamięci lub pochodzi z żądania sieciowego, możesz zamiast tego przekazać `MemoryStream` lub ciąg URL. API działa w ten sam sposób.

## Krok 3: Skonfiguruj opcje zapisu

Utwórz instancję `HtmlSaveOptions` i przypisz własny handler utworzony w Kroku 1. To informuje Aspose.HTML, aby używał handlera przy każdym napotkanym zasobie.

```csharp
// Prepare save options and attach the custom resource handler.
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // The ResourceHandler property is what enables resource stripping.
    ResourceHandler = new CustomResourceHandler()
};
```

Możesz także dostosować inne opcje, np. `CompressImages = false`, jeśli chcesz zachować dane obrazów, ale nadal pominąć inne zasoby. Przykład pozostawia domyślne ustawienia kompresji.

## Krok 4: Zapisz dokument jako archiwum ZIP

Na koniec wywołaj `Save` z docelową ścieżką i skonfigurowanymi opcjami. Plik wyjściowy będzie miał rozszerzenie `.zip` i będzie zawierał `index.html` (lub oryginalną nazwę pliku) oraz **żadne zewnętrzne zasoby**.

```csharp
// Save the HTML document as a ZIP file. The archive will contain only the HTML markup.
document.Save("YOUR_DIRECTORY/output.zip", saveOptions);
```

### Oczekiwany rezultat

- `output.zip` → zawiera pojedynczy plik `index.html`.  
- Wszystkie obrazy, pliki CSS i odwołania do JavaScript są pominięte, ponieważ własny handler zwrócił pusty strumień dla każdego z nich.  

Możesz zweryfikować archiwum, otwierając je w dowolnym przeglądarce ZIP. Strona HTML nadal będzie odwoływać się do oryginalnych adresów URL, ale te pliki nie będą obecne w archiwum, co utrzymuje pakiet w minimalnym rozmiarze.

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się kompletny program, który możesz skopiować, wkleić i uruchomić. Zastąp `YOUR_DIRECTORY` rzeczywistą ścieżką do folderu na swoim komputerze.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

class Program
{
    static void Main()
    {
        // Step 1: Define a custom resource handler to control how external resources are saved.
        class CustomResourceHandler : ResourceHandler
        {
            public override Stream HandleResource(ResourceInfo info)
            {
                // Returning an empty stream strips the resource from the ZIP output.
                return new MemoryStream();
            }
        }

        // Step 2: Load an HTML document from a file.
        string inputPath = "YOUR_DIRECTORY/input.html";
        HTMLDocument document = new HTMLDocument(inputPath);

        // Step 3: Create HTML save options and assign the custom handler.
        HtmlSaveOptions saveOptions = new HtmlSaveOptions
        {
            ResourceHandler = new CustomResourceHandler()
        };

        // Step 4: Save the document as a ZIP archive containing the HTML and (now omitted) resources.
        string outputPath = "YOUR_DIRECTORY/output.zip";
        document.Save(outputPath, saveOptions);

        Console.WriteLine($"HTML has been saved as ZIP at: {outputPath}");
    }
}
```

Uruchomienie tego programu wygeneruje opisany wcześniej plik ZIP. Teraz możesz dystrybuować stronę HTML bez dołączania niepotrzebnych zasobów.

## Typowe warianty i przypadki brzegowe

| Scenariusz | Dostosowanie |
|------------|--------------|
| **Zachowaj obrazy, ale usuń CSS/JS** | W `CustomResourceHandler` sprawdzaj `info.MimeType`. Zwróć `MemoryStream` tylko dla `text/css` i `application/javascript`. |
| **Zachowaj zewnętrzne czcionki** | Zwróć oryginalny strumień dla typów MIME `font/woff2`, w przeciwnym razie zwróć pusty strumień. |
| **Wygeneruj ZIP z niestandardową nazwą wpisu** | Użyj przeciążenia `HtmlSaveOptions` `Save(string path, SaveOptions options, string entryName)`, aby określić inną nazwę pliku głównego. |
| **Konwertuj wiele plików HTML do jednego ZIP** | Iteruj po każdym pliku, twórz osobny `HTMLDocument` i dodawaj każdy do tego samego `ZipArchive` ręcznie przy pomocy `System.IO.Compression`. |

Te warianty ilustrują **sposób selektywnego usuwania zasobów**, dając pełną kontrolę nad ostatecznym rozmiarem archiwum.

## Porady profesjonalistów

- **Sprawdź wynik**: Po zapisaniu otwórz ZIP i załaduj `index.html` w przeglądarce. Brakujące zasoby pojawią się jako zepsute odnośniki, co potwierdzi działanie handlera.  
- **Wydajność**: Zwracanie pustego `MemoryStream` jest tanie, ale jeśli masz tysiące zasobów, rozważ buforowanie decyzji (np. `HashSet<string>` typów MIME do pominięcia).  
- **Licencjonowanie**: Darmowa wersja ewaluacyjna Aspose.HTML dodaje komentarz z znakiem wodnym wewnątrz HTML. Wdrożenie licencjonowanej wersji usunie go w środowisku produkcyjnym.  

## Podsumowanie

Teraz wiesz, jak **zapisać HTML jako ZIP**, **przekształcić HTML do ZIP** i **usuwać zasoby** przy użyciu Aspose.HTML dla .NET. Implementując własny `ResourceHandler`, możesz pominąć niechciane pliki i utrzymać archiwum w lekkiej formie. Eksperymentuj z logiką handlera, aby zachować tylko te zasoby, które naprawdę są potrzebne, i włącz ten wzorzec do większych potoków automatyzacji.

---

**Kolejne kroki**

- Poznaj inne funkcje `HtmlSaveOptions`, takie jak `EmbedImages`, aby osadzić obrazy bezpośrednio w HTML.  
- Połącz to podejście z `Aspose.PDF`, aby po utworzeniu ZIP przekształcić ten sam HTML w PDF.  
- Zbadaj scenariusze po stronie serwera, w których generujesz ZIP na żądanie i strumieniowo przesyłasz go do klienta bez zapisywania na dysku.  

Miłego kodowania!


## Co powinieneś nauczyć się dalej?


Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu wraz z krok‑po‑kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [How to Use ZipArchive – Save HTML and Resources to a ZIP File](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [How to Save HTML in C# – Custom Resource Handlers & ZIP](/html/english/net/working-with-html-documents/how-to-save-html-in-c-custom-resource-handlers-zip/)
- [How to Save HTML as ZIP in C# – Complete Aspose.HTML Guide](/html/english/net/html-extensions-and-conversions/how-to-save-html-as-zip-in-c-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}