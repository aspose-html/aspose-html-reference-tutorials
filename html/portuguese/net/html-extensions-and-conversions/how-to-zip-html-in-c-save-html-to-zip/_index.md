---
category: general
date: 2025-12-29
description: Como compactar HTML em C# rapidamente usando Aspose.HTML – salvar HTML
  em zip com um ZipResourceHandler personalizado. Aprenda passo a passo.
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: pt
og_description: Como compactar HTML em C# rapidamente usando Aspose.HTML. Siga este
  guia para salvar HTML em zip e criar um arquivo zip com manipulação personalizada
  de recursos.
og_title: Como compactar HTML em C# – Salvar HTML em Zip
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: Como compactar HTML em C# – Salvar HTML em Zip
url: /pt/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Compactar HTML em C# – Salvar HTML em Zip

Compactar HTML em C# é uma necessidade comum quando você quer empacotar páginas web para uso offline. Seja agrupando uma única página com suas imagens ou exportando um site inteiro, **salvar HTML em zip** mantém tudo organizado e portátil. Neste tutorial vamos percorrer uma solução completa, pronta‑para‑executar, que não apenas compacta o markup HTML, mas também transmite cada recurso referenciado diretamente para o arquivo.

Você aprenderá a:

* Criar um arquivo zip programaticamente com o `System.IO.Compression` do .NET.
* Inserir um `ResourceHandler` personalizado no Aspose.HTML para que os recursos fluam diretamente para o zip.
* Lidar com casos de borda como arquivos zip existentes e ativos binários grandes.

Nenhuma ferramenta externa necessária — apenas C#, Aspose.HTML e algumas linhas de código.

## O que você precisará

Antes de começarmos, certifique‑se de que tem:

* **.NET 6+** (o código também funciona no .NET Framework 4.6.2 e posteriores).
* **Aspose.HTML for .NET** – você pode obter uma avaliação gratuita no site da Aspose ou usar uma cópia licenciada.
* Um ambiente de desenvolvimento (Visual Studio, VS Code, Rider — o que preferir).

É só isso. Nenhum pacote NuGet extra além de `System.IO.Compression` (já incluído no .NET) e `Aspose.HTML`.

## Etapa 1: Configurar o Projeto e os Imports

Crie um novo projeto de console (ou adicione o código a um já existente). Adicione as diretivas `using` necessárias no topo do seu arquivo:

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **Dica profissional:** Se você estiver usando o Visual Studio, o IDE sugerirá a adição do pacote NuGet ausente para `Aspose.Html`. Aceite a sugestão e você estará pronto para prosseguir.

## Etapa 2: Implementar um ZipResourceHandler Personalizado

O Aspose.HTML chama um `ResourceHandler` sempre que precisa gravar um recurso (como uma imagem, arquivo CSS ou script). Sobrescrevendo `HandleResource`, podemos decidir exatamente onde cada recurso será colocado. O handler abaixo cria uma entrada zip que espelha o caminho lógico do recurso e devolve um stream gravável que aponta diretamente para essa entrada.

```csharp
/// <summary>
/// Streams each HTML resource straight into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Ensure the entry's directory structure exists inside the zip.
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        // The returned stream writes directly into the zip entry.
        return entry.Open();
    }
}
```

**Por que isso importa:**  
Em vez de gravar recursos em uma pasta temporária e depois compactar a pasta, este handler transmite os dados em tempo real, economizando I/O de disco e mantendo o uso de memória baixo. Ele também garante que a hierarquia de pastas interna do zip corresponda aos caminhos relativos do HTML, que os navegadores esperam ao descompactar e abrir a página.

## Etapa 3: Preparar o Arquivo Zip

Agora vamos abrir (ou criar) o arquivo zip de destino. O sinalizador `FileMode.Create` sobrescreve qualquer arquivo existente — perfeito para builds repetíveis. Se preferir preservar um arquivo zip já existente, troque para `FileMode.OpenOrCreate` e trate entradas duplicadas conforme necessário.

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **Caso de borda:** Se o processo travar antes que o bloco `using` descarte o archive, você pode acabar com um zip corrompido. Executar o código dentro de um `try/catch` e excluir o arquivo parcialmente criado em caso de falha é uma salvaguarda simples.

## Etapa 4: Construir o Documento HTML com um Recurso Incorporado

Para demonstração, criaremos uma página HTML mínima que referencia uma imagem chamada `image.png`. Em um cenário real você carregaria o HTML de um arquivo ou de uma string proveniente de um banco de dados.

```csharp
// Sample HTML containing an <img> tag.
// Aspose.HTML will ask the ResourceHandler for "image.png".
string htmlContent = @"
<html>
<head><title>Sample Zip</title></head>
<body>
    <h1>Hello, zipped world!</h1>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

// Create the document from the string.
var html = new HTMLDocument(htmlContent);
```

Se você possui arquivos de imagem reais no disco, pode adicioná‑los ao zip manualmente antes de salvar o HTML, ou deixar o Aspose.HTML buscá‑los via handler (por exemplo, a partir de uma URL). O handler que escrevemos funciona tanto para caminhos locais quanto para URLs remotas.

## Etapa 5: Configurar as Opções de Salvamento para Usar o ZipResourceHandler

Agora instruímos o Aspose.HTML a usar nosso handler personalizado ao gravar os recursos. A classe `HTMLSaveOptions` também permite especificar o nome do arquivo de saída dentro do zip (por padrão é `index.html`).

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## Etapa 6: Salvar o Documento – Tudo Transmite para o Zip

Por fim, invoque `Save`. O Aspose.HTML analisa o markup, localiza a tag `<img>`, chama `HandleResource` para `image.png` e grava tanto o arquivo HTML quanto a imagem no mesmo arquivo zip.

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

Quando os blocos `using` são finalizados, o `ZipArchive` conclui o arquivo, tornando‑o pronto para distribuição.

### Exemplo Completo Funcional

A seguir está o programa inteiro montado. Copie‑e cole em `Program.cs` e execute — nenhuma modificação adicional é necessária.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare the zip file.
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);
        using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);

        // 2️⃣ Build a simple HTML document with an image reference.
        string htmlContent = @"
        <html>
        <head><title>Sample Zip</title></head>
        <body>
            <h1>Hello, zipped world!</h1>
            <img src='image.png' alt='Demo image'>
        </body>
        </html>";
        var html = new HTMLDocument(htmlContent);

        // 3️⃣ Set save options to stream resources into the zip.
        var saveOptions = new HTMLSaveOptions
        {
            OutputFileName = "index.html",
            OutputStorage = new ZipResourceHandler(zip)
        };

        // 4️⃣ Save – everything ends up in output.zip.
        html.Save(saveOptions);
        Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
    }
}
```

**Resultado esperado:** Após a execução, `output.zip` contém duas entradas:

```
index.html
image.png
```

Se você descompactar o arquivo e abrir `index.html` em um navegador, a imagem será exibida corretamente porque o caminho relativo foi preservado.

## Perguntas Frequentes

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}