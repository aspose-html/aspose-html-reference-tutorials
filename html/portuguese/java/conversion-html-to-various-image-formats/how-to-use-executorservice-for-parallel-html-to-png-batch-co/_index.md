---
category: general
date: 2026-02-21
description: Como usar ExecutorService para converter HTML em PNG rapidamente. Aprenda
  a converter arquivos HTML em lote com tarefas paralelas em Java.
draft: false
keywords:
- how to use executorservice
- convert html to png
- how to run parallel tasks
- how to convert html to png
- batch convert html files
language: pt
og_description: Como usar ExecutorService para converter em lote arquivos HTML em
  PNG. Guia passo a passo com exemplo completo em Java.
og_title: Como usar ExecutorService para conversão paralela de HTML para PNG
tags:
- Java
- concurrency
- Aspose.HTML
- image‑conversion
title: Como usar ExecutorService para conversão em lote paralela de HTML para PNG
url: /pt/java/conversion-html-to-various-image-formats/how-to-use-executorservice-for-parallel-html-to-png-batch-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar ExecutorService para conversão em lote de HTML‑para‑PNG em paralelo

Já se perguntou **como usar ExecutorService** quando você tem uma pasta cheia de páginas HTML que precisam se tornar imagens PNG? Você não está sozinho — muitos desenvolvedores encontram esse obstáculo quando seu pipeline de web‑reporting trava em um loop de conversão monothread.  

A boa notícia? Com algumas linhas de Java e o poderoso Aspose.HTML `Converter`, você pode criar um pool de threads de trabalho, alimentar cada arquivo HTML ao conversor e observar as imagens sendo geradas em paralelo. Neste tutorial também abordaremos os fundamentos de **convert html to png**, mostraremos como **run parallel tasks**, e forneceremos um script pronto‑para‑executar de **batch convert html files**.

## Pré-requisitos

- Java 17 ou posterior (o código usa a moderna API `java.nio.file`).  
- Biblioteca Aspose.HTML for Java no seu classpath. Você pode obtê-la no Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

- Um diretório que contém os arquivos `.html` de origem e uma pasta de saída vazia.  
- Uma quantidade modesta de RAM — cada conversão roda em sua própria thread, portanto o tamanho do pool deve corresponder ao número de núcleos de CPU que você possui.

> **Dica profissional:** Se você está em uma máquina com hyper‑threading, `Runtime.getRuntime().availableProcessors()` geralmente retorna a contagem ideal de núcleos.

## Etapa 1 – Definir caminhos de entrada e saída

Primeiro precisamos informar ao Java onde o HTML está localizado e onde os PNGs devem ser gravados. Usar objetos `Path` mantém o código independente de plataforma.

```java
import java.nio.file.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Input folder containing .html files
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        // Output folder for the generated .png files
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");

        // Ensure the output folder exists
        Files.createDirectories(outputDir);
```

> **Por que isso importa:** Criar o diretório de saída antecipadamente evita `FileNotFoundException` quando a primeira thread de trabalho tenta gravar um arquivo.

## Etapa 2 – Construir um pool de threads de tamanho fixo

O coração de **how to use ExecutorService** está em criar um pool que corresponda ao seu hardware. Um pool *fixo* garante que não criaremos mais threads do que realmente podemos executar.

```java
        // Create a thread pool sized to the number of available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());
```

> **Explicação:** `ExecutorService` abstrai o gerenciamento de threads de baixo nível. Ao usar `newFixedThreadPool`, deixamos a JVM reutilizar threads, o que reduz a sobrecarga de criar e destruir constantemente.

## Etapa 3 – Enviar uma tarefa de conversão por arquivo HTML

Agora percorremos o diretório de entrada, selecionamos cada arquivo `*.html` e o entregamos ao pool. Cada tarefa é uma pequena lambda que chama `Converter.convert`.

```java
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        // Build the output filename by swapping .html for .png
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();

                        // Perform the actual conversion
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }
```

### O que está acontecendo nos bastidores?

1. **DirectoryStream** lê os nomes dos arquivos de forma preguiçosa, então o uso de memória permanece baixo mesmo com milhares de arquivos.  
2. A lambda captura `htmlFile` e `outputDir` — não há necessidade de uma classe `Runnable` separada.  
3. `Converter.convert` é uma chamada bloqueante que lê o HTML, renderiza e grava um PNG. Como cada chamada roda em sua própria thread, vários arquivos são processados simultaneamente — exatamente o comportamento esperado ao **run parallel tasks**.

## Etapa 4 – Encerrar o pool graciosamente

Depois que todas as tarefas são enfileiradas, instruímos o pool a parar de aceitar novo trabalho e esperar que tudo termine. Se algo travar, o tempo limite abortará após uma hora, o que é generoso para a maioria dos trabalhos em lote.

```java
        // No more tasks will be submitted
        pool.shutdown();

        // Wait up to 1 hour for all conversions to complete
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }

        System.out.println("All conversions completed.");
    }
}
```

> **Caso extremo:** Se você tem arquivos HTML excepcionalmente grandes, pode querer aumentar o tempo limite ou monitorar o uso de memória. Adicionar `pool.setRejectedExecutionHandler(new ThreadPoolExecutor.CallerRunsPolicy())` força a thread chamadora a executar tarefas excedentes, evitando `RejectedExecutionException`.

## Exemplo completo, pronto‑para‑executar

Abaixo está o programa completo, pronto para copiar e colar em um único arquivo `ParallelBatchConversion.java`.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.*;
import java.util.concurrent.*;

public class ParallelBatchConversion {
    public static void main(String[] args) throws Exception {
        // Step 1: Define source and destination folders
        Path inputDir  = Paths.get("YOUR_DIRECTORY/input/html");
        Path outputDir = Paths.get("YOUR_DIRECTORY/output/png");
        Files.createDirectories(outputDir);

        // Step 2: Create a thread pool sized to the available CPU cores
        ExecutorService pool = Executors.newFixedThreadPool(
                Runtime.getRuntime().availableProcessors());

        // Step 3: Submit a conversion task for each HTML file found
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(inputDir, "*.html")) {
            for (Path htmlFile : stream) {
                pool.submit(() -> {
                    try {
                        String outputFile = outputDir.resolve(
                                htmlFile.getFileName().toString().replaceAll("\\.html$", ".png"))
                                .toString();
                        Converter.convert(htmlFile.toString(), outputFile);
                        System.out.println("Converted: " + htmlFile.getFileName());
                    } catch (Exception e) {
                        System.err.println("Failed: " + htmlFile.getFileName()
                                           + " – " + e.getMessage());
                    }
                });
            }
        }

        // Step 4: Shut down the pool and wait for all conversions to finish
        pool.shutdown();
        if (!pool.awaitTermination(1, TimeUnit.HOURS)) {
            System.err.println("Timeout: some files didn't finish in time.");
        }
        System.out.println("All conversions completed.");
    }
}
```

### Saída esperada

Executar o programa imprime uma linha para cada conversão bem‑sucedida:

```
Converted: report1.html
Converted: dashboard.html
Converted: summary.html
All conversions completed.
```

Se um arquivo falhar, você verá uma linha de erro com a mensagem da exceção, facilitando a depuração.

## Como estender esse padrão

- **Different image formats:** Troque a extensão `.png` por `.jpg` ou `.bmp` e ajuste as opções de conversão do Aspose adequadamente.  
- **Dynamic thread count:** Para cargas de trabalho I/O‑bound você pode aumentar o tamanho do pool (`availableProcessors() * 2`).  
- **Progress monitoring:** Substitua `System.out.println` por uma biblioteca de barra de progresso thread‑safe como `jline` ou registre em um arquivo.  
- **Error handling:** Colete os caminhos que falharam em um `List<Path>` e tente novamente após o término do loop principal.

## Perguntas Frequentes

**Q: Isso funciona no Windows e Linux?**  
A: Sim. `java.nio.file` abstrai o sistema de arquivos subjacente, então o mesmo código roda sem alterações em qualquer SO que suporte Java.

**Q: E se eu tiver mais de 10 000 arquivos HTML?**  
A: O iterador `DirectoryStream` lê as entradas de forma preguiçosa, portanto a memória permanece baixa. Apenas certifique‑se de que seu disco tenha espaço livre suficiente para a saída PNG.

**Q: Posso limitar a memória que cada conversão usa?**  
A: Aspose.HTML permite configurar o motor de renderização via `HtmlLoadOptions` e `ImageSaveOptions`. Você pode definir um tamanho máximo de bitmap ou habilitar renderização de baixa qualidade para manter o consumo de RAM sob controle.

## Conclusão

Percorremos **how to use ExecutorService** para **batch convert html files** em imagens PNG, explicamos por que um pool de tamanho fixo é o ponto ideal para renderização CPU‑bound, e fornecemos um programa Java completo, pronto‑para‑copiar‑colar. Seguindo os passos acima, você transformará um loop lento e monothread em um pipeline rápido e escalável que pode lidar com milhares de arquivos com um único comando.

Pronto para o próximo desafio? Experimente substituir `Converter.convert` pela exportação PDF da Aspose para **convert html to pdf**, ou integre essa lógica em um microserviço Spring Boot que aceita solicitações de upload‑e‑conversão. A ideia central — usar `ExecutorService` para **run parallel tasks** — permanece a mesma, e você a encontrará útil em inúmeros cenários de processamento em lote.

Feliz codificação, e que suas threads estejam sempre vivas! 

![how to use executorservice diagram](placeholder.png "Diagram illustrating the thread pool workflow for parallel HTML‑to‑PNG conversion")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}