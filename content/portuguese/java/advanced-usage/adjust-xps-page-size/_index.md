---
title: Ajuste o tamanho da página XPS com Aspose.HTML para Java
linktitle: Ajustando o tamanho da página XPS
second_title: Processamento Java HTML com Aspose.HTML
description: Aprenda como ajustar o tamanho da página XPS com Aspose.HTML para Java. Controle facilmente as dimensões de saída dos seus documentos XPS.
type: docs
weight: 16
url: /pt/java/advanced-usage/adjust-xps-page-size/
---

Neste tutorial, iremos guiá-lo através do processo de ajuste do tamanho da página XPS usando Aspose.HTML para Java. Esta poderosa biblioteca permite manipular documentos HTML e renderizá-los em vários formatos, incluindo XPS. Ajustar o tamanho da página é essencial quando você precisa controlar as dimensões de saída do seu documento XPS.

## Pré-requisitos

Antes de começarmos, certifique-se de ter os seguintes pré-requisitos em vigor:

1. Ambiente de Desenvolvimento Java: Certifique-se de ter o Java Development Kit (JDK) instalado em seu sistema.

2.  Biblioteca Aspose.HTML para Java: você precisa baixar e incluir a biblioteca Aspose.HTML para Java em seu projeto Java. Você pode encontrar a biblioteca[aqui](https://releases.aspose.com/html/java/).

3. Arquivo HTML de entrada: prepare um arquivo HTML que você deseja renderizar e ajuste o tamanho da página XPS. Você pode usar seu próprio arquivo HTML para este tutorial.

## Importar pacotes

Primeiro, você precisa importar os pacotes necessários para trabalhar com Aspose.HTML for Java. Inclua estes pacotes no início da sua classe Java:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Etapa 1: definir o nome do arquivo de entrada

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 Nesta etapa, lemos seu arquivo de entrada HTML usando um`FileInputStream`.

## Etapa 2: crie um documento HTML e defina estilos

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 Esta etapa envolve a criação de um`HTMLDocument` e adicionando estilos a ele.

## Etapa 3: criar opções de renderização XPS

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Aqui, criamos opções de renderização XPS para configurar o processo de renderização.

## Etapa 4: ajuste o tamanho da página

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

Esta etapa envolve definir o tamanho da página e especificar se deseja ajustá-lo para a página mais larga.

## Etapa 5: renderizar a saída

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

Na etapa final, renderizamos a saída XPS usando as opções configuradas.

## Conclusão

Neste tutorial, mostramos como ajustar o tamanho da página XPS usando Aspose.HTML para Java. Você pode controlar as dimensões de saída dos seus documentos XPS, garantindo que eles atendam aos seus requisitos específicos. Com o código e as etapas fornecidas, você pode implementar facilmente esse recurso em seus aplicativos Java.

 Se você tiver alguma dúvida ou precisar de mais assistência, sinta-se à vontade para visitar o[Documentação Aspose.HTML para Java](https://reference.aspose.com/html/java/) ou peça ajuda no[Aspor Fórum](https://forum.aspose.com/).

## Perguntas frequentes

### Q1: O que é Aspose.HTML para Java?

A1: Aspose.HTML for Java é uma biblioteca Java que permite aos desenvolvedores manipular e converter documentos HTML em vários formatos, como XPS, PDF e imagens.

### Q2: Onde posso baixar Aspose.HTML para Java?

 A2: Você pode baixar a biblioteca Aspose.HTML para Java em[esse link](https://releases.aspose.com/html/java/).

### Q3: Existe uma avaliação gratuita disponível para Aspose.HTML para Java?

 A3: Sim, você pode obter uma avaliação gratuita do Aspose.HTML para Java em[aqui](https://releases.aspose.com/).

### Q4: Como posso obter uma licença temporária do Aspose.HTML para Java?

 A4: Para obter uma licença temporária do Aspose.HTML para Java, visite[esta página](https://purchase.aspose.com/temporary-license/).

### Q5: Posso obter suporte para Aspose.HTML para Java?

 A5: Sim, você pode procurar ajuda e apoio da comunidade Aspose no[Aspor Fórum](https://forum.aspose.com/).