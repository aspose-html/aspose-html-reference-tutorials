---
title: Konwersja EPUB do obrazu w .NET za pomocą Aspose.HTML
linktitle: Konwersja EPUB na obraz w .NET
second_title: Aspose.HTML .NET API manipulacji HTML
description: Dowiedz się, jak konwertować EPUB na obrazy za pomocą Aspose.HTML dla .NET. Samouczek krok po kroku z przykładami kodu i opcjami dostosowywania.
weight: 11
url: /pl/net/html-extensions-and-conversions/convert-epub-to-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwersja EPUB do obrazu w .NET za pomocą Aspose.HTML


dzisiejszej erze cyfrowej umiejętność manipulowania i konwertowania różnych formatów dokumentów jest cenną umiejętnością. Aspose.HTML dla .NET to potężne narzędzie, które pozwala deweloperom bezproblemowo pracować z dokumentami HTML i EPUB. W tym samouczku zagłębimy się w świat Aspose.HTML dla .NET i przeprowadzimy Cię przez proces konwersji dokumentów EPUB do różnych formatów obrazów. Podzielimy każdy przykład na wiele kroków, wyjaśniając każdy krok po drodze.

## Wymagania wstępne

Zanim zagłębimy się w świat Aspose.HTML dla .NET, upewnij się, że spełnione są następujące wymagania wstępne:

1. Visual Studio: Upewnij się, że masz zainstalowany Visual Studio w swoim systemie. Możesz go pobrać ze strony internetowej.

2.  Aspose.HTML dla .NET: Bibliotekę można pobrać ze strony internetowej Aspose[Tutaj](https://releases.aspose.com/html/net/).

3. Twój katalog danych: Przygotuj katalog, w którym będziesz przechowywać pliki EPUB i w którym będą zapisywane obrazy wyjściowe.

4. Podstawowa znajomość języka C#: Znajomość programowania w języku C# jest niezbędna do zrozumienia i wdrożenia przykładów kodu przedstawionych w tym samouczku.

## Importowanie niezbędnych przestrzeni nazw

Zanim zaczniemy pracę z Aspose.HTML dla .NET, musisz zaimportować wymagane przestrzenie nazw do swojego kodu C#. Te przestrzenie nazw zapewniają dostęp do funkcji Aspose.HTML dla .NET.

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

Teraz, gdy mamy już wymagania wstępne i przestrzenie nazw, możemy przejść do przykładów krok po kroku.

## Konwersja EPUB do JPEG

```csharp
    string dataDir = "Your Data Directory";
    // Otwórz istniejący plik EPUB do odczytania.
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // Wywołaj metodę ConvertEPUB, aby przekonwertować plik EPUB na obraz.
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### Kroki

1. Podaj ścieżkę do pliku EPUB w zmiennej dataDir.
2. Otwórz plik EPUB do odczytu za pomocą FileStream.
3. Wywołaj metodę ConvertEPUB, przekazując strumień EPUB, ImageSaveOptions określający format wyjściowy (JPEG) i nazwę pliku wyjściowego („output.jpg”).
5. Plik EPUB zostanie przekonwertowany na obraz JPEG.

tym przykładzie otwieramy plik EPUB, odczytujemy jego zawartość i konwertujemy go do formatu obrazu JPEG. Obraz wyjściowy jest zapisywany jako „output.jpg”.

## Konwersja EPUB do PNG

Możesz łatwo konwertować pliki EPUB do różnych formatów obrazów, takich jak PNG, BMP, GIF i TIFF, używając podobnych struktur kodu. Oto przykład konwersji do PNG:

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
2. Zainicjuj obiekt ImageSaveOptions z pożądanym formatem wyjściowym (w tym przypadku PNG).
3. Wywołaj metodę ConvertEPUB, przekazując strumień EPUB, opcje zapisu obrazu i nazwę pliku wyjściowego.
4. Plik EPUB zostanie przekonwertowany do określonego formatu obrazu.

## Określ opcje zapisywania obrazu

Możesz dostosować wyjście obrazu, określając opcje, takie jak rozmiar strony i kolor tła. Oto przykład:

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

1.  Podaj ścieżkę do pliku EPUB w`dataDir` zmienny.
2.  Otwórz plik EPUB do odczytu za pomocą`FileStream`.
3.  Utwórz`ImageSaveOptions` obiekt i określ żądany format wyjściowy (JPEG).
4. W razie potrzeby dostosuj rozmiar strony i kolor tła.
5.  Zadzwoń`ConvertEPUB`metodę, przekazując strumień EPUB, opcje zapisu obrazu i nazwę pliku wyjściowego.
6. Plik EPUB zostanie przekonwertowany na obraz z określonymi opcjami.

## Określ niestandardowego dostawcę strumienia

Jeśli musisz manipulować strumieniem wyjściowym, możesz użyć niestandardowego dostawcy strumienia. Oto przykład:

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

### Kroki
1.  Podaj ścieżkę do pliku EPUB w`dataDir` zmienny.
2.  Otwórz plik EPUB do odczytu za pomocą`FileStream`.
3.  Utwórz`MemoryStreamProvider` do obsługi niestandardowych strumieni wyjściowych.
4.  Zadzwoń`ConvertEPUB` metoda, przekazująca strumień EPUB, opcje zapisu obrazu (JPEG) i niestandardowego dostawcę strumienia.
5. Przejrzyj strumienie pamięci w niestandardowym dostawcy i zapisz je w osobnych plikach.
6. Ten przykład umożliwia manipulowanie wieloma strumieniami wyjściowymi i zapisywanie ich według potrzeb.

## Wniosek

Aspose.HTML dla .NET to wszechstronna biblioteka, która upraszcza pracę z dokumentami EPUB i HTML. Dzięki możliwości konwersji dokumentów EPUB do różnych formatów obrazów i konfigurowalnym opcjom oferuje szeroki zakres aplikacji dla deweloperów.

---

## Często zadawane pytania

### 1. Gdzie mogę pobrać Aspose.HTML dla .NET?

 Aspose.HTML dla .NET można pobrać ze strony z wersjami[Tutaj](https://releases.aspose.com/html/net/).

### 2. Jak mogę uzyskać tymczasową licencję na Aspose.HTML dla .NET?

 Aby uzyskać tymczasową licencję, odwiedź stronę licencji tymczasowej[Tutaj](https://purchase.aspose.com/temporary-license/).

### 3. Gdzie mogę znaleźć dodatkowe wsparcie dla Aspose.HTML dla .NET?

 W przypadku jakichkolwiek pytań lub problemów możesz zwrócić się o pomoc do społeczności Aspose na forum wsparcia[Tutaj](https://forum.aspose.com/).

### 4. Czy mogę konwertować dokumenty EPUB do innych formatów, takich jak PDF lub XPS?

Tak, możesz użyć Aspose.HTML dla .NET do konwersji dokumentów EPUB do różnych formatów, w tym PDF i XPS.

### 5. Czy Aspose.HTML dla .NET nadaje się zarówno do projektów małych, jak i dużych?

Oczywiście! Aspose.HTML dla .NET jest zaprojektowany tak, aby był skalowalny, co czyni go świetnym wyborem dla projektów każdej wielkości.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
