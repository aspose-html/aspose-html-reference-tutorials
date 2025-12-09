---
date: 2025-12-05
description: Aprenda como definir margens de página HTML usando Java com Aspose.HTML
  e adicionar números de página e títulos aos seus documentos.
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: Como definir margens de página HTML em Java com Aspose.HTML
url: /pt/java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Definir Margens de Página HTML em Java com Aspose.HTML

Neste tutorial você descobrirá **como definir margens de página HTML em Java** usando Aspose.HTML for Java. Vamos percorrer a criação de margens de página personalizadas, inserção de números de página e adição de um título ao documento — tudo com código passo a passo que você pode copiar para seu próprio projeto.

## Respostas Rápidas
- **Qual biblioteca é necessária?** Aspose.HTML for Java  
- **Posso controlar as margens programaticamente?** Sim, via uma regra CSS `@page` na folha de estilos do usuário  
- **Quais formatos de saída suportam margens?** XPS, PDF e outros formatos raster  
- **Preciso de licença para produção?** Uma licença válida do Aspose.HTML é necessária para uso não‑trial  
- **É compatível com Java 11+?** Absolutamente – a biblioteca funciona com versões modernas do Java  

## O que Significa “Definir Margens de Página HTML em Java”?
Definir margens de página HTML em Java significa configurar o motor de renderização (fornecido pelo Aspose.HTML) para aplicar propriedades CSS de caixa de página antes que o documento seja convertido para um formato imprimível como XPS ou PDF. Ao definir uma regra `@page` personalizada, você controla a área imprimível, os números de página e o conteúdo de cabeçalho/rodapé.

## Por Que Usar Aspose.HTML para Controle de Margens?
- **Layout preciso** – CSS `@page` oferece controle pixel‑a‑pixel sobre margens, cabeçalhos e rodapés.  
- **Consistência entre formatos** – As mesmas definições de margem funcionam para XPS, PDF e saídas de imagem.  
- **Sem dependência de navegador** – A renderização ocorre no servidor, dispensando um navegador headless.  

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem os seguintes pré‑requisitos:

1. **Ambiente de Desenvolvimento Java** – JDK 11 ou superior instalado.  
2. **Aspose.HTML for Java** – Baixe e instale a biblioteca a partir de [here](https://releases.aspose.com/html/java/).  

## Importar Pacotes

Para iniciar, importe as classes necessárias do Aspose.HTML:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## Como Definir Margens de Página HTML em Java – Guia Passo a Passo

### Etapa 1: Inicializar Configuração e Definir Margens de Página Personalizadas

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

Neste bloco criamos um objeto `Configuration`, obtemos o `IUserAgentService` e injetamos uma regra CSS `@page` que define as margens, um contador de página no canto inferior‑direito e um título do documento no topo central.

### Etapa 2: Criar o Documento HTML

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Aqui instanciamos um `HTMLDocument` com um trecho simples “Hello World”. A mesma configuração da Etapa 1 é aplicada, de modo que as margens personalizadas são respeitadas ao renderizar o documento.

### Etapa 3: Renderizar para um Arquivo XPS (ou qualquer saída suportada)

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Esta etapa cria um `XpsDevice` que grava as páginas renderizadas em `output.xps`. As margens, números de página e título definidos anteriormente aparecerão no arquivo final.

## Problemas Comuns & Dicas

- **As margens parecem inalteradas** – Garanta que a regra `@page` não seja sobrescrita por outras folhas de estilo. A chamada `setUserStyleSheet` a força com prioridade máxima.  
- **Números de página exibem “NaN”** – Verifique se está usando o Aspose.HTML versão 23.10 ou mais recente; versões anteriores não possuem a função `currentPageNumber()`.  
- **Arquivo de saída está em branco** – Confirme se o caminho `Resources.output` está resolvido corretamente e se você tem permissão de escrita.  

## Perguntas Frequentes

### Q1: O que é Aspose.HTML for Java?

**R:** Aspose.HTML for Java é uma biblioteca Java que fornece ferramentas poderosas para trabalhar com documentos HTML em aplicações Java, incluindo conversão, renderização e manipulação.

### Q2: Posso personalizar ainda mais as margens da página?

**R:** Sim, basta editar o CSS dentro de `setUserStyleSheet`. Você pode alterar quaisquer valores `margin-*` ou adicionar caixas `@top-*` / `@bottom-*` adicionais.

### Q3: Como posso adicionar mais conteúdo ao documento HTML?

**R:** Substitua a string em `new HTMLDocument("<div>Hello World!!!</div>", …)` pelo seu próprio markup HTML, ou carregue um arquivo externo usando o construtor `HTMLDocument(String url, …)`.

### Q4: O Aspose.HTML for Java é compatível com outros formatos de documento?

**R:** Absolutamente. O mesmo `HTMLDocument` pode ser renderizado para PDF, XPS, imagens ou até EPUB trocando o dispositivo de saída (por exemplo, `PdfDevice`, `PngDevice`).

### Q5: Preciso de licença para usar Aspose.HTML for Java?

**R:** Sim, uma licença é exigida para uso em produção. Você pode obter uma licença trial ou comprar uma licença em [here](https://purchase.aspose.com/buy) ou [here](https://releases.aspose.com/).

### Q6: Como definir margens diferentes para páginas ímpares e pares?

**R:** Use as pseudo‑classes `@page :left` e `@page :right` dentro da sua folha de estilos para definir margens distintas para páginas à esquerda (pares) e à direita (ímpares).

### Q7: Posso incorporar fontes personalizadas no documento renderizado?

**R:** Sim. Adicione regras `@font-face` à folha de estilos do usuário e faça referência às fontes no seu conteúdo HTML.

## Conclusão

Agora você domina **como definir margens de página HTML em Java** usando Aspose.HTML, e sabe como adicionar números de página e um título para tornar seus documentos mais profissionais. Sinta‑se à vontade para experimentar caixas `@page` adicionais, fontes customizadas ou diferentes formatos de saída conforme as necessidades do seu projeto.

Se encontrar algum desafio, a documentação oficial do [Aspose.HTML for Java](https://reference.aspose.com/html/java/) e o [fórum de suporte da Aspose](https://forum.aspose.com/) são excelentes fontes de ajuda.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Última Atualização:** 2025-12-05  
**Testado Com:** Aspose.HTML for Java 23.12  
**Autor:** Aspose  

---