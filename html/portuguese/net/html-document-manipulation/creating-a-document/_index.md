---
title: Criando um documento em .NET com Aspose.HTML
linktitle: Criando um documento no .NET
second_title: Aspose.HTML .NET API de manipulação de HTML
description: Libere o poder do Aspose.HTML para .NET. Aprenda a criar, manipular e otimizar documentos HTML e SVG com facilidade. Explore exemplos passo a passo e perguntas frequentes.
type: docs
weight: 14
url: /pt/net/html-document-manipulation/creating-a-document/
---

No mundo em constante evolução do desenvolvimento web, ficar à frente da curva é essencial. O Aspose.HTML para .NET fornece aos desenvolvedores um kit de ferramentas robusto para trabalhar com documentos HTML. Quer você esteja começando do zero, carregando de um arquivo, puxando de uma URL ou manipulando documentos SVG, esta biblioteca oferece a versatilidade de que você precisa.

Neste guia passo a passo, vamos nos aprofundar nos fundamentos do uso do Aspose.HTML para .NET, garantindo que você esteja bem equipado para usar esta ferramenta poderosa em seus projetos de desenvolvimento web. Antes de mergulharmos nos detalhes, vamos analisar os pré-requisitos e os namespaces necessários para dar o pontapé inicial em sua jornada.

## Pré-requisitos

Para seguir este tutorial com sucesso e aproveitar o poder do Aspose.HTML para .NET, você precisará dos seguintes pré-requisitos:

- Uma máquina Windows com .NET Framework ou .NET Core instalado.
- Um editor de código como o Visual Studio.
- Conhecimento básico de programação em C#.

Agora que você tem seus pré-requisitos definidos, vamos começar.

## Importando namespaces

Antes de começar a usar o Aspose.HTML para .NET, você precisa importar os namespaces necessários. Esses namespaces contêm classes e métodos que são vitais para trabalhar com documentos HTML. Abaixo está uma lista de namespaces que você deve importar:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Com esses namespaces importados, você está pronto para mergulhar nos exemplos passo a passo.

## Criando um documento HTML do zero

### Etapa 1: inicializar um documento HTML vazio

```csharp
// Inicializa um documento HTML vazio.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Crie um elemento de texto e adicione-o ao documento
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Salve o documento no disco.
    document.Save("document.html");
}
```

Neste exemplo, começamos criando um documento HTML vazio e adicionando um texto "Hello World!" a ele. Então salvamos o documento em um arquivo.

## Criando um documento HTML a partir de um arquivo

### Etapa 1: preparar um arquivo 'document.html'

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### Etapa 2: Carregar de um arquivo 'document.html'

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Grave o conteúdo do documento no fluxo de saída.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Aqui, preparamos um arquivo com conteúdo "Hello World!" e então o carregamos como um documento HTML. Imprimimos o conteúdo do documento no console.

## Criando um documento HTML a partir de uma URL

### Etapa 1: Carregue um documento de uma página da web

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // Grave o conteúdo do documento no fluxo de saída.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Neste exemplo, carregamos um documento HTML diretamente de uma página da web e exibimos seu conteúdo.

## Criando um documento HTML a partir de uma string

### Etapa 1: Prepare um código HTML

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

Aqui, criamos um documento HTML a partir de uma variável de string e o salvamos em um arquivo.

## Criando um documento HTML a partir de um MemoryStream

### Etapa 1: Crie um objeto de fluxo de memória

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // Escreva o código HTML no objeto de memória
    sw.Write("<p>Hello World!</p>");
    // Defina a posição para o início
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // Inicializar documento a partir do fluxo de memória
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

### Etapa 1: Crie a instância do documento HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Etapa 2: Inscreva-se no evento 'ReadyStateChange'

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    // Verifique o valor da propriedade 'ReadyState'.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Etapa 3: Navegue de forma assíncrona no Uri especificado

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Neste exemplo, carregamos um documento HTML de forma assíncrona e manipulamos o evento 'ReadyStateChange' para exibir o conteúdo quando o carregamento estiver concluído.

## Manipulando o evento 'OnLoad'

### Etapa 1: Crie a instância do documento HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Etapa 2: Inscreva-se no evento 'OnLoad'

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### Etapa 3: Navegue de forma assíncrona no Uri especificado

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Este exemplo demonstra o carregamento de um documento HTML de forma assíncrona e o tratamento do evento 'OnLoad' para exibir o conteúdo após a conclusão.

## Para concluir

No mundo dinâmico do desenvolvimento web, ter as ferramentas certas à sua disposição é crucial. O Aspose.HTML para .NET equipa você com os meios para criar, manipular e processar documentos HTML e SVG de forma eficiente. Este guia abrangente o guiou pelos fundamentos, garantindo que você possa aproveitar o poder do Aspose.HTML para .NET em seus projetos.

## Perguntas frequentes

### P1: O que é Aspose.HTML para .NET?

A1: Aspose.HTML para .NET é uma biblioteca .NET poderosa que permite que desenvolvedores trabalhem com documentos HTML e SVG. Ela fornece uma ampla gama de recursos, desde a criação de documentos do zero até a análise e manipulação de arquivos HTML e SVG existentes.

### P2: Posso usar Aspose.HTML para .NET com .NET Core?

R2: Sim, o Aspose.HTML para .NET é compatível com o .NET Framework e o .NET Core, o que o torna uma escolha versátil para aplicativos .NET modernos.

### Q3: O Aspose.HTML para .NET é adequado para análise e extração de dados da web?

A3: Com certeza! Aspose.HTML para .NET é uma excelente escolha para tarefas de web scraping e parsing, graças à sua capacidade de carregar documentos HTML de URLs e strings. Você pode extrair dados, executar análises e muito mais.

### P4: Como posso acessar o suporte para Aspose.HTML para .NET?

 A4: Se você encontrar algum problema ou tiver dúvidas ao usar o Aspose.HTML para .NET, você pode visitar o[Fórum Aspose](https://forum.aspose.com/) para apoio e assistência da comunidade e dos especialistas da Aspose.

### R5: Onde posso encontrar documentação detalhada e opções de download?

R5: Para documentação abrangente e acesso às opções de download, você pode consultar os seguintes links:

- [Documentação](https://reference.aspose.com/html/net/)
- [Download](https://releases.aspose.com/html/net/)
- [Comprar](https://purchase.aspose.com/buy)
- [Teste grátis](https://releases.aspose.com/)
- [Licença Temporária](https://purchase.aspose.com/temporary-license/)