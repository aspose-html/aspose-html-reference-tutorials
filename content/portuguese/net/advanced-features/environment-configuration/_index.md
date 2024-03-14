---
title: Configuração de ambiente em .NET com Aspose.HTML
linktitle: Configuração do ambiente em .NET
second_title: API de manipulação de HTML Aspose.HTML .NET
description: Aprenda como trabalhar com documentos HTML em .NET usando Aspose.HTML para tarefas como gerenciamento de scripts, estilos personalizados, controle de execução de JavaScript e muito mais. Este tutorial abrangente fornece exemplos passo a passo e perguntas frequentes para você começar.
type: docs
weight: 10
url: /pt/net/advanced-features/environment-configuration/
---

No mundo digital de hoje, criar e manipular documentos HTML é uma tarefa fundamental para muitos desenvolvedores. Esteja você construindo um aplicativo da web ou precise converter HTML para outros formatos, como PDF ou imagens, o Aspose.HTML for .NET é uma ferramenta poderosa para ter em seu kit de ferramentas. Neste tutorial, exploraremos vários aspectos do Aspose.HTML for .NET, incluindo pré-requisitos, importação de namespaces e exemplos passo a passo com explicações detalhadas.

## Pré-requisitos

Antes de começarmos a usar o Aspose.HTML para .NET, você precisará garantir que possui os seguintes pré-requisitos:

1. Visual Studio: certifique-se de ter o Visual Studio instalado em sua máquina de desenvolvimento. Aspose.HTML for .NET foi projetado para funcionar perfeitamente com o Visual Studio.

2.  Aspose.HTML for .NET: Você pode baixar a biblioteca Aspose.HTML for .NET do site. Use o seguinte link para acessar a página de download:[Baixe Aspose.HTML para .NET](https://releases.aspose.com/html/net/).

3. Instalação e Licença: Após baixar a biblioteca, siga as instruções de instalação fornecidas na documentação. Você também pode precisar de uma licença válida para usar alguns dos recursos avançados. Você pode obter uma licença no site Aspose:[Adquira a licença Aspose.HTML](https://purchase.aspose.com/buy).

4.  Avaliação gratuita: se quiser experimentar o Aspose.HTML antes de comprar uma licença, você pode obter uma versão de avaliação gratuita neste link:[Avaliação gratuita do Aspose.HTML](https://releases.aspose.com/).

Agora que você tem os pré-requisitos necessários, vamos prosseguir para a próxima seção, onde importaremos os namespaces necessários.

## Importar namespaces

Para trabalhar com Aspose.HTML for .NET de maneira eficaz, você precisará importar os namespaces apropriados para o seu projeto. Abaixo, listaremos os namespaces necessários para os exemplos que abordaremos:

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

Com esses namespaces importados, você pode acessar a funcionalidade fornecida pelo Aspose.HTML for .NET.

## Desabilitar execução de scripts

Vamos começar com um exemplo básico de como desabilitar a execução de script em um documento HTML e convertê-lo em PDF. Siga esses passos:

1. Crie um trecho de código HTML e salve-o em um arquivo chamado “document.html”.

```csharp
var code = "<span>Hello World!!</span> " +
           "<script>document.write('Have a nice day!');</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Inicialize a configuração do Aspose.HTML, marcando 'scripts' como um recurso não confiável.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    configuration.Security |= Aspose.Html.Sandbox.Scripts;
    
    // Inicialize um documento HTML com a configuração especificada
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Converter HTML em PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

Neste exemplo, evitamos a execução de scripts dentro do documento HTML, garantindo segurança na conversão para PDF. Agora, vamos passar para o próximo exemplo.

## Especifique a folha de estilo do usuário

Às vezes, você pode querer aplicar estilos personalizados a elementos de um documento HTML. Veja como você pode fazer isso usando Aspose.HTML para .NET:

1. Crie um trecho de código HTML e salve-o em um arquivo chamado “document.html”.

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2.  Defina uma cor personalizada para o`<span>` elemento usando uma folha de estilo do usuário.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var userAgent = configuration.GetService<Aspose.Html.Services.IUserAgentService>();
    userAgent.UserStyleSheet = "span { color: green; }";
    
    // Inicialize um documento HTML com a configuração especificada
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Converter HTML em PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

 Neste exemplo, aplicamos um estilo personalizado ao`<span>`elemento, definindo sua cor de texto para verde. Aspose.HTML for .NET permite manipular estilos com facilidade.

## Tempo limite de execução do JavaScript

Ao lidar com código JavaScript potencialmente demorado, é essencial definir um tempo limite para evitar a execução indefinida. Veja como você pode fazer isso:

1. Crie um trecho de código HTML com um loop infinito e salve-o em um arquivo chamado “document.html”.

```csharp
var code = @"<script>while(true){}</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Defina um tempo limite de execução do JavaScript para 10 segundos.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var runtime = configuration.GetService<Aspose.Html.Services.IRuntimeService>();
    runtime.JavaScriptTimeout = TimeSpan.FromSeconds(10);
    
    // Inicialize um documento HTML com a configuração especificada
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Aguarde até que todos os scripts sejam concluídos/cancelados e converta HTML para PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

Neste exemplo, limitamos o tempo de execução do JavaScript a 10 segundos, garantindo que o script não seja executado indefinidamente, o que poderia causar problemas de desempenho.

## Manipulador de mensagens personalizado

Às vezes, você pode precisar lidar com mensagens de erro ou recursos ausentes ao carregar um documento HTML. Aqui está um exemplo de como criar um manipulador de mensagens personalizado:

1. Crie um trecho de código HTML com uma referência de arquivo de imagem ausente e salve-o em um arquivo chamado “document.html”.

```csharp
var code = @"<img src='missing.jpg'>";
System.IO.File.WriteAllText("document.html", code);
```

2. Adicione um manipulador de mensagens de erro ao serviço de rede para registrar solicitações com falha.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var network = configuration.GetService<Aspose.Html.Services.INetworkService>();
    network.MessageHandlers.Add(new LogMessageHandler());
    
    // Inicialize um documento HTML com a configuração especificada
    // Durante o carregamento do documento, a aplicação tentará carregar a imagem, e veremos o resultado desta operação no console.
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Converter HTML em PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

Neste exemplo, adicionamos um manipulador de mensagens personalizado (`LogMessageHandler`) para registrar informações sobre solicitações com falha. Isso pode ser particularmente útil para depurar e lidar com recursos ausentes de maneira adequada.

## Conclusão

Aspose.HTML for .NET é uma biblioteca versátil que permite aos desenvolvedores trabalhar com documentos HTML de forma eficiente. Neste tutorial, cobrimos conceitos essenciais e fornecemos exemplos passo a passo para tarefas comuns, incluindo gerenciamento de scripts, personalização de folhas de estilo, controle de execução de JavaScript e manipulação de mensagens personalizadas.

Seguindo as etapas descritas neste tutorial, você pode aproveitar o poder do Aspose.HTML for .NET para criar, manipular e converter documentos HTML em seus aplicativos .NET com confiança.

## Perguntas frequentes

### Q1: Posso usar Aspose.HTML for .NET sem comprar uma licença?

A1: Sim, você pode experimentar o Aspose.HTML for .NET com uma versão de teste gratuita, mas alguns recursos avançados podem exigir uma licença válida.

### Q2: Como posso obter uma licença para Aspose.HTML for .NET?

 A2: Você pode comprar uma licença no site Aspose:[Adquira a licença Aspose.HTML](https://purchase.aspose.com/buy).

### Q3: Para quais formatos posso converter documentos HTML usando Aspose.HTML for .NET?

A3: Aspose.HTML for .NET suporta conversão para vários formatos, incluindo PDF, imagens e muito mais.

### Q4: Existe uma comunidade ou fórum de suporte para Aspose.HTML for .NET?

 A4: Sim, você pode encontrar ajuda e suporte nos fóruns do Aspose:[Fórum de suporte Aspose.HTML](https://forum.aspose.com/).

### Q5: O Aspose.HTML for .NET fornece documentação e tutoriais?

 A5: Sim, você pode acessar a documentação aqui:[Documentação Aspose.HTML para .NET](https://reference.aspose.com/html/net/).