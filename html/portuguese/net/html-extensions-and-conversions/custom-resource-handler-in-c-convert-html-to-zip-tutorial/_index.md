---
category: general
date: 2026-02-10
description: O manipulador de recursos personalizado permite converter HTML em ZIP
  em C#. Aprenda como salvar HTML como zip e transmitir recursos HTML de forma eficiente.
draft: false
keywords:
- custom resource handler
- convert html to zip
- save html as zip
- create zip with html
- stream html resources
language: pt
og_description: Manipulador de recurso personalizado permite converter HTML em ZIP
  em C#. Siga este guia passo a passo para salvar HTML como zip e transmitir recursos
  HTML.
og_title: Manipulador de Recurso Personalizado em C# – Converter HTML para ZIP
tags:
- Aspose.HTML
- C#
- ZIP archive
- file streaming
title: Manipulador de Recurso Personalizado em C# – Tutorial de Conversão de HTML
  para ZIP
url: /pt/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Manipulador de Recurso Personalizado – Converter HTML para ZIP em C#

Já se perguntou como **personalizar o manipulador de recursos** para transformar HTML bruto diretamente em um arquivo ZIP? Você não está sozinho. Muitos desenvolvedores encontram um obstáculo quando precisam agrupar uma página HTML com seus recursos sem sujar o disco com arquivos temporários. A boa notícia? Com Aspose.HTML você pode fazer tudo na memória, e o truque está em um manipulador de recurso personalizado.

Neste tutorial vamos percorrer um exemplo completo e executável que mostra como **converter HTML para ZIP**, **salvar HTML como ZIP** e **transmitir recursos HTML** em tempo real. Ao final, você terá um único método que recebe uma string de HTML e gera um `result.zip` pronto para download contendo a página e todos os recursos vinculados.

> **Pré‑requisitos** – .NET 6+ (ou .NET Framework 4.6+), Aspose.HTML for .NET instalado e compreensão básica de streams. Nenhuma ferramenta externa necessária.

---

## Manipulador de Recurso Personalizado – Conceito Central

Um *resource handler* no Aspose.HTML é um objeto que decide **onde** cada parte de um documento será armazenada — seja um arquivo no disco, um buffer de memória ou, como mostraremos, uma entrada dentro de um arquivo ZIP. Ao estender `ResourceHandler` você obtém controle total sobre o destino de saída para o arquivo HTML principal **e** todos os recursos auxiliares (CSS, imagens, fontes, etc.).

Pense nele como um agente de trânsito para os ativos do seu documento: o método `HandleResource` fornece um `Stream` para o HTML principal, enquanto o evento `ResourceSaving` permite interceptar cada arquivo dependente imediatamente antes de ser gravado.

---

## Etapa 1: Implementar um Manipulador de Recurso Personalizado

Primeiro, crie uma classe que herde de `ResourceHandler`. Vamos sobrescrever `HandleResource` para fornecer ao Aspose um novo `MemoryStream` para a saída do HTML principal. Para os ativos vinculados, conectaremos ao `ResourceSaving` mais adiante.

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using System.IO;

/// <summary>
/// Supplies a stream for every resource the HTML document needs to save.
/// </summary>
class MyHandler : ResourceHandler
{
    /// <summary>
    /// Returns a new stream for the main HTML content.
    /// </summary>
    public override Stream HandleResource(ResourceInfo info)
    {
        // In real life you might return a FileStream or a ZipEntry stream.
        // Here we just hand back a clean MemoryStream.
        return new MemoryStream();
    }
}
```

**Por que isso importa:** Retornar um novo `MemoryStream` significa que o HTML nunca toca o sistema de arquivos. Essa é a base para a criação limpa de um ZIP totalmente em memória posteriormente.

---

## Etapa 2: Salvar HTML em um único MemoryStream

Agora que temos um manipulador, podemos gerar um documento HTML e capturá‑lo inteiramente na memória. Esta etapa é opcional se você precisar apenas do ZIP, mas ilustra como o manipulador funciona isoladamente.

```csharp
using Aspose.Html;

// Sample HTML – replace with your own markup or load from a file.
string htmlContent = "<html><head><title>Demo</title></head><body>Hello world!</body></html>";

// Create the document from a string.
HTMLDocument htmlDocument = new HTMLDocument(htmlContent);

// Instantiate our custom handler.
MyHandler memoryHandler = new MyHandler();

using (MemoryStream htmlStream = new MemoryStream())
{
    // Save triggers HandleResource and writes the HTML into htmlStream.
    htmlDocument.Save(htmlStream, memoryHandler);

    // Reset position for potential reading.
    htmlStream.Position = 0;

    // For demo purposes, dump the HTML to console.
    using (StreamReader reader = new StreamReader(htmlStream))
    {
        Console.WriteLine("Generated HTML:");
        Console.WriteLine(reader.ReadToEnd());
    }
}
```

**Saída esperada** (formatada para legibilidade):

```
Generated HTML:
<html><head><title>Demo</title></head><body>Hello world!</body></html>
```

Se você executar este trecho verá que o HTML vive apenas na RAM — nenhum arquivo temporário é criado.

---

## Etapa 3: Empacotar HTML e Recursos em um Arquivo ZIP

Chegou a parte mais interessante: agrupar o HTML **e** todos os recursos referenciados em um arquivo ZIP sem jamais gravar arquivos intermediários no disco. Usaremos `System.IO.Compression.ZipArchive` junto com o evento `ResourceSaving`.

```csharp
using Aspose.Html;
using System.IO;
using System.IO.Compression;

// Re‑use the same HTMLDocument from the previous step.
HTMLDocument htmlDocument = new HTMLDocument("<html><body>Hello world!</body></html>");

// Path where the final ZIP will be written.
string zipPath = Path.Combine(Environment.CurrentDirectory, "result.zip");

// Open a FileStream for the ZIP file.
using (FileStream zipFile = new FileStream(zipPath, FileMode.Create))
using (ZipArchive zipArchive = new ZipArchive(zipFile, ZipArchiveMode.Update))
{
    // Create a fresh handler for the ZIP operation.
    MyHandler zipHandler = new MyHandler();

    // Hook the ResourceSaving event – this fires for every resource.
    zipHandler.ResourceSaving += (sender, e) =>
    {
        // Ensure we don't create leading folder entries like "/css/style.css".
        string entryName = e.ResourceInfo.Path.TrimStart('/');

        // Create a new entry inside the ZIP.
        ZipArchiveEntry entry = zipArchive.CreateEntry(entryName);

        // Provide the stream that Aspose will write into.
        e.Stream = entry.Open();
    };

    // Save the document; the handler will fill the ZIP for us.
    htmlDocument.Save(zipHandler);
}

// Verify the ZIP exists.
Console.WriteLine($"ZIP created at: {zipPath}");
```

### O que acontece nos bastidores?

1. **`ResourceSaving` é disparado** para o arquivo HTML principal e cada recurso vinculado.
2. Nossa lambda cria uma entrada correspondente (`CreateEntry`) dentro do ZIP aberto.
3. Ao atribuir `e.Stream = entry.Open()`, entregamos ao Aspose um stream gravável que escreve diretamente na entrada do ZIP.
4. Quando `htmlDocument.Save` termina, o ZIP contém uma página HTML totalmente formada mais qualquer CSS, imagens ou fontes referenciadas pelo markup.

**Resultado:** Um único arquivo `result.zip` que você pode servir a navegadores, anexar a e‑mails ou armazenar em blob storage — sem arquivos temporários deixados para trás.

---

## Bônus: Usando o ZIP em uma Web API

Se você está construindo um endpoint ASP.NET Core que devolve o ZIP sob demanda, a mesma lógica se aplica. Aqui está uma ação de controlador compacta:

```csharp
[ApiController]
[Route("api/[controller]")]
public class HtmlZipController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult DownloadZip()
    {
        // Build the document (could be loaded from a DB, etc.).
        var html = "<html><body><h1>Dynamic report</h1></body></html>";
        var doc = new HTMLDocument(html);
        var handler = new MyHandler();

        // Prepare an in‑memory ZIP.
        using var zipStream = new MemoryStream();
        using (var archive = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            handler.ResourceSaving += (s, e) =>
            {
                var entry = archive.CreateEntry(e.ResourceInfo.Path.TrimStart('/'));
                e.Stream = entry.Open();
            };
            doc.Save(handler);
        }

        zipStream.Position = 0;
        return File(zipStream, "application/zip", "report.zip");
    }
}
```

Agora uma requisição GET para `/api/HtmlZip/download` transmite o ZIP gerado diretamente ao cliente — perfeito para relatórios gerados em tempo real.

---

## Armadilhas Comuns & Dicas Profissionais

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **Pastas vazias no ZIP** | `ResourceInfo.Path` começa com `/`, gerando uma entrada como `/` | Use `TrimStart('/')` como mostrado no manipulador de evento. |
| **Imagens ausentes** | Imagens referenciadas com URLs absolutas não são buscadas automaticamente | Defina `htmlDocument.Options.ResourceLoading = ResourceLoadingMode.Stream` e forneça um `ResourceHandler` personalizado que faça download dos ativos remotos. |
| **Arquivos grandes causam pressão de memória** | Todos os streams são mantidos na memória até o ZIP ser fechado | Troque `ZipArchiveMode.Update` por `Create` e escreva cada entrada diretamente sem buffer, ou faça streaming a partir do disco se o tamanho exceder a RAM. |
| **Exceção “The stream does not support seeking”** | Tentativa de reutilizar um stream não buscável para múltiplos recursos | Sempre forneça um novo `MemoryStream` ou `entry.Open()` para cada recurso. |

---

## Conclusão

Acabamos de demonstrar como um **manipulador de recurso personalizado** permite **converter HTML para ZIP**, **salvar HTML como ZIP** e **transmitir recursos HTML** sem tocar o sistema de arquivos. Ao sobrescrever `HandleResource` e aproveitar o `ResourceSaving`, você obtém controle granular sobre cada byte que sai do Aspose.HTML.

O padrão escala: troque o `MemoryStream` em memória por um stream de blob na nuvem, adicione configurações de compressão ou insira uma camada de logging para auditar quais ativos são empacotados. O céu é o limite quando você domina o pipeline de recursos.

Pronto para o próximo passo? Experimente incorporar CSS e imagens no seu HTML, teste o carregamento de recursos remotos ou integre esse fluxo em uma Azure Function que devolve um ZIP sob demanda. Feliz codificação!

--- 

*Imagem ilustrando o fluxo de um manipulador de recurso personalizado transformando HTML em um arquivo ZIP.*

![fluxo do manipulador de recurso personalizado](https://example.com/placeholder-image.png "fluxo do manipulador de recurso personalizado")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}