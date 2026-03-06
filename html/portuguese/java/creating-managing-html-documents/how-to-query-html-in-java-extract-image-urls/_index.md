---
category: general
date: 2026-03-05
description: Como consultar HTML em Java para ler um arquivo HTML e extrair imagens.
  Aprenda a ler arquivos HTML em Java, obter URLs de imagens em Java e iterar sobre
  NodeList em Java.
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: pt
og_description: Como consultar HTML em Java e recuperar URLs de imagens. Este guia
  mostra como ler um arquivo HTML em Java, localizar imagens e iterar sobre NodeList
  em Java.
og_title: Como consultar HTML em Java – Extrair URLs de imagens
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: Como Consultar HTML em Java – Extrair URLs de Imagens
url: /pt/java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Consultar HTML em Java – Extrair URLs de Imagens

Já se perguntou **como consultar HTML** em Java para extrair todas as imagens de uma página? Você não está sozinho—desenvolvedores precisam constantemente ler arquivos HTML, raspar imagens e fazer algo útil com as URLs. Neste tutorial, vamos percorrer um exemplo prático que mostra exatamente **como consultar HTML**, ler um arquivo HTML ao estilo Java e obter URLs de imagens em Java.

Usaremos o Aspose.HTML para Java, mas os conceitos—XPath, seletores CSS e iteração sobre um `NodeList`—se aplicam a qualquer biblioteca DOM. Ao final deste guia, você estará confortável com **como extrair imagens**, saberá **como iterar sobre NodeList Java** e terá um trecho de código pronto‑para‑usar que pode inserir em seu projeto.

![Exemplo de como consultar HTML em Java](https://example.com/placeholder.png "Como consultar HTML em Java")

---

## O Que Você Vai Aprender

- Carregar um documento HTML a partir do disco (read HTML file Java)  
- Localizar tags `<img>` usando tanto XPath quanto seletores CSS (how to extract images)  
- Percorrer o `NodeList` resultante (iterate over NodeList Java)  
- Imprimir o atributo `src` de cada imagem (get image URLs Java)

Sem serviços externos, sem ferramentas de build complexas—apenas Java puro e uma única dependência Maven.

---

## Pré‑requisitos

- Java 8 ou superior instalado  
- Maven ou Gradle para gerenciamento de dependências  
- Familiaridade básica com a estrutura HTML  
- Opcional, mas útil: um arquivo HTML simples (`sample.html`) contendo alguns elementos `<figure><img …></figure>`

Se você tem isso, podemos começar imediatamente.

---

## Etapa 1: Read HTML File Java – Carregar o Documento

Primeiro de tudo: precisamos trazer o HTML para a memória. A classe `HTMLDocument` do Aspose.HTML faz o trabalho pesado. Pense nela como abrir um livro para poder folhear qualquer página.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.NodeList;
import com.aspose.html.dom.Element;

/**
 * Demonstrates how to query HTML in Java and extract image URLs.
 */
public class QueryExample {
    public static void main(String[] args) throws Exception {

        // ① Load the HTML document from a local file.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

**Por que isso importa:** Carregar o arquivo fornece uma árvore DOM que você pode consultar. Se o caminho estiver errado, você receberá um `FileNotFoundException`, então verifique a localização antes de executar.

---

## Etapa 2: Localizar Imagens com XPath – How to Extract Images

XPath é uma linguagem de consulta poderosa que permite apontar nós com precisão laser. Aqui pedimos por cada `<img>` dentro de um `<figure>` que também possua um atributo `alt`.

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**Por que XPath?** É conciso e funciona mesmo quando o HTML está bagunçado. A expressão `//figure/img[@alt]` traduz‑se para: “qualquer `<img>` sob um `<figure>` que tenha um atributo `alt`.” Se precisar filtrar por outros atributos, basta ajustar os colchetes.

---

## Etapa 3: Localizar Imagens com Seletor CSS – Alternative Way to Extract Images

Às vezes você prefere a sintaxe CSS porque ela reflete o que escreve em folhas de estilo. `querySelectorAll` aceita o mesmo seletor que você usaria em um navegador.

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**Por que ambos?** Demonstrar as duas abordagens mostra que você pode escolher a ferramenta com a qual se sente mais confortável. Na prática, você usaria apenas uma, mas ter ambos os exemplos torna o tutorial mais completo.

---

## Etapa 4: Iterate Over NodeList Java – Get Image URLs Java

Agora que temos uma coleção, precisamos percorrê‑la. É aqui que **iterate over NodeList Java** entra em ação. Vamos extrair o atributo `src` de cada imagem e imprimi‑lo.

```java
        // ④ Loop through the NodeList returned by the CSS query.
        for (int i = 0; i < cssImages.getLength(); i++) {
            Element imageElement = (Element) cssImages.item(i);
            // Extract the "src" attribute – that’s the image URL.
            System.out.println("Image src: " + imageElement.getAttribute("src"));
        }
    }
}
```

**Por que um loop `for` clássico?** O `NodeList` da Aspose não implementa `Iterable`, então a sintaxe aprimorada `for‑each` não compila. Usar um loop por índice é a forma confiável de **iterate over NodeList Java**.

---

## Saída Esperada

Executar o programa contra um HTML de exemplo como:

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

Produzirá algo semelhante a:

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

Se o seu arquivo contiver mais tags `<img>` que atendam ao critério, o número aumentará proporcionalmente.

---

## Armadilhas Comuns & Dicas Profissionais

- **Problemas de caminho de arquivo:** Use um caminho absoluto ou coloque `sample.html` relativo ao diretório de trabalho do seu projeto.  
- **Atributo `alt` ausente:** Nossas consultas XPath/CSS filtram por `[@alt]`. Se precisar *de todas* as imagens, remova o filtro de atributo (`//figure/img` ou `figure img`).  
- **Desempenho:** Para documentos muito grandes, considere analisadores de streaming, mas para a maioria das tarefas de web‑scraping a abordagem DOM é suficiente.  
- **Problemas de codificação:** Aspose.HTML respeita o charset declarado no HTML. Se vir caracteres estranhos, garanta que o arquivo esteja salvo como UTF‑8.  

---

## Expandindo o Exemplo

Agora que você pode **get image URLs Java**, talvez queira:

1. **Baixar as imagens** usando `java.net.URL` e `Files.copy`.  
2. **Armazenar URLs em um banco de dados** para processamento posterior.  
3. **Filtrar por extensão de arquivo** (`src.endsWith(".png")`).  

Todas essas são extensões diretas do loop mostrado na Etapa 4.

---

## Conclusão

Neste guia abordamos **como consultar HTML** em Java do início ao fim: carregamento do arquivo, localização de imagens com XPath e seletores CSS, e **iterar sobre NodeList Java** para imprimir o `src` de cada imagem. Agora você tem uma base sólida para **como extrair imagens**, e sabe exatamente **como ler HTML file Java** usando Aspose.HTML.

Sinta‑se à vontade para adaptar o código às suas necessidades de scraping—seja extraindo outros atributos, manipulando tags `<a>`, ou enviando as URLs para um downloader. O padrão permanece o mesmo: carregar, consultar, iterar e agir.

Tem perguntas ou quer compartilhar um caso de uso interessante? Deixe um comentário abaixo e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}