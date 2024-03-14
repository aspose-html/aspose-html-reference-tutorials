---
title: Skrobanie sieci w .NET za pomocą Aspose.HTML
linktitle: Skrobanie sieci w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Naucz się manipulować dokumentami HTML w .NET za pomocą Aspose.HTML. Efektywnie nawiguj, filtruj, wysyłaj zapytania i wybieraj elementy, aby usprawnić tworzenie stron internetowych.
type: docs
weight: 13
url: /pl/net/advanced-features/web-scraping/
---

dzisiejszej erze cyfrowej manipulowanie i wydobywanie informacji z dokumentów HTML jest częstym zadaniem programistów. Aspose.HTML dla .NET to potężne narzędzie, które upraszcza przetwarzanie i manipulowanie HTML w aplikacjach .NET. W tym samouczku omówimy różne aspekty Aspose.HTML dla .NET, w tym wymagania wstępne, przestrzenie nazw i przykłady krok po kroku, które pomogą Ci wykorzystać jego pełny potencjał.

## Warunki wstępne

Zanim zagłębisz się w świat Aspose.HTML dla .NET, będziesz potrzebować kilku wymagań wstępnych:

1. Środowisko programistyczne: Upewnij się, że masz skonfigurowane działające środowisko programistyczne z Visual Studio lub innym zgodnym IDE dla programowania .NET.

2.  Aspose.HTML dla .NET: Pobierz i zainstaluj bibliotekę Aspose.HTML dla .NET z[link do pobrania](https://releases.aspose.com/html/net/). W zależności od potrzeb możesz wybrać bezpłatną wersję próbną lub wersję licencjonowaną.

3. Podstawowa znajomość HTML: Znajomość struktury i elementów HTML jest niezbędna do efektywnego korzystania z Aspose.HTML dla .NET.

## Importowanie przestrzeni nazw

Aby rozpocząć, musisz zaimportować niezbędne przestrzenie nazw do swojego projektu C#. Te przestrzenie nazw zapewniają dostęp do klas i funkcjonalności Aspose.HTML for .NET:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

Po spełnieniu wymagań wstępnych i zaimportowaniu przestrzeni nazw przeanalizujmy krok po kroku kilka kluczowych przykładów, aby zilustrować, jak efektywnie używać Aspose.HTML dla .NET.

## Nawigacja po HTML

W tym przykładzie będziemy krok po kroku poruszać się po dokumencie HTML i uzyskać dostęp do jego elementów.

```csharp
public static void NavigateThroughHTML()
{
    // Przygotuj kod HTML
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    // Zainicjuj dokument z przygotowanego kodu
    using (var document = new HTMLDocument(html_code, "."))
    {
        // Uzyskaj odniesienie do pierwszego dziecka (pierwszego SPAN) BODY
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // Wyjście: Witam

        // Pobierz odwołanie do białych znaków między elementami HTML
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Wyjście: ' '

        // Pobierz odwołanie do drugiego elementu SPAN
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Wyjście: Świat!
    }
}
```

 W tym przykładzie tworzymy dokument HTML, uzyskujemy dostęp do jego pierwszego dziecka (a`SPAN` element), odstęp między elementami i drugi`SPAN` element demonstrujący podstawową nawigację.

## Korzystanie z filtrów węzłów

Filtry węzłów umożliwiają selektywne przetwarzanie określonych elementów w dokumencie HTML.

```csharp
public static void NodeFilterUsageExample()
{
    // Przygotuj kod HTML
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    // Zainicjuj dokument na podstawie przygotowanego kodu
    using (var document = new HTMLDocument(code, "."))
    {
        // Utwórz TreeWalker z niestandardowym filtrem elementów obrazu
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                // Dane wyjściowe: image1.png
                // Dane wyjściowe: image2.png
            }
        }
    }
}
```

 Ten przykład pokazuje, jak użyć niestandardowego filtru węzłów do wyodrębnienia określonych elementów (w tym przypadku`IMG` elementy) z dokumentu HTML.

## Zapytania XPath

Zapytania XPath umożliwiają wyszukiwanie elementów w dokumencie HTML na podstawie określonych kryteriów.

```csharp
public static void XPathQueryUsageExample()
{
    // Przygotuj kod HTML
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello!</span>
            </div>
        </div>
        <p class='happy'>
            <span>World</span>
        </p>
    ";
    
    // Zainicjuj dokument na podstawie przygotowanego kodu
    using (var document = new HTMLDocument(code, "."))
    {
        // Oceń wyrażenie XPath, aby wybrać określone elementy
        var result = document.Evaluate("//*[@class='szczęśliwy']//rozpiętość",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // Iteruj po powstałych węzłach
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // Wyjście: Witam
            // Wyjście: Świat!
        }
    }
}
```

Ten przykład ilustruje użycie zapytań XPath do lokalizowania elementów w dokumencie HTML na podstawie ich atrybutów i struktury.

## Selektory CSS

Selektory CSS zapewniają alternatywny sposób wybierania elementów w dokumencie HTML, podobny do tego, w jaki sposób arkusze stylów CSS wybierają elementy.

```csharp
public static void CSSSelectorUsageExample()
{
    // Przygotuj kod HTML
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello</span>
            </div>
        </div>
        <p class='happy'>
            <span>World!</span>
        </p>
    ";
    
    // Zainicjuj dokument na podstawie przygotowanego kodu
    using (var document = new HTMLDocument(code, "."))
    {
        //Użyj selektora CSS, aby wyodrębnić elementy na podstawie klasy i hierarchii
        var elements = document.QuerySelectorAll(".happy span");
        
        // Wykonaj iterację po wynikowej liście elementów
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // Wyjście: Witam
            // Wyjście: Świat!
        }
    }
}
```

Tutaj pokazujemy, jak używać selektorów CSS do kierowania na określone elementy w dokumencie HTML.

Dzięki tym przykładom zyskałeś podstawową wiedzę na temat nawigacji, filtrowania, wykonywania zapytań i wybierania elementów w dokumentach HTML przy użyciu Aspose.HTML dla .NET.

## Wniosek

 Aspose.HTML dla .NET to wszechstronna biblioteka, która umożliwia programistom .NET efektywną pracę z dokumentami HTML. Dzięki zaawansowanym funkcjom nawigacji, filtrowania, wysyłania zapytań i wybierania elementów możesz bezproblemowo obsługiwać różne zadania związane z przetwarzaniem HTML. Postępując zgodnie z tym samouczkiem i zapoznając się z dokumentacją pod adresem[Aspose.HTML dla dokumentacji .NET](https://reference.aspose.com/html/net/), możesz odblokować pełny potencjał tego narzędzia dla swoich aplikacji .NET.

## Często zadawane pytania

### Pytanie 1. Czy korzystanie z Aspose.HTML dla .NET jest darmowe?

O1: Aspose.HTML dla .NET oferuje bezpłatną wersję próbną, ale do użytku produkcyjnego musisz kupić licencję. Szczegóły i opcje dotyczące licencji można znaleźć na stronie[Zakup Aspose.HTML](https://purchase.aspose.com/buy).

### Pytanie 2. Jak mogę uzyskać tymczasową licencję na Aspose.HTML dla .NET?

 Odpowiedź 2: Możesz uzyskać tymczasową licencję do celów testowych od[Licencja tymczasowa Aspose.HTML](https://purchase.aspose.com/temporary-license/).

### Pytanie 3. Gdzie mogę szukać pomocy lub wsparcia dla Aspose.HTML dla .NET?

 A3: Jeśli napotkasz jakiekolwiek problemy lub masz pytania, możesz odwiedzić stronę[Forum Aspose.HTML](https://forum.aspose.com/) za pomoc i wsparcie społeczne.

### Pytanie 4. Czy są jakieś dodatkowe zasoby do nauki Aspose.HTML dla .NET?

 O4: Wraz z tym samouczkiem możesz poznać więcej samouczków i dokumentacji na temat[Strona dokumentacji Aspose.HTML dla .NET](https://reference.aspose.com/html/net/).

### Pytanie 5. Czy Aspose.HTML dla .NET jest kompatybilny z najnowszymi wersjami .NET?

O5: Aspose.HTML dla .NET jest regularnie aktualizowany, aby zapewnić kompatybilność z najnowszymi wersjami i technologiami .NET.