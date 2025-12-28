---
category: general
date: 2025-12-27
description: Szybko utwórz strumień pamięci w C# dzięki przewodnikowi krok po kroku.
  Dowiedz się, jak tworzyć strumień, zarządzać zasobami i implementować własne tworzenie
  strumieni w .NET.
draft: false
keywords:
- create memory stream c#
- how to create stream
- how to handle resources
- custom stream creation
language: pl
og_description: Utwórz pamięciowy strumień w C# w kilka sekund. Ten samouczek pokazuje,
  jak stworzyć strumień, zarządzać zasobami i budować własne tworzenie strumieni przy
  użyciu nowoczesnych interfejsów .NET.
og_title: Tworzenie strumienia pamięci w C# – Kompletny przewodnik po własnych strumieniach
tags:
- stream
- csharp
- .net
- resource-handling
title: Tworzenie strumienia pamięci w C# – Przewodnik tworzenia własnych strumieni
url: /pl/net/advanced-features/create-memory-stream-c-custom-stream-creation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utworzenie strumienia pamięci c# – Przewodnik tworzenia własnych strumieni

Czy kiedykolwiek potrzebowałeś **create memory stream c#**, ale nie byłeś pewien, którego API wybrać? Nie jesteś jedyny. W wielu starszych projektach znajdziesz `IOutputStorage`, podczas gdy nowsze bazy kodu preferują `ResourceHandler`. W każdym razie cel jest ten sam: dostarczyć `Stream`, który może wykorzystać Twój framework.

W tym samouczku nauczysz się **how to create stream** obiektów, **how to handle resources** bezpiecznie, oraz opanujesz **custom stream creation** zarówno dla wersji przed‑24.2, jak i 24.2+ biblioteki. Po zakończeniu będziesz mieć działający przykład, który możesz wstawić do dowolnego rozwiązania .NET — bez tajemniczych odwołań, po prostu czysty C#.

## Co wyniesiesz z tego tutorialu

- Jasne porównanie starszego wzorca `IOutputStorage` vs. nowoczesnego podejścia `ResourceHandler`.
- Kompletny kod gotowy do kopiowania i wklejania, kompilujący się z .NET 6+ (lub starszym, jeśli potrzebujesz).
- Wskazówki dotyczące przypadków brzegowych, takich jak zwalnianie strumieni, obsługa dużych ładunków i testowanie własnego strumienia.

> **Pro tip:** Jeśli celujesz w .NET 8, nowszy `ResourceHandler` zapewnia wbudowane wsparcie async, co może zaoszczędzić milisekundy w scenariuszach o wysokiej przepustowości.

---

## Utworzenie strumienia pamięci c# – Podejście legacy (przed‑24.2)

Gdy utkniesz na starszej wersji biblioteki, kontrakt, który musisz spełnić, to `IOutputStorage`. Interfejs wymaga jedynie metody zwracającej `Stream` dla podanej nazwy zasobu.

```csharp
using System;
using System.IO;

// Step 1: Implement the old IOutputStorage contract.
public class MyStorage : IOutputStorage
{
    /// <summary>
    /// Returns a stream for the requested resource name.
    /// In a real app you might open a file, a network socket,
    /// or generate data on the fly.
    /// </summary>
    /// <param name="name">Logical name of the resource.</param>
    /// <returns>A writable Stream instance.</returns>
    public Stream CreateStream(string name)
    {
        // Custom stream creation logic.
        // Here we simply return an in‑memory stream.
        // You could also wrap a FileStream if you prefer.
        return new MemoryStream();
    }
}
```

### Dlaczego to działa

- **Interface contract** – Framework wywoła `CreateStream`, gdy będzie potrzebował zapisać wyjście.  
- **Flexibility** – Ponieważ zwracasz `Stream`, możesz później zamienić `MemoryStream` na `FileStream` lub nawet własny buforowany strumień, nie modyfikując reszty kodu.  
- **Resource safety** – Wywołujący jest odpowiedzialny za zwolnienie zwróconego strumienia, dlatego nie wywołujemy `Dispose` wewnątrz metody.  

### Typowe pułapki

| Problem | Co się dzieje | Rozwiązanie |
|---------|---------------|-------------|
| Zwracanie zamkniętego strumienia | Konsumenci otrzymają `ObjectDisposedException` przy zapisie. | Upewnij się, że strumień jest **otwarty** przy przekazywaniu. |
| Zapomnienie o ustawieniu `Position = 0` po zapisie | Dane wydają się puste przy późniejszym odczycie. | Wywołaj `stream.Seek(0, SeekOrigin.Begin)` przed zwróceniem, jeśli wstępnie wypełniasz strumień. |
| Używanie dużego `MemoryStream` dla dużych plików | Awaria z powodu braku pamięci. | Przejdź na tymczasowy `FileStream` lub własny buforowany strumień. |

---

## Utworzenie strumienia pamięci c# – Nowoczesne podejście (24.2+)

Od wersji 24.2 biblioteka wprowadziła `ResourceHandler`. Zamiast interfejsu, teraz dziedziczysz po klasie bazowej i nadpisujesz jedną metodę. Daje to czystszy, przyjazny async punkt wejścia.

```csharp
using System;
using System.IO;

// Step 2: Inherit from the new ResourceHandler base class.
public class MyHandler : ResourceHandler
{
    /// <summary>
    /// Called by the framework to obtain a stream for a resource.
    /// </summary>
    /// <param name="name">The logical name of the resource.</param>
    /// <returns>A writable Stream instance.</returns>
    public override Stream HandleResource(string name)
    {
        // Your custom stream creation logic goes here.
        // For demonstration we use a MemoryStream.
        return new MemoryStream();
    }

    // Optional async version (available in 24.2+)
    public override async Task<Stream> HandleResourceAsync(string name, CancellationToken ct = default)
    {
        // Simulate async work, e.g., fetching data from a service.
        await Task.Delay(10, ct);
        return new MemoryStream();
    }
}
```

### Dlaczego warto wybrać `ResourceHandler`

- **Async support** – Metoda `HandleResourceAsync` pozwala wykonywać I/O bez blokowania wątków.  
- **Built‑in error handling** – Klasa bazowa przechwytuje wyjątki i konwertuje je na kody błędów specyficzne dla frameworka.  
- **Future‑proof** – Nowsze wydania dodają haki (np. logowanie, telemetry), które działają tylko z wzorcem handlera.  

### Obsługa przypadków brzegowych

1. **Disposal** – Framework zwalnia strumień po zakończeniu, ale jeśli opakowujesz inny obiekt disposable (np. `FileStream`), powinieneś zaimplementować blok `using` wewnątrz metody i zwrócić wrapper, który przekazuje `Dispose`.  
2. **Large payloads** – Jeśli spodziewasz się ładunków > 100 MB, zamień `MemoryStream` na `FileStream` wskazujący na plik tymczasowy. Przykład:  

   ```csharp
   return new FileStream(Path.GetTempFileName(),
                         FileMode.Create,
                         FileAccess.ReadWrite,
                         FileShare.None,
                         bufferSize: 81920,
                         useAsync: true);
   ```

3. **Testing** – Przetestuj jednostkowo swój handler, wstrzykując mock `IServiceProvider`, jeśli klasa bazowa pobiera usługi z DI. Zweryfikuj, że `HandleResource` zwraca strumień, do którego można zapisywać i odczytywać.

---

## Jak utworzyć strumień – Szybka karta pomocy

| Scenariusz | Zalecane API | Przykładowy kod |
|------------|--------------|-----------------|
| Proste dane w pamięci | `MemoryStream` | `new MemoryStream()` |
| Duże pliki tymczasowe | `FileStream` (temp) | `new FileStream(Path.GetTempFileName(), FileMode.Create, FileAccess.ReadWrite, FileShare.None, 81920, true)` |
| Źródło sieciowe | `NetworkStream` | `new NetworkStream(socket)` |
| Własne buforowanie | Derive from `Stream` | See [dokumentacja Microsoft] for custom stream implementation |

> **Uwaga:** Zawsze ustaw `stream.Position = 0` przed zwróceniem, jeśli wstępnie wypełniasz strumień; w przeciwnym razie czytniki dalszego przetwarzania uznają strumień za pusty.

---

## Ilustracja

![Diagram pokazujący proces tworzenia strumienia pamięci c#](https://example.com/images/create-memory-stream-diagram.png)

*Alt text:* diagram pokazujący proces tworzenia strumienia pamięci c#

---

## Pełny działający przykład

Poniżej znajduje się minimalna aplikacja konsolowa, która demonstruje zarówno podejście legacy, jak i nowoczesne. Możesz skopiować i wkleić ją do nowego projektu konsolowego .NET 6 i uruchomić bez zmian.

```csharp
using System;
using System.IO;
using System.Threading;
using System.Threading.Tasks;

// -------------------------------------------------
// Legacy implementation (pre‑24.2)
// -------------------------------------------------
public class MyStorage : IOutputStorage
{
    public Stream CreateStream(string name) => new MemoryStream();
}

// -------------------------------------------------
// Modern implementation (24.2+)
// -------------------------------------------------
public class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string name) => new MemoryStream();

    public override async Task<Stream> HandleResourceAsync(string name, CancellationToken ct = default)
    {
        await Task.Delay(10, ct); // simulate async work
        return new MemoryStream();
    }
}

// -------------------------------------------------
// Demo program
// -------------------------------------------------
class Program
{
    static async Task Main()
    {
        // Legacy usage
        IOutputStorage legacy = new MyStorage();
        using (var legacyStream = legacy.CreateStream("legacy"))
        using (var writer = new StreamWriter(legacyStream))
        {
            writer.Write("Hello from legacy API!");
            writer.Flush();
            legacyStream.Seek(0, SeekOrigin.Begin);
            Console.WriteLine(new StreamReader(legacyStream).ReadToEnd());
        }

        // Modern sync usage
        var handler = new MyHandler();
        using (var modernStream = handler.HandleResource("modern"))
        using (var writer = new StreamWriter(modernStream))
        {
            writer.Write("Hello from modern API!");
            writer.Flush();
            modernStream.Seek(0, SeekOrigin.Begin);
            Console.WriteLine(new StreamReader(modernStream).ReadToEnd());
        }

        // Modern async usage
        using (var asyncStream = await handler.HandleResourceAsync("async"))
        using (var writer = new StreamWriter(asyncStream))
        {
            await writer.WriteAsync("Hello from async API!");
            await writer.FlushAsync();
            asyncStream.Seek(0, SeekOrigin.Begin);
            Console.WriteLine(await new StreamReader(asyncStream).ReadToEndAsync());
        }
    }
}
```

**Oczekiwany wynik**

```
Hello from legacy API!
Hello from modern API!
Hello from async API!
```

Program pokazuje trzy sposoby **how to create stream**: stary `IOutputStorage`, nowy synchroniczny `HandleResource` oraz asynchroniczny `HandleResourceAsync`. Wszystkie trzy zwracają `MemoryStream`, co dowodzi, że własne tworzenie strumieni działa niezależnie od wersji, którą celujesz.

---

## Najczęściej zadawane pytania (FAQ)

**Q: Czy muszę wywołać `Dispose` na strumieniu, który otrzymuję?**  
A: Framework (lub Twój kod wywołujący) jest odpowiedzialny za zwolnienie. Jeśli opakowujesz inny obiekt disposable w zwróconym strumieniu, upewnij się, że propaguje wywołanie `Dispose`.

**Q: Czy mogę zwrócić strumień tylko do odczytu?**  
A: Tak, ale kontrakt zazwyczaj oczekuje strumienia zapisywalnego. Jeśli potrzebujesz tylko odczytu, zaimplementuj `CanWrite => false` i udokumentuj ograniczenie.

**Q: Co zrobić, jeśli moje dane są większe niż dostępna pamięć RAM?**  
A: Przejdź na `FileStream` oparty na pliku tymczasowym lub zaimplementuj własny buforowany strumień zapisujący na dysk w fragmentach.

**Q: Czy istnieje różnica wydajnościowa między tymi dwoma podejściami?**  
A: Nowoczesny `ResourceHandler` wprowadza niewielki narzut związany z dodatkową logiką klasy bazowej, ale wersja async może znacząco zwiększyć przepustowość przy wysokiej współbieżności.

---

## Podsumowanie

Właśnie omówiliśmy **create memory stream c#** ze wszystkich perspektyw, które możesz napotkać w praktyce. Teraz wiesz **how to create stream** używając zarówno starszego wzorca `IOutputStorage`, jak i nowszej klasy `ResourceHandler`, a także zobaczyłeś praktyczne wskazówki dotyczące **how to handle resources** w odpowiedzialny sposób oraz rozszerzenia wzorca o **custom stream creation** dla dużych plików lub scenariuszy async.

Ready for

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}