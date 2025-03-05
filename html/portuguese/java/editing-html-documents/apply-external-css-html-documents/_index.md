---
title: Aplicar CSS externo a documentos HTML em Aspose.HTML para Java
linktitle: Aplicar CSS externo a documentos HTML em Aspose.HTML para Java
second_title: Processamento HTML Java com Aspose.HTML
description: Descubra como aplicar CSS externo a documentos HTML usando Aspose.HTML para Java! Siga este guia passo a passo para um tutorial completo.
type: docs
weight: 12
url: /pt/java/editing-html-documents/apply-external-css-html-documents/
---
## Introdução
Ao trabalhar com documentos HTML, aplicar estilos pode fazer toda a diferença na apresentação e na experiência do usuário. Se você está mergulhando em Java e quer aprender como aplicar estilos CSS externos aos seus documentos HTML usando a biblioteca Aspose.HTML, você está no lugar certo! Este guia tem como objetivo iluminar o processo passo a passo, tornando-o fácil até mesmo para aqueles que podem ser novos em Java ou CSS.
## Pré-requisitos
Antes de mergulhar no código, há algumas coisas que você precisa ter em mente:
### 1. Kit de desenvolvimento Java (JDK)
 Certifique-se de ter o JDK instalado em sua máquina. Você pode baixar a versão mais recente em[Site Java da Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
### 2. Aspose.HTML para Java
Você precisará ter o Aspose.HTML para Java configurado. Se você ainda não fez isso, vá para o[Página de downloads do Aspose](https://releases.aspose.com/html/java/) e pegue a biblioteca.
### 3. Um IDE ou editor de texto
Escolha um Ambiente de Desenvolvimento Integrado (IDE) como IntelliJ IDEA, Eclipse ou até mesmo um editor de texto simples para escrever seu código Java.
### 4. Conhecimento básico de Java
A familiaridade com a programação Java e noções básicas de CSS certamente ajudará você a acompanhar com mais conforto.
## Pacotes de importação
Depois de ter tudo configurado, o próximo passo é importar os pacotes necessários no seu projeto Java. Aqui está o que você precisa:
```java
import com.aspose.html.HTMLDocument;
```
Essas importações permitirão que você manipule documentos HTML e os renderize em diferentes formatos, como PDF.

Vamos dividir nosso tutorial em etapas gerenciáveis. Cada etapa guiará você pelo processo de aplicação de estilos CSS externos a um documento HTML usando Aspose.HTML para Java.
## Etapa 1: Crie um documento HTML
Primeiro, precisamos criar nosso documento HTML. Começaremos definindo o conteúdo com uma estrutura HTML simples.
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

 Aqui, definimos uma estrutura HTML básica, incluindo um`<div>` com dois parágrafos. O`HTMLDocument` A classe é usada para criar uma representação de documento do nosso conteúdo HTML.
## Etapa 2: Crie um elemento de estilo
 Em seguida, criaremos um`style` elemento para armazenar nossas regras CSS.
```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

 Usando o`createElement` método de`HTMLDocument` , criamos um novo`<style>` elemento e definir seu conteúdo para incluir nossas definições CSS para duas classes:`frame1` e`frame2`. Essas classes definem margens, preenchimento, dimensões, cores de fundo, famílias de fontes e cores de texto.
## Etapa 3: Acrescente o estilo ao cabeçalho do documento
Agora que temos nosso CSS pronto, precisamos acrescentar nosso elemento de estilo ao cabeçalho do documento.
```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

 Recuperamos o cabeçalho do documento e anexamos nosso recém-criado`style` elemento. Esta ação integra efetivamente nosso CSS ao documento HTML, permitindo que ele estilize nosso conteúdo HTML.
## Etapa 4: aplicar classes a elementos HTML
Em seguida, aplicaremos as classes CSS definidas anteriormente aos nossos elementos de parágrafo.
```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

Aqui, acessamos os elementos do primeiro e último parágrafo no documento e atribuímos a eles as classes CSS que criamos. Essa atribuição garante que eles sigam os estilos definidos em nosso CSS.
## Etapa 5: Defina propriedades de estilo adicionais
Para melhorar ainda mais a aparência, definiremos propriedades de estilo adicionais para nossos parágrafos.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

Nesta etapa, estamos ajustando nossos estilos. O tamanho da fonte do primeiro parágrafo é aumentado e centralizado, enquanto a cor, o tamanho da fonte e a família da fonte do último parágrafo são definidos. Esse refinamento é crucial para a legibilidade e o apelo estético.
## Etapa 6: Salve o documento HTML
Depois de aplicar nossos estilos, é hora de salvar o documento HTML.
```java
document.save("edit-internal-css.html");
```

 Aqui, utilizamos o`save` método do`HTMLDocument` classe para gravar o conteúdo HTML modificado em um arquivo, preservando assim nossos estilos e alterações.
## Etapa 7: Renderizar o documento em PDF
Por fim, vamos renderizar o documento em formato PDF para saída.
```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

 Usando o`PdfDevice` classe, configuramos a renderização do nosso documento HTML em um PDF. Esta etapa é essencial quando você deseja compartilhar o documento estilizado em um formato universalmente acessível.
## Conclusão
E aí está — aplicar CSS externo a documentos HTML usando Aspose.HTML para Java é simples e recompensador! Com apenas algumas linhas de código, você pode transformar texto simples em documentos visualmente atraentes e com estilo profissional. Então, se você está projetando para uso pessoal, criando relatórios ou desenvolvendo conteúdo da web, entender como manipular HTML e CSS em Java é uma habilidade poderosa para ter em seu kit de ferramentas.
## Perguntas frequentes
### O que é Aspose.HTML para Java?
Aspose.HTML para Java é uma biblioteca poderosa que permite aos desenvolvedores trabalhar com documentos HTML em aplicativos Java, fornecendo uma ampla gama de recursos, desde manipulação de HTML até renderização.
### Preciso de uma conexão com a Internet para usar o Aspose.HTML?
Não, depois de baixar os arquivos de biblioteca necessários, você pode usar o Aspose.HTML offline.
### Posso aplicar vários arquivos CSS a um documento HTML?
 Sim, você pode criar vários`<link>` elementos e anexá-los ao cabeçalho do documento para vários arquivos CSS.
### Existe alguma diferença entre CSS interno e externo?
Sim! O CSS interno é definido dentro de um documento HTML, enquanto o CSS externo é colocado em um arquivo separado e vinculado ao documento.
### Como posso obter suporte para Aspose.HTML para Java?
 Você pode acessar o suporte da comunidade por meio do[Fórum Aspose](https://forum.aspose.com/c/html/29) para quaisquer dúvidas ou problemas que você possa encontrar.