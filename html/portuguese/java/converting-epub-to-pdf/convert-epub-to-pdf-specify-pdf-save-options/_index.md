---
title: Especificando opções de salvamento de PDF para EPUB em PDF
linktitle: Especificando opções de salvamento de PDF para EPUB em PDF
second_title: Processamento HTML Java com Aspose.HTML
description: Aprenda como converter EPUB para PDF em Java usando Aspose.HTML, uma poderosa biblioteca de manipulação de HTML.
weight: 12
url: /pt/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Especificando opções de salvamento de PDF para EPUB em PDF


## Introdução

Aspose.HTML para Java é uma ferramenta poderosa para trabalhar com documentos HTML e EPUB. Neste guia passo a passo, nós o guiaremos pelo processo de conversão de um arquivo EPUB para PDF usando Aspose.HTML para Java. Seja você um desenvolvedor experiente ou apenas começando, este tutorial fornecerá a você o conhecimento e as habilidades necessárias para executar esta tarefa de forma eficiente.

## Pré-requisitos

Antes de começar, certifique-se de que você tenha os seguintes pré-requisitos:

- Ambiente de desenvolvimento Java: você deve ter um ambiente de desenvolvimento Java configurado no seu sistema.

-  Aspose.HTML para Java: Baixe e instale a biblioteca Aspose.HTML para Java. Você pode encontrar a biblioteca e a documentação relacionada no[site](https://releases.aspose.com/html/java/).

- Arquivo EPUB: você precisará de um arquivo EPUB que deseja converter para PDF.

Agora, vamos mergulhar no guia passo a passo para converter EPUB em PDF usando Aspose.HTML para Java.

## Etapa 1: Abra o arquivo EPUB

 Para começar, abra um arquivo EPUB existente para leitura. Você pode usar um`FileInputStream` para conseguir isso. Aqui está o código para esta etapa:

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Seu código para os próximos passos será colocado aqui.
}
```

## Etapa 2: Defina as opções de salvamento de PDF

 Crie uma instância de`PdfSaveOptions` com tamanho de página e cor de fundo personalizados. Você pode configurar a configuração da página de acordo com seus requisitos. Veja como você pode fazer isso:

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

## Etapa 3: converter EPUB em PDF

 Agora, ligue para o`ConvertEPUB` método para converter o arquivo EPUB para PDF. Especifique o fluxo de entrada, as opções de salvamento do PDF e o local de saída. Veja como é feito:

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

Parabéns! Você converteu com sucesso um arquivo EPUB para PDF usando Aspose.HTML para Java. Agora você pode acessar o arquivo PDF convertido no local de saída especificado.

## Código fonte completo
```java
Specifying PDF Save Options for EPUB to PDF
        // Abra um arquivo EPUB existente para leitura.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Crie uma instância de PdfSaveOptions com um tamanho de página personalizado e uma cor de fundo.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Chame o método ConvertEPUB para converter o EPUB em PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```


## Conclusão

Neste tutorial, aprendemos como usar o Aspose.HTML para Java para converter arquivos EPUB para o formato PDF. Esta biblioteca versátil fornece aos desenvolvedores ferramentas poderosas para manipulação de documentos. Seguindo as etapas descritas neste guia, você pode integrar perfeitamente a conversão de EPUB para PDF em seus aplicativos Java.

## Perguntas Frequentes (FAQs)

### O Aspose.HTML para Java é uma biblioteca gratuita?
 Aspose.HTML para Java é uma biblioteca comercial, mas você pode obter uma versão de teste gratuita em seu site[site](https://releases.aspose.com/).

### Quais formatos EPUB são suportados para conversão?
O Aspose.HTML para Java suporta a conversão de vários formatos EPUB, garantindo compatibilidade com a maioria dos documentos EPUB.

### Posso personalizar ainda mais a saída do PDF?
 Sim, você pode personalizar a saída do PDF ajustando a configuração da página, a cor de fundo e outras configurações no`PdfSaveOptions`.

### Há alguma limitação na versão de teste do Aspose.HTML para Java?
A versão de teste pode ter algumas limitações, por isso é recomendável verificar a documentação para obter detalhes.

### Onde posso obter suporte para Aspose.HTML para Java?
Você pode encontrar respostas para suas perguntas e buscar suporte no[Fórum Aspose.HTML](https://forum.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
