---
title: Web Scraping em .NET com Aspose.HTML
linktitle: Raspagem da Web em .NET
second_title: API de manipulação de HTML Aspose.HTML .NET
description: Aprenda a manipular documentos HTML em .NET com Aspose.HTML. Navegue, filtre, consulte e selecione elementos de forma eficaz para um desenvolvimento web aprimorado.
type: docs
weight: 13
url: /pt/net/advanced-features/web-scraping/
---

Na era digital de hoje, manipular e extrair informações de documentos HTML é uma tarefa comum para desenvolvedores. Aspose.HTML for .NET é uma ferramenta poderosa que simplifica o processamento e manipulação de HTML em aplicativos .NET. Neste tutorial, exploraremos vários aspectos do Aspose.HTML for .NET, incluindo pré-requisitos, namespaces e exemplos passo a passo para ajudá-lo a aproveitar todo o seu potencial.

## Pré-requisitos

Antes de mergulhar no mundo do Aspose.HTML for .NET, você precisará de alguns pré-requisitos:

1. Ambiente de desenvolvimento: certifique-se de ter um ambiente de desenvolvimento funcional configurado com o Visual Studio ou qualquer outro IDE compatível para desenvolvimento .NET.

2.  Aspose.HTML for .NET: Baixe e instale a biblioteca Aspose.HTML for .NET do[Link para Download](https://releases.aspose.com/html/net/). Você pode escolher entre a versão de teste gratuita ou licenciada com base em suas necessidades.

3. Conhecimento básico de HTML: Familiaridade com a estrutura e os elementos HTML é essencial para usar Aspose.HTML for .NET de maneira eficaz.

## Importando Namespaces

Para começar, você precisa importar os namespaces necessários em seu projeto C#. Esses namespaces fornecem acesso às classes e funcionalidades do Aspose.HTML for .NET:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

Com os pré-requisitos em vigor e os namespaces importados, vamos detalhar alguns exemplos importantes passo a passo para ilustrar como usar o Aspose.HTML para .NET de maneira eficaz.

## Navegando pelo HTML

Neste exemplo navegaremos por um documento HTML e acessaremos seus elementos passo a passo.

```csharp
public static void NavigateThroughHTML()
{
    // Prepare um código HTML
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    // Inicialize um documento a partir do código preparado
    using (var document = new HTMLDocument(html_code, "."))
    {
        // Obtenha a referência ao primeiro filho (primeiro SPAN) do BODY
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // Saída: Olá

        // Obtenha a referência ao espaço em branco entre os elementos HTML
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Saída: ' '

        // Obtenha a referência ao segundo elemento SPAN
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Resultado: Mundo!
    }
}
```

 Neste exemplo, criamos um documento HTML, acessamos seu primeiro filho (um`SPAN` elemento), o espaço em branco entre os elementos e o segundo`SPAN` elemento, demonstrando navegação básica.

## Usando filtros de nó

Os filtros de nó permitem processar seletivamente elementos específicos em um documento HTML.

```csharp
public static void NodeFilterUsageExample()
{
    // Prepare um código HTML
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    // Inicialize um documento com base no código preparado
    using (var document = new HTMLDocument(code, "."))
    {
        // Crie um TreeWalker com um filtro personalizado para elementos de imagem
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                // Saída: imagem1.png
                // Saída: image2.png
            }
        }
    }
}
```

 Este exemplo demonstra como usar um filtro de nó personalizado para extrair elementos específicos (neste caso,`IMG` elementos) do documento HTML.

## Consultas XPath

As consultas XPath permitem pesquisar elementos em um documento HTML com base em critérios específicos.

```csharp
public static void XPathQueryUsageExample()
{
    // Prepare um código HTML
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello!</span>
            </div>
        </div>
        <p class='happy'>
            <span>World</span>
        </p>
    ";
    
    // Inicialize um documento com base no código preparado
    using (var document = new HTMLDocument(code, "."))
    {
        // Avalie uma expressão XPath para selecionar elementos específicos
        var result = document.Evaluate("//*[@class='feliz']//span",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // Iterar sobre os nós resultantes
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // Saída: Olá
            // Resultado: Mundo!
        }
    }
}
```

Este exemplo mostra o uso de consultas XPath para localizar elementos no documento HTML com base em seus atributos e estrutura.

## Seletores CSS

Os seletores CSS fornecem uma maneira alternativa de selecionar elementos em um documento HTML, semelhante à forma como as folhas de estilo CSS direcionam os elementos.

```csharp
public static void CSSSelectorUsageExample()
{
    // Prepare um código HTML
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello</span>
            </div>
        </div>
        <p class='happy'>
            <span>World!</span>
        </p>
    ";
    
    // Inicialize um documento com base no código preparado
    using (var document = new HTMLDocument(code, "."))
    {
        //Use um seletor CSS para extrair elementos com base em classe e hierarquia
        var elements = document.QuerySelectorAll(".happy span");
        
        // Iterar sobre a lista de elementos resultante
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // Saída: Olá
            // Resultado: Mundo!
        }
    }
}
```

Aqui, demonstramos como usar seletores CSS para direcionar elementos específicos no documento HTML.

Com esses exemplos, você obteve uma compreensão básica de como navegar, filtrar, consultar e selecionar elementos em documentos HTML usando Aspose.HTML for .NET.

## Conclusão

 Aspose.HTML for .NET é uma biblioteca versátil que permite aos desenvolvedores .NET trabalhar de forma eficiente com documentos HTML. Com seus recursos poderosos para navegação, filtragem, consulta e seleção de elementos, você pode lidar perfeitamente com várias tarefas de processamento de HTML. Seguindo este tutorial e explorando a documentação em[Documentação Aspose.HTML para .NET](https://reference.aspose.com/html/net/), você pode desbloquear todo o potencial desta ferramenta para seus aplicativos .NET.

## Perguntas frequentes

### Q1. O uso do Aspose.HTML para .NET é gratuito?

A1: Aspose.HTML for .NET oferece uma versão de teste gratuita, mas para uso em produção, você precisará adquirir uma licença. Você pode encontrar detalhes e opções de licenciamento em[Compra Aspose.HTML](https://purchase.aspose.com/buy).

### Q2. Como posso obter uma licença temporária do Aspose.HTML for .NET?

 A2: Você pode obter uma licença temporária para fins de teste em[Licença temporária Aspose.HTML](https://purchase.aspose.com/temporary-license/).

### Q3. Onde posso procurar ajuda ou suporte para Aspose.HTML for .NET?

 A3: Se você encontrar algum problema ou tiver dúvidas, poderá visitar o[Fórum Aspose.HTML](https://forum.aspose.com/) para assistência e apoio comunitário.

### Q4. Existem recursos adicionais para aprender Aspose.HTML for .NET?

 A4: Junto com este tutorial, você pode explorar mais tutoriais e documentação sobre o[Página de documentação do Aspose.HTML para .NET](https://reference.aspose.com/html/net/).

### Q5. O Aspose.HTML for .NET é compatível com as versões mais recentes do .NET?

R5: Aspose.HTML for .NET é atualizado regularmente para garantir compatibilidade com as versões e tecnologias mais recentes do .NET.