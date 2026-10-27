---
date: 2026-08-28
description: Ajuste o tamanho da página XPS ao converter HTML para XPS em Java usando
  Aspose.HTML. Renderize HTML para XPS com dimensões precisas.
keywords:
- adjust xps page size
- render html to xps
- aspose.html java
- xps conversion java
- html to xps
lastmod: 2026-08-28
linktitle: Ajustando o Tamanho da Página XPS
og_description: Ajuste o tamanho da página XPS ao converter HTML para XPS em Java
  usando Aspose.HTML. Aprenda a renderizar HTML para XPS com dimensões precisas em
  segundos.
og_image_alt: Tutorial showing how to adjust XPS page size during HTML to XPS conversion
  with Aspose.HTML for Java
og_title: Ajustar o tamanho da página XPS ao converter HTML para XPS em Java
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  headline: Adjust XPS page size when converting HTML to XPS in Java
  type: TechArticle
- description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  name: Adjust XPS page size when converting HTML to XPS in Java
  steps:
  - name: set the input file name
    text: The `FileInputStream` class reads raw bytes from a file, providing the HTML
      source to the renderer.
  - name: create an HTML document and set styles
    text: The `HTMLDocument` class represents an in‑memory HTML DOM used by Aspose.HTML
      for rendering.
  - name: create XPS rendering options
    text: The `XpsRenderingOptions` class holds settings that control how HTML is
      rendered to XPS, such as page size and image quality.
  - name: adjust the page size
    text: '**How to set XPS page size** – Define a custom page size (width × height
      in points) and tell the renderer whether it should automatically expand to the
      widest page. Setting `adjustToWidestPage` to `false` preserves the exact dimensions
      you specify. The `PageSetup` class defines page size, margins, a'
  - name: render the output
    text: The `XpsDevice` class is the rendering target that writes the processed
      content to an XPS file.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a Java library that allows developers to manipulate
      and convert HTML documents into various formats, such as XPS, PDF, and images.
      You can download the library from [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).
    question: What is Aspose.HTML for Java?
  - answer: You can download the Aspose.HTML for Java library from [Aspose product
      releases page](https://releases.aspose.com/).
    question: Where can I download Aspose.HTML for Java?
  - answer: Yes, you can get a free trial of Aspose.HTML for Java from the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: Is there a free trial available for Aspose.HTML for Java?
  - answer: To get a temporary license for Aspose.HTML for Java, visit the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: How can I obtain a temporary license for Aspose.HTML for Java?
  - answer: Yes, you can seek help and support from the Aspose community on the [Aspose
      Forum](https://forum.aspose.com/).
    question: Can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
tags:
- adjust xps page size
- Aspose.HTML
- Java XPS conversion
- HTML to XPS
- document rendering
title: Ajustar o tamanho da página XPS ao converter HTML para XPS em Java
url: /pt/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajustar o tamanho da página XPS ao converter HTML para XPS em Java

Neste tutorial, você aprenderá **como ajustar o tamanho da página XPS** ao converter HTML para XPS com Aspose.HTML for Java. Seja para faturas imprimíveis, relatórios de arquivamento ou etiquetas de tamanho personalizado, controlar as dimensões da página garante que o XPS final tenha exatamente a aparência desejada. Vamos percorrer a configuração do ambiente, as opções de renderização e a geração final do XPS para que você possa incorporar essa funcionalidade diretamente em suas aplicações Java.

## Respostas rápidas
- **O que significa “converter HTML para XPS”?** Ele renderiza um documento HTML em um arquivo XPS, preservando o layout e o estilo.  
- **Preciso de uma licença?** Um teste gratuito funciona para desenvolvimento; uma licença comercial é necessária para produção.  
- **Qual versão do Java é suportada?** Java 8 ou superior (JDK 11+ recomendado).  
- **Posso alterar o tamanho da página?** Sim – Aspose.HTML permite especificar dimensões personalizadas antes da renderização.  
- **Quanto tempo leva a conversão?** Normalmente menos de um segundo para páginas padrão; documentos maiores podem levar mais tempo.

## O que é converter HTML para XPS?
Converter HTML para XPS significa pegar um arquivo de marcação orientado à web e produzir um documento XPS (XML Paper Specification) — um formato de layout fixo, pronto para impressão, semelhante ao PDF. Isso é útil quando você precisa de documentos de alta fidelidade e independentes de dispositivo para arquivamento ou impressão a partir de aplicações Java.

## Por que ajustar o tamanho da página XPS?
Ajustar o tamanho da página XPS lhe dá controle sobre as dimensões físicas do documento final (por exemplo, A4, Letter, etiquetas personalizadas). Isso evita escalonamento indesejado, garante que o conteúdo se ajuste perfeitamente e pode reduzir o tamanho do arquivo ao eliminar espaços em branco desnecessários.

## Como renderizar HTML para XPS com um tamanho de página personalizado?
Carregue seu HTML, configure `XpsRenderingOptions` com um `PageSetup` que define a largura e altura exatas que você precisa, então renderize para um `XpsDevice`. Esse fluxo de duas etapas permite manter o layout intacto enquanto impõe as dimensões especificadas, tudo em uma única chamada de API.

## Pré-requisitos

Antes de começarmos, certifique‑se de que você tem os seguintes pré‑requisitos configurados:

1. **Ambiente de Desenvolvimento Java** – Java Development Kit (JDK) instalado no seu sistema.  
2. **Biblioteca Aspose.HTML for Java** – Baixe e inclua a biblioteca Aspose.HTML for Java em seu projeto. Você pode encontrar a biblioteca na [página de download do Aspose.HTML for Java](https://releases.aspose.com/html/java/).  
3. **Arquivo HTML de Entrada** – Prepare um arquivo HTML que você deseja renderizar e ajustar o tamanho da página XPS. Você pode usar seu próprio arquivo HTML para este tutorial.

## Importar pacotes

A classe `Page` representa as dimensões e configurações da página para a saída XPS. A classe `HtmlRenderer` realiza a conversão de HTML para XPS.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Guia passo a passo

Abaixo está um guia conciso, numerado, que espelha os passos originais enquanto adiciona contexto extra para clareza.

### Etapa 1: definir o nome do arquivo de entrada

A classe `FileInputStream` lê bytes brutos de um arquivo, fornecendo a fonte HTML ao renderizador.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### Etapa 2: criar um documento HTML e definir estilos

A classe `HTMLDocument` representa um DOM HTML em memória usado pelo Aspose.HTML para renderização.

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### Etapa 3: criar opções de renderização XPS

A classe `XpsRenderingOptions` contém configurações que controlam como o HTML é renderizado para XPS, como tamanho da página e qualidade da imagem.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### Etapa 4: ajustar o tamanho da página  

**Como definir o tamanho da página XPS** – Defina um tamanho de página personalizado (largura × altura em pontos) e indique ao renderizador se ele deve expandir automaticamente para a página mais larga. Definir `adjustToWidestPage` como `false` preserva as dimensões exatas que você especificar.

A classe `PageSetup` define o tamanho da página, margens e orientação para a saída XPS.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### Etapa 5: renderizar a saída

A classe `XpsDevice` é o destino de renderização que grava o conteúdo processado em um arquivo XPS.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Problemas comuns e soluções

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **Saída XPS em branco** | Fluxo de entrada não fechado ou HTMLDocument aponta para o arquivo errado. | Certifique‑se de que o `FileInputStream` esteja corretamente encapsulado em um bloco try‑with‑resources e que o caminho do arquivo esteja correto. |
| **Tamanho da página não aplicado** | `adjustToWidestPage` deixado como `true`. | Defina `pageSetup.setAdjustToWidestPage(false);` conforme mostrado na Etapa 4. |
| **CSS não suportado** | Aspose.HTML suporta um subconjunto de CSS. | Mantenha‑se em layout básico, fontes e cores; evite seletores avançados ou CSS Grid. |
| **LicenseException** | Executando sem uma licença válida em produção. | Aplique sua licença temporária ou comprada antes da renderização (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Perguntas frequentes

**Q: O que é Aspose.HTML for Java?**  
R: Aspose.HTML for Java é uma biblioteca Java que permite aos desenvolvedores manipular e converter documentos HTML em vários formatos, como XPS, PDF e imagens. Você pode baixar a biblioteca na [página de download do Aspose.HTML for Java](https://releases.aspose.com/html/java/).

**Q: Onde posso baixar o Aspose.HTML for Java?**  
R: Você pode baixar a biblioteca Aspose.HTML for Java na [página de lançamentos de produtos da Aspose](https://releases.aspose.com/).

**Q: Existe uma versão de avaliação gratuita do Aspose.HTML for Java?**  
R: Sim, você pode obter uma avaliação gratuita do Aspose.HTML for Java na [página de solicitação de licença temporária](https://purchase.aspose.com/temporary-license/).

**Q: Como posso obter uma licença temporária para o Aspose.HTML for Java?**  
R: Para obter uma licença temporária para o Aspose.HTML for Java, visite a [página de solicitação de licença temporária](https://purchase.aspose.com/temporary-license/).

**Q: Posso obter suporte para o Aspose.HTML for Java?**  
R: Sim, você pode buscar ajuda e suporte da comunidade Aspose no [Aspose Forum](https://forum.aspose.com/).

**Q: Posso converter HTML para XPS em um servidor sem interface gráfica?**  
R: Absolutamente. Aspose.HTML funciona em ambientes sem GUI; basta garantir que o runtime Java esteja configurado corretamente.

**Q: A biblioteca suporta margens de página personalizadas?**  
R: Sim. Use `PageSetup.setMarginTop()`, `setMarginBottom()`, etc., antes de atribuir o `PageSetup` às opções de renderização.

## Conclusão

Caminhamos pelo processo completo de **converter HTML para XPS** e **ajustar o tamanho da página XPS** com Aspose.HTML for Java. Seguindo estas etapas, você pode gerar documentos XPS prontos para impressão que correspondem exatamente aos seus requisitos de layout. Sinta‑se à vontade para experimentar diferentes dimensões de página, estilos ou até mesmo adicionar cabeçalhos e rodapés para atender às necessidades do seu projeto.

Se você tiver dúvidas ou precisar de mais assistência, explore a [documentação do Aspose.HTML for Java](https://reference.aspose.com/html/java/) ou participe da conversa no [Aspose Forum](https://forum.aspose.com/).

---

**Última atualização:** 2026-08-28  
**Testado com:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Autor:** Aspose

## Tutoriais Relacionados

- [Converter HTML para XPS com Aspose.HTML for Java](/html/java/conversion-html-to-other-formats/convert-html-to-xps/)
- [Ajustar tamanho da página PDF com Aspose.HTML for Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Conversão de EPUB para XPS com Aspose.HTML for Java](/html/java/converting-epub-to-xps/convert-epub-to-xps/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}