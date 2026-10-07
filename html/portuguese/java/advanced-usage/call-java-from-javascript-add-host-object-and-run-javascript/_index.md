---
category: general
date: 2026-03-14
description: Aprenda como chamar Java a partir de JavaScript usando Aspose.HTML. Este
  guia mostra como adicionar um objeto host, executar JavaScript em Java e registrar
  a partir de JavaScript.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: pt
og_description: Chame Java a partir de JavaScript usando Aspose.HTML. Adicione objeto
  host, execute JavaScript em Java e registre logs do JavaScript em um único tutorial.
og_title: Chame Java a partir de JavaScript – Guia Completo com Objeto Host
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: Chamar Java a partir de JavaScript – Adicionar objeto host e executar JavaScript
  em Java
url: /pt/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chamar Java a partir de JavaScript – Adicionar Objeto Host e Executar JavaScript em Java

Já precisou **chamar Java a partir de JavaScript** dentro de uma aplicação Java? Talvez você esteja construindo um motor de relatórios HTML dinâmico ou simplesmente queira expor um logger Java para um script que você controla. Neste tutorial você verá exatamente como adicionar um objeto host, executar JavaScript em Java e até **registrar a partir de JavaScript** de volta para a JVM — tudo com Aspose.HTML.

Percorreremos um exemplo completo e executável que cria um documento HTML vazio, injeta uma classe Java `Logger` como objeto host, executa um pequeno script e imprime o resultado no console. Nenhum navegador externo necessário, sem “magia” — apenas código Java puro que você pode copiar‑colar e executar hoje.

## Pré‑requisitos

- Java 17 (ou qualquer JDK recente) instalado e configurado.  
- Biblioteca Aspose.HTML for Java (versão 23.10 ou mais recente). Você pode obtê‑la no Maven Central ou no site da Aspose.  
- Um IDE simples ou editor de texto; o exemplo funciona também via linha de comando.

> **Dica:** Se você usa Maven, adicione a seguinte dependência ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Ou, para Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Agora que temos o básico pronto, vamos mergulhar na solução passo a passo.

## Etapa 1: Criar um Projeto Java Minimalista

Primeiro, crie uma nova classe Java chamada `JsHostObjectDemo`. A classe conterá nosso método `main` e a definição do objeto host. Manter tudo em um único arquivo torna o tutorial autocontido e fácil de copiar.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### Por que um `HTMLDocument`?

A classe `HTMLDocument` do Aspose.HTML cria um ambiente de script completo e compatível com HTML‑5. Mesmo que nunca carreguemos nenhuma marcação, o objeto `window` do documento nos dá acesso ao motor JavaScript, onde acontece a mágica de **executar JavaScript em Java**.

## Etapa 2: Adicionar o Objeto Host – “javaLogger”

A linha

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

faz o trabalho pesado para o requisito de **adicionar objeto host**. Ao registrar a instância `Logger` sob o nome `"javaLogger"`, qualquer script avaliado neste documento pode chamar `javaLogger.log(...)`. Esse é o cerne do conceito de **objeto host javascript**: uma ponte que permite ao JavaScript alcançar a JVM.

### Armadilhas Comuns

- **Colisões de nomes** – Se já existir uma variável global chamada `javaLogger` no seu script, o objeto host será sobrescrito. Escolha um nome único.  
- **Segurança de threads** – O objeto host é compartilhado entre execuções de script no mesmo documento. Se você pretende executar scripts simultaneamente, torne a classe host thread‑safe (por exemplo, usando `synchronized` ou primitivas de `java.util.concurrent`).

## Etapa 3: Escrever e Executar JavaScript

O script que passamos para `eval` é deliberadamente pequeno:

```javascript
javaLogger.log('Hello from JavaScript!');
```

Quando `document.getWindow().eval(script)` é executado, o motor procura `javaLogger` em seu escopo global, encontra o objeto Java que adicionamos e invoca seu método `log` com a string fornecida.

### Saída Esperada

Executar o método `main` imprime a seguinte linha no console:

```
[JS] Hello from JavaScript!
```

Essa pequena linha prova que conseguimos **chamar java a partir de javascript**, e o **log a partir de javascript** aparece exatamente onde uma mensagem normal de `System.out` apareceria.

## Etapa 4: Expandindo o Host – Mais Que Apenas Logging

Se precisar expor funcionalidade adicional (por exemplo, acesso a arquivos, consultas a banco de dados), basta adicionar mais métodos à classe `Logger` — ou criar uma nova classe host. Aqui vai um exemplo rápido que também devolve um valor:

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

Agora o console mostra:

```
[JS] 3+4=7
```

Isso demonstra a flexibilidade do padrão de **objeto host javascript**: você pode expor qualquer API Java que precisar, contanto que os tipos de dados sejam conversíveis entre Java e JavaScript (primitivos, strings, arrays, etc.).

## Etapa 5: Liberar Recursos

Quando terminar de usar o ambiente de script, descarte o `HTMLDocument` para liberar recursos nativos:

```java
document.dispose(); // Important for long‑running applications
```

Ignorar a liberação pode causar vazamentos de memória, especialmente se você criar muitos documentos dentro de um loop.

## Exemplo Completo Funcional

Abaixo está o arquivo‑fonte completo que você pode compilar e executar imediatamente. Salve como `JsHostObjectDemo.java`, garanta que o JAR do Aspose.HTML esteja no seu classpath e execute `java JsHostObjectDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

Executar este programa produz:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

Esse é todo o fluxo de **chamar java a partir de javascript** em poucas linhas.

## Perguntas Frequentes

### Isso funciona no Android?

Aspose.HTML é uma biblioteca pura‑Java, então roda em qualquer JVM, inclusive no Dalvik/ART do Android. Basta incluir o JAR e você terá as mesmas capacidades de objeto host.

### E se eu precisar passar objetos complexos?

Você pode expor POJOs (plain old Java objects) que contenham campos, getters e setters. O motor os mapeará automaticamente para objetos JavaScript. Para coleções, use `java.util.List` ou arrays — ambos são conversíveis.

### Como funciona o tratamento de erros?

Se o script lançar um erro JavaScript, `eval` propagará uma `ScriptException`. Envolva a chamada em um bloco try‑catch para registrar ou recuperar:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### Posso executar vários scripts sequencialmente?

Com certeza. A mesma instância de `HTMLDocument` mantém seu escopo global, então você pode chamar `eval` repetidamente. Apenas fique atento a possíveis colisões de nomes entre scripts.

## Boas Práticas & Dicas

- **Nomeie seus objetos host de forma clara** — `javaLogger`, `javaUtils`, etc. — para evitar confusão.  
- **Mantenha os métodos do host pequenos e sem efeitos colaterais** sempre que possível; isso facilita a depuração.  
- **Descarte o documento** assim que terminar; isso libera a memória nativa que o Aspose.HTML aloca.  
- **Valide entradas** vindas do JavaScript, especialmente se os scripts vierem de fontes não confiáveis. Trate‑as como qualquer dado externo.

## Conclusão

Agora você tem um exemplo sólido, de ponta a ponta, de como **chamar java a partir de javascript** ao **adicionar um objeto host**, **executar JavaScript em Java** e **registrar a partir de JavaScript** usando Aspose.HTML. O padrão é poderoso: qualquer serviço Java pode ser exposto a scripts, transformando sua aplicação Java em uma plataforma de script leve.

A seguir, você pode explorar:

- Injetar uma página HTML completa e manipular o DOM a partir de JavaScript.  
- Usar o objeto host para transmitir dados de volta ao lado Java (por exemplo, serialização JSON).  
- Integrar com outros motores de script como Nashorn ou GraalVM para suporte a linguagens adicionais.

Experimente, ajuste as classes `Logger` ou `Utils` e veja até onde você pode levar o conceito de **objeto host javascript** em seus próprios projetos.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}