---
category: general
date: 2026-08-15
description: Crie um manipulador de recursos personalizado em C# para gerenciar recursos
  HTML, como imagens e CSS. Aprenda HTMLLoadOptions, fluxos de memória e o carregamento
  de HTMLDocument.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: pt
lastmod: 2026-08-15
og_description: Criar manipulador de recursos personalizado em C# para controlar como
  os recursos HTML são transmitidos. Este tutorial mostra a configuração de HTMLLoadOptions,
  o tratamento de streams de memória e o carregamento de HTMLDocument com lógica personalizada.
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: Crie um manipulador de recursos personalizado em C# – guia completo para
  gerenciamento de recursos HTML
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: Criar manipulador de recurso personalizado em C# para carregamento de HTML
url: /pt/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar manipulador de recurso personalizado em C# para carregamento de HTML

Se você precisa **criar manipulador de recurso personalizado** para arquivos HTML, este guia mostra exatamente como fazer. Você aprenderá a interceptar imagens, CSS e outros recursos ao carregar um documento HTML, usando `HTMLLoadOptions` e um stream baseado em memória.

O tutorial cobre tudo o que é necessário para implementar um manipulador reutilizável, configurar opções de carregamento e verificar se os recursos são capturados corretamente. Nenhuma documentação externa é necessária — apenas o código abaixo e as explicações.

## Pré-requisitos

- .NET 6.0 ou posterior
- Familiaridade básica com C#
- Uma referência à biblioteca de processamento HTML que fornece `HTMLDocument`, `HtmlLoadOptions` e `ResourceHandler` (por exemplo, GroupDocs.Viewer for .NET)

## Visão geral da solução

Vamos:

1. **Criar um manipulador de recurso personalizado** ao estender `ResourceHandler`.
2. Configurar `HTMLLoadOptions` para usar o manipulador.
3. Carregar um arquivo HTML com `HTMLDocument` enquanto o manipulador fornece um stream para cada recurso.
4. (Opcional) Armazenar os recursos recebidos em disco para verificação.

Cada passo inclui o código-fonte completo e o raciocínio por trás dele.

## Passo 1: Definir a classe do manipulador de recurso personalizado

Criar um manipulador personalizado significa sobrescrever `HandleResource` para que a biblioteca possa gravar os bytes do recurso em um stream que você controla. Usar um `MemoryStream` mantém os dados na memória, o que é ideal para testes ou processamento adicional.

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**Por que isso importa:**  
Sobrescrever `HandleResource` lhe dá controle total sobre onde os dados do recurso são enviados. Se mais tarde precisar armazenar imagens em cache, transformar CSS ou registrar o uso de recursos, você pode substituir o `MemoryStream` por qualquer implementação de stream personalizada.

## Passo 2: Configurar `HTMLLoadOptions` para usar o manipulador

`HTMLLoadOptions` permite conectar o manipulador ao pipeline de carregamento. Definir a propriedade `ResourceHandler` indica ao visualizador para invocar `MyHandler` para cada recurso externo.

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**Por que isso importa:**  
Sem atribuir `ResourceHandler`, o visualizador gravaria os recursos em seu local padrão (geralmente uma pasta temporária). Ao especificar seu próprio manipulador, você **cria manipulador de recurso personalizado** que se alinha à estratégia de armazenamento da sua aplicação.

## Passo 3: Carregar o documento HTML com as opções configuradas

Agora carregue o arquivo HTML. O visualizador chamará `MyHandler.HandleResource` para cada recurso que encontrar.

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

Neste ponto o conteúdo HTML é analisado, e todos os recursos externos foram transmitidos para os buffers de memória fornecidos por `MyHandler`.

## Passo 4 (opcional): Acessar os recursos capturados

Se precisar inspecionar ou persistir os recursos, você pode modificar `MyHandler` para armazenar cada `MemoryStream` em um dicionário indexado pelo nome do recurso.

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

Após o carregamento, você pode iterar sobre `handler.Resources` e gravar cada um em disco:

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**Por que isso importa:**  
Armazenar recursos permite pós‑processamento como otimização de imagens, minificação de CSS ou arquivamento. Também fornece uma verificação tangível de que a lógica de **criar manipulador de recurso personalizado** funciona como esperado.

## Passo 5: Limpar

Tanto `HTMLDocument` quanto quaisquer streams devem ser descartados para liberar recursos não gerenciados.

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## Exemplo completo executável

Abaixo está um programa autônomo que demonstra todos os passos, desde a definição da classe até a extração de recursos.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**Saída esperada**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

O console lista cada recurso que o visualizador transmitiu através do seu manipulador personalizado, confirmando que o fluxo de trabalho de **criar manipulador de recurso personalizado** foi bem‑sucedido.

## Perguntas comuns e casos de borda

| Pergunta | Resposta |
|----------|----------|
| *E se um recurso for grande (por exemplo, imagem de alta resolução)?* | Substitua `MemoryStream` por um `FileStream` apontando para uma pasta temporária. Isso evita consumo excessivo de memória. |
| *Posso filtrar recursos por tipo?* | Dentro de `HandleResource`, inspecione `info.MimeType` ou `info.Extension` e retorne `null` para tipos indesejados. Retornar `null` indica ao visualizador que ele deve ignorar o recurso. |
| *É necessária segurança de thread?* | Se a mesma instância do manipulador for usada em múltiplos carregamentos concorrentes, proteja o dicionário `Resources` com um lock ou use uma coleção concorrente. |
| *Como posso suportar URLs relativas?* | `ResourceInfo` contém a URL original; você pode combiná‑la com o caminho base do arquivo HTML para resolver referências relativas antes de armazenar. |

## Conclusão

Agora você sabe como **criar manipulador de recurso personalizado** em C# para carregamento de HTML, configurar `HTMLLoadOptions`, capturar ativos transmitidos e limpar de forma responsável. Esse padrão lhe dá controle total sobre o gerenciamento de recursos, permitindo cenários como processamento de imagens em tempo real, reescrita de CSS ou armazenamento seguro.

Em seguida, explore tópicos relacionados como **carregamento de HTMLDocument** com diferentes opções de renderização, ou estenda o manipulador para implementações de **manipulador de recurso C#** que escrevem diretamente em armazenamento na nuvem. Experimente o método `HandleResource` do manipulador para adequá‑lo ao fluxo de recursos específico do seu projeto.

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar HTML a partir de String em C# – Guia de Manipulador de Recurso Personalizado](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Manipulador de Recurso Personalizado em C# – Tutorial de Conversão de HTML para ZIP](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [Como Salvar HTML em C# – Guia Completo Usando um Manipulador de Recurso Personalizado](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}