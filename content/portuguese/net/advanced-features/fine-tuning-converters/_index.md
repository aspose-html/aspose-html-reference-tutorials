---
title: Conversores de ajuste fino em .NET com Aspose.HTML
linktitle: Conversores de ajuste fino em .NET
second_title: API de manipulação de HTML Aspose.HTML .NET
description: Aprenda como converter HTML em PDF, XPS e imagens com Aspose.HTML para .NET. Tutorial passo a passo com exemplos de código e perguntas frequentes.
type: docs
weight: 16
url: /pt/net/advanced-features/fine-tuning-converters/
---

## Introdução

Aspose.HTML for .NET é uma biblioteca poderosa que permite aos desenvolvedores manipular e converter documentos HTML em vários formatos. Se você precisa converter HTML em PDF, XPS ou imagens, ou realizar outras tarefas relacionadas a HTML, o Aspose.HTML fornece um conjunto robusto de ferramentas para ajudá-lo a realizar o trabalho.

Neste tutorial, exploraremos alguns recursos essenciais do Aspose.HTML for .NET e forneceremos explicações passo a passo para cada exemplo. Ao final deste tutorial, você terá um conhecimento sólido de como usar Aspose.HTML for .NET em seus aplicativos .NET.

## Pré-requisitos

Antes de mergulharmos nos exemplos, certifique-se de ter os seguintes pré-requisitos em vigor:

-  Aspose.HTML for .NET: você deve ter a biblioteca Aspose.HTML for .NET instalada. Você pode baixá-lo no[Link para Download](https://releases.aspose.com/html/net/).

- Licença Temporária (Opcional): Se você não tiver uma licença válida, poderá obter uma licença temporária em[aqui](https://purchase.aspose.com/temporary-license/).

Agora, vamos explorar alguns casos de uso comuns com Aspose.HTML para .NET.

## Importar namespaces

No seu código C#, comece importando os namespaces necessários:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## Converter HTML em PDF

### Etapa 1: preparar o código HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Etapa 2: inicializar o documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Passo 3: Criar Dispositivo PDF e Especificar Arquivo de Saída

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Etapa 4: renderizar HTML em PDF

```csharp
document.RenderTo(device);
```

Este exemplo converte um snippet HTML em um documento PDF. Você pode personalizar o código HTML e o arquivo de saída conforme necessário.

## Definir tamanho de página personalizado

### Etapa 1: preparar o código HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Etapa 2: inicializar o documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Passo 3: Crie opções de renderização de PDF

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### Etapa 4: Criar dispositivo PDF e especificar opções e arquivo de saída

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Etapa 5: renderizar HTML em PDF

```csharp
document.RenderTo(device);
```

Este exemplo demonstra como definir um tamanho de página personalizado para o documento PDF resultante.

## Ajustar resolução

### Etapa 1: preparar o código HTML e salvar em arquivo

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Etapa 2: inicializar o documento HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Etapa 3: Crie opções de renderização de PDF para baixa resolução

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### Etapa 4: Criar dispositivo PDF e especificar opções e arquivo de saída para baixa resolução

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Etapa 5: renderizar HTML em PDF para baixa resolução

```csharp
document.RenderTo(device);
```

### Etapa 6: Crie opções de renderização de PDF para alta resolução

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### Etapa 7: Crie um dispositivo PDF e especifique as opções e o arquivo de saída para alta resolução

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Etapa 8: renderizar HTML em PDF para alta resolução

```csharp
document.RenderTo(device);
```

Este exemplo ilustra como ajustar a resolução ao renderizar HTML para PDF, considerando telas de baixa e alta resolução.

## Especifique a cor de fundo

### Etapa 1: preparar o código HTML e salvar em arquivo

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Etapa 2: inicializar o documento HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Etapa 3: inicializar as opções de renderização de PDF com cor de fundo

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### Etapa 4: Criar dispositivo PDF e especificar opções e arquivo de saída

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Etapa 5: renderizar HTML em PDF

```csharp
document.RenderTo(device);
```

Este exemplo demonstra como especificar uma cor de fundo ao converter HTML em PDF.

## Definir tamanhos de página esquerda e direita

### Etapa 1: preparar o código HTML

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### Etapa 2: inicializar o documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Etapa 3: Crie opções de renderização de PDF com tamanhos de página esquerdo e direito

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### Etapa 4: Criar dispositivo PDF e especificar opções e arquivo de saída

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Etapa 5: renderizar HTML em PDF

```csharp
document.RenderTo(device);
```

Este exemplo mostra como definir tamanhos de página diferentes para as páginas esquerda e direita ao converter HTML em PDF.

## Ajuste o tamanho da página ao conteúdo

### Etapa 1: preparar o código HTML

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### Etapa 2: inicializar o documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Passo 3: Crie opções de renderização de PDF

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Etapa 4: Criar dispositivo PDF e especificar opções e arquivo de saída

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Etapa 5: renderizar HTML em PDF

```csharp
document.RenderTo(device);
```

Este exemplo demonstra como ajustar o tamanho da página para o conteúdo mais amplo ao converter HTML em PDF.

## Especifique permissões de PDF

### Etapa 1: preparar o código HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### Etapa 2: inicializar o documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Etapa 3: Crie opções de renderização de PDF com permissões

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### Etapa 4: Criar dispositivo PDF e especificar opções e arquivo de saída

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Etapa 5: renderizar HTML em PDF

```csharp
document.RenderTo(device);
```

Este exemplo demonstra como especificar permissões e criptografia ao converter HTML em um PDF protegido.

## Especifique opções específicas de imagem

### Etapa 1: preparar o código HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### Etapa 2: inicializar o documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Etapa 3: criar opções de renderização de imagem

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Etapa 4: criar dispositivo de imagem e especificar opções e arquivo de saída

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Etapa 5: renderizar HTML em imagem

```csharp
document.RenderTo(device);
```

Este exemplo demonstra como converter HTML em uma imagem com opções de renderização específicas, como formato, resolução e modo de suavização.

## Especifique opções de renderização XPS

### Etapa 1: preparar o código HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Etapa 2: inicializar o documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Etapa 3: criar opções de renderização XPS com tamanho de página

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### Etapa 4: Criar dispositivo XPS e especificar opções e arquivo de saída

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### Etapa 5: renderizar HTML para XPS

```csharp
document.RenderTo(device);
```

Este exemplo mostra como converter HTML em XPS com tamanho de página personalizado e opções de renderização.

## Combine vários documentos HTML em PDF

### Etapa 1: preparar código HTML para vários documentos

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### Etapa 2: crie documentos HTML para mesclar

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### Etapa 3: inicializar o renderizador HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Passo 4: Crie um dispositivo PDF para saída mesclada

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Etapa 5: mesclar documentos HTML em PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

Este exemplo demonstra como combinar vários documentos HTML em um único arquivo PDF usando Aspose.HTML for .NET.

## Definir tempo limite de renderização

### Etapa 1: preparar o código HTML com JavaScript

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### Etapa 2: inicializar o documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Etapa 3: inicializar o renderizador HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Passo 4: Crie um dispositivo PDF e defina o tempo limite de renderização

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Etapa 5: renderizar HTML em PDF com tempo limite

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

Este exemplo demonstra como definir um tempo limite de renderização ao converter HTML em PDF, o que pode ser útil ao lidar com conteúdo dinâmico ou scripts de longa execução.

## Conclusão

Aspose.HTML for .NET é uma biblioteca versátil que permite aos desenvolvedores trabalhar com documentos HTML de forma eficiente. Neste tutorial, cobrimos vários exemplos, desde conversões básicas de HTML para PDF até recursos mais avançados, como tamanhos de página personalizados, resoluções e permissões. Seguindo esses exemplos, você pode aproveitar todo o potencial do Aspose.HTML for .NET em seus aplicativos .NET.

 Se você tiver alguma dúvida ou precisar de mais assistência, não hesite em visitar o[Fórum Aspose.HTML](https://forum.aspose.com/) para apoio e orientação.

## Perguntas frequentes

### Q1. O que é Aspose.HTML para .NET?
   
A1: Aspose.HTML for .NET é uma biblioteca .NET que permite aos desenvolvedores manipular e converter documentos HTML programaticamente. Ele oferece uma ampla gama de recursos para trabalhar com conteúdo HTML, incluindo HTML para PDF, XPS e conversão de imagens, bem como opções avançadas de renderização.

### Q2. Onde posso baixar o Aspose.HTML para .NET?

 A2: Você pode baixar Aspose.HTML para .NET no[Link para Download](https://releases.aspose.com/html/net/).

### Q3. Preciso de uma licença para usar o Aspose.HTML for .NET?

A3: Embora você possa usar o Aspose.HTML for .NET sem licença, é recomendável obter uma licença para uso em produção para desbloquear todos os recursos e remover quaisquer marcas d'água ou limitações.

### Q4. Como posso proteger meus arquivos PDF gerados com Aspose.HTML for .NET?

A4: Você pode especificar permissões de PDF e configurações de criptografia ao renderizar HTML para PDF usando Aspose.HTML for .NET. Isso permite controlar quem pode acessar e modificar os arquivos PDF resultantes.

### Q5. Posso converter HTML para outros formatos como XPS ou imagens?

R5: Sim, Aspose.HTML for .NET suporta a conversão de HTML para vários formatos, incluindo PDF, XPS e imagens (por exemplo, JPEG). Você pode personalizar as configurações de conversão para atender aos seus requisitos específicos.