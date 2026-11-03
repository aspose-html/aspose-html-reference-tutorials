---
category: general
date: 2026-10-14
description: Chame java a partir de javascript usando Aspose.HTML. Aprenda como add
  host object, execute javascript em java e log a partir de javascript em um tutorial
  conciso.
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: Chame java a partir de javascript usando Aspose.HTML. Este guia mostra
  como add host object, execute javascript em java e log a partir de javascript, tudo
  em poucas linhas de código.
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: Chamar java a partir de javascript – add host object e executar javascript
  em java
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Call java from javascript using Aspose.HTML. Learn how to add a host
    object, execute javascript in java, and log from javascript in a concise tutorial.
  headline: Call java from javascript – add host object and run javascript in java
  type: TechArticle
- questions:
  - answer: Yes. Aspose.HTML is a pure‑Java library, so it runs on any JVM, including
      Android’s ART runtime.
    question: Does this work on Android?
  - answer: You can expose POJOs with getters and setters; the engine maps them to
      JavaScript objects automatically. Collections such as `java.util.List` or arrays
      are also convertible.
    question: What if I need to pass complex objects?
  - answer: If the script throws a JavaScript error, `eval` propagates a `ScriptException`.
      Wrap the call in a try‑catch block to log or recover.
    question: How does error handling work?
  - answer: Absolutely. The same `HTMLDocument` retains its global scope, so you can
      call `eval` repeatedly. Just manage variable names to avoid clashes.
    question: Can I run multiple scripts sequentially?
  - answer: Treat any external script as untrusted input. Validate parameters and
      consider sandboxing by exposing only the minimal required methods.
    question: Is the host object safe for untrusted scripts?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- scripting
- host object
title: Chamar java a partir de javascript – add host object e executar javascript
  em java
url: /pt/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chamar java a partir de javascript – adicionar objeto host e executar javascript em java

Já precisou **chamar java a partir de javascript** dentro de uma aplicação Java? Talvez você esteja construindo um mecanismo de relatórios HTML dinâmico ou simplesmente queira expor um logger Java para um script que você controla. Neste tutorial você verá exatamente como adicionar um objeto host, executar JavaScript em Java e até **registrar a partir de JavaScript** de volta para a JVM — tudo com Aspose.HTML.

Vamos percorrer um exemplo completo e executável que cria um documento HTML vazio, injeta uma classe Java `Logger` como objeto host, executa um pequeno script e imprime o resultado no console. Nenhum navegador externo necessário, sem “magia” — apenas código Java puro que você pode copiar‑colar e executar hoje.

## Respostas rápidas
- **Como adiciono um objeto host?** Registre uma instância Java com `document.getWindow().addHostObject("name", object)`.  
- **Posso executar JavaScript em Java?** Sim — use `document.getWindow().eval(yourScript)`.  
- **É possível registrar a partir de JavaScript?** Absolutamente; o objeto host pode expor qualquer método `void log(String)`.  
- **Qual versão do Aspose.HTML é necessária?** A versão 23.10 ou mais recente suporta a API completa de objeto host.  
- **Preciso de um navegador web?** Não — o Aspose.HTML fornece um motor embutido, então tudo roda sem interface gráfica.

## O que é chamar java a partir de javascript?
**Call java from javascript** é a técnica de expor objetos Java a um runtime JavaScript para que scripts possam invocar métodos Java diretamente. Aspose.HTML cria um motor JavaScript leve dentro de um processo Java, permitindo comunicação bidirecional fluida sem navegadores externos.

## Por que usar Aspose.HTML para executar javascript em java?
Aspose.HTML suporta **50+ formatos de entrada e saída** e pode avaliar JavaScript em um ambiente HTML5 totalmente compatível. Ele processa scripts em até 200 ms em média para códigos simples de uma linha, e faz isso sem carregar uma pilha completa de navegador, reduzindo o uso de memória em até 80 % comparado a abordagens baseadas em Selenium.

## Pré-requisitos

- Java 17 (ou qualquer JDK recente) instalado e configurado.  
- Biblioteca Aspose.HTML for Java (versão 23.10 ou mais recente). Você pode obtê-la no Maven Central ou no site da Aspose.  
- Um IDE simples ou editor de texto; o exemplo funciona também via linha de comando.

> **Dica profissional:** Se você usa Maven, adicione a seguinte dependência ao seu `pom.xml`:

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

Agora que organizamos o básico, vamos mergulhar na solução passo a passo.

## Como adicionar um objeto host e executar javascript em java?
`addHostObject` registra um objeto Java como uma variável global no contexto JavaScript. Carregue seu `HTMLDocument`, registre um logger Java sob o nome `"javaLogger"` usando `addHostObject` e, em seguida, avalie um pequeno script que chama `javaLogger.log`. Todo o fluxo requer apenas três chamadas de API e funciona em qualquer runtime Java 17.

### Etapa 1: criar um projeto java minimalista

Primeiro, configure uma nova classe Java chamada `JsHostObjectDemo`. A classe conterá nosso método `main` e a definição do objeto host. Manter tudo em um único arquivo torna o tutorial autocontido e fácil de copiar.

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
`HTMLDocument` representa um documento HTML em memória e fornece um motor JavaScript. A classe `HTMLDocument` inicia um ambiente de script totalmente compatível com HTML‑5. Mesmo que nunca carreguemos marcação, o objeto `window` do documento nos dá acesso ao motor JavaScript, onde acontece a magia de **executar javascript em java**. Além disso, você pode manipular o DOM, carregar recursos, ou avaliar scripts sem um navegador.

## Como adicionar o objeto host – “javaLogger”?
`Logger` é uma classe Java simples com um método `log(String)` que grava mensagens no console. Registre a instância `Logger` sob o nome `"javaLogger"` para que qualquer script avaliado neste documento possa chamar `javaLogger.log(...)`. Este é o núcleo do requisito de **adicionar objeto host** e disponibiliza o logger como variável global para o código JavaScript.

### Armadilhas comuns

- **Colisões de nomes** — Se você já tem uma variável global chamada `javaLogger` no seu script, o objeto host será sobrescrito. Escolha um nome único.  
- **Segurança de thread** — O objeto host é compartilhado entre execuções de script no mesmo documento. Se você planeja executar scripts simultaneamente, torne a classe host thread‑safe (por exemplo, use `synchronized` ou primitivas de `java.util.concurrent`).

## Como escrever e executar javascript em java?
`eval` executa uma string JavaScript no motor de script do documento e retorna qualquer resultado. Alimente um pequeno script em `eval`. O motor resolve `javaLogger` a partir do escopo global e invoca seu método `log` com a string fornecida. Você também pode retornar valores, tratar exceções e encadear múltiplas avaliações para interações mais complexas.

### Saída esperada

Executar o método `main` imprime a linha a seguir no console:

```
[JS] Hello from JavaScript!
```

## Como estender o host – mais do que apenas registro?
Um objeto host é qualquer instância Java exposta ao JavaScript via `addHostObject`. Expanda a funcionalidade adicionando métodos à classe `Logger` ou criando uma nova classe host. Abaixo está um exemplo rápido que também retorna um valor para o JavaScript. O objeto host pode expor tipos complexos, realizar I/O ou interagir com outros serviços. Ao retornar um valor, o script pode receber dados de volta, permitindo comunicação bidirecional entre Java e JavaScript.

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

## Como limpar recursos após executar scripts?
`dispose` libera recursos nativos mantidos pela instância `HTMLDocument`. Quando terminar com o ambiente de script, descarte o `HTMLDocument` para liberar recursos nativos. Não chamar `dispose()` pode causar vazamentos de memória, especialmente ao criar muitos documentos em loops ou serviços de longa duração. Sempre envolva o uso em um bloco try‑with‑resources ou garanta que `document.dispose()` seja chamado em um bloco finally.

```java
document.dispose(); // Important for long‑running applications
```

## Exemplo completo em funcionamento

A seguir está o arquivo fonte completo que você pode compilar e executar imediatamente. Salve como `JsHostObjectDemo.java`, assegure que o JAR do Aspose.HTML esteja no classpath e execute `java JsHostObjectDemo`.

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

## Perguntas frequentes

**P: Isso funciona no Android?**  
R: Sim. Aspose.HTML é uma biblioteca pura Java, portanto roda em qualquer JVM, incluindo o runtime ART do Android.

**P: E se eu precisar passar objetos complexos?**  
R: Você pode expor POJOs com getters e setters; o motor os mapeia automaticamente para objetos JavaScript. Coleções como `java.util.List` ou arrays também são convertíveis.

**P: Como funciona o tratamento de erros?**  
R: Se o script lançar um erro JavaScript, `eval` propaga uma `ScriptException`. Envolva a chamada em um bloco try‑catch para registrar ou recuperar.

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**P: Posso executar vários scripts sequencialmente?**  
R: Absolutamente. O mesmo `HTMLDocument` mantém seu escopo global, então você pode chamar `eval` repetidamente. Apenas gerencie os nomes de variáveis para evitar conflitos.

**P: O objeto host é seguro para scripts não confiáveis?**  
R: Trate qualquer script externo como entrada não confiável. Valide parâmetros e considere sandboxing expondo apenas os métodos mínimos necessários.

## Melhores práticas e dicas

- **Nomeie seus objetos host claramente** — `javaLogger`, `javaUtils`, etc. — para evitar confusão.  
- **Mantenha os métodos host pequenos e sem efeitos colaterais** quando possível; isso facilita a depuração.  
- **Libere o documento** assim que terminar; isso libera a memória nativa que o Aspose.HTML aloca.  
- **Valide as entradas** provenientes de JavaScript, especialmente se os scripts vierem de fontes não confiáveis. Trate-as como quaisquer dados externos.

## Conclusão

Agora você tem um exemplo sólido de ponta a ponta de como **chamar java a partir de javascript** ao **adicionar um objeto host**, **executar javascript em java** e **registrar a partir de javascript** usando Aspose.HTML. O padrão é poderoso: qualquer serviço Java pode ser exposto a scripts, transformando sua aplicação Java em uma plataforma de script leve.

Em seguida, você pode explorar:

- Injetar uma página HTML completa e manipular o DOM a partir de JavaScript.  
- Usar o objeto host para transmitir dados de volta ao lado Java (por exemplo, serialização JSON).  
- Integrar com outros motores de script como Nashorn ou GraalVM para suporte a mais linguagens.

Teste, ajuste as classes `Logger` ou `Utils` e veja até onde você pode levar o conceito de **objeto host javascript** em seus próprios projetos.

**Última atualização:** 2026-10-14  
**Testado com:** Aspose.HTML for Java 23.10  
**Autor:** Aspose






```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## Tutoriais relacionados

- [Habilitar Execução de Script em Java Guia Completo Aspose Html](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Executar Javascript em Java Guia Completo para Executar Js De](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [Como Isolar Javascript Guia Completo Aspose Html](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}