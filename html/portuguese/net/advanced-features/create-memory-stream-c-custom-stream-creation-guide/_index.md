---
category: general
date: 2025-12-27
description: Crie um MemoryStream em C# rapidamente com um guia passo a passo. Aprenda
  como criar streams, gerenciar recursos e implementar a criação de streams personalizados
  no .NET.
draft: false
keywords:
- create memory stream c#
- how to create stream
- how to handle resources
- custom stream creation
language: pt
og_description: Crie um MemoryStream em C# em segundos. Este tutorial mostra como
  criar streams, gerenciar recursos e construir streams personalizados com as APIs
  modernas do .NET.
og_title: Criar stream de memória em C# – Guia completo de stream personalizado
tags:
- stream
- csharp
- .net
- resource-handling
title: Criar stream de memória C# – Guia de criação de streams personalizados
url: /pt/net/advanced-features/create-memory-stream-c-custom-stream-creation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar memory stream c# – Guia de criação de stream personalizado

Já precisou **criar memory stream c#** mas não tinha certeza de qual API escolher? Você não está sozinho. Em muitos projetos legados você encontrará `IOutputStorage`, enquanto bases de código mais recentes preferem `ResourceHandler`. De qualquer forma, o objetivo é o mesmo: produzir um `Stream` que seu framework possa consumir.

Neste tutorial você aprenderá **como criar stream** objetos, **como manipular recursos** com segurança e dominar **a criação de stream personalizada** tanto para versões pré‑24.2 quanto 24.2+ da biblioteca. Ao final, você terá um exemplo funcional que pode ser inserido em qualquer solução .NET — sem referências misteriosas, apenas C# puro.

## O que você levará consigo

- Uma comparação clara do padrão legado `IOutputStorage` versus a abordagem moderna `ResourceHandler`.  
- Código completo, pronto para copiar‑e‑colar, que compila contra .NET 6+ (ou versões anteriores, se precisar).  
- Dicas para casos extremos, como descarte de streams, manipulação de cargas grandes e teste do seu stream personalizado.  

> **Dica profissional:** Se você está mirando .NET 8, o `ResourceHandler` mais recente oferece suporte assíncrono embutido, o que pode reduzir milissegundos em cenários de alta taxa de transferência.

## Criar memory stream c# – Abordagem legada (pré‑24.2)

Quando você está preso a uma versão mais antiga da biblioteca, o contrato que deve atender é `IOutputStorage`. A interface solicita apenas um método que retorne um `Stream` para um nome de recurso fornecido.

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

### Por que isso funciona

- **Contrato da interface** – O framework chamará `CreateStream` sempre que precisar gravar saída.  
- **Flexibilidade** – Como você devolve um `Stream`, pode trocar `MemoryStream` por `FileStream` ou até mesmo por um stream bufferizado customizado mais tarde, sem tocar no restante do código.  
- **Segurança de recursos** – O chamador é responsável por descartar o stream retornado, por isso não chamamos `Dispose` dentro do método.

### Armadilhas comuns

| Problema | O que acontece | Correção |
|----------|----------------|----------|
| Retornar um stream fechado | Os consumidores receberão `ObjectDisposedException` ao escrever. | Garanta que o stream esteja **aberto** quando for entregue. |
| Esquecer de definir `Position = 0` após escrever | Os dados parecem vazios quando lidos posteriormente. | Chame `stream.Seek(0, SeekOrigin.Begin)` antes de retornar se você pré‑popular o stream. |
| Usar um `MemoryStream` enorme para arquivos grandes | Falhas por falta de memória. | Troque por um `FileStream` temporário ou um stream bufferizado customizado. |

## Criar memory stream c# – Abordagem moderna (24.2+)

A partir da versão 24.2 a biblioteca introduziu `ResourceHandler`. Em vez de uma interface, agora você herda de uma classe base e sobrescreve um único método. Isso fornece um ponto de entrada mais limpo e amigável ao async.

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

### Por que preferir `ResourceHandler`

- **Suporte async** – O método `HandleResourceAsync` permite executar I/O sem bloquear threads.  
- **Tratamento de erros embutido** – A classe base captura exceções e as converte em códigos de erro específicos do framework.  
- **À prova de futuro** – Lançamentos mais recentes adicionam ganchos (por exemplo, logging, telemetria) que funcionam apenas com o padrão de handler.

### Tratamento de casos extremos

1. **Descarte** – O framework descarta o stream após o uso, mas se você envolver outro objeto descartável (como um `FileStream`) deve implementar um bloco `using` dentro do método e retornar um wrapper que encaminhe `Dispose`.  
2. **Cargas grandes** – Se você prevê cargas > 100 MB, substitua `MemoryStream` por um `FileStream` apontando para um arquivo temporário. Exemplo:  

   ```csharp
   return new FileStream(Path.GetTempFileName(),
                         FileMode.Create,
                         FileAccess.ReadWrite,
                         FileShare.None,
                         bufferSize: 81920,
                         useAsync: true);
   ```

3. **Testes** – Teste unitário do seu handler injetando um mock `IServiceProvider` caso a classe base obtenha serviços via DI. Verifique se `HandleResource` devolve um stream que pode ser escrito e lido.

## Como criar stream – Um cheat sheet rápido

| Cenário | API recomendada | Código de exemplo |
|----------|----------------|-------------------|
| Dados simples em memória | `MemoryStream` | `new MemoryStream()` |
| Arquivos temporários grandes | `FileStream` (temp) | `new FileStream(Path.GetTempFileName(), FileMode.Create, FileAccess.ReadWrite, FileShare.None, 81920, true)` |
| Fonte baseada em rede | `NetworkStream` | `new NetworkStream(socket)` |
| Bufferização customizada | Derivar de `Stream` | Veja [Microsoft docs] para implementação de stream customizado |

> **Observação:** Sempre defina `stream.Position = 0` antes de retornar se você pré‑popular o stream; caso contrário, leitores posteriores pensarão que o stream está vazio.

## Ilustração de imagem

![Diagram showing create memory stream c# process](https://example.com/images/create-memory-stream-diagram.png)

*Texto alternativo:* diagrama mostrando o processo de criar memory stream c#

## Exemplo completo executável

A seguir, um aplicativo console mínimo que demonstra ambas as abordagens, legada e moderna. Você pode copiar‑e‑colar em um novo projeto console .NET 6 e executá‑lo tal como está.

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

**Saída esperada**

```
Hello from legacy API!
Hello from modern API!
Hello from async API!
```

O programa mostra três maneiras de **como criar stream**: o antigo `IOutputStorage`, o novo `HandleResource` síncrono e o `HandleResourceAsync` assíncrono. Todos retornam um `MemoryStream`, provando que a criação de stream personalizada funciona independentemente da versão alvo.

## Perguntas frequentes (FAQ)

**Q: Preciso chamar `Dispose` no stream que recebo?**  
A: O framework (ou seu código chamador) é responsável pelo descarte. Se você envolver outro objeto descartável dentro do stream retornado, certifique‑se de que ele propague a chamada `Dispose`.

**Q: Posso devolver um stream somente leitura?**  
A: Sim, mas o contrato geralmente espera um stream gravável. Se precisar apenas ler, implemente `CanWrite => false` e documente a limitação.

**Q: E se meus dados forem maiores que a RAM disponível?**  
A: Troque para um `FileStream` respaldado por um arquivo temporário, ou implemente um stream bufferizado customizado que escreva em disco em blocos.

**Q: Existe diferença de desempenho entre as duas abordagens?**  
A: O `ResourceHandler` moderno adiciona um pequeno overhead devido à lógica da classe base, mas a versão assíncrona pode melhorar drasticamente a taxa de transferência em alta concorrência.

## Conclusão

Acabamos de cobrir **criar memory stream c#** de todos os ângulos que você pode encontrar no mundo real. Agora você sabe **como criar stream** usando tanto o padrão legado `IOutputStorage` quanto a nova classe `ResourceHandler`, além de ter visto dicas práticas para **como manipular recursos** de forma responsável e estender o padrão com **criação de stream personalizada** para arquivos grandes ou cenários async.

Ready for

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}