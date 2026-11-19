---
category: general
date: 2026-03-29
description: Como incorporar imagens ao converter MHTML para PDF com Aspose HTML.
  Reduza o tamanho do arquivo PDF e domine as técnicas de conversão de Aspose HTML
  para PDF em minutos.
draft: false
keywords:
- how to embed images
- convert mhtml to pdf
- reduce pdf file size
- aspose html to pdf
- reduce pdf size
language: pt
og_description: Como incorporar imagens ao converter MHTML para PDF com Aspose HTML.
  Aprenda a reduzir o tamanho do arquivo PDF e aproveite ao máximo o Aspose HTML para
  PDF.
og_title: Como incorporar imagens ao converter MHTML para PDF – Guia Aspose
tags:
- Aspose
- Java
- PDF
- MHTML
title: Como incorporar imagens ao converter MHTML para PDF – Guia Aspose
url: /pt/java/conversion-html-to-other-formats/how-to-embed-images-when-converting-mhtml-to-pdf-aspose-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como incorporar imagens ao converter MHTML para PDF – Guia Aspose

Já se perguntou **como incorporar imagens** durante uma conversão de MHTML‑para‑PDF e manter o arquivo resultante leve? Você não está sozinho. Muitos desenvolvedores esbarram em um problema quando seus PDFs aumentam porque cada recurso — fontes, scripts, até pequenos ícones — é inserido dentro. A boa notícia? Com Aspose.HTML for Java você pode instruir o conversor a incorporar **apenas as imagens**, deixando todo o resto como referências externas. Essa única alteração costuma reduzir drasticamente o tamanho do PDF.

Neste tutorial, percorreremos a conversão de um relatório MHTML para PDF, focaremos em **como incorporar imagens** e adicionaremos algumas dicas extras para **reduzir o tamanho do arquivo PDF**. Ao final, você terá uma classe Java pronta‑para‑executar, entenderá por que incorporar apenas imagens é importante e saberá onde ir caso precise posteriormente incorporar fontes ou outros recursos. Sem atalhos vagos como “veja a documentação” — apenas uma solução completa, pronta para copiar e colar.

## O que você aprenderá

- As chamadas de API exatas necessárias para **converter MHTML para PDF** com Aspose.HTML.
- Como configurar `PdfConversionOptions` para que o conversor **incorpore apenas imagens**.
- Por que incorporar apenas imagens ajuda a **reduzir o tamanho do PDF** e quando você pode querer uma configuração diferente.
- Um exemplo Java completo e executável que você pode inserir em qualquer projeto Maven/Gradle.
- Armadilhas comuns (recursos ausentes, caminhos de arquivo incorretos) e correções rápidas.

### Pré-requisitos

- Java 8 ou superior instalado.
- Maven ou Gradle para gerenciar dependências (mostraremos o trecho Maven).
- Biblioteca Aspose.HTML for Java (você pode obter uma avaliação gratuita no site da Aspose).
- Um arquivo MHTML que você deseja transformar em PDF (o exemplo usa `report.mhtml`).

> **Dica profissional:** Mantenha seu MHTML e o PDF de saída na mesma pasta durante os testes; caminhos relativos mantêm tudo organizado.

---

## Etapa 1 – Adicionar Aspose.HTML ao seu projeto

Se você estiver usando Maven, cole o seguinte no seu `pom.xml`. A versão mostrada é a mais recente em março de 2026; verifique o repositório da Aspose para lançamentos mais novos.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

Para Gradle, o equivalente é:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

Depois que a dependência for resolvida, você estará pronto para importar as classes que precisaremos.

## Etapa 2 – Criar opções de conversão e definir o modo de incorporação

O núcleo de **como incorporar imagens** está em `PdfConversionOptions`. Por padrão, Aspose incorpora *todos* os recursos (fonts, CSS, imagens). Vamos mudar isso para `EMBED_IMAGES_ONLY`.

```java
// Step 2: Prepare conversion options – embed only images
PdfConversionOptions options = new PdfConversionOptions();
options.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);
```

Por que isso importa? Imagine um relatório corporativo que referencia uma fonte corporativa armazenada em um compartilhamento de rede. Incorporar essa fonte inflaciona o PDF em centenas de kilobytes, mesmo que o visualizador possa buscá‑la remotamente. Ao incorporar apenas as imagens, o PDF mantém a fidelidade visual necessária enquanto permanece leve.

## Etapa 3 – Executar a conversão

Agora chamamos `Converter.convert`, passando o caminho do MHTML de origem, o caminho do PDF de destino e as opções que acabamos de configurar.

```java
// Step 3: Convert MHTML to PDF using the options above
String sourcePath = "YOUR_DIRECTORY/report.mhtml";
String targetPath = "YOUR_DIRECTORY/report.pdf";

Converter.convert(sourcePath, targetPath, options);
```

Se tudo estiver configurado corretamente, você verá um `report.pdf` aparecer ao lado do seu arquivo MHTML. Abra‑lo — cada imagem do relatório original deve estar presente, enquanto fontes e CSS permanecem como referências externas.

## Etapa 4 – Verificar a redução do tamanho do PDF

Uma verificação rápida ajuda a confirmar que você realmente **reduziu o tamanho do PDF**. Compare o tamanho do arquivo antes e depois de mudar o modo de incorporação:

```java
File before = new File("YOUR_DIRECTORY/report_full.pdf"); // generated with default settings
File after  = new File(targetPath); // our image‑only PDF

System.out.println("Full embed size: " + before.length() / 1024 + " KB");
System.out.println("Images‑only size: " + after.length() / 1024 + " KB");
```

Na maioria dos casos, você verá uma queda de 30‑70 % dependendo de quantas fontes ou arquivos CSS foram originalmente incorporados. Isso representa uma vitória considerável para quem distribui PDFs pela web ou os armazena em um bucket na nuvem.

## Etapa 5 – Exemplo completo e executável

Abaixo está a classe Java completa que você pode copiar para sua IDE. Substitua `YOUR_DIRECTORY` pelo caminho real da pasta onde o `report.mhtml` está localizado.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.converters.ResourceEmbeddingMode;

import java.io.File;

public class MhtmlToPdf {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define source and destination ----------
        String sourcePath = "YOUR_DIRECTORY/report.mhtml";
        String targetPath = "YOUR_DIRECTORY/report.pdf";

        // ---------- Step 2: Set conversion options (embed only images) ----------
        PdfConversionOptions conversionOptions = new PdfConversionOptions();
        conversionOptions.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);

        // ---------- Step 3: Run the conversion ----------
        Converter.convert(sourcePath, targetPath, conversionOptions);
        System.out.println("Conversion complete! PDF saved to: " + targetPath);

        // ---------- Step 4: (Optional) Show size reduction ----------
        File outputPdf = new File(targetPath);
        System.out.println("Resulting PDF size: " + outputPdf.length() / 1024 + " KB");
    }
}
```

**Saída esperada** (no console):

```
Conversion complete! PDF saved to: YOUR_DIRECTORY/report.pdf
Resulting PDF size: 842 KB
```

Abra `report.pdf` em qualquer visualizador; você deverá ver todas as imagens originais renderizadas corretamente. Se notar imagens ausentes, verifique se as URLs das imagens no MHTML são absolutas ou se os arquivos são acessíveis a partir da máquina de conversão.

## Perguntas comuns e tratamento de casos extremos

### E se eu *precisar* incorporar fontes?

Mude `ResourceEmbeddingMode` para `EMBED_ALL` ou `EMBED_FONTS_ONLY`. O enum oferece quatro opções:

| Modo                     | O que é incorporado |
|--------------------------|---------------------|
| `EMBED_ALL`              | Imagens, fontes, CSS |
| `EMBED_IMAGES_ONLY`      | Apenas imagens (nosso padrão) |
| `EMBED_FONTS_ONLY`       | Apenas fontes |
| `EMBED_NONE`             | Nada (apenas referências externas) |

### Meu MHTML contém CSS externo que afeta o layout — o PDF ficará quebrado?

Como não estamos incorporando CSS, o conversor ainda o baixará durante a conversão. Se o CSS estiver hospedado em uma intranet que o servidor de conversão não conseguir alcançar, o layout pode voltar aos padrões. Nesses casos, incorpore o CSS (`EMBED_ALL`) ou copie a folha de estilos localmente e ajuste o MHTML para apontar para o arquivo local.

### Posso processar em lote uma pasta de arquivos MHTML?

Com certeza. Envolva a lógica de conversão em um loop que itere sobre `File.listFiles()` e altere o nome do arquivo de destino conforme necessário. Apenas lembre‑se de reutilizar uma única instância de `PdfConversionOptions` para melhorar o desempenho.

### E quanto ao consumo de memória para documentos enormes?

O Aspose.HTML faz streaming do conteúdo, portanto o uso de memória permanece modesto. Contudo, imagens muito grandes ainda podem causar picos. Se você encontrar `OutOfMemoryError`, considere reduzir a resolução das imagens antes de incorporá‑las — a Aspose oferece `ImageConversionOptions` para isso, mas esse é um tópico para outro tutorial.

## Conclusão

Agora você sabe **como incorporar imagens** ao converter MHTML para PDF com Aspose.HTML, e viu por que essa pequena configuração pode **reduzir drasticamente o tamanho do arquivo PDF**. O exemplo Java completo, pronto para copiar e colar, demonstra todo o fluxo — desde a adição da dependência Maven até a impressão do tamanho final do arquivo.

Daqui você pode:

- Experimentar `EMBED_FONTS_ONLY` se seus PDFs precisarem ser completamente autossuficientes.
- Automatizar conversões em lote para uma pasta inteira de relatórios.
- Combinar esta técnica com as APIs de otimização de PDF da Aspose para arquivos ainda menores.

Seja construindo um serviço de relatórios, um pipeline de e‑mail‑para‑PDF, ou apenas organizando páginas da web arquivadas, controlar o que é incorporado é uma alavanca crucial para desempenho e custo. Experimente, ajuste as opções e mantenha seus PDFs o mais leves possível.

*Feliz codificação!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}