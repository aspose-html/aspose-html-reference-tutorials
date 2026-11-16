---
category: general
date: 2026-04-06
description: Dowiedz się, jak włączyć antyaliasing, ustawić szerokość i wysokość obrazu
  oraz zapisać dokument jako PNG w C# – szybki przewodnik po eksporcie dokumentu do
  obrazu.
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: pl
og_description: Jak włączyć antyaliasing podczas eksportowania dokumentu do obrazu.
  Ten przewodnik pokazuje, jak ustawić szerokość obrazu, wysokość obrazu oraz zapisać
  dokument jako PNG.
og_title: Jak włączyć antyaliasing – Eksportuj dokument do obrazu
tags:
- C#
- ImageRendering
- Antialiasing
title: Jak włączyć antyaliasing – eksport dokumentu do obrazu w C#
url: /pl/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak włączyć antyaliasing – eksport dokumentu do obrazu w C#

Zastanawiałeś się **jak włączyć antyaliasing** podczas zamiany dokumentu na obraz? Być może próbowałeś szybkiego wywołania `Save` i wynik wyglądał poszarpanie, szczególnie na liniach ukośnych. Dobra wiadomość: nie potrzebujesz czarodzieja grafiki — wystarczy kilka linii C# i odpowiednie opcje.

W tym samouczku przejdziemy przez ustawianie szerokości obrazu, wysokości obrazu oraz w końcu **zapisanie dokumentu jako PNG**, abyś mógł **wyeksportować dokument do obrazu** z gładkimi krawędziami. Po zakończeniu będziesz mieć gotowy fragment kodu, który tworzy wyraźny PNG 800 × 600 z włączonym antyaliasingiem.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa także na .NET Framework 4.7+)  
- Odwołanie do biblioteki renderującej obsługującej `ImageRenderingOptions` (np. Aspose.Words, Syncfusion lub dowolnego API udostępniającego podobne właściwości)  
- Podstawowa znajomość składni C#  

Bez skomplikowanej konfiguracji — po prostu dodaj pakiet NuGet i możesz zaczynać.

## Krok 1: Zainstaluj bibliotekę renderującą

Najpierw pobierz pakiet do swojego projektu. Jeśli używasz Aspose.Words, uruchom:

```bash
dotnet add package Aspose.Words
```

> **Pro tip:** Utrzymuj wersję biblioteki aktualną; najnowsze wydanie (stan na kwiecień 2026) wprowadza ulepszenia wydajności dla antyaliasingu.

## Krok 2: Utwórz obiekt dokumentu

Załaduj lub utwórz dokument, który chcesz renderować. Oto minimalny przykład tworzący jednosekcyjny dokument z prostym akapitem:

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

Klasa `Document` jest punktem wejścia; wszystko, co renderujesz, pochodzi z niej. W prawdziwych projektach prawdopodobnie załadujesz istniejący plik .docx:

```csharp
// Document doc = new Document("input.docx");
```

## Krok 3: Zdefiniuj opcje renderowania (szerokość, wysokość, antyaliasing)

Teraz odpowiemy na kluczowe pytanie: **jak włączyć antyaliasing**. Obiekt `ImageRenderingOptions` pozwala przełączać wygładzanie i kontrolować wymiary.

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

Zwróć uwagę na komentarze: wyraźnie wspominają **set image width**, **set image height** oraz **UseAntialiasing** — trzy najważniejsze „gałki”, które decydują o jakości PNG.

### Dlaczego antyaliasing ma znaczenie

Bez antyaliasingu linie ukośne i krzywe wyglądają jak schodki, ponieważ renderer traktuje każdy piksel jako włączony lub wyłączony. Włączenie go miesza piksele brzegowe, co daje wizualne zmiękczenie podobne do tego, co widzisz w edytorze zdjęć. Koszt to niewielki wzrost czasu przetwarzania, ale w większości eksportów UI jest pomijalny.

## Krok 4: Zapisz dokument jako PNG (Export Document to Image)

Gdy opcje są gotowe, w końcu **zapisujemy dokument jako PNG**. Metoda `Save` przyjmuje ścieżkę pliku oraz skonfigurowane opcje.

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

Gotowe — Twój dokument jest teraz PNG 800 × 600 z zastosowanym antyaliasingiem. Jeśli otworzysz `output.png`, zobaczysz czysty tekst, gładkie linie i brak poszarpanych artefaktów.

### Weryfikacja wyniku

Możesz szybko sprawdzić plik w dowolnym przeglądarce obrazów. Zwróć uwagę na:

- Poprawne wymiary (800 × 600)  
- Brak widocznych „schodków” na tekście lub kształtach  
- Przezroczyste tło, jeśli dokument nie zawierał koloru tła (większość bibliotek domyślnie ustawia białe)

Jeśli obraz wygląda poszarpanie, upewnij się, że `UseAntialiasing = true` nie jest nadpisane w innym miejscu.

## Krok 5: Przypadki brzegowe i warianty

### Zmiana formatu wyjściowego

Chcesz JPEG zamiast PNG? Po prostu zmień rozszerzenie pliku i opcjonalnie dostosuj kompresję:

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### Eksport wielu stron

Gdy dokument źródłowy ma kilka stron, renderer domyślnie tworzy osobne pliki obrazu dla każdej strony. Możesz przeiterować po stronach:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### Zapis do strumienia (np. odpowiedź HTTP)

Jeśli tworzysz API webowe, możesz zwrócić PNG bezpośrednio:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do skopiowania program, który zawiera wszystkie omówione kroki:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

Uruchomienie tego programu tworzy `output.png` w katalogu wykonywalnym. Otwórz go, a zobaczysz gładki PNG 800 × 600 — dokładnie to, co chcieliśmy osiągnąć.

## Częste pytania i rozwiązywanie problemów

- **Co zrobić, gdy obraz jest rozmyty?**  
  Rozmycie może wystąpić przy skalowaniu małej strony w górę. Trzymaj rozmiar strony zbliżony do docelowych wymiarów lub zwiększ DPI za pomocą `imageOptions.Resolution` (np. `Resolution = 300`).

- **Czy to działa na .NET Framework?**  
  Tak. Ten sam interfejs API istnieje w klasycznym frameworku; wystarczy odwołać odpowiedni plik DLL.

- **Czy mogę kontrolować kolor tła?**  
  Oczywiście. Ustaw `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` przed zapisem.

- **Czy antyaliasing jest przyspieszany sprzętowo?**  
  Większość bibliotek wykonuje antyaliasing programowo. Jeśli potrzebujesz przyspieszenia GPU, poszukaj silnika renderującego, który wyraźnie to obsługuje.

## Podsumowanie

Omówiliśmy **jak włączyć antyaliasing** przy **eksportowaniu dokumentu do obrazu**, przeszliśmy przez **set image width** i **set image height**, oraz pokazaliśmy dokładne kroki do **save document as PNG**. Powyższy fragment kodu jest gotowy do produkcji, a Ty możesz go teraz dostosować do JPEG, wielostronicowych PDF‑ów lub strumieniowego przesyłania obrazu do klienta.

Następnie możesz eksperymentować z dodawaniem znaków wodnych, regulacją DPI dla wydruków wysokiej jakości lub integracją tej logiki w endpointzie ASP.NET Core. Zasady pozostają te same — zamień tylko ścieżkę pliku na strumień odpowiedzi.

Miłego kodowania i ciesz się ostrymi, antyaliasowanymi obrazami! 

![Rendered PNG with antialiasing enabled](output.png "Rendered PNG with antialiasing enabled")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}