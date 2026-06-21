---
category: general
date: 2026-02-14
description: Como definir DPI para conversão de SVG para PNG usando Java. Exporte
  PNG em alta resolução, aprenda a converter SVG para PNG e use uma biblioteca de
  conversão de imagens Java.
draft: false
keywords:
- how to set dpi
- convert svg to png
- export high resolution png
- how to convert svg
- java image conversion library
language: pt
og_description: Como definir DPI para conversão de SVG para PNG usando Java. Este
  guia mostra como exportar PNG em alta resolução e usar uma biblioteca de conversão
  de imagens Java.
og_title: Como definir DPI ao converter SVG para PNG com Java
tags:
- java
- image-conversion
- svg
- png
title: Como definir DPI ao converter SVG para PNG com Java
url: /pt/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/
---

final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Definir DPI ao Converter SVG para PNG com Java

Já se perguntou **como definir DPI** para uma conversão de SVG‑para‑PNG de modo que o resultado fique nítido em um pôster pronto para impressão? Você não está sozinho. Em muitos projetos—pense em folhetos de marketing, mock‑ups de UI ou diagramas técnicos—obter um PNG de alta resolução a partir de um SVG é indispensável.  

Neste tutorial vamos percorrer os passos exatos para **converter SVG para PNG**, **exportar PNG em alta resolução** e, mais importante, controlar o DPI usando a biblioteca Aspose.HTML for Java. Ao final, você terá um trecho reutilizável que pode ser inserido em qualquer aplicação Java, seja ela uma ferramenta desktop ou um serviço backend.

## O que Você Precisa

- **Java 8+** (o código compila com qualquer JDK recente)
- **Aspose.HTML for Java** JARs (disponíveis no Maven Central ou no site da Aspose)
- Um arquivo SVG que você deseja rasterizar  
- Um pouquinho de curiosidade—nada mais.

Se você está confortável com Maven, basta adicionar a dependência mostrada na próxima seção; caso contrário, faça o download dos JARs manualmente e adicione‑os ao seu classpath.

## Etapa 1: Adicionar a Biblioteca de Conversão de Imagem Java

Primeiro de tudo—seu projeto precisa da **java image conversion library** que realmente sabe ler SVG e gravar PNG. Aspose.HTML é uma escolha sólida porque lida com CSS, fontes e recursos vetoriais complexos prontamente.

**Usuários Maven** podem colar isto no seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- use the latest stable version -->
</dependency>
```

**Entusiastas do Gradle** podem adicionar:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

Se preferir a rota manual, faça o download do JAR na página de download da Aspose e coloque‑o em `libs/`, depois adicione‑o ao caminho de compilação da sua IDE.

> **Dica de especialista:** Fique de olho no número da versão; lançamentos mais recentes costumam melhorar o tratamento de DPI e corrigir bugs de casos extremos.

## Etapa 2: Criar Opções de Conversão e Definir o DPI Desejado

Agora que a biblioteca está incluída, precisamos dizer a ela *como* queremos que o PNG de saída pareça. É aqui que a palavra‑chave principal—**como definir DPI**—entra em ação. A classe `ImageConversionOptions` oferece controle granular sobre a resolução horizontal (`dpiX`) e vertical (`dpiY`).

```java
import com.aspose.html.converters.ImageConversionOptions;

// Step 2: Build the options object and set DPI
ImageConversionOptions conversionOptions = new ImageConversionOptions();
conversionOptions.setDpiX(300); // 300 DPI horizontally
conversionOptions.setDpiY(300); // 300 DPI vertically
```

Por que 300 DPI? Para a maioria dos fluxos de trabalho de impressão, 300 pontos‑por‑polegada é considerado “qualidade de impressão”. Se você está mirando em ativos apenas para web, pode reduzir isso para 72 ou 96 DPI para manter os tamanhos de arquivo menores.

> **E se eu precisar de um DPI diferente para largura e altura?**  
> Basta alterar `setDpiX` e `setDpiY` independentemente. A biblioteca respeita valores não uniformes, o que é útil para imagens anamórficas.

## Etapa 3: Executar a Conversão de SVG‑para‑PNG

Com as opções prontas, a conversão real é uma única chamada estática. Usaremos `java.nio.file.Paths` para manter tudo independente de plataforma.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.Paths;

public class SvgToPng {
    public static void main(String[] args) throws Exception {
        // Paths to input SVG and output PNG
        var inputSvg  = Paths.get("YOUR_DIRECTORY/input.svg").toUri();
        var outputPng = Paths.get("YOUR_DIRECTORY/output.png").toUri();

        // Convert using the DPI settings we defined earlier
        Converter.convert(inputSvg, outputPng, conversionOptions);
    }
}
```

É isso—execute o método `main` e você encontrará um PNG nítido de 300 DPI em `YOUR_DIRECTORY`. A biblioteca escala automaticamente os gráficos vetoriais para corresponder ao DPI especificado, preservando a proporção e a clareza do texto.

## Etapa 4: Verificar o Resultado (Opcional, mas Recomendado)

Uma verificação rápida pode evitar dores de cabeça depois. Abra o PNG gerado em qualquer visualizador de imagens que mostre metadados de DPI (por exemplo, Photoshop, GIMP ou até a aba “Detalhes” do Windows Explorer). Você deverá ver **300 DPI** listado sob resolução horizontal e vertical.

Se o arquivo parecer borrado, verifique:

1. Se o SVG original não está em baixa resolução (arquivos vetoriais são independentes de resolução, mas imagens raster incorporadas podem limitar a qualidade).  
2. Se você realmente salvou o arquivo após definir o DPI—às vezes IDEs armazenam em cache builds antigos.  
3. Se as opções de conversão não foram sobrescritas em outro ponto do seu código.

## Por Que o DPI Importa ao Exportar PNG de Alta Resolução

Você pode perguntar: “Por que se preocupar com DPI? PNG não são apenas pixels?” A verdade é que DPI é uma *metadata* que indica a aplicativos downstream (especialmente os orientados à impressão) quantos pixels correspondem a uma polegada de espaço físico. Se você entregar um PNG 1200 × 800 a uma impressora sem metadados de DPI adequados, a impressora pode assumir um padrão (geralmente 72 DPI) e ampliar a imagem, resultando em saída desfocada.

Definir o DPI corretamente também traz ganho de desempenho: você evita a necessidade de redimensionar imagens raster posteriormente, o que pode ser computacionalmente caro e degradar a qualidade.

## Casos de Borda & Armadilhas Comuns

| Situação | O Que Observar | Como Corrigir |
|-----------|-------------------|------------|
| **SVG contém imagens bitmap incorporadas** | O bitmap incorporado pode ser de baixa resolução, fazendo o PNG final parecer pixelado mesmo com DPI alto. | Substitua o bitmap por uma versão de maior resolução ou edite o SVG para referenciar uma imagem externa. |
| **Valores de DPI muito altos (ex.: 1200 DPI)** | O consumo de memória dispara; você pode encontrar um `OutOfMemoryError`. | Aumente o tamanho do heap da JVM (`-Xmx2g`) ou limite o DPI a um máximo sensato para seu caso de uso. |
| **Pixels não quadrados** | Alguns monitores interpretam DPI de forma diferente, resultando em imagens esticadas. | Garanta que `setDpiX` seja igual a `setDpiY`, a menos que haja um motivo específico para diferir. |
| **Fontes ausentes** | Texto no SVG pode recair para uma fonte padrão, alterando o layout. | Incorpore fontes no SVG ou instale as fontes necessárias na máquina de execução. |

## Resumo Rápido (em Uma Frase)

Para **como definir DPI** em uma conversão de SVG‑para‑PNG, crie um objeto `ImageConversionOptions`, defina `dpiX`/`dpiY` e chame `Converter.convert` da biblioteca Aspose.HTML Java.

## Próximos Passos & Tópicos Relacionados

- **Processamento em lote:** Percorra um diretório de arquivos SVG e aplique as mesmas configurações de DPI.  
- **DPI dinâmico:** Leia um arquivo de configuração ou argumento de linha de comando para definir o DPI em tempo de execução.  
- **Bibliotecas alternativas:** Se não puder usar Aspose, considere **Batik** (Apache) ou **SVG Salamander**, embora possam exigir código extra para lidar com DPI.  
- **Exportar PNG de alta resolução** para ativos Android: combine esta técnica com as pastas `drawable‑hdpi`, `xhdpi`, etc., do Android.

Sinta‑se à vontade para experimentar—tente 72 DPI para miniaturas web, 600 DPI para impressões de grande formato ou até 150 DPI como um meio‑termo. O código permanece o mesmo; apenas os números mudam.

---

![como definir dpi](placeholder-image.png "Ilustração da definição de DPI no fluxo de trabalho de conversão Java")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}