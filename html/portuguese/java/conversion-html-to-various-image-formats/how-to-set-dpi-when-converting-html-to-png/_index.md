---
category: general
date: 2026-03-04
description: Aprenda como definir DPI ao converter HTML para PNG. Este guia também
  aborda exportar HTML como PNG, salvar HTML como PNG e gerar PNG a partir de HTML
  usando Aspose.HTML para Java.
draft: false
keywords:
- how to set dpi
- convert html to png
- export html as png
- save html as png
- generate png from html
language: pt
og_description: Como definir DPI para conversão de HTML para PNG explicado. Siga o
  guia passo a passo para exportar HTML como PNG, salvar HTML como PNG e gerar PNG
  a partir de HTML.
og_title: Como definir DPI ao converter HTML para PNG
tags:
- Aspose.HTML
- Java
- Image Conversion
title: Como definir DPI ao converter HTML para PNG
url: /pt/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Definir DPI ao Converter HTML para PNG

Já se perguntou **como definir DPI** para uma imagem raster que você gera a partir de uma página web? Talvez você esteja construindo uma ferramenta de relatórios, um serviço de miniaturas ou um pipeline de ativos pronto para impressão — qualquer um desses cenários geralmente começa com um documento HTML que precisa se tornar um PNG de alta resolução.  

A boa notícia é que o Aspose.HTML for Java facilita muito **convert HTML to PNG**, e você pode controlar o DPI com apenas uma linha de código. Neste tutorial, percorreremos todo o processo, desde o carregamento do seu arquivo HTML até a exportação como PNG a 300 DPI, abordando também tarefas relacionadas como **export HTML as PNG**, **save HTML as PNG**, e **generate PNG from HTML**.

## O que Você Vai Aprender

- Como configurar o DPI (dots per inch) para a imagem de saída.
- A diferença entre DPI, resolução e qualidade de compressão.
- Um exemplo Java completo e executável que você pode copiar‑colar.
- Armadilhas comuns (por exemplo, fontes ausentes, páginas grandes) e como evitá‑las.
- Dicas rápidas para ajustar a saída quando você precisar **convert HTML to PNG** em diferentes ambientes.

### Pré‑requisitos

- Java 8 ou superior instalado na sua máquina.
- Biblioteca Aspose.HTML for Java (a versão mais recente até março 2026). Você pode obtê‑la do Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

- Um arquivo simples `input.html` que você deseja transformar em uma imagem PNG.

---

## Como Definir DPI para Conversão de HTML para PNG

![Diagram showing DPI setting in code – how to set dpi when converting HTML to PNG](https://example.com/images/dpi-setting.png)

A **etapa principal** que controla a nitidez da imagem é a propriedade `Resolution` de `ImageSaveOptions`. A seguir, dividiremos o processo em etapas pequenas.

### Etapa 1: Definir Caminhos de Entrada e Saída (convert html to png)

Primeiro, informe ao conversor onde está o seu HTML de origem e onde o PNG deve ser gravado.

```java
// Step 1 – file locations
String htmlFilePath = "YOUR_DIRECTORY/input.html";
String pngFilePath  = "YOUR_DIRECTORY/output.png";
```

> **Por que isso importa:** Codificar caminhos de forma fixa funciona para uma demonstração, mas em produção você provavelmente os obterá de configurações ou argumentos de linha de comando. Isso mantém o código flexível para qualquer fluxo de trabalho **save HTML as PNG**.

### Etapa 2: Criar ImageSaveOptions e Definir DPI (how to set dpi)

Agora instanciamos `ImageSaveOptions` para PNG e definimos o DPI para 300. O DPI determina quantos pixels são embalados em cada polegada quando a imagem é impressa ou exibida em seu tamanho nativo.

```java
// Step 2 – configure PNG options
ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
saveOptions.setResolution(300);   // <-- This is the DPI you asked for
saveOptions.setQuality(95);       // PNG compression (0‑100); higher = larger file, better fidelity
```

> **Explicação:**  
> - `setResolution(300)` indica ao Aspose.HTML para renderizar a página a 300 dots per inch.  
> - `setQuality(95)` é opcional para PNG; controla o nível de compressão ZLIB. Você pode diminuí‑lo para arquivos menores se não precisar que cada pixel seja perfeito.

### Etapa 3: Executar a Conversão (export html as png)

Com as opções prontas, a conversão real é feita em uma única linha.

```java
// Step 3 – run the conversion
Converter.convert(htmlFilePath, pngFilePath, saveOptions);
```

> **O que acontece nos bastidores?** Aspose.HTML analisa o HTML, aplica CSS, dispõe o DOM, rasteriza o layout no DPI solicitado e, finalmente, grava um arquivo PNG. Se você precisar **generate PNG from HTML** em um serviço web, pode substituir os caminhos de arquivo por streams.

### Exemplo Completo Funcional

Juntando tudo, aqui está uma classe Java completa que você pode compilar e executar.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.*;
import com.aspose.html.saving.*;

public class ConvertHtmlToPngWithDpi {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the input HTML file and the output PNG file
        String htmlFilePath = "YOUR_DIRECTORY/input.html";
        String pngFilePath  = "YOUR_DIRECTORY/output.png";

        // Step 2: Create image save options for PNG and configure high‑resolution output
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        saveOptions.setResolution(300);   // Set resolution to 300 DPI (how to set dpi)
        saveOptions.setQuality(95);       // PNG compression quality (0‑100)

        // Step 3: Perform the conversion from HTML to PNG using the configured options
        Converter.convert(htmlFilePath, pngFilePath, saveOptions);

        System.out.println("Conversion complete! PNG saved at " + pngFilePath);
    }
}
```

Execute o programa e você encontrará um PNG nítido de 300 DPI no local especificado. Abra‑o em qualquer visualizador de imagens e verifique as propriedades da imagem — o DPI deve indicar **300**.

---

## Perguntas Frequentes & Casos Limítrofes

### E se a configuração de DPI parecer ser ignorada?

- **Certifique‑se de que está usando uma versão recente do Aspose.HTML.** Versões mais antigas ignoravam `Resolution` para PNG.
- **Verifique o tamanho do HTML de origem.** Uma página HTML pequena renderizada a 300 DPI ainda pode produzir uma dimensão de pixel pequena. O DPI afeta apenas o fator de escala, não o tamanho inerente da página.

### Como o DPI difere das dimensões da imagem?

DPI é uma medida *física* (dots per inch). A largura/altura real em pixels é calculada como:

```
pixel width  = CSS width  * DPI / 96
pixel height = CSS height * DPI / 96
```

Se o corpo do seu HTML tem 800 px de largura, a 300 DPI o PNG de saída terá aproximadamente 2500 px de largura (800 × 300 ÷ 96).

### Posso usar outros formatos (JPEG, BMP) ainda controlando o DPI?

Com certeza. Basta mudar `SaveFormat.PNG` para `SaveFormat.JPEG` (ou `BMP`) e manter `setResolution`. Lembre‑se de que JPEG também respeita a configuração `Quality`, que corresponde ao nível de compressão.

### E as fontes que não estão instaladas no servidor?

Aspose.HTML recorrerá a uma fonte padrão, o que pode alterar o layout. Para garantir renderização idêntica, incorpore as fontes necessárias usando `FontSettings`:

```java
FontSettings fontSettings = new FontSettings();
fontSettings.setFontFolder("YOUR_FONT_DIRECTORY", true);
saveOptions.setFontSettings(fontSettings);
```

### Gerando múltiplos PNGs em lote

Se você precisar **generate PNG from HTML** para muitos arquivos, envolva a lógica de conversão em um loop e reutilize uma única instância de `ImageSaveOptions`. Isso reduz o consumo de memória e acelera o processamento.

```java
for (Path htmlPath : Files.newDirectoryStream(Paths.get("batch_html"))) {
    String outPath = htmlPath.toString().replace(".html", ".png");
    Converter.convert(htmlPath.toString(), outPath, saveOptions);
}
```

---

## Dicas Profissionais para Exportação de PNG de Alta Qualidade

1. **Use CSS amigável a vetores** (por exemplo, `transform: scale(1)`) para evitar artefatos de anti‑aliasing em DPI alto.  
2. **Defina uma cor de fundo** se o seu HTML tiver elementos transparentes e você precisar de uma tela sólida:

   ```java
   saveOptions.setBackgroundColor(Color.WHITE);
   ```

3. **Evite imagens inline base64** maiores que alguns MB — elas podem inflar o uso de memória durante a conversão.  
4. **Teste em diferentes DPIs de tela** (por exemplo, monitores de 72 DPI vs. impressoras de 300 DPI) para garantir que a qualidade visual atenda às expectativas.  
5. **Aproveite `setPageSize()`** se quiser que o PNG corresponda a um tamanho de impressão específico (A4, Letter, etc.) independentemente das dimensões originais do HTML.

## Conclusão

Cobremos **como definir DPI** ao **convert HTML to PNG** usando Aspose.HTML for Java, demonstramos um exemplo completo e pronto‑para‑executar, e exploramos tarefas relacionadas como **export HTML as PNG**, **save HTML as PNG** e **generate PNG from HTML**. Ajustando `ImageSaveOptions.setResolution` você controla a nitidez física da saída, enquanto `setQuality` permite equilibrar o tamanho do arquivo com a fidelidade visual.

Próximos passos? Experimente trocar o formato PNG por JPEG para ver como a compressão interage com o DPI, ou experimente o processamento em lote para **convert HTML to PNG** em escala. Você também pode explorar a adição de marcas d'água ou metadados personalizados — ambos são suportados pela rica API do Aspose.HTML.

Tem um cenário complicado que não foi abordado? Deixe um comentário, e nós vamos descobrir juntos. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}