---
category: general
date: 2026-06-19
description: Aprenda como gerar PDF a partir de HTML usando um exemplo simples em
  Java. Este tutorial de HTML para PDF mostra como converter um arquivo HTML em PDF
  com o OpenHTMLtoPDF.
draft: false
keywords:
- html to pdf tutorial
- generate pdf from html
- convert html file pdf
- create pdf from html
- convert webpage to pdf
language: pt
og_description: O tutorial html para pdf mostra como gerar PDF a partir de HTML usando
  Java. Siga os passos para converter rapidamente um arquivo HTML em PDF.
og_title: 'Tutorial de HTML para PDF: Guia de conversão Java'
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  headline: 'html to pdf tutorial: Convert HTML to PDF in Java'
  type: TechArticle
- description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  name: 'html to pdf tutorial: Convert HTML to PDF in Java'
  steps:
  - name: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
    text: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
  - name: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
    text: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
  - name: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
    text: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: 'Tutorial de HTML para PDF: Converta HTML em PDF em Java'
url: /pt/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial html para pdf – Transforme uma página HTML em PDF com Java

Já se perguntou como transformar uma página HTML estática em um documento PDF elegante sem sair do seu IDE? Você não está sozinho. Neste **html to pdf tutorial** vamos percorrer um exemplo completo, pronto‑para‑executar em Java que **generate pdf from html** em apenas alguns minutos.

Cobriremos tudo o que você precisa — configuração do projeto, adição da biblioteca correta, escrita do código de conversão e até uma dica rápida para converter uma página da web ao vivo em PDF. Ao final, você será capaz de **convert html file pdf** na sua própria máquina e entenderá como **create pdf from html** para qualquer projeto futuro.

## O que você precisará

- Java 17 ou mais recente (o código funciona com qualquer JDK recente)
- Maven ou Gradle (mostraremos o trecho Maven)
- Um pequeno arquivo HTML que você deseja transformar em PDF (criaremos um rapidamente)
- Uma IDE ou um editor de texto simples — você decide

É isso. Sem servidores pesados, sem SDKs pagos, apenas Java puro e uma biblioteca gratuita e de código aberto.

## Etapa 1: html to pdf tutorial – Configurar um projeto Maven

Primeiro, o básico. Crie um novo projeto Maven (ou adicione a um existente). A única dependência que você realmente precisa é **OpenHTMLtoPDF**, que faz o trabalho pesado de renderizar HTML e CSS em um PDF.

```xml
<!-- pom.xml snippet -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>html-to-pdf-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- OpenHTMLtoPDF core -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-pdfbox</artifactId>
            <version>1.0.10</version>
        </dependency>
        <!-- Optional: support for SVG, if your HTML uses it -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-svg-support</artifactId>
            <version>1.0.10</version>
        </dependency>
    </dependencies>
</project>
```

> **Dica profissional:** Se você estiver usando Gradle, as mesmas dependências podem ser adicionadas em `implementation` no `build.gradle`.  

Por que esta etapa importa: sem a biblioteca, a JVM não tem ideia de como traduzir tags HTML em comandos de desenho PDF. OpenHTMLtoPDF é leve, mantida ativamente e funciona com CSS‑2.1, portanto seu estilo permanece intacto.

## Etapa 2: generate pdf from html – Preparar um arquivo HTML de exemplo

Vamos criar um pequeno `input.html` ao lado do nosso código Java. Isso mantém o exemplo autocontido e demonstra o fluxo de trabalho **create pdf from html**.

```html
<!-- src/main/resources/input.html -->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Sample Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        h1 { color: #2E86C1; }
        p { line-height: 1.5; }
    </style>
</head>
<body>
    <h1>Monthly Sales Report</h1>
    <p>This PDF was generated directly from an HTML file using Java.</p>
    <p>All you need is a few lines of code.</p>
</body>
</html>
```

Você pode substituir o conteúdo por qualquer coisa — tabelas, imagens, até JavaScript (embora o renderizador ignore scripts). A parte importante é que o arquivo esteja no classpath para que o conversor possa localizá‑lo.

## Etapa 3: convert html file pdf – Escrever a utilidade de conversão

Agora o coração do **html to pdf tutorial**: uma pequena classe `HtmlToPdfConverter` que lê o HTML e grava um PDF. O código abaixo é um exemplo completo e executável; copie‑e cole em `src/main/java/com/example/HtmlToPdfConverter.java`.

```java
package com.example;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;

/**
 * Simple utility that converts an HTML file to PDF.
 * It demonstrates the "convert html file pdf" use‑case.
 */
public class HtmlToPdfConverter {

    /**
     * Converts the given HTML file to a PDF file.
     *
     * @param htmlPath path to the source HTML file (can be absolute or classpath)
     * @param pdfPath  destination path for the generated PDF
     * @throws IOException if reading or writing fails
     */
    public static void convert(String htmlPath, String pdfPath) throws IOException {
        // Resolve the HTML file – support both absolute paths and classpath resources
        InputStream htmlStream = Files.exists(Path.of(htmlPath))
                ? Files.newInputStream(Path.of(htmlPath))
                : HtmlToPdfConverter.class.getResourceAsStream(htmlPath);

        if (htmlStream == null) {
            throw new FileNotFoundException("HTML source not found: " + htmlPath);
        }

        // Ensure the output directory exists
        Path pdfFile = Path.of(pdfPath);
        Files.createDirectories(pdfFile.getParent());

        try (OutputStream os = Files.newOutputStream(pdfFile);
             InputStream is = htmlStream) {

            // Builder does the heavy lifting – it parses HTML + CSS and writes PDF bytes
            new PdfRendererBuilder()
                    .withHtmlContent(new String(is.readAllBytes()), null) // base URI null = no external resources
                    .toStream(os)
                    .run();
        }
    }

    // Demo entry point – feel free to run this class directly
    public static void main(String[] args) {
        // Step 1: Specify the input HTML file location
        String htmlPath = "src/main/resources/input.html";

        // Step 2: Specify the desired output PDF file location
        String pdfPath = "target/output.pdf";

        // Step 3: Convert the HTML document to PDF using default conversion settings
        try {
            convert(htmlPath, pdfPath);
            System.out.println("✅ PDF successfully created at " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Por que este código funciona

1. **Resource flexibility** – o método primeiro verifica se o caminho fornecido aponta para um arquivo real; caso contrário, recorre a um recurso do classpath. Isso significa que você pode **convert webpage to pdf** mais tarde fornecendo uma string URL (basta substituir a chamada `withHtmlContent` por `withUri`).

2. **Automatic directory creation** – `Files.createDirectories` garante que a pasta `target/` exista, evitando o erro “No such file or directory”.

3. **Single‑line conversion** – `PdfRendererBuilder` lida com CSS, fontes e layout de página internamente. Não há necessidade de gerenciar manualmente as páginas PDF; a biblioteca faz isso por você, mantendo o exemplo curto e focado no conceito **convert html file pdf**.

## Etapa 4: create pdf from html – Executar o programa e verificar

Abra um terminal na raiz do projeto e execute:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HtmlToPdfConverter
```

Se tudo estiver configurado corretamente, você verá:

```
✅ PDF successfully created at target/output.pdf
```

Abra `target/output.pdf` com qualquer visualizador de PDF. Você deverá ver o cabeçalho estilizado “Monthly Sales Report”, o texto do parágrafo e as mesmas margens que você definiu no bloco `<style>` do HTML.

> **E se você não vir o estilo?**  
> Certifique‑se de que o CSS esteja inline ou localizado na mesma pasta que o HTML. OpenHTMLtoPDF resolve URLs relativas com base no URI base que você passa para `withHtmlContent`. No trecho acima passamos `null`, o que funciona para CSS inline simples. Para folhas de estilo externas, forneça o caminho do diretório como segundo argumento.

## Etapa 5: convert webpage to pdf – Manipulando URLs remotas (opcional)

Às vezes você precisa **convert webpage to pdf** diretamente da internet — pense em arquivar um recibo online. A biblioteca suporta isso via `withUri`. Aqui está uma rápida adaptação:

```java
public static void convertUrl(String url, String pdfPath) throws IOException {
    Path pdfFile = Path.of(pdfPath);
    Files.createDirectories(pdfFile.getParent());

    try (OutputStream os = Files.newOutputStream(pdfFile)) {
        new PdfRendererBuilder()
                .withUri(url)          // Load HTML from the web
                .toStream(os)
                .run();
    }
}
```

Chame assim:



## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Converter HTML para PDF em Java – Usando Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Converter HTML para PDF em Java – Configurando o Ambiente no Aspose.HTML](/html/english/java/configuring-environment/)
- [Converter HTML para PDF em Java – Guia passo a passo com configurações de tamanho de página](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}