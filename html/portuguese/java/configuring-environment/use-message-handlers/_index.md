---
date: 2026-02-10
description: Aprenda a usar o Aspose para lidar com links quebrados em Java, converter
  HTML em PNG e carregar documentos HTML em Java com o Aspose.HTML para Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Converter HTML para PNG com manipuladores de mensagens Aspose.HTML em Java
url: /pt/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter HTML para PNG com Manipuladores de Mensagens Aspose.HTML em Java

## Introdução
Neste tutorial você descobrirá **como converter HTML para PNG** lidando elegantemente com recursos ausentes usando Aspose.HTML para Java. Vamos percorrer a criação de uma página HTML mínima que aponta para uma imagem inexistente, conectar um **manipulador de mensagens personalizado** para **interceptar solicitações de rede**, configurar o **serviço de rede**, carregar o documento e, finalmente, executar a **conversão de HTML para imagem**. Ao final, você terá um padrão sólido tanto para **handle broken links java** quanto para a geração de PNGs de alta qualidade — perfeito para relatórios, miniaturas ou pré‑visualizações de e‑mail.

## Respostas Rápidas
- **O que faz um manipulador de mensagens?** Ele intercepta operações de rede (como solicitações de imagens) e permite reagir a códigos de status como 404.  
- **O Aspose.HTML pode converter HTML para PNG?** Sim — `Converter.convertHTML` realiza a conversão em uma única chamada.  
- **Preciso de licença para este exemplo?** Uma licença temporária remove os limites de avaliação; uma licença permanente é necessária para uso em produção.  
- **Qual versão do Java funciona?** Qualquer JDK 8+ (o exemplo roda no JDK 11).  
- **Posso configurar o serviço de rede?** Absolutamente — use `configuration.getService(INetworkService.class)` para adicionar seu manipulador.

## Pré‑requisitos
Antes de mergulharmos, certifique‑se de que você tem o seguinte pronto:

1. **Java Development Kit (JDK)** – faça o download no [site da Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – obtenha a biblioteca na [página de releases da Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse ou NetBeans funcionam bem.  
4. **Conhecimento básico de Java** – você deve estar confortável com classes, try‑with‑resources e tratamento de exceções.  
5. **Licença Temporária** – se estiver em avaliação, adquira uma [licença temporária](https://purchase.aspose.com/temporary-license/) para evitar marcas d’água.

## Importar Pacotes
Primeiro, importe a classe Java I/O que usaremos para manipular arquivos. As demais classes da Aspose são referenciadas com nomes totalmente qualificados mais adiante, mantendo a lista de imports enxuta.

```java
import java.io.IOException;
```

## Etapa 1: Preparar o Código HTML
Criamos um trecho HTML mínimo que deliberadamente referencia uma imagem ausente. Isso acionará nosso manipulador quando o motor tentar buscar o recurso.

```java
String code = "<img src='missing.jpg'>";
```

## Etapa 2: Gravar o Código HTML em um Arquivo
Em seguida, persistimos o trecho em *document.html*. Usar um bloco try‑with‑resources garante que o `FileWriter` seja fechado corretamente.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Etapa 3: Escrever um Manipulador de Mensagens Personalizado
Agora construímos um **manipulador de mensagens personalizado** que verifica o status HTTP de cada solicitação de rede. Se a resposta não for `200`, registramos um aviso amigável. Observe a chamada a `invoke(context);` ao final — ela encaminha a solicitação para o próximo manipulador na cadeia, evitando recursão.

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

## Etapa 4: Configurar o Serviço de Rede
Para que o Aspose.HTML reconheça nosso manipulador, recuperamos o **serviço de rede** de uma instância `Configuration` e adicionamos o manipulador à sua coleção. Esta é a etapa onde **configuramos o serviço de rede** para comportamento personalizado.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Etapa 5: Carregar o Documento HTML
Com a configuração pronta, carregamos *document.html*. O motor agora usa nosso serviço de rede, de modo que a solicitação da imagem ausente é interceptada pelo manipulador que acabamos de adicionar.

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

## Etapa 6: Converter HTML para PNG
Aqui está o coração do processo de **conversão de HTML para imagem**. O método `Converter.convertHTML` recebe o `HTMLDocument` carregado, opções opcionais `ImageSaveOptions` (onde você pode ajustar DPI ou qualidade) e o nome do arquivo de saída.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Etapa 7: Liberar Recursos
Boa prática em Java determina que liberemos todos os recursos nativos. O bloco `finally` garante que o `Configuration` seja descartado mesmo que uma exceção seja propagada.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Por que Usar Manipuladores de Mensagens?
Manipuladores de mensagens dão a você **controle granular** sobre cada solicitação de rede — seja uma imagem, CSS, JavaScript ou arquivo de fonte. Em vez de deixar a biblioteca falhar silenciosamente, você pode registrar ativos ausentes, fornecer conteúdo alternativo ou até mesmo tentar a solicitação novamente. Isso torna seu pipeline de processamento HTML **robusto**, **pronto para produção** e mais fácil de depurar.

## Problemas Comuns e Soluções
- **Recursão do manipulador** – Chame `invoke(context);` apenas uma vez para evitar loops infinitos.  
- **Licença ausente** – Sem uma licença válida, o PNG de saída conterá uma marca d’água.  
- **Caminhos de arquivo incorretos** – Use caminhos absolutos ou configure o diretório de trabalho corretamente ao carregar `document.html`.  
- **Tipos de recurso não suportados** – Certifique‑se de que o recurso que você deseja interceptar (imagem, CSS, etc.) está realmente sendo solicitado pelo motor HTML.

## Perguntas Frequentes

**P: Posso encadear vários manipuladores de mensagens?**  
R: Sim, você pode adicionar vários manipuladores à coleção `network.getMessageHandlers()`; eles serão executados na ordem em que foram adicionados.

**P: O manipulador funciona para recursos CSS ou scripts também?**  
R: Absolutamente — qualquer solicitação de rede feita pelo motor HTML (imagens, CSS, JS, fontes) passa pelo manipulador.

**P: Como altero a solicitação HTTP antes de enviá‑la?**  
R: Implemente um manipulador que modifique `context.getRequest()` antes de chamar `invoke(context)`.

**P: Existe uma forma de suprimir o aviso para URLs específicas?**  
R: Dentro do manipulador, inspecione `context.getRequest().getRequestUri()` e condicionalmente ignore o registro.

**P: Qual versão do Aspose.HTML é necessária para essas APIs?**  
R: O código funciona com Aspose.HTML for Java 22.10 ou posterior.

## Conclusão
Agora você tem um exemplo completo, de ponta a ponta, de **como converter HTML para PNG** usando um **manipulador de mensagens personalizado** para **interceptar solicitações de rede** e **lidar com broken links java**. Ao configurar o serviço de rede, carregar o documento e invocar o conversor, você pode gerar miniaturas PNG ou capturas de tela de página inteira de forma confiável em qualquer aplicação Java.

---

**Última atualização:** 2026-02-10  
**Testado com:** Aspose.HTML for Java 24.11  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}