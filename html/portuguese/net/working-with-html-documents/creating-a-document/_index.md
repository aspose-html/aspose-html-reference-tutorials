---
title: Criando um documento HTML no .NET com Aspose.HTML
linktitle: Criando um documento HTML no .NET
second_title: Aspose.HTML .NET API de manipulação de HTML
description: Aprenda a criar documentos HTML em .NET usando Aspose.HTML, do zero ou de URLs. Um tutorial abrangente para desenvolvedores web.
weight: 10
url: /pt/net/working-with-html-documents/creating-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criando um documento HTML no .NET com Aspose.HTML


No reino do desenvolvimento web e manipulação de dados, ter uma ferramenta poderosa para criar, modificar e trabalhar com documentos HTML é indispensável. Aspose.HTML para .NET é uma dessas ferramentas que pode simplificar suas tarefas relacionadas a HTML. Neste tutorial abrangente, exploraremos como criar documentos HTML usando Aspose.HTML para .NET passo a passo. Antes de mergulharmos nos exemplos, vamos cobrir alguns pré-requisitos.

## Pré-requisitos

Antes de embarcar nessa jornada, certifique-se de ter os seguintes pré-requisitos em vigor:

1. Visual Studio: certifique-se de ter o Visual Studio instalado no seu sistema.

2. Aspose.HTML para .NET: Baixe e instale a biblioteca Aspose.HTML para .NET. Você pode encontrar o link para download[aqui](https://releases.aspose.com/html/net/).

3. Conhecimento básico de C#: familiarize-se com os conceitos básicos da linguagem de programação C#.

Agora que cobrimos os pré-requisitos, vamos começar a criar documentos HTML.

## Importando namespaces

Primeiro, você precisa importar os namespaces necessários para usar Aspose.HTML no seu projeto C#. Adicione as seguintes diretivas using ao seu arquivo de código:

```csharp
using Aspose.Html.Dom.Svg;
using Aspose.Html;
```

## Criando um documento SVG

```csharp
static void CreateSVG()
{
    using (var document = new SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "sobre:em branco"))
    {
        // Execute ações no documento SVG aqui...
    }
}
```

 Neste exemplo, criamos um documento SVG fornecendo o conteúdo SVG e uma URL base. O`SVGDocument` A classe do Aspose.HTML para .NET permite que você manipule documentos SVG sem esforço.

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

 Este exemplo demonstra como criar um documento HTML do zero. O`HTMLDocument`class fornece uma tela em branco para seu conteúdo HTML.

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

## Criando um documento HTML a partir de uma URL remota

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

## Criando um documento HTML a partir de uma URL remota (alternativa)

```csharp
static void FromRemoteURL1()
{
    using (var document = new HTMLDocument(new Url("http://seu.site.com/")))
    {
        // Execute ações no documento HTML aqui...
    }
}
```

Essa abordagem alternativa também mostra como criar um documento HTML a partir de uma URL remota usando um construtor diferente.

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

## Criando um documento HTML a partir de um fluxo

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

Neste exemplo, mostramos como criar um documento HTML a partir de dados em um fluxo de memória. Isso pode ser útil quando você tem conteúdo HTML em um fluxo e quer manipulá-lo.

## Conclusão

O Aspose.HTML para .NET fornece um poderoso conjunto de ferramentas para criar e trabalhar com documentos HTML em seus aplicativos .NET. Com os exemplos fornecidos neste tutorial, você pode facilmente começar a criar documentos HTML, seja do zero, arquivos locais, URLs remotos ou conteúdo HTML existente.

 Tem dúvidas ou precisa de assistência? Visite o fórum da comunidade Aspose.HTML para obter suporte em[https://forum.aspose.com/](https://forum.aspose.com/).

## Perguntas frequentes

### P1: O Aspose.HTML para .NET é gratuito?
 A1: Aspose.HTML para .NET oferece um teste gratuito, mas para uso completo, você precisará comprar uma licença. Você pode encontrar mais detalhes em[https://purchase.aspose.com/buy](https://purchase.aspose.com/buy).

### P2: Como posso obter uma licença temporária para Aspose.HTML para .NET?
 A2: Se você precisar de uma licença temporária, você pode obtê-la em[https://purchase.aspose.com/temporary-license/](https://purchase.aspose.com/temporary-license/).

### Q3: Onde posso encontrar documentação do Aspose.HTML para .NET?
A3: A documentação pode ser encontrada em[https://reference.aspose.com/html/net/](https://reference.aspose.com/html/net/).

### Q4: Existem outras bibliotecas Aspose para desenvolvimento .NET?
 A4: Sim, a Aspose fornece uma variedade de bibliotecas para vários formatos de arquivo e tarefas de manipulação de documentos. Confira suas ofertas em[https://products.aspose.com/](https://products.aspose.com/).

### P5: Posso usar Aspose.HTML para .NET em meus aplicativos web?
R5: Sim, o Aspose.HTML para .NET é compatível com aplicativos web, o que o torna uma escolha versátil para projetos de desktop e baseados na web.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
