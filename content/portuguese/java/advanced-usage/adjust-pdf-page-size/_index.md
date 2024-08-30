---
title: Ajuste o tamanho da página PDF com Aspose.HTML para Java
linktitle: Ajustando o tamanho da página do PDF
second_title: Processamento HTML Java com Aspose.HTML
description: Aprenda a ajustar o tamanho da página PDF com Aspose.HTML para Java. Crie PDFs de alta qualidade a partir de HTML sem esforço. Controle as dimensões da página de forma eficaz.
type: docs
weight: 15
url: /pt/java/advanced-usage/adjust-pdf-page-size/
---

Na era digital de hoje, a necessidade de gerar PDFs de alta qualidade a partir de conteúdo HTML está aumentando. Aspose.HTML para Java é uma poderosa biblioteca Java que permite converter documentos HTML para o formato PDF sem esforço. Neste tutorial, focaremos em ajustar o tamanho da página ao converter HTML para PDF usando Aspose.HTML para Java.

## Pré-requisitos

Antes de começar, certifique-se de ter os seguintes pré-requisitos em vigor:

- Ambiente de desenvolvimento Java: certifique-se de ter o Java Development Kit (JDK) instalado no seu sistema.
-  Aspose.HTML para Java: Você precisa baixar e instalar o Aspose.HTML para Java do site[aqui](https://releases.aspose.com/html/java/).
- Documento HTML: Você deve ter um documento HTML pronto para conversão. Se não, crie um ou use um arquivo HTML existente.

## Pacotes de importação

Para começar, você precisa importar os pacotes necessários para trabalhar com Aspose.HTML para Java. O seguinte trecho de código demonstra como fazer isso:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

Agora que você tem os pré-requisitos definidos e importou os pacotes necessários, vamos dividir o processo de ajuste do tamanho da página do PDF em várias etapas:

## Etapa 1: Lendo conteúdo HTML

Primeiro, você precisa ler o conteúdo HTML que deseja converter para PDF. Neste exemplo, leremos o HTML de um arquivo chamado "FirstFile.html".

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Etapa 2: Escrevendo conteúdo HTML

Em seguida, você escreverá o conteúdo HTML em um arquivo chamado "FirstFileOut.html".

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Adicione estilos ou conteúdo HTML personalizados aqui
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## Etapa 3: Renderizando HTML para PDF

Agora, você renderizará o conteúdo HTML para um arquivo PDF. Cobriremos dois cenários: um em que o tamanho da página não é ajustado à largura do conteúdo e outro em que é ajustado.

### Tamanho da página não ajustado

Nesse cenário, o tamanho da página é definido como largura e altura fixas, o que pode cortar o conteúdo se ele exceder essas dimensões.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Crie uma instância HTMLDocument a partir do arquivo HTML
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Definir opções de renderização de PDF
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Renderizar a saída
pdf_renderer.render(device, html_document);
```

### Tamanho da página ajustado à largura do conteúdo

Neste cenário, o tamanho da página é ajustado de acordo com a largura do conteúdo.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Renderizar a saída
pdf_renderer.render(device, html_document);
```

## Conclusão

Neste tutorial, exploramos como ajustar o tamanho da página PDF ao converter HTML para PDF usando Aspose.HTML para Java. Você aprendeu os pré-requisitos, importou os pacotes necessários e seguiu um guia passo a passo para realizar esta tarefa. Com Aspose.HTML para Java, você pode controlar facilmente o tamanho da página dos seus PDFs gerados, garantindo que seu conteúdo seja exibido conforme o esperado.

 Sinta-se à vontade para experimentar diferentes tamanhos de página e configurações para atender às suas necessidades específicas. Se você encontrar algum problema ou tiver mais perguntas, não hesite em procurar assistência do[Aspose.HTML para documentação Java](https://reference.aspose.com/html/java/) ou o[Fórum de suporte Aspose](https://forum.aspose.com/).

## Perguntas frequentes

### P1: O que é Aspose.HTML para Java?

A1: Aspose.HTML para Java é uma biblioteca Java que permite trabalhar com documentos HTML, manipulá-los, convertê-los e renderizá-los em vários formatos, incluindo PDF.

### P2: Como posso ajustar o tamanho da página PDF ao converter HTML para PDF com Aspose.HTML para Java?

 A2: Você pode ajustar o tamanho da página do PDF usando o`PageSetup` classe e configuração do`AdjustToWidestPage` propriedade para`true` ou `falso, dependendo de suas necessidades.

### P3: Posso personalizar o estilo do conteúdo HTML antes de convertê-lo em PDF?

R3: Sim, você pode personalizar o estilo adicionando elementos CSS e HTML ao seu conteúdo HTML antes de convertê-lo em PDF, conforme demonstrado no tutorial.

### P4: Onde posso encontrar a documentação do Aspose.HTML para Java?

 A4: Você pode consultar a documentação[aqui](https://reference.aspose.com/html/java/) para obter informações e exemplos abrangentes.

### P5: Existe uma avaliação gratuita disponível do Aspose.HTML para Java?

 R5: Sim, você pode acessar uma avaliação gratuita do Aspose.HTML para Java em[este link](https://releases.aspose.com/).