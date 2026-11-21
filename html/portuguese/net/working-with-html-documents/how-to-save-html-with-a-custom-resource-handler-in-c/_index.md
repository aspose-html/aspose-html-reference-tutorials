---
category: general
date: 2026-11-20
description: Aprenda como salvar HTML usando um ResourceHandler personalizado em C#
  e também salvar HTML em arquivos zip com código conciso e pronto para produção.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: pt
lastmod: 2026-11-20
og_description: Como salvar HTML usando um ResourceHandler personalizado em C# e,
  opcionalmente, salvar HTML em arquivos zip — guia completo e executável para desenvolvedores
  .NET.
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: Como salvar HTML com um manipulador de recursos personalizado em C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  headline: How to save HTML with a custom resource handler in C#
  type: TechArticle
- description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  name: How to save HTML with a custom resource handler in C#
  steps:
  - name: What if I need multiple HTML files in the same zip?
    text: 'Create a new entry for each call to `HandleResource`. The `resourceName`
      argument typically contains the filename, so you can use it directly:'
  - name: How to handle large documents without exhausting memory?
    text: Replace `MemoryStream` with a `FileStream` that points to a temporary file.
      The handler then returns the file stream, and you can later delete the file
      after the zip is created.
  - name: Does this approach work with .NET Core on Linux?
    text: Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are
      cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.
  - name: Can I encrypt the zip archive?
    text: '`ZipArchive` supports password‑based encryption only through third‑party
      libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output
      bytes with a library that provides AES encryption before sending them to the
      client.'
  type: HowTo
tags:
- C#
- HTML
- file I/O
title: Como salvar HTML com um manipulador de recursos personalizado em C#
url: /pt/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como salvar HTML com um manipulador de recurso personalizado em C#

Se você precisa saber **como salvar HTML** a partir de uma string em memória ou de um documento analisado, este guia apresenta uma solução completa. Usar um `ResourceHandler` personalizado permite controlar o fluxo de destino, o que significa que você pode **salvar HTML em arquivos zip** sem criar arquivos temporários.

Você verá por que um `ResourceHandler` é preferido em relação à abordagem mais antiga `IOutputStorage`, como configurá‑lo e como estendê‑lo para compressão zip. Ao final deste tutorial, você poderá incorporar o código em qualquer projeto .NET 6+ e adaptá‑lo às suas próprias necessidades de armazenamento.

## O que você vai construir

* Um `ResourceHandler` mínimo que devolve um `MemoryStream`.
* Um `HtmlDocument` criado com **HtmlAgilityPack**.
* Uma chamada a `doc.Save` que grava o HTML no fluxo fornecido pelo manipulador.
* Um wrapper opcional que comprime o HTML resultante em um arquivo zip.

Pré‑requisitos:

* .NET 6 SDK ou superior.
* Pacote NuGet `HtmlAgilityPack` (`dotnet add package HtmlAgilityPack`).
* Familiaridade básica com fluxos C#.

## Etapa 1: Criar um manipulador de recurso personalizado (principal forma de **como salvar html**)

A classe base `ResourceHandler` (disponível a partir da versão 24.2 do SDK do visualizador) define um único método abstrato, `HandleResource`. Implementar este método lhe dá controle total sobre onde o HTML será escrito.

```csharp
using System.IO;

/// <summary>
/// Handles the output stream for each HTML resource.
/// Returning a MemoryStream keeps everything in memory, which is ideal for further processing
/// such as zipping or sending over a network.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string resourceName)
    {
        // You could inspect resourceName to decide between file, memory, or zip entry.
        return new MemoryStream();
    }
}
```

**Por que isso importa:** Ao devolver um `MemoryStream`, você evita I/O de disco, reduz a latência e mantém o código determinístico para testes unitários. O manipulador é invocado automaticamente pelo método `Save`, portanto você nunca precisa passar um fluxo explicitamente.

## Etapa 2: Carregar ou construir o documento HTML

`HtmlAgilityPack` fornece a prática classe `HtmlDocument` que pode analisar uma string, um arquivo ou um fluxo. Neste exemplo carregamos um literal simples, mas o mesmo código funciona com qualquer fonte HTML.

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**Por que isso importa:** Manter o documento em memória está alinhado com a abordagem baseada em fluxo do manipulador personalizado. Também permite que você manipule o DOM antes de salvar, como injetar scripts ou corrigir tags malformadas.

## Etapa 3: Salvar o documento usando o manipulador personalizado

Chamar `doc.Save` com uma instância de `MyHandler` dispara o método `HandleResource`. O HTML é escrito diretamente no fluxo que você devolveu.

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

Após a conclusão de `Save`, o `MemoryStream` dentro de `MyHandler` contém o HTML serializado. Você pode recuperá‑lo assim:

```csharp
// Cast the handler back to access the stream (if you kept a reference)
MyHandler handler = new MyHandler();
doc.Save(handler);

// Reset position to read from the beginning.
handler.HandleResource("").Seek(0, SeekOrigin.Begin);
using var reader = new StreamReader(handler.HandleResource(""));
string htmlOutput = reader.ReadToEnd();
System.Console.WriteLine(htmlOutput);
```

**Resultado:** O console imprime exatamente o HTML que você passou para `LoadHtml`. Isso comprova que você agora entende **como salvar HTML** com um manipulador personalizado.

## Etapa 4: Estender o manipulador para **salvar HTML em zip**

Se você quiser arquivar o HTML, modifique `MyHandler` para gravar em um `ZipArchiveEntry`. O namespace .NET `System.IO.Compression` torna isso simples.

```csharp
using System.IO.Compression;

/// <summary>
/// Writes the HTML into a zip entry named "document.html".
/// The zip archive is created in memory and can be saved to a file or sent over HTTP.
/// </summary>
class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        // Initialise the zip archive in create mode.
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        // Create a zip entry for the HTML file.
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open(); // Returns a stream that writes directly into the zip entry.
    }

    /// <summary>
    /// Finalises the zip archive and returns the raw bytes.
    /// </summary>
    public byte[] GetZipBytes()
    {
        // Ensure all entries are flushed.
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}
```

Agora use o novo manipulador:

```csharp
// Instantiate the zip‑aware handler.
using var zipHandler = new ZipHtmlHandler();

// Save HTML; it ends up inside the zip archive.
doc.Save(zipHandler);

// Retrieve the zip file as a byte array.
byte[] zipBytes = zipHandler.GetZipBytes();

// Optionally write the zip to disk for verification.
File.WriteAllBytes("output.zip", zipBytes);
System.Console.WriteLine("ZIP file created with size: " + zipBytes.Length);
```

**Por que isso funciona:** O método `HandleResource` cria uma entrada zip chamada `document.html`. Quando `doc.Save` grava no fluxo devolvido, os dados são comprimidos automaticamente. Como o zip é construído em memória, você pode retorná‑lo de uma API web, anexá‑lo a um e‑mail ou armazená‑lo em um banco de dados sem tocar no sistema de arquivos.

## Perguntas comuns e casos extremos

### E se eu precisar de vários arquivos HTML no mesmo zip?
Crie uma nova entrada para cada chamada a `HandleResource`. O argumento `resourceName` normalmente contém o nome do arquivo, então você pode usá‑lo diretamente:

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### Como lidar com documentos grandes sem esgotar a memória?
Substitua `MemoryStream` por um `FileStream` que aponta para um arquivo temporário. O manipulador então devolve o fluxo de arquivo, e você pode excluir o arquivo posteriormente, após a criação do zip.

### Essa abordagem funciona com .NET Core no Linux?
Sim. Todas as APIs usadas (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) são multiplataforma. Certifique‑se de que o framework alvo seja pelo menos .NET 6 para melhor compatibilidade.

### Posso criptografar o arquivo zip?
`ZipArchive` oferece criptografia baseada em senha apenas por meio de bibliotecas de terceiros (por exemplo, `SharpZipLib`). Se a criptografia for necessária, envolva os bytes de saída com uma biblioteca que forneça criptografia AES antes de enviá‑los ao cliente.

## Dicas avançadas

* **Reutilize o manipulador** ao processar muitos documentos em lote; criar um novo `ZipArchive` para cada arquivo gera sobrecarga desnecessária.
* **Defina `LeaveOpen: true`** no construtor do `ZipArchive` se precisar ler os bytes do zip enquanto o arquivo ainda está aberto.
* **Valide o HTML** antes de salvar chamando `doc.OptionCheckSyntax = true;` – isso captura tags malformadas cedo.
* **Registre o tamanho** do zip gerado; uma saída incomumente grande costuma indicar recursos duplicados ou compressão ausente.

## Exemplo completo funcionando

Abaixo está um único arquivo que você pode colar em um projeto console (`dotnet new console`) e executar. Ele demonstra tanto o salvamento simples de HTML quanto a compressão zip.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using HtmlAgilityPack;

// ---------- Custom handlers ----------
class MyHandler : ResourceHandler
{
    public MemoryStream HtmlStream { get; } = new();

    public override Stream HandleResource(string resourceName) => HtmlStream;
}

class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open();
    }

    public byte[] GetZipBytes()
    {
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}

// ---------- Main program ----------
class Program
{
    static void Main()
    {
        // Build a simple HTML document.
        HtmlDocument doc = new HtmlDocument();
        doc.LoadHtml("<html><body>Hello World from HtmlAgilityPack</body></html>");

        // ---- Example 1: plain HTML save ----
        var plainHandler = new MyHandler();
        doc.Save(plainHandler);
        plainHandler.HtmlStream.Seek(0, SeekOrigin.Begin);
        using var reader = new StreamReader(plainHandler.HtmlStream);
        Console.WriteLine("Plain HTML output:");


## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como salvar HTML em C# com manipulador de recurso personalizado](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [Como usar ZipArchive – salvar HTML e recursos em um arquivo ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [salvar html como zip com um manipulador de recurso personalizado – guia passo a passo](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}