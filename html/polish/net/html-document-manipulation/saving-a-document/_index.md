---
title: Zapisywanie dokumentu w .NET za pomocą Aspose.HTML
linktitle: Zapisywanie dokumentu w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Odblokuj moc Aspose.HTML dla .NET dzięki naszemu przewodnikowi krok po kroku. Naucz się tworzyć, manipulować i konwertować dokumenty HTML i SVG
weight: 16
url: /pl/net/html-document-manipulation/saving-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zapisywanie dokumentu w .NET za pomocą Aspose.HTML


W dzisiejszej erze cyfrowej tworzenie i manipulowanie dokumentami HTML i SVG jest niezbędne dla wielu programistów i firm. Aspose.HTML dla .NET to potężna biblioteka, która upraszcza te zadania, oferując różne funkcjonalności do pracy z HTML, SVG i innymi. W tym kompleksowym przewodniku zagłębimy się w podstawy Aspose.HTML dla .NET, dzieląc każdy przykład na łatwe do wykonania kroki. Niezależnie od tego, czy jesteś doświadczonym programistą, czy dopiero zaczynasz, ten przewodnik okaże się nieoceniony w wykorzystaniu możliwości Aspose.HTML.

## Wymagania wstępne

Zanim wyruszymy w tę podróż, upewnijmy się, że masz wszystko, czego potrzebujesz:

- Środowisko programistyczne: Upewnij się, że na komputerze jest zainstalowany program Visual Studio lub inne środowisko programistyczne .NET.

- Aspose.HTML dla .NET: Musisz uzyskać bibliotekę Aspose.HTML dla .NET. Możesz ją pobrać z[Tutaj](https://releases.aspose.com/html/net/).

- Znajomość języka C#: Znajomość języka programowania C# jest korzystna, ale nieobowiązkowa. Ten przewodnik jest przyjazny dla początkujących.

## Importuj przestrzeń nazw

Aby rozpocząć używanie Aspose.HTML dla .NET, musisz zaimportować niezbędne przestrzenie nazw do swojego projektu. W swoim kodzie C# uwzględnij następującą przestrzeń nazw:

### Krok 1: Importuj przestrzeń nazw Aspose.HTML
```csharp
using Aspose.Html;
```

Ta przestrzeń nazw zapewni Ci dostęp do różnych możliwości manipulowania plikami HTML i SVG.

## HTML do pliku

### Krok 1: Zainicjuj pusty dokument HTML
```csharp
// Zainicjuj pusty dokument HTML.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Utwórz element tekstowy i dodaj go do dokumentu
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Zapisz kod HTML do pliku na dysku.
    document.Save("document.html");
}
```

W tym przykładzie tworzymy dokument HTML i dodajemy do niego prosty tekst „Hello World!”. Następnie zapisujemy HTML do pliku na dysku.

## HTML bez pliku powiązanego

### Krok 1: Przygotuj prosty plik HTML
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Tutaj tworzymy podstawowy plik HTML z linkiem kotwiczącym do innego pliku.

### Krok 2: Załaduj „document.html” do pamięci
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Utwórz instancję opcji zapisywania
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //Ustaw maksymalną głębokość obsługi na 0, aby odciąć połączone pliki HTML.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // Zapisz dokument
    document.Save(@".\html-to-file-example\document.html", options);
}
```

W tym przykładzie ładujemy dokument HTML do pamięci, ustawiamy maksymalną głębokość obsługi, aby odciąć powiązane pliki, i zapisujemy dokument. 

## HTML do MHTML

### Krok 1: Przygotuj prosty plik HTML
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Podobnie jak w Przykładzie 2, tworzymy podstawowy plik HTML z linkiem kotwiczącym do innego pliku.

### Krok 2: Załaduj „document.html” do pamięci i zapisz jako MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Zapisz dokument jako MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

Tutaj ładujemy dokument HTML do pamięci i zapisujemy go w formacie MHTML.

## HTML do Markdown

### Krok 1: Przygotuj kod HTML
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 W tym kroku zdefiniujemy fragment kodu HTML zawierający`<H2>` element.

### Krok 2: Zainicjuj dokument z kodu HTML i zapisz jako Markdown
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Zapisz dokument jako plik Markdown.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

Na podstawie fragmentu kodu tworzymy dokument HTML i zapisujemy go jako plik Markdown.

## SVG do pliku

### Krok 1: Przygotuj kod SVG
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' wysokość='80' szerokość='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

Tutaj tworzymy kod SVG, który rysuje prostą, kolorową grafikę.

### Krok 2: Zainicjuj dokument SVG z kodu i zapisz na dysku
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // Zapisz plik SVG na dysku
    document.Save("document.svg");
}
```

W tym kroku utworzymy dokument SVG z kodu i zapiszemy go jako plik SVG.

## Wniosek

Aspose.HTML dla .NET to wszechstronna biblioteka, która upraszcza obsługę dokumentów HTML i SVG w aplikacjach .NET. W tym przewodniku omówiliśmy pięć podstawowych przykładów, dzieląc każdy na instrukcje krok po kroku. Niezależnie od tego, czy tworzysz, manipulujesz czy konwertujesz dokumenty, Aspose.HTML ma dla Ciebie wszystko. Postępując zgodnie z tymi krokami, jesteś na dobrej drodze do opanowania tego potężnego narzędzia.

## Najczęściej zadawane pytania

### P1: Czym jest Aspose.HTML dla .NET?

A1: Aspose.HTML for .NET to biblioteka .NET oferująca szeroką gamę funkcji do pracy z dokumentami HTML i SVG, w tym ich tworzenie, modyfikowanie i konwersję.

### P2: Gdzie mogę pobrać Aspose.HTML dla platformy .NET?

 A2: Aspose.HTML dla .NET można pobrać z[Tutaj](https://releases.aspose.com/html/net/).

### P3: Czy Aspose.HTML dla .NET nadaje się dla początkujących?

A3: Tak, Aspose.HTML dla .NET może być używany zarówno przez początkujących, jak i doświadczonych programistów. Przykłady w tym przewodniku są zaprojektowane tak, aby były przyjazne dla początkujących.

### P4: Czy mogę konwertować HTML do innych formatów za pomocą Aspose.HTML dla .NET?

A4: Tak, Aspose.HTML dla .NET obsługuje konwersję do różnych formatów, w tym MHTML i Markdown, jak pokazano w przykładach.

### P5: Gdzie mogę uzyskać pomoc dotyczącą Aspose.HTML dla .NET?

 A5: Wsparcie i odpowiedzi na swoje pytania znajdziesz na forum społeczności Aspose.HTML[Tutaj](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
