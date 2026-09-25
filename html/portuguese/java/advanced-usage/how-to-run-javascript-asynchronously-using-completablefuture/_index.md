---
category: general
date: 2026-02-16
description: Aprenda como executar JavaScript em Java com CompletableFuture, atrasar
  JS e avaliar código assíncrono. Guia completo passo a passo para avaliação assíncrona
  de JavaScript.
draft: false
keywords:
- how to run javascript
- how to use completablefuture
- how to delay js
- how to evaluate async
- evaluate javascript asynchronously
language: pt
og_description: Domine como executar JavaScript a partir do Java, atrasar JS e avaliar
  código assíncrono com CompletableFuture neste tutorial completo.
og_title: Como Executar JavaScript Assincronamente Usando CompletableFuture
tags:
- javascript
- java
- asynchronous
- completablefuture
title: Como Executar JavaScript Assincronamente Usando CompletableFuture
url: /pt/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Executar JavaScript Assincronamente Usando CompletableFuture

Já se perguntou **como executar JavaScript** dentro de uma aplicação Java sem bloquear a thread principal? Talvez você precise chamar um pequeno script que busca dados, mas não quer que sua UI congele. A boa notícia é que bibliotecas Java modernas permitem avaliar JavaScript **assincronamente**, e você pode até introduzir atrasos como faria em um navegador. Neste guia mostraremos um exemplo completo e executável que usa o `ScriptEngine` do Aspose HTML junto com `CompletableFuture` para **como executar javascript** e obter o resultado de volta em Java.

Também abordaremos **como usar CompletableFuture**, **como atrasar JS**, e **como avaliar código async** para que você possa **avaliar JavaScript assincronamente** em qualquer projeto Java. Ao final, você terá um modelo sólido que pode copiar‑colar, ajustar e incorporar em sistemas maiores.

---

## O Que Você Vai Aprender

- Configurar um `ScriptEngine` Java que execute JavaScript ES2022 moderno.  
- Escrever uma função `async` que inclua um atraso (`como atrasar js`).  
- Chamar `evaluateAsync` e receber um `CompletableFuture` (`como usar completablefuture`).  
- Recuperar o resultado quando a promessa JavaScript for resolvida (`como avaliar async`).  
- Dicas para tratamento de erros, gerenciamento de threads e extensão do padrão.

Nenhuma ferramenta de build externa é necessária além do JAR do Aspose HTML for Java, que pode ser adicionado ao seu classpath. Vamos mergulhar.

---

## Etapa 1: Como Executar JavaScript – Inicializar o Motor de Scripting

Primeiro, a biblioteca Aspose HTML fornece a classe `ScriptEngine` que pode executar código JavaScript. Pense nela como um pequeno motor Chromium rodando dentro da sua JVM.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Por que isso importa:** Ao instanciar `ScriptEngine` obtemos um ambiente sandbox onde JavaScript moderno (incluindo `async/await`) funciona imediatamente. Não é preciso iniciar um processo Node externo.

---

## Etapa 2: Como Atrasar JS – Escrever uma Função Async com Timer Baseado em Promise

O `setTimeout` do JavaScript é a forma clássica de pausar a execução. No código moderno o encapsulamos em uma `Promise` para poder usar `await`. É exatamente isso que faremos na string do script.

```java
        // ES2022 async function that resolves after a short delay
        String asyncScript = """
            async function fetchMessage() {
                const delay = ms => new Promise(r => setTimeout(r, ms));
                await delay(500); // 500 ms pause
                return "Hello from async JS!";
            }
            fetchMessage(); // Return the promise to Java
            """;
```

> **Como atrasar js:** O helper `delay` cria uma promise que é concluída após `ms` milissegundos. Ao fazer `await` nela, a função pausa sem bloquear a thread Java.

---

## Etapa 3: Como Avaliar Async – Executar o Script e Obter um CompletableFuture

Em vez do método síncrono `evaluate`, chamamos `evaluateAsync`. Ele retorna imediatamente um `CompletableFuture<Object>` que será completado quando a promise JavaScript for resolvida.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **Como avaliar async:** `evaluateAsync` faz a ponte entre o loop de eventos JavaScript e o `CompletableFuture` de Java. Este é o núcleo de **avaliar javascript assincronamente**.

---

## Etapa 4: Como Usar CompletableFuture – Anexar um Callback e Bloquear para Demonstração

Agora anexamos um callback com `thenAccept` para imprimir o resultado, e bloqueamos a thread principal apenas o tempo suficiente para a demonstração terminar.

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **Por que chamamos `get()`:** Em uma aplicação real você provavelmente continuará o processamento em outro lugar. Aqui bloqueamos para manter o exemplo autocontido.

---

## Visão Geral Visual

![Diagrama mostrando como executar JavaScript assincronamente com CompletableFuture](https://example.com/diagram.png "Como Executar JavaScript – Fluxo Assíncrono")

*Texto alternativo:* **Diagrama mostrando como executar JavaScript assincronamente com CompletableFuture** – a imagem ilustra o fluxo do Java para o motor de script, o atraso async e a conclusão do CompletableFuture.

---

## Armadilhas Comuns & Boas Práticas (Como Avaliar Async com Segurança)

| Armadilha | O Que Acontece | Solução |
|-----------|----------------|---------|
| Esquecer de retornar a promise | `evaluateAsync` resolve imediatamente com `undefined` | Garanta que a última linha do script seja a promise (`fetchMessage();`) |
| Usar `Thread.sleep` bloqueante em JS | Bloqueia o loop de eventos do motor, anula o async | Use o padrão de promise `delay` (conforme mostrado) |
| Ignorar exceções | O Future completa excepcionalmente, mas você nunca vê | Anexe `.exceptionally(e -> { e.printStackTrace(); return null; })` |
| Não encerrar o motor | Vazamento de recursos em aplicações de longa duração | Chame `scriptEngine.dispose()` quando terminar |

---

## Extendendo o Padrão (Como Usar CompletableFuture em Projetos Reais)

Você pode encadear múltiplas chamadas JavaScript async, combiná‑las com outros futures, ou até executá‑las em um `Executor` customizado. Aqui vai um esboço rápido:

```java
ExecutorService jsPool = Executors.newFixedThreadPool(4);
CompletableFuture<Object> future = scriptEngine.evaluateAsync(asyncScript, jsPool)
    .thenApply(result -> {
        // Post‑process the JS string result
        return ((String) result).toUpperCase();
    })
    .exceptionally(ex -> {
        System.err.println("JS error: " + ex);
        return "fallback";
    });
```

> **Como usar CompletableFuture:** Ao passar um `Executor` você controla o pool de threads, mantendo a UI responsiva e evitando starvation de threads.

---

## Saída Esperada

Execute a classe `JsAsyncDemo` e você deverá ver:

```
JS result: Hello from async JS!
```

A pausa de 500 ms não é visível no console, mas você pode adicionar timestamps para verificar o atraso, se desejar.

---

## Recapitulação – Como Executar JavaScript com CompletableFuture

Começamos **como executar javascript** dentro do Java, escrevemos uma função `async` que **como atrasar js**, executamos com `evaluateAsync` (**como avaliar async**) e capturamos o resultado usando um **como usar completablefuture**. Todo o fluxo demonstra **avaliar javascript assincronamente** em um padrão limpo e reutilizável.

---

## O Que Vem a Seguir?

- **Integrar com clientes HTTP:** Buscar dados de um endpoint REST dentro do JS async e retornar ao Java.  
- **Usar múltiplos scripts:** Encadear várias chamadas `evaluateAsync` para pipelines complexas.  
- **Trocar de motor:** O mesmo padrão funciona com Nashorn, GraalVM ou outros runtimes JavaScript—basta substituir `ScriptEngine`.

Sinta‑se à vontade para experimentar atrasos maiores, scripts que lançam erros, ou até módulos WebAssembly. O céu é o limite quando você combina os primitivos de concorrência do Java com JavaScript moderno.

---

### Tem Perguntas?

Se algo não ficou claro—talvez você esteja se perguntando como lidar com uma promise rejeitada ou como passar variáveis do Java para o script—deixe um comentário abaixo. Boa codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}