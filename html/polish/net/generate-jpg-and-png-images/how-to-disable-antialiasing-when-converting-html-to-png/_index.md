---
category: general
date: 2026-03-25
description: Dowiedz się, jak wyłączyć antyaliasing podczas konwertowania HTML na
  PNG, zapewniając renderowanie piksel‑idealne. Zawiera kroki, jak renderować HTML
  jako obraz, zapisać HTML jako PNG oraz utworzyć PNG z HTML.
draft: false
keywords:
- how to disable antialiasing
- convert html to png
- render html as image
- save html as png
- create png from html
language: pl
og_description: Odkryj krok po kroku metodę wyłączania antyaliasingu przy konwertowaniu
  HTML na PNG, zapewniającą idealnie dopasowany do pikseli obraz za każdym razem.
og_title: Jak wyłączyć antyaliasing przy konwertowaniu HTML na PNG
tags:
- Aspose.HTML
- C#
- Image Rendering
title: Jak wyłączyć antyaliasing przy konwertowaniu HTML na PNG
url: /pl/net/generate-jpg-and-png-images/how-to-disable-antialiasing-when-converting-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyłączyć antyaliasing przy konwertowaniu HTML na PNG

Zastanawiałeś się kiedyś **jak wyłączyć antyaliasing**, aby konwersja HTML‑do‑PNG wyglądała dokładnie tak jak źródłowy kod? Być może tworzysz generator miniatur dla komponentów UI i rozmyte krawędzie psują jakość wizualną. Nie jesteś sam — wielu programistów napotyka ten problem, gdy próbują **konwertować HTML na PNG** w celu uzyskania zrzutów ekranu o pikselowej precyzji.

W tym samouczku przeprowadzimy Cię przez cały proces **renderowania HTML jako obrazu**, dostosujemy potok renderowania, aby wyłączyć antyaliasing, i w końcu **zapiszemy HTML jako PNG** przy użyciu Aspose.HTML dla .NET. Po zakończeniu będziesz mieć gotowy do uruchomienia fragment kodu, który tworzy wyraźny PNG z dowolnego pliku HTML, oraz zrozumiesz, dlaczego wyłączanie antyaliasingu ma znaczenie w niektórych scenariuszach wrażliwych na projekt.

## Czego będziesz potrzebować

- **.NET 6.0** lub nowszy (kod działa również na .NET Framework 4.6+).  
- Pakiet NuGet **Aspose.HTML for .NET** (`Aspose.HTML`).  
- Prosty plik `input.html`, który chcesz rasteryzować.  
- Dowolne IDE, które lubisz — Visual Studio, Rider, a nawet VS Code z rozszerzeniem C#.

Nie są wymagane dodatkowe biblioteki natywne ani zewnętrzne narzędzia; Aspose.HTML zajmuje się wszystkim w tle.

## Krok 1: Zainstaluj Aspose.HTML

Pierwszą rzeczą, której potrzebujesz, jest biblioteka Aspose.HTML. Otwórz terminal (lub konsolę Package Manager) i uruchom:

```bash
dotnet add package Aspose.HTML
```

Lub, jeśli wolisz interfejs UI NuGet, wyszukaj **Aspose.HTML** i kliknij *Install*. Ten pakiet zawiera potężny silnik renderujący, który może generować PNG, JPEG, BMP i inne formaty.

> **Pro tip:** Używaj najnowszej stabilnej wersji (stan na marzec 2026 to 23.12), aby skorzystać z poprawek błędów związanych z renderowaniem obrazu i kontrolą antyaliasingu.

## Krok 2: Załaduj dokument HTML

Gdy pakiet jest już zainstalowany, możesz załadować HTML, który chcesz przekształcić. Klasa `HTMLDocument` abstrahuje DOM i pozwala na manipulację przed renderowaniem, jeśli to konieczne.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;

// Path to your source HTML file
string inputPath = Path.Combine(Environment.CurrentDirectory, "input.html");

// Create a new HTMLDocument instance
HTMLDocument htmlDoc = new HTMLDocument(inputPath);
```

> **Dlaczego to ważne:** Załadowanie dokumentu najpierw daje możliwość wstrzyknięcia CSS lub naprawienia względnych URL‑ów przed etapem rasteryzacji. Izoluje to także renderowanie od systemu plików, co ułatwia testowanie kodu.

## Krok 3: Skonfiguruj ImageSaveOptions i wyłącz antyaliasing

Oto sedno samouczka: wyłączenie antyaliasingu. Aspose.HTML udostępnia `ImageRenderingOptions`, w którym możesz przełączyć `UseAntialiasing`. Ustawienie go na `false` zmusza silnik do renderowania każdego piksela dokładnie tak, jak określają to kształty wektorowe, co daje **pikselowo‑idealny PNG**.

```csharp
// Create ImageSaveOptions for PNG output
ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.Png)
{
    // Attach rendering options
    ImageRenderingOptions = new ImageRenderingOptions
    {
        // Disable antialiasing for a crisp raster image
        UseAntialiasing = false
    }
};
```

### Co tak naprawdę robi antyaliasing

Antialiasing wygładza krawędzie kształtów, mieszając kolory sąsiadujących pikseli. Choć wygląda to świetnie w przypadku fotografii czy skomplikowanej grafiki, może rozmywać ostre elementy UI (np. ikony lub tekst w małych rozmiarach). Wyłączenie go zapewnia, że każda linia pozostaje ostra jak brzytwa — dokładnie tego potrzebujesz, gdy **tworzysz PNG z HTML** do testów UI lub dokumentacji.

## Krok 4: Renderuj i zapisz PNG

Gdy opcje są już ustawione, wywołaj `Save` na obiekcie `HTMLDocument`. Metoda przyjmuje ścieżkę wyjściową oraz wcześniej skonfigurowane `ImageSaveOptions`.

```csharp
// Destination path for the PNG file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.png");

// Render the HTML and write the PNG file
htmlDoc.Save(outputPath, saveOptions);
```

Uruchomienie powyższego kodu wygeneruje `output.png` tuż obok Twojego pliku wykonywalnego. Otwórz go w dowolnym przeglądarce obrazów — powinieneś zobaczyć wyraźną, pozbawioną antyaliasingu wersję `input.html`.

### Oczekiwany rezultat

| Przed (Antialiasing włączony) | Po (Antialiasing wyłączony) |
|--------------------------|--------------------------|
| ![Wynik z antyaliasingiem](antialiased.png "przykład wyłączania antyaliasingu z rozmytymi krawędziami") | ![Wynik pikselowo‑idealny](pixelperfect.png "przykład wyłączania antyaliasingu z ostrymi krawędziami") |

*Lewy obrazek pokazuje domyślne renderowanie z antyaliasingiem, natomiast prawy obrazek demonstruje ostry wynik po wyłączeniu antyaliasingu.*

> **Uwaga:** Powyższe zrzuty ekranu są symboliczne; zamień je na własne pliki przy publikacji.

## Krok 5: Zweryfikuj wynik programowo (opcjonalnie)

Jeśli musisz upewnić się, że PNG spełnia określone kryteria (np. dokładne wymiary lub głębię kolorów), możesz go sprawdzić przy użyciu `System.Drawing` lub `SixLabors.ImageSharp`. Oto szybka weryfikacja z `ImageSharp`:

```csharp
using SixLabors.ImageSharp;
using SixLabors.ImageSharp.PixelFormats;

using (Image<Rgba32> img = Image.Load<Rgba32>(outputPath))
{
    Console.WriteLine($"Width: {img.Width}px, Height: {img.Height}px");
    // Verify that the image has no blended pixels (simple heuristic)
    // You could compare a few pixel values against expected RGBA values.
}
```

Ten dodatkowy krok jest przydatny, gdy automatyzujesz generowanie PNG w pipeline CI i musisz zapewnić spójność.

## Przypadki brzegowe i najczęstsze pytania

### Co zrobić, gdy mój HTML używa zewnętrznych zasobów?

Jeśli HTML odwołuje się do CSS, czcionek lub obrazów za pomocą względnych URL‑ów, upewnij się, że bazowy URL `HTMLDocument` wskazuje na folder zawierający te zasoby:

```csharp
HTMLDocument htmlDoc = new HTMLDocument(inputPath, new Uri("file:///" + Path.GetDirectoryName(inputPath) + "/"));
```

### Czy mogę zmienić DPI lub rozmiar obrazu?

Oczywiście. `ImageRenderingOptions` pozwala również ustawić `Resolution` (punkty na cal) oraz `Width`/`Height`:

```csharp
saveOptions.ImageRenderingOptions.Resolution = 300; // High‑resolution PNG
saveOptions.ImageRenderingOptions.Width = 800;      // Desired pixel width
saveOptions.ImageRenderingOptions.Height = 600;     // Desired pixel height
```

Pamiętaj jednak, że zwiększenie DPI bez skalowania viewportu może spowodować większy plik przy tej samej wielkości wizualnej.

### Czy wyłączenie antyaliasingu wpływa na czytelność tekstu?

W przypadku większości nowoczesnych czcionek wyłączenie antyaliasingu może sprawić, że mały tekst będzie wyglądał ząbkowanie. Jeśli potrzebujesz wyraźnego tekstu **i** gładkich krawędzi, rozważ renderowanie w wyższej rozdzielczości, a następnie zmniejszenie przy użyciu wysokiej jakości algorytmu resamplingu. Ten trik zachowuje czytelność, jednocześnie dając kontrolę nad ostateczną siatką pikseli.

### Czy to podejście jest wieloplatformowe?

Tak. Aspose.HTML jest czystym .NET i działa na Windows, Linux oraz macOS. Jedyną specyficzną dla platformy kwestią jest dostępność czcionek systemowych; może być konieczne osadzenie własnych czcionek w HTML lub ich instalacja na docelowej maszynie.

## Pełny działający przykład

Poniżej znajduje się kompletny, samodzielny program, który możesz skopiować i wkleić do aplikacji konsolowej. Zawiera wszystkie niezbędne dyrektywy `using`, obsługę błędów i komentarze.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering.Image;

namespace HtmlToPngDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // -------------------------------------------------
                // 1️⃣ Define input and output paths
                // -------------------------------------------------
                string inputHtml = Path.Combine(Environment.CurrentDirectory, "input.html");
                string outputPng = Path.Combine(Environment.CurrentDirectory, "output.png");

                // -------------------------------------------------
                // 2️⃣ Load the HTML document
                // -------------------------------------------------
                // BaseUri ensures relative resources resolve correctly
                var htmlDoc = new HTMLDocument(inputHtml, new Uri("file:///" + Path.GetDirectoryName(inputHtml) + "/"));

                // -------------------------------------------------
                // 3️⃣ Configure rendering options – disable antialiasing
                // -------------------------------------------------
                var saveOptions = new ImageSaveOptions(SaveFormat.Png)
                {
                    ImageRenderingOptions = new ImageRenderingOptions
                    {
                        UseAntialiasing = false,   // 👈 The key line for pixel‑perfect output
                        // Optional: set resolution or size here
                    }
                };

                // -------------------------------------------------
                // 4️⃣ Render and save the PNG
                // -------------------------------------------------
                htmlDoc.Save(outputPng, saveOptions);
                Console.WriteLine($"✅ PNG created at: {outputPng}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
            }
        }
    }
}
```

Uruchom program, a zobaczysz **output.png** pojawiający się obok pliku wykonywalnego. Otwórz go — bez rozmytych krawędzi, po prostu czysta rasterowa kopia Twojego HTML.

## Zakończenie

Omówiliśmy **jak wyłączyć antyaliasing** podczas **konwersji HTML na PNG**, przeszliśmy przez każdy krok konfiguracji i dostarczyliśmy pełny, działający przykład, który **renderuje HTML jako obraz**, **zapisuje HTML jako PNG** i pozwala **tworzyć PNG z HTML** z pikselową precyzją.

Jeśli chcesz iść dalej, spróbuj eksperymentować z różnymi formatami obrazu (JPEG, BMP), zbadaj triki skalowania wektor‑do‑raster oraz zintegrować ten fragment kodu z usługą webową generującą miniatury w locie. Te same zasady mają zastosowanie, niezależnie od tego, czy tworzysz generator dokumentacji, narzędzie do testów regresji wizualnej, czy dynamiczny eksport wykresów.

Masz więcej pytań dotyczących niuansów renderowania lub funkcji Aspose.HTML? zostaw komentarz poniżej i szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}