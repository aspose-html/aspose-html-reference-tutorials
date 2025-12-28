---
category: general
date: 2025-12-27
description: Créez rapidement un flux mémoire en C# avec un guide étape par étape.
  Apprenez à créer un flux, à gérer les ressources et à implémenter la création de
  flux personnalisés dans .NET.
draft: false
keywords:
- create memory stream c#
- how to create stream
- how to handle resources
- custom stream creation
language: fr
og_description: Créez un flux mémoire en C# en quelques secondes. Ce tutoriel montre
  comment créer un flux, gérer les ressources et concevoir une création de flux personnalisée
  avec les API .NET modernes.
og_title: Créer un flux mémoire en C# – Guide complet du flux personnalisé
tags:
- stream
- csharp
- .net
- resource-handling
title: Créer un flux mémoire C# – Guide de création de flux personnalisé
url: /fr/net/advanced-features/create-memory-stream-c-custom-stream-creation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un flux mémoire c# – Guide de création de flux personnalisé

Vous avez déjà eu besoin de **créer un flux mémoire c#** sans savoir quelle API choisir ? Vous n'êtes pas seul. Dans de nombreux projets hérités, vous trouverez `IOutputStorage`, tandis que les bases de code plus récentes privilégient `ResourceHandler`. Dans les deux cas, l'objectif est le même : produire un `Stream` que votre framework peut consommer.

Dans ce tutoriel, vous apprendrez **comment créer des objets stream**, **comment gérer les ressources** en toute sécurité, et maîtriserez **la création de flux personnalisés** pour les versions pré‑24.2 et 24.2+ de la bibliothèque. À la fin, vous disposerez d'un exemple fonctionnel à intégrer dans n'importe quelle solution .NET—sans références mystères, juste du pur C#.

## Ce que vous allez retenir

- Une comparaison claire du modèle hérité `IOutputStorage` vs. l'approche moderne `ResourceHandler`.  
- Un code complet, prêt à copier‑coller, qui compile avec .NET 6+ (ou antérieur, si besoin).  
- Des astuces pour les cas limites comme la libération des flux, la gestion de gros chargements, et les tests de votre flux personnalisé.  

> **Astuce pro :** Si vous ciblez .NET 8, le nouveau `ResourceHandler` vous offre un support asynchrone intégré, ce qui peut économiser des millisecondes dans les scénarios à haut débit.

---

## Créer un flux mémoire c# – Approche héritée (pré‑24.2)

Lorsque vous êtes bloqué sur une version plus ancienne de la bibliothèque, le contrat à satisfaire est `IOutputStorage`. L'interface ne demande qu'une méthode qui renvoie un `Stream` pour un nom de ressource donné.

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

### Pourquoi cela fonctionne

- **Contrat d'interface** – Le framework appellera `CreateStream` chaque fois qu'il devra écrire la sortie.  
- **Flexibilité** – Comme vous renvoyez un `Stream`, vous pouvez remplacer `MemoryStream` par `FileStream` ou même un flux tampon personnalisé plus tard sans toucher au reste du code.  
- **Sécurité des ressources** – L'appelant est responsable de la libération du flux retourné, c'est pourquoi nous n'appelons pas `Dispose` à l'intérieur de la méthode.

### Pièges courants

| Problème | Ce qui se passe | Solution |
|----------|-----------------|----------|
| Retour d'un flux fermé | Les consommateurs recevront `ObjectDisposedException` lors de l'écriture. | Assurez‑vous que le flux est **ouvert** lorsqu'il est remis. |
| Oublier de définir `Position = 0` après l'écriture | Les données semblent vides lors de la lecture ultérieure. | Appelez `stream.Seek(0, SeekOrigin.Begin)` avant de retourner le flux si vous le pré‑remplissez. |
| Utiliser un `MemoryStream` gigantesque pour de gros fichiers | Crashs pour manque de mémoire. | Passez à un `FileStream` temporaire ou à un flux tampon personnalisé. |

---

## Créer un flux mémoire c# – Approche moderne (24.2+)

À partir de la version 24.2, la bibliothèque a introduit `ResourceHandler`. Au lieu d'une interface, vous héritez maintenant d'une classe de base et surchargez une seule méthode. Cela vous donne un point d'entrée plus propre et compatible async.

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

### Pourquoi privilégier `ResourceHandler`

- **Support async** – La méthode `HandleResourceAsync` vous permet d'effectuer des I/O sans bloquer les threads.  
- **Gestion d'erreurs intégrée** – La classe de base intercepte les exceptions et les convertit en codes d'erreur spécifiques au framework.  
- **Préparation au futur** – Les versions récentes ajoutent des hooks (par ex., journalisation, télémétrie) qui ne fonctionnent qu'avec le pattern handler.

### Gestion des cas limites

1. **Libération** – Le framework libère le flux après utilisation, mais si vous encapsulez un autre objet jetable (comme un `FileStream`) vous devez implémenter un bloc `using` à l'intérieur de la méthode et retourner un wrapper qui transmet `Dispose`.  
2. **Gros chargements** – Si vous prévoyez des charges > 100 Mo, remplacez `MemoryStream` par un `FileStream` pointant vers un fichier temporaire. Exemple :  

   ```csharp
   return new FileStream(Path.GetTempFileName(),
                         FileMode.Create,
                         FileAccess.ReadWrite,
                         FileShare.None,
                         bufferSize: 81920,
                         useAsync: true);
   ```

3. **Tests** – Testez votre handler en injectant un `IServiceProvider` factice si la classe de base récupère des services via DI. Vérifiez que `HandleResource` renvoie un flux pouvant être écrit et lu.

---

## Comment créer un flux – Fiche mémo rapide

| Scénario | API recommandée | Exemple de code |
|----------|-----------------|-----------------|
| Données simples en mémoire | `MemoryStream` | `new MemoryStream()` |
| Gros fichiers temporaires | `FileStream` (temp) | `new FileStream(Path.GetTempFileName(), FileMode.Create, FileAccess.ReadWrite, FileShare.None, 81920, true)` |
| Source réseau | `NetworkStream` | `new NetworkStream(socket)` |
| Bufferisation personnalisée | Dériver de `Stream` | Voir [Microsoft docs] pour l'implémentation d'un flux personnalisé |

> **Remarque :** Toujours définir `stream.Position = 0` avant de retourner le flux si vous le pré‑remplissez ; sinon les lecteurs en aval penseront que le flux est vide.

---

## Illustration d'image

![Diagramme montrant le processus de création d'un flux mémoire c# process](https://example.com/images/create-memory-stream-diagram.png)

*Texte alternatif :* diagramme montrant le processus de création d'un flux mémoire c# process

---

## Exemple complet exécutable

Voici une application console minimale qui montre les deux approches, héritée et moderne. Vous pouvez la copier‑coller dans un nouveau projet console .NET 6 et l'exécuter tel quel.

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

**Sortie attendue**

```
Hello from legacy API!
Hello from modern API!
Hello from async API!
```

Le programme montre trois façons de **créer un flux** : l'ancienne `IOutputStorage`, le nouveau `HandleResource` synchrone, et le `HandleResourceAsync` asynchrone. Les trois retournent un `MemoryStream`, prouvant que la création de flux personnalisés fonctionne quel que soit la version ciblée.

---

## Questions fréquemment posées (FAQ)

**Q : Dois‑je appeler `Dispose` sur le flux que je récupère ?**  
R : Le framework (ou votre code appelant) est responsable de la libération. Si vous encapsulez un autre objet jetable dans votre flux retourné, assurez‑vous qu'il propage l'appel `Dispose`.

**Q : Puis‑je retourner un flux en lecture seule ?**  
R : Oui, mais le contrat attend généralement un flux inscriptible. Si vous avez seulement besoin de lecture, implémentez `CanWrite => false` et documentez la limitation.

**Q : Que faire si mes données dépassent la RAM disponible ?**  
R : Passez à un `FileStream` basé sur un fichier temporaire, ou implémentez un flux tampon personnalisé qui écrit sur disque par blocs.

**Q : Y a‑t‑il une différence de performance entre les deux approches ?**  
R : `ResourceHandler` moderne ajoute un léger surcoût lié à la logique de la classe de base, mais la version async peut améliorer considérablement le débit sous forte concurrence.

---

## Conclusion

Nous venons de couvrir **créer un flux mémoire c#** sous tous les angles que vous pourriez rencontrer. Vous savez maintenant **comment créer des flux** en utilisant à la fois le modèle hérité `IOutputStorage` et la classe moderne `ResourceHandler`, ainsi que des astuces pratiques pour **gérer les ressources** de façon responsable et étendre le pattern avec **la création de flux personnalisés** pour les gros fichiers ou les scénarios async.

Prêt pour

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}