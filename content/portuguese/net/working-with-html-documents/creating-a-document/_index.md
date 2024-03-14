---
title: Criando um documento HTML em .NET com Aspose.HTML
linktitle: Criando um documento HTML em .NET
second_title: API de manipulação de HTML Aspose.HTML .NET
description: Aprenda como criar documentos HTML em .NET usando Aspose.HTML, do zero ou a partir de URLs. Um tutorial abrangente para desenvolvedores web.
type: docs
weight: 10
url: /pt/net/working-with-html-documents/creating-a-document/
---

No domínio do desenvolvimento web e manipulação de dados, é indispensável ter uma ferramenta poderosa para criar, modificar e trabalhar com documentos HTML. Aspose.HTML for .NET é uma ferramenta que pode simplificar suas tarefas relacionadas a HTML. Neste tutorial abrangente, exploraremos como criar documentos HTML usando Aspose.HTML for .NET passo a passo. Antes de mergulharmos nos exemplos, vamos abordar alguns pré-requisitos.

## Pré-requisitos

Antes de embarcar nesta jornada, certifique-se de ter os seguintes pré-requisitos em vigor:

1. Visual Studio: certifique-se de ter o Visual Studio instalado em seu sistema.

2.  Aspose.HTML para .NET: Baixe e instale a biblioteca Aspose.HTML para .NET. Você pode encontrar o link para download[aqui](https://releases.aspose.com/html/net/).

3. Conhecimento básico de C#: Familiarize-se com os fundamentos da linguagem de programação C#.

Agora que cobrimos os pré-requisitos, vamos começar a criar documentos HTML.

## Importando Namespaces

Primeiramente, você precisa importar os namespaces necessários para usar Aspose.HTML em seu projeto C#. Adicione as seguintes diretivas using ao seu arquivo de código:

```csharp
using Aspose.Html.Dom.Svg;
using Aspose.Html;
```

## Criando um documento SVG

```csharp
static void CreateSVG()
{
    using (var document = new SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "about:blank"))
    {
        // Execute ações no documento SVG aqui...
    }
}
```

 Neste exemplo, criamos um documento SVG fornecendo o conteúdo SVG e uma URL base. O`SVGDocument`class do Aspose.HTML for .NET permite manipular documentos SVG sem esforço.

## Criando um documento HTML do zero

```csharp
static void FromScratch()
{
    using (var document = new HTMLDocument())
    {
        // Execute ações no documento HTML aqui...
    }
}
```

 Este exemplo demonstra como criar um documento HTML do zero. O`HTMLDocument` class fornece uma tela em branco para seu conteúdo HTML.

## Criando um documento HTML a partir de um arquivo local

```csharp
static void FromLocalFile()
{
    string dataDir = "Your Data Directory";
    using (var document = new HTMLDocument(dataDir + "input.html"))
    {
        // Execute ações no documento HTML aqui...
    }
}
```

 Se você tiver um arquivo HTML existente em seu sistema local, poderá carregá-lo usando o`HTMLDocument` classe, como mostrado neste exemplo.

## Criando um documento HTML a partir de um URL remoto

```csharp
static void FromRemoteURL()
{
    using (var document = new HTMLDocument("http://seu.site.com/"))
    {
        // Execute ações no documento HTML aqui...
    }
}
```

Às vezes, você pode precisar trabalhar com conteúdo HTML hospedado em um servidor remoto. Este exemplo demonstra como criar um documento HTML a partir de uma URL remota.

## Criando um documento HTML a partir de um URL remoto (alternativa)

```csharp
static void FromRemoteURL1()
{
    using (var document = new HTMLDocument(new Url("http://seu.site.com/")))
    {
        // Execute ações no documento HTML aqui...
    }
}
```

Esta abordagem alternativa também mostra como criar um documento HTML a partir de uma URL remota usando um construtor diferente.

## Criando um documento HTML a partir de conteúdo HTML

```csharp
static void FromHTML()
{
    using (var document = new HTMLDocument("<p>my first paragraph</p>", "."))
    {
        // Execute ações no documento HTML aqui...
    }
}
```

Se você tiver conteúdo HTML em formato de string, poderá criar um documento HTML com ele, conforme demonstrado neste exemplo.

## Criando um documento HTML a partir de um stream

```csharp
static void FromStream()
{
    using (MemoryStream mem = new MemoryStream())
    using (StreamWriter sw = new StreamWriter(mem))
    {
        sw.Write("<p>my first paragraph</p>");
        sw.Flush();
        mem.Seek(0, SeekOrigin.Begin);
        using (var document = new HTMLDocument(mem, "about:blank"))
        {
            // Execute ações no documento HTML aqui...
        }
    }
}
```

Neste exemplo, mostramos como criar um documento HTML a partir de dados em um fluxo de memória. Isso pode ser útil quando você tem conteúdo HTML em um stream e deseja manipulá-lo.

## Conclusão

Aspose.HTML for .NET fornece um poderoso conjunto de ferramentas para criar e trabalhar com documentos HTML em seus aplicativos .NET. Com os exemplos fornecidos neste tutorial, você pode começar facilmente a criar documentos HTML, seja do zero, arquivos locais, URLs remotos ou conteúdo HTML existente.

 Tem perguntas ou precisa de assistência? Visite o fórum da comunidade Aspose.HTML para suporte em[https://forum.aspose.com/](https://forum.aspose.com/).

## Perguntas frequentes

### Q1: O uso do Aspose.HTML for .NET é gratuito?
 A1: Aspose.HTML for .NET oferece uma avaliação gratuita, mas para uso completo, você precisará adquirir uma licença. Você pode encontrar mais detalhes em[https://purchase.aspose.com/buy](https://purchase.aspose.com/buy).

### Q2: Como posso obter uma licença temporária do Aspose.HTML for .NET?
A2: Se precisar de uma licença temporária, você pode obter uma em[https://purchase.aspose.com/temporary-license/](https://purchase.aspose.com/temporary-license/).

### Q3: Onde posso encontrar documentação para Aspose.HTML for .NET?
 A3: A documentação pode ser encontrada em[https://reference.aspose.com/html/net/](https://reference.aspose.com/html/net/).

### Q4: Existem outras bibliotecas Aspose para desenvolvimento .NET?
 A4: Sim, o Aspose fornece uma variedade de bibliotecas para vários formatos de arquivo e tarefas de manipulação de documentos. Confira suas ofertas em[https://produtos.aspose.com/](https://products.aspose.com/).

### Q5: Posso usar Aspose.HTML for .NET em meus aplicativos da web?
R5: Sim, o Aspose.HTML for .NET é compatível com aplicativos da web, o que o torna uma escolha versátil para projetos de desktop e baseados na web.
