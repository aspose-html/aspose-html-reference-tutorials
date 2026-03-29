---
date: 2026-03-29
description: Aprenda a usar o Aspose.HTML para Java para especificar opções de salvamento
  XPS, converter EPUB para XPS e lidar com licenciamento.
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: Como usar as opções de salvamento de HTML da Aspose para EPUB em XPS
url: /pt/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar as Opções de Salvamento do Aspose HTML para EPUB em XPS

Neste guia, mostraremos **como usar Aspose** HTML Save Options para converter um documento EPUB em XPS com controle total sobre as dimensões da página, cor de fundo e considerações de licenciamento. Seja você está construindo um pipeline de processamento em lote ou uma ferramenta de conversão única, estas etapas ajudarão a obter resultados confiáveis rapidamente.

## Respostas Rápidas
- **O que o Aspose HTML Save Options faz?** Ele permite personalizar o tamanho da página, a cor de fundo e outras configurações de renderização ao salvar em formatos como XPS.  
- **Qual biblioteca é necessária?** Aspose.HTML for Java (latest version).  
- **Preciso de uma licença?** Um teste gratuito funciona para avaliação; uma licença comercial é necessária para produção.  
- **Posso alterar as dimensões da página?** Sim – você pode definir qualquer largura e altura via `PageSetup`.  
- **A conversão é rápida?** Para arquivos EPUB típicos, a conversão é concluída em segundos em uma JVM moderna.

## O que significa “how to use aspose” neste contexto?
A expressão **how to use Aspose** refere‑se aos passos práticos para aproveitar a biblioteca Aspose.HTML para manipular e converter documentos baseados na web. Neste tutorial, focamos nas **aspose html save options** que permitem ajustar finamente a saída ao **converter EPUB para XPS**.

## Por que usar Aspose.HTML para Java para converter EPUB em XPS?
- **Alta fidelidade** – preserva layouts complexos, fontes e gráficos vetoriais.  
- **Controle programático** – automatiza conversões em lote dentro de aplicações Java.  
- **Sem dependências externas** – biblioteca Java pura, sem componentes nativos.  
- **Saída personalizável** – graças às opções de salvamento, você pode adaptar o XPS às suas necessidades exatas, como **especificar dimensões da página** ou definir um plano de fundo personalizado.  

## Pré-requisitos

Antes de mergulharmos no código, certifique‑se de que você tem o seguinte:

1. **Ambiente de Desenvolvimento Java** – JDK 8 ou superior instalado.  
2. **Biblioteca Aspose.HTML para Java** – faça o download a partir do [download link](https://releases.aspose.com/html/java/).  
3. **Arquivo EPUB** – o EPUB de origem que você deseja **converter EPUB para XPS**.  

Ter esses itens prontos permitirá que você siga as etapas sem interrupções.

## Importar Pacotes

Primeiro, importe as classes necessárias. Coloque as importações no início do seu arquivo fonte Java:

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

Essas importações dão acesso ao motor de conversão e às **Aspose HTML Save Options** necessárias para ajuste fino.

## Abrir o Arquivo EPUB

Em seguida, abra o EPUB que deseja converter. O helper `Resources.input` carrega um arquivo da pasta de recursos de demonstração:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

Usar um bloco try‑with‑resources garante que o stream seja fechado automaticamente.

## Criar XPS Save Options (Configurar Tamanho da Página e Plano de Fundo)

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

- **Tamanho da página** – definido como 3000 × 1000 pixels neste exemplo; ajuste para corresponder ao tamanho de papel desejado ou use `Length.fromInches` para **especificar dimensões da página** em polegadas.  
- **Cor de fundo** – `AliceBlue` demonstra como mudar o fundo da tela; você pode escolher qualquer `Color`.  

Essas configurações fazem parte das **aspose html save options** que afetam o documento XPS final.

## Converter EPUB para XPS

Finalmente, invoque o conversor com o stream, as opções configuradas e um caminho de saída:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

Quando esta linha for executada, o Aspose.HTML lê o EPUB, aplica a configuração de página e a cor de fundo que você definiu, e grava um arquivo XPS totalmente compatível.

## Problemas Comuns e Dicas
- **Dimensões de página incorretas** – certifique‑se de que as dimensões estejam expressas em pixels (ou use `Length.fromInches`).  
- **Fontes ausentes** – incorpore as fontes necessárias no EPUB ou instale‑as no host JVM para evitar fallback.  
- **Arquivos grandes** – para EPUBs muito grandes, aumente o heap da JVM (`-Xmx`) para evitar `OutOfMemoryError`.  
- **Licenciamento do Aspose HTML** – garanta que uma licença válida esteja carregada antes da conversão; caso contrário, a marca d'água de avaliação aparecerá.

## Conclusão

Ao aproveitar as **Aspose HTML Save Options**, você obtém controle preciso sobre como um EPUB é renderizado para XPS. As etapas acima mostram como **converter EPUB**, definir **dimensões da página**, mudar o plano de fundo e executar a conversão com apenas algumas linhas de código Java. Integre este padrão em seus pipelines de processamento em lote para automatizar tarefas de publicação de forma eficiente.

## Perguntas Frequentes

**Q: O que é Aspose.HTML para Java?**  
A: É uma biblioteca Java que permite aos desenvolvedores criar, editar, renderizar e converter HTML, EPUB e outros documentos baseados na web sem precisar de um navegador.

**Q: Posso usar isso em um projeto comercial?**  
A: Sim. Para uso em produção você precisa de uma licença válida. Você pode comprar uma na [purchase page](https://purchase.aspose.com/buy).

**Q: Existe uma versão de avaliação gratuita disponível?**  
A: Absolutamente. Baixe uma versão de avaliação a partir de [aqui](https://releases.aspose.com/).

**Q: Onde posso obter suporte?**  
A: Suporte da comunidade e assistência oficial estão disponíveis nos fóruns da Aspose em [https://forum.aspose.com/](https://forum.aspose.com/).

**Q: Quais são os requisitos do sistema?**  
A: Um Java Development Kit (JDK) 8+ e um sistema operacional suportado pelo runtime da Aspose. Certifique‑se de que seu ambiente atenda aos pré‑requisitos listados anteriormente.

---

**Última atualização:** 2026-03-29  
**Testado com:** Aspose.HTML for Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}