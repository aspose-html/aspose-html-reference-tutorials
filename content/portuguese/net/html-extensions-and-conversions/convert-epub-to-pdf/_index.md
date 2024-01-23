---
title: Converta EPUB para PDF em .NET com Aspose.HTML
linktitle: Converta EPUB para PDF em .NET
second_title: API de manipulação de HTML Aspose.HTML .NET
description: Aprenda como converter EPUB em PDF usando Aspose.HTML para .NET. Este guia passo a passo cobre opções de personalização, perguntas frequentes e muito mais para uma conversão perfeita de documentos.
type: docs
weight: 12
url: /pt/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

Neste tutorial, exploraremos como usar Aspose.HTML for .NET para converter arquivos EPUB em PDF. Aspose.HTML é uma biblioteca .NET poderosa que oferece várias funcionalidades para trabalhar com documentos HTML e EPUB. Abordaremos os pré-requisitos, importaremos os namespaces necessários e detalharemos vários exemplos, explicando cada etapa detalhadamente.

## Pré-requisitos

Antes de começar, certifique-se de ter os seguintes pré-requisitos em vigor:

1. Aspose.HTML for .NET: Certifique-se de ter o Aspose.HTML for .NET instalado em seu projeto .NET. Você pode baixá-lo em[aqui](https://releases.aspose.com/html/net/).

2. Seu diretório de dados: você precisará de um diretório de dados onde seus arquivos EPUB sejam armazenados.

Agora, vamos mergulhar no processo passo a passo de conversão de EPUB em PDF usando Aspose.HTML para .NET.

## Converter EPUB em PDF

### Etapa 1: inicialize seu projeto

Certifique-se de ter um projeto .NET configurado e que o Aspose.HTML for .NET esteja instalado.

### Etapa 2: importar namespaces necessários

No seu arquivo de código C#, importe os namespaces necessários:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### Etapa 3: abra o arquivo EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continue para o próximo passo...
}
```

-  Substituir`"Your Data Directory"` com o diretório real onde seu arquivo EPUB está localizado.
- Este código abre o arquivo EPUB para leitura.

### Passo 4: Definir opções de PDF e realizar a conversão

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Crie uma instância de`PdfSaveOptions` para especificar as configurações de conversão de PDF.
-  Use o`Converter.ConvertEPUB` método para converter EPUB em PDF com as opções fornecidas.
- Salve o PDF resultante como “output.pdf”.

## Especifique as opções de salvamento de PDF

### Etapa 1: inicialize seu projeto

Certifique-se de ter um projeto .NET configurado e Aspose.HTML para .NET instalado.

### Etapa 2: importar namespaces necessários

Importe os namespaces necessários em seu código C#:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### Etapa 3: abra o arquivo EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continue para o próximo passo...
}
```

-  Substituir`"Your Data Directory"` com o diretório real do seu arquivo EPUB.
- Abra o arquivo EPUB para leitura.

### Passo 4: Personalize as opções de PDF

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  Crie uma instância de`PdfSaveOptions` e personalize-o de acordo com suas necessidades.
- Neste exemplo, definimos o tamanho da página para 3.000 pixels de largura e 1.000 pixels de altura, e a cor de fundo para Alice Blue.

### Etapa 5: realizar a conversão

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Use o`Converter.ConvertEPUB` método para converter EPUB em PDF com as opções personalizadas.
- Salve o PDF resultante como “output.pdf”.

## Use provedor de stream personalizado

### Etapa 1: inicialize seu projeto

Configure um projeto .NET e instale Aspose.HTML for .NET.

### Etapa 2: importar namespaces necessários

No seu código C#, importe os namespaces necessários:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### Etapa 3: abra o arquivo EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continue para o próximo passo...
}
```

-  Substituir`"Your Data Directory"` com o diretório real do seu arquivo EPUB.
- Abra o arquivo EPUB para leitura.

### Etapa 4: use um provedor de streaming personalizado

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // Continue para o próximo passo...
}
```

-  Criar uma`MemoryStreamProvider` para gerenciar o resultado da conversão como um fluxo de memória.
-  Use o`Converter.ConvertEPUB` método com o provedor de stream personalizado.

### Etapa 5: salve o resultado

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
Agora você aprendeu como converter arquivos EPUB em PDF usando Aspose.HTML for .NET com várias opções e possibilidades de personalização. Aspose.HTML simplifica o processo, proporcionando flexibilidade e controle sobre a conversão de documentos.

## Conclusão

Aspose.HTML for .NET é uma ferramenta versátil para converter arquivos EPUB em PDF, oferecendo opções de personalização para adaptar o documento PDF resultante às suas necessidades. Quer você precise de conversões simples ou personalização avançada, Aspose.HTML tem o que você precisa.

 Se ainda não o fez, você pode baixar Aspose.HTML para .NET no[local na rede Internet](https://releases.aspose.com/html/net/) e comece a usá-lo em seus aplicativos .NET hoje mesmo.

---

## Perguntas frequentes

### O uso do Aspose.HTML para .NET é gratuito?
    Aspose.HTML for .NET é um produto comercial, mas uma avaliação gratuita está disponível[aqui](https://releases.aspose.com/).

### Posso personalizar a aparência do PDF convertido?
   Sim, você pode personalizar a aparência do PDF ajustando opções como tamanho da página e cor de fundo, conforme mostrado no Exemplo 2.

### Como posso obter suporte para Aspose.HTML for .NET?
    Você pode encontrar suporte e recursos no site[Fórum Aspose.HTML](https://forum.aspose.com/).

### Existem outros formatos que posso converter com Aspose.HTML para .NET?
   Sim, Aspose.HTML for .NET oferece suporte a vários formatos de documentos, incluindo HTML, EPUB e muito mais.

### O Aspose.HTML for .NET é adequado para conversão de documentos em grande escala?
   Aspose.HTML for .NET foi projetado para lidar com conversões de documentos em grande escala com eficiência, tornando-o adequado para uma ampla gama de aplicações.

