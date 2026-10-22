---
category: general
date: 2026-10-21
description: Aprenda a salvar HTML como ZIP usando Aspose.HTML, converter HTML para
  ZIP e remover recursos para um pacote limpo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save html as zip
- convert html to zip
- how to omit resources
- how to strip resources
- create html zip
language: pt
lastmod: 2026-10-21
og_description: Salve HTML como ZIP com Aspose.HTML, aprenda como converter HTML para
  ZIP e remover recursos para um arquivo leve.
og_image_alt: Screenshot showing the save html as zip process with resources omitted
og_title: Salvar HTML como ZIP com Aspose.HTML – omitir recursos em uma única etapa
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to save HTML as ZIP using Aspose.HTML, convert HTML to ZIP,
    and strip resources for a clean package.
  headline: How to save HTML as ZIP with Aspose.HTML and omit resources
  type: TechArticle
tags:
- Aspose.HTML
- C#
- ZIP archive
- HTML conversion
- Resource handling
title: Como salvar HTML como ZIP com Aspose.HTML e omitir recursos
url: /pt/net/html-extensions-and-conversions/how-to-save-html-as-zip-with-aspose-html-and-omit-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como salvar HTML como ZIP com Aspose.HTML e omitir recursos

Se você precisa **salvar HTML como ZIP** enquanto remove arquivos externos, este guia mostra uma solução completa e pronta‑para‑executar. Ao final do tutorial você será capaz de **converter HTML para ZIP**, controlar quais recursos são mantidos e gerar um arquivo compactado limpo que contém apenas a marcação principal.

Muitos cenários de automação web exigem empacotar uma página para uso offline, anexo de e‑mail ou armazenamento de arquivo. Incluir imagens, fontes ou scripts costuma inflar o arquivo desnecessariamente. As etapas abaixo explicam **como omitir recursos** e **como remover recursos** da saída, de modo que o ZIP resultante permaneça leve.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

- .NET 6.0 ou superior instalado  
- Uma licença do Aspose.HTML for .NET (ou uma avaliação gratuita)  
- Um ambiente básico de desenvolvimento C# (Visual Studio, VS Code ou Rider)  

Nenhum pacote NuGet adicional é necessário além do `Aspose.Html`.

## Etapa 1: Criar um manipulador de recursos personalizado

O núcleo de **como omitir recursos** está em uma subclasse de `ResourceHandler`. O Aspose.HTML chama esse manipulador para cada ativo externo (imagens, CSS, scripts). Ao retornar um stream vazio, você efetivamente indica ao conversor que ignore o recurso.

```csharp
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Prevents external resources from being written to the output package.
/// </summary>
class CustomResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Returning an empty MemoryStream strips the resource from the ZIP.
        return new MemoryStream();
    }
}
```

**Por que isso importa:** O comportamento padrão copia todo arquivo vinculado para o ZIP, o que pode dobrar ou triplicar o tamanho do arquivo. Substituir `HandleResource` fornece controle granular sem modificar o HTML original.

## Etapa 2: Carregar o documento HTML

Carregue o arquivo fonte com `HTMLDocument`. O construtor aceita um caminho de arquivo, uma URL ou um stream. Neste exemplo lemos um arquivo local chamado `input.html`.

```csharp
// Load the source HTML file from the local file system.
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

Se o seu HTML estiver em memória ou vier de uma requisição web, você pode passar um `MemoryStream` ou uma string de URL em vez disso. A API funciona da mesma forma.

## Etapa 3: Configurar as opções de salvamento

Crie uma instância de `HtmlSaveOptions` e atribua o manipulador personalizado criado na Etapa 1. Isso indica ao Aspose.HTML para usar o manipulador sempre que encontrar um recurso.

```csharp
// Prepare save options and attach the custom resource handler.
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // The ResourceHandler property is what enables resource stripping.
    ResourceHandler = new CustomResourceHandler()
};
```

Você também pode ajustar outras opções aqui, como `CompressImages = false` se quiser manter os dados das imagens mas ainda omitir outros ativos. O exemplo mantém as configurações de compressão padrão.

## Etapa 4: Salvar o documento como um arquivo ZIP

Por fim, invoque `Save` com o caminho de destino e as opções configuradas. O arquivo de saída será um `.zip` que contém `index.html` (ou o nome original do arquivo) e **nenhum recurso externo**.

```csharp
// Save the HTML document as a ZIP file. The archive will contain only the HTML markup.
document.Save("YOUR_DIRECTORY/output.zip", saveOptions);
```

### Resultado esperado

- `output.zip` → contém um único arquivo `index.html`.  
- Todas as imagens, arquivos CSS e referências JavaScript são omitidos, porque o manipulador personalizado retornou um stream vazio para cada um.  

Você pode verificar o arquivo abrindo-o com qualquer visualizador de ZIP. A página HTML ainda referenciará as URLs originais, mas esses arquivos não estarão presentes no arquivo, mantendo o pacote mínimo.

## Exemplo completo, executável

Abaixo está o programa completo que você pode copiar, colar e executar. Substitua `YOUR_DIRECTORY` por um caminho de pasta real na sua máquina.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

class Program
{
    static void Main()
    {
        // Step 1: Define a custom resource handler to control how external resources are saved.
        class CustomResourceHandler : ResourceHandler
        {
            public override Stream HandleResource(ResourceInfo info)
            {
                // Returning an empty stream strips the resource from the ZIP output.
                return new MemoryStream();
            }
        }

        // Step 2: Load an HTML document from a file.
        string inputPath = "YOUR_DIRECTORY/input.html";
        HTMLDocument document = new HTMLDocument(inputPath);

        // Step 3: Create HTML save options and assign the custom handler.
        HtmlSaveOptions saveOptions = new HtmlSaveOptions
        {
            ResourceHandler = new CustomResourceHandler()
        };

        // Step 4: Save the document as a ZIP archive containing the HTML and (now omitted) resources.
        string outputPath = "YOUR_DIRECTORY/output.zip";
        document.Save(outputPath, saveOptions);

        Console.WriteLine($"HTML has been saved as ZIP at: {outputPath}");
    }
}
```

Executar este programa gera o arquivo ZIP descrito anteriormente. Agora você pode distribuir a página HTML sem agrupar ativos desnecessários.

## Variações comuns e casos de borda

| Cenário | Ajuste |
|----------|------------|
| **Manter imagens, mas remover CSS/JS** | No `CustomResourceHandler`, inspecione `info.MimeType`. Retorne um `MemoryStream` apenas para `text/css` e `application/javascript`. |
| **Preservar fontes externas** | Retorne o stream original para tipos MIME `font/woff2`, caso contrário retorne um stream vazio. |
| **Gerar um ZIP com nome de entrada personalizado** | Use a sobrecarga de `HtmlSaveOptions` `Save(string path, SaveOptions options, string entryName)` para especificar um nome de arquivo raiz diferente. |
| **Converter vários arquivos HTML em um único ZIP** | Percorra cada arquivo, crie um `HTMLDocument` separado e adicione cada um ao mesmo `ZipArchive` manualmente usando `System.IO.Compression`. |

Essas variações ilustram **como remover recursos** seletivamente, dando a você controle total sobre o tamanho final do arquivo.

## Dicas avançadas

- **Validar o resultado**: Após salvar, abra o ZIP e carregue `index.html` em um navegador. Recursos ausentes aparecerão como links quebrados, confirmando que o manipulador funcionou.  
- **Desempenho**: Retornar um `MemoryStream` vazio é barato, mas se você tiver milhares de ativos, considere armazenar em cache a decisão (por exemplo, um `HashSet<string>` de tipos MIME a serem ignorados).  
- **Licenciamento**: A versão de avaliação gratuita do Aspose.HTML adiciona um comentário de marca d'água dentro do HTML. Implante uma versão licenciada para removê‑lo em produção.  

## Conclusão

Agora você sabe como **salvar HTML como ZIP**, **converter HTML para ZIP** e **remover recursos** usando o Aspose.HTML para .NET. Ao implementar um `ResourceHandler` personalizado, você pode omitir arquivos indesejados e manter o arquivo compacto. Experimente a lógica do manipulador para manter apenas os recursos que realmente precisa e integre esse padrão em pipelines de automação maiores.

---

**Próximos passos**

- Explore outros recursos de `HtmlSaveOptions` como `EmbedImages` para incorporar imagens diretamente no HTML.  
- Combine esta abordagem com `Aspose.PDF` para converter o mesmo HTML em PDF após criar o ZIP.  
- Investigue cenários server‑side onde você gera o ZIP sob demanda e o transmite ao cliente sem gravar em disco.  

Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Use ZipArchive – Save HTML and Resources to a ZIP File](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [How to Save HTML in C# – Custom Resource Handlers & ZIP](/html/english/net/working-with-html-documents/how-to-save-html-in-c-custom-resource-handlers-zip/)
- [How to Save HTML as ZIP in C# – Complete Aspose.HTML Guide](/html/english/net/html-extensions-and-conversions/how-to-save-html-as-zip-in-c-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}