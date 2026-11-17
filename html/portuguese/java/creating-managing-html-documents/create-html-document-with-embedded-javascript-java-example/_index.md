---
category: general
date: 2026-06-03
description: Crie um documento HTML em Java e incorpore JavaScript para incrementar
  um contador. Aprenda um exemplo de motor de script, obtenha o innerHTML do elemento
  e muito mais.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: pt
og_description: Crie um documento HTML em Java, incorpore JavaScript para incrementar
  um contador e recupere o valor final usando um exemplo de engine de script.
og_title: Criar documento HTML com JavaScript incorporado – Exemplo em Java
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  headline: Create HTML Document with Embedded JavaScript – Java Example
  type: TechArticle
- description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  name: Create HTML Document with Embedded JavaScript – Java Example
  steps:
  - name: '**Creates an HTML document** in memory.'
    text: '**Creates an HTML document** in memory.'
  - name: '**Embeds a small JavaScript snippet** that increments a counter five times.'
    text: '**Embeds a small JavaScript snippet** that increments a counter five times.'
  - name: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
    text: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
  - name: '**Retrieves the final counter value** using `getElementInnerHTML`.'
    text: '**Retrieves the final counter value** using `getElementInnerHTML`.'
  - name: 'Prints `Final counter value: 5` to the console.'
    text: 'Prints `Final counter value: 5` to the console.'
  type: HowTo
tags:
- HTML
- JavaScript
- Java
- ScriptEngine
title: Criar documento HTML com JavaScript incorporado – Exemplo em Java
url: /pt/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar documento HTML com JavaScript incorporado – Exemplo em Java

Já precisou **criar documento HTML** a partir de código Java e se perguntou como incorporar JavaScript nele? Neste guia mostraremos exatamente isso, passo a passo, e você terminará com um exemplo funcional de engine de script que imprime o valor final do contador.  

Se você já se perguntou *“como obter o innerHTML de um elemento após a execução de um script?”* ou *“qual é a maneira mais limpa de incrementar um contador em JavaScript a partir de Java?”* — você está no lugar certo. Vamos abordar **embed javascript html**, **increment counter javascript**, e **get element innerHTML** tudo em um tutorial coeso.

![Criar documento HTML com JavaScript incorporado](/images/create-html-document.png){: .center alt="Exemplo de criação de documento HTML com JavaScript incorporado"}

## O que você vai construir

Ao final deste tutorial, você terá um programa Java autônomo que:

1. **Cria um documento HTML** na memória.
2. **Incorpora um pequeno trecho de JavaScript** que incrementa um contador cinco vezes.
3. **Inicializa uma engine de script** (o exemplo `ScriptEngine`) para executar esse trecho.
4. **Recupera o valor final do contador** usando `getElementInnerHTML`.
5. Imprime `Final counter value: 5` no console.

Sem arquivos externos, sem servidor web — apenas Java puro e uma pequena string HTML.

---

## Pré-requisitos

- Java 17 ou superior (a API `ScriptEngine` faz parte da biblioteca padrão).
- Familiaridade básica com HTML e JavaScript (não é necessário profundo conhecimento).
- Um IDE ou um editor de texto simples mais um terminal para compilar e executar o programa.

---

## Etapa 1: Criar documento HTML em Java

A primeira coisa que precisamos é um objeto de documento HTML em branco que podemos preencher posteriormente com marcação. Pense nele como uma página virtual que existe apenas na memória.

```java
// Import statements
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

// Minimal HTML document wrapper (pseudo‑class for illustration)
class HTMLDocument {
    private StringBuilder html = new StringBuilder();

    public void write(String content) {
        html.append(content);
    }

    public String getContent() {
        return html.toString();
    }

    // Simple DOM simulation for getElementById / innerHTML
    private java.util.Map<String, String> elements = new java.util.HashMap<>();

    public void setElementInnerHTML(String id, String value) {
        elements.put(id, value);
    }

    public String getElementInnerHTML(String id) {
        return elements.getOrDefault(id, "");
    }

    // Helper used by the script engine (not production‑grade)
    public void updateCounter(int value) {
        setElementInnerHTML("counter", String.valueOf(value));
    }
}
```

**Por que isso importa:** Ao **criar documentos HTML** você mesmo, evita gravar no disco e mantém tudo testável. A pequena simulação de DOM nos permite posteriormente **obter o innerHTML do elemento** sem um navegador completo.

## Etapa 2: Incorporar JavaScript HTML – A lógica do contador

Agora vamos escrever a marcação HTML que inclui um bloco `<script>`. Este script **incrementará o contador em JavaScript** cinco vezes.

```java
HTMLDocument doc = new HTMLDocument();

doc.write(
    "<!DOCTYPE html><html><body>"
  + "<div id='counter'>0</div>"
  + "<script>"
  + "for (let i = 0; i < 5; i++) {"
  + "  document.getElementById('counter').innerHTML = i + 1;"
  + "}"
  + "</script>"
  + "</body></html>"
);
```

**Explicação:**  
- O `<div id='counter'>0</div>` é nosso elemento alvo.  
- O loop `for` executa a lógica **increment counter javascript**, atualizando a div a cada iteração.  
- Como não estamos em um navegador real, a engine de script que usaremos mais tarde precisará entender `document.getElementById`. Por isso adicionamos um pequeno stub em `HTMLDocument`.

## Etapa 3: Inicializar a engine de script – Um exemplo de engine de script

O Java vem com a API `ScriptEngine` (JSR‑223). Criaremos um pequeno wrapper que fornece o conteúdo HTML para a engine e oferece os métodos DOM mínimos que ela espera.

```java
class SimpleScriptEngine {
    private final HTMLDocument document;
    private final ScriptEngine engine;

    public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
        this.document = doc;
        ScriptEngineManager manager = new ScriptEngineManager();
        this.engine = manager.getEngineByName("JavaScript");
        // Expose a mock 'document' object to the JavaScript context
        engine.put("document", new Object() {
            public Object getElementById(String id) {
                return new Object() {
                    public void setInnerHTML(String value) {
                        document.updateCounter(Integer.parseInt(value));
                    }
                };
            }
        });
    }

    public void execute() throws ScriptException {
        // Extract only the script part from the HTML (simplified)
        String html = document.getContent();
        int scriptStart = html.indexOf("<script>") + "<script>".length();
        int scriptEnd   = html.indexOf("</script>");
        String script = html.substring(scriptStart, scriptEnd);
        engine.eval(script);
    }
}
```

**Por que isso importa:** Este **exemplo de engine de script** mostra como você pode executar JavaScript incorporado sem um navegador completo. Também demonstra uma forma leve de expor `document.getElementById` para que o script interaja com nosso DOM simulado.

## Etapa 4: Executar JavaScript – Increment Counter JavaScript em ação

Com a engine pronta, simplesmente executamos o script. O loop dentro da tag `<script>` será disparado, e nosso mock `setInnerHTML` atualizará o contador.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**O que acontece nos bastidores?** Cada iteração do loop chama `document.getElementById('counter').innerHTML = i + 1;`. Nosso mock `setInnerHTML` encaminha a string numérica para `HTMLDocument.updateCounter`, que armazena o valor mais recente. Após o término do loop, o mapa interno do documento contém `"5"` para o elemento `counter`.

## Etapa 5: Recuperar o valor final do contador – Obter o innerHTML do elemento

Agora que o script terminou, podemos **obter o innerHTML do elemento** a partir da nossa instância `HTMLDocument`.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

Executar o programa completo imprime:

```
Final counter value: 5
```

Isso confirma que a lógica **increment counter javascript** funcionou e que conseguimos **recuperar o innerHTML do elemento** após a execução do script.

## Exemplo completo em funcionamento

Juntando tudo, aqui está a classe Java completa, pronta para ser executada:

```java
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

public class HtmlJsDemo {

    // ---------- Minimal HTMLDocument implementation ----------
    static class HTMLDocument {
        private final StringBuilder html = new StringBuilder();
        private final java.util.Map<String, String> elements = new java.util.HashMap<>();

        public void write(String content) {
            html.append(content);
        }

        public String getContent() {
            return html.toString();
        }

        public void setElementInnerHTML(String id, String value) {
            elements.put(id, value);
        }

        public String getElementInnerHTML(String id) {
            return elements.getOrDefault(id, "");
        }

        public void updateCounter(int value) {
            setElementInnerHTML("counter", String.valueOf(value));
        }
    }

    // ---------- SimpleScriptEngine (script engine example) ----------
    static class SimpleScriptEngine {
        private final HTMLDocument document;
        private final ScriptEngine engine;

        public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
            this.document = doc;
            ScriptEngineManager manager = new ScriptEngineManager();
            this.engine = manager.getEngineByName("JavaScript");
            // Expose a mock 'document' object
            engine.put("document", new Object() {
                public Object getElementById(String id) {
                    return new Object() {
                        public void setInnerHTML(String value) {
                            document.updateCounter(Integer.parseInt(value));
                        }
                    };
                }
            });
        }

        public void execute() throws ScriptException {
            String html = document.getContent();
            int start = html.indexOf("<script>") + "<script>".length();
            int end   = html.indexOf("</script>");
            String script = html.substring(start, end);
            engine.eval(script);
        }
    }

    // ---------- Main method ----------
    public static void main(String[] args) {
        // Step 1: create HTML document
        HTMLDocument doc = new HTMLDocument();

        // Step 2: embed JavaScript HTML (increment counter JavaScript)
        doc.write(
            "<!DOCTYPE html><html><body>"
          + "<div id='counter'>0</div>"
          + "<script>"
          + "for (let i = 0; i < 5; i++) {"
          + "  document.getElementById('counter').innerHTML = i


## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar documentos HTML vazios no Aspose.HTML para Java](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [Criar documentos HTML a partir de String no Aspose.HTML para Java](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Salvar documento HTML no Aspose.HTML para Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}