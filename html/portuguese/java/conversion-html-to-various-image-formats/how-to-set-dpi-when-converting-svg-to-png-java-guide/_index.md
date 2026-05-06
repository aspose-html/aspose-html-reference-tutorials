---
category: general
date: 2026-05-06
description: Como definir DPI para conversão de SVG para PNG em alta resolução em
  Java usando Aspose.HTML. Aprenda a converter SVG para PNG, exportar SVG como PNG
  e converter vetor em raster.
draft: false
keywords:
- how to set dpi
- convert svg to png
- how to convert svg
- export svg as png
- convert vector to raster
language: pt
og_description: Como definir DPI para conversão de SVG para PNG em alta resolução
  em Java usando Aspose.HTML. Obtenha código passo a passo e dicas de especialistas.
og_title: Como definir DPI ao converter SVG para PNG – Guia Java
tags:
- Java
- Aspose.HTML
- Image Conversion
title: Como definir DPI ao converter SVG para PNG – Guia Java
url: /pt/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Definir DPI ao Converter SVG para PNG – Guia Java

Já se perguntou **como definir DPI** para uma conversão de SVG‑para‑PNG e obter uma imagem nítida, pronta para impressão? Você não está sozinho. Muitos desenvolvedores esbarram quando o PNG exportado fica borrado porque o DPI padrão (geralmente 96) simplesmente não é suficiente para uma saída profissional.

Neste tutorial vamos percorrer um exemplo completo, pronto‑para‑executar, que mostra **como definir DPI** usando Aspose.HTML para Java. Ao final, você será capaz de **converter SVG para PNG**, **exportar SVG como PNG**, e até **converter vetor em raster** com qualquer DPI que precisar — sem mistério, apenas código claro.

## O Que Você Vai Aprender

- Os passos exatos para configurar DPI antes da conversão.
- Por que o DPI importa quando você **converte vetor em raster**.
- Como **converter SVG para PNG** em uma única linha de código.
- Dicas para lidar com SVGs grandes e processamento em lote.
- Um programa completo, compilável, que você pode inserir no seu projeto agora mesmo.

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

- Java 17 ou superior (a última versão LTS funciona melhor).
- Maven ou Gradle para puxar a biblioteca Aspose.HTML.
- Um arquivo SVG simples que você queira rasterizar (por exemplo, `logo.svg`).
- Uma IDE ou editor de texto — IntelliJ IDEA, VS Code, ou até um bom e velho Bloco de Notas serve.

Nenhuma outra ferramenta externa é necessária; a biblioteca faz todo o trabalho pesado.

## Etapa 1: Adicionar Aspose.HTML ao Seu Projeto

Primeiro de tudo, você precisa do JAR do Aspose.HTML. Se estiver usando Maven, adicione este trecho ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Para Gradle, fica assim:

```groovy
implementation 'com.aspose:aspose-html:23.10'
```

> **Dica de especialista:** Sempre use a versão estável mais recente; lançamentos mais novos incluem correções de desempenho para renderização em alta DPI.

## Etapa 2: Como Definir DPI para a Conversão

Agora chegamos ao ponto central — **como definir DPI**. O Aspose.HTML expõe `ImageConversionOptions`, onde você pode especificar tanto a resolução horizontal (`dpiX`) quanto a vertical (`dpiY`). Definir ambas para `300` lhe dá aquela densidade clássica de qualidade de impressão.

```java
import com.aspose.html.converters.ImageConversionOptions;
import com.aspose.html.rendering.Converter;

public class SvgHighRes {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create conversion options
        ImageConversionOptions conversionOptions = new ImageConversionOptions();

        // 2️⃣ Set target DPI for high‑resolution output (300 dpi → crisp print quality)
        conversionOptions.setDpiX(300);
        conversionOptions.setDpiY(300);

        // 3️⃣ Convert the SVG file to a PNG using the configured options
        Converter.convertSvgToPng(
                "YOUR_DIRECTORY/logo.svg",        // source SVG
                "YOUR_DIRECTORY/logo_300dpi.png", // destination PNG
                conversionOptions);
    }
}
```

> **Por que 300 dpi?** É o padrão de fato para impressão profissional. Se precisar de uma imagem para a web, 72 dpi já basta, mas para folhetos ou brochuras você desejará pelo menos 300 dpi.

### Pré‑visualização da Imagem

![Como definir DPI ao converter SVG para PNG](https://example.com/placeholder.png "Como definir DPI ao converter SVG para PNG")

*A imagem acima ilustra a diferença entre um PNG de baixa DPI (esquerda) e um resultado de 300 dpi (direita).*

## Etapa 3: Converter SVG para PNG – Uma Linha de Código

Se o que você quer é um **convert svg to png** rápido, sem mexer no DPI, pode pular o objeto de opções completamente:

```java
Converter.convertSvgToPng("logo.svg", "logo_default.png", null);
```

Passar `null` indica ao Aspose.HTML que use o DPI padrão (geralmente 96). Isso é útil para miniaturas ou quando a qualidade de impressão não importa.

## Etapa 4: Verificar o Resultado – Exportar SVG como PNG

Depois que a conversão terminar, abra o PNG gerado em qualquer visualizador de imagens. Você deverá ver uma imagem raster que corresponde às dimensões do vetor original, mas agora com o DPI que você definiu. A maioria dos visualizadores exibe o DPI nas propriedades da imagem; no Windows, clique com o botão direito → Propriedades → Detalhes.

Se precisar verificar o DPI programaticamente, o `ImageIO` do Java pode lê‑lo:

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File("logo_300dpi.png"));
int dpi = (int) img.getProperty("dpi");
System.out.println("Exported PNG DPI: " + dpi);
```

> **Observação:** Nem todos os formatos de imagem armazenam metadados de DPI; PNG armazena, mas JPEG pode exigir tratamento adicional.

## Casos Limite & Variações

### 1️⃣ Valores de DPI Diferentes

Você pode se perguntar: “E se eu precisar de 600 dpi para um grande cartaz?” Basta mudar os números:

```java
conversionOptions.setDpiX(600);
conversionOptions.setDpiY(600);
```

DPI mais alto significa arquivo maior, então fique atento às restrições de memória ao processar muitos arquivos.

### 2️⃣ Conversão em Lote de uma Pasta

Quando você tem dezenas de SVGs, envolva a conversão em um loop simples:

```java
File dir = new File("YOUR_DIRECTORY");
for (File svg : dir.listFiles((d, name) -> name.endsWith(".svg"))) {
    String pngName = svg.getName().replace(".svg", "_300dpi.png");
    Converter.convertSvgToPng(svg.getAbsolutePath(),
                              new File(dir, pngName).getAbsolutePath(),
                              conversionOptions);
}
```

Esse padrão **converte vetor em raster** em massa, economizando horas de trabalho manual.

### 3️⃣ Lidando com Fundos Transparentes

Se o seu SVG contém transparência e você deseja um fundo branco, renderize primeiro para um `BufferedImage`, depois preencha o fundo:

```java
// Render SVG to BufferedImage with DPI
BufferedImage raster = Converter.convertSvgToImage(
        "logo.svg", conversionOptions);

// Fill background (optional)
Graphics2D g = raster.createGraphics();
g.setComposite(AlphaComposite.SrcOver);
g.setColor(Color.WHITE);
g.fillRect(0, 0, raster.getWidth(), raster.getHeight());
g.dispose();

// Write out PNG
ImageIO.write(raster, "png", new File("logo_whitebg.png"));
```

## Perguntas Frequentes

**Q: Isso funciona no Linux?**  
A: Absolutamente. Aspose.HTML é independente de plataforma; basta garantir que você tenha a runtime Java adequada.

**Q: E se meu SVG referenciar imagens externas?**  
A: Certifique‑se de que esses recursos estejam acessíveis via caminhos absolutos ou URLs; caso contrário, o renderizador os ignorará.

**Q: Posso converter SVG para outros formatos raster como JPEG ou BMP?**  
A: Sim. Use `Converter.convertSvgToJpeg` ou `Converter.convertSvgToBmp` com o mesmo `ImageConversionOptions`.

## Dicas de Especialista para Rasterização de Alta Qualidade

- **Combine DPI ao tamanho final de saída.** Um logotipo de 2 polegadas impresso a 300 dpi precisa de 600 px de largura (2 in × 300 dpi). Escale o SVG adequadamente antes da conversão se precisar de uma dimensão de pixel específica.
- **Fique atento ao perfil de cores.** PNGs não incorporam perfis ICC por padrão; se a fidelidade de cor for importante, converta para TIFF ou use uma biblioteca que suporte incorporação de perfis.
- **Reutilize o objeto `ImageConversionOptions`** ao converter muitos arquivos — isso evita a criação desnecessária de objetos e pode melhorar o desempenho.

## Conclusão

Agora você sabe **como definir DPI** para uma conversão de SVG‑para‑PNG em Java, e viu como a mesma abordagem permite **convert svg to png**, **export svg as png**, e, de modo geral, **convert vector to raster** com controle total sobre a resolução. O exemplo completo acima funciona imediatamente, e as dicas extras fornecem um roteiro para escalar a solução em projetos reais.

Qual será o próximo passo? Experimente trocar o valor de 300 dpi por 600 dpi, teste o processamento em lote, ou explore outros formatos raster. Os mesmos princípios se aplicam — basta mudar o método de saída e você está pronto.

Tem um SVG complicado ou uma dúvida de desempenho? Deixe um comentário, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}