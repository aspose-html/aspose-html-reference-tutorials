---
category: general
date: 2026-02-22
description: Crie um pool de threads fixo para converter HTML em PDF em lote de forma
  eficiente em Java. Aprenda um exemplo de pool de threads em Java que salva HTML
  como PDF rapidamente.
draft: false
keywords:
- create fixed thread pool
- convert html to pdf
- batch html to pdf
- thread pool java example
- save html as pdf
language: pt
og_description: Crie um pool de threads fixo para conversão em lote de HTML para PDF.
  Este guia orienta você através de um exemplo de pool de threads em Java que salva
  HTML como PDF de forma eficiente.
og_title: Criar pool de threads fixas para conversão em lote de HTML para PDF
tags:
- Java
- Concurrency
- PDF Generation
title: Criar pool de threads fixa para conversão em lote de HTML para PDF
url: /pt/java/conversion-html-to-other-formats/create-fixed-thread-pool-for-batch-html-to-pdf-conversion/
---

blocks unchanged.

At the end there is an incomplete code snippet: after "thread" truncated. We must preserve as is (the original content). Keep the truncated line.

Also there are closing shortcodes.

Let's produce final output.

Be careful with markdown tables: translate headers and content.

Also translate "Pro tip:" etc.

Let's write translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crie um Pool de Threads Fixas para Conversão em Lote de HTML para PDF

Já se perguntou como **criar um pool de threads fixas** que transforma uma pilha de arquivos HTML em PDFs sem sobrecarregar sua CPU? Você não está sozinho. Quando você tem dezenas — ou até centenas — de páginas para processar, executá‑las uma a uma é um peso, mas iniciar um pool de threads ilimitado pode rapidamente esgotar a memória.  

Neste tutorial vamos resolver esse dilema mostrando um **exemplo de pool de threads em Java** que **processa HTML em lote para PDF**, salva cada resultado e encerra tudo de forma limpa. Ao final você será capaz de **converter HTML para PDF** em paralelo e entenderá por que um pool de threads fixas é a escolha ideal para a maioria dos trabalhos em lote.

## O Que Você Vai Aprender

- Um programa Java completo e executável que cria um pool de threads fixas.  
- Explicação passo a passo de cada linha, para que você saiba **por que** fazemos o que fazemos.  
- Orientação sobre como escolher uma biblioteca PDF (para que você possa **salvar HTML como PDF** sem caçar trechos de código).  
- Dicas para lidar com erros, ajustar o tamanho do pool e estender a solução para lotes maiores.

**Pré‑requisitos** – Java 8+ instalado, uma IDE básica (IntelliJ, Eclipse ou VS Code) e uma biblioteca de conversão PDF no seu classpath (usaremos *OpenHTMLtoPDF* no exemplo). Nenhum outro framework é necessário.

---

## Crie um Pool de Threads Fixas – Por Que Isso Importa

Quando você **cria um pool de threads fixas**, informa à JVM exatamente quantas threads de trabalho podem ser executadas simultaneamente. Isso impede tempestades de criação de threads, mantém o uso de memória previsível e permite que o SO agende o trabalho de forma eficiente.  

Pense nisso como uma fila de caixas em um supermercado: você abre um número definido de caixas, deixa os clientes se alinharem e fecha as caixas quando a fila desaparece. Um `FixedThreadPool` funciona da mesma forma — as tarefas esperam sua vez, mas nenhuma thread extra é criada sob demanda.

```java
// Step 1: Build a fixed‑size thread pool with 4 workers
ExecutorService threadPool = Executors.newFixedThreadPool(4);
```

O número `4` é um bom ponto de partida em um laptop quad‑core; você pode ajustá‑lo com base nos núcleos da sua CPU e nas características de I/O.

## Conversão em Lote de HTML para PDF: Processando Cada Página

Agora que o pool existe, precisamos alimentá‑lo com tarefas que **convertem HTML para PDF**. Cada tarefa irá:

1. Carregar um documento HTML do disco.  
2. Passá‑lo para a biblioteca PDF.  
3. Gravar o PDF resultante de volta no mesmo diretório.

Como o trabalho é intensivo em I/O (leitura de arquivos, gravação de PDFs), um pool pequeno costuma ter desempenho melhor que um maior que fica ocioso aguardando o disco.

```java
// Step 2: Submit a conversion job for every HTML file you have
for (int i = 0; i < 4; i++) {
    final int pageIndex = i;               // capture loop variable for the lambda
    threadPool.submit(() -> {
        // Load the HTML file
        Path htmlPath = Paths.get("YOUR_DIRECTORY/page" + pageIndex + ".html");
        String html = Files.readString(htmlPath, StandardCharsets.UTF_8);

        // Convert and save as PDF
        Path pdfPath = Paths.get("YOUR_DIRECTORY/page" + pageIndex + ".pdf");
        convertHtmlToPdf(html, pdfPath);
    });
}
```

> **Dica de especialista:** Se você tem mais de quatro páginas, basta aumentar o limite do laço ou ler a lista de arquivos dinamicamente — `Files.list(Paths.get("YOUR_DIRECTORY")).filter(p -> p.toString().endsWith(".html"))` torna tudo simples.

## Exemplo de Pool de Threads em Java Explicado

Vamos destrinchar o **exemplo de pool de threads em Java** linha por linha para que você não esteja apenas copiando código, mas realmente entendendo o fluxo.

| Linha | O Que Faz | Por Que É Importante |
|------|--------------|--------------------|
| `ExecutorService threadPool = Executors.newFixedThreadPool(4);` | Instancia um pool com exatamente quatro threads. | Garante um número limitado de conversões simultâneas, evitando erros de falta de memória. |
| `for (int i = 0; i < 4; i++) { … }` | Itera sobre as páginas que você deseja processar. | O laço gera a criação das tarefas; você pode substituir o limite estático por uma lista dinâmica. |
| `final int pageIndex = i;` | Captura o índice do laço para uso dentro da lambda. | Sem `final` (ou efetivamente final) a lambda veria uma variável mutável, gerando nomes de arquivos incorretos. |
| `threadPool.submit(() -> { … });` | Envia um `Runnable` ao pool para execução assíncrona. | O pool agenda o runnable em uma thread ociosa, liberando a thread principal para continuar enfileirando trabalho. |
| `Files.readString(htmlPath, …);` | Lê o arquivo HTML para uma `String`. | Necessário porque a maioria das bibliotecas PDF aceita HTML como string ou stream. |
| `convertHtmlToPdf(html, pdfPath);` | Chama um método auxiliar que realiza a conversão real. | Mantém a lambda limpa e isola o código específico da biblioteca. |

A seguir está o método auxiliar completo usando **OpenHTMLtoPDF**, uma biblioteca leve que **salva HTML como PDF** com uma única chamada.

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

private static void convertHtmlToPdf(String html, Path outputPdf) throws IOException {
    try (OutputStream os = Files.newOutputStream(outputPdf)) {
        PdfRendererBuilder builder = new PdfRendererBuilder();
        builder.withHtmlContent(html, null);     // base URI is null because we use absolute paths
        builder.toStream(os);
        builder.run();                           // blocks until PDF is written
    } catch (Exception e) {
        // Wrap any checked exception as an unchecked one so the lambda can compile
        throw new RuntimeException("Failed to convert HTML to PDF for " + outputPdf, e);
    }
}
```

> **Por que OpenHTMLtoPDF?** É puro Java, sem dependências nativas, e respeita CSS, o que faz com que os PDFs resultantes se pareçam muito com as páginas web originais. Se preferir iText ou Flying Saucer, basta trocar a implementação dentro de `convertHtmlToPdf`.

## Salvar HTML como PDF – Escolhendo uma Biblioteca

Você pode se perguntar: “Qual biblioteca devo usar para **converter HTML para PDF**?” Aqui está uma comparação rápida:

| Biblioteca | Coordenadas Maven | Prós | Contras |
|------------|-------------------|------|---------|
| OpenHTMLtoPDF | `com.openhtmltopdf:openhtmltopdf-pdfbox:1.0.10` | Puro Java, bom suporte a CSS, leve | Recursos avançados de PDF limitados (ex.: criptografia) |
| iText 7 + html2pdf | `com.itextpdf:html2pdf:3.0.6` | Conjunto rico de recursos, suporte comercial | Requer licença paga para muitos casos de uso |
| Flying Saucer | `org.xhtmlrenderer:flying-saucer-pdf:9.1.22` | Maduro, funciona com versões antigas do Java | Mais lento em documentos grandes, cobertura de CSS menor |

Escolha a que melhor se adapta às necessidades do seu projeto. Para um trabalho de **batch HTML to PDF**, o OpenHTMLtoPDF costuma ser o ponto ideal: rápido, simples e gratuito.

## Encerramento Gracioso e Tratamento de Erros

Deixar o executor ativo pode impedir que sua JVM finalize, e exceções não capturadas dentro de uma thread podem ser difíceis de detectar. O padrão a seguir garante um encerramento ordenado:

```java
// Step 5: Initiate an orderly shutdown after all tasks are queued
threadPool.shutdown();                     // No new tasks accepted
try {
    // Wait up to 60 seconds for existing tasks to finish
    if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
        threadPool.shutdownNow();          // Force shutdown if tasks linger
    }
} catch (InterruptedException ex) {
    threadPool.shutdownNow();              // Preserve interrupt status
    Thread.currentThread().interrupt();
}
```

- `shutdown()` indica ao pool que termine o que está em andamento, mas rejeite novos trabalhos.  
- `awaitTermination` bloqueia até que tudo finalize ou o tempo limite expire.  
- `shutdownNow()` tenta cancelar tarefas em execução — útil para uma parada forçada.

Se alguma conversão falhar, a `RuntimeException` que lançamos sobe até o executor, que a registra no console por padrão. Em produção você poderia anexar um `ThreadPoolExecutor` customizado com o método `afterExecute` sobrescrito para registrar em arquivo ou sistema de monitoramento.

## Exemplo Completo e Funcional

Juntando tudo, aqui está uma classe Java autônoma que você pode copiar‑colar em `src/main/java/com/example/BatchPdfConverter.java`. Certifique‑se de que a dependência OpenHTMLtoPDF esteja no seu classpath.

```java
package com.example;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;
import java.util.concurrent.*;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;

/**
 * Demonstrates how to create a fixed thread pool to batch HTML to PDF conversion.
 * Adjust POOL_SIZE and DIRECTORY constants to fit your environment.
 */
public class BatchPdfConverter {

    private static final int POOL_SIZE = 4;                     // Number of parallel workers
    private static final Path DIRECTORY = Paths.get("YOUR_DIRECTORY"); // Change to your folder

    public static void main(String[] args) {
        ExecutorService threadPool = Executors.newFixedThreadPool(POOL_SIZE);

        // Discover all *.html files in the target directory
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(DIRECTORY, "*.html")) {
            for (Path htmlPath : stream) {
                threadPool.submit(() -> processFile(htmlPath));
            }
        } catch (IOException e) {
            System.err.println("Failed to list HTML files: " + e.getMessage());
        }

        // Graceful shutdown
        thread

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}