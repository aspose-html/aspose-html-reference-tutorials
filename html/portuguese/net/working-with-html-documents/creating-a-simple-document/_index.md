---
title: Criando um documento simples em .NET com Aspose.HTML
linktitle: Criando um documento simples no .NET
second_title: Aspose.HTML .NET API de manipulação de HTML
description: Aprenda a trabalhar com documentos HTML em .NET usando Aspose.HTML. Crie, manipule e converta HTML sem esforço. Comece hoje mesmo!
type: docs
weight: 11
url: /pt/net/working-with-html-documents/creating-a-simple-document/
---

## Introdução

No mundo do desenvolvimento web, criar e manipular documentos HTML é uma tarefa fundamental. Não importa se você está construindo uma página web simples ou um aplicativo web complexo, ter uma ferramenta confiável para manipulação de documentos HTML é crucial. Neste tutorial, vamos mergulhar no mundo do Aspose.HTML para .NET, uma biblioteca poderosa que permite que você trabalhe com documentos HTML perfeitamente. 

## Pré-requisitos

Antes de embarcarmos nessa jornada, vamos garantir que você tenha os pré-requisitos necessários:

### 1. Ambiente de desenvolvimento .NET

Você deve ter um ambiente de desenvolvimento .NET configurado em sua máquina. Se ainda não tiver, você pode baixar e instalar a versão mais recente do .NET do site da Microsoft.

### 2. Aspose.HTML para .NET

 Para acompanhar os exemplos neste tutorial, você precisará baixar e instalar a biblioteca Aspose.HTML for .NET. Você pode encontrar o link para download[aqui](https://releases.aspose.com/html/net/).

### 3. Editor de texto ou IDE

Você precisará de um editor de texto ou de um Integrated Development Environment (IDE) para escrever e executar seu código .NET. Escolhas populares incluem Visual Studio, Visual Studio Code ou JetBrains Rider.

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

Neste exemplo, criaremos um documento HTML simples com uma imagem, uma lista ordenada e uma tabela. Vamos dividir cada passo e explicá-lo em detalhes.

### Etapa 1: Configurando o arquivo de saída

Começamos definindo o arquivo de saída onde nosso documento HTML será salvo.

```csharp
string dataDir = "Your Data Directory";
String outputHtml = dataDir + "SimpleDocument.html";
```

### Etapa 2: Criando um documento HTML

 Em seguida, criamos uma instância do`HTMLDocument` classe, que representa um documento HTML.

```csharp
var document = new HTMLDocument();
```

### Etapa 3: Adicionar uma imagem

Agora, adicionamos uma imagem ao documento HTML. Criamos uma`img` elemento usando o`CreateElement` método, defina seu`Src`, `Alt` e`Title` atributos e, em seguida, anexá-lo ao documento`Body`.

```csharp
if (document.CreateElement("img") is HTMLImageElement img)
{
    img.Src = "http://via.placeholder.com/400x200";
    img.Alt = "Placeholder 400x200";
    img.Title = "Placeholder image";
    document.Body.AppendChild(img);
}
```

### Etapa 4: Adicionando uma lista ordenada

 Em seguida, adicionamos uma lista ordenada ao documento. Criamos uma`ol` elemento e iterar para adicionar itens de lista a ele.

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

### Etapa 5: Adicionando uma tabela

 Por fim, adicionamos uma tabela ao documento. Criamos uma`table` elemento, criar linhas e células, definir suas`Id` e`TextContent`, e anexá-los à tabela.

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

### Etapa 6: Salvando o documento

Por fim, salvamos o documento HTML no arquivo de saída especificado.

```csharp
document.Save(outputHtml);
```

Parabéns! Você acabou de criar um documento HTML simples usando Aspose.HTML para .NET. Este é apenas o começo do que você pode conseguir com esta biblioteca poderosa.

## Conclusão

Neste tutorial, apresentamos a você o Aspose.HTML para .NET e o orientamos na criação de um documento HTML básico. Conforme você explora mais esta biblioteca, descobrirá seus amplos recursos para trabalhar com documentos HTML em aplicativos .NET. Não importa se você está desenvolvendo aplicativos da web, automatizando tarefas relacionadas a HTML ou realizando conversões complexas de documentos, o Aspose.HTML para .NET tem tudo o que você precisa.

Boa codificação!

## Perguntas frequentes

### 1. O que é Aspose.HTML para .NET?

Aspose.HTML para .NET é uma biblioteca .NET que fornece funcionalidade abrangente para trabalhar com documentos HTML de várias maneiras, como criação, manipulação e conversão.

### 2. Onde posso encontrar a documentação do Aspose.HTML para .NET?

 Você pode encontrar a documentação do Aspose.HTML para .NET[aqui](https://reference.aspose.com/html/net/).

### 3. Existe uma versão de avaliação gratuita disponível para o Aspose.HTML para .NET?

 Sim, você pode obter uma avaliação gratuita do Aspose.HTML para .NET[aqui](https://releases.aspose.com/).

### 4. Como posso obter uma licença temporária para Aspose.HTML para .NET?

 Você pode obter uma licença temporária para Aspose.HTML para .NET[aqui](https://purchase.aspose.com/temporary-license/).

### 5. Onde posso obter suporte para Aspose.HTML para .NET?

 Você pode obter suporte e fazer perguntas sobre Aspose.HTML para .NET no[Fórum Aspose](https://forum.aspose.com/).
