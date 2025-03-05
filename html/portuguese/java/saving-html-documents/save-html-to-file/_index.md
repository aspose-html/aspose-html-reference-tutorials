---
title: Salvar documento HTML em arquivo no Aspose.HTML para Java
linktitle: Salvar documento HTML em arquivo no Aspose.HTML para Java
second_title: Processamento HTML Java com Aspose.HTML
description: Aprenda a salvar um documento HTML em um arquivo usando o Aspose.HTML para Java, perfeito para manipular vários recursos vinculados com facilidade.
type: docs
weight: 11
url: /pt/java/saving-html-documents/save-html-to-file/
---
## Introdução
Neste tutorial, exploraremos como salvar um documento HTML em um arquivo enquanto gerencia recursos vinculados. Isso é particularmente útil quando você está trabalhando em projetos que envolvem vários arquivos HTML — pense nisso como uma página da web que faz referência a outras páginas da web. Ao final deste guia, você estará equipado para usar o Aspose.HTML para Java para gerenciar seus documentos HTML de forma flexível e eficiente.
## Pré-requisitos
Antes de começar, há algumas coisas que você precisa ter em mãos:
1.  Java Development Kit (JDK): Certifique-se de ter o JDK instalado em sua máquina. A versão 8 ou superior é recomendada. Você pode baixá-lo[aqui](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html).
2.  Biblioteca Aspose.HTML para Java: Você precisa baixar a biblioteca Aspose.HTML. Você pode obtê-la na página de lançamentos[aqui](https://releases.aspose.com/html/java/).
3. IDE ou Editor de Texto: Você pode usar qualquer IDE ou editor de texto que preferir para desenvolvimento Java. IntelliJ IDEA, Eclipse, ou até mesmo um editor simples como o Notepad++ vai servir bem.
4. Conhecimento básico de Java: Familiaridade com os conceitos básicos de programação Java será útil. Você precisará entender como trabalhar com arquivos e lidar com exceções.
Com tudo configurado, vamos para a parte divertida: a codificação!
## Pacotes de importação
Para usar Aspose.HTML, você precisa importar os pacotes necessários para seu projeto Java. Veja como você pode fazer isso:
### Incluir dependências Aspose
 Se você estiver usando Maven, você pode adicionar a dependência Aspose.HTML em seu`pom.xml` arquivo. Aqui está a sintaxe do Maven:
```xml
<dependency>
   <groupId>com.aspose</groupId>
   <artifactId>aspose-html</artifactId>
   <version>{latest_version}</version>
</dependency>
```
 Certifique-se de substituir`{latest_version}` com o número da versão real disponível na página de downloads do Aspose.
### Importar instruções em seu arquivo Java
Você também precisará incluir as instruções de importação relevantes no início do seu arquivo Java:
```java
import java.io.IOException;
```

## Etapa 1: Preparando o caminho de saída
Primeiro, você precisa especificar onde seu documento será salvo. Você pode fazer isso definindo um caminho de arquivo em seu código.
```java
String documentPath = "save-with-linked-file.html";
```
 Aqui, estamos nomeando nosso documento HTML principal`save-with-linked-file.html`.
## Etapa 2: Criando o arquivo HTML principal
Em seguida, você vai querer criar seu arquivo HTML principal, que será vinculado a outro documento. É aqui que escrevemos o conteúdo HTML.
```java
java.nio.file.Files.write(java.nio.file.Paths.get(documentPath), "<p>Hello World!</p><a href='linked.html'>linked file</a>".getBytes());
```
 Nesta etapa, estamos criando uma estrutura HTML simples com um parágrafo e um link para outro documento HTML`linked.html`.
## Etapa 3: Criando o arquivo HTML vinculado
Agora, vamos também criar o arquivo HTML vinculado que mencionamos na etapa anterior.
```java
java.nio.file.Files.write(java.nio.file.Paths.get("linked.html"), "<p>Hello linked file!</p>".getBytes());
```
Isso cria um arquivo HTML que será exibido quando você clicar no link do seu documento principal.
## Etapa 4: Carregando o documento HTML na memória
Depois que ambos os arquivos forem criados, o próximo passo é carregar o documento HTML principal na memória para trabalhar com ele programaticamente.
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(documentPath);
```
 Com este comando, estamos inicializando um`HTMLDocument` objeto que você pode manipular nas próximas etapas.
## Etapa 5: Criando opções de salvamento
Antes de salvar seu documento, é crucial configurar como ele deve ser salvo. Isso envolve criar uma instância de`HTMLSaveOptions`.
```java
com.aspose.html.saving.HTMLSaveOptions options = new com.aspose.html.saving.HTMLSaveOptions();
```
## Etapa 6: Configurando opções de tratamento de recursos
Esta parte é crítica se você tiver arquivos vinculados. Você deve decidir se os inclui na sua saída ou os exclui. 
```java
options.getResourceHandlingOptions().setMaxHandlingDepth(1);
```
 Definindo o`MaxHandlingDepth` para`1` garante que o documento vinculado não seja salvo junto com seu documento principal. Altere esse valor para incluir arquivos HTML vinculados conforme necessário.
## Etapa 7: Salvando o documento
Por fim, é hora de salvar seu documento usando as opções configuradas.
```java
document.save("save-with-linked-file_out.html", options);
```
 Aqui, salvamos o documento principal como`save-with-linked-file_out.html`, aplicando nossas opções especificadas ao processo de salvamento.
## Conclusão
aí está! Agora você pode salvar um documento HTML com recursos vinculados usando Aspose.HTML para Java. Esta API não é apenas poderosa, mas também fácil de integrar em seus projetos, tornando o manuseio de HTML uma brisa. Seja você um desenvolvedor iniciante ou experiente, o Aspose.HTML para Java tem recursos que podem melhorar significativamente seu fluxo de trabalho.
## Perguntas frequentes
### O que é Aspose.HTML?  
Aspose.HTML é uma API poderosa usada para manipulação, conversão e renderização de HTML. Ela permite que desenvolvedores trabalhem perfeitamente com documentos HTML.
### Posso incluir imagens e outros recursos nos meus arquivos HTML?  
Sim! O Aspose.HTML suporta vários tipos de recursos, incluindo imagens, estilos e scripts, permitindo um manuseio abrangente de documentos.
### Existe uma avaliação gratuita disponível para o Aspose.HTML?  
 Absolutamente! Você pode obter uma avaliação gratuita do Aspose.HTML[aqui](https://releases.aspose.com/).
### Como obtenho suporte técnico para o Aspose.HTML?  
 Você pode visitar o fórum de suporte do Aspose[aqui](https://forum.aspose.com/c/html/29) para quaisquer dúvidas ou ajuda que você possa precisar.
### Posso usar o Aspose.HTML para projetos comerciais?  
Sim, o Aspose.HTML pode ser usado em projetos comerciais, mas você precisará comprar uma licença. Você pode encontrar opções de licenciamento[aqui](https://purchase.aspose.com/buy).