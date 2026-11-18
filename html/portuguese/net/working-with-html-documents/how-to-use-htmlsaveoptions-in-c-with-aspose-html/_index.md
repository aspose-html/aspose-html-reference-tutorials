---
category: general
date: 2026-09-10
description: Aprenda a usar HtmlSaveOptions em C# para controlar estilos de fontes
  da web e salvar arquivos HTML com Aspose.HTML. Exemplo de código completo e dicas
  práticas incluídos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use htmlsaveoptions
- Aspose HTML library
- WebFontStyle flags
- HTMLDocument conversion
- C# save HTML
- Aspose.Html SaveOptions
language: pt
lastmod: 2026-09-10
og_description: Como usar HtmlSaveOptions em C# para habilitar estilos de fonte web
  em negrito e itálico ao salvar HTML com Aspose.HTML. Siga o exemplo completo e as
  dicas de boas práticas.
og_image_alt: Screenshot showing how to use HtmlSaveOptions to save an HTML file in
  C#
og_title: Como usar HtmlSaveOptions em C# com Aspose.HTML – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  headline: How to use HtmlSaveOptions in C# with Aspose.HTML
  type: TechArticle
- description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  name: How to use HtmlSaveOptions in C# with Aspose.HTML
  steps:
  - name: Why configure WebFontStyle?
    text: 'When you export an HTML document, Aspose.HTML can embed web fonts that
      match the original styling. By setting `WebFontStyle`, you tell the exporter
      which font variants to include. This reduces the final file size when you only
      need specific styles and guarantees that the rendered output matches the '
  - name: 5.1 Controlling CSS embedding
    text: 'You can decide whether to embed CSS inline, keep external links, or embed
      everything:'
  - name: 5.2 Saving to a specific encoding
    text: '```csharp saveOptions.Encoding = Encoding.UTF8; ```'
  - name: 5.3 Handling large documents
    text: 'For very large HTML files, consider streaming the output to avoid high
      memory consumption:'
  - name: 5.4 Error handling best practice
    text: 'Wrap the entire workflow in a try‑catch block and log the exception details.
      This ensures that any I/O or parsing errors are captured:'
  - name: Expected console output
    text: '``` HTML saved successfully to ''YOUR_DIRECTORY/output.html''. ```'
  type: HowTo
tags:
- Aspose.HTML
- C#
- HTML processing
title: Como usar HtmlSaveOptions em C# com Aspose.HTML
url: /pt/net/working-with-html-documents/how-to-use-htmlsaveoptions-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar HtmlSaveOptions em C# com Aspose.HTML

Se você precisa controlar como o Aspose.HTML salva um documento HTML, **aprender a usar HtmlSaveOptions é essencial**. Este tutorial mostra passo a passo como usar HtmlSaveOptions para habilitar estilos de fonte web em negrito e itálico ao salvar um documento.

A biblioteca Aspose HTML fornece uma API rica para carregar, manipular e exportar conteúdo HTML. Ao final deste guia você será capaz de:

* Carregar um arquivo HTML existente em um `HTMLDocument`.
* Configurar `HtmlSaveOptions` para aplicar flags específicas de `WebFontStyle`.
* Salvar o documento modificado em um novo local ou em um stream.
* Expandir a solução para outros estilos de fonte, CSS personalizado e tratamento de erros.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou posterior instalado.
* Uma licença válida para **Aspose.HTML for .NET** (a versão de avaliação gratuita funciona para este exemplo).
* Visual Studio 2022 (ou qualquer IDE C#) para compilar e executar o código.

Nenhum pacote NuGet adicional é necessário além do `Aspose.HTML`.

## Etapa 1: Configurar o projeto e importar namespaces

Crie um novo projeto **Console App** e adicione o pacote NuGet Aspose.HTML:

```bash
dotnet add package Aspose.HTML
```

Em seguida, no topo do `Program.cs`, importe os namespaces necessários:

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

Esses namespaces expõem os tipos `HTMLDocument`, `HtmlSaveOptions` e `WebFontStyle` que você usará ao longo do tutorial.

## Etapa 2: Carregar o documento HTML de origem

A primeira operação é ler o HTML que você deseja processar. Substitua `"YOUR_DIRECTORY/input.html"` pelo caminho real do seu arquivo.

```csharp
// Load the source HTML document from disk
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

`HTMLDocument` analisa a marcação, constrói uma árvore DOM e a deixa pronta para manipulação. Se o arquivo não existir, uma exceção será lançada, portanto, pode ser interessante envolver esta chamada em um bloco try‑catch em código de produção.

## Etapa 3: Criar e configurar HtmlSaveOptions

`HtmlSaveOptions` permite ajustar finamente o processo de salvamento. Para habilitar estilos de fonte web em negrito e itálico, combine as flags correspondentes de `WebFontStyle` usando o operador OR bit a bit (`|`).

```csharp
// Create a new HtmlSaveOptions instance
HtmlSaveOptions saveOptions = new HtmlSaveOptions();

// Enable bold and italic web‑font styles (equivalent to the old FontStyle flags)
saveOptions.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

### Por que configurar WebFontStyle?

Ao exportar um documento HTML, o Aspose.HTML pode incorporar fontes web que correspondam ao estilo original. Definindo `WebFontStyle`, você indica ao exportador quais variantes de fonte incluir. Isso reduz o tamanho final do arquivo quando você precisa apenas de estilos específicos e garante que a saída renderizada corresponda à fonte.

#### Variações comuns

| Estilo desejado | Flag `WebFontStyle` correspondente |
|-----------------|------------------------------------|
| Normal (regular) | `WebFontStyle.Regular` |
| Negrito | `WebFontStyle.Bold` |
| Itálico | `WebFontStyle.Italic` |
| Negrito + Itálico | `WebFontStyle.Bold | WebFontStyle.Italic` |
| Todas as variantes | `WebFontStyle.All` |

Você pode combinar qualquer combinação que se ajuste ao seu cenário.

## Etapa 4: Salvar o documento com as opções configuradas

Agora escreva o documento em um novo arquivo. O método `Save` aceita o caminho de destino e a instância de `HtmlSaveOptions` que você preparou.

```csharp
// Save the processed HTML using the configured options
document.Save("YOUR_DIRECTORY/output.html", saveOptions);
```

Se precisar escrever em um memory stream (por exemplo, para enviar o arquivo via HTTP), use a sobrecarga que aceita um objeto `Stream`:

```csharp
using (var stream = new MemoryStream())
{
    document.Save(stream, saveOptions);
    // Reset the position to read the content later
    stream.Position = 0;
    // Example: return the stream from a Web API endpoint
}
```

## Etapa 5: Verificar o resultado

Abra `output.html` em um navegador ou inspecione o arquivo com um editor de texto. Você deverá ver que o bloco `<style>` agora contém regras `@font-face` para as variantes negrito e itálico de quaisquer fontes web referenciadas no documento original.

**Trecho de saída esperado:**

```html
<link rel="stylesheet" href="fonts/Roboto-Bold.woff2" type="font/woff2">
<link rel="stylesheet" href="fonts/Roboto-Italic.woff2" type="font/woff2">
```

Se o HTML original referenciar uma família de fontes que possua apenas o peso regular, o Aspose.HTML incluirá apenas esse arquivo, respeitando a configuração de `WebFontStyle`.

## Avançado: Usando HtmlSaveOptions com recursos adicionais

### 5.1 Controlando a incorporação de CSS

Você pode decidir se deseja incorporar CSS inline, manter links externos ou incorporar tudo:

```csharp
saveOptions.CssSavingMode = CssSavingMode.EmbedAllCss;
```

### 5.2 Salvando com uma codificação específica

```csharp
saveOptions.Encoding = Encoding.UTF8;
```

### 5.3 Manipulando documentos grandes

Para arquivos HTML muito grandes, considere fazer streaming da saída para evitar alto consumo de memória:

```csharp
using (FileStream fs = new FileStream("large_output.html", FileMode.Create, FileAccess.Write))
{
    document.Save(fs, saveOptions);
}
```

### 5.4 Melhores práticas de tratamento de erros

Envolva todo o fluxo de trabalho em um bloco try‑catch e registre os detalhes da exceção. Isso garante que quaisquer erros de I/O ou de análise sejam capturados:

```csharp
try
{
    // Load, configure, and save as shown earlier
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error processing HTML: {ex.Message}");
}
```

## Dica profissional: Reutilizar HtmlSaveOptions em múltiplas gravações

Se precisar salvar vários documentos com a mesma configuração de estilo de fonte, crie uma única instância de `HtmlSaveOptions` e reutilize‑a. Isso reduz a sobrecarga de alocação de objetos e garante uma saída consistente.

```csharp
HtmlSaveOptions sharedOptions = new HtmlSaveOptions
{
    WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
    CssSavingMode = CssSavingMode.EmbedAllCss
};

foreach (var file in Directory.GetFiles("input_folder", "*.html"))
{
    HTMLDocument doc = new HTMLDocument(file);
    string outputPath = Path.Combine("output_folder", Path.GetFileName(file));
    doc.Save(outputPath, sharedOptions);
}
```

## Exemplo completo executável

Abaixo está o programa completo que incorpora todas as etapas discutidas. Copie‑o para `Program.cs` e execute‑o após ajustar os caminhos dos arquivos.

```csharp
using System;
using System.IO;
using System.Text;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath = "YOUR_DIRECTORY/input.html";
        string outputPath = "YOUR_DIRECTORY/output.html";

        try
        {
            // Step 1: Load the source HTML document
            HTMLDocument document = new HTMLDocument(inputPath);

            // Step 2: Create HtmlSaveOptions and enable bold + italic web‑font styles
            HtmlSaveOptions saveOptions = new HtmlSaveOptions
            {
                WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
                // Optional: embed all CSS and use UTF‑8 encoding
                CssSavingMode = CssSavingMode.EmbedAllCss,
                Encoding = Encoding.UTF8
            };

            // Step 3: Save the document with the configured options
            document.Save(outputPath, saveOptions);

            Console.WriteLine($"HTML saved successfully to '{outputPath}'.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### Saída esperada no console

```
HTML saved successfully to 'YOUR_DIRECTORY/output.html'.
```

Abra o `output.html` gerado para confirmar que os estilos de fonte web em negrito e itálico estão presentes.

## Conclusão

Agora você sabe **como usar HtmlSaveOptions** para controlar a incorporação de fontes web, o tratamento de CSS e a codificação ao salvar HTML com a biblioteca Aspose HTML em C#. Ao configurar as flags `WebFontStyle` você pode adaptar a saída para incluir apenas as variantes de fonte necessárias, melhorando o desempenho e reduzindo o tamanho do arquivo.

A partir daqui, você pode explorar outras propriedades de `HtmlSaveOptions` como `ImageSavingMode`, `JavaScriptSavingMode`, ou combinar múltiplas opções para pipelines de conversão complexas. Experimente salvar em streams para APIs web ou integrar o fluxo de trabalho em um sistema maior de geração de documentos.

---


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como salvar HTML com Aspose.Html – Guia completo em C#](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [Como usar Aspose para renderizar HTML em PNG em C#](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-in-c/)
- [Como usar Aspose para renderizar HTML em PNG – Guia passo a passo](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}