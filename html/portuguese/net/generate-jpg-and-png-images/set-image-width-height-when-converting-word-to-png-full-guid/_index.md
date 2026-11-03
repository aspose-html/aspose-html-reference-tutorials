---
category: general
date: 2026-05-22
description: Defina a largura e a altura da imagem ao converter um documento Word
  para PNG. Aprenda a exportar docx como imagem com renderização de alta qualidade
  em um tutorial passo a passo.
draft: false
keywords:
- set image width height
- convert word to png
- save docx as png
- export docx as image
- how to render word
language: pt
og_description: Defina a largura e a altura da imagem ao converter um documento Word
  para PNG. Este tutorial mostra como exportar um docx como imagem com configurações
  de alta qualidade.
og_title: Defina Largura e Altura da Imagem ao Converter Word para PNG – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-05-22'
  description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  headline: Set Image Width Height When Converting Word to PNG – Full Guide
  type: TechArticle
- description: Set image width height while converting a Word document to PNG. Learn
    how to export docx as image with high‑quality rendering in a step‑by‑step tutorial.
  name: Set Image Width Height When Converting Word to PNG – Full Guide
  steps:
  - name: 1. Preserve Transparent Backgrounds
    text: 'If your Word document contains shapes with transparent backgrounds and
      you want to keep that transparency, set the `BackgroundColor` to `Color.Transparent`:'
  - name: 2. Render Only a Specific Range
    text: Sometimes you only need a paragraph or a table, not the whole page. Use
      `DocumentVisitor` to extract the node and render it separately. That’s a more
      advanced scenario, but it shows **how to render word** content at a granular
      level.
  - name: 3. Adjust DPI Dynamically
    text: 'If you need different DPI per page (e.g., high‑resolution for the cover
      page), modify `Resolution` inside the loop:'
  - name: 4. Batch Processing
    text: When converting dozens of documents, wrap the whole flow in a method and
      reuse the same `ImageRenderingOptions` instance. Re‑using the options object
      reduces allocation overhead.
  type: HowTo
tags:
- Aspose.Words
- C#
- Image Rendering
title: Defina a Largura e Altura da Imagem ao Converter Word para PNG – Guia Completo
url: /pt/net/generate-jpg-and-png-images/set-image-width-height-when-converting-word-to-png-full-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir Largura e Altura da Imagem ao Converter Word para PNG – Guia Completo

Já se perguntou como **definir largura e altura da imagem** enquanto **converte Word para PNG**? Você não está sozinho. Muitos desenvolvedores se deparam com um obstáculo quando a exportação padrão gera uma imagem borrada ou com dimensões erradas, e então passam horas procurando uma solução que realmente funcione.

Neste tutorial, percorreremos uma solução limpa e de ponta a ponta que mostra **como renderizar documentos Word** como imagens PNG, permitindo que você **salve docx como PNG** com controle preciso de largura‑altura e antialiasing de alta qualidade. Ao final, você terá um trecho de código pronto para usar, uma compreensão sólida das opções da API e algumas dicas avançadas para evitar armadilhas comuns.

## O que você aprenderá

- Carregar um arquivo `.docx` usando Aspose.Words for .NET.
- **Definir largura e altura da imagem** com `ImageRenderingOptions`.
- **Exportar docx como imagem** (PNG) com antialiasing habilitado.
- Como **converter word para png** para uma única página ou todo o documento.
- Dicas para lidar com documentos grandes, considerações de DPI e caminhos de sistema de arquivos.

Sem ferramentas externas, sem complicações de linha de comando — apenas código C# puro que você pode inserir em qualquer projeto .NET.

---

## Pré-requisitos

Antes de mergulharmos, certifique‑se de que você tem o seguinte:

| Requirement | Why it matters |
|-------------|----------------|
| **.NET 6.0+** (or .NET Framework 4.7.2) | Aspose.Words suporta ambos, mas runtimes mais recentes oferecem melhor desempenho. |
| **Aspose.Words for .NET** NuGet package (`Install-Package Aspose.Words`) | Fornece a classe `Document` e o motor de renderização. |
| A **Word document** (`.docx`) you want to turn into a PNG. | A fonte que você irá converter. |
| Basic C# knowledge – you’ll understand `using` statements and object initialization. | Mantém a curva de aprendizado suave. |

Se você não tem o pacote NuGet, execute isto no Console do Gerenciador de Pacotes:

```powershell
Install-Package Aspose.Words
```

É isso — uma vez que o pacote esteja instalado, você está pronto para começar a codificar.

---

## Etapa 1: Carregar o Documento Fonte

A primeira coisa que você precisa fazer é apontar a biblioteca para o arquivo Word que deseja transformar.

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Load the .docx file from disk
Document doc = new Document(@"C:\MyFiles\input.docx");
```

**Por que isso importa:** A classe `Document` lê todo o pacote Word na memória, dando acesso a páginas, estilos e tudo mais. Se o caminho estiver errado, você receberá uma `FileNotFoundException`, então verifique se o arquivo existe e se o caminho usa barras invertidas escapadas (`\\`) ou uma string literal (`@`).  

> **Dica profissional:** Envolva a chamada de carregamento em um bloco `try/catch` se você esperar que o arquivo possa estar ausente em tempo de execução.

---

## Etapa 2: Configurar Opções de Renderização de Imagem (Definir Largura e Altura da Imagem)

Agora vem o coração do tutorial: **como definir largura e altura da imagem** para que o PNG resultante não fique esticado ou pixelado. A classe `ImageRenderingOptions` oferece controle detalhado sobre dimensões, DPI e suavização.

```csharp
// Create rendering options and explicitly set width and height
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Desired output size in pixels
    Width = 1024,          // Set image width height: 1024px wide
    Height = 768,          // Set image width height: 768px tall

    // High‑quality antialiasing works on Windows, Linux, and macOS
    UseAntialiasing = true,

    // Optional: increase DPI for sharper output (default is 96)
    Resolution = 300
};
```

**Explicação das propriedades principais:**

- `Width` e `Height` – Estas são as dimensões exatas em pixels que você deseja. Ao defini-las, você **define largura e altura da imagem** diretamente, sobrescrevendo o tamanho padrão da página.
- `UseAntialiasing` – Habilita suavização de alta qualidade para texto e gráficos vetoriais, o que é crucial quando você **converte word para png** e deseja bordas nítidas.
- `Resolution` – DPI mais alto gera mais detalhes, especialmente em layouts complexos. Fique atento ao uso de memória; uma imagem de 300 DPI pode ser grande.

> **Por que não confiar apenas no tamanho padrão?** O padrão usa as dimensões físicas da página (por exemplo, A4 a 96 DPI). Isso frequentemente produz uma imagem de 794 × 1123 pixels — adequado para alguns casos, mas não quando você precisa de uma miniatura de UI específica ou de uma pré‑visualização de tamanho fixo.

---

## Etapa 3: Renderizar e Salvar como PNG (Exportar Docx como Imagem)

Com o documento carregado e as opções configuradas, você pode finalmente **exportar docx como imagem**. O método `RenderToImage` faz o trabalho pesado.

```csharp
// Render the first page (page index 0) to a PNG file
doc.RenderToImage(@"C:\MyFiles\output.png", imageOptions);
```

Se você quiser renderizar **todo o documento** (todas as páginas) em arquivos PNG separados, faça um loop sobre a coleção de páginas:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string outPath = $@"C:\MyFiles\page_{i + 1}.png";
    doc.RenderToImage(outPath, imageOptions, i);
}
```

**O que está acontecendo nos bastidores?** O renderizador rasteriza cada página usando as dimensões que você forneceu, aplica antialiasing e grava um fluxo de bytes PNG no disco. Como o PNG é sem perdas, você mantém a fidelidade total do layout original do Word.

**Saída esperada:** Um arquivo PNG nítido exatamente de 1024 × 768 pixels (ou o tamanho que você definiu). Abra‑o em qualquer visualizador de imagens e você verá o conteúdo do Word renderizado exatamente como aparece no documento original, mas agora como uma imagem bitmap.

---

## Dicas Avançadas e Variações

### 1. Preservar Fundos Transparentes

Se o seu documento Word contém formas com fundos transparentes e você deseja manter essa transparência, defina `BackgroundColor` como `Color.Transparent`:

```csharp
imageOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### 2. Renderizar Apenas um Intervalo Específico

Às vezes você precisa apenas de um parágrafo ou de uma tabela, não da página inteira. Use `DocumentVisitor` para extrair o nó e renderiz‑lo separadamente. Esse é um cenário mais avançado, mas demonstra **como renderizar word** em nível granular.

### 3. Ajustar DPI Dinamicamente

Se você precisar de DPI diferente por página (por exemplo, alta resolução para a capa), modifique `Resolution` dentro do loop:

```csharp
if (i == 0) imageOptions.Resolution = 600; // cover page
else imageOptions.Resolution = 300;
```

### 4. Processamento em Lote

Ao converter dezenas de documentos, envolva todo o fluxo em um método e reutilize a mesma instância de `ImageRenderingOptions`. Reutilizar o objeto de opções reduz a sobrecarga de alocação.

---

## Armadilhas Comuns e Como Evitá‑las

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| PNG está borrado apesar de DPI alto | `UseAntialiasing` deixado como `false` | Defina `UseAntialiasing = true`. |
| Tamanho de saída não corresponde a `Width`/`Height` | DPI não considerado | Multiplique o tamanho desejado por `Resolution / 96` ou ajuste `Resolution`. |
| Exceção Out‑of‑memory em documentos grandes | Renderizando todo o documento a 300 DPI | Renderize uma página por vez, descarte cada imagem após salvar. |
| PNG mostra fundo branco em imagens transparentes | `BackgroundColor` não definido | Defina `imageOptions.BackgroundColor = Color.Transparent`. |

---

## Exemplo Completo Funcionando

Abaixo está um programa autônomo que você pode copiar e colar em um aplicativo console. Ele demonstra **converter word para png**, **salvar docx como png**, e claro **definir largura e altura da imagem**.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;
using System.Drawing; // For Color

namespace WordToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            string inputPath = @"C:\MyFiles\input.docx";
            Document doc = new Document(inputPath);

            // 2️⃣ Configure rendering options (set image width height)
            ImageRenderingOptions options = new ImageRenderingOptions
            {
                Width = 1024,          // Desired pixel width
                Height = 768,          // Desired pixel height
                UseAntialiasing = true,
                Resolution = 300,
                BackgroundColor = Color.Transparent // Keep transparency if needed
            };

            // 3️⃣ Render the first page to PNG (export docx as image)
            string outputPath = @"C:\MyFiles\output.png";
            doc.RenderToImage(outputPath, options);

            Console.WriteLine($"✅ Document rendered successfully to {outputPath}");
            // Optional: render all pages
            //RenderAllPages(doc, options);
        }

        // Helper method for batch rendering (uncomment if needed)
        static void RenderAllPages(Document doc, ImageRenderingOptions options)
        {
            for (int i = 0; i < doc.PageCount; i++)
            {
                string pagePath = $@"C:\MyFiles\page_{i + 1}.png";
                doc.RenderToImage(pagePath, options, i);
                Console.WriteLine($"Page {i + 1} saved to {pagePath}");
            }
        }
    }
}
```

**Execute:** Compile o projeto, coloque um `input.docx` válido no caminho que você especificou e execute. Você deverá ver um `output.png` exatamente **1024 × 768** pixels, renderizado com bordas suaves.

---

## Tutoriais Relacionados

- [Como Habilitar Antialiasing ao Converter DOCX para PNG/JPG](/html/english/net/generate-jpg-and-png-images/how-to-enable-antialiasing-when-converting-docx-to-png-jpg/)
- [converter docx para png – tutorial de criação de arquivo zip em C#](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)
- [Como Usar Aspose para Renderizar HTML em PNG – Guia Passo a Passo](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}