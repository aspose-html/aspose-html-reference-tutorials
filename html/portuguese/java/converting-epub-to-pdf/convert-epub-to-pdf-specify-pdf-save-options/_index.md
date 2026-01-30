---
date: 2026-01-02
description: Aprenda como converter EPUB para PDF em Java com Aspose.HTML enquanto
  define um tamanho de página PDF personalizado e outras opções de salvamento em PDF.
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 'Tamanho de página PDF personalizado: especificando opções de salvamento de
  PDF para EPUB em PDF'
url: /pt/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tamanho de Página PDF Personalizado: Especificando Opções de Salvamento PDF para EPUB para PDF

## Introdução

O Aspose.HTML for Java facilita a **conversão de EPUB para PDF** e oferece controle total sobre a saída, incluindo a definição de um **tamanho de página PDF personalizado**. Neste guia passo a passo, vamos percorrer tudo o que você precisa — desde a preparação do ambiente até o ajuste do `PdfSaveOptions` para que o PDF gerado corresponda exatamente às dimensões de página que você requer. Seja construindo um pipeline de publicação, uma plataforma de e‑learning ou apenas precisando automatizar a conversão de documentos, você achará as técnicas aqui apresentadas valiosas.

## Respostas Rápidas
- **Qual é o objetivo principal deste tutorial?** Converter um arquivo EPUB para PDF aplicando um tamanho de página PDF personalizado.  
- **Qual biblioteca é usada?** Aspose.HTML for Java.  
- **Preciso de licença?** Um teste gratuito está disponível; uma licença comercial é necessária para produção.  
- **Posso mudar a cor de fundo?** Sim, usando `PdfSaveOptions`.  
- **Java 8+ é suportado?** Absolutamente — qualquer runtime Java moderno funciona.

## O que é um tamanho de página PDF personalizado?

Um tamanho de página PDF personalizado permite definir a largura e a altura exatas de cada página no PDF de saída, em vez de depender de tamanhos padrão como A4 ou Letter. Isso é especialmente útil para e‑books, folhetos ou qualquer cenário onde o layout visual deve corresponder a um design específico.

## Por que usar Aspose.HTML para conversão de EPUB para PDF?

- **Alta fidelidade:** Preserva layouts complexos, fontes e imagens.  
- **Controle granular:** Ajusta tamanho de página, fundo, margens e mais via `PdfSaveOptions`.  
- **Multiplataforma:** Funciona no Windows, Linux e macOS com o mesmo código Java.  
- **Desempenho:** Motor de renderização otimizado para conversões rápidas.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

- **Ambiente de Desenvolvimento Java:** JDK 8 ou superior instalado e configurado.  
- **Aspose.HTML for Java:** Baixe o JAR mais recente do [site](https://releases.aspose.com/html/java/).  
- **Arquivo EPUB:** Um documento `.epub` que você deseja converter.  

Agora que tudo está pronto, vamos mergulhar nos passos reais de conversão.

## Etapa 1: Abrir o Arquivo EPUB

Primeiro, precisamos abrir o arquivo EPUB usando um `FileInputStream`. Esse stream será passado para o conversor mais tarde.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## Etapa 2: Definir Opções de Salvamento PDF

É aqui que definimos o **tamanho de página PDF personalizado** e a cor de fundo opcional. Ajuste os valores em pixels para corresponder às dimensões desejadas.

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

### Dica profissional:
- **Pixels vs. Points:** `Length.fromPixels` converte pixels da tela em pontos PDF (1 ponto = 1/72 polegada). Escolha valores que reflitam o tamanho impresso final que você precisa.

## Etapa 3: Converter EPUB para PDF

Com o stream de entrada e as opções personalizadas prontos, invoque o conversor. O PDF de saída será salvo no local que você especificar.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## Código Fonte Completo

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
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
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## Problemas Comuns e Soluções

| Problema | Causa | Solução |
|----------|-------|---------|
| **Páginas PDF estão em branco** | Stream de entrada fechado antes da conversão | Mantenha o bloco `try‑with‑resources` aberto até depois de `convertEPUB`. |
| **Dimensões de página incorretas** | Uso de pixels que não correspondem ao tamanho de impressão desejado | Converta as polegadas desejadas em pontos (`1 polegada = 72 pontos`) e depois em pixels usando `Length.fromPixels`. |
| **Fontes ausentes** | Fontes não incorporadas no EPUB | Certifique‑se de que as fontes estejam empacotadas dentro do EPUB ou instale‑as na máquina host. |

## Perguntas Frequentes (FAQs)

### O Aspose.HTML for Java é uma biblioteca gratuita?
O Aspose.HTML for Java é uma biblioteca comercial, mas você pode obter uma versão de teste gratuito no [site](https://releases.aspose.com/).

### Quais formatos EPUB são suportados para conversão?
O Aspose.HTML for Java suporta a conversão de vários formatos EPUB, garantindo compatibilidade com a maioria dos documentos EPUB.

### Posso personalizar ainda mais a saída PDF?
Sim, você pode personalizar a saída PDF ajustando a configuração de página, cor de fundo e outras opções em `PdfSaveOptions`.

### Existem limitações na versão de avaliação do Aspose.HTML for Java?
A versão de avaliação pode ter algumas limitações; recomenda‑se verificar a documentação para detalhes.

### Onde posso obter suporte para Aspose.HTML for Java?
Você pode encontrar respostas às suas perguntas e buscar suporte no [fórum Aspose.HTML](https://forum.aspose.com/).

---

**Last Updated:** 2026-01-02  
**Tested With:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}