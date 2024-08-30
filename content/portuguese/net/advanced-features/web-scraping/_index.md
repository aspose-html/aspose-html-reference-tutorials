---
title: Web Scraping em .NET com Aspose.HTML
linktitle: Raspagem da Web em .NET
second_title: Aspose.HTML .NET API de manipulação de HTML
description: Aprenda a manipular documentos HTML em .NET com Aspose.HTML. Navegue, filtre, consulte e selecione elementos de forma eficaz para desenvolvimento web aprimorado.
type: docs
weight: 13
url: /pt/net/advanced-features/web-scraping/
---

Na era digital de hoje, manipular e extrair informações de documentos HTML é uma tarefa comum para desenvolvedores. Aspose.HTML para .NET é uma ferramenta poderosa que simplifica o processamento e a manipulação de HTML em aplicativos .NET. Neste tutorial, exploraremos vários aspectos do Aspose.HTML para .NET, incluindo pré-requisitos, namespaces e exemplos passo a passo para ajudar você a aproveitar todo o seu potencial.

## Pré-requisitos

Antes de mergulhar no mundo do Aspose.HTML para .NET, você precisará de alguns pré-requisitos:

1. Ambiente de desenvolvimento: certifique-se de ter um ambiente de desenvolvimento funcional configurado com o Visual Studio ou qualquer outro IDE compatível para desenvolvimento .NET.

2.  Aspose.HTML para .NET: Baixe e instale a biblioteca Aspose.HTML para .NET do[link para download](https://releases.aspose.com/html/net/). Você pode escolher entre a versão de teste gratuita ou uma licenciada com base em suas necessidades.

3. Conhecimento básico de HTML: A familiaridade com a estrutura e os elementos HTML é essencial para usar efetivamente o Aspose.HTML para .NET.

## Importando namespaces

Para começar, você precisa importar os namespaces necessários no seu projeto C#. Esses namespaces fornecem acesso às classes e funcionalidades do Aspose.HTML para .NET:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

Com os pré-requisitos definidos e os namespaces importados, vamos analisar alguns exemplos importantes passo a passo para ilustrar como usar o Aspose.HTML para .NET de forma eficaz.

## Navegando pelo HTML

Neste exemplo, navegaremos por um documento HTML e acessaremos seus elementos passo a passo.

```csharp
public static void NavigateThroughHTML()
{
    // Preparar um código HTML
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    // Inicializar um documento a partir do código preparado
    using (var document = new HTMLDocument(html_code, "."))
    {
        // Obter a referência para o primeiro filho (primeiro SPAN) do BODY
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // Saída: Olá

        // Obter a referência ao espaço em branco entre os elementos HTML
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Saída: ' '

        // Obter a referência ao segundo elemento SPAN
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Saída: Mundo!
    }
}
```

 Neste exemplo, criamos um documento HTML, acessamos seu primeiro filho (um`SPAN` elemento), o espaço em branco entre os elementos e o segundo`SPAN` elemento, demonstrando navegação básica.

## Usando filtros de nó

Os filtros de nós permitem que você processe seletivamente elementos específicos dentro de um documento HTML.

```csharp
public static void NodeFilterUsageExample()
{
    // Preparar um código HTML
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    // Inicializar um documento com base no código preparado
    using (var document = new HTMLDocument(code, "."))
    {
        // Crie um TreeWalker com um filtro personalizado para elementos de imagem
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                // Saída: image1.png
                // Saída: image2.png
            }
        }
    }
}
```

 Este exemplo demonstra como usar um filtro de nó personalizado para extrair elementos específicos (neste caso,`IMG` elementos) do documento HTML.

## Consultas XPath

Consultas XPath permitem que você pesquise elementos em um documento HTML com base em critérios específicos.

```csharp
public static void XPathQueryUsageExample()
{
    // Preparar um código HTML
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
    
    // Inicializar um documento com base no código preparado
    using (var document = new HTMLDocument(code, "."))
    {
        // Avalie uma expressão XPath para selecionar elementos específicos
        var result = document.Evaluate("//*[@class='feliz']//período",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // Iterar sobre os nós resultantes
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // Saída: Olá
            // Saída: Mundo!
        }
    }
}
```

Este exemplo mostra o uso de consultas XPath para localizar elementos no documento HTML com base em seus atributos e estrutura.

## Seletores CSS

Os seletores CSS fornecem uma maneira alternativa de selecionar elementos em um documento HTML, semelhante à forma como as folhas de estilo CSS direcionam elementos.

```csharp
public static void CSSSelectorUsageExample()
{
    // Preparar um código HTML
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
    
    // Inicializar um documento com base no código preparado
    using (var document = new HTMLDocument(code, "."))
    {
        //Use um seletor CSS para extrair elementos com base na classe e hierarquia
        var elements = document.QuerySelectorAll(".happy span");
        
        // Iterar sobre a lista resultante de elementos
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // Saída: Olá
            // Saída: Mundo!
        }
    }
}
```

Aqui, demonstramos como usar seletores CSS para direcionar elementos específicos no documento HTML.

Com esses exemplos, você adquiriu uma compreensão fundamental de como navegar, filtrar, consultar e selecionar elementos em documentos HTML usando o Aspose.HTML para .NET.

## Conclusão

 Aspose.HTML para .NET é uma biblioteca versátil que capacita desenvolvedores .NET a trabalhar eficientemente com documentos HTML. Com seus poderosos recursos para navegação, filtragem, consulta e seleção de elementos, você pode lidar com várias tarefas de processamento HTML perfeitamente. Seguindo este tutorial e explorando a documentação em[Aspose.HTML para documentação .NET](https://reference.aspose.com/html/net/), você pode desbloquear todo o potencial desta ferramenta para seus aplicativos .NET.

## Perguntas frequentes

### Q1. O Aspose.HTML para .NET é gratuito?

A1: Aspose.HTML para .NET oferece uma versão de teste gratuita, mas para uso em produção, você precisará comprar uma licença. Você pode encontrar detalhes e opções de licenciamento em[Aspose.HTML Compra](https://purchase.aspose.com/buy).

### Q2. Como posso obter uma licença temporária para Aspose.HTML para .NET?

 A2: Você pode obter uma licença temporária para fins de teste em[Licença temporária Aspose.HTML](https://purchase.aspose.com/temporary-license/).

### Q3. Onde posso buscar ajuda ou suporte para Aspose.HTML para .NET?

 A3: Se você encontrar algum problema ou tiver dúvidas, você pode visitar o[Fórum Aspose.HTML](https://forum.aspose.com/) para assistência e apoio comunitário.

### Q4. Há algum recurso adicional para aprender Aspose.HTML para .NET?

 A4: Junto com este tutorial, você pode explorar mais tutoriais e documentação sobre o[Página de documentação do Aspose.HTML para .NET](https://reference.aspose.com/html/net/).

### Q5. O Aspose.HTML para .NET é compatível com as versões mais recentes do .NET?

R5: O Aspose.HTML para .NET é atualizado regularmente para garantir compatibilidade com as últimas versões e tecnologias do .NET.