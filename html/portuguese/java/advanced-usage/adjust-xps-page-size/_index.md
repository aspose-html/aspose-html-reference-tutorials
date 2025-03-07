---
title: Ajuste o tamanho da página XPS com Aspose.HTML para Java
linktitle: Ajustando o tamanho da página XPS
second_title: Processamento HTML Java com Aspose.HTML
description: Aprenda como ajustar o tamanho da página XPS com Aspose.HTML para Java. Controle as dimensões de saída dos seus documentos XPS facilmente.
weight: 16
url: /pt/java/advanced-usage/adjust-xps-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajuste o tamanho da página XPS com Aspose.HTML para Java


Neste tutorial, nós o guiaremos pelo processo de ajuste do tamanho da página XPS usando Aspose.HTML para Java. Esta biblioteca poderosa permite que você manipule documentos HTML e os renderize em vários formatos, incluindo XPS. Ajustar o tamanho da página é essencial quando você precisa controlar as dimensões de saída do seu documento XPS.

## Pré-requisitos

Antes de começar, certifique-se de que você tenha os seguintes pré-requisitos:

1. Ambiente de desenvolvimento Java: certifique-se de ter o Java Development Kit (JDK) instalado no seu sistema.

2.  Biblioteca Aspose.HTML para Java: Você precisa baixar e incluir a biblioteca Aspose.HTML para Java no seu projeto Java. Você pode encontrar a biblioteca[aqui](https://releases.aspose.com/html/java/).

3. Arquivo HTML de entrada: Prepare um arquivo HTML que você deseja renderizar e ajuste o tamanho da página XPS para ele. Você pode usar seu próprio arquivo HTML para este tutorial.

## Pacotes de importação

Primeiro, você precisa importar os pacotes necessários para trabalhar com Aspose.HTML para Java. Inclua esses pacotes no início da sua classe Java:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Etapa 1: Defina o nome do arquivo de entrada

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 Nesta etapa, lemos seu arquivo de entrada HTML usando um`FileInputStream`.

## Etapa 2: Crie um documento HTML e defina estilos

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

 Esta etapa envolve a criação de um`HTMLDocument` e adicionar estilos a ele.

## Etapa 3: Criar opções de renderização XPS

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

Esta etapa envolve definir o tamanho da página e especificar se ela deve ser ajustada para a página mais larga.

## Etapa 5: renderizar a saída

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

Na etapa final, renderizamos a saída XPS usando as opções configuradas.

## Conclusão

Neste tutorial, mostramos como ajustar o tamanho da página XPS usando Aspose.HTML para Java. Você pode controlar as dimensões de saída dos seus documentos XPS, garantindo que eles atendam aos seus requisitos específicos. Com o código e as etapas fornecidas, você pode implementar facilmente esse recurso em seus aplicativos Java.

 Se você tiver alguma dúvida ou precisar de mais assistência, sinta-se à vontade para visitar o[Aspose.HTML para documentação Java](https://reference.aspose.com/html/java/) ou peça ajuda no[Fórum Aspose](https://forum.aspose.com/).

## Perguntas frequentes

### P1: O que é Aspose.HTML para Java?

A1: Aspose.HTML para Java é uma biblioteca Java que permite aos desenvolvedores manipular e converter documentos HTML em vários formatos, como XPS, PDF e imagens.

### P2: Onde posso baixar o Aspose.HTML para Java?

 A2: Você pode baixar a biblioteca Aspose.HTML para Java em[este link](https://releases.aspose.com/html/java/).

### P3: Existe uma avaliação gratuita disponível para o Aspose.HTML para Java?

 R3: Sim, você pode obter uma avaliação gratuita do Aspose.HTML para Java em[aqui](https://releases.aspose.com/).

### P4: Como posso obter uma licença temporária para Aspose.HTML para Java?

 A4: Para obter uma licença temporária para Aspose.HTML para Java, visite[esta página](https://purchase.aspose.com/temporary-license/).

### P5: Posso obter suporte para Aspose.HTML para Java?

 R5: Sim, você pode buscar ajuda e suporte da comunidade Aspose no[Fórum Aspose](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
