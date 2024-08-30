---
title: Konwertuj EPUB do XPS w .NET za pomocą Aspose.HTML
linktitle: Konwersja EPUB do XPS w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Dowiedz się, jak przekonwertować EPUB na XPS w .NET za pomocą Aspose.HTML dla .NET. Postępuj zgodnie z naszym przewodnikiem krok po kroku, aby uzyskać bezproblemową konwersję.
type: docs
weight: 13
url: /pl/net/html-extensions-and-conversions/convert-epub-to-xps/
---

Szukasz bezproblemowego sposobu na konwersję plików EPUB do formatu XPS w aplikacjach .NET? Aspose.HTML dla .NET zapewnia potężne rozwiązanie, aby osiągnąć to bez wysiłku. W tym przewodniku krok po kroku przeprowadzimy Cię przez proces konwersji EPUB do XPS przy użyciu Aspose.HTML. Zaczynajmy!

## Wymagania wstępne

Zanim rozpoczniesz proces konwersji pliku EPUB do XPS, musisz upewnić się, że spełnione są następujące wymagania wstępne:

### 1. Biblioteka Aspose.HTML dla .NET

 Upewnij się, że w projekcie zainstalowano bibliotekę Aspose.HTML for .NET. Jeśli tego nie zrobiłeś, możesz ją uzyskać z[Strona pobierania Aspose.HTML dla .NET](https://releases.aspose.com/html/net/).

### 2. Wprowadź plik EPUB

Będziesz potrzebować pliku EPUB, który chcesz przekonwertować na XPS. Upewnij się, że masz plik EPUB dostępny do konwersji.

### 3. Środowisko programistyczne .NET

W tym przewodniku założono, że na swoim komputerze masz już skonfigurowane środowisko programistyczne .NET.

## Importuj przestrzeń nazw

Na początek należy zaimportować niezbędną przestrzeń nazw dla Aspose.HTML:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## Konwertuj EPUB do XPS

Omówmy proces konwersji pliku EPUB do formatu XPS w kilku krokach.

### Krok 1.1: Otwórz plik EPUB

Najpierw otwórz istniejący plik EPUB do odczytu za pomocą FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Kontynuuj proces konwersji
}
```

### Krok 1.2: Utwórz XpsSaveOptions

Utwórz instancję XpsSaveOptions. Ten krok jest kluczowy dla konfiguracji wyjścia XPS:

```csharp
var options = new XpsSaveOptions();
```

### Krok 1.3: Konwersja EPUB do XPS

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

### Krok 2.2: Konwersja EPUB do XPS z opcjami niestandardowymi

Teraz wywołaj metodę ConvertEPUB, aby przekonwertować EPUB na XPS z opcjami niestandardowymi:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Użyj niestandardowego dostawcy strumienia

W tym kroku przekonwertujemy EPUB na XPS przy użyciu niestandardowego dostawcy strumieniowego, co umożliwi Ci manipulowanie danymi wynikowymi.

### Krok 3.1: Utwórz MemoryStreamProvider

Utwórz instancję MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Kontynuuj proces konwersji
}
```

### Krok 3.2: Konwertuj EPUB na XPS za pomocą Stream Provider

Konwertuj EPUB do XPS przy użyciu MemoryStreamProvider:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Krok 3.3: Dostęp i zapisywanie wyników

Pobierz strumień pamięci zawierający przekonwertowane dane i zapisz go w pliku wyjściowym:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Klasa MemoryStreamProvider Kod źródłowy

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Lista obiektów MemoryStream utworzonych podczas renderowania dokumentu
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Tę metodę wywoływana jest w przypadku, gdy wymagany jest tylko jeden strumień wyjściowy, na przykład w przypadku formatów XPS, PDF lub TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Ta metoda jest wywoływana, gdy wymagane jest utworzenie wielu strumieni wyjściowych. Na przykład podczas renderowania HTML w celu wyświetlenia listy plików graficznych (JPG, PNG itp.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Tutaj możesz zwolnić strumień wypełniony danymi i np. zrzucić go na dysk twardy
            }
            public void Dispose()
            {
                // Uwalnianie zasobów
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Gratulacje! Udało Ci się przekonwertować plik EPUB do formatu XPS przy użyciu Aspose.HTML dla .NET.

## Wniosek

W tym kompleksowym samouczku zbadaliśmy, jak wykorzystać Aspose.HTML dla .NET do konwersji plików EPUB do formatu XPS z różnymi opcjami dostosowywania. Niezależnie od tego, czy jesteś doświadczonym programistą, czy dopiero zaczynasz, Aspose.HTML upraszcza proces, umożliwiając łatwą obsługę konwersji EPUB do XPS.

 Masz jakieś pytania lub napotkałeś problemy? Sprawdź[Dokumentacja Aspose.HTML](https://reference.aspose.com/html/net/) aby uzyskać więcej informacji lub zwrócić się o pomoc do[Forum społeczności Aspose.HTML](https://forum.aspose.com/).

## Często zadawane pytania

### Czym jest Aspose.HTML dla .NET?
Aspose.HTML for .NET to zaawansowana biblioteka umożliwiająca programistom pracę z dokumentami HTML, EPUB i XPS w aplikacjach .NET.

### Gdzie mogę pobrać Aspose.HTML dla .NET?
 Aspose.HTML dla .NET można pobrać ze strony[strona do pobrania](https://releases.aspose.com/html/net/).

### Czy jest dostępna bezpłatna wersja próbna Aspose.HTML dla .NET?
 Tak, możesz otrzymać bezpłatną wersję próbną[Tutaj](https://releases.aspose.com/).

### jaki sposób mogę uzyskać tymczasową licencję na Aspose.HTML dla platformy .NET?
 Aby uzyskać tymczasową licencję, odwiedź stronę[tymczasowa strona licencji](https://purchase.aspose.com/temporary-license/).

### Gdzie mogę znaleźć więcej samouczków i dokumentacji dotyczącej Aspose.HTML dla .NET?
 Zapoznaj się z szeroką gamą samouczków i szczegółowej dokumentacji na temat[Dokumentacja Aspose.HTML](https://reference.aspose.com/html/net/) strona.