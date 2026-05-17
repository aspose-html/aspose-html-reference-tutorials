---
category: general
date: 2026-04-06
description: Aprenda como habilitar antialiasing, definir a largura e a altura da
  imagem e salvar o documento como PNG em C# – um guia rápido para exportar o documento
  como imagem.
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: pt
og_description: Como habilitar o antialiasing ao exportar um documento para uma imagem.
  Este guia mostra como definir a largura da imagem, definir a altura da imagem e
  salvar o documento como PNG.
og_title: Como habilitar antialiasing – Exportar documento para imagem
tags:
- C#
- ImageRendering
- Antialiasing
title: Como habilitar o antialiasing – Exportar documento para imagem com C#
url: /pt/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como habilitar antialiasing – Exportar documento para imagem em C#

Já se perguntou **como habilitar antialiasing** ao transformar um documento em uma imagem? Talvez você tenha tentado uma chamada rápida `Save` e o resultado ficou serrilhado, especialmente em linhas diagonais. A boa notícia é que você não precisa ser um mago da gráfica — basta algumas linhas de C# e as opções corretas.

Neste tutorial, vamos percorrer a definição da largura da imagem, a definição da altura da imagem e, finalmente, **salvar documento como PNG** para que você possa **exportar documento para imagem** com bordas suaves. Ao final, você terá um trecho pronto‑para‑executar que produz um PNG nítido de 800 × 600 com antialiasing ativado.

## Pré-requisitos

- .NET 6.0 ou posterior (o código também funciona no .NET Framework 4.7+)
- Uma referência a uma biblioteca de renderização que suporte `ImageRenderingOptions` (por exemplo, Aspose.Words, Syncfusion ou qualquer API que exponha propriedades semelhantes)
- Um entendimento básico da sintaxe C#

Nenhuma configuração pesada — basta adicionar o pacote NuGet e você está pronto para usar.

## Etapa 1: Instalar a Biblioteca de Renderização

Primeiro, adicione o pacote ao seu projeto. Se você estiver usando Aspose.Words, execute:

```bash
dotnet add package Aspose.Words
```

> **Dica profissional:** Mantenha a versão da biblioteca atualizada; a versão mais recente (a partir de abril de 2026) adiciona ajustes de desempenho para antialiasing.

## Etapa 2: Criar o Objeto Document

Carregue ou crie o documento que deseja renderizar. Aqui está um exemplo mínimo que cria um documento de uma página com um parágrafo simples:

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

A classe `Document` é o ponto de entrada; tudo o que você renderiza provém dela. Em projetos reais, você provavelmente carregará um .docx existente:

```csharp
// Document doc = new Document("input.docx");
```

## Etapa 3: Definir Opções de Renderização (Largura, Altura, Antialiasing)

Agora respondemos à pergunta principal: **como habilitar antialiasing**. O objeto `ImageRenderingOptions` permite alternar o suavização e controlar as dimensões.

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

Observe os comentários: eles mencionam explicitamente **set image width**, **set image height** e **UseAntialiasing** — os três controles que mais importam quando você deseja um PNG refinado.

### Por que o Antialiasing é Importante

Sem antialiasing, linhas diagonais e curvas aparecem em degraus porque o renderizador trata cada pixel como ligado ou desligado. Ao habilitá‑lo, os pixels das bordas são mesclados, produzindo um suavização visual que imita o que você veria em um editor de fotos. O trade‑off é um pequeno aumento no tempo de processamento, mas para a maioria das exportações voltadas para UI isso é insignificante.

## Etapa 4: Salvar Documento como PNG (Exportar Documento para Imagem)

Com as opções prontas, finalmente **salvamos o documento como PNG**. O método `Save` recebe o caminho do arquivo e as opções que configuramos.

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

É isso — seu documento agora é um PNG de 800 × 600 com antialiasing aplicado. Se você abrir `output.png` verá texto nítido, linhas suaves e nenhum artefato serrilhado.

### Verificando o Resultado

Você pode verificar rapidamente o arquivo em qualquer visualizador de imagens. Procure por:

- Dimensões corretas (800 × 600)
- Nenhuma borda em degraus visível no texto ou em quaisquer formas
- Um fundo transparente se o seu documento não continha cor de fundo (a maioria das bibliotecas usa branco como padrão)

Se a imagem parecer serrilhada, verifique novamente se `UseAntialiasing = true` não está sendo sobrescrito em outro lugar.

## Etapa 5: Casos de Borda & Variações

### Alterando o Formato de Saída

Quer um JPEG em vez de PNG? Basta mudar a extensão do arquivo e, opcionalmente, ajustar a compressão:

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### Exportando Múltiplas Páginas

Quando o documento de origem tem várias páginas, o renderizador cria arquivos de imagem separados por página por padrão. Você pode percorrer as páginas:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### Salvando em um Stream (por exemplo, resposta HTTP)

Se você estiver construindo uma API web, pode querer retornar o PNG diretamente:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## Exemplo Completo Funcional

Abaixo está o programa completo, pronto para copiar e colar, que incorpora todas as etapas discutidas:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

Executar este programa gera `output.png` na pasta do executável. Abra-o, e você verá um PNG suave de 800 × 600 — exatamente o que pretendíamos alcançar.

## Perguntas Frequentes & Solução de Problemas

- **E se a imagem parecer borrada?**  
  A borrado pode acontecer quando você aumenta uma página de origem pequena. Mantenha o tamanho da página de origem próximo às dimensões alvo, ou aumente o DPI via `imageOptions.Resolution` (por exemplo, `Resolution = 300`).

- **Isso funciona no .NET Framework?**  
  Sim. A mesma API existe no framework clássico; basta referenciar o DLL apropriado.

- **Posso controlar a cor de fundo?**  
  Absolutamente. Defina `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` antes de salvar.

- **O antialiasing é acelerado por hardware?**  
  A maioria das bibliotecas realiza antialiasing por software. Se você precisar de aceleração GPU, procure um motor de renderização que suporte isso explicitamente.

## Conclusão

Cobremos **como habilitar antialiasing** ao **exportar documento para imagem**, percorrendo **set image width** e **set image height**, e mostramos os passos exatos para **save document as PNG**. O trecho acima está pronto para produção, e agora você pode adaptá‑lo para JPEG, PDFs de várias páginas ou até mesmo transmitir a imagem diretamente para um cliente.

Em seguida, você pode explorar a adição de marcas d'água, ajustar o DPI para saída de qualidade de impressão, ou integrar essa lógica em um endpoint ASP.NET Core. Os mesmos princípios se aplicam — basta trocar o caminho do arquivo por um stream de resposta.

Feliz codificação, e aproveite essas imagens nítidas e antialiased!

![PNG renderizado com antialiasing habilitado](output.png "PNG renderizado com antialiasing habilitado")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}