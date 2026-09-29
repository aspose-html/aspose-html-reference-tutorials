---
category: general
date: 2026-09-29
description: Alterar a cor de fundo com JavaScript em um arquivo HTML usando Java.
  Aprenda a carregar HTML em Java, executar JS no HTML e modificar o HTML com Java
  para um novo fundo de página.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change background color javascript
- load html in java
- run js in html
- modify html with java
- set page background
language: pt
lastmod: 2026-09-29
og_description: Altere a cor de fundo com JavaScript em uma página HTML usando Java.
  Este tutorial mostra como carregar HTML em Java, executar JavaScript no HTML e definir
  o fundo da página programaticamente.
og_image_alt: Screenshot of Java code that changes the page background color
og_title: Alterar cor de fundo com JavaScript usando Java – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Change background color javascript in an HTML file using Java. Learn
    to load html in java, run js in html, and modify html with java for a new page
    background.
  headline: How to change background color javascript using Java
  type: TechArticle
tags:
- Java
- HTMLUnit
- JavaScript
- HTML manipulation
title: Como mudar a cor de fundo em JavaScript usando Java
url: /pt/java/editing-html-documents/how-to-change-background-color-javascript-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como mudar a cor de fundo javascript usando Java

Se você precisar **change background color javascript** em um arquivo HTML existente, pode fazer isso totalmente a partir do Java sem abrir um navegador. Este tutorial mostra como **load html in java**, executar um pequeno trecho de JavaScript e então **modify html with java** para que o fundo da página seja atualizado.  

A solução funciona com a biblioteca de código aberto **HTMLUnit**, que fornece um navegador headless capaz de avaliar JavaScript exatamente como um navegador real faria. Ao final deste guia, você terá um método reutilizável que **sets page background** para qualquer cor que escolher.

## Pré-requisitos

| O que você precisa | Por que isso importa |
|--------------------|----------------------|
| Java 8 ou superior | HTMLUnit requer pelo menos Java 8. |
| Ferramenta de build Maven ou Gradle | Para obter a dependência HTMLUnit automaticamente. |
| Um arquivo HTML que você deseja editar (por exemplo, `input.html`) | O documento fonte que será carregado e alterado. |

Adicione HTMLUnit ao seu projeto:

*Maven*  

```xml
<dependency>
    <groupId>net.sourceforge.htmlunit</groupId>
    <artifactId>htmlunit</artifactId>
    <version>2.71.0</version>
</dependency>
```

*Gradle*  

```gradle
implementation 'net.sourceforge.htmlunit:htmlunit:2.71.0'
```

> **Dica profissional:** Use a versão estável mais recente do HTMLUnit para obter o motor JavaScript mais preciso.

## Mudar cor de fundo javascript – carregar HTML em Java

O primeiro passo é carregar o documento HTML em um objeto `HTMLPage`. Isso fornece uma API semelhante ao DOM e um contexto de execução de JavaScript.

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;

public class BackgroundColorChanger {

    /**
     * Loads an HTML file from the given path.
     *
     * @param htmlPath absolute or relative path to the source HTML file
     * @return HtmlPage representing the loaded document
     * @throws IOException if the file cannot be read
     */
    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        // WebClient acts as a headless browser; disabling CSS speeds up loading.
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);

        // Convert the file path to a URL that HTMLUnit can understand.
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }
}
```

*Por que isso importa*: `WebClient` cria um ambiente sandbox onde o JavaScript pode ser executado, permitindo que você **run js in html** exatamente como o navegador do usuário faria.

## Executar js em html para definir o fundo da página

Depois que a página é carregada, você pode avaliar qualquer expressão JavaScript. O trecho abaixo altera o estilo `backgroundColor` do elemento `<body>`.

```java
/**
 * Executes JavaScript that changes the page background color.
 *
 * @param page   the HtmlPage loaded earlier
 * @param color  any valid CSS color string, e.g., "lightblue" or "#ffcc00"
 */
private static void changeBackground(HtmlPage page, String color) {
    // The eval method runs JavaScript in the page's context.
    String script = "document.body.style.backgroundColor = '" + color + "';";
    page.getEnclosingWindow().getScriptableObject().eval(script);
}
```

*Explicação*:  
- `document.body.style.backgroundColor` é a propriedade DOM padrão para o fundo da página.  
- Ao chamar `eval`, nós **run js in html** sem precisar de uma janela de navegador real.  
- O método é reutilizável para qualquer cor, atendendo ao requisito de **set page background**.

## Modificar html com java e salvar o resultado

Depois que o script é executado, o DOM reflete o novo estilo. Agora você pode gravar o HTML atualizado de volta ao disco.

```java
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Saves the modified HTML content to a new file.
 *
 * @param page          the HtmlPage that has been altered
 * @param outputPath    destination file path
 * @throws IOException  if writing fails
 */
private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
    // page.asXml() returns the current HTML markup, including the changed style.
    String updatedHtml = page.asXml();
    Files.write(Paths.get(outputPath), updatedHtml.getBytes());
}
```

Juntando tudo, você obtém um único programa executável:

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class BackgroundColorChanger {

    public static void main(String[] args) {
        // Adjust these paths for your environment.
        String inputFile = "YOUR_DIRECTORY/input.html";
        String outputFile = "YOUR_DIRECTORY/js_modified.html";
        String newColor = "lightblue"; // Change to any CSS color you need.

        try {
            HtmlPage page = loadHtml(inputFile);
            changeBackground(page, newColor);
            saveModifiedHtml(page, outputFile);
            System.out.println("Background color changed to '" + newColor + "' and saved to " + outputFile);
        } catch (IOException e) {
            System.err.println("Error processing HTML file: " + e.getMessage());
        }
    }

    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }

    private static void changeBackground(HtmlPage page, String color) {
        String script = "document.body.style.backgroundColor = '" + color + "';";
        page.getEnclosingWindow().getScriptableObject().eval(script);
    }

    private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
        String updatedHtml = page.asXml();
        Files.write(Paths.get(outputPath), updatedHtml.getBytes());
    }
}
```

### Saída esperada

Executar o programa imprime:

```
Background color changed to 'lightblue' and saved to YOUR_DIRECTORY/js_modified.html
```

Abrir `js_modified.html` em qualquer navegador mostra a página com um fundo azul claro, confirmando que a operação **change background color javascript** foi bem-sucedida.

## Variações comuns e casos de borda

| Situação | Como lidar |
|----------|------------|
| **Diferentes formatos de cor** | Passe qualquer valor compatível com CSS (`"red"`, `"#ff0000"`, `"rgb(255,0,0)"`). |
| **Tag `<body>` ausente** | O script falhará silenciosamente; você pode primeiro garantir que `<body>` exista com `page.getFirstByXPath("//body")`. |
| **Arquivos HTML grandes** | Desative CSS (`setCssEnabled(false)`) e habilite apenas os recursos de JavaScript que você precisa para reduzir o uso de memória. |
| **Executar múltiplos scripts** | Chame `changeBackground` repetidamente ou crie um método utilitário que aceite uma lista de comandos JavaScript. |

## Conclusão

Agora você sabe como **change background color javascript** carregando um arquivo HTML em Java, **run js in html**, e **modify html with java** para **set page background** para qualquer cor que escolher. O exemplo completo acima funciona com a biblioteca HTMLUnit mais recente e pode ser integrado a pipelines de automação maiores, como processamento em lote de relatórios HTML ou preparação de modelos de e‑mail.

**Próximos passos**  
- Explore outras manipulações de DOM (por exemplo, inserir elementos, remover scripts).  
- Combine esta abordagem com um renderizador PDF para gerar PDFs das páginas estilizadas.  
- Experimente usar um motor headless diferente, como Selenium WebDriver, se precisar de fidelidade completa ao navegador.

Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Obter Estilo Computado Java – Extrair Cor de Fundo do HTML](/html/english/java/css-html-form-editing/get-computed-style-java-extract-background-color-from-html/)
- [Como Carregar HTML, Definir DPI do Dispositivo e Ler Cor de Fundo](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Gerar HTML a partir de JavaScript em Java – Guia Completo Passo a Passo](/html/english/java/creating-managing-html-documents/generate-html-from-javascript-in-java-complete-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}