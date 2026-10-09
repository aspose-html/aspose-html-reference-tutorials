---
category: general
date: 2026-10-09
description: Utwórz instancję ImageRenderingOptions, aby włączyć antyaliasing i poprawić
  jakość renderowania grafiki w aplikacjach .NET.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create imagerenderingoptions instance
- ImageRenderingOptions
- antialiasing
- SmoothingMode
- graphics rendering
language: pl
lastmod: 2026-10-09
og_description: Utwórz instancję ImageRenderingOptions, aby włączyć antyaliasing i
  uzyskać płynniejsze renderowanie grafiki w .NET. Postępuj zgodnie z przewodnikiem
  krok po kroku.
og_image_alt: Screenshot showing smooth edges after enabling antialiasing with ImageRenderingOptions
og_title: Utwórz instancję ImageRenderingOptions – zwiększ jakość grafiki w .NET
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  headline: Create imagerenderingoptions instance for high‑quality graphics rendering
  type: TechArticle
- description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  name: Create imagerenderingoptions instance for high‑quality graphics rendering
  steps:
  - name: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
    text: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
  - name: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
    text: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
  - name: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
    text: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
  type: HowTo
tags:
- .NET
- C#
- rendering
title: Utwórz instancję ImageRenderingOptions dla renderowania grafiki wysokiej jakości
url: /pl/net/canvas-and-image-manipulation/create-imagerenderingoptions-instance-for-high-quality-graph/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz instancję imagerenderingoptions dla renderowania grafiki wysokiej jakości

Jeśli potrzebujesz **utworzyć instancję imagerenderingoptions**, aby uzyskać płynniejsze grafiki, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Konfigurując antyaliasing, eliminujesz ząbkowane krawędzie i otrzymujesz wynik o jakości profesjonalnej bez dodatkowych bibliotek.

Dowiesz się, jak zainicjować `ImageRenderingOptions`, włączyć antyaliasing oraz podłączyć opcje do silnika renderującego, takiego jak Aspose.Slides lub System.Drawing. Tutorial zakłada, że znasz podstawową składnię C# i masz gotowe środowisko programistyczne .NET.

## Wymagania wstępne

- .NET 6.0 lub nowszy (API jest dostępne w .NET Standard 2.0+)
- Odwołanie do zestawu, który zawiera `ImageRenderingOptions` (np. `Aspose.Slides.NET`)
- IDE, takie jak Visual Studio 2022 lub VS Code z rozszerzeniem C#
- Podstawowa znajomość pipeline’ów renderowania grafiki

## Krok 1: Utwórz instancję imagerenderingoptions

Pierwszą operacją jest alokacja nowego obiektu `ImageRenderingOptions`. Obiekt ten działa jako kontener dla wszystkich flag związanych z renderowaniem.

```csharp
using Aspose.Slides;          // Replace with the appropriate namespace
using Aspose.Slides.Export;   // Needed for ImageRenderingOptions

// Step 1: Create the ImageRenderingOptions instance
ImageRenderingOptions imgOptions = new ImageRenderingOptions();
```

Utworzenie instancji daje pełną kontrolę nad tym, jak grafika wektorowa jest rasteryzowana. Później możesz włączać lub wyłączać konkretne funkcje, takie jak antyaliasing, tryb renderowania tekstu czy kompresja obrazu.

## Krok 2: Włącz antyaliasing, aby poprawić jakość renderowania grafiki

Antyaliasing wygładza przejścia między kolorami pikseli, zmniejszając efekt schodkowy na liniach ukośnych i krzywych. Starsza właściwość `SmoothingMode` jest przestarzała; `UseAntialiasing` jest nowoczesnym, zalecanym podejściem.

```csharp
// Step 2: Turn on antialiasing for smoother output
imgOptions.UseAntialiasing = true;
```

Ustawienie `UseAntialiasing` na `true` informuje silnik renderujący, aby zastosował filtr wysokiej jakości podczas rasteryzacji. Flaga działa zarówno dla kształtów wektorowych, jak i tekstu, zapewniając spójną wierność wizualną na całym slajdzie.

### Dlaczego nie używać SmoothingMode?

`SmoothingMode` należy do `System.Drawing.Graphics` i wpływa wyłącznie na rysowanie GDI+. Gdy renderujesz slajdy lub PDF‑y przy pomocy Aspose.Slides, jedyną flagą respektowaną przez bibliotekę jest `ImageRenderingOptions.UseAntialiasing`. Użycie nowszej właściwości gwarantuje kompatybilność w przyszłości i eliminuje nieoczekiwane zachowanie na platformach nie‑Windowsowych.

## Krok 3: Zastosuj opcje w operacji renderowania

Po skonfigurowaniu instancji `ImageRenderingOptions` przekaż ją do metody wykonującej rzeczywiste renderowanie. Poniżej znajduje się kompletny, gotowy do uruchomienia przykład, który ładuje prezentację, renderuje pierwszy slajd jako PNG i zapisuje obraz z włączonym antyaliasingiem.

```csharp
using System;
using Aspose.Slides;
using Aspose.Slides.Export;

class Program
{
    static void Main()
    {
        // Load a sample presentation
        using Presentation pres = new Presentation("sample.pptx");

        // Create and configure ImageRenderingOptions
        ImageRenderingOptions imgOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true   // Enable antialiasing
        };

        // Render the first slide to a PNG file
        Slide slide = pres.Slides[0];
        slide.GetThumbnail(2f, 2f, imgOptions)   // 2x scale for higher resolution
            .Save("slide1_antialiased.png", Export.SaveFormat.Png);

        Console.WriteLine("Slide rendered with antialiasing.");
    }
}
```

**Wyjaśnienie kluczowych linii**

- `new Presentation("sample.pptx")` ładuje plik źródłowy.  
- `GetThumbnail(2f, 2f, imgOptions)` tworzy bitmapę slajdu przy podwojonym domyślnym DPI, jednocześnie stosując skonfigurowane opcje renderowania.  
- Wynikowy PNG (`slide1_antialiased.png`) wyświetla gładkie krzywe i tekst dzięki `UseAntialiasing = true`.

### Oczekiwany wynik

Otwórz `slide1_antialiased.png` w dowolnym przeglądarce obrazów. W porównaniu z renderowaniem bez antyaliasingu zauważysz:

- Zaokrąglone rogi kształtów nie mają ząbkowanych kroków.  
- Krawędzie tekstu są ostre, ale jednocześnie złagodzone, eliminując pikselowe artefakty.  
- Ogólna jakość wizualna odpowiada temu, co widzisz w oryginalnym widoku PowerPointa.

## Krok 4: Opcjonalne dopasowania dla zaawansowanego renderowania grafiki

Choć antyaliasing jest najczęściej używaną flagą, `ImageRenderingOptions` oferuje dodatkowe kontrolki:

| Właściwość | Cel | Typowa wartość |
|------------|-----|----------------|
| `UseHighQualityRendering` | Włącza renderowanie sub‑pikselowe dla tekstu | `true` |
| `PixelFormat` | Określa głębię kolorów wyjściowej bitmapy | `PixelFormat.Format32bppArgb` |
| `ImageFormat` | Ustawia docelowy format obrazu (PNG, JPEG, itp.) | `Export.SaveFormat.Png` |

Możesz łączyć te ustawienia:

```csharp
imgOptions.UseHighQualityRendering = true;
imgOptions.PixelFormat = System.Drawing.Imaging.PixelFormat.Format32bppArgb;
```

**Pro tip:** Generując PDF‑y dużej skali lub wysokiej rozdzielczości PNG, pozostaw `UseAntialiasing` włączone, ale monitoruj zużycie pamięci. Antyaliasing dodaje dodatkowy narzut przetwarzania, co może być zauważalne na słabszych maszynach.

## Typowe pułapki i jak ich unikać

1. **Zapomnienie o przekazaniu opcji** – Metody renderujące przyjmujące `ImageRenderingOptions` zignorują antyaliasing, jeśli wywołasz przeciążenie bez parametru opcji. Zawsze używaj trzy‑parametrowej wersji `GetThumbnail` lub równoważnej metody.  
2. **Mieszanie SmoothingMode z ImageRenderingOptions** – Ustawienie `Graphics.SmoothingMode` nie ma wpływu na renderowanie w Aspose.Slides. Polegaj wyłącznie na `UseAntialiasing`.  
3. **Używanie przestarzałej wersji biblioteki** – `ImageRenderingOptions` zostało wprowadzone w Aspose.Slides 20.5. Upewnij się, że Twój pakiet NuGet jest aktualny; w przeciwnym razie klasa może być nieobecna lub nie zawierać właściwości `UseAntialiasing`.

## Podsumowanie

Teraz wiesz, jak **utworzyć instancję imagerenderingoptions**, włączyć antyaliasing i zintegrować opcje z przepływem renderowania. To podejście zapewnia płynniejsze renderowanie grafiki, zastępuje przestarzałe ustawienie `SmoothingMode` i działa konsekwentnie na platformach .NET.

Od tego momentu możesz eksplorować dodatkowe flagi renderowania, eksperymentować z różnymi skalami DPI lub połączyć technikę z eksportem PDF, aby uzyskać zasoby o jakości gotowej do druku. Opanowanie `ImageRenderingOptions` jest kluczowym elementem programowania grafiki .NET o wysokiej wierności.

---


## Co powinieneś nauczyć się dalej?


Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu wraz z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Create PNG from HTML – Full C# Rendering Guide](/html/english/net/rendering-html-documents/create-png-from-html-full-c-rendering-guide/)
- [Create image from HTML in C# – Complete Step‑by‑Step Guide](/html/english/net/rendering-html-documents/create-image-from-html-in-c-complete-step-by-step-guide/)
- [Create canvas text – Full Guide to Rendering Text on Images](/html/english/net/canvas-and-image-manipulation/create-canvas-text-full-guide-to-rendering-text-on-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}