---
title: Ajuste o tamanho da página PDF com Aspose.HTML para Java
linktitle: Ajustando o tamanho da página PDF
second_title: Processamento Java HTML com Aspose.HTML
description: Aprenda como ajustar o tamanho da página PDF com Aspose.HTML para Java. Crie PDFs de alta qualidade a partir de HTML sem esforço. Controle as dimensões da página de forma eficaz.
type: docs
weight: 15
url: /pt/java/advanced-usage/adjust-pdf-page-size/
---

Na era digital de hoje, a necessidade de gerar PDFs de alta qualidade a partir de conteúdo HTML está aumentando. Aspose.HTML for Java é uma biblioteca Java poderosa que permite converter documentos HTML para o formato PDF sem esforço. Neste tutorial, focaremos no ajuste do tamanho da página ao converter HTML em PDF usando Aspose.HTML para Java.

## Pré-requisitos

Antes de começar, certifique-se de ter os seguintes pré-requisitos em vigor:

- Ambiente de Desenvolvimento Java: Certifique-se de ter o Java Development Kit (JDK) instalado em seu sistema.
-  Aspose.HTML para Java: Você precisa baixar e instalar o Aspose.HTML para Java do site[aqui](https://releases.aspose.com/html/java/).
- Documento HTML: você deve ter um documento HTML pronto para conversão. Caso contrário, crie um ou use um arquivo HTML existente.

## Importar pacotes

Para começar, você precisa importar os pacotes necessários para trabalhar com Aspose.HTML for Java. O trecho de código a seguir demonstra como fazer isso:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

Agora que você atendeu aos pré-requisitos e importou os pacotes necessários, vamos dividir o processo de ajuste do tamanho da página PDF em várias etapas:

## Etapa 1: Lendo conteúdo HTML

Primeiro, você precisa ler o conteúdo HTML que deseja converter para PDF. Neste exemplo, leremos o HTML de um arquivo chamado “FirstFile.html”.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Etapa 2: escrever conteúdo HTML

A seguir, você gravará o conteúdo HTML em um arquivo chamado “FirstFileOut.html”.

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Adicione estilos ou conteúdo HTML personalizado aqui
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

## Passo 3: Renderizando HTML para PDF

Agora, você renderizará o conteúdo HTML em um arquivo PDF. Cobriremos dois cenários: um onde o tamanho da página não é ajustado à largura do conteúdo e outro onde é ajustado.

### Tamanho da página não ajustado

Nesse cenário, o tamanho da página é definido com largura e altura fixas, o que pode cortar o conteúdo se exceder essas dimensões.

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

Neste tutorial, exploramos como ajustar o tamanho da página PDF ao converter HTML em PDF usando Aspose.HTML para Java. Você aprendeu os pré-requisitos, importou os pacotes necessários e seguiu um guia passo a passo para realizar esta tarefa. Com Aspose.HTML for Java, você pode controlar facilmente o tamanho da página dos PDFs gerados, garantindo que seu conteúdo seja exibido conforme pretendido.

 Sinta-se à vontade para experimentar diferentes tamanhos e configurações de página para atender às suas necessidades específicas. Se você encontrar algum problema ou tiver mais dúvidas, não hesite em procurar ajuda do[Documentação Aspose.HTML para Java](https://reference.aspose.com/html/java/) ou o[Aspose fórum de suporte](https://forum.aspose.com/).

## Perguntas frequentes

### Q1: O que é Aspose.HTML para Java?

A1: Aspose.HTML for Java é uma biblioteca Java que permite trabalhar com documentos HTML, manipular, converter e renderizá-los em vários formatos, incluindo PDF.

### Q2: Como posso ajustar o tamanho da página PDF ao converter HTML em PDF com Aspose.HTML para Java?

 A2: Você pode ajustar o tamanho da página PDF usando o`PageSetup` classe e definir o`AdjustToWidestPage` propriedade para`true` ou `false, dependendo de seus requisitos.

### P3: Posso personalizar o estilo do conteúdo HTML antes de convertê-lo para PDF?

A3: Sim, você pode personalizar o estilo adicionando elementos CSS e HTML ao seu conteúdo HTML antes de convertê-lo para PDF, conforme demonstrado no tutorial.

### Q4: Onde posso encontrar a documentação do Aspose.HTML para Java?

 A4: Você pode consultar a documentação[aqui](https://reference.aspose.com/html/java/) para obter informações abrangentes e exemplos.

### Q5: Existe uma avaliação gratuita disponível para Aspose.HTML para Java?

 A5: Sim, você pode acessar uma avaliação gratuita do Aspose.HTML for Java em[esse link](https://releases.aspose.com/).