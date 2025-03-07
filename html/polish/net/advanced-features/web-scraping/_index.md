---
title: Web Scraping w .NET z Aspose.HTML
linktitle: Web Scraping w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Naucz się manipulować dokumentami HTML w .NET za pomocą Aspose.HTML. Nawiguj, filtruj, wysyłaj zapytania i wybieraj elementy efektywnie, aby usprawnić tworzenie stron internetowych.
weight: 13
url: /pl/net/advanced-features/web-scraping/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Web Scraping w .NET z Aspose.HTML


dzisiejszej erze cyfrowej manipulowanie i wyodrębnianie informacji z dokumentów HTML jest powszechnym zadaniem dla programistów. Aspose.HTML dla .NET to potężne narzędzie, które upraszcza przetwarzanie i manipulację HTML w aplikacjach .NET. W tym samouczku przyjrzymy się różnym aspektom Aspose.HTML dla .NET, w tym wymaganiom wstępnym, przestrzeniom nazw i przykładom krok po kroku, które pomogą Ci wykorzystać jego pełny potencjał.

## Wymagania wstępne

Zanim zanurzysz się w świecie Aspose.HTML dla .NET, będziesz potrzebować kilku rzeczy wstępnych:

1. Środowisko programistyczne: Upewnij się, że masz skonfigurowane środowisko programistyczne z programem Visual Studio lub innym zgodnym środowiskiem IDE przeznaczonym do programowania w środowisku .NET.

2.  Aspose.HTML dla .NET: Pobierz i zainstaluj bibliotekę Aspose.HTML dla .NET z[link do pobrania](https://releases.aspose.com/html/net/)Możesz wybrać wersję próbną lub licencjonowaną, w zależności od swoich potrzeb.

3. Podstawowa znajomość HTML: Znajomość struktury i elementów HTML jest niezbędna do efektywnego korzystania z Aspose.HTML dla .NET.

## Importowanie przestrzeni nazw

Na początek musisz zaimportować niezbędne przestrzenie nazw w swoim projekcie C#. Te przestrzenie nazw zapewniają dostęp do klas i funkcjonalności Aspose.HTML dla .NET:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

Mając na uwadze wymagania wstępne i zaimportowane przestrzenie nazw, przeanalizujmy krok po kroku kilka kluczowych przykładów, aby zilustrować, jak efektywnie używać Aspose.HTML dla .NET.

## Nawigacja po HTML

W tym przykładzie pokażemy Ci, jak poruszać się po dokumencie HTML i uzyskiwać dostęp do jego elementów krok po kroku.

```csharp
public static void NavigateThroughHTML()
{
    // Przygotuj kod HTML
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    // Zainicjuj dokument z przygotowanego kodu
    using (var document = new HTMLDocument(html_code, "."))
    {
        // Pobierz odniesienie do pierwszego dziecka (pierwszego SPAN) BODY
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // Wyjście: Cześć

        // Pobierz odwołanie do odstępu między elementami HTML
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Wyjście: ' '

        // Pobierz odwołanie do drugiego elementu SPAN
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Wyjście: Świat!
    }
}
```

 W tym przykładzie tworzymy dokument HTML, uzyskujemy dostęp do jego pierwszego elementu podrzędnego (`SPAN` element), odstęp między elementami i drugi`SPAN` element, pokazujący podstawową nawigację.

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
        // Utwórz TreeWalker z niestandardowym filtrem dla elementów obrazu
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                // Wyjście: image1.png
                // Wyjście: image2.png
            }
        }
    }
}
```

 W tym przykładzie pokazano, jak używać niestandardowego filtra węzłów do wyodrębniania określonych elementów (w tym przypadku`IMG` elementów) z dokumentu HTML.

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
        var result = document.Evaluate("//*[@class='happy']//rozpiętość",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // Przeprowadź iterację po powstałych węzłach
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // Wyjście: Cześć
            // Wyjście: Świat!
        }
    }
}
```

W tym przykładzie pokazano, jak użyć zapytań XPath do zlokalizowania elementów w dokumencie HTML na podstawie ich atrybutów i struktury.

## Selektory CSS

Selektory CSS zapewniają alternatywny sposób wybierania elementów w dokumencie HTML, podobny do sposobu, w jaki arkusze stylów CSS wybierają elementy.

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
        
        // Przejrzyj wynikową listę elementów
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // Wyjście: Cześć
            // Wyjście: Świat!
        }
    }
}
```

Pokażemy tutaj, jak używać selektorów CSS, aby kierować reklamy do konkretnych elementów w dokumencie HTML.

Dzięki tym przykładom zyskasz podstawową wiedzę na temat tego, jak nawigować, filtrować, wyszukiwać i zaznaczać elementy w dokumentach HTML za pomocą Aspose.HTML dla .NET.

## Wniosek

 Aspose.HTML dla .NET to wszechstronna biblioteka, która umożliwia programistom .NET wydajną pracę z dokumentami HTML. Dzięki jej potężnym funkcjom nawigacji, filtrowania, wyszukiwania i wybierania elementów możesz bezproblemowo obsługiwać różne zadania przetwarzania HTML. Postępując zgodnie z tym samouczkiem i przeglądając dokumentację na stronie[Dokumentacja Aspose.HTML dla .NET](https://reference.aspose.com/html/net/), możesz wykorzystać cały potencjał tego narzędzia w swoich aplikacjach .NET.

## Najczęściej zadawane pytania

### P1. Czy korzystanie z Aspose.HTML dla .NET jest bezpłatne?

A1: Aspose.HTML dla .NET oferuje bezpłatną wersję próbną, ale do użytku produkcyjnego musisz kupić licencję. Szczegóły i opcje licencjonowania znajdziesz na stronie[Zakup Aspose.HTML](https://purchase.aspose.com/buy).

### P2. Jak mogę uzyskać tymczasową licencję na Aspose.HTML dla .NET?

 A2: Licencję tymczasową do celów testowych można uzyskać od[Aspose.HTML Tymczasowa licencja](https://purchase.aspose.com/temporary-license/).

### P3. Gdzie mogę szukać pomocy lub wsparcia dla Aspose.HTML dla .NET?

 A3: Jeśli napotkasz jakiekolwiek problemy lub będziesz mieć pytania, możesz odwiedzić stronę[Forum Aspose.HTML](https://forum.aspose.com/) o pomoc i wsparcie społeczności.

### P4. Czy istnieją jakieś dodatkowe zasoby do nauki języka Aspose.HTML dla platformy .NET?

 A4: Oprócz tego samouczka możesz zapoznać się z większą liczbą samouczków i dokumentacji na temat[Strona dokumentacji Aspose.HTML dla .NET](https://reference.aspose.com/html/net/).

### P5. Czy Aspose.HTML dla .NET jest kompatybilny z najnowszymi wersjami .NET?

A5: Aspose.HTML dla platformy .NET jest regularnie aktualizowany w celu zapewnienia zgodności z najnowszymi wersjami i technologiami platformy .NET.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
