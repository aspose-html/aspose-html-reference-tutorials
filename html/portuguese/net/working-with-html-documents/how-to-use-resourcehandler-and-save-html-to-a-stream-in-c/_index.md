---
category: general
date: 2026-10-25
description: Como usar ResourceHandler para controlar o carregamento de recursos e
  como salvar HTML em um fluxo usando Aspose.HTML em C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use resourcehandler
- how to save html to stream
- Aspose.HTML ResourceHandler
- HTML to MemoryStream C#
- custom resource handling C#
language: pt
lastmod: 2026-10-25
og_description: Como usar ResourceHandler para controlar o carregamento de recursos
  e como salvar HTML em um stream com Aspose.HTML para .NET.
og_image_alt: Screenshot of C# code using ResourceHandler to save HTML to a memory
  stream
og_title: Como usar ResourceHandler e salvar HTML em um stream em C#
schemas:
- author: Aspose
  dateModified: '2026-10-25'
  description: How to use ResourceHandler to control resource loading and how to save
    HTML to a stream using Aspose.HTML in C#.
  headline: How to use ResourceHandler and save HTML to a stream in C#
  type: TechArticle
- description: How to use ResourceHandler to control resource loading and how to save
    HTML to a stream using Aspose.HTML in C#.
  name: How to use ResourceHandler and save HTML to a stream in C#
  steps:
  - name: Expected output
    text: 'Running the code above prints:'
  - name: 1. Embedding real resources
    text: 'If you need to embed an image, modify `MyHandler` to return a stream that
      contains the image bytes:'
  - name: 2. Handling large documents
    text: For very large HTML files, consider using `BufferedStream` or writing directly
      to a file‑based `FileStream` if memory becomes a bottleneck. The pattern for
      **how to save HTML to a stream** stays the same; only the stream type changes.
  - name: 3. Thread safety
    text: '`ResourceHandler` instances are **not** guaranteed to be thread‑safe. If
      you plan to reuse a handler across parallel conversions, either:'
  - name: 4. Disposing resources
    text: Both `HTMLDocument` and any streams you create implement `IDisposable`.
      Wrapping them in `using` blocks, as shown in Step 4, guarantees clean release
      of unmanaged resources.
  - name: What’s next?
    text: '* **Embed real images or CSS** by extending `MyHandler` (see the “Embedding
      real resources” section). * **Convert the stream to PDF** with `HtmlConverter.ConvertHtml`
      if you need a printable version. * **Stream the result directly from a Web API**
      using `FileStreamResult` or `MemoryStream` in ASP.NE'
  type: HowTo
tags:
- Aspose.HTML
- C#
- Stream handling
title: Como usar ResourceHandler e salvar HTML em um stream em C#
url: /pt/net/working-with-html-documents/how-to-use-resourcehandler-and-save-html-to-a-stream-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar ResourceHandler e salvar HTML em um stream em C#

Se você precisa **como usar ResourceHandler** ao renderizar HTML com Aspose.HTML, este guia mostra uma solução completa, pronta‑para‑executar. Você também aprenderá **como salvar HTML em um stream** para que possa transmitir a saída sem tocar no sistema de arquivos.

Trabalhar com HTML na memória é comum quando você gera e‑mails, respostas de API ou PDFs sob demanda. Ao final deste tutorial, você terá um programa C# autônomo que cria um `HTMLDocument`, fornece um `ResourceHandler` personalizado e grava o resultado em um `MemoryStream`.

## Pré-requisitos

* .NET 6.0 ou posterior (o código também funciona com .NET Core 3.1 e .NET Framework 4.7+)
* O pacote NuGet **Aspose.HTML for .NET**  
  ```bash
  dotnet add package Aspose.HTML
  ```
* Um entendimento básico de C# async/await (opcional, mas útil)

## O que o tutorial cobre

* Como **como usar ResourceHandler** para interceptar solicitações de imagem, CSS ou script
* Como configurar `HtmlSaveOptions` com um manipulador personalizado
* Como **como salvar HTML em um stream** usando `MemoryStream`
* Tratamento de casos de borda, como recursos ausentes e descarte de stream
* Dicas para estender o manipulador para incorporar recursos reais posteriormente

## Etapa 1: Criar um documento HTML simples a partir de uma string

O primeiro passo é instanciar um `HTMLDocument` a partir de HTML bruto. Este objeto representa a árvore DOM que o Aspose.HTML renderizará.

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using System.IO;

// Simple HTML markup – you can replace this with any valid HTML string.
string htmlContent = "<html><body>Hello World</body></html>";

// The HTMLDocument constructor parses the string into a DOM.
HTMLDocument document = new HTMLDocument(htmlContent);
```

> **Por que isso importa:** Criar o documento a partir de uma string mantém todo o fluxo de trabalho na memória, o que é essencial quando você posteriormente **como salvar HTML em um stream** sem tocar no disco.

## Etapa 2: Implementar um ResourceHandler personalizado

`ResourceHandler` é o ponto de extensão que o Aspose.HTML usa sempre que precisa de um recurso externo (imagens, CSS, fontes, etc.). Ao sobrescrever `HandleResource`, você decide qual stream retornar para cada solicitação.

```csharp
// Define a handler that supplies an empty stream for every resource request.
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(Resource resource)
    {
        // Returning an empty MemoryStream effectively disables external resources.
        // You could return a real image stream here if you need to embed assets.
        return new MemoryStream();
    }
}

// Instantiate the handler so it can be attached to the save options.
MyHandler customHandler = new MyHandler();
```

> **Por que você pode precisar disso:** Ao gerar HTML para e‑mail ou respostas de API, muitas vezes você não deseja chamadas externas. Fornecer streams vazios impede erros 404 e acelera a renderização. Isso demonstra **como usar ResourceHandler** para uma saída “sem recursos”.

## Etapa 3: Configurar HtmlSaveOptions para usar o manipulador personalizado

`HtmlSaveOptions` permite controlar o processo de salvamento. Atribua a propriedade `ResourceHandler` à sua implementação personalizada.

```csharp
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // Attach the handler so every resource request goes through MyHandler.
    ResourceHandler = customHandler
};
```

> **Dica:** Se mais tarde precisar incorporar CSS ou imagens, substitua `MyHandler` por uma versão que retorne os streams apropriados com base em `resource.Uri`.

## Etapa 4: Salvar o documento em um MemoryStream

Agora você tem tudo pronto para **como salvar HTML em um stream**. Usar um `MemoryStream` mantém a saída na RAM, facilitando o envio via HTTP, o armazenamento em um banco de dados ou a passagem para outra API.

```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    // The Save method writes the HTML (and any referenced resources) into the stream.
    document.Save(outputStream, saveOptions);

    // Reset the position so callers can read from the beginning.
    outputStream.Position = 0;

    // Example: Convert the stream to a string for debugging.
    using (StreamReader reader = new StreamReader(outputStream))
    {
        string resultHtml = reader.ReadToEnd();
        System.Console.WriteLine(resultHtml);
    }

    // At this point, outputStream can be returned from a web API, attached to an email,
    // or passed to another component without ever touching the file system.
}
```

### Saída esperada

Executar o código acima imprime:

```html
<html><head></head><body>Hello World</body></html>
```

Como o manipulador personalizado retorna streams vazios, nenhuma tag `<link>` ou `<img>` externa é resolvida, e o HTML permanece limpo.

## Variações comuns e casos de borda

### 1. Incorporando recursos reais

Se precisar incorporar uma imagem, modifique `MyHandler` para retornar um stream que contenha os bytes da imagem:

```csharp
public override Stream HandleResource(Resource resource)
{
    if (resource.Uri.EndsWith(".png"))
    {
        // Load the PNG from embedded resources or a database.
        byte[] imageBytes = File.ReadAllBytes("logo.png");
        return new MemoryStream(imageBytes);
    }
    return new MemoryStream(); // Fallback for other resources.
}
```

### 2. Manipulando documentos grandes

Para arquivos HTML muito grandes, considere usar `BufferedStream` ou gravar diretamente em um `FileStream` baseado em arquivo se a memória se tornar um gargalo. O padrão para **como salvar HTML em um stream** permanece o mesmo; apenas o tipo de stream muda.

### 3. Segurança de thread

Instâncias de `ResourceHandler` **não** são garantidas como thread‑safe. Se você planeja reutilizar um manipulador em conversões paralelas, faça uma das opções:

* Crie um novo manipulador por conversão, ou
* Proteja o estado compartilhado dentro de `HandleResource` com bloqueios.

### 4. Liberando recursos

Tanto `HTMLDocument` quanto quaisquer streams que você criar implementam `IDisposable`. Envolvê-los em blocos `using`, como mostrado na Etapa 4, garante a liberação limpa de recursos não gerenciados.

## Dica profissional: Reutilizar o mesmo MemoryStream

Se precisar concatenar várias saídas HTML em um único stream, redefina a posição antes de cada chamada `Save`:

```csharp
outputStream.Position = 0; // Clear previous content
document.Save(outputStream, saveOptions);
```

Alternativamente, crie um novo `MemoryStream` para cada conversão para evitar mistura acidental de dados.

## Exemplo completo em funcionamento

Abaixo está o programa completo que você pode copiar‑colar em uma aplicação console. Ele compila com .NET 6.0 e Aspose.HTML 23.9 (ou posterior).

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using System;
using System.IO;

namespace ResourceHandlerDemo
{
    // Custom handler that supplies empty streams for any requested resource.
    class MyHandler : ResourceHandler
    {
        public override Stream HandleResource(Resource resource)
        {
            // Return an empty stream to suppress external resources.
            return new MemoryStream();
        }
    }

    class Program
    {
        static void Main()
        {
            // Step 1: Create the HTML document.
            string htmlContent = "<html><body>Hello World</body></html>";
            HTMLDocument document = new HTMLDocument(htmlContent);

            // Step 2: Attach the custom ResourceHandler.
            MyHandler customHandler = new MyHandler();

            // Step 3: Configure save options.
            HtmlSaveOptions saveOptions = new HtmlSaveOptions
            {
                ResourceHandler = customHandler
            };

            // Step 4: Save to a MemoryStream.
            using (MemoryStream outputStream = new MemoryStream())
            {
                document.Save(outputStream, saveOptions);
                outputStream.Position = 0;

                // Display the generated HTML for verification.
                using (StreamReader reader = new StreamReader(outputStream))
                {
                    string resultHtml = reader.ReadToEnd();
                    Console.WriteLine("Generated HTML:");
                    Console.WriteLine(resultHtml);
                }
            }
        }
    }
}
```

Execute o programa e você verá o HTML gerado impresso no console, confirmando que **como usar ResourceHandler** e **como salvar HTML em um stream** funcionam juntos perfeitamente.

## Conclusão

Este tutorial demonstrou **como usar ResourceHandler** para controlar o carregamento de recursos externos e os passos exatos **como salvar HTML em um stream** usando Aspose.HTML em C#. Agora você tem um padrão reutilizável para geração de HTML em memória, ideal para APIs web, modelagem de e‑mail e pipelines de conversão para PDF.

### O que vem a seguir?

* **Incorporar imagens ou CSS reais** estendendo `MyHandler` (veja a seção “Incorporando recursos reais”).
* **Converter o stream para PDF** com `HtmlConverter.ConvertHtml` se precisar de uma versão imprimível.
* **Transmitir o resultado diretamente de uma Web API** usando `FileStreamResult` ou `MemoryStream` no ASP.NET

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como salvar HTML em C# – Guia completo usando um manipulador de recursos personalizado](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Como salvar HTML em C# com manipulador de recursos personalizado](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [como usar manipulador no Aspose.HTML – Carregar HTML, salvar como ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-handler-in-aspose-html-load-html-save-as-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}