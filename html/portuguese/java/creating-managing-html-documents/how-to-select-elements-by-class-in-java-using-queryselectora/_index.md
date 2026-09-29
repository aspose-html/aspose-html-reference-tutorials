---
category: general
date: 2026-09-29
description: Aprenda a selecionar elementos por classe, ler HTML de um arquivo e encontrar
  links externos em Java. Este guia passo a passo aborda a iteração eficiente de um
  NodeList.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: pt
lastmod: 2026-09-29
og_description: Selecione elementos por classe em Java, leia HTML de um arquivo e
  encontre links externos usando querySelectorAll. Siga o exemplo completo para iterar
  um NodeList.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Selecionar elementos por classe em Java – guia completo com querySelectorAll
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: Como selecionar elementos por classe em Java usando querySelectorAll
url: /pt/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como selecionar elementos por classe em Java usando querySelectorAll

Se você precisa **selecionar elementos por classe** ao processar um arquivo HTML em Java, este guia mostra exatamente como fazer isso. Você aprenderá a ler HTML de um arquivo, usar `querySelectorAll` para encontrar links externos e percorrer o `NodeList` resultante com segurança.

Trabalhar com HTML em Java costuma parecer pesado, mas bibliotecas modernas oferecem uma API concisa baseada em seletores CSS. O exemplo abaixo usa **jsoup** (versão 1.17.2) porque ele implementa seletores no estilo `querySelectorAll` e devolve uma coleção `Elements` que se comporta como um `NodeList`. Você pode adaptar a mesma lógica para outras implementações de DOM, se necessário.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* JDK 17 ou superior instalado.
* Maven ou Gradle para gerenciamento de dependências.
* Familiaridade básica com streams Java e o modelo DOM.

Adicione o jsoup ao seu projeto:

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## Etapa 1: Ler HTML a partir do arquivo

A primeira tarefa é carregar o documento HTML do disco. `Jsoup.parse(Path, Charset)` lê o arquivo e constrói uma árvore DOM que pode ser consultada.

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*Por que isso importa*: Carregar o arquivo uma única vez evita I/O repetido enquanto você itera sobre os elementos depois. O objeto `Document` contém todo o DOM, permitindo consultas rápidas com seletores.

## Etapa 2: Usar `querySelectorAll` para selecionar elementos por classe

Agora que o documento está na memória, você pode **selecionar elementos por classe** usando um seletor CSS. O seletor `"a.external"` corresponde a tags `<a>` que possuem a classe `external` — exatamente o que você precisa para **encontrar links externos**.

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*Por que isso importa*: Usar um seletor de classe é ao mesmo tempo expressivo e performático. A biblioteca traduz o seletor em uma travessia otimizada, de modo que você não precise escrever loops manuais sobre cada nó.

## Etapa 3: Percorrer o NodeList (Elements) em Java

`Elements` implementa `Iterable<Element>`, o que significa que você pode usar um loop `for‑each` padrão para **iterar NodeList Java**. O loop abaixo imprime o atributo `href` de cada link.

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*Por que isso importa*: A iteração direta mantém o código legível e evita a sobrecarga de converter a coleção em um stream quando você só precisa de uma saída simples.

## Exemplo completo

Juntando as três etapas, obtém‑se um programa autocontido que pode ser executado a partir da linha de comando.

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### Saída esperada

Assumindo que `input.html` contenha:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

Executando o programa, a saída será:

```
External link: https://example.com
External link: https://openai.com
```

## Dicas avançadas e armadilhas comuns

* **Codificação importa** – Sempre leia o arquivo com UTF‑8 (ou o charset que corresponde à sua fonte). Codificação incorreta pode corromper caracteres nos valores dos atributos.
* **Múltiplas classes** – Se um elemento tem várias classes (ex.: `class="btn external"`), o seletor `"a.external"` ainda corresponde porque seletores de classe CSS verificam a presença do token, não a string exata.
* **Dica de performance** – Se você só precisa do atributo `href`, pode solicitá‑lo diretamente com `doc.select("a.external[href]").eachAttr("href")`. Isso evita a criação de objetos `Element` completos para cada correspondência.
* **Segurança contra null** – `link.attr("href")` devolve uma string vazia se o atributo estiver ausente, portanto não é necessário fazer verificação de null antes de imprimir.

## Perguntas frequentes

**Q: Isso funciona com fragmentos HTML que não possuem uma raiz `<html>`?**  
A: Sim. `Jsoup.parse` trata a entrada como um fragmento e adiciona automaticamente os elementos raiz que faltam, permitindo que os seletores funcionem no corpo do fragmento.

**Q: Posso usar `querySelectorAll` sem o jsoup?**  
A: A API DOM padrão do Java (`org.w3c.dom`) não inclui `querySelectorAll`. Bibliotecas como **HTMLUnit** ou **jodd-lagarto** fornecem métodos semelhantes. O padrão mostrado aqui — carregar, selecionar com CSS, iterar — permanece o mesmo.

**Q: E se eu precisar modificar os links ao invés de apenas imprimi‑los?**  
A: Após obter cada `Element`, você pode chamar `link.attr("href", "newUrl")` e então escrever o documento de volta ao disco com `Files.writeString`.

## Conclusão

Agora você sabe como **selecionar elementos por classe**, **ler HTML de um arquivo**, **encontrar links externos** e **iterar um NodeList em Java** usando seletores no estilo `querySelectorAll`. O exemplo completo demonstra um fluxo limpo e pronto para produção, que pode ser incorporado em pipelines maiores de raspagem ou transformação.

Em seguida, explore tópicos relacionados como **analisar conteúdo dinâmico com HTMLUnit**, **escrever HTML modificado de volta ao disco** ou **usar streams Java para coletar URLs de links em uma lista**. Cada um desses amplia a técnica central de seleção baseada em classe demonstrada aqui. Boa codificação!


## O que você deve aprender a seguir?


Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to query HTML in Java – Select elements, filter by attribute, and get text](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [Iterate NodeList Java – Read HTML & Get Image src](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}