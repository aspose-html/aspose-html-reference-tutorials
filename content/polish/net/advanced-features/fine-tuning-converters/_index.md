---
title: Dostrajanie konwerterów w .NET za pomocą Aspose.HTML
linktitle: Dostrajanie konwerterów w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Dowiedz się, jak konwertować HTML do formatu PDF, XPS i obrazów za pomocą Aspose.HTML dla .NET. Samouczek krok po kroku z przykładami kodu i często zadawanymi pytaniami.
type: docs
weight: 16
url: /pl/net/advanced-features/fine-tuning-converters/
---

## Wstęp

Aspose.HTML dla .NET to potężna biblioteka, która pozwala programistom manipulować i konwertować dokumenty HTML w różnych formatach. Niezależnie od tego, czy chcesz przekonwertować HTML na PDF, XPS lub obrazy, czy też wykonać inne zadania związane z HTML, Aspose.HTML zapewnia solidny zestaw narzędzi, które pomogą Ci wykonać to zadanie.

W tym samouczku omówimy kilka podstawowych funkcji Aspose.HTML dla .NET i przedstawimy wyjaśnienia krok po kroku dla każdego przykładu. Pod koniec tego samouczka będziesz mieć solidną wiedzę na temat używania Aspose.HTML dla .NET w aplikacjach .NET.

## Warunki wstępne

Zanim przejdziemy do przykładów, upewnij się, że spełnione są następujące wymagania wstępne:

-  Aspose.HTML dla .NET: Powinieneś mieć zainstalowaną bibliotekę Aspose.HTML dla .NET. Można go pobrać z[link do pobrania](https://releases.aspose.com/html/net/).

- Licencja tymczasowa (opcjonalna): Jeśli nie masz ważnej licencji, możesz uzyskać licencję tymczasową od[Tutaj](https://purchase.aspose.com/temporary-license/).

Przyjrzyjmy się teraz kilku typowym przypadkom użycia Aspose.HTML dla .NET.

## Importuj przestrzenie nazw

W kodzie C# zacznij od zaimportowania niezbędnych przestrzeni nazw:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## Konwertuj HTML na PDF

### Krok 1: Przygotuj kod HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Krok 2: Zainicjuj dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Utwórz urządzenie PDF i określ plik wyjściowy

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Krok 4: Renderuj HTML do formatu PDF

```csharp
document.RenderTo(device);
```

Ten przykład konwertuje fragment kodu HTML do dokumentu PDF. W razie potrzeby możesz dostosować kod HTML i plik wyjściowy.

## Ustaw niestandardowy rozmiar strony

### Krok 1: Przygotuj kod HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Krok 2: Zainicjuj dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Utwórz opcje renderowania pliku PDF

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### Krok 4: Utwórz urządzenie PDF i określ opcje oraz plik wyjściowy

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Krok 5: Renderuj HTML do formatu PDF

```csharp
document.RenderTo(device);
```

Ten przykład pokazuje, jak ustawić niestandardowy rozmiar strony dla wynikowego dokumentu PDF.

## Dostosuj rozdzielczość

### Krok 1: Przygotuj kod HTML i zapisz do pliku

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Krok 2: Zainicjuj dokument HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Krok 3: Utwórz opcje renderowania plików PDF dla niskiej rozdzielczości

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### Krok 4: Utwórz urządzenie PDF i określ opcje oraz plik wyjściowy dla niskiej rozdzielczości

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Krok 5: Renderuj HTML do formatu PDF w niskiej rozdzielczości

```csharp
document.RenderTo(device);
```

### Krok 6: Utwórz opcje renderowania plików PDF w wysokiej rozdzielczości

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### Krok 7: Utwórz urządzenie PDF i określ opcje oraz plik wyjściowy w wysokiej rozdzielczości

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Krok 8: Renderuj HTML do formatu PDF w wysokiej rozdzielczości

```csharp
document.RenderTo(device);
```

Ten przykład ilustruje, jak dostosować rozdzielczość podczas renderowania HTML do formatu PDF, biorąc pod uwagę ekrany o niskiej i wysokiej rozdzielczości.

## Określ kolor tła

### Krok 1: Przygotuj kod HTML i zapisz do pliku

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Krok 2: Zainicjuj dokument HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Krok 3: Zainicjuj opcje renderowania PDF za pomocą koloru tła

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### Krok 4: Utwórz urządzenie PDF i określ opcje oraz plik wyjściowy

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Krok 5: Renderuj HTML do formatu PDF

```csharp
document.RenderTo(device);
```

Ten przykład pokazuje, jak określić kolor tła podczas konwersji HTML do formatu PDF.

## Ustaw rozmiary lewej i prawej strony

### Krok 1: Przygotuj kod HTML

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### Krok 2: Zainicjuj dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Utwórz opcje renderowania plików PDF z rozmiarami lewej i prawej strony

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### Krok 4: Utwórz urządzenie PDF i określ opcje oraz plik wyjściowy

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Krok 5: Renderuj HTML do formatu PDF

```csharp
document.RenderTo(device);
```

Ten przykład pokazuje, jak ustawić różne rozmiary strony dla lewej i prawej strony podczas konwersji HTML do formatu PDF.

## Dopasuj rozmiar strony do treści

### Krok 1: Przygotuj kod HTML

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### Krok 2: Zainicjuj dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Utwórz opcje renderowania pliku PDF

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Krok 4: Utwórz urządzenie PDF i określ opcje oraz plik wyjściowy

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Krok 5: Renderuj HTML do formatu PDF

```csharp
document.RenderTo(device);
```

Ten przykład pokazuje, jak dostosować rozmiar strony do najszerszej zawartości podczas konwersji HTML do formatu PDF.

## Określ uprawnienia PDF

### Krok 1: Przygotuj kod HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### Krok 2: Zainicjuj dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Utwórz opcje renderowania plików PDF z uprawnieniami

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### Krok 4: Utwórz urządzenie PDF i określ opcje oraz plik wyjściowy

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Krok 5: Renderuj HTML do formatu PDF

```csharp
document.RenderTo(device);
```

Ten przykład pokazuje, jak określić uprawnienia i szyfrowanie podczas konwertowania kodu HTML do chronionego pliku PDF.

## Określ opcje specyficzne dla obrazu

### Krok 1: Przygotuj kod HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### Krok 2: Zainicjuj dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Utwórz opcje renderowania obrazu

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Krok 4: Utwórz urządzenie obrazu i określ opcje oraz plik wyjściowy

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Krok 5: Renderuj HTML do obrazu

```csharp
document.RenderTo(device);
```

Ten przykład pokazuje, jak przekonwertować kod HTML na obraz z określonymi opcjami renderowania, takimi jak format, rozdzielczość i tryb wygładzania.

## Określ opcje renderowania XPS

### Krok 1: Przygotuj kod HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Krok 2: Zainicjuj dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Utwórz opcje renderowania XPS z rozmiarem strony

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### Krok 4: Utwórz urządzenie XPS i określ opcje oraz plik wyjściowy

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### Krok 5: Renderuj HTML do XPS

```csharp
document.RenderTo(device);
```

Ten przykład pokazuje, jak przekonwertować HTML na XPS przy użyciu niestandardowego rozmiaru strony i opcji renderowania.

## Połącz wiele dokumentów HTML w plik PDF

### Krok 1: Przygotuj kod HTML dla wielu dokumentów

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### Krok 2: Utwórz dokumenty HTML do połączenia

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### Krok 3: Zainicjuj moduł renderujący HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Krok 4: Utwórz urządzenie PDF dla scalonych wyników

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Krok 5: Scal dokumenty HTML w formacie PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

Ten przykład pokazuje, jak połączyć wiele dokumentów HTML w jeden plik PDF przy użyciu Aspose.HTML dla .NET.

## Ustaw limit czasu renderowania

### Krok 1: Przygotuj kod HTML za pomocą JavaScript

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### Krok 2: Zainicjuj dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Zainicjuj moduł renderujący HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Krok 4: Utwórz urządzenie PDF i ustaw limit czasu renderowania

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Krok 5: Renderuj HTML do formatu PDF z limitem czasu

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

Ten przykład pokazuje, jak ustawić limit czasu renderowania podczas konwersji HTML do formatu PDF, co może być przydatne w przypadku treści dynamicznych lub długotrwałych skryptów.

## Wniosek

Aspose.HTML dla .NET to wszechstronna biblioteka, która umożliwia programistom efektywną pracę z dokumentami HTML. W tym samouczku omówiliśmy różne przykłady, od podstawowych konwersji HTML do PDF po bardziej zaawansowane funkcje, takie jak niestandardowe rozmiary stron, rozdzielczości i uprawnienia. Postępując zgodnie z tymi przykładami, możesz wykorzystać pełny potencjał Aspose.HTML dla .NET w swoich aplikacjach .NET.

 Jeśli masz jakieś pytania lub potrzebujesz dalszej pomocy, nie wahaj się odwiedzić witryny[Forum Aspose.HTML](https://forum.aspose.com/) o wsparcie i wskazówki.

## Często zadawane pytania

### Pytanie 1. Co to jest Aspose.HTML dla .NET?
   
O1: Aspose.HTML dla .NET to biblioteka .NET, która umożliwia programistom programowe manipulowanie i konwertowanie dokumentów HTML. Oferuje szeroką gamę funkcji do pracy z treścią HTML, w tym HTML do PDF, XPS i konwersję obrazów, a także zaawansowane opcje renderowania.

### Pytanie 2. Gdzie mogę pobrać Aspose.HTML dla .NET?

 A2: Możesz pobrać Aspose.HTML dla .NET z[link do pobrania](https://releases.aspose.com/html/net/).

### Pytanie 3. Czy potrzebuję licencji, aby używać Aspose.HTML dla .NET?

O3: Chociaż możesz używać Aspose.HTML dla .NET bez licencji, zaleca się uzyskanie licencji do użytku produkcyjnego, aby odblokować wszystkie funkcje i usunąć wszelkie znaki wodne i ograniczenia.

### Pytanie 4. Jak mogę chronić moje pliki PDF wygenerowane za pomocą Aspose.HTML dla .NET?

O4: Możesz określić uprawnienia PDF i ustawienia szyfrowania podczas renderowania HTML do formatu PDF przy użyciu Aspose.HTML dla .NET. Dzięki temu możesz kontrolować, kto może uzyskać dostęp do wynikowych plików PDF i je modyfikować.

### Pytanie 5. Czy mogę przekonwertować HTML na inne formaty, takie jak XPS lub obrazy?

O5: Tak, Aspose.HTML dla .NET obsługuje konwersję HTML do różnych formatów, w tym PDF, XPS i obrazów (np. JPEG). Możesz dostosować ustawienia konwersji, aby spełnić Twoje specyficzne wymagania.