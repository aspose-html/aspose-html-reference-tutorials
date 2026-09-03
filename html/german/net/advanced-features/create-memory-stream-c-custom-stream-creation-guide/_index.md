---
category: general
date: 2025-12-27
description: Erstelle schnell einen MemoryStream in C# mit einer Schritt‑für‑Schritt‑Anleitung.
  Lerne, wie du einen Stream erstellst, Ressourcen verwaltest und die benutzerdefinierte
  Stream‑Erstellung in .NET implementierst.
draft: false
keywords:
- create memory stream c#
- how to create stream
- how to handle resources
- custom stream creation
language: de
og_description: Erstelle MemoryStream in C# in Sekundenschnelle. Dieses Tutorial zeigt,
  wie man einen Stream erstellt, Ressourcen verwaltet und die Erstellung benutzerdefinierter
  Streams mit modernen .NET‑APIs aufbaut.
og_title: Memory-Stream in C# erstellen – Vollständiger Leitfaden für benutzerdefinierte
  Streams
tags:
- stream
- csharp
- .net
- resource-handling
title: Memory-Stream in C# erstellen – Leitfaden zur benutzerdefinierten Stream-Erstellung
url: /de/net/advanced-features/create-memory-stream-c-custom-stream-creation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Memory-Stream in C# erstellen – Anleitung zur benutzerdefinierten Stream-Erstellung

Haben Sie jemals **create memory stream c#** benötigt, waren sich aber nicht sicher, welche API Sie wählen sollen? Sie sind nicht allein. In vielen Legacy‑Projekten finden Sie `IOutputStorage`, während neuere Codebasen `ResourceHandler` bevorzugen. In beiden Fällen ist das Ziel dasselbe: einen `Stream` erzeugen, den Ihr Framework konsumieren kann.

In diesem Tutorial lernen Sie **how to create stream** Objekte, **how to handle resources** sicher zu handhaben und meistern **custom stream creation** für sowohl pre‑24.2 als auch 24.2+ Versionen der Bibliothek. Am Ende haben Sie ein funktionierendes Beispiel, das Sie in jede .NET‑Lösung einbinden können – keine mysteriösen Referenzen, nur reines C#.

## Was Sie mitnehmen werden

- Ein klarer Vergleich des Legacy‑`IOutputStorage`‑Musters gegenüber dem modernen `ResourceHandler`‑Ansatz.  
- Vollständiger, copy‑paste‑fertiger Code, der gegen .NET 6+ (oder früher, falls nötig) kompiliert.  
- Tipps für Randfälle wie das Entsorgen von Streams, das Verarbeiten großer Payloads und das Testen Ihres benutzerdefinierten Streams.  

> **Pro‑Tipp:** Wenn Sie .NET 8 anvisieren, bietet der neuere `ResourceHandler` integrierte Async‑Unterstützung, die Millisekunden bei Hochdurchsatz‑Szenarien einsparen kann.

## Memory-Stream in C# erstellen – Legacy‑Ansatz (pre‑24.2)

Wenn Sie auf einer älteren Version der Bibliothek feststecken, müssen Sie den Vertrag `IOutputStorage` erfüllen. Das Interface verlangt nur eine Methode, die für einen gegebenen Ressourcennamen einen `Stream` zurückgibt.

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

### Warum das funktioniert

- **Interface‑Vertrag** – Das Framework ruft `CreateStream` auf, wann immer es Ausgaben schreiben muss.  
- **Flexibilität** – Da Sie einen `Stream` zurückgeben, können Sie später `MemoryStream` durch `FileStream` oder sogar einen benutzerdefinierten gepufferten Stream ersetzen, ohne den Rest des Codes zu berühren.  
- **Ressourcensicherheit** – Der Aufrufer ist für das Entsorgen des zurückgegebenen Streams verantwortlich, weshalb wir `Dispose` nicht innerhalb der Methode aufrufen.  

### Häufige Fallstricke

| Problem | Was passiert | Lösung |
|---------|--------------|--------|
| Rückgabe eines geschlossenen Streams | Verbraucher erhalten beim Schreiben eine `ObjectDisposedException`. | Stellen Sie sicher, dass der Stream **offen** ist, wenn Sie ihn übergeben. |
| Vergessen, nach dem Schreiben `Position = 0` zu setzen | Daten erscheinen leer, wenn sie später gelesen werden. | Rufen Sie `stream.Seek(0, SeekOrigin.Begin)` vor der Rückgabe auf, wenn Sie ihn vorher befüllen. |
| Verwendung eines riesigen `MemoryStream` für große Dateien | Out‑of‑Memory‑Abstürze. | Wechseln Sie zu einem temporären `FileStream` oder einem benutzerdefinierten gepufferten Stream. |

## Memory-Stream in C# erstellen – Moderner Ansatz (24.2+)

Ab Version 24.2 hat die Bibliothek `ResourceHandler` eingeführt. Statt eines Interfaces erben Sie jetzt von einer Basisklasse und überschreiben eine einzige Methode. Das bietet Ihnen einen saubereren, async‑freundlichen Einstiegspunkt.

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

### Warum `ResourceHandler` bevorzugen

- **Async‑Unterstützung** – Die Methode `HandleResourceAsync` ermöglicht I/O ohne Blockierung von Threads.  
- **Integrierte Fehlerbehandlung** – Die Basisklasse fängt Ausnahmen ab und wandelt sie in framework‑spezifische Fehlercodes um.  
- **Zukunftssicher** – Neuere Versionen fügen Hooks (z. B. Logging, Telemetrie) hinzu, die nur mit dem Handler‑Muster funktionieren.  

### Umgang mit Randfällen

1. **Entsorgung** – Das Framework entsorgt den Stream, sobald er fertig ist, aber wenn Sie ein weiteres `IDisposable` (wie einen `FileStream`) einbetten, sollten Sie innerhalb der Methode einen `using`‑Block implementieren und einen Wrapper zurückgeben, der `Dispose` weiterleitet.  
2. **Große Payloads** – Wenn Sie Payloads > 100 MB erwarten, ersetzen Sie `MemoryStream` durch einen `FileStream`, der auf eine temporäre Datei zeigt. Beispiel:  

   ```csharp
   return new FileStream(Path.GetTempFileName(),
                         FileMode.Create,
                         FileAccess.ReadWrite,
                         FileShare.None,
                         bufferSize: 81920,
                         useAsync: true);
   ```

3. **Testing** – Testen Sie Ihren Handler per Unit‑Test, indem Sie einen Mock `IServiceProvider` injizieren, falls die Basisklasse Dienste aus DI bezieht. Verifizieren Sie, dass `HandleResource` einen Stream zurückgibt, der beschrieben und gelesen werden kann.  

## Wie man einen Stream erstellt – Schnellübersicht

| Szenario | Empfohlene API | Beispielcode |
|----------|----------------|--------------|
| Einfacher In‑Memory‑Daten | `MemoryStream` | `new MemoryStream()` |
| Große temporäre Dateien | `FileStream` (temp) | `new FileStream(Path.GetTempFileName(), FileMode.Create, FileAccess.ReadWrite, FileShare.None, 81920, true)` |
| Netzwerkbasierte Quelle | `NetworkStream` | `new NetworkStream(socket)` |
| Benutzerdefiniertes Puffering | Derive from `Stream` | Siehe [Microsoft docs] for custom stream implementation |

> **Hinweis:** Setzen Sie immer `stream.Position = 0`, bevor Sie zurückgeben, wenn Sie den Stream vorher befüllen; andernfalls gehen nachgelagerte Leser davon aus, dass der Stream leer ist.

## Bildillustration

![Diagramm, das den Prozess zum Erstellen eines Memory-Streams in C# zeigt](https://example.com/images/create-memory-stream-diagram.png)

*Alt text:* diagram showing create memory stream c# process

## Vollständiges ausführbares Beispiel

Unten finden Sie eine minimale Konsolen‑App, die sowohl den Legacy‑ als auch den modernen Ansatz demonstriert. Sie können sie in ein neues .NET 6‑Konsolenprojekt kopieren und unverändert ausführen.

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

**Erwartete Ausgabe**

```
Hello from legacy API!
Hello from modern API!
Hello from async API!
```

Das Programm zeigt drei Wege, **how to create stream** zu verwenden: das alte `IOutputStorage`, das neue synchrone `HandleResource` und das asynchrone `HandleResourceAsync`. Alle drei geben einen `MemoryStream` zurück, was beweist, dass benutzerdefinierte Stream‑Erstellung unabhängig von der Zielversion funktioniert.

## Häufig gestellte Fragen (FAQ)

**F: Muss ich `Dispose` für den zurückgegebenen Stream aufrufen?**  
A: Das Framework (oder Ihr Aufrufercode) ist für das Entsorgen verantwortlich. Wenn Sie ein weiteres `IDisposable` in Ihrem zurückgegebenen Stream einbetten, stellen Sie sicher, dass es den `Dispose`‑Aufruf weiterleitet.

**F: Kann ich einen schreibgeschützten Stream zurückgeben?**  
A: Ja, aber der Vertrag erwartet normalerweise einen beschreibbaren Stream. Wenn Sie nur lesen müssen, implementieren Sie `CanWrite => false` und dokumentieren die Einschränkung.

**F: Was, wenn meine Daten größer sind als der verfügbare RAM?**  
A: Wechseln Sie zu einem `FileStream`, der auf einer temporären Datei basiert, oder implementieren Sie einen benutzerdefinierten gepufferten Stream, der in Stücke auf die Festplatte schreibt.

**F: Gibt es Leistungsunterschiede zwischen den beiden Ansätzen?**  
A: Der moderne `ResourceHandler` fügt einen kleinen Overhead durch die zusätzliche Basisklassen‑Logik hinzu, aber die Async‑Version kann den Durchsatz bei hoher Parallelität deutlich steigern.

## Fazit

Wir haben gerade **create memory stream c#** aus allen Blickwinkeln behandelt, die Sie in der Praxis antreffen können. Sie wissen jetzt **how to create stream** sowohl mit dem Legacy‑`IOutputStorage`‑Muster als auch mit der neueren `ResourceHandler`‑Klasse, und Sie haben praktische Tipps für **how to handle resources** verantwortungsbewusst erhalten sowie das Muster mit **custom stream creation** für große Dateien oder Async‑Szenarien erweitert.

Ready for

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}