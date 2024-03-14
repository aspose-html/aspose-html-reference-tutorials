---
title: Usando modelos HTML em .NET com Aspose.HTML
linktitle: Usando modelos HTML em .NET
second_title: API de manipulação de HTML Aspose.HTML .NET
description: Aprenda como usar Aspose.HTML for .NET para gerar documentos HTML dinamicamente a partir de dados JSON. Aproveite o poder da manipulação de HTML em seus aplicativos .NET.
type: docs
weight: 17
url: /pt/net/advanced-features/using-html-templates/
---

Se você deseja trabalhar com documentos e modelos HTML em suas aplicações .NET, você está no lugar certo! Aspose.HTML for .NET é uma biblioteca versátil que permite aos desenvolvedores manipular documentos e modelos HTML sem esforço. Neste tutorial, nos aprofundaremos nos fundamentos do uso do Aspose.HTML para .NET, detalhando cada etapa e fornecendo uma explicação clara ao longo do caminho.

## Pré-requisitos

Antes de mergulharmos nos detalhes do Aspose.HTML para .NET, certifique-se de ter os seguintes pré-requisitos em vigor:

1. Visual Studio: certifique-se de ter o Visual Studio instalado em sua máquina. Você pode baixá-lo do site, caso ainda não o tenha feito.

2.  Aspose.HTML for .NET: você precisa ter o Aspose.HTML for .NET instalado em seu projeto do Visual Studio. Você pode obtê-lo no[documentação](https://reference.aspose.com/html/net/).

3. Dados JSON: prepare uma fonte de dados JSON que você deseja usar para preencher seu modelo HTML. Para este tutorial, usaremos os seguintes dados JSON:

```json
{
    'FirstName': 'John',
    'LastName': 'Smith',
    'Address': {
        'City': 'Dallas',
        'Street': 'Austin rd.',
        'Number': '200'
    }
}
```

4. Modelo HTML: crie um modelo HTML que deseja preencher com os dados JSON. Aqui está um exemplo simples:

```html
<table border=1>
    <tr>
        <th>Person</th>
        <th>Address</th>
    </tr>
    <tr>
        <td>{{FirstName}} {{LastName}}</td>
        <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
    </tr>
</table>
```

## Importando Namespaces

Primeiramente, vamos importar os namespaces necessários em seu projeto .NET:

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Loading;
```

Agora que cobrimos os pré-requisitos e importamos os namespaces necessários, vamos detalhar cada etapa.

## Etapa 1: preparar uma fonte de dados JSON

Comece criando uma fonte de dados JSON que contém as informações que você deseja inserir em seu modelo HTML. Neste exemplo, já preparamos uma fonte de dados JSON conforme mencionado nos pré-requisitos. Salve-o em um arquivo, por exemplo, “data-source.json”.

```csharp
var data = @"{
    'FirstName': 'John',
    'LastName': 'Smith',
    'Address': {
        'City': 'Dallas',
        'Street': 'Austin rd.',
        'Number': '200'
    }
}";
System.IO.File.WriteAllText("data-source.json", data);
```

Este trecho de código lê os dados JSON e os grava em um arquivo chamado “data-source.json”.

## Etapa 2: preparar um modelo HTML

Agora, vamos criar um modelo HTML que você deseja preencher com os dados JSON. Salve este modelo em um arquivo, como “template.html”.

```csharp
var template = @"
<table border=1>
    <tr>
        <th>Person</th>
        <th>Address</th>
    </tr>
    <tr>
        <td>{{FirstName}} {{LastName}}</td>
        <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
    </tr>
</table>
";
System.IO.File.WriteAllText("template.html", template);
```

 Este modelo HTML inclui espaços reservados como`{{FirstName}}`, `{{LastName}}`, `{{Address.Street}}`, `{{Address.Number}}` e`{{Address.City}}`, que substituiremos pelos dados reais.

## Etapa 3: preencher o modelo HTML

 Por fim, invoque o`Converter.ConvertTemplate` método para preencher seu modelo HTML com os dados da fonte JSON.

```csharp
Aspose.Html.Converters.Converter.ConvertTemplate(
"template.html", new Aspose.Html.Converters.TemplateData("data-source.json"), new Aspose.Html.Loading.TemplateLoadOptions(), "document.html"
);
```

Este código pega o arquivo “template.html”, substitui os espaços reservados pelos valores JSON correspondentes e salva o resultado em “document.html”.

Parabéns! Você aproveitou com sucesso o poder do Aspose.HTML for .NET para gerar dinamicamente documentos HTML a partir de dados JSON.

## Conclusão

Neste tutorial, exploramos os fundamentos do uso do Aspose.HTML for .NET para criar documentos HTML dinamicamente. Abordamos os pré-requisitos, a importação de namespaces e detalhamos cada etapa. Seguindo essas etapas, você pode integrar perfeitamente a geração de documentos HTML em seus aplicativos .NET.

## Perguntas frequentes

### Q1. O que é Aspose.HTML para .NET?

A1: Aspose.HTML for .NET é uma biblioteca poderosa que permite aos desenvolvedores .NET trabalhar com documentos e modelos HTML programaticamente. Ele simplifica tarefas como geração, conversão e manipulação de HTML.

### Q2. Onde posso encontrar a documentação do Aspose.HTML para .NET?

 A2: Você pode acessar a documentação do Aspose.HTML for .NET[aqui](https://reference.aspose.com/html/net/). Ele fornece informações abrangentes, incluindo referências de API e exemplos de código.

### Q3. Como posso baixar o Aspose.HTML para .NET?

A3: Você pode baixar Aspose.HTML para .NET na página de download[aqui](https://releases.aspose.com/html/net/).

### Q4. Existe uma avaliação gratuita disponível para Aspose.HTML for .NET?

 A4: Sim, você pode experimentar o Aspose.HTML for .NET baixando a versão de teste gratuita em[aqui](https://releases.aspose.com/).

### Q5. Preciso de uma licença temporária para Aspose.HTML for .NET?

 R5: Se você precisar de uma licença temporária para fins de avaliação, poderá obtê-la em[aqui](https://purchase.aspose.com/temporary-license/).