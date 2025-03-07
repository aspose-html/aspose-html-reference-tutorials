---
title: Salvando um documento no .NET com Aspose.HTML
linktitle: Salvando um documento no .NET
second_title: Aspose.HTML .NET API de manipulação de HTML
description: Desbloqueie o poder do Aspose.HTML para .NET com nosso guia passo a passo. Aprenda a criar, manipular e converter documentos HTML e SVG
weight: 16
url: /pt/net/html-document-manipulation/saving-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salvando um documento no .NET com Aspose.HTML


Na era digital de hoje, criar e manipular documentos HTML e SVG é essencial para muitos desenvolvedores de software e empresas. Aspose.HTML para .NET é uma biblioteca poderosa que simplifica essas tarefas, oferecendo várias funcionalidades para trabalhar com HTML, SVG e muito mais. Neste guia abrangente, vamos mergulhar nos fundamentos do Aspose.HTML para .NET, dividindo cada exemplo em etapas fáceis de seguir. Seja você um desenvolvedor experiente ou apenas começando, você achará este guia inestimável para aproveitar os recursos do Aspose.HTML.

## Pré-requisitos

Antes de embarcarmos nessa jornada, vamos garantir que você tenha tudo o que precisa:

- Ambiente de desenvolvimento: certifique-se de ter o Visual Studio ou qualquer outro ambiente de desenvolvimento .NET instalado no seu computador.

- Aspose.HTML para .NET: Você precisa obter a biblioteca Aspose.HTML para .NET. Você pode baixá-la de[aqui](https://releases.aspose.com/html/net/).

- Conhecimento de C#: Familiaridade com a linguagem de programação C# é benéfica, mas não obrigatória. Este guia foi criado para ser amigável a iniciantes.

## Importar namespace

Para começar a usar o Aspose.HTML para .NET, você precisará importar os namespaces necessários para o seu projeto. No seu código C#, inclua o seguinte namespace:

### Etapa 1: Importar o namespace Aspose.HTML
```csharp
using Aspose.Html;
```

Este namespace concederá a você acesso a vários recursos de manipulação de HTML e SVG.

## HTML para arquivo

### Etapa 1: inicializar um documento HTML vazio
```csharp
// Inicializa um documento HTML vazio.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Crie um elemento de texto e adicione-o ao documento
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Salve o HTML no arquivo em disco.
    document.Save("document.html");
}
```

Neste exemplo, criamos um documento HTML e adicionamos um texto simples "Hello World!" a ele. Então salvamos o HTML em um arquivo no disco.

## HTML sem arquivo vinculado

### Etapa 1: Prepare um arquivo HTML simples
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Aqui, criamos um arquivo HTML básico com um link âncora para outro arquivo.

### Etapa 2: Carregue 'document.html' na memória
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Criar instância de Opções de salvamento
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //Defina a profundidade máxima de manipulação como 0 para cortar arquivos HTML vinculados.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // Salvar o documento
    document.Save(@".\html-to-file-example\document.html", options);
}
```

Neste exemplo, carregamos um documento HTML na memória, definimos a profundidade máxima de manipulação para cortar arquivos vinculados e salvamos o documento. 

## HTML para MHTML

### Etapa 1: Prepare um arquivo HTML simples
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Assim como no Exemplo 2, criamos um arquivo HTML básico com um link âncora para outro arquivo.

### Etapa 2: Carregue 'document.html' na memória e salve como MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Salvar o documento como MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

Aqui, carregamos o documento HTML na memória e o salvamos no formato MHTML.

## HTML para Markdown

### Etapa 1: Prepare um código HTML
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 Nesta etapa, definimos um trecho de código HTML contendo um`<H2>` elemento.

### Etapa 2: inicializar o documento a partir do código HTML e salvar como Markdown
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Salve o documento como um arquivo Markdown.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

Criamos um documento HTML a partir do trecho de código e o salvamos como um arquivo Markdown.

## SVG para arquivo

### Etapa 1: Prepare um código SVG
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' altura='80' largura='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

Aqui, criamos um código SVG que desenha um gráfico simples e colorido.

### Etapa 2: inicializar um documento SVG a partir do código e salvar no disco
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // Salve o arquivo SVG no disco
    document.Save("document.svg");
}
```

Nesta etapa, criamos um documento SVG a partir do código e o salvamos como um arquivo SVG.

## Conclusão

Aspose.HTML para .NET é uma biblioteca versátil que simplifica o manuseio de documentos HTML e SVG em seus aplicativos .NET. Neste guia, cobrimos cinco exemplos essenciais, dividindo cada um em instruções passo a passo. Não importa se você está criando, manipulando ou convertendo documentos, o Aspose.HTML tem tudo o que você precisa. Seguindo essas etapas, você está no caminho certo para dominar essa ferramenta poderosa.

## Perguntas frequentes

### P1: O que é Aspose.HTML para .NET?

A1: Aspose.HTML para .NET é uma biblioteca .NET que fornece uma ampla gama de recursos para trabalhar com documentos HTML e SVG, incluindo criação, manipulação e conversão.

### P2: Onde posso baixar o Aspose.HTML para .NET?

 A2: Você pode baixar Aspose.HTML para .NET em[aqui](https://releases.aspose.com/html/net/).

### Q3: O Aspose.HTML para .NET é adequado para iniciantes?

A3: Sim, o Aspose.HTML para .NET pode ser usado tanto por iniciantes quanto por desenvolvedores experientes. Os exemplos neste guia são projetados para serem amigáveis para iniciantes.

### P4: Posso converter HTML para outros formatos usando Aspose.HTML para .NET?

R4: Sim, o Aspose.HTML para .NET suporta conversão para vários formatos, incluindo MHTML e Markdown, conforme mostrado nos exemplos.

### P5: Onde posso obter suporte para Aspose.HTML para .NET?

 A5: Você pode encontrar suporte e respostas para suas perguntas no fórum da comunidade Aspose.HTML[aqui](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
