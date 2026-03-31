---
category: general
date: 2026-02-19
description: Crie imagem a partir de HTML rapidamente com Aspose.HTML em C#. Aprenda
  como renderizar HTML em imagem, converter HTML para PNG, definir dimensões da imagem
  e definir tamanho de fonte personalizado.
draft: false
keywords:
- create image from html
- render html to image
- convert html to png
- set image dimensions
- set custom font size
language: pt
og_description: Crie imagem a partir de HTML usando Aspose.HTML. Este guia mostra
  como renderizar HTML para imagem, converter HTML em PNG e definir as dimensões da
  imagem com tamanho de fonte personalizado.
og_title: Criar Imagem a partir de HTML em C# – Tutorial Completo
tags:
- Aspose.HTML
- C#
- Image Rendering
title: Criar imagem a partir de HTML em C# – Guia passo a passo
url: /pt/net/generate-jpg-and-png-images/create-image-from-html-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crie Imagem a partir de HTML em C# – Guia Passo a Passo

Já precisou **criar imagem a partir de HTML** mas não sabia qual biblioteca entregaria resultados pixel‑perfeitos? Você não está sozinho. No mundo .NET, o Aspose.HTML facilita **renderizar HTML para imagem**, permitindo transformar qualquer marcação em PNG, JPEG ou até BMP com apenas algumas linhas de código.

Neste tutorial vamos percorrer um exemplo completo e executável que mostra como **converter HTML para PNG**, como **definir dimensões da imagem** e como **definir tamanho de fonte personalizado** para controle tipográfico perfeito. Ao final, você terá um programa autônomo que pode ser inserido em qualquer projeto C#.

## O que Você Precisa

- **.NET 6+** (o código também funciona com .NET Framework 4.6+)
- **Aspose.HTML for .NET** – você pode obtê‑lo no NuGet (`Install-Package Aspose.HTML`)
- Um arquivo HTML simples (`input.html`) que você deseja transformar em imagem
- Uma IDE ou editor de sua preferência (Visual Studio, Rider, VS Code…)

Nenhuma outra ferramenta de terceiros é necessária. A biblioteca inclui seu próprio motor de renderização, portanto você não precisará de um navegador headless ou serviços externos.

---

## Etapa 1: Carregar o Documento HTML que Você Quer Renderizar

A primeira coisa que fazemos é ler o HTML de origem. A classe `HTMLDocument` do Aspose.HTML pode carregar um arquivo, uma URL ou até uma string bruta.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Rendering.Image;

// Load the HTML file from disk
HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

// Verify that the document is loaded (optional sanity check)
if (htmlDoc == null)
{
    throw new InvalidOperationException("Failed to load the HTML document.");
}
```

**Por que isso importa:** Carregar o documento fornece ao renderizador um DOM para trabalhar. Se você pular esta etapa, não haverá nada para pintar na tela, e a saída ficará em branco.

---

## Etapa 2: Definir o Estilo da Fonte com a Nova API `WebFontStyle`

Se precisar de um peso ou estilo de fonte específico—por exemplo **negrito itálico**—você pode usar `WebFontStyle`. É aqui que também atendemos ao requisito de **definir tamanho de fonte personalizado** mais adiante.

```csharp
// Create a WebFontStyle object to control weight and style
WebFontStyle webFontStyle = new WebFontStyle
{
    Weight = FontWeight.Bold,          // Makes the text bold
    Style  = FontStyleEnum.Italic      // Makes the text italic
};
```

**Dica de especialista:** A API `WebFontStyle` funciona com qualquer fonte web‑segura ou uma fonte que você incorpore via `@font-face`. Se precisar de uma tipografia não padrão, basta **referenciá‑la** no seu HTML que o Aspose.HTML a buscará automaticamente.

---

## Etapa 3: Configurar Opções de Renderização de Texto (Incluindo Tamanho de Fonte Personalizado)

Agora indicamos ao renderizador como desenhar o texto. Este é o ponto onde **definimos tamanho de fonte personalizado** e aplicamos o estilo que criamos.

```csharp
// Configure text rendering options
TextOptions textRenderOptions = new TextOptions
{
    FontFamily = "Arial",          // Fallback generic font
    FontSize   = 14,               // Custom font size in points
    FontStyle  = webFontStyle      // Apply bold‑italic style
};
```

**Por que esta etapa é crucial:** Sem definir explicitamente `FontSize`, o renderizador recorre ao tamanho definido no HTML ou CSS. Sobrescrevê‑lo garante uma saída consistente, independentemente da marcação de origem.

---

## Etapa 4: Configurar Opções de Renderização de Imagem – Tamanho, Formato e Configurações de Texto

Aqui respondemos à pergunta **definir dimensões da imagem** e também decidimos o formato de saída (`PNG` neste caso). A classe `ImageRenderingOptions` une tudo.

```csharp
// Define the overall image rendering options
ImageRenderingOptions imageRenderOptions = new ImageRenderingOptions
{
    TextOptions   = textRenderOptions, // Attach the text options we built
    Width         = 800,               // Desired image width in pixels
    Height        = 600,               // Desired image height in pixels
    OutputFormat  = ImageFormat.Png    // Convert HTML to PNG
};
```

**Observação sobre casos extremos:** Se o seu HTML contiver elementos que excedam a largura/altura especificada, o Aspose.HTML recortará ou dimensionará automaticamente com base nas propriedades CSS `Background` e `Overflow`. Você também pode habilitar `PreserveAspectRatio` se preferir dimensionamento proporcional.

---

## Etapa 5: Renderizar o Documento HTML para um Arquivo de Imagem

Por fim, chamamos `RenderToImage`. Esta única linha realiza todo o trabalho pesado—layout, rasterização e gravação do arquivo.

```csharp
// Render the document and save it as a PNG file
htmlDoc.RenderToImage("YOUR_DIRECTORY/output.png", imageRenderOptions);

// Quick verification: open the file (optional, works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.png",
    UseShellExecute = true
});
```

Depois de executar o programa, você deverá ver `output.png` com as dimensões exatas (800 × 600) e o texto renderizado em **Arial negrito itálico de 14 pt**. A imagem representará fielmente o HTML original, incluindo cores CSS, bordas e imagens incorporadas.

---

## Exemplo Completo Funcional (Todas as Etapas Combinadas)

Abaixo está o programa completo, pronto para copiar e colar. Substitua `YOUR_DIRECTORY` pelo caminho real onde seu `input.html` está localizado.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Rendering.Image;

namespace HtmlToImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the HTML document
            HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");
            if (htmlDoc == null)
                throw new InvalidOperationException("Unable to load HTML document.");

            // 2️⃣ Define font style (bold + italic)
            WebFontStyle webFontStyle = new WebFontStyle
            {
                Weight = FontWeight.Bold,
                Style  = FontStyleEnum.Italic
            };

            // 3️⃣ Set custom font size and family
            TextOptions textRenderOptions = new TextOptions
            {
                FontFamily = "Arial",
                FontSize   = 14,
                FontStyle  = webFontStyle
            };

            // 4️⃣ Configure image size, format, and attach text options
            ImageRenderingOptions imageRenderOptions = new ImageRenderingOptions
            {
                TextOptions   = textRenderOptions,
                Width         = 800,
                Height        = 600,
                OutputFormat  = ImageFormat.Png
            };

            // 5️⃣ Render to PNG
            htmlDoc.RenderToImage("YOUR_DIRECTORY/output.png", imageRenderOptions);

            // Optional: open the generated image automatically
            System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
            {
                FileName = "YOUR_DIRECTORY/output.png",
                UseShellExecute = true
            });
        }
    }
}
```

**Saída esperada:** Um arquivo PNG chamado `output.png` que corresponde ao layout visual de `input.html`, com tamanho exatamente 800 × 600 px, e todo o texto exibido em Arial negrito itálico de 14 pt.

---

## Perguntas Frequentes & Casos Especiais

### E se o meu HTML referenciar CSS ou imagens externas?

O Aspose.HTML segue as mesmas regras de um navegador. Desde que os caminhos sejam acessíveis (URLs absolutas ou caminhos relativos corretos), o renderizador os baixará automaticamente. Se você executar o código em uma máquina sem acesso à internet, certifique‑se de que todos os recursos estejam armazenados localmente.

### Posso renderizar para JPEG ou BMP em vez de PNG?

Claro. Basta alterar `OutputFormat`:

```csharp
OutputFormat = ImageFormat.Jpeg   // For JPEG
// or
OutputFormat = ImageFormat.Bmp    // For BMP
```

Lembre‑se de que JPEG é com perdas, portanto o texto pode ficar ligeiramente borrado—PNG é a escolha mais segura para tipografia nítida.

### Como preservo a proporção original quando a largura do HTML é desconhecida?

Defina apenas uma dimensão (por exemplo, `Width = 800`) e deixe a outra como `0`. O Aspose.HTML calculará a altura automaticamente com base no layout renderizado.

```csharp
Width = 800,
Height = 0, // Auto‑calculate height
```

### E se eu precisar de um DPI (pontos por polegada) diferente?

Use a propriedade `Resolution` dentro de `ImageRenderingOptions`:

```csharp
Resolution = new Resolution(300) // 300 DPI for high‑quality prints
```

Um DPI maior gera arquivos maiores, mas com saída mais nítida—use quando planejar imprimir a imagem.

---

## 🎉 Conclusão

Agora você sabe como **criar imagem a partir de HTML** usando Aspose.HTML para .NET, cobrindo tudo, desde carregar a marcação até **renderizar HTML para imagem**, **converter HTML para PNG**, **definir dimensões da imagem** e **definir tamanho de fonte personalizado**. O código completo está pronto para ser executado, e as explicações fornecem o “porquê” de cada linha, permitindo que você adapte a solução a cenários mais complexos.

### Próximos Passos

- Experimente **formatos de saída diferentes** (JPEG, BMP, GIF) para observar como a compressão afeta a qualidade.
- Tente **incorporar fontes web personalizadas** via `@font-face` no seu HTML e veja como o Aspose.HTML as respeita.
- Combine esta técnica com **geração de PDF** para inserir imagens renderizadas diretamente em relatórios.
- Explore **opções avançadas de renderização** como anti‑aliasing, cores de fundo ou suporte a SVG.

Se encontrar algum problema, fique à vontade para deixar um comentário—bom código!

---

![Create image from HTML example](example-output.png "Create image from HTML – rendered PNG output")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}