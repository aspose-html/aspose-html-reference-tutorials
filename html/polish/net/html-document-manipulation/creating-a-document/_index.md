---
title: Tworzenie dokumentu w .NET z Aspose.HTML
linktitle: Tworzenie dokumentu w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Uwolnij moc Aspose.HTML dla .NET. Naucz się łatwo tworzyć, manipulować i optymalizować dokumenty HTML i SVG. Poznaj przykłady krok po kroku i często zadawane pytania.
weight: 14
url: /pl/net/html-document-manipulation/creating-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie dokumentu w .NET z Aspose.HTML


W ciągle ewoluującym świecie rozwoju sieci WWW, bycie o krok przed innymi jest niezbędne. Aspose.HTML dla .NET zapewnia programistom solidny zestaw narzędzi do pracy z dokumentami HTML. Niezależnie od tego, czy zaczynasz od zera, ładujesz z pliku, pobierasz z adresu URL lub obsługujesz dokumenty SVG, ta biblioteka oferuje wszechstronność, której potrzebujesz.

tym przewodniku krok po kroku zagłębimy się w podstawy korzystania z Aspose.HTML dla .NET, zapewniając, że jesteś dobrze wyposażony do korzystania z tego potężnego narzędzia w swoich projektach rozwoju sieci. Zanim przejdziemy do szczegółów, omówmy wymagania wstępne i niezbędne przestrzenie nazw, aby rozpocząć swoją podróż.

## Wymagania wstępne

Aby pomyślnie ukończyć ten samouczek i wykorzystać potencjał Aspose.HTML dla platformy .NET, musisz spełnić następujące wymagania wstępne:

- Komputer z systemem Windows i zainstalowanym środowiskiem .NET Framework lub .NET Core.
- Edytor kodu, taki jak Visual Studio.
- Podstawowa znajomość programowania w języku C#.

Teraz, gdy spełniliśmy już wszystkie wymagania wstępne, możemy zaczynać.

## Importowanie przestrzeni nazw

Zanim zaczniesz używać Aspose.HTML dla .NET, musisz zaimportować niezbędne przestrzenie nazw. Te przestrzenie nazw zawierają klasy i metody, które są niezbędne do pracy z dokumentami HTML. Poniżej znajduje się lista przestrzeni nazw, które powinieneś zaimportować:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Po zaimportowaniu tych przestrzeni nazw możesz przejść do przykładów krok po kroku.

## Tworzenie dokumentu HTML od podstaw

### Krok 1: Zainicjuj pusty dokument HTML

```csharp
// Zainicjuj pusty dokument HTML.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Utwórz element tekstowy i dodaj go do dokumentu
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Zapisz dokument na dysku.
    document.Save("document.html");
}
```

W tym przykładzie zaczynamy od utworzenia pustego dokumentu HTML i dodania do niego tekstu „Hello World!”. Następnie zapisujemy dokument do pliku.

## Tworzenie dokumentu HTML z pliku

### Krok 1: Przygotuj plik „document.html”

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### Krok 2: Załaduj z pliku „document.html”

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Zapisz zawartość dokumentu do strumienia wyjściowego.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Tutaj przygotowujemy plik z treścią „Hello World!”, a następnie ładujemy go jako dokument HTML. Drukujemy zawartość dokumentu na konsoli.

## Tworzenie dokumentu HTML z adresu URL

### Krok 1: Załaduj dokument ze strony internetowej

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html”))
{
    // Zapisz zawartość dokumentu do strumienia wyjściowego.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

W tym przykładzie ładujemy dokument HTML bezpośrednio ze strony internetowej i wyświetlamy jego zawartość.

## Tworzenie dokumentu HTML z ciągu znaków

### Krok 1: Przygotuj kod HTML

```csharp
var html_code = "<p>Hello World!</p>";
```

### Krok 2: Zainicjuj dokument ze zmiennej ciągu

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Zapisz dokument na dysku.
    document.Save("document.html");
}
```

Tutaj tworzymy dokument HTML ze zmiennej ciągu i zapisujemy go do pliku.

## Tworzenie dokumentu HTML z MemoryStream

### Krok 1: Utwórz obiekt strumienia pamięci

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // Wpisz kod HTML do obiektu pamięci
    sw.Write("<p>Hello World!</p>");
    // Ustaw pozycję na początek
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // Zainicjuj dokument ze strumienia pamięci
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // Zapisz dokument na dysku.
        document.Save("document.html");
    }
}
```

W tym przykładzie tworzymy dokument HTML ze strumienia pamięci i zapisujemy go do pliku.

## Praca z dokumentami SVG

### Krok 1: Zainicjuj dokument SVG z ciągu

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // Zapisz zawartość dokumentu do strumienia wyjściowego.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Tutaj tworzymy i wyświetlamy dokument SVG z ciągu znaków.

## Asynchroniczne ładowanie dokumentu HTML

### Krok 1: Utwórz wystąpienie dokumentu HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Krok 2: Subskrybuj wydarzenie „ReadyStateChange”

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    // Sprawdź wartość właściwości „ReadyState”.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Krok 3: Nawiguj asynchronicznie w określonym adresie URI

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html”);
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

W tym przykładzie ładujemy dokument HTML asynchronicznie i obsługujemy zdarzenie „ReadyStateChange”, aby wyświetlić zawartość po zakończeniu ładowania.

## Obsługa zdarzenia „OnLoad”

### Krok 1: Utwórz wystąpienie dokumentu HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Krok 2: Subskrybuj wydarzenie „OnLoad”

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### Krok 3: Nawiguj asynchronicznie w określonym adresie URI

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html”);
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

W tym przykładzie pokazano asynchroniczne ładowanie dokumentu HTML i obsługę zdarzenia „OnLoad” w celu wyświetlenia zawartości po zakończeniu.

## Podsumowując

W dynamicznym świecie rozwoju sieci, posiadanie odpowiednich narzędzi jest kluczowe. Aspose.HTML dla .NET wyposaża Cię w środki do wydajnego tworzenia, manipulowania i przetwarzania dokumentów HTML i SVG. Ten kompleksowy przewodnik przeprowadzi Cię przez podstawy, zapewniając, że możesz wykorzystać moc Aspose.HTML dla .NET w swoich projektach.

## Najczęściej zadawane pytania

### P1: Czym jest Aspose.HTML dla .NET?

A1: Aspose.HTML for .NET to potężna biblioteka .NET, która umożliwia programistom pracę z dokumentami HTML i SVG. Zapewnia szeroki zakres funkcji, od tworzenia dokumentów od podstaw po parsowanie i manipulowanie istniejącymi plikami HTML i SVG.

### P2: Czy mogę używać Aspose.HTML dla .NET z .NET Core?

A2: Tak, Aspose.HTML dla .NET jest kompatybilny zarówno z .NET Framework, jak i .NET Core, co czyni go wszechstronnym wyborem dla nowoczesnych aplikacji .NET.

### P3: Czy Aspose.HTML dla .NET nadaje się do scrapowania i parsowania stron internetowych?

A3: Oczywiście! Aspose.HTML dla .NET to doskonały wybór do zadań web scrapingu i parsowania, dzięki możliwości ładowania dokumentów HTML z adresów URL i ciągów znaków. Możesz wyodrębnić dane, przeprowadzić analizę i wiele więcej.

### P4: W jaki sposób mogę uzyskać dostęp do pomocy technicznej dla Aspose.HTML dla .NET?

 A4: Jeśli podczas korzystania z Aspose.HTML dla .NET napotkasz jakiekolwiek problemy lub będziesz mieć pytania, możesz odwiedzić stronę[Forum Aspose](https://forum.aspose.com/) aby uzyskać wsparcie i pomoc od społeczności i ekspertów Aspose.

### A5: Gdzie mogę znaleźć szczegółową dokumentację i opcje pobierania?

A5: Aby uzyskać pełną dokumentację i dostęp do opcji pobierania, zapoznaj się z poniższymi linkami:

- [Dokumentacja](https://reference.aspose.com/html/net/)
- [Pobierać](https://releases.aspose.com/html/net/)
- [Kupić](https://purchase.aspose.com/buy)
- [Bezpłatna wersja próbna](https://releases.aspose.com/)
- [Licencja tymczasowa](https://purchase.aspose.com/temporary-license/)
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
