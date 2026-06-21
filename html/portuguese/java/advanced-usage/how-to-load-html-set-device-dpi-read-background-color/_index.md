---
category: general
date: 2026-02-16
description: Como carregar HTML em Java, definir DPI do dispositivo, especificar um
  tamanho de tela virtual e ler a cor de fundo computada de qualquer elemento.
draft: false
keywords:
- how to load html
- read background color
- set device dpi
- set virtual screen size
- get computed background color
language: pt
og_description: Como carregar HTML em Java, definir DPI do dispositivo, especificar
  um tamanho de tela virtual e ler a cor de fundo computada de qualquer elemento.
og_title: Como carregar HTML, definir DPI do dispositivo e ler a cor de fundo
tags:
- Aspose.HTML
- Java
title: Como carregar HTML, definir DPI do dispositivo e ler a cor de fundo
url: /pt/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/
---

translated content and unchanged shortcodes.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Carregar HTML, Definir DPI do Dispositivo e Ler a Cor de Fundo

Já se perguntou **como carregar html** em um aplicativo Java e depois inspecionar os estilos da página? Você não está sozinho—os desenvolvedores frequentemente precisam renderizar uma página web fora da tela, capturar os valores finais de CSS e usá-los para conversão em PDF, capturas de tela ou até testes automatizados.  

Neste guia, vamos percorrer exatamente isso: vamos carregar um arquivo HTML, **definir DPI do dispositivo**, definir um **tamanho de tela virtual** e, finalmente, **ler a cor de fundo** do elemento `<body>`. Ao final, você terá um trecho de código totalmente executável que imprime a **cor de fundo computada**—sem mistério, apenas Java puro.

## O que Você Precisa

* Java 17 ou mais recente (o código funciona com qualquer JDK recente).  
* Aspose.HTML for Java 23.9 ou posterior—baixe o JAR no site da Aspose ou adicione via Maven.  
* Um arquivo HTML simples (por exemplo, `responsive.html`) que define uma cor de fundo em CSS.

É isso—sem frameworks extras, sem drivers de navegador. Pronto? Vamos começar.

![Diagrama ilustrando como carregar html e extrair estilos computados](/images/load-html-diagram.png){alt="Diagrama ilustrando como carregar html"}

## Etapa 1: Como Carregar HTML e Configurar Opções de Renderização

A primeira coisa que você faz é criar um objeto `HtmlLoadOptions`. Esse objeto informa ao Aspose.HTML **como carregar html**—incluindo as dimensões da tela virtual e o DPI que você deseja emular.

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create load options and define the virtual screen size and DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        // setVirtualScreenSize – width × height in CSS pixels
        loadOptions.setScreenSize(new Size(1280, 800));
        // setDeviceDpi – typical desktop DPI (96 is the default for most monitors)
        loadOptions.setDeviceDpi(96);
```

**Por que isso importa:**  
Definir um tamanho de tela virtual garante que consultas de mídia como `@media (max-width: 600px)` se comportem como se a página fosse renderizada em um monitor real. O DPI influencia como unidades CSS `px` são mapeadas para pixels físicos—crucial quando você gera imagens ou PDFs posteriormente.

## Etapa 2: Carregar o Arquivo HTML Usando as Opções Configuradas

Agora realmente carregamos o arquivo. Observe que passamos o mesmo `loadOptions` que acabamos de configurar.

```java
        // 2️⃣ Load the HTML file with the options we just set.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);
```

Se o arquivo não for encontrado, o Aspose lança uma clara `FileNotFoundException`. Em produção, você pode querer envolver isso em um try‑catch e usar uma string HTML padrão como fallback.

## Etapa 3: Definir Tamanho da Tela Virtual e DPI do Dispositivo (Explicitamente)

Embora já tenhamos chamado `setScreenSize` e `setDeviceDpi` acima, vale destacar que **definir tamanho da tela virtual** e **definir DPI do dispositivo** podem ser ajustados a qualquer momento antes da renderização. Por exemplo, você pode aumentar o DPI para capturas de tela de alta resolução:

```java
        // 3️⃣ Adjust DPI for a high‑resolution render (optional).
        loadOptions.setDeviceDpi(300);   // 300 DPI is common for print‑ready images
        // 4️⃣ Change screen size for a mobile layout test.
        loadOptions.setScreenSize(new Size(375, 667)); // iPhone X viewport
```

Lembre-se de recarregar o documento se alterar essas configurações após a primeira carga—o Aspose as trata como imutáveis assim que o `Document` é criado.

## Etapa 4: Ler a Cor de Fundo e Obter a Cor de Fundo Computada

Com o documento na memória, você pode consultar o estilo computado de qualquer elemento. Aqui nos concentramos na tag `<body>`, mas a mesma abordagem funciona para `<div>`, `<p>` ou até pseudo‑elementos.

```java
        // 5️⃣ Retrieve the <body> element.
        Element bodyElement = document.getBody();

        // 6️⃣ Output the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

**O que você verá:** Se `responsive.html` contiver `body { background: #ff5722; }`, o console imprimirá algo como:

```
Computed background color: rgba(255,87,34,1)
```

Esse é o resultado do **get computed background color**—o Aspose resolve todas as regras de cascata CSS, consultas de mídia e até declarações `!important` antes de retornar o valor final.

## Exemplo Completo Funcional

Juntando tudo, aqui está o programa completo, pronto para copiar e colar:

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create load options – virtual screen size + DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setScreenSize(new Size(1280, 800)); // set virtual screen size
        loadOptions.setDeviceDpi(96);                  // set device DPI (default desktop)

        // Optional: tweak for high‑resolution or mobile rendering.
        // loadOptions.setDeviceDpi(300);
        // loadOptions.setScreenSize(new Size(375, 667));

        // Step 2: Load the HTML document with the options.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);

        // Step 3: Grab the <body> element.
        Element bodyElement = document.getBody();

        // Step 4: Print the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

### Saída Esperada

```
Computed background color: rgba(255,255,255,1)
```

*(Os valores RGBA exatos dependem do CSS no seu arquivo HTML.)*

## Armadilhas Comuns & Dicas Profissionais

* **Configuração de DPI ausente?** O Aspose usa 96 DPI por padrão, o que pode desfocar capturas de tela de alta resolução. Sempre defina‑o explicitamente se precisar de saída nítida.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}