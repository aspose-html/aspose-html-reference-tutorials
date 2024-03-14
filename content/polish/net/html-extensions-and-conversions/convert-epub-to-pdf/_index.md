---
title: Konwertuj EPUB na PDF w .NET za pomocą Aspose.HTML
linktitle: Konwertuj EPUB na PDF w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Dowiedz się, jak przekonwertować EPUB na PDF za pomocą Aspose.HTML dla .NET. Ten przewodnik krok po kroku obejmuje opcje dostosowywania, często zadawane pytania i inne informacje dotyczące bezproblemowej konwersji dokumentów.
type: docs
weight: 12
url: /pl/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

W tym samouczku odkryjemy, jak używać Aspose.HTML dla .NET do konwersji plików EPUB do formatu PDF. Aspose.HTML to potężna biblioteka .NET, która zapewnia różne funkcje do pracy z dokumentami HTML i EPUB. Omówimy wymagania wstępne, zaimportujemy niezbędne przestrzenie nazw i podzielimy się wieloma przykładami, szczegółowo wyjaśniając każdy krok.

## Warunki wstępne

Zanim zaczniesz, upewnij się, że spełnione są następujące wymagania wstępne:

1. Aspose.HTML dla .NET: Upewnij się, że masz zainstalowany Aspose.HTML dla .NET w swoim projekcie .NET. Można go pobrać z[Tutaj](https://releases.aspose.com/html/net/).

2. Twój katalog danych: Będziesz potrzebował katalogu danych, w którym przechowywane są Twoje pliki EPUB.

Teraz przyjrzyjmy się krok po kroku procesowi konwersji formatu EPUB do formatu PDF przy użyciu Aspose.HTML dla .NET.

## Konwertuj EPUB na PDF

### Krok 1: Zainicjuj swój projekt

Upewnij się, że masz skonfigurowany projekt .NET i zainstalowany jest Aspose.HTML dla .NET.

### Krok 2: Zaimportuj wymagane przestrzenie nazw

W pliku kodu C# zaimportuj niezbędne przestrzenie nazw:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### Krok 3: Otwórz plik EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Przejdź do następnego kroku...
}
```

-  Zastępować`"Your Data Directory"` z rzeczywistym katalogiem, w którym znajduje się plik EPUB.
- Ten kod otwiera plik EPUB do odczytu.

### Krok 4: Ustaw opcje PDF i wykonaj konwersję

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Utwórz instancję`PdfSaveOptions` aby określić ustawienia konwersji PDF.
-  Użyj`Converter.ConvertEPUB` metoda konwersji pliku EPUB na format PDF przy użyciu podanych opcji.
- Zapisz wynikowy plik PDF jako „wyjście.pdf”.

## Określ opcje zapisywania plików PDF

### Krok 1: Zainicjuj swój projekt

Upewnij się, że masz skonfigurowany projekt .NET i zainstalowany Aspose.HTML dla .NET.

### Krok 2: Zaimportuj wymagane przestrzenie nazw

Zaimportuj niezbędne przestrzenie nazw do swojego kodu C#:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### Krok 3: Otwórz plik EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Przejdź do następnego kroku...
}
```

-  Zastępować`"Your Data Directory"` z rzeczywistym katalogiem pliku EPUB.
- Otwórz plik EPUB do odczytu.

### Krok 4: Dostosuj opcje PDF

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  Utwórz instancję`PdfSaveOptions` i dostosuj go do swoich wymagań.
- W tym przykładzie ustawiliśmy rozmiar strony na 3000 pikseli szerokości i 1000 pikseli wysokości, a kolor tła na Alice Blue.

### Krok 5: Wykonaj konwersję

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Użyj`Converter.ConvertEPUB` metoda konwersji pliku EPUB na format PDF z opcjami niestandardowymi.
- Zapisz wynikowy plik PDF jako „wyjście.pdf”.

## Użyj niestandardowego dostawcy strumienia

### Krok 1: Zainicjuj swój projekt

Skonfiguruj projekt .NET i zainstaluj Aspose.HTML dla .NET.

### Krok 2: Zaimportuj wymagane przestrzenie nazw

W kodzie C# zaimportuj niezbędne przestrzenie nazw:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### Krok 3: Otwórz plik EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Przejdź do następnego kroku...
}
```

-  Zastępować`"Your Data Directory"` z rzeczywistym katalogiem pliku EPUB.
- Otwórz plik EPUB do odczytu.

### Krok 4: Użyj niestandardowego dostawcy strumienia

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // Przejdź do następnego kroku...
}
```

-  Stwórz`MemoryStreamProvider` do zarządzania wynikiem konwersji jako strumieniem pamięci.
-  Użyj`Converter.ConvertEPUB` metodę z niestandardowym dostawcą strumienia.

### Krok 5: Zapisz wynik

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- Uzyskaj dostęp do strumienia pamięci zawierającego przekonwertowane dane.
- Ustaw pozycję strumienia na początek.
- Utwórz wyjściowy plik PDF i skopiuj do niego zawartość ze strumienia pamięci.

### Kod źródłowy klasy MemoryStreamProvider. 

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Lista obiektów MemoryStream utworzonych podczas renderowania dokumentu
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Ta metoda jest wywoływana, gdy wymagany jest tylko jeden strumień wyjściowy, na przykład w przypadku formatów XPS, PDF lub TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Ta metoda jest wywoływana, gdy wymagane jest utworzenie wielu strumieni wyjściowych. Na przykład podczas renderowania HTML na listę plików graficznych (JPG, PNG itp.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Tutaj możesz wypuścić strumień wypełniony danymi i np. zrzucić go na dysk twardy
            }
            public void Dispose()
            {
                // Uwalnianie zasobów
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Teraz nauczyłeś się konwertować pliki EPUB do formatu PDF przy użyciu Aspose.HTML dla .NET z różnymi opcjami i możliwościami dostosowywania. Aspose.HTML upraszcza proces, zapewniając elastyczność i kontrolę nad konwersją dokumentów.

## Wniosek

Aspose.HTML dla .NET to wszechstronne narzędzie do konwersji plików EPUB do formatu PDF, oferujące opcje dostosowywania w celu dostosowania wynikowego dokumentu PDF do Twoich potrzeb. Niezależnie od tego, czy potrzebujesz prostych konwersji, czy zaawansowanego dostosowywania, Aspose.HTML jest dla Ciebie rozwiązaniem.

 Jeśli jeszcze tego nie zrobiłeś, możesz pobrać Aspose.HTML dla .NET z[strona internetowa](https://releases.aspose.com/html/net/) i już dziś zacznij używać go w swoich aplikacjach .NET.

---

## Często zadawane pytania

### Czy korzystanie z Aspose.HTML dla .NET jest bezpłatne?
    Aspose.HTML dla .NET jest produktem komercyjnym, ale dostępna jest bezpłatna wersja próbna[Tutaj](https://releases.aspose.com/).

### Czy mogę dostosować wygląd przekonwertowanego pliku PDF?
   Tak, możesz dostosować wygląd pliku PDF, dostosowując opcje, takie jak rozmiar strony i kolor tła, jak pokazano w przykładzie 2.

### Jak mogę uzyskać wsparcie dla Aspose.HTML dla .NET?
    Wsparcie i zasoby znajdziesz na stronie[Forum Aspose.HTML](https://forum.aspose.com/).

### Czy są inne formaty, które mogę przekonwertować za pomocą Aspose.HTML dla .NET?
   Tak, Aspose.HTML dla .NET obsługuje różne formaty dokumentów, w tym HTML, EPUB i inne.

### Czy Aspose.HTML dla ..NET nadaje się do konwersji dokumentów na dużą skalę?
   Aspose.HTML dla .NET został zaprojektowany do wydajnej obsługi konwersji dokumentów na dużą skalę, dzięki czemu nadaje się do szerokiego zakresu zastosowań.

