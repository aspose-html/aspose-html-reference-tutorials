---
date: 2025-12-10
description: Aprenda a usar o Aspose para lidar com links quebrados em Java, converter
  HTML em PNG e carregar documento HTML em Java com Aspose.HTML para Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Como usar manipuladores de mensagens Aspose.HTML em Java
url: /pt/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar Manipuladores de Mensagens do Aspose.HTML em Java

## Introdução
Neste tutorial, **how to use aspose** para lidar com recursos ausentes em HTML é demonstrado passo a passo. Criaremos um documento HTML simples que referencia uma imagem inexistente, anexaremos um manipulador de mensagens personalizado e mostraremos como **load html document java** enquanto tratamos elegantemente links quebrados. Ao final, você também verá como **convert html to png** usando Aspose.HTML, proporcionando uma visão completa da conversão de HTML para imagem em Java.

## Respostas Rápidas
- **Qual é o objetivo principal de um manipulador de mensagens?** Interceptar operações de rede e reagir a códigos de status, como recursos ausentes.  
- **O Aspose.HTML pode converter HTML para PNG?** Sim, usando `Converter.convertHTML` você pode realizar a conversão de html para imagem.  
- **Preciso de uma licença para este exemplo?** Uma licença temporária remove limites de avaliação; uma licença permanente é necessária para produção.  
- **Qual versão do Java é suportada?** Qualquer JDK 8+ (o tutorial usa JDK 11).  
- **É possível lidar com vários links quebrados?** Absolutamente – você pode encadear vários manipuladores para gerenciar diferentes cenários.

## Pré-requisitos
Antes de mergulharmos no guia passo a passo, certifique‑se de que você tem tudo o que precisa:
1. Java Development Kit (JDK): Certifique‑se de que o JDK está instalado no seu sistema. Você pode baixá‑lo no [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).
2. Aspose.HTML for Java: Você precisará ter o Aspose.HTML for Java instalado. Você pode baixá‑lo na [página de releases da Aspose](https://releases.aspose.com/html/java/).
3. IDE: Use sua IDE Java favorita, como IntelliJ IDEA, Eclipse ou NetBeans.
4. Conhecimento Básico de Java: Familiaridade com programação Java é essencial para seguir este tutorial de forma eficaz.
5. Licença Temporária: Se você estiver usando a versão de avaliação do Aspose.HTML, considere obter uma [licença temporária](https://purchase.aspose.com/temporary-license/) para evitar limitações durante o desenvolvimento.

## Importar Pacotes
Antes de começarmos, certifique‑se de que os pacotes necessários estejam importados no seu projeto Java. Abaixo estão as importações essenciais que você precisará:
```java
import java.io.IOException;
```
Essas importações lhe darão acesso às classes e métodos necessários para manipular operações de rede, criar documentos HTML e realizar a conversão de HTML‑para‑PNG.

## Etapa 1: Preparar o Código HTML
A primeira coisa que precisamos é um trecho HTML simples que referencia um arquivo de imagem. Deliberadamente referiremos uma imagem que não existe para acionar o mecanismo de tratamento de erros.
```java
String code = "<img src='missing.jpg'>";
```
Esse código cria uma tag `<img>` que aponta para `missing.jpg`. Como a imagem está ausente, o serviço de rede retornará um código de status diferente de 200, que nosso manipulador personalizado capturará.

## Etapa 2: Gravar o Código HTML em um Arquivo
Em seguida, precisamos persistir o trecho HTML para que o Aspose.HTML possa carregá‑lo como documento.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
Usando um `FileWriter` salvamos o HTML em **document.html**. Esse arquivo se torna a fonte para a etapa **load html document java** posterior.

## Etapa 3: Criar um Manipulador de Mensagens Personalizado
Agora vamos construir um manipulador de mensagens personalizado que reage quando a imagem não pode ser encontrada. O manipulador verifica o código de status HTTP e imprime uma mensagem amigável.
```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```
O método `invoke` examina `context.getResponse().getStatusCode()`. Se não for **200**, exibimos um aviso claro de que o arquivo está ausente. A chamada final `invoke(context);` passa o controle para o próximo manipulador na cadeia.

## Etapa 4: Configurar o Serviço de Rede
Para que o Aspose.HTML reconheça nosso manipulador, registramos ele no serviço de rede via a classe `Configuration`.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Aqui criamos uma instância de `Configuration`, recuperamos o `INetworkService` e adicionamos nosso manipulador personalizado à sua coleção. Isso garante que o manipulador seja executado durante qualquer requisição de rede, como o carregamento de imagens.

## Etapa 5: Carregar o Documento HTML
Com a configuração pronta, podemos agora carregar o arquivo HTML que criamos anteriormente. Esta etapa demonstra **load html document java** enquanto a imagem ausente aciona nosso manipulador.
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```
O construtor `HTMLDocument` recebe tanto o caminho do arquivo quanto a `configuration` personalizada. Quando o documento analisa a tag `<img>`, o serviço de rede tenta buscar `missing.jpg`, recebe um 404 e nosso manipulador imprime o aviso.

## Etapa 6: Converter HTML para PNG
Para ilustrar as capacidades mais amplas do Aspose.HTML, converteremos o documento carregado em uma imagem PNG. Este é um cenário clássico de **convert html to png**.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` recebe o `HTMLDocument`, opções opcionais `ImageSaveOptions` (onde você pode definir DPI, qualidade, etc.) e o nome do arquivo de saída. O resultado é uma imagem rasterizada do HTML renderizado.

## Etapa 7: Limpar Recursos
Gerenciamento adequado de recursos é essencial em qualquer aplicação Java. Dispensamos tanto a `Configuration` quanto o `HTMLDocument` para evitar vazamentos de memória.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Envolver a limpeza em um bloco `finally` garante a execução mesmo que uma exceção ocorra anteriormente.

## Por Que Usar Manipuladores de Mensagens?
Manipuladores de mensagens dão controle granular sobre operações de rede, como **handle broken links java**. Em vez de deixar a biblioteca falhar silenciosamente, você pode registrar, tentar novamente, substituir recursos ou fornecer conteúdo alternativo — tornando seu processamento HTML robusto e pronto para produção.

## Problemas Comuns e Soluções
- **Recursão do manipulador** – Certifique‑se de chamar `invoke(context);` apenas uma vez para evitar loops infinitos.  
- **Licença ausente** – Sem uma licença válida, a conversão pode gerar uma imagem com marca d'água.  
- **Erros de caminho de arquivo** – Use caminhos absolutos ou configure o diretório de trabalho corretamente ao carregar `document.html`.

## Perguntas Frequentes

**P: Posso encadear vários manipuladores de mensagens?**  
R: Sim, você pode adicionar vários manipuladores à coleção `network.getMessageHandlers()`; eles serão executados na ordem em que foram adicionados.

**P: O manipulador funciona para recursos CSS ou de script também?**  
R: Absolutamente—qualquer requisição de rede feita pelo motor HTML (imagens, CSS, JS, fontes) passa pelo manipulador.

**P: Como altero a requisição HTTP antes de enviá‑la?**  
R: Implemente um manipulador que modifique `context.getRequest()` antes de chamar `invoke(context)`.

**P: Existe uma forma de suprimir o aviso para URLs específicas?**  
R: Dentro do manipulador, inspecione `context.getRequest().getRequestUri()` e condicionalmente ignore o log.

**P: Qual versão do Aspose.HTML é necessária para essas APIs?**  
R: O código funciona com Aspose.HTML para Java 22.10 ou posterior.

## Conclusão
E aí está — um guia abrangente sobre **how to use aspose** manipuladores de mensagens em Java. Cobrimos a criação de um arquivo HTML, a ligação de um manipulador personalizado para **handle broken links java**, o carregamento do documento e a execução de **convert html to png**. Com esse padrão, você pode gerenciar recursos ausentes com confiança, aplicar políticas personalizadas e estender as capacidades de rede do Aspose.HTML em qualquer aplicação Java.

---

**Última atualização:** 2025-12-10  
**Testado com:** Aspose.HTML for Java 24.11  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}