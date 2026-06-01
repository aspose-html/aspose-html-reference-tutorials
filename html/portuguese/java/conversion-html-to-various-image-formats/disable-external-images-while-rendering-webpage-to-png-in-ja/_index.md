---
category: general
date: 2026-05-31
description: Desative imagens externas ao renderizar a página da web para PNG em Java
  usando Aspose HTML. Aprenda a carregar a página da web em sandbox com segurança
  e salvar o documento HTML como PNG.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: pt
og_description: Desative imagens externas ao renderizar uma página da web para PNG
  em Java. Este guia passo a passo mostra como carregar uma página da web em sandbox
  e salvar o documento HTML como PNG.
og_title: Desativar imagens externas ao renderizar página web para PNG em Java
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: Desativar Imagens Externas ao Renderizar Página Web para PNG em Java
url: /pt/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Desativar Imagens Externas ao Renderizar Página Web para PNG em Java

Já precisou **desativar imagens externas** ao renderizar uma página web para PNG em Java? Talvez você esteja construindo um serviço de miniaturas que deve permanecer isolado da internet pública, ou simplesmente queira garantir que nenhuma imagem de terceiros vaze durante a conversão. Seja como for, você chegou ao lugar certo.

Neste tutorial vamos percorrer o carregamento de uma página web em um sandbox, desativar a busca de imagens externas e, finalmente, salvar o documento HTML como um arquivo PNG — tudo com Aspose.HTML para Java. Ao final, você terá um exemplo pronto‑para‑executar, além de várias dicas práticas para evitar armadilhas comuns.

## O que você aprenderá

- **Como renderizar HTML para imagem Java** usando o `Converter` do Aspose.HTML.
- As etapas exatas para **carregar página web em sandbox** com viewport e DPI personalizados.
- A configuração necessária para **desativar imagens externas** mantendo a renderização da página.
- Como **salvar documento HTML como PNG** (ou qualquer outro formato suportado) no disco.
- Tratamento de casos extremos, dicas de desempenho e conselhos de solução de problemas.

### Pré-requisitos

- Java 8 ou superior instalado (o código funciona também com JDK 11+).
- Maven ou Gradle para obter a biblioteca Aspose.HTML para Java.
- Familiaridade básica com sintaxe Java e tratamento de exceções.
- Uma conexão à internet para o carregamento inicial da página (a menos que você sirva o HTML localmente).

> **Dica profissional:** Se você estiver trabalhando atrás de um proxy corporativo, defina as propriedades JVM `http.proxyHost` e `http.proxyPort` antes de executar o exemplo.

---

## Etapa 1: Configurar seu projeto e adicionar Aspose.HTML

Primeiro de tudo — adicione a dependência do Aspose.HTML. Se você estiver usando Maven, insira isto no seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Para Gradle, o equivalente é:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Com a biblioteca no classpath, você está pronto para começar a codificar.

---

## Etapa 2: **Desativar Imagens Externas** com um Ambiente Sandbox

O coração da solução está em `DocumentSandbox`. Ao passar `false` para a flag *allowExternalImages*, instruímos o Aspose.HTML a ignorar quaisquer tags `<img>` que apontem para URLs fora do sandbox. Esse é o mecanismo exato que **desativa imagens externas**.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **Por que isso importa:** Sem o sandbox, o renderizador tentaria baixar cada imagem referenciada pela página, o que pode ser lento, pouco confiável ou até um risco de segurança. Definir a flag como `false` garante uma passagem de renderização limpa e autocontida.

---

## Etapa 3: **Carregar Página Web no Sandbox**  

Agora apontamos o Aspose.HTML para a URL que queremos capturar. O construtor `HTMLDocument` aceita a instância do sandbox, aplicando automaticamente as restrições que definimos.

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

Se a página depender fortemente de scripts externos para o layout, você pode notar conteúdo ausente porque também desativamos scripts. Nesse caso, altere a flag `allowExternalScripts` para `true` mantendo `allowExternalImages` definido como `false`.

---

## Etapa 4: **Renderizar Página Web para PNG**  

Com o documento carregado, convertê‑lo para uma imagem é uma única linha usando `Converter.convert`. O objeto `ImageSaveOptions` permite escolher o formato de saída; aqui escolhemos PNG.

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

O arquivo resultante, `sandboxed.png`, contém uma captura da página **sem quaisquer imagens externas** — apenas SVGs embutidos ou gráficos codificados em base64 permanecem, se houver.

---

## Etapa 5: Verificar a Saída e Depurar Problemas Comuns

Depois de executar o programa, abra `sandboxed.png` em qualquer visualizador de imagens. Você deverá ver o layout da página, texto e estilos CSS, mas todos os elementos `<img src="http://…">` aparecerão em branco (geralmente renderizados como um retângulo branco ou omitidos totalmente).

### Problemas típicos e como corrigi-los

| Sintoma | Causa provável | Solução |
|---|---|---|
| Página em branco | A URL de destino bloqueou a requisição (ex.: Cloudflare) | Adicione cabeçalhos adequados ao user‑agent do sandbox ou use um proxy. |
| Fontes ausentes | Arquivos de fonte estão hospedados externamente | Instale as fontes localmente ou incorpore‑as como `@font-face` com URIs de dados. |
| Deslocamento de layout | CSS referencia folhas de estilo externas que foram bloqueadas | Defina `allowExternalScripts` como `true` *apenas* para carregamento de CSS, então execute novamente. |
| `java.lang.OutOfMemoryError` | Renderizando uma página muito grande em DPI alto | Reduza o tamanho da viewport ou DPI, ou aumente o heap da JVM (`-Xmx2g`). |

---

## Etapa 6: Extendendo o Exemplo – Salvar em Outros Formatos

O mesmo código funciona para JPEG, BMP ou até PDF. Basta mudar o enum `SaveFormat`:

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

Se precisar de um PDF, substitua `ImageSaveOptions` por `PdfSaveOptions` e ajuste a extensão do arquivo adequadamente.

---

## Exemplo Completo (Pronto para Copiar‑Colar)

Abaixo está o **programa completo e executável**. Crie uma nova classe Java, cole o código, garanta que o diretório `output` exista e execute-o.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**Saída esperada** (console):

```
PNG image saved to: output/sandboxed.png
```

Abra `sandboxed.png` — você verá a página renderizada **sem quaisquer imagens externas**.

---

## Perguntas Frequentes

**Q: Ainda posso exibir imagens que estão incorporadas dentro do HTML?**  
A: Sim. URIs `data:` inline ou imagens codificadas em base64 são tratadas como parte do documento e aparecerão no PNG.

**Q: E se eu precisar manter algumas imagens externas, mas bloquear outras?**  
A: O sandbox funciona como um interruptor tudo‑ou‑nada. Para controle mais granular, faça o download das imagens permitidas você mesmo, incorpore‑as como URIs de dados e então renderize.

**Q: Essa abordagem funciona em servidores sem interface gráfica?**  
A: Absolutamente. Aspose.HTML é uma biblioteca pura‑Java; não requer servidor de exibição ou motor de navegador.

**Q: Como isso difere do uso de Selenium ou Puppeteer?**  
A: Selenium controla um navegador real, que é pesado e mais difícil de sandbox. Aspose.HTML renderiza HTML diretamente na memória, oferecendo desempenho determinístico e controles de segurança mais simples, como **desativar imagens externas**.

---

## Conclusão

Agora você tem uma receita sólida, de ponta a ponta, para **desativar imagens externas ao renderizar uma página web para PNG em Java**. Ao aproveitar o `DocumentSandbox`, você obtém controle rígido sobre quais recursos externos são permitidos, garantindo segurança e reprodutibilidade. A partir daqui, experimente diferentes tamanhos de viewport, configurações de DPI ou formatos de saída — cada ajuste abre uma nova possibilidade para gerar miniaturas, pré‑visualizações ou capturas de arquivo.

Pronto para o próximo desafio? Tente renderizar um lote de URLs em paralelo, ou integre essa lógica a um microserviço Spring Boot que devolve PNGs sob demanda. O céu é o limite quando você combina a flexibilidade do Aspose.HTML com as ferramentas de concorrência do Java.

Feliz codificação, e não se esqueça de compartilhar suas histórias de sucesso nos comentários!

## O que você deve aprender a seguir?

- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [How to Render HTML to PNG with Aspose – Complete Guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [How to Edit CSS - Advanced External CSS Editing with Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}