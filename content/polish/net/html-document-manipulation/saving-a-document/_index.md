---
title: Zapisywanie dokumentu w .NET za pomocą Aspose.HTML
linktitle: Zapisywanie dokumentu w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Odblokuj moc Aspose.HTML dla .NET dzięki naszemu przewodnikowi krok po kroku. Naucz się tworzyć, manipulować i konwertować dokumenty HTML i SVG
type: docs
weight: 16
url: /pl/net/html-document-manipulation/saving-a-document/
---

W dzisiejszej erze cyfrowej tworzenie dokumentów HTML i SVG oraz manipulowanie nimi jest niezbędne dla wielu twórców oprogramowania i firm. Aspose.HTML dla .NET to potężna biblioteka, która upraszcza te zadania, oferując różne funkcje do pracy z HTML, SVG i nie tylko. W tym obszernym przewodniku zagłębimy się w podstawy Aspose.HTML dla .NET, dzieląc każdy przykład na łatwe do wykonania kroki. Niezależnie od tego, czy jesteś doświadczonym programistą, czy dopiero zaczynasz, ten przewodnik będzie bezcenny w wykorzystaniu możliwości Aspose.HTML.

## Warunki wstępne

Zanim wyruszymy w tę podróż, upewnijmy się, że masz wszystko, czego potrzebujesz:

- Środowisko programistyczne: Upewnij się, że na komputerze jest zainstalowane Visual Studio lub inne środowisko programistyczne .NET.

- Aspose.HTML dla .NET: Musisz uzyskać bibliotekę Aspose.HTML dla .NET. Można go pobrać z[Tutaj](https://releases.aspose.com/html/net/).

- Znajomość języka C#: Znajomość języka programowania C# będzie korzystna, ale nie obowiązkowa. Ten przewodnik został zaprojektowany tak, aby był przyjazny dla początkujących.

## Importuj przestrzeń nazw

Aby rozpocząć korzystanie z Aspose.HTML dla .NET, musisz zaimportować niezbędne przestrzenie nazw do swojego projektu. W kodzie C# uwzględnij następującą przestrzeń nazw:

### Krok 1: Zaimportuj przestrzeń nazw Aspose.HTML
```csharp
using Aspose.Html;
```

Ta przestrzeń nazw zapewni Ci dostęp do różnych możliwości manipulacji HTML i SVG.

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

W tym przykładzie tworzymy dokument HTML i dodajemy proste „Hello World!” napisz do niego. Następnie zapisujemy kod HTML do pliku na dysku.

## HTML bez połączonego pliku

### Krok 1: Przygotuj prosty plik HTML
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Tutaj tworzymy podstawowy plik HTML z linkiem kotwiczącym do innego pliku.

### Krok 2: Załaduj plik „document.html” do pamięci
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Utwórz instancję opcji zapisu
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //Ustaw maksymalną głębokość obsługi na 0, aby odciąć połączone pliki HTML.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // Zapisz dokument
    document.Save(@".\html-to-file-example\document.html", options);
}
```

W tym przykładzie ładujemy dokument HTML do pamięci, ustawiamy maksymalną głębokość obsługi, aby odciąć połączone pliki i zapisujemy dokument. 

## HTML do MHTML

### Krok 1: Przygotuj prosty plik HTML
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Podobnie jak w przykładzie 2, tworzymy podstawowy plik HTML z kotwicą do innego pliku.

### Krok 2: Załaduj plik „document.html” do pamięci i zapisz jako MHTML
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

 Na tym etapie definiujemy fragment kodu HTML zawierający plik`<H2>` element.

### Krok 2: Zainicjuj dokument z kodu HTML i zapisz jako Markdown
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Zapisz dokument jako plik Markdown.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

Tworzymy dokument HTML z fragmentu kodu i zapisujemy go jako plik Markdown.

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

W tym kroku tworzymy dokument SVG z kodu i zapisujemy go jako plik SVG.

## Wniosek

Aspose.HTML dla .NET to wszechstronna biblioteka, która upraszcza obsługę dokumentów HTML i SVG w aplikacjach .NET. W tym przewodniku omówiliśmy pięć podstawowych przykładów, dzieląc każdy z nich na instrukcje krok po kroku. Niezależnie od tego, czy tworzysz, manipulujesz czy konwertujesz dokumenty, Aspose.HTML Ci to umożliwi. Wykonując poniższe kroki, jesteś na dobrej drodze do opanowania tego potężnego narzędzia.

## Często zadawane pytania

### P1: Co to jest Aspose.HTML dla .NET?

O1: Aspose.HTML dla .NET to biblioteka .NET, która zapewnia szeroką gamę funkcji do pracy z dokumentami HTML i SVG, w tym tworzenie, manipulowanie i konwersję.

### P2: Gdzie mogę pobrać Aspose.HTML dla .NET?

 A2: Możesz pobrać Aspose.HTML dla .NET z[Tutaj](https://releases.aspose.com/html/net/).

### P3: Czy Aspose.HTML dla .NET jest odpowiedni dla początkujących?

O3: Tak, Aspose.HTML dla .NET może być używany zarówno przez początkujących, jak i doświadczonych programistów. Przykłady zawarte w tym przewodniku zostały zaprojektowane tak, aby były przyjazne dla początkujących.

### P4: Czy mogę przekonwertować HTML na inne formaty przy użyciu Aspose.HTML dla .NET?

O4: Tak, Aspose.HTML dla .NET obsługuje konwersję do różnych formatów, w tym MHTML i Markdown, jak pokazano w przykładach.

### P5: Gdzie mogę uzyskać pomoc dotyczącą Aspose.HTML dla .NET?

 Odpowiedź 5: Możesz znaleźć pomoc i odpowiedzi na swoje pytania na forum społeczności Aspose.HTML[Tutaj](https://forum.aspose.com/).