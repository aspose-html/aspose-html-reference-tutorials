---
title: Konwertuj EPUB na XPS w .NET za pomocą Aspose.HTML
linktitle: Konwertuj EPUB na XPS w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Dowiedz się, jak przekonwertować EPUB na XPS w .NET przy użyciu Aspose.HTML dla .NET. Postępuj zgodnie z naszym przewodnikiem krok po kroku, aby dokonać konwersji bez wysiłku.
type: docs
weight: 13
url: /pl/net/html-extensions-and-conversions/convert-epub-to-xps/
---

Szukasz bezproblemowego sposobu na konwersję plików EPUB do formatu XPS w aplikacjach .NET? Aspose.HTML dla .NET zapewnia potężne rozwiązanie, które pozwala to osiągnąć bez wysiłku. W tym przewodniku krok po kroku przeprowadzimy Cię przez proces konwersji EPUB na XPS przy użyciu Aspose.HTML. Zacznijmy!

## Warunki wstępne

Zanim zagłębisz się w proces konwersji EPUB na XPS, musisz upewnić się, że spełnione są następujące wymagania wstępne:

### 1. Aspose.HTML dla biblioteki .NET

 Upewnij się, że w swoim projekcie masz zainstalowaną bibliotekę Aspose.HTML for .NET. Jeśli jeszcze tego nie zrobiłeś, możesz go uzyskać od[Strona pobierania Aspose.HTML dla .NET](https://releases.aspose.com/html/net/).

### 2. Wprowadź plik EPUB

Będziesz potrzebował pliku EPUB, który chcesz przekonwertować na XPS. Upewnij się, że masz plik EPUB do konwersji.

### 3. Środowisko programistyczne .NET

W tym przewodniku założono, że na komputerze jest skonfigurowane działające środowisko programistyczne .NET.

## Importuj przestrzeń nazw

Na początek powinieneś zaimportować niezbędną przestrzeń nazw dla Aspose.HTML:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## Konwertuj EPUB na XPS

Podzielmy proces konwersji pliku EPUB na format XPS na wiele kroków.

### Krok 1.1: Otwórz plik EPUB

Najpierw otwórz istniejący plik EPUB do odczytu za pomocą FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Kontynuuj proces konwersji
}
```

### Krok 1.2: Utwórz opcje XpsSave

Utwórz instancję XpsSaveOptions. Ten krok jest kluczowy dla konfiguracji wyjścia XPS:

```csharp
var options = new XpsSaveOptions();
```

### Krok 1.3: Konwertuj EPUB na XPS

Teraz wywołajmy metodę ConvertEPUB, aby przekonwertować EPUB na XPS:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Określ niestandardowe opcje XPS

Można dodatkowo dostosować wydruk XPS, określając opcje niestandardowe, takie jak rozmiar strony i kolor tła.

### Krok 2.1: Niestandardowy rozmiar strony i kolor tła

Utwórz instancję XpsSaveOptions z niestandardowym rozmiarem strony i kolorem tła:

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### Krok 2.2: Konwertuj EPUB na XPS za pomocą opcji niestandardowych

Teraz wywołaj metodę ConvertEPUB, aby przekonwertować plik EPUB na XPS za pomocą opcji niestandardowych:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Użyj niestandardowego dostawcy strumienia

Na tym etapie przekonwertujemy EPUB na XPS przy użyciu niestandardowego dostawcy strumieniowego, co umożliwi Ci manipulowanie wynikowymi danymi.

### Krok 3.1: Utwórz element MemoryStreamProvider

Utwórz instancję MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Kontynuuj proces konwersji
}
```

### Krok 3.2: Konwertuj EPUB na XPS za pomocą dostawcy strumienia

Konwertuj EPUB na XPS za pomocą MemoryStreamProvider:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Krok 3.3: Uzyskaj dostęp i zapisz wynik

Pobierz strumień pamięci zawierający przekonwertowane dane i zapisz go w pliku wyjściowym:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Kod źródłowy klasy MemoryStreamProvider

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
Gratulacje! Pomyślnie przekonwertowałeś plik EPUB do formatu XPS przy użyciu Aspose.HTML dla .NET.

## Wniosek

W tym kompleksowym samouczku zbadaliśmy, jak wykorzystać Aspose.HTML dla .NET do konwersji plików EPUB do formatu XPS z różnymi opcjami dostosowywania. Niezależnie od tego, czy jesteś doświadczonym programistą, czy dopiero zaczynasz, Aspose.HTML upraszcza proces, umożliwiając z łatwością obsługę konwersji EPUB na XPS.

 Masz pytania lub napotkałeś problemy? Sprawdź[Dokumentacja Aspose.HTML](https://reference.aspose.com/html/net/) aby uzyskać więcej informacji lub zwrócić się o pomoc do[Forum społeczności Aspose.HTML](https://forum.aspose.com/).

## Często Zadawane Pytania

### Co to jest Aspose.HTML dla .NET?
Aspose.HTML dla .NET to potężna biblioteka, która umożliwia programistom pracę z dokumentami HTML, EPUB i XPS w aplikacjach .NET.

### Gdzie mogę pobrać Aspose.HTML dla .NET?
 Możesz pobrać Aspose.HTML dla .NET z[strona pobierania](https://releases.aspose.com/html/net/).

### Czy dostępna jest bezpłatna wersja próbna Aspose.HTML dla .NET?
 Tak, możesz uzyskać bezpłatną wersję próbną od[Tutaj](https://releases.aspose.com/).

### Jak mogę uzyskać tymczasową licencję na Aspose.HTML dla .NET?
 Aby uzyskać licencję tymczasową, odwiedź stronę[strona licencji tymczasowej](https://purchase.aspose.com/temporary-license/).

### Gdzie mogę znaleźć więcej samouczków i dokumentacji dla Aspose.HTML dla .NET?
 Zapoznaj się z szeroką gamą samouczków i szczegółowej dokumentacji na temat[Dokumentacja Aspose.HTML](https://reference.aspose.com/html/net/) strona.