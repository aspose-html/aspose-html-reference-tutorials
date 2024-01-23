---
title: Especificando opções de salvamento de PDF para EPUB em PDF
linktitle: Especificando opções de salvamento de PDF para EPUB em PDF
second_title: Processamento Java HTML com Aspose.HTML
description: Aprenda como converter EPUB para PDF em Java usando Aspose.HTML, uma poderosa biblioteca de manipulação de HTML.
type: docs
weight: 12
url: /pt/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
---

## Introdução

Aspose.HTML for Java é uma ferramenta poderosa para trabalhar com documentos HTML e EPUB. Neste guia passo a passo, orientaremos você no processo de conversão de um arquivo EPUB em PDF usando Aspose.HTML para Java. Quer você seja um desenvolvedor experiente ou esteja apenas começando, este tutorial fornecerá o conhecimento e as habilidades necessárias para executar esta tarefa com eficiência.

## Pré-requisitos

Antes de começarmos, certifique-se de ter os seguintes pré-requisitos em vigor:

- Ambiente de Desenvolvimento Java: Você deve ter um ambiente de desenvolvimento Java configurado em seu sistema.

-  Aspose.HTML para Java: Baixe e instale a biblioteca Aspose.HTML para Java. Você pode encontrar a biblioteca e a documentação relacionada no site[local na rede Internet](https://releases.aspose.com/html/java/).

- Arquivo EPUB: você precisará de um arquivo EPUB que deseja converter em PDF.

Agora, vamos mergulhar no guia passo a passo para converter EPUB em PDF usando Aspose.HTML para Java.

## Etapa 1: abra o arquivo EPUB

 Para começar, abra um arquivo EPUB existente para leitura. Você pode usar um`FileInputStream` Para alcançar isto. Aqui está o código para esta etapa:

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Seu código para as próximas etapas irá aqui.
}
```

## Passo 2: Definir opções para salvar PDF

 Crie uma instância de`PdfSaveOptions` com tamanho de página personalizado e cor de fundo. Você pode definir a configuração da página de acordo com seus requisitos. Veja como você pode fazer isso:

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

## Passo 3: Converter EPUB em PDF

 Agora, ligue para o`ConvertEPUB` método para converter o arquivo EPUB em PDF. Especifique o fluxo de entrada, as opções de salvamento do PDF e o local de saída. Veja como isso é feito:

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

Parabéns! Você converteu com sucesso um arquivo EPUB em PDF usando Aspose.HTML para Java. Agora você pode acessar o arquivo PDF convertido no local de saída especificado.

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
            // Chame o método ConvertEPUB para converter EPUB em PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```


## Conclusão

Neste tutorial, aprendemos como usar Aspose.HTML for Java para converter arquivos EPUB para o formato PDF. Esta biblioteca versátil oferece aos desenvolvedores ferramentas poderosas para manipulação de documentos. Seguindo as etapas descritas neste guia, você pode integrar perfeitamente a conversão de EPUB para PDF em seus aplicativos Java.

## Perguntas frequentes (FAQ)

### Aspose.HTML for Java é uma biblioteca gratuita?
 Aspose.HTML for Java é uma biblioteca comercial, mas você pode obter uma versão de teste gratuita em seu site.[local na rede Internet](https://releases.aspose.com/).

### Quais formatos EPUB são suportados para conversão?
Aspose.HTML for Java suporta a conversão de vários formatos EPUB, garantindo compatibilidade com a maioria dos documentos EPUB.

### Posso personalizar ainda mais a saída do PDF?
 Sim, você pode personalizar a saída do PDF ajustando a configuração da página, a cor de fundo e outras configurações no`PdfSaveOptions`.

### Há alguma limitação para a versão de teste do Aspose.HTML for Java?
A versão de teste pode ter algumas limitações, por isso é recomendável verificar a documentação para obter detalhes.

### Onde posso obter suporte para Aspose.HTML para Java?
Você pode encontrar respostas para suas perguntas e buscar suporte no[Fórum Aspose.HTML](https://forum.aspose.com/).
