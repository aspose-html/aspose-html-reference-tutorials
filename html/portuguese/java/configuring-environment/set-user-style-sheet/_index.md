---
date: 2025-12-05
description: Aprenda como criar PDF a partir de HTML definindo uma folha de estilo
  personalizada do usuário no Aspose.HTML para Java e converta HTML para PDF facilmente
  com o Serviço de Agente de Usuário.
linktitle: Set User Style Sheet in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Criar PDF a partir de HTML – Definir folha de estilo do usuário no Aspose.HTML
  para Java
url: /pt/java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF a partir de HTML – Definir Folha de Estilo do Usuário no Aspose.HTML para Java

## Introdução
Neste tutorial você aprenderá como **criar PDF a partir de HTML** usando Aspose.HTML para Java enquanto aplica uma folha de estilo personalizada do usuário.  
Já se pegou querendo ajustar a aparência dos seus documentos HTML com um estilo único? Imagine que você está criando uma página web e precisa que os títulos se destaquem com uma cor específica ou que os parágrafos tenham um visual consistente em todos os dispositivos. É aí que uma *folha de estilo do usuário* e o **User Agent Service** entram em ação. Vamos percorrer cada passo — desde escrever um arquivo HTML simples, configurar o agente de usuário, até finalmente **converter HTML para PDF** — para que você veja o resultado instantaneamente.

## Respostas Rápidas
- **O que significa “criar PDF a partir de HTML”?** Significa renderizar um documento HTML (com CSS, imagens, fontes, etc.) e salvar a saída visual como um arquivo PDF.  
- **Qual componente Aspose é necessário?** A biblioteca Aspose.HTML para Java fornece o motor de conversão e o User Agent Service.  
- **Preciso de licença para testes?** Uma avaliação gratuita funciona para desenvolvimento; uma licença comercial é necessária para produção.  
- **Posso usar um arquivo CSS externo?** Sim – você pode vincular folhas de estilo externas como em um navegador comum.  
- **Quanto tempo leva a conversão?** Para um documento simples como o deste guia, a conversão termina em menos de um segundo.

## Pré-requisitos
Antes de mergulharmos no código, certifique‑se de que você tem o seguinte:

1. **Aspose.HTML para Java** – faça o download do JAR mais recente na [página de releases da Aspose](https://releases.aspose.com/html/java/).  
2. **Java Development Kit (JDK) 8+** – verifique se `java -version` exibe 8 ou superior.  
3. **IDE** – IntelliJ IDEA, Eclipse ou NetBeans funcionam bem.  
4. **Conhecimento básico de HTML/CSS** – útil, mas não obrigatório.

## Importar Pacotes
Para começar, importe as classes Java essenciais. A única importação explícita necessária para este exemplo é `java.io.IOException`; as classes Aspose são referenciadas com nomes totalmente qualificados mais adiante.

```java
import java.io.IOException;
```

## Etapa 1: Criar um Documento HTML Simples
Primeiro, vamos escrever um arquivo HTML mínimo (`document.html`) que servirá como fonte para a conversão em PDF.

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Dica profissional:** Mantenha o arquivo HTML no mesmo diretório do seu código Java para evitar problemas relacionados a caminhos.

## Etapa 2: Configurar o Aspose.HTML
Crie um objeto `Configuration`. Esse objeto atua como um contêiner para todos os serviços (incluindo o User Agent Service) que você usará posteriormente.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Etapa 3: Acessar o User Agent Service  
O **User Agent Service** permite injetar uma folha de estilo personalizada, definir o conjunto de caracteres padrão e controlar outras opções de renderização.

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## Etapa 4: Definir e Aplicar a Folha de Estilo do Usuário  
Agora fornecemos as regras CSS que estilizarão o HTML quando ele for renderizado. É aqui que **usamos o user agent service** para definir a folha de estilo.

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **Por que isso importa:** Ao aplicar uma folha de estilo no nível do agente de usuário, você garante que os estilos sejam respeitados mesmo que o HTML original não faça referência a um arquivo CSS.

## Etapa 5: Carregar o Documento HTML com a Configuração Personalizada  
Passe tanto o caminho do arquivo quanto a instância `Configuration` ao construtor `HTMLDocument`. Isso vincula a folha de estilo do usuário ao documento.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## Etapa 6: Converter HTML para PDF  
Com o documento totalmente estilizado, invoque o método estático `convertHTML` para **converter HTML para PDF**. O objeto `PdfSaveOptions` permite ajustar finamente a saída (por exemplo, tamanho da página, compressão).

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **Resultado:** `user-agent-stylesheet_out.pdf` conterá o título em marrom e o parágrafo com fundo GhostWhite, exatamente como definido na folha de estilo.

## Etapa 7: Limpar Recursos  
Sempre libere os objetos Aspose para liberar memória nativa.

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

## Problemas Comuns & Soluções
| Problema | Causa | Solução |
|----------|-------|---------|
| **Saída PDF em branco** | Nenhuma folha de estilo aplicada ou documento não carregado com a configuração. | Verifique se `configuration` é passado ao `HTMLDocument` e se `setUserStyleSheet` é chamado antes do carregamento. |
| **Aviso de propriedade CSS não suportada** | Aspose.HTML não suporta alguns recursos avançados de CSS. | Use apenas propriedades CSS listadas na documentação do Aspose.HTML ou recorra a estilos mais simples. |
| **FileNotFoundException** | Caminho incorreto para `document.html`. | Use um caminho absoluto ou coloque o arquivo HTML na raiz do projeto. |

## Perguntas Frequentes

**Q: Posso aplicar estilos diferentes para diferentes elementos HTML?**  
A: Absolutamente! Você pode definir quantas regras CSS precisar dentro da folha de estilo do usuário.

**Q: E se eu precisar mudar a folha de estilo dinamicamente?**  
A: Chame `setUserStyleSheet` novamente antes de criar uma nova instância de `HTMLDocument`; os novos estilos serão aplicados na próxima conversão.

**Q: É possível usar arquivos CSS externos com Aspose.HTML para Java?**  
A: Sim – você pode vincular uma folha de estilo externa no HTML ou carregar seu conteúdo e passá‑lo para `setUserStyleSheet`.

**Q: Como o Aspose.HTML lida com propriedades CSS não suportadas?**  
A: Propriedades não suportadas são ignoradas, permitindo que o restante da folha de estilo seja renderizado sem erros.

**Q: Posso converter HTML para formatos além de PDF?**  
A: Sim, o Aspose.HTML suporta conversão para XPS, TIFF, PNG, JPEG e outros usando a classe `SaveOptions` apropriada.

## Conclusão
Você acabou de ver como **criar PDF a partir de HTML** definindo uma folha de estilo personalizada do usuário com Aspose.HTML para Java. Esse fluxo de trabalho oferece controle total sobre a aparência visual do PDF gerado, tornando‑o ideal para geração automática de relatórios, criação de faturas ou qualquer cenário onde a consistência de estilo seja crucial. Sinta‑se à vontade para experimentar CSS mais complexo, fontes externas ou formatos de conversão adicionais para expandir esta base.

---

**Last Updated:** 2025-12-05  
**Tested With:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}