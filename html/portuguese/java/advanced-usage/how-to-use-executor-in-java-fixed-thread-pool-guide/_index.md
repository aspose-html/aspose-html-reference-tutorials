---
category: general
date: 2026-05-28
description: como usar executor em Java com um pool de threads fixo, extrair texto
  de HTML e acelerar o processamento – um exemplo completo de pool de threads Java.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: pt
og_description: como usar executor em Java com um pool de threads fixo. Aprenda um
  exemplo completo de pool de threads Java que extrai texto de arquivos HTML de forma
  eficiente.
og_title: Como usar Executor em Java – Guia de Pool de Threads Fixas
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: how to use executor in Java with a fixed thread pool, extract text
    from HTML and speed up processing – a complete java thread pool example.
  headline: How to Use Executor in Java – Fixed Thread Pool Guide
  type: TechArticle
tags:
- Java
- Concurrency
- HTML Parsing
title: Como usar Executor em Java – Guia de Pool de Threads Fixas
url: /pt/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar Executor em Java – Guia de Pool de Threads Fixas

Já se perguntou **como usar executor** para executar muitas tarefas ao mesmo tempo sem estourar sua memória? Você não está sozinho. Em muitos aplicativos do mundo real, você precisará percorrer uma pasta de arquivos HTML, extrair o texto do corpo e fazer isso rapidamente — exatamente o cenário que este tutorial resolve.

Vamos percorrer uma implementação **fixed thread pool java** que extrai texto de HTML, imprime a contagem de caracteres de cada arquivo e encerra de forma limpa. Ao final, você terá um **java thread pool example** autônomo que pode inserir em qualquer projeto, além de algumas dicas sobre como personalizar o tamanho do pool e lidar com casos extremos.

> **O que você precisará**  
> * Java 17 (ou qualquer JDK recente)  
> * Uma pequena biblioteca de parsing de HTML – usaremos *jsoup* porque é testada em batalha e zero‑config.  
> * Um conjunto de arquivos *.html* de exemplo em um diretório de sua escolha.

---

## Como Usar Executor com um Pool de Threads Fixas

O coração de qualquer programa Java intensivo em concorrência é o `ExecutorService`. Ao criar um **fixed thread pool**, informamos à JVM para manter exatamente N threads de trabalho ativos, o que evita a sobrecarga de criação de threads e limita o uso de recursos.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Por que isso importa:*  
Se você iniciasse um novo `Thread` para cada arquivo HTML, o SO teria que agendar dezenas de threads em um laptop modesto, levando a trocas de contexto excessivas. Um pool fixo reutiliza as mesmas quatro threads, proporcionando um uso de CPU previsível.

---

## Defina os Arquivos HTML a Processar – Fixed Thread Pool Java

Em seguida listamos os arquivos que queremos alimentar ao pool. Em um aplicativo real, você provavelmente percorreria uma árvore de diretórios; aqui mantemos simples.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Dica:* `List.of` retorna uma lista imutável, que é segura para ser compartilhada entre threads sem sincronização extra.

---

## Envie uma Tarefa Separada para Cada Arquivo HTML

Agora entregamos cada caminho ao executor. A lambda que enviamos será executada **em paralelo** em uma das quatro threads de trabalho.

```java
// Step 3: Dispatch a parsing job for every file
for (String htmlFilePath : htmlFilePaths) {
    executor.submit(() -> {
        // Each lambda runs on a thread from the pool
        try {
            // Step 4: Open the document, extract its text, and display the length
            String text = extractBodyText(htmlFilePath);
            System.out.println(htmlFilePath + " → " + text.length() + " chars");
        } catch (IOException e) {
            System.err.println("Failed to read " + htmlFilePath);
            e.printStackTrace();
        }
    });
}
```

**Por que encapsulamos a lógica em um método** (`extractBodyText`) ficará claro na próxima seção — isso mantém a lambda organizada e nos permite reutilizar o código de extração em outros lugares.

---

## Extraia Texto de HTML – A Lógica Central

Aqui está o helper reutilizável que realmente **extrai texto de html** usando Jsoup. Ele abre o arquivo, analisa o DOM e retorna o texto puro do corpo.

```java
/**
 * Reads an HTML file and returns the plain text inside the <body>.
 *
 * @param path absolute or relative path to the .html file
 * @return body text without tags
 * @throws IOException if the file cannot be read
 */
private static String extractBodyText(String path) throws IOException {
    // Jsoup parses the file into a Document object.
    org.jsoup.nodes.Document doc = org.jsoup.Jsoup.parse(new java.io.File(path), "UTF-8");
    // getBody() gives us the <body> element; text() strips all tags.
    return doc.body().text();
}
```

*Por que Jsoup?* É leve, lida com marcação malformada de forma elegante e não requer um motor de navegador completo. O método lança `IOException` para que o chamador possa decidir como registrar ou recuperar — perfeito para um cenário de thread‑pool onde você não quer que um único arquivo problemático termine todo o executor.

---

## Encerre o Executor Graciosamente – Crie Fixed Thread Pool

Depois de enviarmos todos os trabalhos, devemos instruir o pool a parar de aceitar novas tarefas e a concluir as que já estão na fila.

```java
// Step 5: Initiate an orderly shutdown once all tasks are queued
executor.shutdown();
try {
    // Wait up to 30 seconds for all tasks to finish
    if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
        System.err.println("Timed out waiting for tasks; forcing shutdown.");
        executor.shutdownNow();
    }
} catch (InterruptedException ie) {
    // Preserve interrupt status and force shutdown
    Thread.currentThread().interrupt();
    executor.shutdownNow();
}
```

*Explicação:* `shutdown()` impede novas submissões, enquanto `awaitTermination` bloqueia até que cada tarefa de parsing termine (ou o tempo limite expire). Se algo travar, `shutdownNow()` tenta cancelar as tarefas em execução. Esse padrão é a forma recomendada de **create fixed thread pool** com segurança.

---

## Exemplo Completo e Executável

Juntando tudo, aqui está um único arquivo que você pode compilar e executar. Ele inclui as importações necessárias, o método `main` e o helper descrito acima.

```java
import java.io.IOException;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

/**
 * Demonstrates how to use executor with a fixed thread pool to
 * extract text from multiple HTML files concurrently.
 */
public class HtmlThreadPoolDemo {

    public static void main(String[] args) {
        // 1️⃣ Build a fixed‑size pool (adjust the size for your hardware)
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ Define the files we want to process
        List<String> htmlFilePaths = List.of(
                "YOUR_DIRECTORY/a.html",
                "YOUR_DIRECTORY/b.html",
                "YOUR_DIRECTORY/c.html",
                "YOUR_DIRECTORY/d.html"
        );

        // 3️⃣ Submit a parsing task for each file
        for (String htmlFilePath : htmlFilePaths) {
            executor.submit(() -> {
                try {
                    String text = extractBodyText(htmlFilePath);
                    System.out.println(htmlFilePath + " → " + text.length() + " chars");
                } catch (IOException e) {
                    System.err.println("Error processing " + htmlFilePath);
                    e.printStackTrace();
                }
            });
        }

        // 5️⃣ Shut down the pool cleanly
        executor.shutdown();
        try {
            if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("Tasks took too long; forcing shutdown.");
                executor.shutdownNow();
            }
        } catch (InterruptedException ie) {
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }

    /**
     * Reads an HTML file and returns the plain text inside the <body>.
     *
     * @param path path to the .html file
     * @return body text without markup
     * @throws IOException if file cannot be read
     */
    private static String extractBodyText(String path) throws IOException {
        Document doc = Jsoup.parse(new java.io.File(path), "UTF-8");
        return doc.body().text();
    }
}
```

**Saída esperada** (supondo que cada arquivo contenha aproximadamente 1 200 caracteres de texto do corpo):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

Se algum arquivo estiver ausente ou malformado, você verá um stack trace impresso em `stderr`, mas as demais tarefas continuarão inalteradas — exatamente o que um **java thread pool example** bem‑comportado deve fazer.

---

## Perguntas Frequentes & Casos Limites

| Pergunta | Resposta |
|----------|----------|
| *E se eu tiver mais de quatro arquivos?* | O pool enfileirará as tarefas extras e as executará assim que uma thread ficar livre. Nenhum código extra é necessário. |
| *Devo usar `newCachedThreadPool` em vez disso?* | `newCachedThreadPool` cria threads sob demanda e pode crescer indefinidamente, o que é arriscado para trabalhos intensivos em I/O. Um **fixed thread pool** oferece uso de memória e CPU previsível. |
| *Como mudar o tamanho do pool com base nos núcleos da CPU?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` é um padrão comum. |
| *E se o parsing falhar para um arquivo?* | O `catch (IOException e)` dentro da lambda isola a falha, registra‑a e permite que o restante do pool continue trabalhando. |
| *Posso retornar o texto extraído ao chamador?* | Sim — use `Future<String>` em vez de `submit(Runnable)`. O código ficaria assim `Future<String> f = executor.submit(() -> extractBodyText(path));` e depois `String result = f.get();`. |

---

## Conclusão

Cobri­mos **como usar executor** para iniciar um **fixed thread pool java** que processa uma coleção de arquivos HTML em paralelo, extrai o texto do corpo e relata a contagem de caracteres. O **java thread pool example** completo demonstra gerenciamento adequado de recursos, tratamento de erros e um método de extração reutilizável.

Próximos passos? Experimente trocar a implementação de `extractBodyText` por um scraper mais sofisticado, experimente um pool maior ou alimente os resultados em um banco de dados. Você também pode explorar `CompletionService` para recuperar resultados assim que estiverem prontos, o que é útil quando os tamanhos dos arquivos variam bastante.

Sinta‑se à vontade para ajustar o caminho do diretório, adicionar mais arquivos ou integrar este trecho em um framework de crawling maior. O padrão central — criar um pool, submeter tarefas independentes e encerrar graciosamente — permanece o mesmo, não importa quão complexo seu workload se torne.

Feliz codificação, e que suas threads permaneçam sempre vivas (até que você as encerre, é claro)!

## Tutoriais Relacionados

- [Fixed thread pool java – Limpeza Paralela de HTML com ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [Como Consultar HTML em Java – Tutorial Completo](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Como Usar Aspose.HTML para Java - Dominando a Renderização de Canvas HTML5](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}