---
category: general
date: 2025-12-29
description: Crie um documento HTML em C# e aprenda como definir a família de fontes,
  definir o tamanho da fonte e, em seguida, salvar o HTML como PDF ou converter HTML
  para PDF usando Aspose.HTML.
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: pt
og_description: Crie um documento HTML em C# e veja instantaneamente como definir
  a família da fonte, definir o tamanho da fonte, e então salvar o HTML como PDF ou
  converter HTML para PDF com Aspose.HTML.
og_title: Criar Documento HTML – Texto Estilizado e Exportação em PDF
tags:
- aspnet
- csharp
- pdf-generation
title: Criar documento HTML com texto formatado e exportar para PDF – Guia completo
url: /pt/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Documento HTML com Texto Estilizado e Exportar para PDF

Já precisou **criar documento HTML** rapidamente e transformá‑lo em PDF sem sair do seu código C#? Talvez você esteja construindo um motor de relatórios, um gerador de faturas ou apenas uma pré‑visualização rápida para usuários. A boa notícia é que você pode fazer isso em poucas linhas usando Aspose.HTML, e terá controle total sobre a família da fonte, o tamanho da fonte e até estilos negrito‑itálico.

Neste tutorial vamos percorrer todo o processo — desde a criação de um documento HTML em memória até a gravação dele como arquivo PDF. Ao final, você saberá exatamente como **definir família da fonte**, **definir tamanho da fonte** e **salvar HTML como PDF** (também conhecido como **converter HTML para PDF**) com um exemplo de código limpo e pronto para produção.

## O que você vai precisar

- .NET 6+ (a API funciona tanto com .NET Core quanto com .NET Framework)  
- Pacote NuGet Aspose.HTML for .NET (`Aspose.Html`) – instale via `dotnet add package Aspose.Html`  
- Uma pasta no disco onde o PDF gerado possa ser gravado  

Sem templates HTML extras, sem conversores externos, apenas C# puro.

![ilustração de criação de documento html](/images/create-html-document.png){alt="exemplo de criação de documento html"}

## Etapa 1: Criar o Documento HTML

Primeiro, precisamos de um objeto de documento HTML vazio. Pense nele como uma tela em branco onde você pintará seu parágrafo estilizado.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**Por que isso importa:** `HTMLDocument` fornece uma estrutura semelhante a DOM que pode ser manipulada programaticamente. Não é necessário lidar com strings brutas ou I/O de arquivos até o final.

## Etapa 2: Adicionar um Parágrafo e Definir Família da Fonte & Tamanho da Fonte

Agora vamos criar um elemento `<p>`, inserir algum texto e definir explicitamente a família da fonte e o tamanho. É aqui que as palavras‑chave **set font family** e **set font size** entram em ação.

```csharp
// Step 2 – create a <p> element with some sample text
HtmlElement paragraph = htmlDocument.CreateElement("p");
paragraph.InnerHtml = "Bold & Italic text";

// Define the base font style
paragraph.Style.FontFamily = "Arial";   // set font family
paragraph.Style.FontSize = "18px";      // set font size

// Attach the paragraph to the document body
body.AppendChild(paragraph);
```

**Dica de especialista:** Se precisar de um fallback seguro para web, pode fornecer uma lista separada por vírgulas como `"Arial, Helvetica, sans-serif"`; o navegador (ou Aspose) escolherá a primeira fonte disponível.

## Etapa 3: Aplicar Estilos Negrito e Itálico com Flags WebFontStyle

Aspose.HTML expõe um enum útil `WebFontStyle` que permite combinar estilos com um OR bit‑a‑bit. Vamos deixar o texto tanto em negrito **quanto** itálico.

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**O que está acontecendo nos bastidores?** A propriedade `FontStyle` é traduzida para as declarações CSS `font-weight` e `font-style`. Ao combinar as flags com OR evitamos escrever duas linhas separadas de CSS.

## Etapa 4: Converter o HTML para PDF (Salvar HTML como PDF)

A etapa final é a conversão propriamente dita. Com uma única chamada a `Save`, Aspose.HTML renderiza o DOM e grava um arquivo PDF no disco. Isso atende aos requisitos de **save html as pdf** e **convert html to pdf**.

```csharp
// Step 4 – save the HTML document as a PDF file
string outputPath = @"C:\Temp\styled.pdf";
htmlDocument.Save(outputPath, new PDFSaveOptions());

// Optional: open the PDF automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Resultado esperado:** Abra `styled.pdf` e você verá um único parágrafo exibindo “Bold & Italic text” em Arial 18 px, renderizado em negrito e itálico. As dimensões do PDF correspondem a uma página A4 padrão, e o texto é selecionável — graças à renderização vetorial.

## Exemplo Completo em Funcionamento

Juntando tudo, aqui está o programa completo, pronto para ser executado:

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new HTML document
        HTMLDocument htmlDocument = new HTMLDocument();
        HTMLBodyElement body = htmlDocument.Body;

        // 2️⃣ Add a styled paragraph
        HtmlElement paragraph = htmlDocument.CreateElement("p");
        paragraph.InnerHtml = "Bold & Italic text";

        // Set font family and size
        paragraph.Style.FontFamily = "Arial";
        paragraph.Style.FontSize = "18px";

        // 3️⃣ Apply bold + italic
        paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // Append to body
        body.AppendChild(paragraph);

        // 4️⃣ Save as PDF (convert HTML to PDF)
        string outputFile = @"C:\Temp\styled.pdf";
        htmlDocument.Save(outputFile, new PDFSaveOptions());

        Console.WriteLine($"PDF generated at: {outputFile}");
    }
}
```

### Executando o código

1. Instale o pacote NuGet Aspose.HTML:  
   ```bash
   dotnet add package Aspose.Html
   ```
2. Substitua `C:\Temp\styled.pdf` por uma pasta onde você tenha permissão de gravação.  
3. Compile e execute: `dotnet run`.  

Você deverá ver a mensagem no console confirmando a localização do arquivo, e o PDF conterá o parágrafo estilizado.

## Perguntas Frequentes & Casos de Borda

- **E se eu precisar de uma fonte web personalizada?**  
  Carregue a fonte com `HTMLFontFaceRule` ou referencie um arquivo CSS remoto `@font-face` antes de criar o parágrafo.

- **Posso adicionar imagens antes de converter?**  
  Absolutamente. Use `HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");` e defina `img.Source` para um caminho local ou data URI.

- **E quanto a PDFs com várias páginas?**  
  Adicione mais elementos (tabelas, divs, etc.) e Aspose.HTML paginará automaticamente quando o conteúdo exceder a altura da página.

- **Existe uma forma de controlar os metadados do PDF?**  
  Passe uma instância de `PdfSaveOptions` e defina propriedades como `Author`, `Title` ou `PdfAConformanceLevel`.

## Recapitulação

Cobrimos como **criar documento HTML** em C#, **definir família da fonte**, **definir tamanho da fonte**, aplicar estilos negrito‑itálico e, finalmente, **salvar HTML como PDF** — efetivamente **converter HTML para PDF** com Aspose.HTML. O trecho é curto o suficiente para ser inserido em qualquer projeto .NET, mas completo o bastante para servir como base sólida para cenários de relatórios mais complexos.

## Próximos Passos

- Experimente classes CSS para estilos reutilizáveis.  
- Combine múltiplos parágrafos, tabelas e imagens para criar PDFs mais ricos.  
- Explore a conformidade PDF/A se precisar de documentos de arquivamento.  

Sinta‑se à vontade para ajustar a fonte, o tamanho ou as cores — não há limite para o que você pode gerar programaticamente. Boa codificação, e que seus PDFs sempre renderizem exatamente como você imagina!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}