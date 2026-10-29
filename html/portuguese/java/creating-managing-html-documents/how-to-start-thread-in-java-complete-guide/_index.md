---
category: general
date: 2026-06-19
description: Como iniciar uma thread em Java com um Runnable reutilizável, iniciar
  múltiplas threads, imprimir o nome da thread e analisar HTML com Java. Exemplo passo
  a passo.
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: pt
og_description: Como iniciar uma thread em Java usando Runnable, executar múltiplas
  threads, imprimir o nome da thread e analisar HTML com Java em um único exemplo
  executável.
og_title: Como iniciar uma thread em Java – Guia completo
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to start thread in Java with a reusable Runnable, start multiple
    threads, print thread name, and parse HTML with Java. Step‑by‑step example.
  headline: How to start thread in Java – Complete Guide
  type: TechArticle
tags:
- java
- multithreading
- html-parsing
- runnable
title: Como iniciar uma thread em Java – Guia completo
url: /pt/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como iniciar thread em Java – Guia Completo

Já se perguntou **como iniciar thread** em Java sem se afogar em código boilerplate? Você não está sozinho. Seja construindo um rastreador web, um atualizador de UI, ou apenas precisando descarregar um cálculo pesado, dominar a criação de threads é uma habilidade indispensável para qualquer desenvolvedor Java.

Neste tutorial vamos percorrer um cenário prático: **parse HTML with Java**, imprimir o nome da thread atual e **start multiple threads** que compartilham a mesma lógica. Ao final você saberá **how to use Runnable**, iniciar vários workers e ver a saída esperada — tudo em um exemplo **self‑contained** que você pode copiar e colar agora mesmo.

## O que você aprenderá

- Os passos exatos **how to start thread** usando a classe `Thread` e um `Runnable`.
- Como **start multiple threads** que executam a mesma tarefa sem duplicar código.
- A maneira mais simples de **print thread name** ao lado dos resultados do seu processamento.
- Um método limpo para **parse HTML with Java** usando um helper leve `HTMLDocument` (ou qualquer parser que preferir).
- Por que **how to use runnable** é importante para código reutilizável e testável.

Nenhuma biblioteca externa é necessária para o exemplo principal, mas indicaremos onde você pode trocar por Jsoup ou outro parser se precisar de mais recursos.

---

## Etapa 1: Definir uma tarefa reutilizável – **how to use runnable**

A primeira coisa que você precisa saber **how to use runnable** é encapsular o trabalho que deseja que cada thread execute. Um `Runnable` é apenas uma interface funcional com um único método `run()`, o que o torna perfeito para expressões lambda.

```java
// Define the reusable task
Runnable extractTextLength = () -> {
    // Open the HTML file inside a try‑with‑resources block
    try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
        // Get the length of the body text
        int textLength = doc.getBody().getTextContent().length();

        // Print the thread name and the length
        System.out.println(Thread.currentThread().getName() + ": " + textLength);
    } catch (Exception e) {
        e.printStackTrace();
    }
};
```

**Por que isso importa:** Ao manter a lógica dentro de um `Runnable`, você pode entregá‑la a qualquer número de objetos `Thread`, a um pool de threads ou até mesmo a um executor service posteriormente. Isso mantém seu código DRY e testável.

---

## Etapa 2: **How to start thread** – criar o primeiro worker

Agora que temos um `Runnable`, iniciar uma thread é tão fácil quanto chamar o construtor `Thread`. A pergunta **how to start thread** é respondida em uma única linha:

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

Observe o segundo argumento, `"Worker-1"`. Esse nome aparecerá quando mais tarde **print thread name**, tornando a depuração muito menos críptica.

---

## Etapa 3: **Start multiple threads** – reutilizar o mesmo Runnable

Quer processar vários arquivos HTML ao mesmo tempo? Basta iniciar outra `Thread` com o mesmo `Runnable`. Isso demonstra **start multiple threads** sem copiar o código da tarefa:

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

Tanto `Worker-1` quanto `Worker-2` executarão o bloco definido em `extractTextLength` simultaneamente. Como a tarefa é sem estado (apenas lê um arquivo), não há condição de corrida a se preocupar.

---

## Etapa 4: **Print thread name** ao analisar HTML

Dentro do `Runnable` já chamamos `Thread.currentThread().getName()`. Essa é a forma canônica de **print thread name**. A saída será algo como isto (supondo que o corpo do HTML contenha 1 234 caracteres):

```
Worker-1: 1234
Worker-2: 1234
```

Se você executar o programa em um arquivo maior, cada linha mostrará o mesmo comprimento porque ambas as threads leem o mesmo arquivo. Altere o caminho ou passe o nome do arquivo como parâmetro para ver resultados diferentes.

---

## Etapa 5: Exemplo completo e executável – da importação à execução

Abaixo está o programa completo, **self‑contained**, que você pode colocar em um arquivo chamado `HtmlThreadDemo.java`. Ele inclui um pequeno stub `HTMLDocument` para que o código compile mesmo que você não tenha um parser real disponível. Substitua o stub por Jsoup ou qualquer biblioteca que preferir para uso em produção.

```java
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Minimal HTMLDocument helper.
 * In a real project you would use Jsoup or another robust parser.
 */
class HTMLDocument implements AutoCloseable {
    private final String content;

    private HTMLDocument(String html) {
        this.content = html;
    }

    public static HTMLDocument load(String path) throws IOException {
        String html = new String(Files.readAllBytes(Paths.get(path)));
        return new HTMLDocument(html);
    }

    public Body getBody() {
        // Very naive extraction of <body>...</body>
        int start = content.indexOf("<body");
        if (start == -1) return new Body("");
        start = content.indexOf('>', start) + 1;
        int end = content.indexOf("</body>", start);
        if (end == -1) end = content.length();
        return new Body(content.substring(start, end));
    }

    @Override
    public void close() {
        // No resources to free in this stub
    }

    /** Simple wrapper for body text */
    static class Body {
        private final String text;
        Body(String text) { this.text = text; }
        public String getTextContent() { return text; }
    }
}

public class HtmlThreadDemo {

    public static void main(String[] args) {
        // Step 1: Define a reusable task (how to use runnable)
        Runnable extractTextLength = () -> {
            try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
                int textLength = doc.getBody().getTextContent().length();
                // Step 4: Print thread name and length
                System.out.println(Thread.currentThread().getName() + ": " + textLength);
            } catch (Exception e) {
                e.printStackTrace();
            }
        };

        // Step 2 & 3: How to start thread and start multiple threads
        new Thread(extractTextLength, "Worker-1").start();
        new Thread(extractTextLength, "Worker-2").start();
    }
}
```

### Saída esperada

Assumindo que `page.html` contenha 2 567 caracteres dentro da tag `<body>`, você verá algo como:

```
Worker-1: 2567
Worker-2: 2567
```

Se o arquivo não puder ser lido, o stack trace será impresso — graças ao bloco `catch`.

---

## Armadilhas Comuns & Dicas Profissionais

| Problema | Por que acontece | Correção |
|----------|------------------|----------|
| **File not found** | O caminho `"YOUR_DIRECTORY/page.html"` é relativo ao local onde você inicia a JVM. | Use um caminho absoluto ou `Paths.get("").toAbsolutePath()` para depurar. |
| **Race conditions** | Se o `Runnable` muta estado compartilhado, as threads podem entrar em conflito. | Mantenha a tarefa sem estado, ou sincronize o acesso a objetos compartilhados. |
| **Too many threads** | Criar dezenas de `Thread`s pode esgotar os recursos do SO. | Mude para um `ExecutorService` com um pool limitado depois de dominar o básico. |
| **Incorrect HTML parsing** | O stub `HTMLDocument` é simplista; páginas complexas falham. | Substitua-o por Jsoup: `Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

---

## Expandindo o Exemplo

Agora que você sabe **how to start thread**, pode querer:

- **Parse different files** passando o nome do arquivo para o `Runnable` (use um construtor ou uma lambda que capture a variável).
- **Collect results** com um `ConcurrentLinkedQueue<Integer>` ao invés de apenas imprimir.
- **Leverage a thread pool** (`Executors.newFixedThreadPool(4)`) para melhor escalabilidade.
- **Swap the parser** por Jsoup, HtmlUnit, ou qualquer biblioteca que atenda às necessidades do seu projeto.

Todas essas etapas ainda dependem da ideia central que abordamos: definir uma tarefa reutilizável, entregá‑la a uma ou várias threads e observar qual thread está realizando o trabalho através de **print thread name**.

---

## Conclusão

Cobremos **how to start thread** em Java, demonstramos **how to use runnable** para trabalho reutilizável, mostramos como **start multiple threads**, e ilustramos uma maneira simples de **parse HTML with Java** enquanto **print thread name** para cada worker. O trecho de código completo acima está pronto para ser executado, e os conceitos escalam para aplicações mais complexas e de nível produção.

Sinta‑se à vontade para experimentar: altere o caminho do arquivo, aumente o número de workers ou conecte um parser HTML real. Os fundamentos permanecem os mesmos, e agora você tem uma base sólida para qualquer projeto Java multithread.

Tem perguntas sobre segurança de threads, executor services ou bibliotecas de parsing HTML? Deixe um comentário abaixo, e feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [Como editar HTML usando Aspose.HTML para Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Como converter HTML para PDF Java – Usando Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}