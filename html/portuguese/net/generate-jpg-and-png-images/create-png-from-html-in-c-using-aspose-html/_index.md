---
category: general
date: 2026-08-12
description: Crie PNG a partir de HTML em C# com Aspose.HTML. Aprenda como converter
  HTML para PNG e renderizar HTML como imagem em apenas algumas linhas de código.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from html
- convert html to png
- render html as image
- how to render html to image
language: pt
lastmod: 2026-08-12
og_description: Crie PNG a partir de HTML em C# usando Aspose.HTML. Este guia mostra
  como renderizar HTML como imagem rapidamente, abordando opções de conversão, configuração
  de código e solução de problemas.
og_image_alt: Screenshot of a C# program converting HTML to a PNG image
og_title: Criar PNG a partir de HTML em C# – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Create PNG from HTML in C# with Aspose.HTML. Learn how to convert HTML
    to PNG and render HTML as image in just a few lines of code.
  headline: Create PNG from HTML in C# using Aspose.HTML
  type: TechArticle
- description: Create PNG from HTML in C# with Aspose.HTML. Learn how to convert HTML
    to PNG and render HTML as image in just a few lines of code.
  name: Create PNG from HTML in C# using Aspose.HTML
  steps:
  - name: Why this works
    text: '- **`HtmlDocument.Open`** parses the HTML string into a DOM that Aspose.HTML
      can render. - **`ImageRenderingOptions`** lets you control anti‑aliasing, text
      hinting, and font handling, which are essential when you **render HTML as image**
      to avoid blurry text. - **`ImageConverter.ConvertHtmlToImage`*'
  - name: 1. Preparing the HTML source
    text: You can load HTML from a string (as shown), a local file, or a remote URL.
  - name: 2. Fine‑tuning rendering options
    text: '| Option | Effect | When to adjust | |--------|--------|----------------|
      | `UseAntialiasing` | Reduces jagged edges on vector graphics | Always enable
      for high‑quality output | | `TextOptions.UseHinting` | Sharpens glyph edges
      | Important for small font sizes | | `FontOptions.WebFontStyle` | Choose'
  - name: 3. Performing the conversion
    text: The `ImageConverter` overload you used writes a single PNG file. If you
      need multiple pages (e.g., a multi‑page HTML document), use the overload that
      returns a collection of images.
  - name: a. Missing fonts
    text: If the HTML references a custom web font that isn’t installed on the server,
      the rendered text falls back to a default font, which may affect layout.
  - name: b. Large pages and memory consumption
    text: Rendering a very tall page can consume a lot of RAM.
  - name: c. Transparent backgrounds
    text: PNG supports transparency, but the default background is white.
  type: HowTo
tags:
- Aspose.HTML
- C#
- image rendering
- HTML conversion
title: Criar PNG a partir de HTML em C# usando Aspose.HTML
url: /pt/net/generate-jpg-and-png-images/create-png-from-html-in-c-using-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PNG a partir de HTML em C# usando Aspose.HTML

Se você precisa **criar PNG a partir de HTML** em uma aplicação .NET, este guia mostra todo o processo. Você verá como **converter HTML para PNG** com apenas algumas linhas de código C#, usando o poderoso mecanismo de renderização do Aspose.HTML.

Renderizar HTML como imagem é uma necessidade comum ao gerar miniaturas, pré‑visualizações de e‑mail ou relatórios que precisam ser incorporados em PDFs. Nas seções a seguir, você aprenderá os passos exatos, verá um exemplo completo em funcionamento e entenderá por que cada configuração é importante.

## O que você vai aprender

- Como criar um `HtmlDocument` a partir de uma string ou arquivo.  
- Como configurar `ImageRenderingOptions` para melhorar a qualidade.  
- Como **converter HTML para PNG** e salvar o resultado no disco.  
- Dicas para lidar com fontes, páginas grandes e caminhos de saída personalizados.  

**Pré‑requisitos**  
- .NET 6.0 SDK (ou superior) instalado.  
- Uma licença válida do Aspose.HTML for .NET (ou uma chave de avaliação temporária).  
- Familiaridade básica com C# e Visual Studio ou qualquer IDE compatível com .NET.

---

## Criar PNG a partir de HTML com Aspose.HTML

O primeiro passo é configurar o ambiente e referenciar os namespaces necessários do Aspose.HTML.

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;
using Aspose.Html.Converters;

namespace HtmlToPngDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Build the HTML document from a raw string.
            var html = "<html><body><p style='font-weight:bold;'>Bold text</p></body></html>";
            using var document = new HtmlDocument();
            document.Open(html);

            // 2️⃣ Configure rendering options for best visual fidelity.
            var renderOptions = new ImageRenderingOptions
            {
                UseAntialiasing = true,                     // Smooths edges of drawn shapes
                TextOptions = { UseHinting = true },        // Improves glyph clarity
                FontOptions = { WebFontStyle = WebFontStyle.Normal } // Uses standard web‑font style
            };

            // 3️⃣ Convert the HTML document to a PNG file.
            string outputPath = @"output.png";
            ImageConverter.ConvertHtmlToImage(document, outputPath, renderOptions);

            Console.WriteLine($"PNG image created at: {outputPath}");
        }
    }
}
```

### Por que isso funciona

- **`HtmlDocument.Open`** analisa a string HTML em um DOM que o Aspose.HTML pode renderizar.  
- **`ImageRenderingOptions`** permite controlar anti‑aliasing, hinting de texto e tratamento de fontes, essenciais ao **renderizar HTML como imagem** para evitar texto borrado.  
- **`ImageConverter.ConvertHtmlToImage`** faz o trabalho pesado: rasteriza o DOM em um bitmap e grava o arquivo PNG.

Executar o programa gera `output.png` que contém o parágrafo em negrito exatamente como definido na fonte HTML.

---

## Converter HTML para PNG passo a passo

A seguir, um detalhamento mais aprofundado de cada fase. Entender o propósito de cada linha ajuda a adaptar o código para páginas maiores ou mais complexas.

### 1. Preparando a fonte HTML

Você pode carregar HTML a partir de uma string (como mostrado), de um arquivo local ou de uma URL remota.

```csharp
// Load from a file
var document = new HtmlDocument();
document.Open(@"C:\templates\invoice.html");

// Load from a URL (requires internet access)
document.Open("https://example.com/report.html");
```

**Dica:** Ao carregar recursos externos (CSS, imagens), certifique‑se de que a propriedade `BaseUrl` aponta para a pasta correta, de modo que links relativos sejam resolvidos adequadamente.

### 2. Ajustando finamente as opções de renderização

| Opção | Efeito | Quando ajustar |
|--------|--------|----------------|
| `UseAntialiasing` | Reduz bordas serrilhadas em gráficos vetoriais | Sempre habilite para saída de alta qualidade |
| `TextOptions.UseHinting` | Aguça as bordas dos glifos | Importante para tamanhos de fonte pequenos |
| `FontOptions.WebFontStyle` | Escolhe a renderização normal, itálica ou oblíqua de web‑fonts | Use `WebFontStyle.Oblique` para fontes inclinadas |
| `ResolutionX` / `ResolutionY` | DPI da imagem de saída | Aumente para PNGs prontos para impressão (ex.: 300 DPI) |

Exemplo de aumento de DPI:

```csharp
renderOptions.ResolutionX = 300;
renderOptions.ResolutionY = 300;
```

### 3. Executando a conversão

A sobrecarga do `ImageConverter` que você usou grava um único arquivo PNG. Se precisar de várias páginas (ex.: um documento HTML multipágina), use a sobrecarga que retorna uma coleção de imagens.

```csharp
ImageConverter.ConvertHtmlToImages(document, "output_folder", renderOptions);
```

Cada página torna‑se `output_folder/page_0.png`, `page_1.png`, etc.

---

## Renderizar HTML como imagem – lidando com armadilhas comuns

### a. Fontes ausentes

Se o HTML referencia uma web‑font personalizada que não está instalada no servidor, o texto renderizado recai para uma fonte padrão, o que pode afetar o layout.

**Solução:** Incorpore a fonte usando uma regra `@font-face` no seu CSS ou forneça uma pasta de fontes local via `FontOptions`.

```csharp
renderOptions.FontOptions.FontFolder = @"C:\fonts";
```

### b. Páginas grandes e consumo de memória

Renderizar uma página muito alta pode consumir muita RAM.

**Solução:** Defina uma altura máxima ou divida o documento em seções antes da conversão.

```csharp
renderOptions.PageHeight = 2000; // pixels
```

### c. Fundos transparentes

PNG suporta transparência, mas o fundo padrão é branco.

**Solução:** Altere a cor de fundo para transparente.

```csharp
renderOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

---

## Como renderizar HTML para imagem – recapitulação do exemplo completo

Juntando tudo, aqui está um trecho pronto para produção que cobre os requisitos mais frequentes:

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;
using Aspose.Html.Converters;

namespace HtmlToPngDemo
{
    class Program
    {
        static void Main()
        {
            // Load HTML (string, file, or URL)
            string html = "<html><head><style>p{font-weight:bold;color:#0066CC;}</style></head>"
                        + "<body><p>Bold blue text</p></body></html>";
            using var document = new HtmlDocument();
            document.Open(html);

            // Configure rendering for high quality and transparency
            var renderOptions = new ImageRenderingOptions
            {
                UseAntialiasing = true,
                TextOptions = { UseHinting = true },
                FontOptions = { WebFontStyle = WebFontStyle.Normal, FontFolder = @"C:\fonts" },
                BackgroundColor = System.Drawing.Color.Transparent,
                ResolutionX = 150,
                ResolutionY = 150
            };

            // Convert and save
            string outPath = @"C:\temp\html_snapshot.png";
            ImageConverter.ConvertHtmlToImage(document, outPath, renderOptions);

            Console.WriteLine($"Image saved to {outPath}");
        }
    }
}
```

**Saída esperada:** Um arquivo `html_snapshot.png` contendo um parágrafo em negrito e azul sobre um canvas transparente. A imagem será anti‑aliased, com texto nítido graças ao hinting.

---

## Conclusão

Agora você sabe como **criar PNG a partir de HTML** em C# usando Aspose.HTML. Ao construir um `HtmlDocument`, configurar `ImageRenderingOptions` e chamar `ImageConverter.ConvertHtmlToImage`, você pode converter HTML para PNG de forma confiável e **renderizar HTML como imagem** para qualquer cenário de automação.

A partir daqui, você pode explorar:

- Gerar miniaturas para páginas web dinâmicas.  
- Incorporar o PNG em PDFs com Aspose.PDF.  
- Usar a mesma abordagem para produzir JPEG ou BMP alterando a extensão do arquivo.  

Sinta‑se à vontade para experimentar DPI, cores de fundo e renderização multipágina para atender exatamente às necessidades do seu projeto. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui código completo e exemplos passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Renderizar HTML como PNG em .NET com Aspose.HTML](/html/english/net/rendering-html-documents/render-html-as-png/)
- [Como Renderizar HTML como PNG – Guia Completo em C#](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)
- [Criar PNG a partir de HTML – Guia Completo de Renderização em C#](/html/english/net/rendering-html-documents/create-png-from-html-full-c-rendering-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}