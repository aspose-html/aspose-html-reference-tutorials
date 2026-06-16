---
category: general
date: 2026-06-16
description: Aprenda a definir o DPI do dispositivo no Aspose e a definir a largura
  e altura da viewport ao renderizar HTML com o sandbox Aspose.HTML em Java. Código
  passo a passo incluído.
draft: false
keywords:
- set device dpi aspose
- set viewport width height
language: pt
og_description: Descubra como definir o DPI do dispositivo no Aspose e definir a largura
  e a altura da viewport usando o sandbox Aspose.HTML para Java. Código completo e
  explicação.
og_title: definir DPI do dispositivo aspose em Java – Guia completo do Sandbox
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to set device dpi aspose and set viewport width height when
    rendering HTML with Aspose.HTML sandbox in Java. Step‑by‑step code included.
  headline: set device dpi aspose in Java – Complete Sandbox Guide
  type: TechArticle
- description: Learn how to set device dpi aspose and set viewport width height when
    rendering HTML with Aspose.HTML sandbox in Java. Step‑by‑step code included.
  name: set device dpi aspose in Java – Complete Sandbox Guide
  steps:
  - name: Configure sandbox options (including DPI and viewport size).
    text: Configure sandbox options (including DPI and viewport size).
  - name: Instantiate a `DocumentSandbox` with those options.
    text: Instantiate a `DocumentSandbox` with those options.
  - name: Load an external HTML page inside the sandbox.
    text: Load an external HTML page inside the sandbox.
  - name: Perform a simple DOM operation—printing the page title.
    text: Perform a simple DOM operation—printing the page title.
  type: HowTo
tags:
- Aspose.HTML
- Java
- HTML rendering
- Sandbox
title: Definir DPI do dispositivo Aspose em Java – Guia Completo do Sandbox
url: /pt/java/advanced-usage/set-device-dpi-aspose-in-java-complete-sandbox-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# set device dpi aspose – Tutorial de Sandbox Java

Já se perguntou como **set device dpi aspose** ao renderizar uma página web em Java? Você não está sozinho. Muitos desenvolvedores esbarram em um obstáculo quando precisam que a página renderizada tenha exatamente a mesma aparência de um dispositivo real—especialmente quando o DPI influencia os cálculos de layout.  

Neste guia vamos percorrer um exemplo prático que não só **set device dpi aspose**, mas também mostra como **set viewport width height** para que a página se comporte como se estivesse em uma janela de navegador de 1280 × 800 pixels. Ao final, você terá um trecho de código executável, uma explicação clara de cada passo e dicas para evitar armadilhas comuns.

## O que este tutorial cobre

Começaremos listando os pré‑requisitos e, em seguida, mergulharemos em quatro passos concisos:

1. Configurar as opções do sandbox (incluindo DPI e tamanho da viewport).  
2. Instanciar um `DocumentSandbox` com essas opções.  
3. Carregar uma página HTML externa dentro do sandbox.  
4. Executar uma operação simples de DOM—imprimir o título da página.

Você verá por que cada parte é importante, como ajustar as configurações para diferentes dispositivos e como deve ser a saída. Não é necessária documentação externa; tudo que você precisa está aqui.

## Pré‑requisitos

- Java 8 ou superior (a biblioteca Aspose.HTML for Java suporta JDK 8+).  
- JARs do Aspose.HTML for Java adicionados ao classpath do seu projeto.  
- Uma IDE ou ferramenta de build (Maven/Gradle) para compilar e executar o código.  
- Acesso à internet se você pretende carregar uma URL ao vivo como `https://example.com`.

Se você já marcou todas essas caixas, vamos começar.

## Passo 1: Set device DPI aspose – Definir opções do Sandbox

A primeira coisa a fazer é dizer ao sandbox qual “tela” você está simulando. É aqui que **set device dpi aspose** entra em ação. O DPI (dots per inch) influencia como as unidades CSS `px` são interpretadas, o que pode mudar tamanhos de fonte, escala de imagens e media queries.

```java
// Step 1: Create sandbox options and configure DPI and viewport.
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setDeviceDpi(96);               // set device dpi aspose
sandboxOptions.setViewportWidth(1280);         // set viewport width height
sandboxOptions.setViewportHeight(800);         // set viewport width height
```

> **Por que isso importa:**  
> *A chamada `setDeviceDpi` informa ao Aspose.HTML que um pixel CSS corresponde a 1/96 de polegada, espelhando a maioria dos monitores de desktop. Se você pular essa etapa, o layout pode aparecer muito pequeno ou muito grande em telas de alta DPI.*

## Passo 2: Criar o Sandbox com as opções configuradas

Agora que as opções estão prontas, você precisa de uma instância de sandbox que as respeite. Pense no sandbox como um pequeno motor de navegador isolado que não tocará seu sistema de arquivos.

```java
// Step 2: Initialise the DocumentSandbox using the options above.
DocumentSandbox documentSandbox = new DocumentSandbox(sandboxOptions);
```

> **Dica profissional:**  
> Reutilizar o mesmo `DocumentSandbox` para várias páginas economiza memória, mas lembre‑se de redefinir as opções se precisar de um DPI ou viewport diferentes depois.

## Passo 3: Carregar um documento HTML dentro do Sandbox

Com o sandbox configurado, carregar uma página é simples. O construtor de `HTMLDocument` aceita a URL e o sandbox que você acabou de criar.

```java
// Step 3: Load a remote HTML page using the sandbox.
HTMLDocument htmlDoc = new HTMLDocument("https://example.com", documentSandbox);
```

> **Caso extremo:**  
> Se o site de destino bloquear requisições automatizadas, você pode receber um erro 403. Nesse caso, baixe o HTML localmente e carregue-o a partir de um caminho de arquivo, ou defina uma string de user‑agent personalizada via `sandboxOptions`.

## Passo 4: Executar operações normais de DOM – Imprimir o título da página

Neste ponto a página está totalmente renderizada dentro do sandbox, então qualquer consulta ao DOM funciona exatamente como em um navegador completo. Vamos manter simples e obter o título.

```java
// Step 4: Access the DOM – print the page title.
System.out.println("Title: " + htmlDoc.getTitle());
```

**Saída esperada**

```
Title: Example Domain
```

Se você vir algo diferente, verifique novamente se a URL está acessível e se você não alterou acidentalmente os valores de DPI ou viewport.

## Por que definir Viewport Width Height é crucial

Você pode se perguntar: “Por que **set viewport width height**?” A resposta está no design responsivo. Media queries como `@media (max-width: 600px)` reagem às dimensões da viewport, não ao tamanho físico da tela. Ao especificar `1280` × `800`, você garante que a página renderize o layout “desktop”, mesmo que o código seja executado em um servidor headless sem display.

```java
sandboxOptions.setViewportWidth(1280);   // set viewport width height
sandboxOptions.setViewportHeight(800);   // set viewport width height
```

Alterar esses números permite simular tablets, smartphones ou até monitores ultra‑largos sem sair da sua IDE.

## Exemplo completo funcional

Abaixo está a classe Java completa, pronta para ser executada, que reúne tudo. Copie‑e cole em um arquivo chamado `SandboxExample.java`, adicione os JARs do Aspose.HTML ao classpath e execute `javac SandboxExample.java && java SandboxExample`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.sandbox.SandboxOptions;

public class SandboxExample {
    public static void main(String[] args) {
        // Step 1: Define sandbox options – set device DPI and viewport.
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setDeviceDpi(96);               // set device dpi aspose
        sandboxOptions.setViewportWidth(1280);         // set viewport width height
        sandboxOptions.setViewportHeight(800);         // set viewport width height

        // Step 2: Create a DocumentSandbox using the defined options.
        DocumentSandbox documentSandbox = new DocumentSandbox(sandboxOptions);

        // Step 3: Load an HTML document inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com", documentSandbox);

        // Step 4: Perform normal DOM operations – print the page title.
        System.out.println("Title: " + htmlDoc.getTitle());
    }
}
```

> **Verificação rápida:**  
> Execute o programa. Se aparecer `Title: Example Domain`, tudo está configurado corretamente. Caso contrário, inspecione o console em busca de exceções—a maioria dos problemas decorre de JARs ausentes ou restrições de rede.

## Armadilhas comuns & como evitá‑las

| Sintoma | Causa provável | Solução |
|---|---|---|
| `NullPointerException` em `htmlDoc.getTitle()` | Sandbox falhou ao carregar a página | Verifique a URL, adicione um try‑catch ao redor do construtor `HTMLDocument`, ou habilite logging via `sandboxOptions.setLogLevel(...)`. |
| Layout parece ampliado/reduzido | DPI não configurado corretamente | Garanta `sandboxOptions.setDeviceDpi(96)` (ou o DPI desejado). |
| Media queries nunca são disparadas | Dimensões da viewport ausentes | Confirme que você chamou tanto `setViewportWidth` **quanto** `setViewportHeight`. |
| Erro de falta de memória em páginas grandes | Reuso de um único sandbox para muitas páginas pesadas | Crie um novo `DocumentSandbox` por página ou chame `documentSandbox.dispose()` após o uso. |

## Expandindo o exemplo

Agora que você sabe como **set device dpi aspose** e **set viewport width height**, pode experimentar ainda mais:

- **Capturar uma screenshot** da página renderizada usando `htmlDoc.renderToBitmap(...)`.  
- **Injetar CSS customizado** antes da renderização para testar temas escuros.  
- **Executar JavaScript** dentro do sandbox com `htmlDoc.getWindow().eval(...)`.  

Todas essas ações respeitam o DPI e a viewport que você configurou, proporcionando um ambiente de teste confiável para layouts responsivos.

## Conclusão

Acabamos de percorrer uma solução concisa, de ponta a ponta, que demonstra como **set device dpi aspose** e **set viewport width height** usando o sandbox do Aspose.HTML em Java. Agora você tem uma base sólida para renderizar páginas exatamente como apareceriam em qualquer dispositivo, tudo dentro de um ambiente seguro e isolado.

Pronto para o próximo passo? Tente renderizar uma página que use CSS Grid, ou carregue uma folha de estilo remota e veja como o DPI influencia a renderização de fontes. O sandbox lhe dá liberdade para experimentar sem afetar seu sistema host.

Se encontrar algum obstáculo, deixe um comentário abaixo ou consulte a documentação do Aspose.HTML for Java—embora tudo o que você precisa já esteja aqui. Boa codificação!  

![diagrama do sandbox set device dpi aspose](https://example.com/images/set-device-dpi-aspose.png "Diagrama mostrando a configuração de DPI e viewport no sandbox Aspose.HTML")


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Create PDF from HTML using Aspose.HTML for Java – Sandbox](/html/english/java/configuring-environment/implement-sandboxing/)
- [Create PDF from HTML – Set User Style Sheet in Aspose.HTML for Java](/html/english/java/configuring-environment/set-user-style-sheet/)
- [How to Set Charset in Aspose.HTML for Java](/html/english/java/configuring-environment/set-character-set/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}