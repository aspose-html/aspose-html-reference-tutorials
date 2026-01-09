---
date: 2026-01-09
description: Aprenda a usar o Aspose.HTML para Java para especificar opções de salvamento
  XPS e converter EPUB para XPS de forma eficiente.
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: Especificando opções de salvamento HTML da Aspose para conversão de EPUB para
  XPS
url: /pt/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Especificando Aspose HTML Save Options para EPUB para XPS

Converter um documento EPUB para XPS pode ser uma etapa útil em um fluxo de trabalho de publicação, e as **Aspose HTML Save Options** oferecem controle detalhado sobre a saída. Neste tutorial vamos percorrer os passos exatos necessários para configurar essas opções de salvamento com Aspose.HTML para Java e produzir um arquivo XPS de alta qualidade.

## Respostas Rápidas
- **O que as Aspose HTML Save Options fazem?** Permitem personalizar o tamanho da página, cor de fundo e outras configurações de renderização ao salvar em formatos como XPS.  
- **Qual biblioteca é necessária?** Aspose.HTML para Java (versão mais recente).  
- **Preciso de licença?** Uma avaliação gratuita funciona para testes; uma licença comercial é necessária para produção.  
- **Posso alterar as dimensões da página?** Sim – você pode definir qualquer largura e altura via `PageSetup`.  
- **A conversão é rápida?** Para arquivos EPUB típicos, a conversão termina em segundos em uma JVM moderna.

## O que são Aspose HTML Save Options?
Aspose HTML Save Options são um conjunto de propriedades que controlam como HTML, EPUB ou outros documentos baseados na web são renderizados e salvos para um formato de destino, como XPS, PDF ou arquivos de imagem. Elas permitem definir layout de página, cores de fundo, margens e mais, garantindo que o arquivo resultante atenda aos requisitos de design.

## Por que usar Aspose.HTML para Java para converter EPUB para XPS?
- **Alta fidelidade** – preserva layouts complexos, fontes e gráficos vetoriais.  
- **Controle programático** – automatize conversões em lote dentro de aplicações Java.  
- **Sem dependências externas** – biblioteca pura Java, sem componentes nativos.  
- **Saída personalizável** – graças às opções de salvamento, você pode adaptar o XPS exatamente às suas necessidades.

## Pré‑requisitos

Antes de mergulharmos no código, certifique‑se de que você tem o seguinte:

1. **Ambiente de Desenvolvimento Java** – JDK 8 ou superior instalado.  
2. **Biblioteca Aspose.HTML para Java** – faça o download a partir do [download link](https://releases.aspose.com/html/java/).  
3. **Arquivo EPUB** – o EPUB de origem que você deseja converter.  

Ter esses itens prontos permitirá que você siga os passos sem interrupções.

## Importar Pacotes

Primeiro, importe as classes necessárias. Coloque as importações no topo do seu arquivo fonte Java:

```java
import java.io.FileInputStream;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import com.aspose.html.system.io.resources.Resources;
```

Essas importações dão acesso ao motor de conversão e às **Aspose HTML Save Options** necessárias para o ajuste fino.

## Abrir o Arquivo EPUB

Em seguida, abra o EPUB que você deseja converter. O helper `Resources.input` carrega um arquivo da pasta de recursos de demonstração:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

Usar um bloco *try‑with‑resources* garante que o stream seja fechado automaticamente.

## Criar XPS Save Options (Configurar Tamanho da Página e Fundo)

Agora criamos uma instância de `XpsSaveOptions` e a personalizamos. É aqui que as **save options** realmente brilham:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **Tamanho da página** – definido como 3000 × 1000 pixels neste exemplo; ajuste para corresponder ao tamanho de papel desejado.  
- **Cor de fundo** – `AliceBlue` demonstra como mudar o fundo da tela; você pode escolher qualquer `Color`.  

Essas configurações fazem parte das **Aspose HTML Save Options** que afetam o documento XPS final.

## Converter EPUB para XPS

Finalmente, invoque o conversor com o stream, as opções configuradas e um caminho de saída:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

Quando esta linha for executada, Aspose.HTML lê o EPUB, aplica a configuração de página e a cor de fundo que você definiu, e grava um arquivo XPS totalmente compatível.

## Problemas Comuns & Dicas

- **Dimensões de página incorretas** – certifique‑se de que as dimensões estejam expressas em pixels (ou use `Length.fromInches`).  
- **Fontes ausentes** – incorpore as fontes necessárias no EPUB ou instale‑as na máquina que executa a JVM para evitar fallback.  
- **Arquivos grandes** – para EPUBs muito volumosos, aumente o heap da JVM (`-Xmx`) para prevenir `OutOfMemoryError`.  

## Conclusão

Ao aproveitar as **Aspose HTML Save Options**, você obtém controle preciso sobre como um EPUB é renderizado para XPS. Os passos acima mostram como definir tamanho de página, cor de fundo e realizar a conversão com apenas algumas linhas de código Java. Integre esse padrão em seus pipelines de processamento em lote para automatizar tarefas de publicação de forma eficiente.

## Perguntas Frequentes

**Q: O que é Aspose.HTML para Java?**  
A: É uma biblioteca Java que permite a desenvolvedores criar, editar, renderizar e converter HTML, EPUB e outros documentos baseados na web sem precisar de um navegador.

**Q: Posso usar isso em um projeto comercial?**  
A: Sim. Para uso em produção você precisa de uma licença válida. Você pode adquirir uma na [página de compra](https://purchase.aspose.com/buy).

**Q: Existe uma versão de avaliação gratuita?**  
A: Absolutamente. Baixe a versão de avaliação a partir de [aqui](https://releases.aspose.com/).

**Q: Onde posso obter suporte?**  
A: Suporte da comunidade e assistência oficial estão disponíveis nos fóruns da Aspose em [https://forum.aspose.com/](https://forum.aspose.com/).

**Q: Quais são os requisitos de sistema?**  
A: Um Java Development Kit (JDK) 8+ e um sistema operacional suportado pelo runtime da Aspose. Certifique‑se de que seu ambiente atenda aos pré‑requisitos listados anteriormente.

---

**Última atualização:** 2026-01-09  
**Testado com:** Aspose.HTML para Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}