---
title: Konwertuj HTML na MHTML w .NET za pomocą Aspose.HTML
linktitle: Konwertuj HTML na MHTML w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Konwertuj HTML na MHTML w .NET za pomocą Aspose.HTML - przewodnik krok po kroku dotyczący wydajnej archiwizacji treści internetowych. Dowiedz się, jak używać Aspose.HTML dla .NET do tworzenia archiwów MHTML.
type: docs
weight: 19
url: /pl/net/html-extensions-and-conversions/convert-html-to-mhtml/
---

W świecie tworzenia stron internetowych wydajna konwersja dokumentów ma kluczowe znaczenie. Biblioteka Aspose.HTML dla .NET to potężne narzędzie, które upraszcza konwersję dokumentów HTML do różnych formatów, w tym MHTML. MHTML, skrót od „MIME HTML”, to format archiwum stron internetowych, który umożliwia zapisanie strony internetowej i jej zasobów w jednym pliku. W tym przewodniku krok po kroku przeprowadzimy Cię przez proces konwersji dokumentu HTML do MHTML przy użyciu Aspose.HTML dla .NET.

## Warunki wstępne

Zanim przejdziemy do procesu konwersji, upewnij się, że spełnione są następujące wymagania wstępne:

### 1. Aspose.HTML dla biblioteki .NET

 Musisz mieć zainstalowaną bibliotekę Aspose.HTML for .NET. Jeśli jeszcze tego nie zrobiłeś, możesz pobrać go ze strony internetowej[Tutaj](https://releases.aspose.com/html/net/). Postępuj zgodnie z instrukcjami instalacji podanymi na stronie internetowej.

### 2. Przykładowy dokument HTML

Aby przeprowadzić konwersję, będziesz potrzebować dokumentu HTML. Upewnij się, że masz gotowy przykładowy plik HTML. Możesz użyć własnego dokumentu HTML lub pobrać próbkę z[Dokumentacja Aspose.HTML](https://reference.aspose.com/html/net/).

Teraz, gdy masz już wymagania wstępne, przejdźmy do konwersji.

## Importuj przestrzeń nazw

Najpierw musisz zaimportować niezbędne przestrzenie nazw do swojego kodu C#. Jest to niezbędne, aby uzyskać dostęp do klas i metod udostępnianych przez bibliotekę Aspose.HTML.

### Zaimportuj wymaganą przestrzeń nazw

```csharp
using Aspose.Html;
```

Po zaimportowaniu niezbędnej przestrzeni nazw możesz przejść do właściwego procesu konwersji.

Dla przejrzystości podzielimy konwersję dokumentu HTML na MHTML na kilka etapów.

## Załaduj dokument HTML

```csharp
string dataDir = "Your Data Directory"; // Określ katalog danych
HTMLDocument htmlDocument = new HTMLDocument(dataDir + "input.html"); // Załaduj dokument HTML
```

W tym kroku podajesz ścieżkę do dokumentu HTML. Aspose.HTML ładuje plik HTML, przygotowując go do konwersji.

## Zainicjuj HTMLSaveOptions

```csharp
MHTMLSaveOptions options = new MHTMLSaveOptions();
```

 Tutaj inicjujesz`MHTMLSaveOptions` class, która udostępnia opcje konwersji MHTML.

## Ustaw reguły obsługi zasobów

```csharp
options.ResourceHandlingOptions.MaxHandlingDepth = 1;
```

Możesz ustawić reguły obsługi zasobów w oparciu o swoje wymagania. W tym przykładzie ograniczamy maksymalną głębokość obsługi do 1, co oznacza, że w pliku MHTML będzie zawarty tylko główny dokument HTML i jego bezpośrednie zasoby.

## Określ ścieżkę wyjściową

```csharp
string outputMHTML = dataDir + "HTMLtoMHTML_Output.mht"; // Określ ścieżkę pliku wyjściowego
```

W tym kroku określisz ścieżkę do wynikowego pliku MHTML. Tutaj zostanie zapisany przekonwertowany dokument MHTML.

## Wykonaj konwersję

```csharp
Converter.ConvertHTML(htmlDocument, options, outputMHTML);
```

 Teraz nadszedł czas na konwersję dokumentu HTML na MHTML. The`ConvertHTML` Metoda przyjmuje załadowany dokument HTML, ustawione opcje i ścieżkę pliku wyjściowego jako parametry.

Gratulacje! Pomyślnie przekonwertowałeś dokument HTML na MHTML przy użyciu Aspose.HTML dla .NET. Możesz teraz uzyskać dostęp do pliku MHTML pod określoną ścieżką wyjściową.

## Wniosek

Efektywna konwersja dokumentów HTML do formatu MHTML to cenna umiejętność dla twórców stron internetowych i twórców treści. Aspose.HTML dla .NET upraszcza ten proces, czyniąc go dostępnym i przyjaznym dla użytkownika. Postępując zgodnie ze szczegółowym przewodnikiem opisanym powyżej, możesz bez wysiłku tworzyć archiwa MHTML swoich treści internetowych.

Odpowiedzmy teraz na niektóre często zadawane pytania (FAQ), aby zapewnić większą jasność w tym temacie.

## Często zadawane pytania

### Co to jest MHTML i dlaczego jest używany?

MHTML, skrót od „MIME HTML”, to format archiwum stron internetowych, który umożliwia zapisanie strony internetowej i jej zasobów w jednym pliku. Jest powszechnie używany do archiwizowania treści internetowych, udostępniania stron internetowych w postaci pojedynczych plików i zapewniania uwzględnienia wszystkich zasobów (obrazów, arkuszy stylów itp.), nawet jeśli są hostowane na różnych serwerach.

### Czy mogę dostosować obsługę zasobów podczas konwersji do MHTML?

 Tak, możesz. Jak pokazano w przykładzie, możesz ustawić reguły obsługi zasobów za pomocą`ResourceHandlingOptions` z`MHTMLSaveOptions`klasa. Możesz kontrolować głębokość uwzględniania zasobów w pliku MHTML.

### Gdzie mogę znaleźć więcej zasobów i dokumentacji dla Aspose.HTML dla .NET?

 Możesz zwiedzać[Dokumentacja Aspose.HTML](https://reference.aspose.com/html/net/) aby uzyskać szczegółowe informacje, samouczki i odniesienia do API. Dodatkowo,[Forum Aspose.HTML](https://forum.aspose.com/) to świetne miejsce, w którym możesz szukać pomocy i omawiać wszelkie problemy lub pytania, jakie możesz mieć.

### Czy dostępna jest bezpłatna wersja próbna Aspose.HTML dla .NET?

 Tak, możesz uzyskać bezpłatną wersję próbną Aspose.HTML dla .NET, odwiedzając stronę[ten link](https://releases.aspose.com/). Wersja próbna umożliwia zapoznanie się z funkcjami biblioteki przed dokonaniem zakupu.

### Jak uzyskać tymczasową licencję na Aspose.HTML dla .NET?

 Jeśli potrzebujesz licencji tymczasowej, możesz ją uzyskać w witrynie[Witryna Aspose.Purchase](https://purchase.aspose.com/temporary-license/). Ta tymczasowa licencja zapewni Ci dostęp do pełnej funkcjonalności biblioteki przez ograniczony czas.

