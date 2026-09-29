---
category: general
date: 2026-09-29
description: Defina um agente de usuário personalizado no Aspose.HTML para Java e
  aprenda como definir o tamanho da tela virtual para renderização precisa de HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: pt
lastmod: 2026-09-29
og_description: Defina um agente de usuário personalizado no Aspose.HTML para Java
  e aprenda como definir o tamanho da tela virtual para renderização precisa de HTML.
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: Defina agente de usuário personalizado e dimensões da tela no Aspose.HTML
  para Java
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: Defina agente de usuário e dimensões de tela personalizados no Aspose.HTML
  para Java
url: /pt/java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir agente de usuário personalizado e dimensões da tela no Aspose.HTML para Java

Se você precisar **definir agente de usuário personalizado** ao renderizar HTML com Aspose.HTML para Java, este guia mostra exatamente como fazer isso. Ao configurar uma sandbox, você também obtém a capacidade de **definir tamanho de tela virtual**, garantindo que o layout corresponda a um viewport de navegador real.

Você concluirá este tutorial com um programa completo e executável que **especifica o agente de usuário**, **define a largura da tela** e **define a altura da tela**. Nenhuma ferramenta externa é necessária — apenas Aspose.HTML para Java e um runtime Java 8+.

## O que você aprenderá

* Como criar um `SandboxConfiguration` para isolar a renderização.
* Como **definir agente de usuário personalizado** e por que isso importa para páginas responsivas.
* Como **definir tamanho de tela virtual** (largura e altura da tela) para um layout preciso.
* Como carregar um arquivo HTML na sandbox e salvar o resultado processado.
* Armadilhas comuns e dicas de melhores práticas para renderização em sandbox.

> **Pré-requisitos** – Você precisa de uma licença válida do Aspose.HTML para Java, Java 8 ou superior, e uma IDE (IntelliJ IDEA, Eclipse ou VS Code). O exemplo usa um arquivo local `input.html`, mas qualquer URL acessível funciona.

![Diagrama de fluxo da sandbox](sandbox-flow.png "exemplo de definição de agente de usuário personalizado em Java")

## Etapa 1: Criar uma configuração de sandbox (a base)

A sandbox isola o ambiente de renderização da JVM host, o que é essencial quando você deseja **definir agente de usuário personalizado** ou alterar o tamanho do viewport.

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*Por que esta etapa?*  
`SandboxConfiguration` contém todas as opções de renderização, incluindo **dimensões da tela** e strings de **user‑agent**. Ao configurá‑la antes de carregar o documento, você garante que o motor HTML respeite essas configurações desde a primeira requisição.

## Etapa 2: Definir dimensões da tela para imitar um dispositivo real

Sites responsivos costumam ler `window.innerWidth` e `window.innerHeight`. Para fazer o motor pensar que está em uma tela de 1024 × 768, você **define tamanho de tela virtual**:

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*Por que isso importa* – Se você omitir **definir dimensões da tela**, o renderizador pode usar um viewport muito pequeno, fazendo com que consultas de mídia CSS escolham o layout móvel. Definindo explicitamente **largura da tela** e **altura da tela**, você controla quais regras CSS são aplicadas.

## Etapa 3: Especificar uma string de agente de usuário personalizada

Algumas páginas entregam conteúdo diferente com base no cabeçalho user‑agent. Para **especificar agente de usuário** basta defini‑lo na configuração da sandbox:

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*Por que usar um agente de usuário personalizado?*  
Uma string personalizada pode contornar a detecção de bots, ativar recursos apenas para desktop ou testar como um site se comporta em uma versão específica de navegador. O motor Aspose encaminha esse valor em todas as requisições HTTP feitas ao carregar recursos externos (CSS, imagens, scripts).

## Etapa 4: Carregar o documento HTML dentro da sandbox

Agora que a sandbox está totalmente configurada, carregue o arquivo HTML. O construtor que recebe um caminho de arquivo e um `SandboxConfiguration` aplica automaticamente todas as configurações definidas.

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

Se precisar carregar de uma URL remota, substitua o caminho do arquivo pela string da URL — Aspose.HTML ainda respeitará o **agente de usuário personalizado** e as **dimensões da tela**.

## Etapa 5: Salvar a saída processada

Depois que o documento terminar de carregar, você pode salvá‑lo em qualquer formato suportado. Aqui gravamos um arquivo HTML sandboxed que reflete quaisquer alterações no DOM causadas pelas configurações personalizadas.

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

O arquivo salvo conterá o mesmo markup, mas quaisquer scripts que consultarem `navigator.userAgent` ou inspecionarem `window.innerWidth` verão agora os valores que você forneceu.

## Exemplo completo e executável

Juntando todas as etapas, você obtém um programa autocontido que pode copiar, colar e executar.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### Saída esperada

Executar o programa cria `sandboxed_output.html`. Se você abri‑lo em um navegador e inspecionar `navigator.userAgent` via console, verá **AsposeHTML/1.0**. Da mesma forma, `window.innerWidth` reportará **1024**, confirmando que as **dimensões da tela** foram definidas corretamente.

## Perguntas comuns e tratamento de casos extremos

| Pergunta | Resposta |
|----------|----------|
| **E se a página carregar recursos adicionais de um domínio diferente?** | A sandbox encaminha o **agente de usuário personalizado** em cada requisição, mas as políticas de origem cruzada ainda se aplicam. Use `sandboxConfig.setAllowCrossDomain(true)` se precisar relaxar essas restrições. |
| **Posso mudar o tamanho da tela após o documento ser carregado?** | Não. As dimensões da tela são lidas durante a primeira passagem de layout. Para renderizar com outro tamanho, crie um novo `SandboxConfiguration` e recarregue o documento. |
| **Preciso chamar `document.close()`?** | O `HTMLDocument` implementa `AutoCloseable`. Usar um bloco try‑with‑resources garante a limpeza adequada, mas chamar `close()` explicitamente é opcional em scripts simples. |
| **Como isso difere de definir um agente de usuário em um cliente HTTP?** | Definir o agente de usuário na sandbox afeta **todos** os pedidos de recursos feitos pelo motor HTML, não apenas a requisição inicial do HTML. Isso imita um navegador real de forma mais precisa. |
| **A sandbox é segura para HTML não confiável?** | Sim. A sandbox isola o acesso ao sistema de arquivos e limita chamadas de rede conforme a configuração, reduzindo o risco de scripts maliciosos afetarem sua JVM host. |

## Dicas profissionais

* **Reutilizar configurações** – Se você renderizar muitas páginas com o mesmo viewport, crie um único `SandboxConfiguration` e reutilize‑o para evitar sobrecarga de criação de objetos.
* **Depurar com logging** – Ative o logging do Aspose.HTML (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`) para ver quais recursos foram buscados com o agente de usuário personalizado.
* **Combinar com consultas de mídia CSS** – Ajustando **largura da tela** você pode testar como seu design responsivo se comporta em tablets, telefones ou desktops grandes sem abrir um navegador real.

## Conclusão

Agora você sabe como **definir agente de usuário personalizado** e **definir dimensões da tela** ao renderizar HTML com Aspose.HTML para Java. Ao configurar uma sandbox, você isola o ambiente, controla o viewport e garante que recursos externos vejam exatamente os cabeçalhos que você especificou. Essa técnica é essencial para testar layouts responsivos, contornar bloqueios de bots ou reproduzir recursos exclusivos de desktop em pipelines automatizados.

Em seguida, você pode explorar **como definir cookies personalizados** ou **capturar screenshots renderizados** usando a API de renderização do Aspose.HTML — ambos os conceitos se baseiam no mesmo padrão de configuração de sandbox que você acabou de dominar.

Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [High DPI Rendering in Java – Capture Webpage Screenshots with Custom User Agent](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [How to Load HTML, Set Device DPI & Read Background Color](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Create HTML File Java & Set Up Network Service (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}