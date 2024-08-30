---
title: Converter EPUB para PDF em .NET com Aspose.HTML
linktitle: Converter EPUB para PDF no .NET
second_title: Aspose.HTML .NET API de manipulação de HTML
description: Aprenda como converter EPUB para PDF usando Aspose.HTML para .NET. Este guia passo a passo abrange opções de personalização, FAQs e muito mais para conversão de documentos sem interrupções.
type: docs
weight: 12
url: /pt/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

Neste tutorial, exploraremos como usar o Aspose.HTML para .NET para converter arquivos EPUB em PDF. O Aspose.HTML é uma biblioteca .NET poderosa que fornece várias funcionalidades para trabalhar com documentos HTML e EPUB. Abordaremos os pré-requisitos, importaremos os namespaces necessários e detalharemos vários exemplos, explicando cada etapa em detalhes.

## Pré-requisitos

Antes de começar, certifique-se de ter os seguintes pré-requisitos em vigor:

1. Aspose.HTML para .NET: Certifique-se de ter o Aspose.HTML para .NET instalado em seu projeto .NET. Você pode baixá-lo de[aqui](https://releases.aspose.com/html/net/).

2. Seu diretório de dados: você precisará de um diretório de dados onde seus arquivos EPUB serão armazenados.

Agora, vamos mergulhar no processo passo a passo de conversão de EPUB em PDF usando o Aspose.HTML para .NET.

## Converter EPUB para PDF

### Etapa 1: inicialize seu projeto

Certifique-se de ter um projeto .NET configurado e que o Aspose.HTML para .NET esteja instalado.

### Etapa 2: Importar os namespaces necessários

No seu arquivo de código C#, importe os namespaces necessários:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### Etapa 3: Abra o arquivo EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continue para o próximo passo...
}
```

-  Substituir`"Your Data Directory"` com o diretório real onde seu arquivo EPUB está localizado.
- Este código abre o arquivo EPUB para leitura.

### Etapa 4: Defina as opções de PDF e execute a conversão

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Crie uma instância de`PdfSaveOptions` para especificar as configurações de conversão de PDF.
-  Use o`Converter.ConvertEPUB` método para converter EPUB em PDF com as opções fornecidas.
- Salve o PDF resultante como "output.pdf".

## Especificar opções de salvamento de PDF

### Etapa 1: inicialize seu projeto

Certifique-se de ter um projeto .NET configurado e o Aspose.HTML para .NET instalado.

### Etapa 2: Importar os namespaces necessários

Importe os namespaces necessários no seu código C#:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### Etapa 3: Abra o arquivo EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continue para o próximo passo...
}
```

-  Substituir`"Your Data Directory"` com o diretório real do seu arquivo EPUB.
- Abra o arquivo EPUB para leitura.

### Etapa 4: personalizar opções de PDF

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  Crie uma instância de`PdfSaveOptions` e personalizá-lo de acordo com suas necessidades.
- Neste exemplo, definimos o tamanho da página como 3000 pixels de largura e 1000 pixels de altura, e a cor de fundo como Azul Alice.

### Etapa 5: Realizar conversão

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Use o`Converter.ConvertEPUB` método para converter EPUB em PDF com opções personalizadas.
- Salve o PDF resultante como "output.pdf".

## Usar Provedor de Fluxo Personalizado

### Etapa 1: inicialize seu projeto

Configure um projeto .NET e instale o Aspose.HTML para .NET.

### Etapa 2: Importar os namespaces necessários

No seu código C#, importe os namespaces necessários:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### Etapa 3: Abra o arquivo EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continue para o próximo passo...
}
```

-  Substituir`"Your Data Directory"` com o diretório real do seu arquivo EPUB.
- Abra o arquivo EPUB para leitura.

### Etapa 4: Use um provedor de fluxo personalizado

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // Continue para o próximo passo...
}
```

-  Criar um`MemoryStreamProvider` para gerenciar o resultado da conversão como um fluxo de memória.
-  Use o`Converter.ConvertEPUB` método com o provedor de fluxo personalizado.

### Etapa 5: Salve o resultado

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- Acesse o fluxo de memória que contém os dados convertidos.
- Defina a posição do fluxo para o início.
- Crie um arquivo PDF de saída e copie o conteúdo do fluxo de memória para ele.

### Código-fonte da classe MemoryStreamProvider. 

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Lista de objetos MemoryStream criados durante a renderização do documento
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Este método é chamado quando apenas um fluxo de saída é necessário, por exemplo, para formatos XPS, PDF ou TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Este método é chamado quando a criação de múltiplos fluxos de saída é necessária. Por exemplo, durante a renderização de HTML para listar os arquivos de imagem (JPG, PNG, etc.)
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
Agora, você aprendeu como converter arquivos EPUB para PDF usando Aspose.HTML para .NET com várias opções e possibilidades de personalização. Aspose.HTML simplifica o processo, fornecendo flexibilidade e controle sobre a conversão do seu documento.

## Conclusão

Aspose.HTML para .NET é uma ferramenta versátil para converter arquivos EPUB em PDF, oferecendo opções de personalização para adaptar o documento PDF resultante às suas necessidades. Se você precisa de conversões simples ou personalização avançada, o Aspose.HTML tem tudo o que você precisa.

 Se ainda não o fez, você pode baixar o Aspose.HTML para .NET do[site](https://releases.aspose.com/html/net/) e comece a usá-lo em seus aplicativos .NET hoje mesmo.

---

## Perguntas frequentes

### O Aspose.HTML para .NET é gratuito?
    Aspose.HTML para .NET é um produto comercial, mas uma versão de avaliação gratuita está disponível[aqui](https://releases.aspose.com/).

### Posso personalizar a aparência do PDF convertido?
   Sim, você pode personalizar a aparência do PDF ajustando opções como tamanho da página e cor de fundo, conforme mostrado no Exemplo 2.

### Como posso obter suporte para Aspose.HTML para .NET?
    Você pode encontrar suporte e recursos no[Fórum Aspose.HTML](https://forum.aspose.com/).

### Existem outros formatos que posso converter com o Aspose.HTML para .NET?
   Sim, o Aspose.HTML para .NET suporta vários formatos de documento, incluindo HTML, EPUB e muito mais.

### O Aspose.HTML para ..NET é adequado para conversão de documentos em larga escala?
   O Aspose.HTML para .NET foi projetado para lidar com conversões de documentos em larga escala de forma eficiente, tornando-o adequado para uma ampla variedade de aplicações.

