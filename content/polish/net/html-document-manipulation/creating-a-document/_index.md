---
title: Tworzenie dokumentu w .NET za pomocą Aspose.HTML
linktitle: Tworzenie dokumentu w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Uwolnij moc Aspose.HTML dla .NET. Naucz się z łatwością tworzyć, manipulować i optymalizować dokumenty HTML i SVG. Zapoznaj się z przykładami krok po kroku i często zadawanymi pytaniami.
type: docs
weight: 14
url: /pl/net/html-document-manipulation/creating-a-document/
---

W stale rozwijającym się świecie tworzenia stron internetowych, wyprzedzanie konkurencji jest niezbędne. Aspose.HTML dla .NET zapewnia programistom solidny zestaw narzędzi do pracy z dokumentami HTML. Niezależnie od tego, czy zaczynasz od zera, ładujesz z pliku, pobierasz z adresu URL, czy obsługujesz dokumenty SVG, ta biblioteka oferuje wszechstronność, której potrzebujesz.

tym przewodniku krok po kroku zagłębimy się w podstawy używania Aspose.HTML dla .NET, upewniając się, że jesteś dobrze przygotowany do korzystania z tego potężnego narzędzia w swoich projektach tworzenia stron internetowych. Zanim zagłębimy się w szczegóły, przyjrzyjmy się wymaganiom wstępnym i niezbędnym przestrzeniom nazw, aby rozpocząć Twoją podróż.

## Warunki wstępne

Aby pomyślnie wykonać ten samouczek i wykorzystać moc Aspose.HTML dla .NET, będziesz potrzebować następujących wymagań wstępnych:

- Komputer z systemem Windows z zainstalowanym programem .NET Framework lub .NET Core.
- Edytor kodu, taki jak Visual Studio.
- Podstawowa znajomość programowania w języku C#.

Teraz, gdy masz już wymagania wstępne, zaczynajmy.

## Importowanie przestrzeni nazw

Zanim zaczniesz używać Aspose.HTML dla .NET, musisz zaimportować niezbędne przestrzenie nazw. Te przestrzenie nazw zawierają klasy i metody niezbędne do pracy z dokumentami HTML. Poniżej znajduje się lista przestrzeni nazw, które należy zaimportować:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Po zaimportowaniu tych przestrzeni nazw możesz teraz przejść do przykładów krok po kroku.

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

W tym przykładzie zaczynamy od utworzenia pustego dokumentu HTML i dodania tekstu „Hello World!” napisz do niego. Następnie zapisujemy dokument do pliku.

## Tworzenie dokumentu HTML z pliku

### Krok 1: Przygotuj plik „document.html”.

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### Krok 2: Załaduj z pliku „document.html”.

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Zapisz treść dokumentu w strumieniu wyjściowym.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Tutaj przygotowujemy plik z napisem „Hello World!” treść, a następnie załaduj ją jako dokument HTML. Wypisujemy treść dokumentu na konsolę.

## Tworzenie dokumentu HTML z adresu URL

### Krok 1: Załaduj dokument ze strony internetowej

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html”))
{
    // Zapisz treść dokumentu w strumieniu wyjściowym.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

W tym przykładzie ładujemy dokument HTML bezpośrednio ze strony internetowej i wyświetlamy jego zawartość.

## Tworzenie dokumentu HTML z ciągu znaków

### Krok 1: Przygotuj kod HTML

```csharp
var html_code = "<p>Hello World!</p>";
```

### Krok 2: Zainicjuj dokument ze zmiennej łańcuchowej

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Zapisz dokument na dysku.
    document.Save("document.html");
}
```

Tutaj tworzymy dokument HTML ze zmiennej łańcuchowej i zapisujemy go do pliku.

## Tworzenie dokumentu HTML z MemoryStream

### Krok 1: Utwórz obiekt strumienia pamięci

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // Zapisz kod HTML w obiekcie pamięci
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

### Krok 1: Zainicjuj dokument SVG z ciągu znaków

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // Zapisz treść dokumentu w strumieniu wyjściowym.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Tutaj tworzymy i wyświetlamy dokument SVG z ciągu znaków.

## Asynchroniczne ładowanie dokumentu HTML

### Krok 1: Utwórz instancję dokumentu HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Krok 2: Subskrybuj wydarzenie „ReadyStateChange”.

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    //Sprawdź wartość właściwości „ReadyState”.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Krok 3: Nawiguj asynchronicznie pod określonym identyfikatorem Uri

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html”);
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

W tym przykładzie asynchronicznie ładujemy dokument HTML i obsługujemy zdarzenie „ReadyStateChange”, aby wyświetlić zawartość po zakończeniu ładowania.

## Obsługa zdarzenia „OnLoad”.

### Krok 1: Utwórz instancję dokumentu HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Krok 2: Zapisz się na wydarzenie „OnLoad”.

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### Krok 3: Nawiguj asynchronicznie pod określonym identyfikatorem Uri

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html”);
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Ten przykład ilustruje asynchroniczne ładowanie dokumentu HTML i obsługę zdarzenia „OnLoad” w celu wyświetlenia zawartości po zakończeniu.

## Podsumowując

W dynamicznym świecie tworzenia stron internetowych posiadanie odpowiednich narzędzi jest kluczowe. Aspose.HTML dla .NET zapewnia środki do wydajnego tworzenia, manipulowania i przetwarzania dokumentów HTML i SVG. Ten kompleksowy przewodnik poprowadził Cię przez najważniejsze kwestie, zapewniając, że możesz wykorzystać moc Aspose.HTML dla .NET w swoich projektach.

## Często zadawane pytania

### P1: Co to jest Aspose.HTML dla .NET?

O1: Aspose.HTML dla .NET to potężna biblioteka .NET, która umożliwia programistom pracę z dokumentami HTML i SVG. Zapewnia szeroką gamę funkcji, od tworzenia dokumentów od podstaw po analizowanie i manipulowanie istniejącymi plikami HTML i SVG.

### P2: Czy mogę używać Aspose.HTML dla .NET z .NET Core?

O2: Tak, Aspose.HTML dla .NET jest kompatybilny zarówno z .NET Framework, jak i .NET Core, co czyni go wszechstronnym wyborem dla nowoczesnych aplikacji .NET.

### P3: Czy Aspose.HTML dla .NET nadaje się do skrobania i analizowania stron internetowych?

A3: Absolutnie! Aspose.HTML dla .NET to doskonały wybór do zadań związanych ze skrobaniem i analizowaniem stron internetowych, dzięki możliwości ładowania dokumentów HTML z adresów URL i ciągów znaków. Możesz wyodrębniać dane, przeprowadzać analizy i nie tylko.

### P4: Jak mogę uzyskać dostęp do wsparcia dla Aspose.HTML dla .NET?

 O4: Jeśli napotkasz jakiekolwiek problemy lub masz pytania podczas korzystania z Aspose.HTML dla .NET, możesz odwiedzić stronę[Forum Aspose](https://forum.aspose.com/) za wsparcie i pomoc ze strony społeczności i ekspertów Aspose.

### O5: Gdzie mogę znaleźć szczegółową dokumentację i opcje pobierania?

Odpowiedź 5: Obszerną dokumentację i dostęp do opcji pobierania można uzyskać, korzystając z następujących łączy:

- [Dokumentacja](https://reference.aspose.com/html/net/)
- [Pobierać](https://releases.aspose.com/html/net/)
- [Kupić](https://purchase.aspose.com/buy)
- [Bezpłatny okres próbny](https://releases.aspose.com/)
- [Licencja tymczasowa](https://purchase.aspose.com/temporary-license/)