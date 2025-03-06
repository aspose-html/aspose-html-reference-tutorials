---
title: Conversores de ajuste fino em .NET com Aspose.HTML
linktitle: Conversores de ajuste fino em .NET
second_title: Aspose.HTML .NET API de manipulação de HTML
description: Aprenda a converter HTML para PDF, XPS e imagens com Aspose.HTML para .NET. Tutorial passo a passo com exemplos de código e perguntas frequentes.
weight: 16
url: /pt/net/advanced-features/fine-tuning-converters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Conversores de ajuste fino em .NET com Aspose.HTML


## Introdução

Aspose.HTML para .NET é uma biblioteca poderosa que permite aos desenvolvedores manipular e converter documentos HTML em vários formatos. Se você precisa converter HTML para PDF, XPS ou imagens, ou executar outras tarefas relacionadas a HTML, o Aspose.HTML fornece um conjunto robusto de ferramentas para ajudar você a fazer o trabalho.

Neste tutorial, exploraremos alguns recursos essenciais do Aspose.HTML para .NET e forneceremos explicações passo a passo para cada exemplo. Ao final deste tutorial, você terá um entendimento sólido de como usar o Aspose.HTML para .NET em seus aplicativos .NET.

## Pré-requisitos

Antes de mergulharmos nos exemplos, certifique-se de ter os seguintes pré-requisitos em vigor:

-  Aspose.HTML para .NET: Você deve ter a biblioteca Aspose.HTML para .NET instalada. Você pode baixá-la do[link para download](https://releases.aspose.com/html/net/).

-  Licença temporária (opcional): se você não tiver uma licença válida, poderá obter uma licença temporária em[aqui](https://purchase.aspose.com/temporary-license/).

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

## Converter HTML para PDF

### Etapa 1: preparar o código HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Etapa 2: Inicializar documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Etapa 3: Crie um dispositivo PDF e especifique o arquivo de saída

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Etapa 4: Renderizar HTML para PDF

```csharp
document.RenderTo(device);
```

Este exemplo converte um snippet HTML em um documento PDF. Você pode personalizar o código HTML e o arquivo de saída conforme necessário.

## Definir tamanho de página personalizado

### Etapa 1: preparar o código HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Etapa 2: Inicializar documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Etapa 3: Criar opções de renderização de PDF

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

### Etapa 4: Crie um dispositivo PDF e especifique opções e arquivo de saída

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Etapa 5: Renderizar HTML para PDF

```csharp
document.RenderTo(device);
```

Este exemplo demonstra como definir um tamanho de página personalizado para o documento PDF resultante.

## Ajustar resolução

### Etapa 1: preparar o código HTML e salvar no arquivo

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

### Etapa 2: Inicializar documento HTML

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

### Etapa 4: Crie um dispositivo PDF e especifique opções e arquivo de saída para baixa resolução

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Etapa 5: renderizar HTML para PDF para baixa resolução

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

### Etapa 7: Crie um dispositivo PDF e especifique opções e arquivo de saída para alta resolução

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Etapa 8: Renderizar HTML para PDF para alta resolução

```csharp
document.RenderTo(device);
```

Este exemplo ilustra como ajustar a resolução ao renderizar HTML para PDF, considerando telas de baixa e alta resolução.

## Especificar cor de fundo

### Etapa 1: preparar o código HTML e salvar no arquivo

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Etapa 2: Inicializar documento HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Etapa 3: inicializar opções de renderização de PDF com cor de fundo

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### Etapa 4: Crie um dispositivo PDF e especifique opções e arquivo de saída

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Etapa 5: Renderizar HTML para PDF

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

### Etapa 2: Inicializar documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Etapa 3: Crie opções de renderização de PDF com tamanhos de página esquerda e direita

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### Etapa 4: Crie um dispositivo PDF e especifique opções e arquivo de saída

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Etapa 5: Renderizar HTML para PDF

```csharp
document.RenderTo(device);
```

Este exemplo mostra como definir tamanhos de página diferentes para as páginas esquerda e direita ao converter HTML em PDF.

## Ajustar o tamanho da página ao conteúdo

### Etapa 1: preparar o código HTML

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### Etapa 2: Inicializar documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Etapa 3: Criar opções de renderização de PDF

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Etapa 4: Crie um dispositivo PDF e especifique opções e arquivo de saída

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Etapa 5: Renderizar HTML para PDF

```csharp
document.RenderTo(device);
```

Este exemplo demonstra como ajustar o tamanho da página para o conteúdo mais largo ao converter HTML em PDF.

## Especificar permissões de PDF

### Etapa 1: preparar o código HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### Etapa 2: Inicializar documento HTML

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

### Etapa 4: Crie um dispositivo PDF e especifique opções e arquivo de saída

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Etapa 5: Renderizar HTML para PDF

```csharp
document.RenderTo(device);
```

Este exemplo demonstra como especificar permissões e criptografia ao converter HTML em um PDF protegido.

## Especificar opções específicas da imagem

### Etapa 1: preparar o código HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### Etapa 2: Inicializar documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Etapa 3: Crie opções de renderização de imagem

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Etapa 4: Crie um dispositivo de imagem e especifique opções e arquivo de saída

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Etapa 5: renderizar HTML para imagem

```csharp
document.RenderTo(device);
```

Este exemplo demonstra como converter HTML em uma imagem com opções de renderização específicas, como formato, resolução e modo de suavização.

## Especificar opções de renderização XPS

### Etapa 1: preparar o código HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Etapa 2: Inicializar documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Etapa 3: Crie opções de renderização XPS com tamanho de página

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### Etapa 4: Crie o dispositivo XPS e especifique as opções e o arquivo de saída

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### Etapa 5: renderizar HTML para XPS

```csharp
document.RenderTo(device);
```

Este exemplo mostra como converter HTML para XPS com tamanho de página personalizado e opções de renderização.

## Combine vários documentos HTML em PDF

### Etapa 1: Prepare o código HTML para vários documentos

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### Etapa 2: Crie documentos HTML para mesclar

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### Etapa 3: Inicializar o renderizador HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Etapa 4: Criar dispositivo PDF para saída mesclada

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Etapa 5: Mesclar documentos HTML em PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

Este exemplo demonstra como combinar vários documentos HTML em um único arquivo PDF usando Aspose.HTML para .NET.

## Definir tempo limite de renderização

### Etapa 1: Prepare o código HTML com JavaScript

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

### Etapa 2: Inicializar documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Etapa 3: Inicializar o renderizador HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Etapa 4: Crie um dispositivo PDF e defina o tempo limite de renderização

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Etapa 5: renderizar HTML para PDF com tempo limite

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

Este exemplo demonstra como definir um tempo limite de renderização ao converter HTML em PDF, o que pode ser útil ao lidar com conteúdo dinâmico ou scripts de longa execução.

## Conclusão

Aspose.HTML para .NET é uma biblioteca versátil que capacita desenvolvedores a trabalhar com documentos HTML de forma eficiente. Neste tutorial, cobrimos vários exemplos, desde conversões básicas de HTML para PDF até recursos mais avançados, como tamanhos de página personalizados, resoluções e permissões. Ao seguir esses exemplos, você pode aproveitar todo o potencial do Aspose.HTML para .NET em seus aplicativos .NET.

 Caso tenha alguma dúvida ou precise de mais assistência, não hesite em visitar o[Fórum Aspose.HTML](https://forum.aspose.com/) para apoio e orientação.

## Perguntas frequentes

### Q1. O que é Aspose.HTML para .NET?
   
A1: Aspose.HTML para .NET é uma biblioteca .NET que permite aos desenvolvedores manipular e converter documentos HTML programaticamente. Ela oferece uma ampla gama de recursos para trabalhar com conteúdo HTML, incluindo HTML para PDF, XPS e conversão de imagem, bem como opções avançadas de renderização.

### Q2. Onde posso baixar o Aspose.HTML para .NET?

 A2: Você pode baixar Aspose.HTML para .NET do[link para download](https://releases.aspose.com/html/net/).

### Q3. Preciso de uma licença para usar o Aspose.HTML para .NET?

R3: Embora você possa usar o Aspose.HTML para .NET sem uma licença, é recomendável obter uma licença para uso em produção para desbloquear todos os recursos e remover quaisquer marcas d'água ou limitações.

### Q4. Como posso proteger meus arquivos PDF gerados com Aspose.HTML para .NET?

A4: Você pode especificar permissões de PDF e configurações de criptografia ao renderizar HTML para PDF usando Aspose.HTML para .NET. Isso permite que você controle quem pode acessar e modificar os arquivos PDF resultantes.

### Q5. Posso converter HTML para outros formatos, como XPS ou imagens?

R5: Sim, o Aspose.HTML para .NET suporta a conversão de HTML para vários formatos, incluindo PDF, XPS e imagens (por exemplo, JPEG). Você pode personalizar as configurações de conversão para atender às suas necessidades específicas.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
