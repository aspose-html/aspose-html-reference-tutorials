---
category: general
date: 2026-06-07
description: Converta HTML em PDF usando o ExecutorService do Java. Aprenda como converter
  arquivos HTML em lote, salvar documento HTML como PDF e encerrar o ExecutorService
  de forma elegante.
draft: false
keywords:
- convert html to pdf
- save html document as pdf
- shutdown executorservice gracefully
- batch convert html to pdf
language: pt
og_description: Converter HTML para PDF usando o ExecutorService do Java. Domine a
  conversão em lote, salvando o documento HTML como PDF, e o encerramento adequado
  do ExecutorService.
og_title: Converter HTML em PDF com Java – Guia de Lote Paralelo
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  headline: Convert HTML to PDF with Java – Parallel Batch Guide
  type: TechArticle
- description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  name: Convert HTML to PDF with Java – Parallel Batch Guide
  steps:
  - name: The HTML file is read into a string.
    text: The HTML file is read into a string.
  - name: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
    text: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
  - name: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
    text: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
  type: HowTo
tags:
- Java
- Concurrency
- PDF Generation
title: Converter HTML em PDF com Java – Guia de Lote Paralelo
url: /pt/java/conversion-html-to-other-formats/convert-html-to-pdf-with-java-parallel-batch-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter HTML para PDF com Java – Guia de Processamento em Lote Paralelo

Já precisou **converter HTML para PDF** mas se sentiu preso lidando com dezenas de arquivos? Você não está sozinho — muitos desenvolvedores enfrentam esse obstáculo ao criar geradores de relatórios ou exportadores de faturas. A boa notícia? Com algumas linhas de Java e um pool de threads inteligente, você pode **converter HTML para PDF em lote** em um instante, **salvar documento HTML como PDF**, e ainda **encerrar o ExecutorService graciosamente** quando o trabalho terminar.

Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar. Você verá por que um pool de threads de tamanho fixo é a escolha ideal para conversão paralela, como o código de conversão realmente se parece, e os passos exatos para terminar o executor de forma limpa. Ao final, você terá um programa autônomo que pode ser inserido em qualquer projeto — sem peças faltando, sem links vagos “veja a documentação”.

---

## O que você vai construir

- Um aplicativo console Java que lê uma lista de arquivos HTML locais.  
- Cada arquivo é passado para uma thread de trabalho que cria uma versão PDF.  
- O aplicativo usa **ExecutorService** para executar as conversões em paralelo.  
- Quando todas as tarefas são enfileiradas, o pool é **encerrado graciosamente**, garantindo que nenhuma thread fique pendente.

**Pré‑requisitos**  
- Java 17 (ou qualquer JDK recente).  
- Uma biblioteca PDF que possa renderizar HTML, como **OpenHTMLtoPDF**, **iText** ou **Flying Saucer**. No código referenciamos uma classe placeholder `HTMLDocument`; substitua‑a pela API da sua biblioteca.  
- Conhecimento básico de concorrência em Java (nada avançado).

---

![Diagram showing batch conversion of HTML files to PDF using ExecutorService](batch-convert-diagram.png "Convert HTML to PDF in parallel with ExecutorService")
*Alt text: Diagrama mostrando conversão em lote de arquivos HTML para PDF usando ExecutorService*

## Converter HTML para PDF em Paralelo (Conversão em Lote de HTML para PDF)

Quando você tem dezenas — ou até milhares — de arquivos HTML, convertê‑los um a um na thread principal se torna um gargalo. Um pool de threads de tamanho fixo permite que a JVM reutilize um número definido de threads de trabalho, mantendo o uso da CPU alto sem sobrecarregar o sistema.

```java
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

/**
 * Simple demo that batch converts HTML files to PDF using a fixed thread pool.
 * Replace HTMLDocument with the actual class from your chosen PDF library.
 */
public class HtmlToPdfBatch {

    public static void main(String[] args) {
        // 1️⃣ Prepare a list of HTML files to convert
        List<String> htmlPaths = List.of(
            "src/main/resources/page1.html",
            "src/main/resources/page2.html",
            "src/main/resources/page3.html"
        );

        // 2️⃣ Create a fixed‑size thread pool – 4 workers is a good starting point
        ExecutorService pool = Executors.newFixedThreadPool(4);

        // 3️⃣ Submit a conversion task for each HTML file
        for (String htmlPath : htmlPaths) {
            pool.submit(() -> convertAndSave(htmlPath));
        }

        // 4️⃣ Shutdown ExecutorService gracefully – no new tasks, wait for running ones
        shutdownGracefully(pool);
    }

    /**
     * Core conversion logic – this is where we **save HTML document as PDF**.
     */
    private static void convertAndSave(String htmlPath) {
        try {
            // Imagine HTMLDocument is from OpenHTMLtoPDF, iText, etc.
            HTMLDocument doc = new HTMLDocument(htmlPath);
            String pdfPath = htmlPath.replace(".html", ".pdf");
            doc.save(pdfPath);
            System.out.println("✅ Converted: " + htmlPath + " → " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Failed to convert " + htmlPath + ": " + e.getMessage());
        }
    }

    /**
     * Helper that **shutdowns ExecutorService gracefully**.
     */
    private static void shutdownGracefully(ExecutorService executor) {
        executor.shutdown(); // stop accepting new tasks
        try {
            // Wait a maximum of 60 seconds for existing tasks to finish
            if (!executor.awaitTermination(60, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("⚠️ Pool didn’t terminate in time – forcing shutdown");
                executor.shutdownNow(); // cancel currently executing tasks
            } else {
                System.out.println("🛑 All tasks completed – executor shut down cleanly.");
            }
        } catch (InterruptedException ie) {
            // Preserve interrupt status & force shutdown
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }
}
```

### Por que isso funciona

- **Parallelism**: Cada chamada `submit` entrega a conversão a uma thread de trabalho, de modo que quatro arquivos podem ser processados simultaneamente em uma máquina quad‑core.  
- **Isolation**: O método `convertAndSave` contém toda a lógica necessária para **salvar documento HTML como PDF**, facilitando a troca da biblioteca subjacente mais tarde.  
- **Graceful termination**: Ao chamar `shutdown()` primeiro, informamos ao pool “não há mais trabalho, por favor finalize o que está em andamento”. O loop `awaitTermination` dá a essas threads a chance de concluir, e só se elas forem teimosas invocamos `shutdownNow()`. Esse padrão é a forma recomendada de **encerrar o ExecutorService graciosamente**.

## Salvar Documento HTML como PDF – Lógica Central de Conversão

O coração de qualquer fluxo de **convert HTML to PDF** é a biblioteca de conversão. Embora o exemplo use um `HTMLDocument` fictício, aqui está um rápido vislumbre de como você poderia fazer isso com **OpenHTMLtoPDF**:

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

public class HTMLDocument {
    private final String htmlPath;

    public HTMLDocument(String htmlPath) {
        this.htmlPath = htmlPath;
    }

    public void save(String pdfPath) throws IOException {
        try (OutputStream os = new FileOutputStream(pdfPath);
             InputStream is = new FileInputStream(htmlPath)) {

            PdfRendererBuilder builder = new PdfRendererBuilder();
            builder.withHtmlContent(new String(is.readAllBytes()), null);
            builder.toStream(os);
            builder.run();
        }
    }
}
```

**O que está acontecendo?**  
1. O arquivo HTML é lido para uma string.  
2. `PdfRendererBuilder` analisa a marcação, aplica CSS e transmite o resultado para um arquivo PDF.  
3. Qualquer `IOException` sobe até `convertAndSave`, onde registramos sucesso ou falha.

Sinta‑se à vontade para substituir este trecho pelo `HtmlConverter.convertToPdf` do iText ou pelo `ITextRenderer` do Flying Saucer. O código que envolve o pool de threads permanece exatamente o mesmo, e é por isso que enfatizamos **salvar documento HTML como PDF** como uma preocupação separada.

## Encerrar ExecutorService Graciosamente – Melhores Práticas

Um erro comum é chamar `shutdownNow()` imediatamente após submeter as tarefas. Isso interrompe abruptamente as threads, podendo deixar arquivos PDF parcialmente gravados no disco. O padrão que usamos — `shutdown()` → `awaitTermination()` → opcional `shutdownNow()` — garante:

- **No new tasks** são aceitas depois que tudo foi enfileirado.  
- **Running tasks** têm a chance de terminar de forma limpa.  
- **Blocked threads** são interrompidas somente se excederem um timeout razoável (aqui, 60 segundos).  

Se você espera PDFs muito grandes ou um motor de renderização lento, aumente o timeout ou use `executor.invokeAll(tasks, timeout, unit)` para um controle mais rigoroso.

## Exemplo Completo em Funcionamento (Todas as Peças Juntas)

A seguir está o programa inteiro que você pode copiar‑colar em um único arquivo `HtmlToPdfBatch.java`. Basta adicionar a dependência OpenHTMLtoPDF (ou sua biblioteca preferida) ao seu `pom.xml` ou build Gradle, e está pronto para usar.

```java
// HtmlToPdfBatch.java
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

public class HtmlToPdfBatch {

    public static void main(String[] args) {
        List<String> htmlPaths = List.of(
            "src/main/resources/page1.html",
            "src/main/resources/page2.html",
            "src/main/resources/page3.html"
        );

        ExecutorService pool = Executors.newFixedThreadPool(4);
        for (String path : htmlPaths) {
            pool.submit(() -> convertAndSave(path));
        }
        shutdownGracefully(pool);
    }

    private static void convertAndSave(String htmlPath) {
        try {
            HTMLDocument doc = new HTMLDocument(htmlPath);
            String pdfPath = htmlPath.replace(".html", ".pdf");
            doc.save(pdfPath);
            System.out.println("✅ Converted: " + htmlPath + " → " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Failed to convert " + htmlPath + ": " + e.getMessage());
        }
    }

    private static void shutdownGracefully(ExecutorService executor) {
        executor.shutdown();
        try {
            if (!executor.awaitTermination(60, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("⚠️ Pool didn’t terminate in time – forcing shutdown");
                executor.shutdownNow();
            } else {
                System.out.println("🛑 All tasks completed – executor shut down cleanly.");
            }
        } catch (InterruptedException ie) {
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }
}

// Helper class – replace with your real PDF library calls
class HTMLDocument {
    private final String htmlPath;

    HTMLDocument(String htmlPath) {
        this.htmlPath = htmlPath;
    }

    void save(String pdfPath) throws IOException {
        try (InputStream is = new FileInputStream(htmlPath);
             OutputStream os = new FileOutputStream(pdfPath)) {

            PdfRendererBuilder builder = new PdfRendererBuilder();
            builder.withHtmlContent(new String(is.readAllBytes()), null);
            builder.toStream(os


## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Converter HTML para PDF em Java – Usando Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Converter HTML para PDF em Java – Configurando o Ambiente no Aspose.HTML](/html/english/java/configuring-environment/)
- [Converter HTML para PDF em Java – Guia passo a passo com Configurações de Tamanho de Página](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}