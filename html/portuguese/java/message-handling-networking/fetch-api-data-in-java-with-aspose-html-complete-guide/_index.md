---
category: general
date: 2026-05-28
description: Buscar dados da API em Java usando Aspose.HTML – aprenda como executar
  JavaScript assíncrono, rodar script assíncrono e definir atributo DOM a partir do
  JSON recuperado.
draft: false
keywords:
- fetch api data
- execute async javascript
- run async script
- set dom attribute
- how to run async
language: pt
og_description: Buscar dados da API em Java com Aspose.HTML. Este tutorial mostra
  como executar JavaScript assíncrono, rodar script assíncrono e definir atributos
  DOM a partir dos resultados da API.
og_title: Buscar dados da API em Java – Guia passo a passo do Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: fetch api data in Java using Aspose.HTML – learn how to execute async
    javascript, run async script, and set dom attribute from fetched JSON.
  headline: fetch api data in Java with Aspose.HTML - Complete Guide
  type: TechArticle
- description: fetch api data in Java using Aspose.HTML – learn how to execute async
    javascript, run async script, and set dom attribute from fetched JSON.
  name: fetch api data in Java with Aspose.HTML - Complete Guide
  steps:
  - name: Expected Output
    text: '``` GitHub stars: 84327 ```'
  - name: What if the fetch call fails?
    text: 'The script will throw a JavaScript exception, which propagates to `ScriptEngine.evaluate`.
      You can catch it in Java:'
  - name: Can I fetch from a private API that requires authentication?
    text: 'Sure—just add the appropriate headers in the script:'
  - name: Does this work on older Java versions?
    text: Aspose.HTML ships with its own JavaScript engine, so you don’t need Nashorn
      or GraalVM. However, the `try‑with‑resources` syntax requires Java 7+. For Java
      6 you’d have to close the document manually.
  type: HowTo
tags:
- Java
- Aspose.HTML
- Async JavaScript
title: Buscar dados da API em Java com Aspose.HTML - Guia Completo
url: /pt/java/message-handling-networking/fetch-api-data-in-java-with-aspose-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fetch api data em Java com Aspose.HTML – Guia Completo

Já se perguntou como **fetch api data** em Java sem sair do conforto do seu IDE? Você não está sozinho. Muitos desenvolvedores encontram um obstáculo quando precisam chamar um serviço remoto a partir de uma página HTML renderizada pelo Aspose.HTML e então trazer o resultado de volta para o Java.  

Neste tutorial, percorreremos um exemplo prático que **executa async javascript**, roda um **async script** e, finalmente, **define um atributo DOM** com o valor obtido. Ao final, você saberá exatamente *como executar async* de forma segura e recuperar os dados de que precisa.

## O que você vai construir

Criaremos um pequeno aplicativo console Java que:

1. Carrega um arquivo HTML contendo uma função async.  
2. Executa um script que usa a **fetch API** para chamar o endpoint público do GitHub.  
3. Aguarda a promessa ser resolvida (até 10 segundos).  
4. Armazena a contagem de estrelas em um atributo personalizado `data-stars` no elemento `<body>`.  
5. Lê esse atributo de volta no Java e o imprime.

Sem bibliotecas externas de cliente HTTP, sem código extra de threading — apenas o Aspose.HTML fazendo o trabalho pesado.

## Pré-requisitos

- **Java 17** ou superior (o código compila em versões anteriores, mas 17 é o LTS atual).  
- Biblioteca **Aspose.HTML for Java** (versão 23.9 ou posterior).  
- Um arquivo HTML simples (`async-page.html`) colocado em algum lugar no seu disco.  
- Uma conexão à internet (a chamada fetch atinge `https://api.github.com`).  

Se você já tem um projeto Maven, adicione a dependência do Aspose.HTML:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

Agora, vamos mergulhar no código.

## Etapa 1: Prepare a página HTML

Primeiro, crie um arquivo HTML mínimo que hospedará a função async. Você não precisa de nenhuma marcação sofisticada — apenas uma tag `<body>`.

```html
<!-- async-page.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Async Demo</title>
</head>
<body>
    <!-- The script we’ll inject later will populate this attribute -->
</body>
</html>
```

Salve este arquivo em algum local acessível, por exemplo, `C:/temp/async-page.html`. O caminho será usado no código Java.

![exemplo de fetch api data](https://example.com/fetch-api-data.png "exemplo de fetch api data")

*Texto alternativo da imagem: exemplo de fetch api data mostrando a saída de console das estrelas do GitHub.*

## Etapa 2: Carregue o documento HTML no Java

Com o arquivo HTML pronto, abrimos ele usando o `HTMLDocument` do Aspose.HTML. O bloco `try‑with‑resources` garante que o documento seja descartado corretamente.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsExample {
    public static void main(String[] args) throws Exception {

        // Load the HTML page that contains an async function
        try (HTMLDocument doc = new HTMLDocument("C:/temp/async-page.html")) {
            // The rest of the steps go here...
        }
    }
}
```

Por que usar `HTMLDocument`? Ele nos fornece um DOM completo, um motor JavaScript embutido e uma maneira conveniente de interagir com a página a partir do Java — tudo sem precisar iniciar um navegador.

## Etapa 3: Escreva o script async

Agora criamos um trecho de JavaScript que **busca dados da API**, aguarda a promessa e então **define um atributo DOM**. Observe o uso de `async/await` — o mesmo padrão que você escreveria em um navegador.

```java
String script =
    "async function run() {" +
    "  const data = await fetch('https://api.github.com').then(r => r.json());" +
    "  document.body.setAttribute('data-stars', data.stargazers_count);" +
    "}" +
    "run();";
```

Alguns pontos a observar:

- A função `run` é declarada `async`, portanto podemos `await` a chamada `fetch`.  
- Após o JSON ser analisado, armazenamos `data.stargazers_count` em um atributo personalizado `data-stars`.  
- Por fim, invocamos `run()` imediatamente.  

Este pequeno script faz tudo que precisamos para **executar async script** e capturar o resultado.

## Etapa 4: Execute o script e aguarde

O `ScriptEngine` do Aspose.HTML pode avaliar JavaScript com um tempo limite. Ao passar `10000` informamos ao motor para aguardar até **10 segundos** para que a operação async termine.

```java
// Execute the script and wait (up to 10 seconds) for the async operation to finish
ScriptEngine engine = doc.getScriptEngine();
engine.evaluate(script, 10000);   // timeout in milliseconds
```

Se a requisição demorar mais que o tempo limite, uma `ScriptException` é lançada — perfeito para lidar com condições de rede instáveis. Em produção, você provavelmente envolveria isso em um try‑catch e tentaria novamente conforme necessário.

## Etapa 5: Recupere o atributo no Java

Depois que o script termina, o atributo `data-stars` agora faz parte do DOM. Traga‑o de volta ao Java com uma chamada simples:

```java
// Retrieve the value set by the script from the document
String stars = doc.getBody().getAttribute("data-stars");
System.out.println("GitHub stars: " + stars);
```

Essa linha imprime algo como `GitHub stars: 12345`. O número exato muda diariamente, mas o padrão permanece o mesmo.

## Exemplo completo em funcionamento

Juntando todas as peças, aqui está o programa completo, pronto‑para‑executar:

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML page that contains an async function
        try (HTMLDocument doc = new HTMLDocument("C:/temp/async-page.html")) {

            // Step 2: Define a script that calls the async function and stores the result in a DOM attribute
            String script =
                "async function run() {" +
                "  const data = await fetch('https://api.github.com').then(r => r.json());" +
                "  document.body.setAttribute('data-stars', data.stargazers_count);" +
                "}" +
                "run();";

            // Step 3: Execute the script and wait (up to 10 seconds) for the async operation to finish
            ScriptEngine engine = doc.getScriptEngine();
            engine.evaluate(script, 10000);

            // Step 4: Retrieve the value set by the script from the document
            String stars = doc.getBody().getAttribute("data-stars");
            System.out.println("GitHub stars: " + stars);
        }
    }
}
```

### Saída esperada

```
GitHub stars: 84327
```

(Seu número será diferente; o importante é que o valor seja uma **string** representando a contagem de estrelas.)

## Perguntas comuns e casos de borda

### E se a chamada fetch falhar?

O script lançará uma exceção JavaScript, que propaga para `ScriptEngine.evaluate`. Você pode capturá‑la no Java:

```java
try {
    engine.evaluate(script, 10000);
} catch (ScriptException e) {
    System.err.println("Failed to fetch data: " + e.getMessage());
}
```

### Posso buscar de uma API privada que requer autenticação?

Claro — basta adicionar os cabeçalhos apropriados no script:

```javascript
await fetch('https://api.example.com/secure', {
    headers: { 'Authorization': 'Bearer YOUR_TOKEN' }
}).then(r => r.json());
```

Lembre‑se de manter segredos fora do controle de versão.

### Isso funciona em versões mais antigas do Java?

O Aspose.HTML vem com seu próprio motor JavaScript, portanto você não precisa do Nashorn ou GraalVM. No entanto, a sintaxe `try‑with‑resources` requer Java 7+. Para Java 6, seria necessário fechar o documento manualmente.

## Dicas profissionais

- **Reutilize o ScriptEngine**: Se precisar executar muitos scripts async, mantenha uma única instância do motor viva — gera menos sobrecarga.  
- **Aumente o timeout** para APIs mais lentas, mas não defina como `Integer.MAX_VALUE`; ainda assim você quer uma rede de segurança.  
- **Valide o atributo** antes de usá‑lo. O atributo DOM pode ser `null` se o script nunca foi executado.  
- **Registre o JSON bruto** durante o desenvolvimento; isso ajuda quando a API muda de estrutura.

## Próximos passos

Agora que você sabe como **fetch api data**, pode estender o padrão:

- **Parsear JSON mais complexo** e injetar múltiplos atributos.  
- **Criar tabelas** dentro da página HTML com base nos dados obtidos.  
- **Combinar com Aspose.PDF** para gerar um PDF que contenha resultados de API ao vivo.  

Cada um desses se baseia nas mesmas ideias centrais: **executar async javascript**, **run async script** e **set dom attribute** a partir do resultado. Sinta‑se à vontade para experimentar — há muito poder oculto no motor de script do Aspose.HTML.

*Feliz codificação! Se você encontrar algum problema, deixe um comentário abaixo e nós iremos solucionar juntos.*

## Tutoriais relacionados

- [Como executar JavaScript em Java – Guia completo](/html/english/java/advanced-usage/how-to-run-javascript-in-java-complete-guide/)
- [Adicionar elemento ao body com Aspose.HTML para Java usando um DOM Mutation Observer](/html/english/java/advanced-usage/dom-mutation-observer-observing-node-additions/)
- [Como definir timeout – Gerenciar timeout de rede no Aspose.HTML para Java](/html/english/java/message-handling-networking/network-timeout/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}