---
category: general
date: 2026-04-19
description: Extraia HTML de MHTML rapidamente usando Java. Aprenda como converter
  MHTML para HTML, extrair o corpo do e‑mail, gravar a string em um arquivo e lidar
  com a conversão de MHT.
draft: false
keywords:
- extract html from mhtml
- convert mhtml to html
- extract email body
- write string to file
- convert mht to html
language: pt
og_description: Extrair HTML de MHTML em Java. Este guia mostra como converter MHTML
  para HTML, extrair o corpo do e‑mail e gravar a string em um arquivo.
og_title: Extrair HTML de MHTML – Java passo a passo
tags:
- Java
- Aspose.HTML
- Email Processing
title: Extrair HTML de MHTML – Guia Completo de Java
url: /pt/java/creating-managing-html-documents/extract-html-from-mhtml-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair HTML de MHTML – Guia Completo em Java

Já precisou **extrair HTML de MHTML** mas não sabia por onde começar? Talvez você tenha recebido um e‑mail arquivado (`.mht`) e queira o corpo limpo para uma pré‑visualização web, ou esteja construindo um script de migração que transforma arquivos legados em páginas HTML modernas. Em qualquer caso, o problema é o mesmo: você tem um arquivo de web‑archive de um único arquivo e precisa do markup HTML bruto dele.

> **Resumo rápido:** Ao final deste guia você será capaz de **extrair o corpo do e‑mail**, **converter MHTML para HTML**, e **escrever a string em um arquivo** com um trecho limpo e reutilizável que funciona para qualquer `.mht` ou `.mhtml` que você usar.

---

## O que você precisará

Antes de mergulharmos, certifique‑se de que você tem:

- **Java 17+** (o código usa o padrão try‑with‑resources, que está disponível desde o Java 7, mas o Java 17 é o LTS atual).
- **Aspose.HTML for Java** JARs no seu classpath. Você pode obtê‑los no [site da Aspose](https://products.aspose.com/html/java/) ou via Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- Um arquivo de exemplo **`.mht` ou `.mhtml`** que você deseja processar. Para a demonstração, chamaremos de `email.mht` e o colocaremos em `YOUR_DIRECTORY`.

É só isso—sem frameworks extras, sem parsers pesados. Apenas Java puro e uma única biblioteca bem documentada.

---

## Etapa 1 – Abrir o arquivo MHTML como um Stream

A primeira coisa que fazemos é abrir o e‑mail arquivado como um `InputStream`. Usar um stream mantém o uso de memória baixo, especialmente para arquivos `.mht` grandes que podem conter imagens ou CSS incorporados.

```java
// Step 1: Open the MHTML file as a stream
try (InputStream mhtmlStream = new FileInputStream("YOUR_DIRECTORY/email.mht")) {
    // Subsequent steps go inside this block
}
```

**Por que um stream?**  
Um stream permite que o `MhtmlDocument` leia os dados sob demanda, o que significa que você não encontrará `OutOfMemoryError` mesmo que o arquivo tenha vários megabytes. Também dá flexibilidade para ler de outras fontes mais tarde (por exemplo, um `ByteArrayInputStream` vindo de um banco de dados).

---

## Etapa 2 – Carregar o Documento MHTML a partir do Stream

Agora entregamos o stream à classe `MhtmlDocument` da Aspose. Essa classe analisa o arquivo MIME‑codificado e constrói uma representação semelhante a um DOM do HTML incorporado.

```java
// Step 2: Load the MHTML document from the stream
MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);
```

**Nos bastidores:**  
A Aspose extrai cada parte MIME (HTML, imagens, CSS) e as re‑monta internamente. Por isso você pode, mais tarde, solicitar apenas a parte HTML sem se preocupar com os recursos incorporados.

---

## Etapa 3 – Recuperar o Conteúdo HTML Principal

Com o documento carregado, obter o HTML bruto é uma linha única. O método `getHtmlContent()` devolve o corpo como uma `String`, preservando o markup original.

```java
// Step 3: Retrieve the main HTML content as a string
String htmlContent = mhtmlDoc.getHtmlContent();
```

**O que você obtém:**  
`htmlContent` contém a página HTML completa—including `<head>` e `<body>` tags—exatamente como apareceu quando o e‑mail foi salvo. Se precisar apenas da parte visível, pode analisá‑la depois com Jsoup e remover o `<head>`.

---

## Etapa 4 – Escrever o HTML Extraído em um Arquivo Separado

Salvar a string no disco é simples com a API `java.nio.file`. Esta etapa demonstra o padrão **escrever string em arquivo** que funciona em qualquer plataforma.

```java
// Step 4: Save the extracted HTML to a separate file
Files.writeString(Path.of("YOUR_DIRECTORY/email_body.html"), htmlContent);
```

**Dica:**  
Se precisar de um conjunto de caracteres específico, use `Files.writeString(Path, CharSequence, Charset)`. O padrão é UTF‑8, que funciona para a maioria dos e‑mails modernos.

---

## Etapa 5 – Confirmar a Extração

Um rápido `System.out.println` permite verificar se tudo foi executado sem exceções. Em um job de produção você substituiria isso por um log adequado.

```java
// Step 5: Indicate successful extraction
System.out.println("HTML extracted.");
```

Ao executar o programa, você deverá ver `HTML extracted.` no console, e o arquivo `email_body.html` aparecerá em `YOUR_DIRECTORY`.

---

## Exemplo Completo, Pronto‑para‑Executar

Juntando tudo, aqui está a classe Java completa e autônoma. Sinta‑se à vontade para copiar‑colar no seu IDE e clicar em **Run**.

```java
import com.aspose.html.MhtmlDocument;
import java.io.FileInputStream;
import java.io.InputStream;
import java.nio.file.Files;
import java.nio.file.Path;

public class MhtmlToHtmlConverter {

    public static void main(String[] args) {
        // Adjust the path to point to your .mht/.mhtml file
        String sourcePath = "YOUR_DIRECTORY/email.mht";
        String targetPath = "YOUR_DIRECTORY/email_body.html";

        // Try-with-resources ensures the stream is closed automatically
        try (InputStream mhtmlStream = new FileInputStream(sourcePath)) {

            // Load the MHTML document
            MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);

            // Extract the HTML content
            String htmlContent = mhtmlDoc.getHtmlContent();

            // Write the HTML string to a new file
            Files.writeString(Path.of(targetPath), htmlContent);

            // Simple confirmation output
            System.out.println("HTML extracted to " + targetPath);
        } catch (Exception e) {
            // In real code you might want to log this instead of printing
            System.err.println("Failed to extract HTML: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Saída Esperada

Executar o programa imprime algo como:

```
HTML extracted to YOUR_DIRECTORY/email_body.html
```

E `email_body.html` conterá o código‑fonte HTML completo do e‑mail original. Abra-o em um navegador—você deverá ver a mesma renderização visual da mensagem arquivada (exceto recursos externos que não foram incluídos).

---

## Tratamento de Casos de Borda Comuns

### 1. Recursos Incorporados Ausentes

Às vezes o arquivo MHTML referencia imagens externas que não foram salvas dentro do arquivo. Nesses casos `getHtmlContent()` ainda devolve a marcação `<img src="...">`, mas as URLs apontarão para o local original na web. Se precisar de um HTML totalmente autocontido, você pode:

- Usar `MhtmlDocument.save(Path, SaveFormat.HTML)` para que a Aspose extraia todos os recursos em uma pasta.
- Ou pós‑processar o HTML com uma biblioteca como **Jsoup** para substituir URLs remotas por data URIs codificados em base64.

### 2. Codificações Não‑UTF‑8

Se o seu e‑mail foi salvo com um charset diferente (por exemplo, `windows-1252`), a string retornada pode conter caracteres corrompidos. Você pode forçar um charset específico ao escrever:

```java
Files.writeString(
    Path.of(targetPath),
    htmlContent,
    StandardCharsets.ISO_8859_1
);
```

### 3. Arquivos Grandes

Para arquivos maiores que algumas centenas de megabytes, considere fazer streaming da saída HTML diretamente para um `BufferedWriter` em vez de carregar a string inteira na memória. A Aspose também oferece um método **`save`** que grava diretamente em um arquivo, ignorando o `String` intermediário.

---

## Dicas Profissionais & Boas Práticas

- **Reutilize o objeto `MhtmlDocument`** se precisar extrair múltiplas partes (por exemplo, CSS, imagens). Ele analisa o arquivo apenas uma vez.
- **Valide a saída** com um validador HTML (validador W3C ou `jsoup.isValid()`) se for alimentar o HTML a outro sistema.
- **Logue, não imprima** em produção. Substitua `System.out.println` por um framework de logging como SLF4J para capturar timestamps e níveis de severidade.
- **Controle de versão das dependências.** A Aspose lança atualizações frequentes; fixe a versão no seu `pom.xml` para evitar mudanças inesperadas.

---

## Conclusão

Acabamos de percorrer uma solução prática, de ponta a ponta, para **extrair HTML de MHTML** usando Java. Ao abrir o arquivo como stream, carregá‑lo com Aspose.HTML, obter a string HTML e **escrevê‑la em um arquivo**, você agora tem um método confiável para **converter MHTML para HTML**, **extrair o corpo do e‑mail** e até **converter MHT para HTML** para processamento posterior.

Sinta‑se livre para adaptar o trecho: troque `FileInputStream` por um `ByteArrayInputStream` se seus arquivos estiverem em um banco de dados, ou integre o código a um job em lote que processe dezenas de e‑mails de uma vez. A ideia central permanece a mesma—deixe a biblioteca dedicada fazer o trabalho pesado e manipule o texto puro como precisar.

**Próximos passos** que você pode explorar:

- Use Jsoup para **limpar o HTML extraído** (remover pixels de rastreamento, CSS inline, etc.).
- Automatize **conversão em massa** percorrendo um diretório de arquivos `.mht`.
- Combine isso com **Apache POI** para incorporar o HTML limpo em documentos Word ou PDF.

Tem dúvidas sobre um caso específico ou quer compartilhar como estendeu o script? Deixe um comentário abaixo—bom código! 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}