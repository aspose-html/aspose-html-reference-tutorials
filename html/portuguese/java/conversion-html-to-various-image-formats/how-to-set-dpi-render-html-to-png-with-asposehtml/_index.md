---
category: general
date: 2026-01-14
description: Como definir DPI ao converter uma URL para PNG. Aprenda a renderizar
  HTML para PNG, definir o tamanho da viewport e salvar HTML como PNG usando Aspose.HTML
  em Java.
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: pt
og_description: como definir dpi ao converter uma URL para PNG. Guia passo a passo
  para renderizar HTML em PNG, controlar o tamanho da viewport e salvar HTML como
  PNG usando Aspose.HTML.
og_title: como definir dpi – Renderizar HTML para PNG com AsposeHTML
tags:
- AsposeHTML
- Java
- image rendering
title: como definir dpi – Renderizar HTML para PNG com AsposeHTML
url: /pt/java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# como definir dpi – Renderizar HTML para PNG com AsposeHTML

Já se perguntou **como definir dpi** para uma imagem semelhante a uma captura de tela gerada a partir de uma página da web? Talvez você precise de um PNG de 300 DPI para impressão, ou de uma miniatura de baixa resolução para um aplicativo móvel. Em qualquer caso, o truque é informar ao motor de renderização qual DPI lógico você deseja, e então deixá‑lo fazer o trabalho pesado.  

Neste tutorial, vamos pegar uma URL ao vivo, renderizá‑la para um arquivo PNG, **definir o tamanho da viewport**, ajustar o DPI e, finalmente, **salvar HTML como PNG** — tudo com Aspose.HTML para Java. Sem navegadores externos, sem ferramentas de linha de comando complicadas — apenas código Java limpo que você pode inserir em qualquer projeto Maven ou Gradle.

> **Dica profissional:** Se você só precisa de uma miniatura rápida, pode manter o DPI em 96 DPI (o padrão para a maioria das telas). Para ativos prontos para impressão, aumente para 300 DPI ou mais.

![exemplo de como definir dpi](https://example.com/images/how-to-set-dpi.png "exemplo de como definir dpi")

## O que você precisará

- **Java 17** (ou qualquer JDK recente).  
- **Aspose.HTML for Java** 24.10 ou mais recente. Você pode obtê‑lo no Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- Uma conexão à internet para buscar a página de destino (o exemplo usa `https://example.com/sample.html`).  
- Permissão de escrita na pasta de saída.

É isso — sem Selenium, sem Chrome headless. Aspose.HTML faz a renderização no processo, o que significa que você permanece dentro da JVM e evita a sobrecarga de iniciar um navegador.

## Etapa 1 – Carregar o Documento HTML a partir de uma URL

Primeiro criamos uma instância de `HTMLDocument` apontando para a página que queremos capturar. O construtor baixa automaticamente o HTML, analisa‑o e prepara o DOM.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*Por que isso importa:* Ao carregar o documento diretamente, você evita a necessidade de um cliente HTTP separado. Aspose.HTML respeita redirecionamentos, cookies e até autenticação básica se você incorporar credenciais na URL.

## Etapa 2 – Construir um Sandbox com DPI e Viewport desejados

Um **sandbox** é a forma que o Aspose.HTML tem de imitar um ambiente de navegador. Aqui instruímos que ele finja ser uma tela de 1280 × 720 e, crucialmente, definimos o **DPI do dispositivo**. Alterar o DPI muda a densidade de pixels da imagem renderizada sem alterar o tamanho lógico.

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*Por que você pode ajustar esses valores:*  
- **Tamanho da viewport** controla como as consultas de mídia CSS (`@media (max-width: …)`) se comportam.  
- **DPI do dispositivo** influencia o tamanho físico da imagem quando impressa. Uma imagem de 96 DPI parece boa em telas; uma imagem de 300 DPI mantém a nitidez no papel.  

Se você precisar de uma miniatura quadrada, basta mudar `setViewportSize(500, 500)` e manter o DPI baixo.

## Etapa 3 – Escolher PNG como Formato de Saída

Aspose.HTML suporta vários formatos raster (PNG, JPEG, BMP, GIF). PNG é sem perdas, o que o torna perfeito para capturas de tela onde você deseja que cada pixel seja preservado.

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

Você também pode ajustar o nível de compressão (`pngOptions.setCompressionLevel(9)`) se estiver preocupado com o tamanho do arquivo.

## Etapa 4 – Renderizar e Salvar a Imagem

Agora instruímos o documento a **salvar** a si mesmo como uma imagem. O método `save` recebe um caminho de arquivo e as opções configuradas anteriormente.

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

Quando o programa terminar, você encontrará um arquivo PNG em `YOUR_DIRECTORY/sandboxed.png`. Abra‑o — se você definiu o DPI para 300, os metadados da imagem refletirão isso, embora as dimensões em pixels permaneçam 1280 × 720.

## Etapa 5 – Verificar o DPI (Opcional, mas Útil)

Se você quiser confirmar que o DPI foi realmente aplicado, pode ler os metadados PNG com uma biblioteca leve como **metadata‑extractor**:

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

Você deverá ver `300` (ou o valor que definiu) impresso no console. Esta etapa não é necessária para a renderização, mas é uma verificação rápida, especialmente quando você está gerando ativos para um fluxo de trabalho de impressão.

## Perguntas Frequentes & Casos Especiais

### “E se a página usar JavaScript para carregar conteúdo?”

Aspose.HTML executa um **subconjunto limitado** de JavaScript. Para a maioria dos sites estáticos, funciona imediatamente. Se a página depender fortemente de frameworks do lado do cliente (React, Angular, Vue), pode ser necessário pré‑renderizar a página ou usar um navegador headless. No entanto, a definição de DPI funciona da mesma forma assim que o DOM estiver pronto.

### “Posso renderizar um PDF em vez de PNG?”

Com certeza. Troque `ImageSaveOptions` por `PdfSaveOptions` e altere a extensão de saída para `.pdf`. A configuração de DPI ainda influencia a aparência rasterizada de quaisquer imagens incorporadas.

### “E quanto a capturas de tela de alta resolução para telas retina?”

Basta dobrar as dimensões da viewport mantendo o DPI em 96 DPI, ou manter a viewport e aumentar o DPI para 192. O PNG resultante conterá o dobro de pixels, proporcionando aquela nitidez típica de retina.

### “Preciso liberar recursos?”

`HTMLDocument` implementa `AutoCloseable`. Em um aplicativo de produção, envolva‑o em um bloco try‑with‑resources:

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa completo, pronto para ser executado. Substitua `YOUR_DIRECTORY` por uma pasta real em sua máquina.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

Execute a classe, e você obterá um PNG que respeita a configuração **como definir dpi** que você especificou.

## Conclusão

Nós percorremos **como definir dpi** ao **renderizar HTML para PNG**, cobrimos a etapa **definir tamanho da viewport** e mostramos como **salvar HTML como PNG** usando Aspose.HTML para Java. Os principais pontos são:

- Use um **sandbox** para controlar DPI e viewport.  
- Escolha o **ImageSaveOptions** correto para saída sem perdas.  
- Verifique os metadados de DPI se precisar garantir a qualidade de impressão.  

A partir daqui você pode experimentar diferentes valores de DPI, viewports maiores ou até processar em lote uma lista de URLs. Quer converter um site inteiro em miniaturas PNG? Basta percorrer um array de URLs e reutilizar a mesma configuração de sandbox.

Boa renderização, e que suas capturas de tela sejam sempre perfeitas em pixels!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}