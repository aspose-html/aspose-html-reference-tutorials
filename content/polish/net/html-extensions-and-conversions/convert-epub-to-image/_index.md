---
title: Konwertuj EPUB na obraz w .NET za pomocą Aspose.HTML
linktitle: Konwertuj EPUB na obraz w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Dowiedz się, jak konwertować EPUB na obrazy przy użyciu Aspose.HTML dla .NET. Samouczek krok po kroku z przykładami kodu i konfigurowalnymi opcjami.
type: docs
weight: 11
url: /pl/net/html-extensions-and-conversions/convert-epub-to-image/
---

dzisiejszej erze cyfrowej umiejętność manipulowania i konwertowania różnych formatów dokumentów jest cenną umiejętnością. Aspose.HTML dla .NET to potężne narzędzie, które pozwala programistom bez wysiłku pracować z dokumentami HTML i EPUB. W tym samouczku zagłębimy się w świat Aspose.HTML dla .NET i przeprowadzimy Cię przez proces konwersji dokumentów EPUB do różnych formatów obrazów. Podzielimy każdy przykład na wiele kroków, wyjaśniając każdy krok po drodze.

## Warunki wstępne

Zanim zagłębimy się w świat Aspose.HTML dla .NET, powinieneś upewnić się, że spełniasz następujące wymagania wstępne:

1. Visual Studio: Upewnij się, że masz zainstalowany program Visual Studio w swoim systemie. Można go pobrać ze strony internetowej.

2.  Aspose.HTML dla .NET: Bibliotekę można uzyskać ze strony internetowej Aspose[Tutaj](https://releases.aspose.com/html/net/).

3. Twój katalog danych: Przygotuj katalog, w którym będziesz przechowywać pliki EPUB i gdzie będą zapisywane obrazy wyjściowe.

4. Podstawowa znajomość języka C#: Znajomość programowania w języku C# jest niezbędna do zrozumienia i wdrożenia przykładów kodu podanych w tym samouczku.

## Importowanie niezbędnych przestrzeni nazw

Zanim zaczniemy pracować z Aspose.HTML dla .NET, musisz zaimportować wymagane przestrzenie nazw do swojego kodu C#. Te przestrzenie nazw zapewniają dostęp do funkcji Aspose.HTML for .NET.

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using Aspose.Html.Rendering.Image;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
using System.IO;
using System.Drawing;
using System.Collections.Generic;
```

Teraz, gdy mamy już wymagania wstępne i przestrzenie nazw, przejdźmy do przykładów krok po kroku.

## Konwersja EPUB na JPEG

```csharp
    string dataDir = "Your Data Directory";
    // Otwórz istniejący plik EPUB do odczytu.
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // Wywołaj metodę ConvertEPUB, aby przekonwertować plik EPUB na obraz.
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### Kroki

1. Podaj ścieżkę do pliku EPUB w zmiennej dataDir.
2. Otwórz plik EPUB do odczytu za pomocą FileStream.
3. Wywołaj metodę ConvertEPUB, przekazując strumień EPUB, opcję ImageSaveOptions określającą format wyjściowy (JPEG) i nazwę pliku wyjściowego („output.jpg”).
5. Plik EPUB jest konwertowany na obraz JPEG.

tym przykładzie otwieramy plik EPUB, czytamy jego zawartość i konwertujemy go do formatu obrazu JPEG. Obraz wyjściowy jest zapisywany jako „output.jpg”.

## Konwersja EPUB na PNG

Możesz łatwo konwertować pliki EPUB na różne formaty obrazów, takie jak PNG, BMP, GIF i TIFF, używając podobnych struktur kodu. Oto przykład konwersji do formatu PNG:

```csharp

    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Png);
        Converter.ConvertEPUB(stream, options, "output.png");
    }

```
### Kroki
1. Otwórz plik EPUB do odczytu za pomocą FileStream.
2. Zainicjuj obiekt ImageSaveOptions z żądanym formatem wyjściowym (w tym przypadku PNG).
3. Wywołaj metodę ConvertEPUB, przekazując strumień EPUB, opcje zapisu obrazu i nazwę pliku wyjściowego.
4. Plik EPUB jest konwertowany do określonego formatu obrazu.

## Określ opcje zapisywania obrazu

Możesz dostosować wyjściowy obraz, określając opcje, takie jak rozmiar strony i kolor tła. Oto przykład:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Jpeg)
        {
            PageSetup =
            {
                AnyPage = new Page()
                {
                    Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
                }
            },
            BackgroundColor = Color.AliceBlue,
        };
        Converter.ConvertEPUB(stream, options, "output.jpg");
    }
```
### Kroki

1.  Podaj ścieżkę do pliku EPUB w formacie`dataDir` zmienny.
2.  Otwórz plik EPUB do odczytu za pomocą pliku`FileStream`.
3.  Stworzyć`ImageSaveOptions` obiekt i określ żądany format wyjściowy (JPEG).
4. W razie potrzeby dostosuj rozmiar strony i kolor tła.
5.  Zadzwoń do`ConvertEPUB`metodę, przekazując strumień EPUB, opcje zapisywania obrazu i nazwę pliku wyjściowego.
6. Plik EPUB jest konwertowany na obraz z określonymi opcjami.

## Określ niestandardowego dostawcę strumienia

Jeśli chcesz manipulować strumieniem wyjściowym, możesz użyć niestandardowego dostawcy strumienia. Oto przykład:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        using (var streamProvider = new MemoryStreamProvider())
        {
            Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), streamProvider);
            
            for (int i = 0; i < streamProvider.Streams.Count; i++)
            {
                var memory = streamProvider.Streams[i];
                memory.Seek(0, SeekOrigin.Begin);
                
                using (FileStream fs = File.Create($"page_{i + 1}.jpg"))
                {
                    memory.CopyTo(fs);
                }
            }
        }
    }

```
Kod źródłowy klasy MemoryStreamProvider.

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

### Kroki
1.  Podaj ścieżkę do pliku EPUB w formacie`dataDir` zmienny.
2.  Otwórz plik EPUB do odczytu za pomocą pliku`FileStream`.
3.  Stwórz`MemoryStreamProvider` do obsługi niestandardowych strumieni wyjściowych.
4.  Zadzwoń do`ConvertEPUB` metodę, przekazując strumień EPUB, opcje zapisywania obrazu (JPEG) i niestandardowego dostawcę strumienia.
5. Iteruj po strumieniach pamięci w dostawcy niestandardowym i zapisuj je w pojedynczych plikach.
6. Ten przykład umożliwia manipulowanie i zapisywanie wielu strumieni wyjściowych w razie potrzeby.

## Wniosek

Aspose.HTML dla .NET to wszechstronna biblioteka, która upraszcza pracę z dokumentami EPUB i HTML. Dzięki możliwości konwersji dokumentów EPUB do różnych formatów obrazów i konfigurowalnym opcjom oferuje szeroką gamę aplikacji dla programistów.

---

## Często Zadawane Pytania

### 1. Gdzie mogę pobrać Aspose.HTML dla .NET?

 Możesz pobrać Aspose.HTML dla .NET ze strony wydań[Tutaj](https://releases.aspose.com/html/net/).

### 2. Jak mogę uzyskać tymczasową licencję na Aspose.HTML dla .NET?

 Aby uzyskać licencję tymczasową, odwiedź stronę licencji tymczasowej[Tutaj](https://purchase.aspose.com/temporary-license/).

### 3. Gdzie mogę znaleźć dodatkowe wsparcie dla Aspose.HTML dla .NET?

 W przypadku jakichkolwiek pytań lub problemów możesz zwrócić się o pomoc do społeczności Aspose na forum wsparcia[Tutaj](https://forum.aspose.com/).

### 4. Czy mogę konwertować dokumenty EPUB na inne formaty, takie jak PDF lub XPS?

Tak, możesz użyć Aspose.HTML dla .NET do konwersji dokumentów EPUB do różnych formatów, w tym PDF i XPS.

### 5. Czy Aspose.HTML for .NET nadaje się zarówno do małych, jak i dużych projektów?

Absolutnie! Aspose.HTML dla .NET został zaprojektowany tak, aby był skalowalny, co czyni go doskonałym wyborem dla projektów każdej wielkości.
