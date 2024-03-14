---
title: Criando um documento simples em .NET com Aspose.HTML
linktitle: Criando um documento simples em .NET
second_title: API de manipulação de HTML Aspose.HTML .NET
description: Aprenda a trabalhar com documentos HTML em .NET usando Aspose.HTML. Crie, manipule e converta HTML sem esforço. Comece hoje!
type: docs
weight: 11
url: /pt/net/working-with-html-documents/creating-a-simple-document/
---

## Introdução

No mundo do desenvolvimento web, criar e manipular documentos HTML é uma tarefa fundamental. Esteja você construindo uma página da web simples ou um aplicativo da web complexo, é crucial ter uma ferramenta confiável para manipulação de documentos HTML. Neste tutorial, mergulharemos no mundo do Aspose.HTML for .NET, uma biblioteca poderosa que permite trabalhar perfeitamente com documentos HTML. 

## Pré-requisitos

Antes de embarcarmos nesta jornada, vamos garantir que você tenha os pré-requisitos necessários:

### 1. Ambiente de desenvolvimento .NET

Você deve ter um ambiente de desenvolvimento .NET configurado em sua máquina. Se ainda não o fez, você pode baixar e instalar a versão mais recente do .NET no site da Microsoft.

### 2. Aspose.HTML para .NET

 Para acompanhar os exemplos deste tutorial, você precisará baixar e instalar a biblioteca Aspose.HTML for .NET. Você pode encontrar o link para download[aqui](https://releases.aspose.com/html/net/).

### 3. Editor de texto ou IDE

Você precisará de um editor de texto ou de um ambiente de desenvolvimento integrado (IDE) para escrever e executar seu código .NET. As escolhas populares incluem Visual Studio, Visual Studio Code ou JetBrains Rider.

Agora que você atendeu aos pré-requisitos, vamos prosseguir com o tutorial.

## Importar namespaces

Antes de nos aprofundarmos nos exemplos de código, vamos importar os namespaces necessários do Aspose.HTML para .NET. Esses namespaces contêm classes e métodos que usaremos para trabalhar com documentos HTML.

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.Dom.HtmlBody;
using Aspose.Html.Rendering;
```

## Criando um documento HTML simples

Neste exemplo, criaremos um documento HTML simples com uma imagem, uma lista ordenada e uma tabela. Vamos analisar cada etapa e explicá-la em detalhes.

### Etapa 1: configurando o arquivo de saída

Começamos definindo o arquivo de saída onde nosso documento HTML será salvo.

```csharp
string dataDir = "Your Data Directory";
String outputHtml = dataDir + "SimpleDocument.html";
```

### Etapa 2: Criando um documento HTML

 A seguir, criamos uma instância do`HTMLDocument` classe, que representa um documento HTML.

```csharp
var document = new HTMLDocument();
```

### Etapa 3: adicionar uma imagem

Agora, adicionamos uma imagem ao documento HTML. Nós criamos um`img` elemento usando o`CreateElement` método, defina seu`Src`, `Alt` e`Title` atributos e, em seguida, anexe-o ao documento`Body`.

```csharp
if (document.CreateElement("img") is HTMLImageElement img)
{
    img.Src = "http://via.placeholder.com/400x200";
    img.Alt = "Placeholder 400x200";
    img.Title = "Placeholder image";
    document.Body.AppendChild(img);
}
```

### Etapa 4: adicionar uma lista ordenada

 A seguir, adicionamos uma lista ordenada ao documento. Nós criamos um`ol` elemento e iterar para adicionar itens de lista a ele.

```csharp
var orderedListElement = document.CreateElement("ol") as HTMLOListElement;
for (int i = 0; i < 10; i++)
{
    var listItem = document.CreateElement("li") as HTMLLIElement;
    listItem.TextContent = $" List Item {i + 1}";
    orderedListElement.AppendChild(listItem);
}
document.Body.AppendChild(orderedListElement);
```

### Passo 5: Adicionando uma Tabela

 Finalmente, adicionamos uma tabela ao documento. Nós criamos um`table` elemento, criar linhas e células, definir seus`Id` e`TextContent`e anexe-os à tabela.

```csharp
var table = document.CreateElement("table") as HTMLTableElement;
var tBody = document.CreateElement("tbody") as HTMLTableSectionElement;
for (var i = 0; i < 3; i++)
{
    var row = document.CreateElement("tr") as HTMLTableRowElement;
    row.Id = "trow_" + i;
    for (var j = 0; j < 3; j++)
    {
        var cell = document.CreateElement("td") as HTMLTableCellElement;
        cell.Id = $"cell{i}_{j}";
        cell.TextContent = "Cell " + j;
        row.AppendChild(cell);
    }
    tBody.AppendChild(row);
}
table.AppendChild(tBody);
document.Body.AppendChild(table);
```

### Etapa 6: salvando o documento

Finalmente, salvamos o documento HTML no arquivo de saída especificado.

```csharp
document.Save(outputHtml);
```

Parabéns! Você acabou de criar um documento HTML simples usando Aspose.HTML para .NET. Este é apenas o começo do que você pode alcançar com esta poderosa biblioteca.

## Conclusão

Neste tutorial, apresentamos o Aspose.HTML para .NET e orientamos você na criação de um documento HTML básico. Ao explorar mais esta biblioteca, você descobrirá seus amplos recursos para trabalhar com documentos HTML em aplicativos .NET. Esteja você desenvolvendo aplicativos da web, automatizando tarefas relacionadas a HTML ou realizando conversões complexas de documentos, o Aspose.HTML for .NET tem o que você precisa.

Boa codificação!

## Perguntas frequentes

### 1. O que é Aspose.HTML para .NET?

Aspose.HTML for .NET é uma biblioteca .NET que fornece funcionalidade abrangente para trabalhar com documentos HTML de várias maneiras, como criação, manipulação e conversão.

### 2. Onde posso encontrar a documentação do Aspose.HTML for .NET?

 Você pode encontrar a documentação do Aspose.HTML para .NET[aqui](https://reference.aspose.com/html/net/).

### 3. Existe uma avaliação gratuita disponível para Aspose.HTML for .NET?

 Sim, você pode obter uma avaliação gratuita do Aspose.HTML para .NET[aqui](https://releases.aspose.com/).

### 4. Como posso obter uma licença temporária do Aspose.HTML for .NET?

Você pode obter uma licença temporária para Aspose.HTML for .NET[aqui](https://purchase.aspose.com/temporary-license/).

### 5. Onde posso obter suporte para Aspose.HTML for .NET?

 Você pode obter suporte e fazer perguntas sobre o Aspose.HTML for .NET no site[Aspor Fórum](https://forum.aspose.com/).
