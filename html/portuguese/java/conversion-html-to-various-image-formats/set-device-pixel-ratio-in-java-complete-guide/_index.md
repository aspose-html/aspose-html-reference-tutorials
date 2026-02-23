---
category: general
date: 2026-02-22
description: Defina a proporção de pixels do dispositivo em Java com o sandbox do
  Aspose.HTML. Aprenda como definir um agente de usuário personalizado, obter o título
  da página em Java e converter HTML para PNG em um único tutorial.
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- save html as image
- convert html to png
- get page title java
language: pt
og_description: Defina a proporção de pixels do dispositivo em Java usando o sandbox
  Aspose.HTML. Este tutorial mostra como definir um agente de usuário personalizado,
  recuperar o título da página em Java e converter HTML em PNG.
og_title: Definir a proporção de pixels do dispositivo em Java – Guia completo
tags:
- Aspose.HTML
- Java
- Web Rendering
title: Definir a proporção de pixels do dispositivo em Java – Guia completo
url: /pt/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir Device Pixel Ratio em Java – Guia Completo

Já se perguntou como **definir device pixel ratio** ao renderizar uma página web a partir de Java? Você não está sozinho. Muitos desenvolvedores precisam emular telas móveis de alta‑DPI para que as capturas de tela fiquem nítidas, especialmente quando depois **salvam html como imagem** para relatórios ou materiais de marketing. Neste tutorial, vamos percorrer um exemplo prático que faz exatamente isso—além de mostrar como **definir user agent personalizado**, **obter título da página java**, e **converter html para png** usando Aspose.HTML.

Começaremos com uma breve visão geral da API sandbox, depois mergulharemos em cada passo de configuração e, por fim, produziremos um arquivo PNG que reproduz a tela de um iPhone real. Ao final, você terá um trecho reutilizável que pode inserir em qualquer projeto Java. Nenhuma ferramenta externa necessária, apenas Java puro e Aspose.HTML 7.x (ou mais recente).

---

## Pré-requisitos

- Java 17 ou posterior (o código compila com versões anteriores, mas 17 é recomendado).
- Biblioteca Aspose.HTML for Java (download no site oficial da Aspose; coordenadas Maven: `com.aspose:aspose-html:23.10`).
- Um IDE ou editor de texto de sua escolha (IntelliJ IDEA, VS Code, Eclipse… todos funcionam).
- Acesso à internet para a URL de demonstração (`https://example.com/responsive.html`), ou substitua por qualquer página HTML pública que você possua.

> **Dica:** Se você estiver atrás de um proxy, configure as propriedades de sistema `http.proxyHost` e `http.proxyPort` da JVM antes de executar o código.

---

## Etapa 1: Definir Device Pixel Ratio e Outras Opções do Sandbox

A primeira coisa que precisamos é de uma instância **SandboxOptions** onde definimos o tamanho da tela virtual e o *device pixel ratio* (DPR). Pense no DPR como o fator que informa ao navegador quantos pixels físicos correspondem a um pixel CSS. Em um iPhone Retina, o DPR costuma ser **2.0**, por isso usaremos esse valor.

```java
// Step 1: Create and configure SandboxOptions
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS width of an iPhone X
sandboxOptions.setScreenHeight(667);         // CSS height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
```

> **Por que isso importa:** Sem definir o DPR correto, a imagem renderizada aparecerá borrada ou superdimensionada porque o rasterizador assume um mapeamento de pixel 1:1.

---

## Etapa 2: Definir User Agent Personalizado

Os sites frequentemente servem marcações diferentes com base no cabeçalho **User‑Agent**. Para garantir que nossa página se comporte como em um iPhone real, injetamos uma string personalizada que imita o Safari no iOS.

```java
// Step 2: Define a mobile‑specific user agent
String iphoneUA = "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                  "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                  "Version/14.0 Mobile/15E148 Safari/604.1";

sandboxOptions.setUserAgent(iphoneUA);   // <-- set custom user agent
```

> **Caso especial:** Alguns sites também verificam o cabeçalho `Accept-Language`. Se você notar traduções ausentes, adicione `sandboxOptions.setAcceptLanguage("en-US,en;q=0.9");`.

---

## Etapa 3: Carregar a Página Dentro do Sandbox e Obter o Título

Agora iniciamos o sandbox com as opções que acabamos de definir. O objeto **Sandbox** isola o processo de renderização, garantindo que nossas configurações de DPR e user‑agent sejam respeitadas.

```java
// Step 3: Create the sandbox and load the HTML document
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
HTMLDocument htmlDoc = new HTMLDocument(
        "https://example.com/responsive.html", mobileSandbox);
```

Depois que a página carrega, recuperar o título é tão simples quanto chamar `getTitle()`. Isso satisfaz o requisito de **get page title java**.

```java
// Step 3b: Print the page title to the console
System.out.println("Title: " + htmlDoc.getTitle());   // <-- get page title java
```

**Saída esperada no console**

```
Title: Responsive Demo – Mobile View
```

Se o título estiver vazio, verifique novamente a URL ou certifique-se de que a página não está bloqueada por políticas CORS.

---

## Etapa 4: Converter HTML para PNG e Salvar HTML como Imagem

Aspose.HTML permite renderizar o DOM diretamente para um arquivo de imagem. Como já definimos o DPR para 2.0, o PNG resultante terá o dobro da densidade de pixels, produzindo uma captura de tela nítida.

```java
// Step 4: Render and save as PNG (convert html to png)
htmlDoc.save("mobile_view.png");   // <-- save html as image
```

O método `save` detecta automaticamente a extensão do arquivo e escolhe o renderizador apropriado. Se precisar de um formato diferente (JPEG, BMP), basta alterar o nome do arquivo conforme necessário.

> **E se você precisar de um tamanho de imagem específico?**  
> Use `ImageSaveOptions` para controlar largura, altura e cor de fundo:

```java
ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
pngOptions.setWidth(750);   // 375 CSS px * DPR 2
pngOptions.setHeight(1334);
htmlDoc.save("mobile_view_custom.png", pngOptions);
```

---

## Exemplo Completo Funcional

Abaixo está o programa completo, pronto‑para‑executar, que une todas as etapas. Copie‑e‑cole em um arquivo `SandboxDemo.java`, adicione a dependência Aspose.HTML e execute `java SandboxDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.rendering.image.ImageSaveOptions;
import com.aspose.html.rendering.image.SaveFormat;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Configure sandbox – set device pixel ratio, screen size, and user agent
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS width (iPhone)
        sandboxOptions.setScreenHeight(667);         // CSS height
        sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                "Version/14.0 Mobile/15E148 Safari/604.1");   // <-- set custom user agent

        // 2️⃣ Create sandbox instance
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // 3️⃣ Load the target page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox);

        // 4️⃣ Retrieve and print the page title (get page title java)
        System.out.println("Title: " + htmlDoc.getTitle());

        // 5️⃣ Render the page – convert html to png and save html as image
        // Simple save (auto‑detect PNG)
        htmlDoc.save("mobile_view.png");   // <-- save html as image

        // 6️⃣ Optional: custom size rendering
        ImageSaveOptions opts = new ImageSaveOptions(SaveFormat.PNG);
        opts.setWidth(750);   // 375 * DPR 2
        opts.setHeight(1334);
        htmlDoc.save("mobile_view_custom.png", opts); // another convert html to png example
    }
}
```

Executar o programa gera dois arquivos PNG:

| Arquivo | Descrição |
|------|-------------|
| `mobile_view.png` | Renderização padrão usando o DPR configurado. |
| `mobile_view_custom.png` | Renderização com largura/altura explícitas (útil para ativos de tamanho fixo). |

Você pode abrir qualquer um dos arquivos em qualquer visualizador de imagens para verificar a saída em alta resolução.

---

## Perguntas Frequentes & Casos Especiais

| Pergunta | Resposta |
|----------|--------|
| **E se a página contiver JavaScript que modifica o DOM após o carregamento?** | Aspose.HTML executa scripts por padrão. Se precisar de um instantâneo estático antes da execução do script, defina `sandboxOptions.setEnableJavaScript(false)`. |
| **Posso renderizar uma página que requer autenticação?** | Sim. Use `sandboxOptions.setCredentials(new NetworkCredential("user","pass"))` ou injete cookies via `sandboxOptions.getCookies().add(...)`. |
| **O DPR está limitado a 2.0?** | Não. Você pode definir qualquer double positivo (por exemplo, 3.0 para dispositivos ultra‑high‑DPI). Apenas lembre-se de que um DPR maior gera arquivos de imagem maiores. |
| **Como lidar com páginas com recursos grandes (imagens, fontes)?** | Aumente o limite de memória do sandbox com `sandboxOptions.setMemoryLimit(512 * 1024 * 1024)` (bytes). Isso evita erros de falta de memória em páginas pesadas. |
| **Preciso fechar o sandbox manualmente?** | O `Sandbox` implementa `AutoCloseable`. Envolva-o em um bloco try‑with‑resources para limpeza automática. |

---

## Conclusão

Mostramos como **definir device pixel ratio** em um sandbox Java, **definir user agent personalizado**, **obter título da página java**, e **converter html para png** (efetivamente **salvar html como imagem**) usando Aspose.HTML. O exemplo completo demonstra um fluxo de trabalho prático que você pode adaptar para geração automatizada de capturas de tela, testes de regressão visual ou qualquer cenário onde seja necessária uma representação pixel‑perfect de uma página web.

Sinta-se à vontade para experimentar—alterar o DPR para 3.0, trocar o user‑agent por uma string Android, ou apontar a URL para um arquivo HTML local. O mesmo padrão funciona para PDFs, SVGs ou até renderização de múltiplas páginas.

Se você achou este guia útil, considere explorar tópicos relacionados como **geração de PDF com Aspose.HTML**, **alternativas ao Chrome headless**, ou **renderização em lote de múltiplas URLs**. Boa codificação, e que suas capturas de tela estejam sempre afiadas! 

![definir device pixel ratio em sandbox Java](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}