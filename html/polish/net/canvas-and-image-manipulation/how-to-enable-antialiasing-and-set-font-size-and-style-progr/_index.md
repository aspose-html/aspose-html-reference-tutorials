---
category: general
date: 2026-11-20
description: Jak włączyć antyaliasing w grafice C# oraz ustawić rozmiar i styl czcionki
  programowo, podając kompletny, uruchamialny przykład z użyciem ImageRenderingOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable antialiasing
- set font size
- set font style programmatically
- C# graphics rendering
- ImageRenderingOptions example
language: pl
lastmod: 2026-11-20
og_description: Jak włączyć antyaliasing w grafice C#, ustawić rozmiar czcionki i
  styl czcionki programowo przy użyciu ImageRenderingOptions – kompletny kod i wyjaśnienie.
og_image_alt: Screenshot of antialiased text with custom font size and style generated
  by C# code showing how to enable antialiasing
og_title: Jak włączyć antyaliasing i ustawić rozmiar oraz styl czcionki programowo
  w C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: How to enable antialiasing in C# graphics and set font size, set font
    style programmatically with a complete, runnable example using ImageRenderingOptions.
  headline: How to enable antialiasing and set font size and style programmatically
    in C#
  type: TechArticle
tags:
- C#
- graphics
- antialiasing
- fonts
title: Jak włączyć antyaliasing i ustawić rozmiar oraz styl czcionki programowo w
  C#
url: /pl/net/canvas-and-image-manipulation/how-to-enable-antialiasing-and-set-font-size-and-style-progr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak włączyć antyaliasing i ustawić rozmiar oraz styl czcionki programowo w C#

Włączanie antyaliasingu w grafice C# jest częstym wymogiem, gdy potrzebne są gładkie krawędzie kształtów lub tekstu. Ten tutorial pokazuje, jak włączyć antyaliasing, ustawić rozmiar czcionki oraz styl czcionki programowo przy użyciu klasy **ImageRenderingOptions**. Po zakończeniu przewodnika będziesz mieć samodzielną aplikację konsolową, która renderuje wyraźny, stylizowany tekst do pliku obrazu.

Nauczysz się konfigurować potok renderowania, wybierać odpowiednią rodzinę czcionek, dostosowywać rozmiar czcionki oraz stosować style pogrubienia lub kursywy bez opuszczania kodu. Jedynym wymogiem wstępnym jest aktualny .NET SDK oraz pakiet NuGet Aspose.Imaging, który przykład instaluję automatycznie.

## Wymagania wstępne

- .NET 6.0 SDK lub nowszy (pobierz z https://dotnet.microsoft.com/)
- Visual Studio 2022 lub dowolny edytor obsługujący projekty .NET
- **Aspose.Imaging** pakiet NuGet (biblioteka udostępniająca `ImageRenderingOptions`)

Pakiet możesz dodać przy pomocy następującego polecenia:

```bash
dotnet add package Aspose.Imaging
```

## Jak włączyć antyaliasing przy użyciu ImageRenderingOptions

`ImageRenderingOptions` jest centralnym obiektem kontrolującym sposób, w jaki Aspose.Imaging rysuje grafikę. Ustawienie właściwości `UseAntialiasing` informuje rasterizer, aby wygładzał krawędzie, co eliminuje ząbkowany efekt „schodków”, pojawiający się przy wyłączonym antyaliasingu.

```csharp
// Step 1: Create a new ImageRenderingOptions instance
ImageRenderingOptions renderingOptions = new ImageRenderingOptions();

// Step 2: Enable antialiasing for smoother graphics
renderingOptions.UseAntialiasing = true;
```

Włączenie antyaliasingu jest niezbędne dla wysokiej jakości elementów UI, renderowania wykresów i każdej sytuacji, w której liczy się wierność wizualna.

## Ustawianie rozmiaru czcionki programowo

Rozmiar czcionki określa, jak duże będą glify w ostatecznym bitmapie. Możesz go zmienić, tworząc obiekt `Font` z żądanym rozmiarem w punktach. Poniższy przykład ustawia rozmiar na **24 pt**, co jest typowym rozmiarem dla czytelnych nagłówków.

```csharp
// Step 3: Choose a font family and size
Font font = new Font("Arial", 24); // 24‑point Arial
```

Możesz zamienić `24` na dowolną liczbę całkowitą lub zmiennoprzecinkową, aby dopasować układ. Klasa `Font` przyjmuje także parametr `GraphicsUnit`, jeśli potrzebujesz rozmiaru w pikselach.

## Ustawianie stylu czcionki programowo

Stosowanie pogrubienia, kursywy lub podkreślenia polega na przekazaniu flagi `WebFontStyle` podczas tworzenia obiektu `Font`. Enum `WebFontStyle` łączy wiele stylów przy użyciu operacji bitowego OR.

```csharp
// Step 4: Apply bold and italic styles
font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);
```

Jeśli potrzebujesz tylko jednego stylu, użyj `WebFontStyle.Bold`, `WebFontStyle.Italic` lub `WebFontStyle.Underline`. Takie podejście pozwala **ustawiać styl czcionki programowo** bez twardego kodowania oddzielnych plików czcionek.

## Pełny, działający przykład

Poniżej znajduje się kompletny program konsolowy, który łączy wszystkie elementy:

```csharp
using System;
using Aspose.Imaging;
using Aspose.Imaging.Brushes;
using Aspose.Imaging.ImageOptions;
using Aspose.Imaging.Sources;
using Aspose.Imaging.FileFormats.Png;
using Aspose.Imaging.Graphics;
using Aspose.Imaging.Fonts;
using Aspose.Imaging.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Create rendering options and enable antialiasing
        ImageRenderingOptions renderingOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            // Enable hinting for sharper text on low‑resolution images
            TextOptions = new TextOptions { UseHinting = true }
        };

        // 2️⃣ Define the font (size + style)
        Font font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);

        // 3️⃣ Prepare a bitmap with a white background
        int width = 800;
        int height = 200;
        using (var bitmap = new RasterImage(width, height, PixelFormat.Format24bppRgb))
        {
            bitmap.SaveOptions = new PngOptions { ColorType = PngColorType.Truecolor };
            bitmap.Fill(new SolidBrush(Color.White));

            // 4️⃣ Create a graphics object that respects our rendering options
            using (Graphics graphics = new Graphics(bitmap, renderingOptions))
            {
                // Position the text in the center of the image
                PointF location = new PointF(50, 80);
                graphics.DrawString("Antialiased Bold Italic Text", font, new SolidBrush(Color.Black), location);
            }

            // 5️⃣ Save the result
            string outputPath = "antialiased_text.png";
            bitmap.Save(outputPath);
            Console.WriteLine($"Image saved to {outputPath}");
        }
    }
}
```

### Wyjaśnienie poszczególnych sekcji

| Sekcja | Dlaczego jest ważna |
|---------|----------------------|
| **Rendering options** | Włączenie `UseAntialiasing` zapewnia gładkie krawędzie zarówno dla wektorowych kształtów, jak i tekstu. |
| **TextOptions.UseHinting** | Hinting poprawia czytelność przy niskiej rozdzielczości, dostosowując kontury glifów. |
| **Font construction** | Konstruktor `Font` łączy **ustawianie rozmiaru czcionki** i **ustawianie stylu czcionki programowo** w jednym wywołaniu. |
| **Graphics object** | Przekazanie `renderingOptions` do `Graphics` zapewnia, że każda operacja rysowania respektuje antyaliasing i hinting. |
| **DrawString** | Ta metoda renderuje tekst z skonfigurowaną czcionką, generując ostateczny antyaliasowany wynik. |
| **Saving** | Format PNG zachowuje dokładne dane pikseli bez dodatkowych artefaktów kompresji. |

#### Oczekiwany wynik

Uruchomienie programu tworzy plik **antialiased_text.png**, który wygląda tak:

![Antialiased text example](https://example.com/antialiased_text.png "Antialiased text with custom font size and style – how to enable antialiasing")

Obraz przedstawia wyraźny, pogrubiony‑kursywa Arial renderowany w 24 pt z gładkimi krawędziami, potwierdzając, że **jak włączyć antyaliasing** działa zgodnie z oczekiwaniami.

## Typowe warianty i przypadki brzegowe

- **Różne rodziny czcionek** – Zamień `"Arial"` na dowolną zainstalowaną nazwę czcionki (np. `"Times New Roman"`). Jeśli czcionka nie jest dostępna, Aspose.Imaging zgłosi `FontNotFoundException`.
- **Zmiana rozmiaru czcionki** – Dostosuj drugi argument konstruktora `Font` do dowolnej wartości zmiennoprzecinkowej. Większe wartości zwiększają czytelność, ale mogą wymagać większej bitmapy.
- **Wiele stylów** – Połącz `WebFontStyle.Underline` z `Bold` i `Italic` przy użyciu operatora `|`: `WebFontStyle.Bold | WebFontStyle.Underline`.
- **Renderowanie w wysokiej rozdzielczości (High‑DPI)** – Dla wyjścia w stylu retina zwiększ wymiary bitmapy (np. 1600 × 400), zachowując ten sam rozmiar czcionki; antyaliasing nadal zapewni gładkie wyniki.
- **Wyłączanie antyaliasingu** – Ustaw `renderingOptions.UseAntialiasing = false;`, aby porównać różnicę wizualną. Tekst będzie wyglądał na ząbkowany, co jest przydatne przy debugowaniu lub testach wydajności.

## Porady profesjonalne

- **Cache'uj obiekt `Font`**, jeśli rysujesz wiele napisów w pętli; tworzenie nowego `Font` w każdej iteracji generuje dodatkowy narzut.
- **Używaj `TextOptions.UseHinting` razem z antyaliasingiem** dla najlepszego kompromisu między ostrością a płynnością na niskiej rozdzielczości obrazów.
- **Waliduj plik wyjściowy**, otwierając go w przeglądarce obrazu pokazującej szczegóły na poziomie pikseli (np. Photoshop lub GIMP). Pomoże to potwierdzić, że antyaliasing rzeczywiście został zastosowany.

## Podsumowanie

Teraz wiesz **jak włączyć antyaliasing** w grafice C#, jak **ustawić rozmiar czcionki** oraz jak **ustawić styl czcionki programowo** przy użyciu `ImageRenderingOptions`. Pełny przykład demonstruje praktyczny przepływ pracy, który możesz skopiować do własnych projektów, niezależnie od tego, czy generujesz wykresy, tworzysz miniatury UI, czy produkujesz dynamiczną grafikę dla usług webowych.

Następnie możesz zbadać **ustawianie koloru czcionki programowo**, dodać **gradientowe wypełnienia** lub renderować **kształty wektorowe** z tymi samymi ustawieniami antyaliasingu. Wszystkie te tematy opierają się na fundamentach przedstawionych tutaj, więc jesteś doskonale przygotowany do tworzenia wysokiej jakości grafiki wyłącznie z kodu. Szczęśliwego renderowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia krok po kroku, pomagające opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Enable Antialiasing When Rendering HTML to PNG in C#](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-when-rendering-html-to-png-in-c/)
- [How to enable antialiasing for HTML image rendering in C#](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-for-html-image-rendering-in-c/)
- [How to Enable Antialiasing in Aspose HTML to PDF Conversion (C#)](/html/english/net/html-extensions-and-conversions/how-to-enable-antialiasing-in-aspose-html-to-pdf-conversion/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}