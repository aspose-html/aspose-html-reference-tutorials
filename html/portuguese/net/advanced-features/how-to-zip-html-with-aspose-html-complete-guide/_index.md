---
category: general
date: 2026-03-02
description: Aprenda a compactar HTML usando Aspose HTML, um manipulador de recursos
  personalizado e .NET ZipArchive. Guia passo a passo sobre como criar zip e incorporar
  recursos.
draft: false
keywords:
- how to zip html
- custom resource handler
- aspose html save
- how to create zip
- how to embed resources
language: pt
og_description: Aprenda a compactar HTML usando Aspose HTML, um manipulador de recursos
  personalizado e .NET ZipArchive. Siga os passos para criar o zip e incorporar recursos.
og_title: Como Compactar HTML com Aspose HTML – Guia Completo
tags:
- Aspose.HTML
- C#
- ZIP archive
title: Como compactar HTML com Aspose HTML – Guia completo
url: /pt/net/advanced-features/how-to-zip-html-with-aspose-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Compactar HTML com Aspose HTML – Guia Completo

Já precisou **compactar HTML** junto com todas as imagens, arquivos CSS e scripts que ele referencia? Talvez você esteja criando um pacote de download para um sistema de ajuda offline, ou simplesmente queira distribuir um site estático como um único arquivo. De qualquer forma, aprender **como compactar HTML** é uma habilidade útil na caixa de ferramentas de um desenvolvedor .NET.

Neste tutorial vamos percorrer uma solução prática que usa **Aspose.HTML**, um **custom resource handler**, e a classe integrada `System.IO.Compression.ZipArchive`. Ao final, você saberá exatamente como **salvar** um documento HTML em um ZIP, **incorporar recursos**, e ainda ajustar o processo caso precise suportar URIs incomuns.

> **Pro tip:** O mesmo padrão funciona para PDFs, SVGs ou qualquer outro formato pesado em recursos web—basta trocar a classe Aspose.

---

## O que você precisará

- .NET 6 ou posterior (o código também compila com .NET Framework)
- Pacote NuGet **Aspose.HTML for .NET** (`Aspose.Html`)
- Um entendimento básico de streams C# e I/O de arquivos
- Uma página HTML que referencia recursos externos (imagens, CSS, JS)

Nenhuma biblioteca ZIP de terceiros adicional é necessária; o namespace padrão `System.IO.Compression` faz todo o trabalho pesado.

---

## Etapa 1: Criar um ResourceHandler Personalizado (custom resource handler)

Aspose.HTML chama um `ResourceHandler` sempre que encontra uma referência externa ao salvar. Por padrão, ele tenta baixar o recurso da web, mas queremos **incorporar** os arquivos exatos que estão no disco. É aí que entra um **custom resource handler**.

```csharp
using System;
using System.IO;
using Aspose.Html;

// Step 1 – custom handler that copies local files into the output stream
class MyResourceHandler : ResourceHandler
{
    public override void HandleResource(string uri, Stream outputStream)
    {
        // Assume uri is a local file path; adjust logic for URLs if needed
        using (var source = new FileStream(uri, FileMode.Open, FileAccess.Read))
        {
            source.CopyTo(outputStream);
        }
    }
}
```

**Por que isso importa:**  
Se você pular esta etapa, o Aspose tentará uma requisição HTTP para cada `src` ou `href`. Isso adiciona latência, pode falhar atrás de firewalls e anula o objetivo de um ZIP autocontido. Nosso handler garante que o arquivo exato que está no disco termine dentro do arquivo.

---

## Etapa 2: Carregar o Documento HTML (aspose html save)

Aspose.HTML pode ingerir uma URL, um caminho de arquivo ou uma string HTML bruta. Para esta demonstração, carregaremos uma página remota, mas o mesmo código funciona com um arquivo local.

```csharp
using Aspose.Html;

// Step 2 – load the HTML document (URL, file path, or raw string)
var htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

**O que está acontecendo nos bastidores?**  
A classe `HTMLDocument` analisa a marcação, constrói um DOM e resolve URLs relativas. Quando você posteriormente chamar `Save`, o Aspose percorre o DOM, solicita ao seu `ResourceHandler` cada arquivo externo e grava tudo no stream de destino.

---

## Etapa 3: Preparar um Arquivo ZIP em Memória (how to create zip)

Em vez de gravar arquivos temporários no disco, manteremos tudo em memória usando `MemoryStream`. Essa abordagem é mais rápida e evita poluir o sistema de arquivos.

```csharp
using System.IO;
using System.IO.Compression;

// Step 3 – create a memory‑backed ZIP archive
using var archiveStream = new MemoryStream();
using var archive = new ZipArchive(archiveStream, ZipArchiveMode.Create, true);
```

**Observação de caso extremo:**  
Se seu HTML referenciar ativos muito grandes (por exemplo, imagens de alta resolução), o stream em memória pode consumir muita RAM. Nesse cenário, troque para um ZIP baseado em `FileStream` (`new FileStream("temp.zip", FileMode.Create)`).

---

## Etapa 4: Salvar o Documento HTML no ZIP (aspose html save)

Agora combinamos tudo: o documento, nosso `MyResourceHandler` e o arquivo ZIP.

```csharp
// Step 4 – save HTML + resources into the ZIP
var resourceHandler = new MyResourceHandler();
htmlDoc.Save(archive, resourceHandler);
```

Nos bastidores, o Aspose cria uma entrada para o arquivo HTML principal (geralmente `index.html`) e entradas adicionais para cada recurso (ex.: `images/logo.png`). O `resourceHandler` grava os dados binários diretamente nessas entradas.

---

## Etapa 5: Gravar o ZIP no Disco (how to embed resources)

Finalmente, persistimos o arquivo ZIP em memória para um arquivo físico. Você pode escolher qualquer pasta; basta substituir `YOUR_DIRECTORY` pelo caminho real.

```csharp
using System.IO;

// Step 5 – persist the ZIP file
File.WriteAllBytes(@"YOUR_DIRECTORY\sample.zip", archiveStream.ToArray());

// Optional: verify the archive size
Console.WriteLine($"ZIP created: {new FileInfo(@"YOUR_DIRECTORY\sample.zip").Length} bytes");
```

**Dica de verificação:**  
Abra o `sample.zip` resultante com o explorador de arquivos do seu sistema operacional. Você deverá ver `index.html` mais uma hierarquia de pastas que espelha as localizações originais dos recursos. Clique duas vezes em `index.html`—ele deve ser renderizado offline sem imagens ou estilos ausentes.

---

## Exemplo Completo (Todas as Etapas Combinadas)

Abaixo está o programa completo, pronto para ser executado. Copie‑e cole em um novo projeto de Console App, restaure o pacote NuGet `Aspose.Html` e pressione **F5**.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

// Step 1: Custom ResourceHandler that copies each external resource into the ZIP entry.
class MyResourceHandler : ResourceHandler
{
    public override void HandleResource(string uri, Stream outputStream)
    {
        // Handle both absolute file paths and relative URLs.
        if (File.Exists(uri))
        {
            using var source = new FileStream(uri, FileMode.Open, FileAccess.Read);
            source.CopyTo(outputStream);
        }
        else
        {
            // Fallback: try to download from the web (rarely needed for offline ZIPs).
            using var client = new System.Net.WebClient();
            var data = client.DownloadData(uri);
            outputStream.Write(data, 0, data.Length);
        }
    }
}

class Program
{
    static void Main()
    {
        // Step 2: Load the HTML document (URL, file path, or raw HTML string).
        var htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // Step 3: Prepare an in‑memory ZIP archive.
        using var archiveStream = new MemoryStream();
        using var archive = new ZipArchive(archiveStream, ZipArchiveMode.Create, true);

        // Step 4: Save the HTML + its resources into the ZIP.
        var resourceHandler = new MyResourceHandler();
        htmlDoc.Save(archive, resourceHandler);

        // Step 5: Persist the ZIP to disk.
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "sample.zip");
        File.WriteAllBytes(outputPath, archiveStream.ToArray());

        Console.WriteLine($"✅ ZIP created at: {outputPath}");
    }
}
```

**Resultado esperado:**  
Um arquivo `sample.zip` aparece na sua Área de Trabalho. Extraia‑o e abra `index.html`—a página deve ficar exatamente como a versão online, mas agora funciona totalmente offline.

---

## Perguntas Frequentes (FAQs)

### Isso funciona com arquivos HTML locais?
Sim. Substitua a URL em `HTMLDocument` por um caminho de arquivo, por exemplo, `new HTMLDocument(@"C:\site\index.html")`. O mesmo `MyResourceHandler` copiará os recursos locais.

### E se um recurso for um data‑URI (codificado em base64)?
O Aspose trata data‑URIs como já incorporados, portanto o handler não é chamado. Nenhum trabalho extra é necessário.

### Posso controlar a estrutura de pastas dentro do ZIP?
Sim. Antes de chamar `htmlDoc.Save`, você pode definir `htmlDoc.SaveOptions` e especificar um caminho base. Alternativamente, modifique `MyResourceHandler` para prefixar um nome de pasta ao criar as entradas.

### Como adiciono um arquivo README ao arquivo?
Basta criar uma nova entrada manualmente:

```csharp
var readme = archive.CreateEntry("README.txt");
using var writer = new StreamWriter(readme.Open());
writer.WriteLine("This ZIP contains an offline HTML site.");
```

---

## Próximos Passos e Tópicos Relacionados

- **How to embed resources** em outros formatos (PDF, SVG) usando as APIs semelhantes da Aspose.  
- **Customizing compression level**: `new ZipArchive(stream, ZipArchiveMode.Create, true, Encoding.UTF8)` permite passar um `ZipArchiveEntry.CompressionLevel` para arquivos mais rápidos ou menores.  
- **Serving the ZIP via ASP.NET Core**: Retorne o `MemoryStream` como um resultado de arquivo (`File(archiveStream, "application/zip", "site.zip")`).  

Experimente essas variações para adequar ao seu projeto. O padrão que cobrimos é flexível o suficiente para lidar com a maioria dos cenários “empacotar tudo em um”.

---

## Conclusão

Acabamos de demonstrar **como compactar HTML** usando Aspose.HTML, um **custom resource handler**, e a classe .NET `ZipArchive`. Ao criar um handler que transmite arquivos locais, carregar o documento, empacotar tudo em memória e, finalmente, persistir o ZIP, você obtém um arquivo totalmente autocontido pronto para distribuição.

Agora você pode criar pacotes ZIP para sites estáticos, exportar bundles de documentação ou até automatizar backups offline—tudo com apenas algumas linhas de C#.

Tem alguma variação que gostaria de compartilhar? Deixe um comentário, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}