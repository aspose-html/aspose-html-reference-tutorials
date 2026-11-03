---
category: general
date: 2026-04-03
description: Aprenda a usar o sandbox no Aspose.HTML Java para definir o agente de
  usuário, definir o tamanho e obter o tamanho da viewport instantaneamente. Código
  completo, explicações e dicas incluídos.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: pt
og_description: Aprenda a usar o sandbox no Aspose.HTML Java para definir o agente
  de usuário, definir o tamanho e obter o tamanho da viewport instantaneamente. Guia
  completo com código e melhores práticas.
og_title: Como usar o Sandbox – Definir o User Agent e obter o tamanho da viewport
tags:
- AsposeHTML
- Java
- Sandbox
title: Como usar o Sandbox – Definir o agente de usuário e obter o tamanho da viewport
url: /pt/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar o Sandbox – Definir User Agent e Obter Tamanho da Viewport

Já se perguntou **como usar o sandbox** ao renderizar HTML com Aspose.HTML for Java? Talvez você tenha encontrado dificuldades ao tentar simular um tamanho de tela específico ou precise falsificar uma string de user‑agent para que a página se comporte como se estivesse sendo visitada a partir de um navegador móvel.  

A boa notícia é que a API do sandbox permite fazer exatamente isso, e você também pode obter o tamanho da viewport calculado após a página ser carregada. Neste tutorial vamos percorrer a criação de um sandbox, a definição do tamanho, a configuração de um user agent personalizado, o carregamento de uma página remota e, finalmente, a leitura das dimensões da viewport. Ao final, você saberá **como definir o tamanho**, **como obter a viewport**, e por que essas etapas são importantes para um renderização headless confiável.

> **Dica rápida:** você terá uma classe Java executável que imprime algo como `Viewport: 1280×800` em segundos.

---

## O Que Você Precisa

- **Aspose.HTML for Java** versão 24.6 ou mais recente (a API que usamos foi introduzida na 24.5).  
- Um kit de desenvolvimento Java 17+ (qualquer JDK recente serve).  
- Uma IDE ou um editor de texto simples — nenhum plugin especial é necessário.  
- Acesso à internet se você quiser carregar um URL externo, como `https://example.com`.

É só isso. Não é obrigatório usar Maven/Gradle; você pode simplesmente colocar os JARs no classpath manualmente, se preferir.  

---

## Como Usar o Sandbox – Visão Geral

O sandbox isola o motor de renderização do sistema operacional host, permitindo que você defina uma tela virtual (largura, altura, DPI) e uma string de **user agent** personalizada. Pense nele como uma janela de navegador em miniatura que vive inteiramente na memória. Quando você posteriormente solicitar a `HTMLDocument` sua visualização padrão, o motor reportará o **tamanho da viewport** que calculou com base nas configurações do sandbox.  

A seguir, um fluxo de alto nível:

1. **Criar** um `DocumentSandbox` e configurar largura, altura, DPI e user‑agent.  
2. **Carregar** um `HTMLDocument` dentro desse sandbox.  
3. **Consultar** a visualização padrão do documento para obter o tamanho da viewport.  

Vamos mergulhar em cada passo.

---

## Passo 1: Criar um Sandbox e Definir o Tamanho

Primeiro, iniciamos um sandbox e informamos o tamanho da tela virtual. É aqui que você responde à pergunta **como definir o tamanho** para uma renderização headless.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **Dica de especialista:** se você estiver testando um layout responsivo, experimente uma largura estreita como `360` para emular um telefone, ou uma larga como `1920` para um desktop. O sandbox respeita o DPI que você definir, então uma tela de alta densidade (por exemplo, 144 DPI) afetará media‑queries que utilizam `device-pixel-ratio`.

---

## Passo 2: Definir User Agent para o Sandbox

Por que se preocupar com um **user agent** personalizado? Alguns sites entregam marcações ou scripts diferentes dependendo do navegador reportado. Chamando `setUserAgent` você pode enganar a página fazendo-a pensar que está sendo visitada a partir do Chrome, Firefox ou de um dispositivo móvel.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

Agora a página acreditará que está sendo renderizada em um iPhone. Se precisar **definir o user agent** de volta ao padrão, basta reutilizar a string “AsposeHTML/24.6 …” anterior.

---

## Passo 3: Carregar um Documento HTML Dentro do Sandbox

Com o sandbox pronto, podemos carregar qualquer URL ou arquivo HTML local. O construtor `HTMLDocument` recebe o sandbox como segundo argumento, vinculando os dois.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

O bloco `try‑with‑resources` garante que o documento seja descartado corretamente, liberando os recursos nativos que o Aspose.HTML aloca nos bastidores.

---

## Passo 4: Obter o Tamanho da Viewport a Partir do Documento

Chegou o momento que você esperava: recuperar o **tamanho da viewport** que o motor de renderização calculou. Isso responde **como obter a viewport** depois que a página foi layoutada.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

Ao executar o programa, você deverá ver algo como:

```
Viewport: 1280×800
```

Se você alterou as dimensões do sandbox no Passo 1, os números impressos refletirão esses novos valores — perfeito para testes automatizados que verificam pontos de quebra responsivos.

---

## Exemplo Completo Funcionando

Abaixo está a classe completa, pronta‑para‑executar, que reúne todas as peças. Copie‑e‑cole em um arquivo chamado `SandboxExample.java`, adicione os JARs do Aspose.HTML ao seu classpath e execute `java SandboxExample`.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**Saída esperada** (considerando as configurações de sandbox acima):

```
Viewport: 1280×800
```

Se você definir uma largura/altura diferente no sandbox, a saída mudará de acordo — exatamente o que você precisa ao testar designs responsivos.

---

## Casos Limites & Perguntas Frequentes

### E se a página usar `window.innerWidth` em vez de media queries CSS?

O tamanho da tela virtual do sandbox influencia tanto o layout CSS quanto o `window.innerWidth/innerHeight` do JavaScript. Portanto, **como obter a viewport** via JavaScript retornará os mesmos números que você vê no console Java.

### Posso executar vários sandboxes em paralelo?

Sim. Cada instância de `DocumentSandbox` é independente, então você pode criar um pool de threads, atribuir a cada thread seu próprio sandbox com dimensões diferentes e renderizar dezenas de páginas simultaneamente. Apenas lembre‑se de que os JARs são thread‑safe (são).

### A configuração de DPI afeta o dimensionamento de imagens?

Absolutamente. Um DPI maior faz com que um pixel CSS corresponda a mais pixels de dispositivo, o que pode fazer imagens de alta resolução parecerem mais nítidas. Se você estiver testando recursos no estilo retina, experimente `sandbox.setDeviceDpi(144)`.

### Como lidar com certificados HTTPS autoassinados?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}