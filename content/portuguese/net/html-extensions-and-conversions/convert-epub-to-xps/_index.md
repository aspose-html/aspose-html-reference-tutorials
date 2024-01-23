---
title: Converta EPUB em XPS em .NET com Aspose.HTML
linktitle: Converter EPUB em XPS em .NET
second_title: API de manipulação de HTML Aspose.HTML .NET
description: Aprenda como converter EPUB em XPS em .NET usando Aspose.HTML para .NET. Siga nosso guia passo a passo para conversões sem esforço.
type: docs
weight: 13
url: /pt/net/html-extensions-and-conversions/convert-epub-to-xps/
---

Você está procurando uma maneira perfeita de converter arquivos EPUB para o formato XPS em seus aplicativos .NET? Aspose.HTML for .NET fornece uma solução poderosa para conseguir isso sem esforço. Neste guia passo a passo, orientaremos você no processo de conversão de EPUB em XPS usando Aspose.HTML. Vamos começar!

## Pré-requisitos

Antes de mergulhar no processo de conversão de EPUB em XPS, você precisará garantir que possui os seguintes pré-requisitos:

### 1. Biblioteca Aspose.HTML para .NET

 Certifique-se de ter a biblioteca Aspose.HTML for .NET instalada em seu projeto. Caso ainda não tenha feito isso, você pode obtê-lo no[Página de download do Aspose.HTML para .NET](https://releases.aspose.com/html/net/).

### 2. Arquivo EPUB de entrada

Você precisará de um arquivo EPUB que deseja converter para XPS. Certifique-se de ter um arquivo EPUB disponível para conversão.

### 3. Ambiente de desenvolvimento .NET

Este guia pressupõe que você tenha um ambiente de desenvolvimento .NET funcional configurado em sua máquina.

## Importar namespace

Para começar, você deve importar o namespace necessário para Aspose.HTML:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## Converter EPUB em XPS

Vamos dividir o processo de conversão de um arquivo EPUB para o formato XPS em várias etapas.

### Etapa 1.1: Abra o arquivo EPUB

Primeiro, abra o arquivo EPUB existente para leitura usando um FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continue com o processo de conversão
}
```

### Etapa 1.2: Criar XpsSaveOptions

Crie uma instância de XpsSaveOptions. Esta etapa é crucial para configurar a saída XPS:

```csharp
var options = new XpsSaveOptions();
```

### Etapa 1.3: Converter EPUB em XPS

Agora, vamos chamar o método ConvertEPUB para converter EPUB em XPS:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Especifique opções XPS personalizadas

Você pode personalizar ainda mais a saída XPS especificando opções personalizadas, como tamanho da página e cor de fundo.

### Etapa 2.1: tamanho de página personalizado e cor de fundo

Crie uma instância de XpsSaveOptions com tamanho de página e cor de fundo personalizados:

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### Etapa 2.2: Converter EPUB em XPS com opções personalizadas

Agora, chame o método ConvertEPUB para converter EPUB em XPS com as opções personalizadas:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Use provedor de stream personalizado

Nesta etapa, converteremos EPUB em XPS usando um provedor de stream personalizado, permitindo manipular os dados resultantes.

### Etapa 3.1: Crie um MemoryStreamProvider

Crie uma instância de MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Continue com o processo de conversão
}
```

### Etapa 3.2: Converter EPUB em XPS com Stream Provider

Converta EPUB em XPS usando MemoryStreamProvider:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Etapa 3.3: Acesse e salve o resultado

Recupere o fluxo de memória que contém os dados convertidos e salve-o em um arquivo de saída:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Código-fonte da classe MemoryStreamProvider

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Lista de objetos MemoryStream criados durante a renderização do documento
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Este método é chamado quando um único fluxo de saída é necessário, por exemplo para formatos XPS, PDF ou TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Este método é chamado quando é necessária a criação de vários fluxos de saída. Por exemplo, durante a renderização de HTML para listar os arquivos de imagem (JPG, PNG, etc.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Aqui você pode liberar o fluxo cheio de dados e, por exemplo, liberá-lo para o disco rígido
            }
            public void Dispose()
            {
                // Liberando recursos
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Parabéns! Você converteu com sucesso um arquivo EPUB para o formato XPS usando Aspose.HTML para .NET.

## Conclusão

Neste tutorial abrangente, exploramos como aproveitar o Aspose.HTML for .NET para converter arquivos EPUB para o formato XPS com várias opções de personalização. Quer você seja um desenvolvedor experiente ou esteja apenas começando, o Aspose.HTML simplifica o processo, permitindo que você lide com conversões de EPUB para XPS com facilidade.

 Tem alguma dúvida ou encontrou problemas? Confira a[Documentação Aspose.HTML](https://reference.aspose.com/html/net/) para obter mais informações ou procure ajuda do[Fórum da comunidade Aspose.HTML](https://forum.aspose.com/).

## perguntas frequentes

### O que é Aspose.HTML para .NET?
Aspose.HTML for .NET é uma biblioteca poderosa que permite aos desenvolvedores trabalhar com documentos HTML, EPUB e XPS em aplicativos .NET.

### Onde posso baixar o Aspose.HTML para .NET?
 Você pode baixar Aspose.HTML para .NET em[página de download](https://releases.aspose.com/html/net/).

### Existe uma avaliação gratuita disponível para Aspose.HTML for .NET?
 Sim, você pode obter um teste gratuito em[aqui](https://releases.aspose.com/).

### Como posso obter uma licença temporária do Aspose.HTML for .NET?
 Para obter uma licença temporária, visite o[página de licença temporária](https://purchase.aspose.com/temporary-license/).

### Onde posso encontrar mais tutoriais e documentação para Aspose.HTML for .NET?
 Explore uma ampla variedade de tutoriais e documentação detalhada sobre o[Documentação Aspose.HTML](https://reference.aspose.com/html/net/) página.