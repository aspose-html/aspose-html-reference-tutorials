---
category: general
date: 2025-12-27
description: Maak snel een memory stream in C# met een stapsgewijze handleiding. Leer
  hoe je een stream maakt, resources beheert en aangepaste streamcreatie implementeert
  in .NET.
draft: false
keywords:
- create memory stream c#
- how to create stream
- how to handle resources
- custom stream creation
language: nl
og_description: Maak een memory stream in C# in enkele seconden. Deze tutorial laat
  zien hoe je een stream maakt, resources beheert en aangepaste streamcreatie bouwt
  met moderne .NET‑API’s.
og_title: Maak een geheugenstroom C# – Complete gids voor aangepaste streams
tags:
- stream
- csharp
- .net
- resource-handling
title: Maak MemoryStream c# – Gids voor aangepaste streamcreatie
url: /nl/net/advanced-features/create-memory-stream-c-custom-stream-creation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak geheugenstroom c# – Gids voor aangepaste streamcreatie

Heb je ooit **create memory stream c#** moeten maken maar wist je niet welke API je moest kiezen? Je bent niet de enige. In veel legacy‑projecten vind je `IOutputStorage`, terwijl nieuwere codebases de voorkeur geven aan `ResourceHandler`. Hoe dan ook, het doel is hetzelfde: een `Stream` produceren die je framework kan gebruiken.

In deze tutorial leer je **how to create stream** objecten, **how to handle resources** veilig te behandelen, en beheers je **custom stream creation** voor zowel pre‑24.2 als 24.2+ versies van de bibliotheek. Aan het einde heb je een werkend voorbeeld dat je in elke .NET‑oplossing kunt plaatsen—geen mysterieuze referenties, alleen pure C#.

## Wat je mee krijgt

- Een duidelijke vergelijking van het legacy `IOutputStorage`‑patroon versus de moderne `ResourceHandler`‑aanpak.  
- Complete, copy‑paste‑klare code die compileert tegen .NET 6+ (of eerder, indien nodig).  
- Tips voor randgevallen zoals het vrijgeven van streams, het verwerken van grote payloads, en het testen van je aangepaste stream.  

> **Pro tip:** Als je richt op .NET 8, biedt de nieuwere `ResourceHandler` ingebouwde async‑ondersteuning, wat milliseconden kan besparen bij scenario's met hoge doorvoer.

## Maak geheugenstroom c# – Legacy‑aanpak (pre‑24.2)

Wanneer je vastzit op een oudere versie van de bibliotheek, is het contract dat je moet voldoen `IOutputStorage`. De interface vraagt alleen om een methode die een `Stream` retourneert voor een opgegeven resource‑naam.

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

### Waarom dit werkt

- **Interface contract** – Het framework zal `CreateStream` aanroepen wanneer het output moet schrijven.  
- **Flexibility** – Omdat je een `Stream` retourneert, kun je later `MemoryStream` vervangen door `FileStream` of zelfs een aangepaste gebufferde stream zonder de rest van de code aan te passen.  
- **Resource safety** – De aanroeper is verantwoordelijk voor het vrijgeven van de geretourneerde stream, daarom roepen we `Dispose` niet aan binnen de methode.  

### Veelvoorkomende valkuilen

| Probleem | Wat gebeurt er | Oplossing |
|----------|----------------|-----------|
| Een gesloten stream retourneren | Consumenten krijgen `ObjectDisposedException` bij schrijven. | Zorg ervoor dat de stream **open** is wanneer je deze overdraagt. |
| Vergeten `Position = 0` in te stellen na het schrijven | Data lijkt leeg bij later lezen. | Roep `stream.Seek(0, SeekOrigin.Begin)` aan vóór het retourneren als je de stream vooraf vult. |
| Een enorme `MemoryStream` gebruiken voor grote bestanden | Out‑of‑memory crashes. | Schakel over naar een tijdelijke `FileStream` of een aangepaste gebufferde stream. |

## Maak geheugenstroom c# – Moderne aanpak (24.2+)

Vanaf versie 24.2 heeft de bibliotheek `ResourceHandler` geïntroduceerd. In plaats van een interface erft je nu van een basisklasse en overschrijf je één methode. Dit geeft je een schoner, async‑vriendelijk toegangspunt.

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

### Waarom `ResourceHandler` verkiezen

- **Async support** – De `HandleResourceAsync`‑methode laat je I/O uitvoeren zonder threads te blokkeren.  
- **Built‑in error handling** – De basisklasse vangt uitzonderingen op en zet ze om in framework‑specifieke foutcodes.  
- **Future‑proof** – Nieuwere releases voegen hooks toe (bijv. logging, telemetry) die alleen werken met het handler‑patroon.  

### Afhandeling van randgevallen

1. **Disposal** – Het framework maakt de stream vrij nadat deze klaar is, maar als je een andere disposable (zoals een `FileStream`) omsluit, moet je een `using`‑blok binnen de methode implementeren en een wrapper retourneren die `Dispose` doorgeeft.  
2. **Large payloads** – Als je > 100 MB payloads verwacht, vervang `MemoryStream` door een `FileStream` die naar een tijdelijk bestand wijst. Voorbeeld:  

   ```csharp
   return new FileStream(Path.GetTempFileName(),
                         FileMode.Create,
                         FileAccess.ReadWrite,
                         FileShare.None,
                         bufferSize: 81920,
                         useAsync: true);
   ```

3. **Testing** – Unit‑test je handler door een mock `IServiceProvider` te injecteren als de basisklasse services uit DI haalt. Verifieer dat `HandleResource` een stream retourneert die zowel geschreven als gelezen kan worden.

## Hoe stream te maken – Een snelle spiekbrief

| Scenario | Aanbevolen API | Voorbeeldcode |
|----------|----------------|---------------|
| Simpele in‑memory data | `MemoryStream` | `new MemoryStream()` |
| Grote tijdelijke bestanden | `FileStream` (temp) | `new FileStream(Path.GetTempFileName(), FileMode.Create, FileAccess.ReadWrite, FileShare.None, 81920, true)` |
| Netwerk‑gebaseerde bron | `NetworkStream` | `new NetworkStream(socket)` |
| Aangepaste buffering | Derive from `Stream` | See [Microsoft docs] for custom stream implementation |

> **Opmerking:** Stel altijd `stream.Position = 0` in vóór het retourneren als je de stream vooraf vult; anders denken downstream‑lezers dat de stream leeg is.

## Afbeeldingsillustratie

![diagram dat het proces van create memory stream c# toont](https://example.com/images/create-memory-stream-diagram.png)

*Alt text:* diagram dat het proces van create memory stream c# toont

## Volledig uitvoerbaar voorbeeld

Hieronder staat een minimale console‑app die zowel de legacy‑ als moderne aanpakken demonstreert. Je kunt het copy‑pasten in een nieuw .NET 6 console‑project en direct uitvoeren.

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

**Verwachte output**

```
Hello from legacy API!
Hello from modern API!
Hello from async API!
```

Het programma toont drie manieren om **how to create stream**: de oude `IOutputStorage`, de nieuwe synchronische `HandleResource` en de asynchrone `HandleResourceAsync`. Alle drie retourneren een `MemoryStream`, wat bewijst dat aangepaste streamcreatie werkt ongeacht welke versie je target.

## Veelgestelde vragen (FAQ)

**Q: Moet ik `Dispose` aanroepen op de stream die ik terugkrijg?**  
A: Het framework (of jouw aanroepende code) is verantwoordelijk voor het vrijgeven. Als je een andere disposable in je geretourneerde stream omsluit, zorg er dan voor dat deze de `Dispose`‑aanroep doorgeeft.

**Q: Kan ik een alleen‑lezen stream retourneren?**  
A: Ja, maar het contract verwacht meestal een schrijfbare stream. Als je alleen hoeft te lezen, implementeer `CanWrite => false` en documenteer de beperking.

**Q: Wat als mijn data groter is dan het beschikbare RAM?**  
A: Schakel over naar een `FileStream` die wordt ondersteund door een tijdelijk bestand, of implementeer een aangepaste gebufferde stream die in stukken naar schijf schrijft.

**Q: Is er een prestatieverschil tussen de twee aanpakken?**  
A: De moderne `ResourceHandler` voegt een kleine overhead toe door de extra basisklasse‑logica, maar de async‑versie kan de doorvoer aanzienlijk verbeteren bij hoge gelijktijdigheid.

## Samenvatting

We hebben zojuist **create memory stream c#** vanuit elk perspectief behandeld dat je in de praktijk kunt tegenkomen. Je weet nu **how to create stream** te gebruiken met zowel het legacy `IOutputStorage`‑patroon als de nieuwere `ResourceHandler`‑klasse, en je hebt praktische tips gezien voor **how to handle resources** op een verantwoorde manier en het uitbreiden van het patroon met **custom stream creation** voor grote bestanden of async‑scenario's.

Ready for

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}