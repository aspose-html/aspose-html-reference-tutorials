---
category: general
date: 2026-10-28
description: Como ler HTML em Java e extrair texto de arquivos HTML. Aprenda a converter
  HTML em texto com Jsoup, abordando a leitura de HTML a partir de arquivos e técnicas
  de HTML para texto em Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: pt
lastmod: 2026-10-28
og_description: Como ler HTML em Java e extrair texto de arquivos HTML. Este tutorial
  mostra uma solução completa para converter HTML em texto usando Jsoup.
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: Como ler HTML e extrair texto em Java – guia rápido
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  headline: How to read HTML and extract text in Java – a step‑by‑step guide
  type: TechArticle
- description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  name: How to read HTML and extract text in Java – a step‑by‑step guide
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>org.jsoup</groupId> <artifactId>jsoup</artifactId>
      <version>1.17.2</version> </dependency> ```'
  - name: Gradle
    text: '```gradle implementation ''org.jsoup:jsoup:1.17.2'' ```'
  - name: Expected output
    text: 'Assuming `input.html` contains:'
  - name: Running the program
    text: '```bash javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java java -cp .:jsoup-1.17.2.jar
      HtmlToTextDemo ```'
  type: HowTo
tags:
- Java
- HTML parsing
- Text extraction
title: Como ler HTML e extrair texto em Java – um guia passo a passo
url: /pt/java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como ler HTML e extrair texto em Java – um guia passo a passo

Se você precisa **como ler html** a partir de um arquivo local, este guia oferece uma solução completa. Você aprenderá a carregar um documento HTML, extrair o texto puro e, opcionalmente, converter HTML em texto com controle detalhado. Ao final do tutorial, você poderá executar o código de exemplo e ver o texto extraído impresso no console.

Ler arquivos HTML é uma tarefa comum ao processar dados extraídos da web, gerar relatórios ou limpar conteúdo gerado por usuários. As etapas abaixo cobrem tudo o que você precisa, desde adicionar a biblioteca necessária até lidar com casos extremos, como marcação malformada ou problemas de codificação de caracteres.

## O que você precisará

- Java 17 ou superior (o código também compila em versões anteriores)
- Maven ou Gradle para gerenciamento de dependências, ou o JAR do Jsoup adicionado manualmente
- Um arquivo HTML chamado `input.html` colocado no diretório `src/main/resources` do projeto (você pode alterar o caminho depois)

## Configurar a biblioteca Jsoup

Jsoup é uma biblioteca leve e bem documentada que analisa HTML em uma estrutura semelhante a DOM. Ela lida com HTML quebrado de forma elegante, o que a torna ideal para tarefas de **extrair texto de html**.

### Maven

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

### Gradle

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Se preferir um download manual, coloque o JAR no seu classpath e importe `org.jsoup.*` no seu arquivo fonte.

## Carregar HTML a partir de um arquivo

A primeira etapa programática é ler o arquivo em um objeto `Document`. Jsoup oferece um método estático `parse` que aceita um `File` e o nome de um charset.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Path to the HTML file – adjust if your file lives elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Parse the file using UTF‑8 encoding
            Document doc = Jsoup.parse(input, "UTF-8");
            // Continue with text extraction…
        } catch (IOException e) {
            System.err.println("Failed to read the HTML file: " + e.getMessage());
        }
    }
}
```

**Por que isso importa:** `Jsoup.parse(File, String)` lê os bytes brutos, decodifica-os de acordo com o charset fornecido e constrói um DOM limpo. Essa abordagem é mais segura do que ler o arquivo em uma string manualmente, pois o Jsoup normaliza quebras de linha e corrige erros de marcação comuns automaticamente.

## Extrair texto puro do HTML

Depois de ter um `Document`, recuperar o texto visível é uma única chamada de método. O método `text()` concatena o conteúdo textual de todos os elementos, descartando tags, scripts e estilos.

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

A chamada `body()` limita a extração ao elemento `<body>`, que é o alvo típico quando você **lê html de um arquivo** para análise de conteúdo. A string resultante contém espaços em branco colapsados em espaços únicos, imitando como um navegador renderizaria o texto.

### Saída esperada

Assumindo que `input.html` contenha:

```html
<!DOCTYPE html>
<html>
<head><title>Sample</title></head>
<body>
  <h1>Hello World</h1>
  <p>This is a <strong>demo</strong> page.</p>
</body>
</html>
```

Executando o programa, imprime:

```
Extracted text:
Hello World This is a demo page.
```

## Converter HTML em texto com opções adicionais

Às vezes você precisa de mais controle do que o `text()` oferece — por exemplo, preservar quebras de linha, manter a numeração de listas ou ignorar certas tags. O `NodeTraversor` do Jsoup combinado com um `NodeVisitor` personalizado fornece essa flexibilidade.

```java
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

public class HtmlToTextDemo {

    // ... (main method unchanged)

    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();
        NodeVisitor visitor = new NodeVisitor() {
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Preserve line breaks for block elements
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }
            public void tail(Node node, int depth) {
                // No action needed on exit
            }
        };
        NodeTraversor.traverse(visitor, doc.body());
        // Collapse multiple newlines into a single one
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

Substitua a simples chamada `doc.body().text()` por:

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**Por que isso funciona:** O visitante percorre o DOM em profundidade, adicionando uma nova linha antes de cada elemento de nível de bloco (ex.: `<p>`, `<div>`, `<h1>`). Isso mantém a separação de parágrafos, o que é útil quando você **converte html em texto** para legibilidade ou pipelines de NLP posteriores.

## Armadilhas comuns e boas práticas

| Problema | Por que ocorre | Correção recomendada |
|----------|----------------|----------------------|
| Charset errado | Arquivos salvos em ISO‑8859‑1 mas analisados como UTF‑8 produzem caracteres corrompidos. | Detecte o charset a partir da meta tag do arquivo (`<meta charset="...">`) ou passe o nome correto para `Jsoup.parse`. |
| Arquivos grandes | Carregar um arquivo HTML muito grande na memória pode causar `OutOfMemoryError`. | Faça streaming do arquivo com `Jsoup.parse(File, String, String baseUri)` e processe os nós incrementalmente, ou aumente o tamanho do heap da JVM. |
| Texto indesejado de script/estilo | `text()` remove o conteúdo de script e estilo, mas visitantes personalizados podem incluí-lo inadvertidamente. | Pule nós cujo nome da tag seja `script` ou `style` dentro do método `head` do visitante. |
| Preservar espaços em branco | Colapsar espaços pode perder a formatação necessária para conversão em markdown. | Use `Element.wholeText()` para nós de texto brutos e, em seguida, processe manualmente os espaços em branco. |

Abordar essas questões garante que sua solução **html to text java** funcione de forma confiável em diferentes entradas.

## Exemplo completo executável

Abaixo está um programa autônomo que demonstra todo o fluxo de trabalho — desde a configuração de dependências até a verificação da saída. Copie o código para um arquivo chamado `HtmlToTextDemo.java`, coloque um arquivo `input.html` ao lado dele e execute `javac && java` conforme mostrado.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Adjust the path if your HTML file is located elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Load and parse the HTML file using UTF‑8
            Document doc = Jsoup.parse(input, "UTF-8");

            // Simple extraction – suitable for most cases
            String plain = doc.body().text();
            System.out.println("=== Simple extraction ===");
            System.out.println(plain);
            System.out.println();

            // Detailed conversion – keeps line breaks for readability
            String detailed = convertHtmlToText(doc);
            System.out.println("=== Detailed conversion ===");
            System.out.println(detailed);
        } catch (IOException e) {
            System.err.println("Error reading HTML file: " + e.getMessage());
        }
    }

    /**
     * Walks the DOM and builds a text representation that preserves
     * line breaks for block‑level elements.
     *
     * @param doc the parsed HTML document
     * @return a readable plain‑text version of the HTML body
     */
    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();

        NodeVisitor visitor = new NodeVisitor() {
            @Override
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Add a newline before block elements (e.g., <p>, <div>, <h1>)
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }

            @Override
            public void tail(Node node, int depth) {
                // No operation needed when exiting a node
            }
        };

        NodeTraversor.traverse(visitor, doc.body());

        // Collapse consecutive newlines and trim leading/trailing whitespace
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

### Executando o programa

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

O console exibe tanto a extração simples quanto a detalhada

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como usar XPath em Java – Ler HTML e Extrair Texto](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [Como analisar HTML em Java – Extrair Texto de Artigos HTML](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Extrair texto de HTML com Java – Guia completo passo a passo](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}