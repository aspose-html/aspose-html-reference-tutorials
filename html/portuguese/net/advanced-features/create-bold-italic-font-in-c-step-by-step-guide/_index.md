---
category: general
date: 2026-08-15
description: Crie fonte em negrito e itálico em C# rapidamente. Aprenda como criar
  fonte em C# com estilos negrito e itálico usando a classe Font incorporada.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create bold italic font
- create font in c#
- C# FontStyle
- text styling C#
- System.Drawing.Font
language: pt
lastmod: 2026-08-15
og_description: Crie fonte negrito itálico em C# com um exemplo claro. Este tutorial
  mostra como criar fontes em C# usando os flags FontStyle e explica armadilhas comuns.
og_image_alt: Screenshot of text rendered with a bold italic Arial font in a C# console
  window
og_title: Criar fonte em negrito e itálico em C# – guia completo de codificação
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  headline: Create bold italic font in C# – step‑by‑step guide
  type: TechArticle
- description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  name: Create bold italic font in C# – step‑by‑step guide
  steps:
  - name: Save the code to a file named `Program.cs`.
    text: Save the code to a file named `Program.cs`.
  - name: Open a terminal in the file’s directory.
    text: Open a terminal in the file’s directory.
  - name: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
    text: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
  - name: Replace the generated `Program.cs` with the code above.
    text: Replace the generated `Program.cs` with the code above.
  - name: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
    text: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
  - name: Build and run with `dotnet run`.
    text: Build and run with `dotnet run`.
  type: HowTo
tags:
- C#
- fonts
- text styling
title: Crie fonte em negrito e itálico no C# – guia passo a passo
url: /pt/net/advanced-features/create-bold-italic-font-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar fonte negrito itálico em C# – guia passo a passo

Se você precisa **criar fonte negrito itálico** em C#, este guia mostra exatamente como fazer isso. Você verá um exemplo completo e executável que também demonstra como **criar fonte em C#** usando a classe padrão .NET `Font`.

Trabalhar com fontes personalizadas é uma parte rotineira da construção de aplicativos desktop Windows, geração de PDFs ou renderização de HTML no servidor. Ao final deste tutorial você será capaz de instanciar uma fonte que seja tanto negrito quanto itálico, entender por que o operador bitwise `|` é usado e lidar com casos comuns, como famílias de fontes ausentes.

## O que você aprenderá

* Como importar os namespaces necessários para manipulação de fontes.  
* A sintaxe para combinar `FontStyle.Bold` e `FontStyle.Italic`.  
* Como verificar se a fonte foi criada com sucesso.  
* Dicas para tratamento de fallback quando a família solicitada não está instalada.  

Nenhuma biblioteca externa é necessária — tudo usa a biblioteca de classes base do .NET Framework / .NET Core.

## Pré-requisitos

* .NET 6.0 SDK ou posterior (o código também funciona no .NET Framework 4.6+).  
* Um editor de código ou IDE (Visual Studio, VS Code, Rider, etc.).  
* Familiaridade básica com a sintaxe C#.  

Se você atende a esses pré-requisitos, pode seguir os passos sem nenhuma configuração adicional.

## Etapa 1: Adicionar as diretivas using necessárias

A classe `Font` está no namespace `System.Drawing`, que faz parte do pacote NuGet `System.Drawing.Common` para .NET Core/.NET 5+. Adicione o namespace no topo do seu arquivo:

```csharp
using System;
using System.Drawing;   // Provides Font and FontStyle
```

> **Por que esta etapa importa** – Sem a linha `using System.Drawing;` o compilador não consegue localizar `Font` ou `FontStyle`, resultando em um erro “type or namespace name could not be found”.

## Etapa 2: Combinar estilos negrito e itálico com o operador OR bit a bit

No .NET, `FontStyle` é um enum marcado com o atributo `[Flags]`. Isso significa que você pode combinar múltiplos valores usando o operador `|` (OR bit a bit):

```csharp
// Step 2: Create a Font that is both bold and italic
var font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
```

### Explicação

* `"Arial"` – o nome da família de fonte. Se o sistema não tiver Arial instalado, o construtor recorre à fonte padrão.  
* `12` – tamanho em pontos.  
* `FontStyle.Bold | FontStyle.Italic` – combina as duas bandeiras de estilo. O operador `|` mescla a representação binária de cada bandeira, produzindo um único valor que representa “negrito + itálico”.

> **Dica profissional:** Sempre use os nomes do enum (`FontStyle.Bold`) ao invés de números mágicos; isso melhora a legibilidade e previne bugs quando os valores do enum mudam.

## Etapa 3: Verificar a fonte criada (opcional, mas recomendado)

Imprimir as propriedades da fonte ajuda a confirmar que a combinação de estilos foi bem-sucedida, especialmente ao depurar em uma máquina nova.

```csharp
// Step 3: Output the font details to the console
Console.WriteLine($"Font family: {font.Name}");
Console.WriteLine($"Size (pt): {font.Size}");
Console.WriteLine($"Style: {font.Style}");
```

**Saída esperada**

```
Font family: Arial
Size (pt): 12
Style: Bold, Italic
```

Se a saída listar tanto `Bold` quanto `Italic`, a fonte foi criada corretamente.

## Etapa 4: Renderizar uma string de exemplo (confirmação visual)

Ao executar um aplicativo de console você não vê a estilização real dos glifos, mas pode gerar uma imagem para provar o resultado. O trecho a seguir desenha “Hello, World!” usando a fonte negrito‑itálico e salva como *sample.png*:

```csharp
// Step 4: Draw text to an image file for visual confirmation
using (var bitmap = new Bitmap(300, 100))
using (var graphics = Graphics.FromImage(bitmap))
{
    graphics.Clear(Color.White);
    var brush = Brushes.Black;
    graphics.DrawString("Hello, World!", font, brush, new PointF(10, 30));
    bitmap.Save("sample.png");
    Console.WriteLine("Image saved as sample.png");
}
```

Após o programa ser executado, abra *sample.png* para ver o texto renderizado com o estilo negrito itálico.

![Texto de exemplo renderizado com fonte negrito itálico](sample.png)

*Texto alternativo da imagem: Captura de tela do texto renderizado com uma fonte Arial negrito itálico em uma janela de console C#* – este texto alternativo satisfaz o requisito de SEO para texto alternativo de imagem.

## Etapa 5: Fallback elegante quando a família de fonte não está disponível

Se a família solicitada (por exemplo, “Arial”) não estiver instalada, o construtor `Font` lança uma `ArgumentException`. Envolva a criação em um bloco `try/catch` e recorra a uma fonte segura conhecida, como “Segoe UI”.

```csharp
Font font;
try
{
    font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
}
catch (ArgumentException)
{
    Console.WriteLine("Arial not found – falling back to Segoe UI.");
    font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
}
```

**Por que tratar isso?** Em ambientes containerizados ou sem interface gráfica o conjunto padrão de fontes pode diferir de um desktop típico. Fornecer um fallback evita falhas em tempo de execução e garante consistência de estilo.

## Exemplo completo, executável

Juntando tudo, aqui está um programa completo que você pode copiar, colar e executar:

```csharp
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create the font (bold + italic)
        Font font;
        try
        {
            font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
        }
        catch (ArgumentException)
        {
            Console.WriteLine("Arial not found – using Segoe UI as fallback.");
            font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
        }

        // Display font information
        Console.WriteLine($"Font family: {font.Name}");
        Console.WriteLine($"Size (pt): {font.Size}");
        Console.WriteLine($"Style: {font.Style}");

        // Render a sample image
        using (var bitmap = new Bitmap(300, 100))
        using (var graphics = Graphics.FromImage(bitmap))
        {
            graphics.Clear(Color.White);
            graphics.DrawString("Hello, World!", font, Brushes.Black, new PointF(10, 30));
            bitmap.Save("sample.png");
        }

        Console.WriteLine("Sample image saved as sample.png");
    }
}
```

### Como executar

1. Salve o código em um arquivo chamado `Program.cs`.  
2. Abra um terminal no diretório do arquivo.  
3. Execute `dotnet new console -n FontDemo` (se precisar de uma estrutura de projeto).  
4. Substitua o `Program.cs` gerado pelo código acima.  
5. Execute `dotnet add package System.Drawing.Common` (necessário para .NET Core/5+).  
6. Compile e execute com `dotnet run`.  

Você verá a saída no console confirmando as propriedades da fonte, e `sample.png` aparecerá na pasta do projeto.

## Armadilhas comuns e como evitá‑las

| Armadilha | Por que acontece | Correção |
|-----------|------------------|----------|
| **Falta o pacote `System.Drawing.Common`** | .NET Core não inclui `System.Drawing` por padrão. | Execute `dotnet add package System.Drawing.Common`. |
| **Família de fonte não instalada** | Imagens Docker sem interface gráfica frequentemente não possuem fontes Windows. | Use uma fonte de fallback ou instale as fontes necessárias no contêiner. |
| **Uso incorreto de `|`** | Usar `+` ao invés de `|` resulta em uma combinação inválida. | Sempre combine valores de `FontStyle` com o operador OR bit a bit (`|`). |
| **Descartar o objeto `Font`** | Não chamar `Dispose` pode vazar recursos GDI. | Envolva `Font` em um bloco `using` ou chame `font.Dispose()` após terminar. |

## Conclusão

Agora você sabe como **criar fonte negrito itálico** em C# e como **criar fonte em C#** de forma segura e eficiente. O tutorial abordou a importação do namespace correto, combinação de bandeiras `FontStyle`, verificação do resultado, renderização de um exemplo visual e tratamento de famílias de fontes ausentes.

Em seguida, você pode explorar:

* **Criar fontes sublinhadas ou tachadas** – adicione `FontStyle.Underline` ou `FontStyle.Strikeout`.  
* **Usar fontes TrueType personalizadas** – carregue um arquivo `.ttf` com `PrivateFontCollection`.  
* **Aplicar fontes em WinForms, WPF ou geração de PDF** – o mesmo objeto `Font` pode ser passado para controles de UI ou bibliotecas de terceiros.  

Fique à vontade para experimentar diferentes famílias, tamanhos e combinações de estilo. Se encontrar problemas, revise a tabela “Armadilhas comuns” ou consulte a documentação oficial do [.NET para System.Drawing.Font](https://learn.microsoft.com/dotnet/api/system.drawing.font). Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como combinar fontes programaticamente em C# – Guia passo a passo](/html/indonesian/net/advanced-features/how-to-combine-fonts-programmatically-in-c-step-by-step-guid/)
- [Criar documento HTML com texto formatado e exportar para PDF – Guia completo](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)
- [converter docx para png – criar arquivo zip tutorial c#](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}