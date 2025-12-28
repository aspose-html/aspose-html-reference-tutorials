---
category: general
date: 2025-12-27
description: Dowiedz się, jak włączyć antyaliasing podczas konwertowania plików DOCX
  na PNG lub JPG. Ten przewodnik krok po kroku obejmuje również konwersję DOCX na
  PNG oraz konwersję DOCX na JPG.
draft: false
keywords:
- how to enable antialiasing
- convert docx to png
- convert docx to jpg
- how to convert docx
- how to render docx
language: pl
og_description: Jak włączyć antyaliasing podczas konwertowania plików DOCX na PNG
  lub JPG. Przeczytaj ten kompletny przewodnik, aby uzyskać płynny, wysokiej jakości
  wynik.
og_title: Jak włączyć antyaliasing przy konwertowaniu DOCX na PNG/JPG
tags:
- C#
- Document Rendering
- Image Processing
title: Jak włączyć antyaliasing przy konwertowaniu DOCX na PNG/JPG
url: /pl/net/generate-jpg-and-png-images/how-to-enable-antialiasing-when-converting-docx-to-png-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak włączyć antyaliasing przy konwertowaniu DOCX na PNG/JPG

Zastanawiałeś się kiedyś **jak włączyć antyaliasing**, aby obrazy po konwersji DOCX wyglądały ostro zamiast ząbkowanie? Nie jesteś sam. Wielu programistów napotyka problem, gdy muszą przekształcić dokument Worda w PNG lub JPG i kończą z rozmytymi krawędziami linii i tekstu. Dobra wiadomość? Kilka linijek C# pozwoli zamienić ten szorstki wynik w grafiki o perfekcyjnej jakości pikselowej — bez potrzeby używania zewnętrznych edytorów graficznych.

W tym tutorialu przejdziemy przez cały proces **convert docx to png** i **convert docx to jpg** przy użyciu nowoczesnej biblioteki renderującej. Nauczysz się nie tylko *jak konwertować docx*, ale także *jak renderować docx* z włączonym antyaliasingiem i hintingiem, tak aby każda krzywa i znak wyglądały płynnie. Nie wymaga to wcześniejszego doświadczenia w programowaniu grafiki; wystarczy podstawowe środowisko C# i plik DOCX, który chcesz przekształcić w obraz.

---

## Co będzie potrzebne

- **.NET 6+** (lub .NET Framework 4.6+, jeśli wolisz klasyczny runtime)  
- Plik **DOCX**, który chcesz wyrenderować (umieść go w folderze o nazwie `input` dla demonstracji)  
- Pakiet NuGet **Aspose.Words for .NET** (lub dowolna biblioteka udostępniająca `Document`, `ImageRenderingOptions` i `ImageDevice`). Zainstaluj go poleceniem:

```bash
dotnet add package Aspose.Words
```

To wszystko — nie są potrzebne dodatkowe narzędzia do przetwarzania obrazów.

---

## Krok 1: Załaduj dokument DOCX (jak konwertować docx)

Najpierw potrzebujemy obiektu `Document`, który reprezentuje plik źródłowy. To cyfrowa wersja Twojego pliku Word, którą biblioteka może odczytać i manipulować.

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;
using Aspose.Words.Saving;

// Load the DOCX you want to render
Document sourceDoc = new Document("input/input.docx");
```

> **Dlaczego to ważne:** Załadowanie dokumentu jest podstawą *jak renderować docx*. Jeśli plik nie zostanie odczytany, żaden z kolejnych kroków nie zadziała, więc zaczynamy właśnie tutaj.

---

## Krok 2: Skonfiguruj opcje renderowania obrazu (włącz antyaliasing)

Teraz następuje magiczna część — włączenie antyaliasingu i hintingu. Antyaliasing wygładza ząbkowane krawędzie, które normalnie widzisz na liniach ukośnych, a hinting poprawia czytelność małego tekstu.

```csharp
// Set up rendering options with antialiasing and hinting
ImageRenderingOptions renderingOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,                // <‑‑ smooth graphics
    Text = { UseHinting = true }           // <‑‑ sharper text
};
```

> **Pro tip:** Jeśli kiedykolwiek potrzebujesz przyspieszyć przetwarzanie bardzo dużych dokumentów, możesz wyłączyć `UseAntialiasing`, ale jakość wizualna zauważalnie spadnie.

---

## Krok 3: Wybierz format wyjściowy – PNG lub JPG (convert docx to png / convert docx to jpg)

Klasa `ImageDevice` decyduje, gdzie trafiają wyrenderowane strony. Zamieniając `ImageSaveOptions`, możesz uzyskać albo PNG (bezstratny), albo JPG (skompresowany). Poniżej tworzymy dwa oddzielne urządzenia, aby w jednym uruchomieniu wygenerować oba formaty.

```csharp
// PNG device – lossless, ideal for screenshots or further editing
ImageDevice pngDevice = new ImageDevice(renderingOptions)
{
    SaveOptions = new ImageSaveOptions(SaveFormat.Png)
    {
        OutputFileName = "output/page_{0}.png"   // {0} will be replaced by page number
    }
};

// JPG device – smaller file size, good for web thumbnails
ImageDevice jpgDevice = new ImageDevice(renderingOptions)
{
    SaveOptions = new ImageSaveOptions(SaveFormat.Jpeg)
    {
        OutputFileName = "output/page_{0}.jpg",
        JpegQuality = 90          // 0‑100, higher = better quality
    }
};
```

> **Dlaczego oba?** PNG zachowuje każdy piksel, co jest idealne, gdy potrzebna jest dokładna wierność (np. do druku). JPG natomiast kompresuje obraz, co przyspiesza jego ładowanie na stronie internetowej.

---

## Krok 4: Renderuj strony dokumentu do obrazów (jak renderować docx)

Mając gotowe urządzenia, instruujemy `Document`, aby wyrenderował każdą stronę. Biblioteka automatycznie przeiteruje wszystkie strony i zapisze je według zdefiniowanego wzorca nazewnictwa.

```csharp
// Render to PNG
sourceDoc.RenderTo(pngDevice);

// Render to JPG
sourceDoc.RenderTo(jpgDevice);
```

Po uruchomieniu kodu znajdziesz serię plików takich jak `page_0.png`, `page_1.png`, … oraz `page_0.jpg`, `page_1.jpg` w folderze `output`. Każdy obraz będzie miał zastosowany antyaliasing, więc linie będą gładkie, a tekst krystalicznie czysty.

---

## Krok 5: Zweryfikuj wynik (oczekiwany output)

Otwórz dowolny z wygenerowanych obrazów. Powinieneś zobaczyć:

- **Gładkie krzywe** w kształtach i wykresach (bez artefaktów schodkowych).  
- **Wyraźny, czytelny tekst** nawet przy małych rozmiarach czcionki, dzięki hintingowi.  
- **Spójne kolory** między PNG a JPG (choć JPG może wykazywać lekkie artefakty kompresji przy niższej jakości).

Jeśli zauważysz rozmycie, sprawdź, czy `UseAntialiasing` jest ustawione na `true` oraz czy źródłowy DOCX nie zawiera niskiej rozdzielczości obrazów rastrowych.

---

## Często zadawane pytania i przypadki brzegowe

### Co zrobić, jeśli potrzebuję tylko jednej strony?

Możesz wyrenderować konkretną stronę, używając przeciążenia `PageInfo`:

```csharp
// Render only the first page to PNG
sourceDoc.RenderTo(pngDevice, new PageInfo(0));
```

### Czy mogę zmienić DPI (dots per inch) dla wyższej rozdzielczości wyjścia?

Oczywiście. Dostosuj właściwość `Resolution` w `ImageRenderingOptions`:

```csharp
renderingOptions.Resolution = 300; // 300 DPI for print‑quality images
```

Wyższe DPI oznacza większe pliki, ale efekt antyaliasingu staje się jeszcze bardziej widoczny.

### Jak obsłużyć duże pliki DOCX, aby nie wyczerpać pamięci?

Renderuj strony pojedynczo i zwalniaj urządzenie po każdej iteracji:

```csharp
for (int i = 0; i < sourceDoc.PageCount; i++)
{
    using var singlePageDevice = new ImageDevice(renderingOptions);
    singlePageDevice.SaveOptions = new ImageSaveOptions(SaveFormat.Png)
    {
        OutputFileName = $"output/page_{i}.png"
    };
    sourceDoc.RenderTo(singlePageDevice, new PageInfo(i));
}
```

### Czy można konwertować do innych formatów, takich jak BMP lub TIFF?

Tak — wystarczy zamienić `SaveFormat.Png` lub `SaveFormat.Jpeg` na `SaveFormat.Bmp` lub `SaveFormat.Tiff`. Te same ustawienia antyaliasingu zostaną zachowane.

---

## Pełny działający przykład (gotowy do kopiowania)

Poniżej znajduje się kompletny program, który możesz wkleić do nowego projektu konsolowego. Zawiera wszystkie dyrektywy `using`, obsługę błędów i komentarze dla przejrzystości.

```csharp
// File: Program.cs
using System;
using System.IO;
using Aspose.Words;
using Aspose.Words.Rendering;
using Aspose.Words.Saving;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the DOCX document (how to convert docx)
        // -------------------------------------------------
        string inputPath = Path.Combine("input", "input.docx");
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❗ Input file not found: {inputPath}");
            return;
        }

        Document sourceDoc = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure rendering options (enable antialiasing)
        // -------------------------------------------------
        ImageRenderingOptions renderingOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            Text = { UseHinting = true },
            Resolution = 150 // optional – 150 DPI is a good balance
        };

        // -------------------------------------------------
        // 3️⃣ Set up PNG and JPG devices (convert docx to png / convert docx to jpg)
        // -------------------------------------------------
        string outputFolder = "output";
        Directory.CreateDirectory(outputFolder);

        // PNG (lossless)
        ImageDevice pngDevice = new ImageDevice(renderingOptions)
        {
            SaveOptions = new ImageSaveOptions(SaveFormat.Png)
            {
                OutputFileName = Path.Combine(outputFolder, "page_{0}.png")
            }
        };

        // JPG (compressed)
        ImageDevice jpgDevice = new ImageDevice(renderingOptions)
        {
            SaveOptions = new ImageSaveOptions(SaveFormat.Jpeg)
            {
                OutputFileName = Path.Combine(outputFolder, "page_{0}.jpg"),
                JpegQuality = 90
            }
        };

        // -------------------------------------------------
        // 4️⃣ Render all pages (how to render docx)
        // -------------------------------------------------
        try
        {
            sourceDoc.RenderTo(pngDevice);
            sourceDoc.RenderTo(jpgDevice);
            Console.WriteLine($"✅ Rendering complete! Check the '{outputFolder}' folder.");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ An error occurred: {ex.Message}");
        }
    }
}
```

> **Rezultat:** Po skompilowaniu (`dotnet run`) zobaczysz serię plików PNG i JPG w katalogu `output`, każdy z zastosowanym antyaliasingiem.

---

## Podsumowanie

Omówiliśmy **jak włączyć antyaliasing** przy **konwertowaniu DOCX do PNG lub JPG**, przeszliśmy przez dokładne kroki **convert docx to png**, **convert docx to jpg**, a także dotknęliśmy tematu **jak renderować docx** dla własnych potrzeb.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}