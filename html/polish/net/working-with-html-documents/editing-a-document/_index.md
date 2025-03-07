---
title: Edycja dokumentu w .NET za pomocą Aspose.HTML
linktitle: Edytowanie dokumentu w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Dowiedz się, jak pracować z dokumentami HTML w .NET przy użyciu Aspose.HTML. Ten kompleksowy samouczek obejmuje tworzenie, manipulację i stylizowanie dokumentów. Zacznij teraz!
weight: 12
url: /pl/net/working-with-html-documents/editing-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Edycja dokumentu w .NET za pomocą Aspose.HTML


Witamy w naszym samouczku dotyczącym korzystania z Aspose.HTML dla .NET, potężnego narzędzia do obsługi dokumentów HTML w aplikacjach .NET. W tym samouczku przeprowadzimy Cię przez podstawowe kroki pracy z dokumentami HTML przy użyciu Aspose.HTML. Niezależnie od tego, czy jesteś doświadczonym programistą, czy dopiero zaczynasz przygodę z programowaniem .NET, ten przewodnik pomoże Ci wykorzystać pełen potencjał Aspose.HTML w Twoich projektach.

## Wymagania wstępne

Zanim przejdziemy do przykładów kodu, upewnij się, że spełnione są następujące wymagania wstępne:

1. Visual Studio: Aby móc korzystać z przykładów, na komputerze musi być zainstalowany program Visual Studio.

2.  Aspose.HTML dla .NET: Powinieneś mieć zainstalowaną bibliotekę Aspose.HTML dla .NET. Możesz ją pobrać z[Tutaj](https://releases.aspose.com/html/net/).

3. Podstawowa znajomość języka C#: Znajomość programowania w języku C# będzie pomocna, ale nawet jeśli dopiero zaczynasz przygodę z tym językiem, możesz śledzić jego tajniki i uczyć się.

## Importowanie niezbędnych przestrzeni nazw

Aby zacząć używać Aspose.HTML dla .NET, musisz zaimportować wymagane przestrzenie nazw. Oto, jak możesz to zrobić:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.Dom.Css;
```

Teraz, gdy omówiliśmy już wymagania wstępne, możemy rozbić każdy przykład na kilka kroków i szczegółowo wyjaśnić każdy z nich.

## Przykład 1: Tworzenie i edytowanie dokumentu HTML

```csharp
static void EditDocumentTree()
{
    using (var document = new Aspose.Html.HTMLDocument())
    {
        var body = document.Body;
        // Utwórz element akapitu
        var p = (Aspose.Html.HTMLParagraphElement)document.CreateElement("p");
        // Ustaw atrybut niestandardowy
        p.SetAttribute("id", "my-paragraph");
        // Utwórz węzeł tekstowy
        var text = document.CreateTextNode("my first paragraph");
        // Dołącz tekst do akapitu
        p.AppendChild(text);
        // Dołącz akapit do treści dokumentu
        body.AppendChild(p);
    }
}
```

### Wyjaśnienie:

1.  Zaczynamy od utworzenia nowego dokumentu HTML za pomocą`Aspose.Html.HTMLDocument()`.

2. Uzyskujemy dostęp do elementu body dokumentu.

3. Następnie tworzymy element akapitu HTML (`<p>` ) używając`document.CreateElement("p")`.

4.  Ustawiamy niestandardowy atrybut`id` dla elementu akapitu.

5.  Węzeł tekstowy jest tworzony za pomocą`document.CreateTextNode("my first paragraph")`.

6.  Dołączamy węzeł tekstowy do elementu akapitu za pomocą`p.AppendChild(text)`.

7. Na koniec dołączamy akapit do treści dokumentu.

Ten przykład pokazuje, jak utworzyć i modyfikować strukturę dokumentu HTML.

## Przykład 2: Usuwanie elementu z dokumentu HTML

```csharp
static void EditDocumentTreeWithAppendRemoveChild()
{
    using (var document = new Aspose.Html.HTMLDocument("<p>paragraph</p><div>some element to remove</div>", "about:blank"))
    {
        var body = document.Body;
        // Pobierz element „div”
        var div = (Aspose.Html.HTMLDivElement)body.GetElementsByTagName("div").First();
        // Usuń znaleziony element
        body.RemoveChild(div);
    }
}
```

### Wyjaśnienie:

1.  Tworzymy dokument HTML z istniejącymi elementami, w tym`<p>` i`<div>`.

2. Uzyskujemy dostęp do elementu body dokumentu.

3.  Używanie`body.GetElementsByTagName("div").First()` , odzyskujemy pierwszy`<div>` element w dokumencie.

4.  Usuwamy wybrane`<div>` element z treści dokumentu za pomocą`body.RemoveChild(div)`.

W tym przykładzie pokazano, jak manipulować elementami istniejącego dokumentu HTML i usuwać je.

## Przykład 3: Edycja zawartości HTML

```csharp
static void EditHtml()
{
    using (var document = new Aspose.Html.HTMLDocument())
    {
        // Pobierz element ciała
        var body = document.Body;
        // Ustaw zawartość elementu body
        body.InnerHTML = "<p>paragraph</p>";
        // Przejdź do pierwszego dziecka
        var node = body.FirstChild;
        System.Console.WriteLine(node.LocalName);
    }
}
```

### Wyjaśnienie:

1. Tworzymy nowy dokument HTML.

2. Uzyskujemy dostęp do elementu body dokumentu.

3.  Używanie`body.InnerHTML` , ustawiamy zawartość HTML ciała na`<p>paragraph</p>`.

4.  Pobieramy pierwszy element podrzędny ciała za pomocą`body.FirstChild`.

5. Wyświetlamy na konsoli nazwę lokalną pierwszego elementu podrzędnego.

W tym przykładzie pokazano, jak ustawić i pobrać zawartość HTML elementu w dokumencie HTML.

## Przykład 4: Edycja stylów elementów

```csharp
static void EditElementStyle()
{
    using (var document = new Aspose.Html.HTMLDocument("<style>p { color: red; }</style><p>my first paragraph</p>", "about:blank"))
    {
        // Pobierz element do sprawdzenia
        var element = document.GetElementsByTagName("p")[0];
        // Pobierz obiekt widoku CSS
        var view = (Aspose.Html.Dom.Css.IViewCSS)document.Context.Window;
        // Pobierz obliczony styl elementu
        var declaration = view.GetComputedStyle(element);
        // Pobierz wartość właściwości „kolor”
        System.Console.WriteLine(declaration.Color); // rgb(255, 0, 0)
    }
}
```

### Wyjaśnienie:

1.  Tworzymy dokument HTML z osadzonym kodem CSS, który ustawia kolor`<p>` elementy na czerwono.

2.  Odzyskujemy`<p>` element używający`document.GetElementsByTagName("p")[0]`.

3.  Uzyskujemy dostęp do obiektu widoku CSS i pobieramy obliczony styl`<p>` element.

4. Pobieramy i drukujemy wartość właściwości „color”, która w CSS jest ustawiona na czerwony.

Ten przykład pokazuje, jak można sprawdzać i manipulować stylami CSS elementów HTML.

## Przykład 5: Zmiana stylu elementu za pomocą atrybutów

```csharp
static void EditElementStyleUsingAttribute()
{
    using (var document = new Aspose.Html.HTMLDocument("<style>p { color: red; }</style><p>my first paragraph</p>", "about:blank"))
    {
        // Pobierz element do edycji
        var element = (Aspose.Html.HTMLElement)document.GetElementsByTagName("p")[0];
        // Pobierz obiekt widoku CSS
        var view = (Aspose.Html.Dom.Css.IViewCSS)document.Context.Window;
        // Pobierz obliczony styl elementu
        var declaration = view.GetComputedStyle(element);
        // Ustaw kolor zielony
        element.Style.Color = "green";
        // Pobierz wartość właściwości „kolor”
        System.Console.WriteLine(declaration.Color); // rgb(0, 128, 0)
    }
}
```

### Wyjaśnienie:

1.  Tworzymy dokument HTML z osadzonym kodem CSS, który ustawia kolor`<p>` elementy na czerwono.

2.  Odzyskujemy`<p>` element używający`document.GetElementsByTagName("p")[0]`.

3.  Uzyskujemy dostęp do obiektu widoku CSS i pobieramy obliczony styl`<p>` element przed jakąkolwiek zmianą.

4.  Zmieniamy kolor`<p>` element na zielony używając`element.Style.Color = "green"`.

5. Pobieramy i drukujemy zaktualizowaną wartość „koloru”

 nieruchomość, która jest teraz zielona.

tym przykładzie pokazano, jak bezpośrednio modyfikować styl elementu HTML za pomocą atrybutów.

## Wniosek

W tym samouczku omówiliśmy podstawy korzystania z Aspose.HTML dla .NET do tworzenia, manipulowania i stylizowania dokumentów HTML w aplikacjach .NET. Przeanalizowaliśmy różne przykłady, od tworzenia dokumentu HTML po edycję jego struktury i stylów. Dzięki tym umiejętnościom możesz skutecznie obsługiwać dokumenty HTML w swoich projektach .NET.

 Jeśli masz jakiekolwiek pytania lub potrzebujesz dalszej pomocy, nie wahaj się odwiedzić naszej strony[Dokumentacja Aspose.HTML dla .NET](https://reference.aspose.com/html/net/) lub poszukaj pomocy na[Forum Aspose](https://forum.aspose.com/).

---

## Często zadawane pytania (FAQ)

### Czym jest Aspose.HTML dla .NET?
Aspose.HTML for .NET to zaawansowana biblioteka do pracy z dokumentami HTML w aplikacjach .NET.

### Gdzie mogę pobrać Aspose.HTML dla .NET?
 Możesz pobrać Aspose.HTML dla .NET z[Tutaj](https://releases.aspose.com/html/net/).

### Czy jest dostępna bezpłatna wersja próbna?
 Tak, możesz otrzymać bezpłatną wersję próbną Aspose.HTML na stronie[Tutaj](https://releases.aspose.com/).

### Jak mogę zakupić licencję?
 Aby zakupić licencję, odwiedź stronę[ten link](https://purchase.aspose.com/buy).

### Czy muszę mieć wcześniejsze doświadczenie w HTML, aby używać Aspose.HTML dla .NET?
Chociaż znajomość języka HTML jest pomocna, możesz używać Aspose.HTML dla .NET nawet jeśli nie jesteś ekspertem w tej dziedzinie.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
