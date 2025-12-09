---
date: 2025-11-29
description: Aprenda a converter HTML para XPS e ajustar o tamanho da página XPS usando
  Aspose.HTML para Java. Controle as dimensões da saída facilmente.
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Converter HTML para XPS e Ajustar o Tamanho da Página XPS com Aspose.HTML para
  Java
url: /pt/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter HTML para XPS e Ajustar o Tamanho da Página XPS com Aspose.HTML para Java

Neste tutorial você descobrirá **como converter HTML para XPS** e ajustar finamente o tamanho da página resultante usando o Aspose.HTML para Java. Seja gerando relatórios imprimíveis, faturas ou documentos de arquivamento, controlar as dimensões do XPS garante que a saída apareça exatamente como você espera. Percorreremos cada passo — desde a configuração do ambiente até a renderização do arquivo XPS final — para que você possa integrar essa funcionalidade em suas aplicações Java imediatamente.

## Respostas Rápidas
- **O que significa “converter HTML para XPS”?** Ele renderiza um documento HTML em um arquivo XPS, preservando o layout e o estilo.  
- **Preciso de licença?** Um teste gratuito funciona para desenvolvimento; uma licença comercial é necessária para produção.  
- **Qual versão do Java é suportada?** Java 8 ou superior (JDK 11+ recomendado).  
- **Posso mudar o tamanho da página?** Sim — o Aspose.HTML permite especificar dimensões personalizadas antes da renderização.  
- **Quanto tempo leva a conversão?** Normalmente menos de um segundo para páginas padrão; documentos maiores podem levar mais tempo.

## O que é converter HTML para XPS?
Converter HTML para XPS significa pegar um arquivo de marcação orientado para a web e produzir um documento XPS (XML Paper Specification) — um formato de layout fixo, pronto para impressão, semelhante ao PDF. Isso é útil quando você precisa de documentos de alta fidelidade e independentes de dispositivo para arquivamento ou impressão a partir de aplicações Java.

## Por que ajustar o tamanho da página XPS?
Ajustar o tamanho da página lhe dá controle sobre as dimensões físicas do documento final (por exemplo, A4, Letter, etiquetas personalizadas). Isso evita escalonamento indesejado, garante que o conteúdo se encaixe perfeitamente e pode reduzir o tamanho do arquivo ao eliminar espaços em branco desnecessários.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem os seguintes pré‑requisitos:

1. **Ambiente de Desenvolvimento Java** – Java Development Kit (JDK) instalado no seu sistema.  
2. **Biblioteca Aspose.HTML para Java** – Baixe e inclua a biblioteca Aspose.HTML para Java no seu projeto. Você pode encontrar a biblioteca [aqui](https://releases.aspose.com/html/java/).  
3. **Arquivo HTML de Entrada** – Prepare um arquivo HTML que você deseja renderizar e ajustar o tamanho da página XPS. Você pode usar seu próprio arquivo HTML para este tutorial.

## Importar Pacotes

Primeiro, importe as classes que você precisará. Esses pacotes dão acesso ao manuseio de documentos, renderização e recursos de configuração de página.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Etapa 1: Definir o Nome do Arquivo de Entrada

Leia o arquivo HTML fonte usando um `FileInputStream`. Esse fluxo alimenta o HTML bruto para o motor Aspose.HTML.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## Etapa 2: Criar um Documento HTML e Definir Estilos

Crie uma instância `HTMLDocument` que representa o conteúdo que será renderizado. Neste exemplo também inserimos um pequeno bloco CSS para demonstrar a estilização — sinta‑se à vontade para substituir pelo seu próprio markup.

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

## Etapa 3: Criar Opções de Renderização XPS

Instancie `XpsRenderingOptions` para armazenar todas as configurações que afetam a conversão de HTML para XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## Etapa 4: Ajustar o Tamanho da Página

Defina um tamanho de página personalizado (largura × altura em pontos) e informe ao renderizador se ele deve expandir automaticamente para a página mais larga. Definir `adjustToWidestPage` como `false` preserva as dimensões exatas que você especificar.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## Etapa 5: Renderizar a Saída

Finalmente, crie um `XpsDevice` com as opções configuradas e renderize o documento HTML. O resultado é um arquivo XPS totalmente formado com as dimensões de página personalizadas que você definiu.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Problemas Comuns e Soluções

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **Saída XPS em branco** | Fluxo de entrada não fechado ou `HTMLDocument` aponta para o arquivo errado. | Garanta que o `FileInputStream` esteja corretamente encapsulado em um bloco try‑with‑resources e que o caminho do arquivo esteja correto. |
| **Tamanho da página não aplicado** | `adjustToWidestPage` deixado como `true`. | Defina `pageSetup.setAdjustToWidestPage(false);` conforme mostrado na Etapa 4. |
| **CSS não suportado** | Aspose.HTML suporta um subconjunto de CSS. | Use layout básico, fontes e cores; evite seletores avançados ou CSS Grid. |
| **LicenseException** | Execução sem licença válida em produção. | Aplique sua licença temporária ou comprada antes da renderização (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Perguntas Frequentes

**P: O que é Aspose.HTML para Java?**  
R: Aspose.HTML para Java é uma biblioteca Java que permite aos desenvolvedores manipular e converter documentos HTML em vários formatos, como XPS, PDF e imagens.

**P: Onde posso baixar Aspose.HTML para Java?**  
R: Você pode baixar a biblioteca Aspose.HTML para Java a partir deste link: [this link](https://releases.aspose.com/html/java/).

**P: Existe uma versão de teste gratuita disponível para Aspose.HTML para Java?**  
R: Sim, você pode obter um teste gratuito de Aspose.HTML para Java [aqui](https://releases.aspose.com/).

**P: Como posso obter uma licença temporária para Aspose.HTML para Java?**  
R: Para obter uma licença temporária para Aspose.HTML para Java, visite [this page](https://purchase.aspose.com/temporary-license/).

**P: Posso obter suporte para Aspose.HTML para Java?**  
R: Sim, você pode buscar ajuda e suporte na comunidade Aspose através do [Aspose Forum](https://forum.aspose.com/).

**P: Posso converter HTML para XPS em um servidor sem interface gráfica?**  
R: Absolutamente. Aspose.HTML funciona em ambientes sem GUI; basta garantir que o runtime Java esteja configurado corretamente.

**P: A biblioteca suporta margens de página personalizadas?**  
R: Sim. Use `PageSetup.setMarginTop()`, `setMarginBottom()`, etc., antes de atribuir o `PageSetup` às opções de renderização.

## Conclusão

Percorremos todo o processo de **converter HTML para XPS** e ajustar o tamanho da página com Aspose.HTML para Java. Seguindo estas etapas, você pode gerar documentos XPS prontos para impressão que correspondem exatamente aos requisitos de layout do seu projeto. Sinta‑se à vontade para experimentar diferentes dimensões de página, estilos ou até mesmo adicionar cabeçalhos e rodapés conforme necessário.

Se tiver dúvidas ou precisar de mais assistência, explore a [documentação do Aspose.HTML para Java](https://reference.aspose.com/html/java/) ou participe da conversa no [Aspose Forum](https://forum.aspose.com/).

---

**Última atualização:** 2025-11-29  
**Testado com:** Aspose.HTML para Java 24.11 (mais recente no momento da escrita)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}