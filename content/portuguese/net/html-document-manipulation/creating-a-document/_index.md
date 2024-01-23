---
title: Criando um documento em .NET com Aspose.HTML
linktitle: Criando um documento em .NET
second_title: API de manipulação de HTML Aspose.HTML .NET
description: Liberte o poder do Aspose.HTML para .NET. Aprenda a criar, manipular e otimizar documentos HTML e SVG com facilidade. Explore exemplos passo a passo e perguntas frequentes.
type: docs
weight: 14
url: /pt/net/html-document-manipulation/creating-a-document/
---

No mundo em constante evolução do desenvolvimento web, ficar à frente da curva é essencial. Aspose.HTML for .NET fornece aos desenvolvedores um kit de ferramentas robusto para trabalhar com documentos HTML. Esteja você começando do zero, carregando de um arquivo, extraindo de um URL ou manipulando documentos SVG, esta biblioteca oferece a versatilidade que você precisa.

Neste guia passo a passo, nos aprofundaremos nos fundamentos do uso do Aspose.HTML para .NET, garantindo que você esteja bem equipado para utilizar esta ferramenta poderosa em seus projetos de desenvolvimento web. Antes de nos aprofundarmos nos detalhes, vamos examinar os pré-requisitos e os namespaces necessários para iniciar sua jornada.

## Pré-requisitos

Para seguir este tutorial com êxito e aproveitar o poder do Aspose.HTML para .NET, você precisará dos seguintes pré-requisitos:

- Uma máquina Windows com .NET Framework ou .NET Core instalado.
- Um editor de código como o Visual Studio.
- Conhecimento básico de programação C#.

Agora que você tem seus pré-requisitos definidos, vamos começar.

## Importando Namespaces

Antes de começar a usar o Aspose.HTML for .NET, você precisa importar os namespaces necessários. Esses namespaces contêm classes e métodos vitais para trabalhar com documentos HTML. Abaixo está uma lista de namespaces que você deve importar:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Com esses namespaces importados, agora você está pronto para mergulhar nos exemplos passo a passo.

## Criando um documento HTML do zero

### Etapa 1: inicializar um documento HTML vazio

```csharp
// Inicialize um documento HTML vazio.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Crie um elemento de texto e adicione-o ao documento
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Salve o documento no disco.
    document.Save("document.html");
}
```

Neste exemplo, começamos criando um documento HTML vazio e adicionando um "Hello World!" texto para ele. Em seguida, salvamos o documento em um arquivo.

## Criando um documento HTML a partir de um arquivo

### Etapa 1: preparar um arquivo ‘document.html’

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### Etapa 2: carregar de um arquivo 'document.html'

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Grave o conteúdo do documento no fluxo de saída.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Aqui preparamos um arquivo com "Hello World!" conteúdo e, em seguida, carregue-o como um documento HTML. Imprimimos o conteúdo do documento no console.

## Criando um documento HTML a partir de um URL

### Etapa 1: carregar um documento de uma página da web

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // Grave o conteúdo do documento no fluxo de saída.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Neste exemplo, carregamos um documento HTML diretamente de uma página web e exibimos seu conteúdo.

## Criando um documento HTML a partir de uma string

### Passo 1: Prepare um código HTML

```csharp
var html_code = "<p>Hello World!</p>";
```

### Etapa 2: inicializar o documento a partir da variável string

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Salve o documento no disco.
    document.Save("document.html");
}
```

Aqui, criamos um documento HTML a partir de uma variável string e o salvamos em um arquivo.

## Criando um documento HTML a partir de um MemoryStream

### Etapa 1: crie um objeto de fluxo de memória

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // Escreva o código HTML no objeto de memória
    sw.Write("<p>Hello World!</p>");
    // Defina a posição para o início
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // Inicialize o documento do fluxo de memória
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // Salve o documento no disco.
        document.Save("document.html");
    }
}
```

Neste exemplo, criamos um documento HTML a partir de um fluxo de memória e o salvamos em um arquivo.

## Trabalhando com documentos SVG

### Etapa 1: inicializar o documento SVG a partir de uma string

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // Grave o conteúdo do documento no fluxo de saída.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Aqui, criamos e exibimos um documento SVG a partir de uma string.

## Carregando um documento HTML de forma assíncrona

### Etapa 1: crie a instância do documento HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Etapa 2: Inscreva-se no evento ‘ReadyStateChange’

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    //Verifique o valor da propriedade 'ReadyState'.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Etapa 3: navegue de forma assíncrona no Uri especificado

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Neste exemplo, carregamos um documento HTML de forma assíncrona e manipulamos o evento 'ReadyStateChange' para exibir o conteúdo quando o carregamento for concluído.

## Tratamento do evento 'OnLoad'

### Etapa 1: crie a instância do documento HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Etapa 2: Inscreva-se no evento ‘OnLoad’

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### Etapa 3: navegue de forma assíncrona no Uri especificado

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Este exemplo demonstra o carregamento de um documento HTML de forma assíncrona e o tratamento do evento 'OnLoad' para exibir o conteúdo após a conclusão.

## Para concluir

No mundo dinâmico do desenvolvimento web, ter as ferramentas certas à sua disposição é crucial. Aspose.HTML for .NET fornece meios para criar, manipular e processar documentos HTML e SVG com eficiência. Este guia abrangente orientou você no essencial, garantindo que você possa aproveitar o poder do Aspose.HTML for .NET em seus projetos.

## Perguntas frequentes

### Q1: O que é Aspose.HTML para .NET?

A1: Aspose.HTML for .NET é uma biblioteca .NET poderosa que permite aos desenvolvedores trabalhar com documentos HTML e SVG. Ele oferece uma ampla gama de recursos, desde a criação de documentos do zero até a análise e manipulação de arquivos HTML e SVG existentes.

### P2: Posso usar Aspose.HTML para .NET com .NET Core?

A2: Sim, Aspose.HTML for .NET é compatível com .NET Framework e .NET Core, tornando-o uma escolha versátil para aplicativos .NET modernos.

### Q3: O Aspose.HTML for .NET é adequado para web scraping e análise?

A3: Com certeza! Aspose.HTML for .NET é uma excelente escolha para tarefas de web scraping e análise, graças à sua capacidade de carregar documentos HTML a partir de URLs e strings. Você pode extrair dados, realizar análises e muito mais.

### Q4: Como posso acessar o suporte para Aspose.HTML for .NET?

 A4: Se você encontrar algum problema ou tiver dúvidas ao usar o Aspose.HTML for .NET, você pode visitar o[Aspor Fórum](https://forum.aspose.com/) pelo apoio e assistência da comunidade e dos especialistas da Aspose.

### R5: Onde posso encontrar documentação detalhada e opções de download?

R5: Para documentação abrangente e acesso às opções de download, você pode consultar os seguintes links:

- [Documentação](https://reference.aspose.com/html/net/)
- [Download](https://releases.aspose.com/html/net/)
- [Comprar](https://purchase.aspose.com/buy)
- [Teste grátis](https://releases.aspose.com/)
- [Licença Temporária](https://purchase.aspose.com/temporary-license/)