---
category: general
date: 2026-11-14
description: Criar PNG a partir de HTML em C# usando Aspose.HTML – um guia passo a
  passo para renderizar HTML em PNG, converter HTML em imagem e salvar HTML como PNG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PNG from HTML
- render HTML to PNG
- convert HTML to image
- save HTML as PNG
- render HTML to image
language: pt
lastmod: 2026-11-14
og_description: Crie PNG a partir de HTML em C# com Aspose.HTML. Aprenda como renderizar
  HTML para PNG, converter HTML em imagem e salvar HTML como PNG em alguns passos
  simples.
og_image_alt: Diagram illustrating create PNG from HTML workflow using Aspose.HTML
  in C#
og_title: Criar PNG a partir de HTML em C# – tutorial completo do Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-11-14'
  description: Create PNG from HTML in C# using Aspose.HTML – a step‑by‑step guide
    to render HTML to PNG, convert HTML to image, and save HTML as PNG.
  headline: How to create PNG from HTML in C# with Aspose.HTML
  type: TechArticle
- description: Create PNG from HTML in C# using Aspose.HTML – a step‑by‑step guide
    to render HTML to PNG, convert HTML to image, and save HTML as PNG.
  name: How to create PNG from HTML in C# with Aspose.HTML
  steps:
  - name: Prerequisites
    text: '* .NET 6.0 SDK or later (the code also works with .NET Core 3.1 and .NET
      Framework 4.7+). * Visual Studio 2022 or any IDE that supports C#. * Basic familiarity
      with C# async/await is helpful but not required.'
  - name: Install Aspose.HTML
    text: 'Open a terminal in your project folder and run:'
  - name: Create a custom resource handler (optional but recommended)
    text: 'When the HTML references external assets (e.g., `logo.png`, CSS files,
      web fonts), Aspose.HTML asks a `ResourceHandler` for a stream. By providing
      our own handler we can:'
  - name: Build the HTML document
    text: You can load HTML from a string, a URL, or a file. For simplicity the tutorial
      uses an inline string that contains an image placeholder.
  - name: Configure image save options
    text: '`ImageSaveOptions` tells Aspose.HTML what raster format to produce and
      which `ResourceHandler` to use.'
  - name: Render the HTML to PNG
    text: The `RenderToImage` method performs the actual conversion. It takes a file
      path and the options defined above.
  - name: Verify the result
    text: Open the generated PNG with any image viewer. You should see the heading
      “Hello, Aspose.HTML!” and a blank placeholder where `logo.png` would appear
      (because our handler returns an empty stream). To **convert HTML to image**
      with the real logo, replace `MyHandler` with a version that loads the actua
  - name: Extending the solution (optional)
    text: Extending the solution (optional)
  type: HowTo
tags:
- Aspose.HTML
- C#
- Image rendering
title: Como criar PNG a partir de HTML em C# com Aspose.HTML
url: /pt/net/generate-jpg-and-png-images/how-to-create-png-from-html-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar PNG a partir de HTML em C# com Aspose.HTML

Se você precisa **criar PNG a partir de HTML** em uma aplicação .NET, este guia mostra os passos exatos. Você aprenderá como **renderizar HTML para PNG**, lidar com recursos externos e **salvar HTML como PNG** sem sair do ambiente C#.

O exemplo usa Aspose.HTML 5.x, uma biblioteca totalmente gerenciada que renderiza HTML, CSS e SVG em imagens raster. Nenhum navegador externo ou dependências nativas são necessárias, tornando a solução ideal para geração de imagens no lado do servidor, criação de miniaturas de e‑mail ou pré‑processamento de PDF.

## O que você irá alcançar

* Configurar um projeto C# com o pacote NuGet Aspose.HTML.  
* Implementar um `ResourceHandler` personalizado para controlar como imagens, CSS e fontes são obtidas.  
* **Renderizar HTML para PNG** usando `ImageSaveOptions`.  
* Verificar o arquivo de saída e entender como **converter HTML em imagem** em outros formatos.

### Pré-requisitos

* .NET 6.0 SDK ou posterior (o código também funciona com .NET Core 3.1 e .NET Framework 4.7+).  
* Visual Studio 2022 ou qualquer IDE que suporte C#.  
* Familiaridade básica com async/await em C# é útil, mas não obrigatória.

> **Dica profissional:** Aspose.HTML é licenciado por desenvolvedor ou por servidor. Para avaliação, você pode usar uma chave de licença temporária; a biblioteca funciona em modo de avaliação com uma marca d'água na imagem renderizada.

## Como criar PNG a partir de HTML com Aspose.HTML

O núcleo da solução está em três pequenas classes: um `ResourceHandler` personalizado, um método que cria o `HTMLDocument` e a chamada de renderização que **salva HTML como PNG**. As seções a seguir explicam cada parte.

### Etapa 1: Instalar Aspose.HTML

Abra um terminal na pasta do seu projeto e execute:

```bash
dotnet add package Aspose.Html
```

O pacote inclui `Aspose.Html`, `Aspose.Html.Rendering` e `Aspose.Html.Rendering.Image`, que são necessários para a saída de imagem.

### Etapa 2: Criar um manipulador de recursos personalizado (opcional, mas recomendado)

Quando o HTML referencia recursos externos (por exemplo, `logo.png`, arquivos CSS, fontes web), o Aspose.HTML solicita um `ResourceHandler` por um stream. Ao fornecer nosso próprio manipulador, podemos:

* Registrar cada URL solicitada.  
* Redirecionar recursos para uma CDN ou um cache em memória.  
* Prevenir chamadas de rede em ambientes isolados.

```csharp
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

/// <summary>
/// Supplies a stream for each external resource referenced by the HTML.
/// </summary>
class MyHandler : ResourceHandler
{
    /// <summary>
    /// Returns a <see cref="Stream"/> that Aspose.HTML will read from.
    /// </summary>
    /// <param name="info">Information about the requested resource.</param>
    /// <returns>A writable <see cref="MemoryStream"/>.</returns>
    public override Stream HandleResource(ResourceInfo info)
    {
        // For demonstration we return an empty MemoryStream.
        // In production you could download the resource, read it from disk,
        // or generate it on the fly.
        return new MemoryStream();
    }
}
```

**Por que usar um manipulador personalizado?**  
Se o HTML contém um `<img src="logo.png">`, o manipulador padrão tentará ler `logo.png` do sistema de arquivos relativo ao diretório de trabalho atual. Em serviços nativos da nuvem, o sistema de arquivos pode ser somente leitura, portanto o manipulador personalizado permite que você controle a origem de cada recurso.

### Etapa 3: Construir o documento HTML

Você pode carregar HTML a partir de uma string, URL ou arquivo. Para simplificar, o tutorial usa uma string embutida que contém um placeholder de imagem.

```csharp
// Build a simple HTML document with an image reference.
string markup = @"
<html>
  <head>
    <style>
      body { font-family: Arial, sans-serif; background:#f8f8f8; }
      img { width:150px; height:auto; }
    </style>
  </head>
  <body>
    <h1>Hello, Aspose.HTML!</h1>
    <img src='logo.png' alt='Company logo'>
  </body>
</html>";

HTMLDocument html = new HTMLDocument(markup);
```

Se você já possui um arquivo HTML, substitua o construtor por `new HTMLDocument("path/to/file.html")`.

### Etapa 4: Configurar opções de salvamento de imagem

`ImageSaveOptions` informa ao Aspose.HTML qual formato raster produzir e qual `ResourceHandler` usar.

```csharp
// Choose PNG as the output format.
ImageSaveOptions options = new ImageSaveOptions(SaveFormat.Png)
{
    // Attach the custom handler defined in Step 2.
    ResourceHandler = new MyHandler(),

    // Optional: control the image size and background.
    Width = 1024,               // Width in pixels.
    Height = 768,               // Height in pixels.
    BackgroundColor = System.Drawing.Color.White
};
```

Você também pode definir `Resolution`, `PageNumber` ou `PageCount` para renderizar páginas específicas quando a fonte é um documento HTML com múltiplos frames.

### Etapa 5: Renderizar o HTML para PNG

O método `RenderToImage` realiza a conversão real. Ele recebe um caminho de arquivo e as opções definidas acima.

```csharp
// Render the HTML document to a PNG file.
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.png");
html.RenderToImage(outputPath, options);

// Inform the user.
Console.WriteLine($"HTML has been rendered to PNG at: {outputPath}");
```

Quando o método termina, `output.png` contém uma captura raster do markup, incluindo quaisquer imagens que o `MyHandler` forneceu.

### Etapa 6: Verificar o resultado

Abra o PNG gerado com qualquer visualizador de imagens. Você deve ver o título “Hello, Aspose.HTML!” e um placeholder em branco onde `logo.png` apareceria (porque nosso manipulador retorna um stream vazio). Para **converter HTML em imagem** com o logotipo real, substitua `MyHandler` por uma versão que carregue o arquivo real:

```csharp
public override Stream HandleResource(ResourceInfo info)
{
    if (info.Uri.EndsWith("logo.png", StringComparison.OrdinalIgnoreCase))
    {
        // Load the real logo from disk.
        return File.OpenRead(@"C:\Images\logo.png");
    }
    // Fallback for other resources.
    return base.HandleResource(info);
}
```

Execute o programa novamente e o logotipo aparecerá no PNG de saída.

### Etapa 7: Estendendo a solução (opcional)

#### Renderizar HTML para outros formatos de imagem
Para **renderizar HTML em imagem** em JPEG, BMP ou TIFF, basta alterar o `SaveFormat`:

```csharp
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.Jpeg);
html.RenderToImage("output.jpg", jpegOptions);
```

#### Gerar múltiplas páginas
Se seu HTML contém quebras de página (`<div style="page-break-after:always;">`), você pode renderizar cada página separadamente:

```csharp
for (int i = 0; i < html.PageCount; i++)
{
    options.PageNumber = i + 1; // 1‑based index
    string pagePath = $"output_page_{i + 1}.png";
    html.RenderToImage(pagePath, options);
}
```

#### Usar renderização assíncrona para serviços de alta taxa de transferência
Aspose.HTML também oferece uma API assíncrona:

```csharp
await html.RenderToImageAsync(outputPath, options);
```

Isso é útil quando a renderização ocorre dentro de um endpoint ASP.NET Core que precisa permanecer responsivo.

## Exemplo completo e executável

Abaixo está um aplicativo console autônomo que reúne todas as peças. Copie o código para um novo projeto console .NET e execute‑o.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

namespace HtmlToPngDemo
{
    /// <summary>
    /// Supplies a stream for each external resource referenced by the HTML.
    /// </summary>
    class MyHandler : ResourceHandler
    {
        public override Stream HandleResource(ResourceInfo info)
        {
            // Load the real logo if the request is for "logo.png".
            if (info.Uri.EndsWith("logo.png", StringComparison.OrdinalIgnoreCase))
            {
                // Adjust the path to where your logo actually lives.
                string logoPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "logo.png");
                return File.OpenRead(logoPath);
            }

            // For any other resource return an empty stream.
            return new MemoryStream();
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Build the HTML markup.
            string markup = @"
            <html>
              <head>
                <style>
                  body { font-family: Arial, sans-serif; background:#f8f8f8; }
                  img { width:150px; height:auto; }
                </style>
              </head>
              <body>
                <h1>Hello, Aspose.HTML!</h1>
                <img src='logo.png' alt='Company logo'>
              </body>
            </html>";

            // 2️⃣ Create the HTML document object.
            HTMLDocument html = new HTMLDocument(markup);

            // 3️⃣ Configure PNG output options.
            ImageSaveOptions options = new ImageSaveOptions(SaveFormat.Png)
            {
                Width = 1024,
                Height = 768,
                BackgroundColor = System.Drawing.Color.White,
                ResourceHandler = new MyHandler()
            };

            // 4️⃣ Render the document to a PNG file.
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.png");
            html.RenderToImage(outputPath, options);

            Console.WriteLine($"✅ HTML successfully rendered to PNG at: {outputPath}");
        }
    }
}
```

**Saída esperada:**  
Um arquivo chamado `output.png` (≈ 1024 × 768 px) aparece no diretório de trabalho do programa. A imagem contém o título e

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar PNG a partir de HTML com Aspose.HTML – Guia completo passo a passo](/html/english/net/generate-jpg-and-png-images/create-png-from-html-with-aspose-html-full-step-by-step-guid/)
- [Criar documento HTML e renderizar HTML para PNG – Guia completo C#](/html/english/net/rendering-html-documents/create-html-document-and-render-html-to-png-full-c-guide/)
- [Como usar Aspose para renderizar HTML para PNG – Guia passo a passo](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}