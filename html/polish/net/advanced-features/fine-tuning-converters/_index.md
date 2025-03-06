---
title: Dokładne dostrajanie konwerterów w .NET za pomocą Aspose.HTML
linktitle: Konwertery dostrajające w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Dowiedz się, jak konwertować HTML na PDF, XPS i obrazy za pomocą Aspose.HTML dla .NET. Samouczek krok po kroku z przykładami kodu i często zadawanymi pytaniami.
weight: 16
url: /pl/net/advanced-features/fine-tuning-converters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dokładne dostrajanie konwerterów w .NET za pomocą Aspose.HTML


## Wstęp

Aspose.HTML dla .NET to potężna biblioteka, która pozwala programistom manipulować dokumentami HTML i konwertować je w różnych formatach. Niezależnie od tego, czy musisz przekonwertować HTML do PDF, XPS lub obrazów, czy wykonać inne zadania związane z HTML, Aspose.HTML zapewnia solidny zestaw narzędzi, które pomogą Ci wykonać zadanie.

tym samouczku przyjrzymy się niektórym podstawowym cechom Aspose.HTML dla .NET i przedstawimy wyjaśnienia krok po kroku dla każdego przykładu. Pod koniec tego samouczka będziesz mieć solidne zrozumienie, jak używać Aspose.HTML dla .NET w swoich aplikacjach .NET.

## Wymagania wstępne

Zanim przejdziemy do przykładów, upewnij się, że spełnione są następujące wymagania wstępne:

-  Aspose.HTML dla .NET: Powinieneś mieć zainstalowaną bibliotekę Aspose.HTML dla .NET. Możesz ją pobrać ze strony[link do pobrania](https://releases.aspose.com/html/net/).

-  Licencja tymczasowa (opcjonalnie): Jeśli nie posiadasz ważnej licencji, możesz uzyskać licencję tymczasową[Tutaj](https://purchase.aspose.com/temporary-license/).

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

## Konwertuj HTML do PDF

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

### Krok 4: Renderowanie HTML do PDF

```csharp
document.RenderTo(device);
```

Ten przykład konwertuje fragment kodu HTML na dokument PDF. Możesz dostosować kod HTML i plik wyjściowy według potrzeb.

## Ustaw niestandardowy rozmiar strony

### Krok 1: Przygotuj kod HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Krok 2: Zainicjuj dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Utwórz opcje renderowania PDF

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

### Krok 5: Renderowanie HTML do PDF

```csharp
document.RenderTo(device);
```

W tym przykładzie pokazano, jak ustawić niestandardowy rozmiar strony dla wynikowego dokumentu PDF.

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

### Krok 3: Utwórz opcje renderowania PDF dla niskiej rozdzielczości

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

### Krok 5: Renderowanie HTML do PDF w niskiej rozdzielczości

```csharp
document.RenderTo(device);
```

### Krok 6: Utwórz opcje renderowania PDF dla wysokiej rozdzielczości

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### Krok 7: Utwórz urządzenie PDF i określ opcje oraz plik wyjściowy dla wysokiej rozdzielczości

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Krok 8: Renderuj HTML do PDF w celu uzyskania wysokiej rozdzielczości

```csharp
document.RenderTo(device);
```

Przykład ten ilustruje, jak dostosować rozdzielczość podczas renderowania kodu HTML do formatu PDF, biorąc pod uwagę zarówno ekrany o niskiej, jak i wysokiej rozdzielczości.

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

### Krok 3: Zainicjuj opcje renderowania PDF z kolorem tła

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

### Krok 5: Renderowanie HTML do PDF

```csharp
document.RenderTo(device);
```

W tym przykładzie pokazano, jak określić kolor tła podczas konwersji pliku HTML do pliku PDF.

## Ustaw rozmiary strony lewej i prawej

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

### Krok 3: Utwórz opcje renderowania PDF z rozmiarami strony lewej i prawej

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

### Krok 5: Renderowanie HTML do PDF

```csharp
document.RenderTo(device);
```

Ten przykład pokazuje, jak ustawić różne rozmiary strony dla lewej i prawej strony podczas konwersji pliku HTML do pliku PDF.

## Dostosuj rozmiar strony do zawartości

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

### Krok 3: Utwórz opcje renderowania PDF

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Krok 4: Utwórz urządzenie PDF i określ opcje oraz plik wyjściowy

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Krok 5: Renderowanie HTML do PDF

```csharp
document.RenderTo(device);
```

Ten przykład pokazuje, jak dostosować rozmiar strony do najszerszej zawartości podczas konwersji HTML do PDF.

## Określ uprawnienia PDF

### Krok 1: Przygotuj kod HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### Krok 2: Zainicjuj dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Utwórz opcje renderowania PDF z uprawnieniami

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

### Krok 5: Renderowanie HTML do PDF

```csharp
document.RenderTo(device);
```

W tym przykładzie pokazano, jak określić uprawnienia i szyfrowanie podczas konwersji pliku HTML na chroniony plik PDF.

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

### Krok 5: Renderowanie HTML do obrazu

```csharp
document.RenderTo(device);
```

tym przykładzie pokazano, jak przekonwertować kod HTML na obraz przy użyciu określonych opcji renderowania, takich jak format, rozdzielczość i tryb wygładzania.

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

### Krok 5: Renderowanie HTML do XPS

```csharp
document.RenderTo(device);
```

W tym przykładzie pokazano, jak przekonwertować HTML na XPS, ustawiając niestandardowy rozmiar strony i opcje renderowania.

## Połącz wiele dokumentów HTML w PDF

### Krok 1: Przygotuj kod HTML dla wielu dokumentów

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### Krok 2: Utwórz dokumenty HTML do scalenia

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### Krok 3: Zainicjuj renderer HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Krok 4: Utwórz urządzenie PDF do scalonego wyjścia

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Krok 5: Scalanie dokumentów HTML z dokumentem PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

W tym przykładzie pokazano, jak połączyć wiele dokumentów HTML w jeden plik PDF za pomocą Aspose.HTML dla platformy .NET.

## Ustaw limit czasu renderowania

### Krok 1: Przygotuj kod HTML z JavaScript

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

### Krok 3: Zainicjuj renderer HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Krok 4: Utwórz urządzenie PDF i ustaw limit czasu renderowania

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Krok 5: Renderowanie HTML do PDF z limitem czasu

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

tym przykładzie pokazano, jak ustawić limit czasu renderowania podczas konwersji HTML do PDF. Może się to okazać przydatne w przypadku zawartości dynamicznej lub długotrwałych skryptów.

## Wniosek

Aspose.HTML dla .NET to wszechstronna biblioteka, która umożliwia programistom wydajną pracę z dokumentami HTML. W tym samouczku omówiliśmy różne przykłady, od podstawowych konwersji HTML do PDF po bardziej zaawansowane funkcje, takie jak niestandardowe rozmiary stron, rozdzielczości i uprawnienia. Postępując zgodnie z tymi przykładami, możesz wykorzystać pełny potencjał Aspose.HTML dla .NET w swoich aplikacjach .NET.

 Jeśli masz jakiekolwiek pytania lub potrzebujesz dalszej pomocy, nie wahaj się odwiedzić naszej strony[Forum Aspose.HTML](https://forum.aspose.com/) w celu uzyskania wsparcia i wskazówek.

## Najczęściej zadawane pytania

### P1. Czym jest Aspose.HTML dla .NET?
   
A1: Aspose.HTML for .NET to biblioteka .NET, która umożliwia programistom manipulowanie dokumentami HTML i ich konwersję programowo. Oferuje szeroki zakres funkcji do pracy z treścią HTML, w tym konwersję HTML do PDF, XPS i obrazów, a także zaawansowane opcje renderowania.

### P2. Gdzie mogę pobrać Aspose.HTML dla .NET?

 A2: Aspose.HTML dla .NET można pobrać ze strony[link do pobrania](https://releases.aspose.com/html/net/).

### P3. Czy potrzebuję licencji, aby używać Aspose.HTML dla .NET?

A3: Chociaż możesz używać Aspose.HTML dla platformy .NET bez licencji, zaleca się uzyskanie licencji do użytku produkcyjnego. Umożliwi to dostęp do wszystkich funkcji i usunięcie znaków wodnych lub ograniczeń.

### P4. W jaki sposób mogę chronić pliki PDF wygenerowane za pomocą Aspose.HTML dla platformy .NET?

A4: Możesz określić uprawnienia PDF i ustawienia szyfrowania podczas renderowania HTML do PDF za pomocą Aspose.HTML dla .NET. Pozwala to kontrolować, kto może uzyskać dostęp i modyfikować wynikowe pliki PDF.

### P5. Czy mogę konwertować HTML do innych formatów, takich jak XPS lub obrazy?

A5: Tak, Aspose.HTML dla .NET obsługuje konwersję HTML do różnych formatów, w tym PDF, XPS i obrazów (np. JPEG). Możesz dostosować ustawienia konwersji, aby spełnić swoje specyficzne wymagania.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
