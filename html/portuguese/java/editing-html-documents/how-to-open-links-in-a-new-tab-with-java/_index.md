---
category: general
date: 2026-10-28
description: Aprenda a abrir links em uma nova aba analisando HTML em Java, encontrando
  links externos e adicionando target="_blank".
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: pt
lastmod: 2026-10-28
og_description: 'Abrir links em uma nova aba usando Java: analisar HTML, encontrar
  links externos, adicionar target="_blank" e salvar o HTML modificado.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Abrir links em uma nova aba com Java – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: Como abrir links em uma nova aba com Java
url: /pt/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como abrir links em uma nova aba com Java

Se você precisa **abrir links em uma nova aba** a partir de um arquivo HTML estático, este guia mostra exatamente como fazer isso. Você aprenderá a **analisar HTML em Java**, **encontrar links externos**, **adicionar target blank**, e **salvar HTML modificado** sem sair do seu IDE.

Abrir links externos em uma nova aba do navegador melhora a experiência do usuário e mantém os visitantes na página original. A solução abaixo funciona com qualquer documento HTML, requer apenas a popular biblioteca jsoup e roda em Java 8 ou superior.

## Pré-requisitos

* JDK 8 + instalado  
* Uma ferramenta de build (Maven ou Gradle) para obter a dependência **jsoup**  
* Um arquivo HTML que contém tags de âncora com a classe `external`

Você não precisa de um servidor web ou de frameworks adicionais — o jsoup lida com tudo localmente.

## Etapa 1: Configurar o jsoup no seu projeto

Adicione o jsoup como dependência. Se você usa Maven, coloque isso em `pom.xml`:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Para Gradle, adicione a seguinte linha ao `build.gradle`:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## Etapa 2: Analisar o documento HTML

Analisar o arquivo é o primeiro passo para **abrir links em nova aba**. O método `Jsoup.parse` lê o arquivo em uma estrutura mutável semelhante a um DOM.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*Por que isso importa*: `Document` fornece seletores no estilo CSS, tornando trivial localizar os elementos que você precisa.

## Etapa 3: Encontrar links externos

Agora localize cada elemento `<a>` que possui a classe `external`. Isso corresponde ao requisito de **encontrar links externos**.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` é uma coleção de nós correspondentes. Se o seletor retornar um conjunto vazio, seu HTML pode não ter a classe ou usar uma convenção de nomenclatura diferente — ajuste o seletor conforme necessário.

## Etapa 4: Adicionar `target="_blank"` a cada link

Para cada nó retornado por **encontrar links externos**, defina o atributo `target` como `_blank`. Isso satisfaz a etapa de **adicionar target blank** e garante que os navegadores abram o link em uma nova aba.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

O método `attr` sobrescreve qualquer valor existente de `target`, garantindo comportamento consistente em todas as âncoras externas.

## Etapa 5: Salvar o HTML modificado

Depois de atualizar o DOM, escreva as alterações de volta para um arquivo. Isso completa a parte de **salvar HTML modificado** do tutorial.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` serializa o documento inteiro, preservando a indentação e a formatação como o jsoup originalmente o analisou.

## Exemplo completo em funcionamento

Juntando todas as etapas resulta em um programa autônomo que você pode copiar, colar e executar.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### Saída esperada

Suponha que `sample.html` contenha:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

Após executar o programa, `updated.html` conterá:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

Somente o link externo recebeu o atributo `target="_blank"`, o que significa que os navegadores agora o abrirão em uma nova aba.

## Dicas profissionais e armadilhas comuns

* **Dica profissional:** Se você precisar tratar links que começam com `http://` ou `https://` como externos mesmo sem uma classe CSS, expanda o seletor: `doc.select("a[href^=http]")`.
* **Caso de borda:** Algumas páginas já especificam `target="_self"`; a chamada `attr` sobrescreve isso, garantindo comportamento consistente.
* **Desempenho:** Para arquivos HTML muito grandes, considere o parsing em streaming (`Jsoup.parse(File, String, String, Parser.htmlParser())`) para reduzir o uso de memória.
* **Teste:** Verifique o resultado abrindo `updated.html` em um navegador e inspecionando o link com as ferramentas de desenvolvedor — procure o atributo `target`.

## Conclusão

Agora você tem uma solução completa e executável para **abrir links em uma nova aba** usando Java. O tutorial abordou como **analisar html em java**, **encontrar links externos**, **adicionar target blank**, e **salvar html modificado**, tudo com a leve biblioteca jsoup.

A partir daqui você pode:

* Expandir o seletor para lidar com outros padrões de link (ex.: `rel="external"`).  
* Combinar essa lógica com uma etapa de build que processe todos os arquivos HTML de um projeto.  
* Integrar o código em um pipeline de gerenciamento de conteúdo maior.

Sinta-se à vontade para experimentar diferentes seletores ou formatos de saída, e compartilhe seus resultados com a comunidade!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como usar CSS em Java – Carregar HTML, Contar Links e Avaliar XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [Como analisar HTML em Java – Extrair texto de artigos HTML](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Criar novo elemento html com Java – Guia completo do Aspose.HTML](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}