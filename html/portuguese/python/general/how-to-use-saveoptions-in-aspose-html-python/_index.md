---
category: general
date: 2026-07-27
description: Como usar SaveOptions no Aspose.HTML (Python) para converter uma página
  HTML grande e aplicar o gerenciamento de recursos de forma eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use SaveOptions
- convert large html page
- apply resource handling
- Aspose.HTML Python
- HTML resource handling
language: pt
lastmod: 2026-07-27
og_description: Como usar SaveOptions no Aspose.HTML (Python) permite converter páginas
  HTML grandes enquanto aplica o gerenciamento de recursos para resultados limpos
  e rápidos.
og_image_alt: Screenshot illustrating how to use SaveOptions in Aspose.HTML for Python
og_title: Como usar SaveOptions no Aspose.HTML – Guia Python
schemas:
- author: Aspose
  dateModified: '2026-07-27'
  description: How to use SaveOptions in Aspose.HTML (Python) to convert large HTML
    page and apply resource handling efficiently.
  headline: How to Use SaveOptions in Aspose.HTML (Python)
  type: TechArticle
- questions:
  - answer: Aspose.HTML follows redirects but won’t send credentials automatically.
      You can pre‑download those assets or use a custom `WebRequest` handler (beyond
      this guide’s scope).
    question: What if the page references resources over HTTPS that require authentication?
  - answer: Yes—set `resource_options.max_handling_depth = 0`. This skips external
      files but leaves any `<style>` blocks intact.
    question: Can I preserve inline CSS while stripping external files?
  - answer: After saving, you can run a secondary pass with Pillow to downscale images,
      or let Aspose.HTML’s built‑in image compression options handle it (use `save_options.image_quality`).
    question: What about very large images that still bloat the output?
  - answer: The limit is global across all resource types (images, scripts, styles).
      If you need granular control, you’d have to filter resources manually after
      loading the document.
    question: Is the depth limit applied per‑resource type?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- HTML processing
title: Como usar SaveOptions no Aspose.HTML (Python)
url: /pt/python/general/how-to-use-saveoptions-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar SaveOptions no Aspose.HTML (Python)

Como usar SaveOptions no Aspose.HTML para Python é algo que muitos desenvolvedores perguntam ao lidar com arquivos HTML massivos. Se você precisa **converter uma página HTML grande** enquanto mantém um controle rigoroso sobre **aplicação de tratamento de recursos**, você está no lugar certo.  

Neste tutorial vamos percorrer um cenário do mundo real: pegar uma página HTML volumosa, limitar a profundidade dos recursos aninhados que são buscados e, finalmente, salvar (ou converter) o resultado com controle cristalino. Sem referências vagas, apenas um exemplo completo e executável que você pode copiar‑colar no seu projeto hoje.

> **Dica profissional:** `SaveOptions` do Aspose.HTML funciona não apenas para salvar novamente em HTML, mas também para converter para PDF, PNG ou até mesmo DOCX. O mesmo padrão que abordamos abaixo se aplica a todos esses formatos.

---

## O que você precisará

- **Python 3.8+** (o código usa dicas de tipo, mas funciona em qualquer versão recente)  
- **Aspose.HTML for Python via .NET** – instale com `pip install aspose-html`  
- Um **arquivo HTML grande** que você deseja reduzir ou transformar (o exemplo usa `big_page.html`)  
- Uma quantidade modesta de espaço em disco para o arquivo de saída  

É só isso—nenhuma biblioteca extra, nenhuma ferramenta de construção pesada.

---

## Como Usar SaveOptions com Opções de Tratamento de Recursos

Este é o ponto central da questão. Criaremos uma instância de `SaveOptions`, anexaremos um objeto `ResourceHandlingOptions` que indica ao Aspose.HTML quão profundo ele deve seguir os recursos vinculados e, em seguida, passaremos tudo para o método `save` do documento.

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Load the source HTML document
input_path = "YOUR_DIRECTORY/big_page.html"
doc = HTMLDocument(input_path)

# Define how deep nested resources should be processed (limit to 3 levels)
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # <-- controls depth of resource fetching

# Attach the resource handling configuration to the save options
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# Save the processed document (or convert to another format if desired)
output_path = "YOUR_DIRECTORY/big_page_processed.html"
doc.save(output_path, save_options)
```

**Por que isso funciona:**  
- `HTMLDocument` carrega o arquivo original, analisando cada `<img>`, `<link>`, `<script>`, etc.  
- `ResourceHandlingOptions.max_handling_depth` indica ao motor para parar de buscar recursos após três níveis de aninhamento — perfeito para evitar loops infinitos em páginas que incorporam outras páginas.  
- `SaveOptions` é o recipiente que transporta tanto o formato de saída (HTML por padrão) quanto as regras de tratamento de recursos.  
- Por fim, `doc.save` grava o novo arquivo, aplicando as regras que acabamos de definir.

Ao executar o script, você verá um novo arquivo em `big_page_processed.html`. Abra-o em um navegador; perceberá que todas as imagens, estilos e scripts até três níveis de profundidade ainda estão presentes, enquanto referências mais profundas foram removidas. Isso reduz drasticamente o tamanho do arquivo sem quebrar o layout principal da página — exatamente o que você precisa quando **converte uma página HTML grande** para uso offline ou envio por e‑mail.

---

## Converta uma Página HTML Grande de Forma Eficiente

Se seu objetivo é *converter uma página HTML grande* para uma versão mais enxuta, o trecho acima já realiza a maior parte do trabalho pesado. No entanto, você pode querer mudar o formato de saída completamente. Aspose.HTML torna isso uma linha de código:

```python
# Convert to PDF instead of HTML
pdf_save_options = SaveOptions()
pdf_save_options.resource_handling_options = resource_options
pdf_save_options.format = "PDF"   # specify desired format

doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_save_options)
```

Basta substituir a propriedade `format` por `"PNG"`, `"JPEG"` ou `"DOCX"` e você terá um pipeline de conversão completo. As mesmas regras de **aplicação de tratamento de recursos** permanecem intactas, de modo que o PDF resultante não incorporará todos os arquivos CSS externos do site original — apenas aqueles dentro da profundidade de três níveis que você definiu.

---

## Aplicando Tratamento de Recursos a Recursos Aninhados

Vamos aprofundar um pouco mais em **aplicação de tratamento de recursos** de forma eficaz. Suponha que seu HTML contenha uma folha de estilo que, por sua vez, importe outras folhas de estilo, cada uma trazendo imagens. Sem um limite de profundidade, o Aspose.HTML poderia seguir a cadeia indefinidamente, inflando o uso de memória e CPU.

```python
# Example: limit to 1 level for aggressive trimming
resource_options.max_handling_depth = 1
save_options.resource_handling_options = resource_options
doc.save("trimmed_page.html", save_options)
```

- **Profundidade 0** – Nenhum recurso externo é buscado; você obtém um esqueleto HTML básico.  
- **Profundidade 1** – Apenas recursos de primeira ordem (tags `<img>` diretas, arquivos CSS imediatos) são incluídos.  
- **Profundidade 2+** – Aninhamentos mais profundos são respeitados, útil para sites complexos onde estilos dependem de outros estilos.

Escolha a profundidade que corresponde ao seu cenário de **converter uma página HTML grande**. Para newsletters por e‑mail, profundidade 1 costuma ser suficiente. Para um arquivo local, profundidade 3 (como no exemplo principal) oferece um bom equilíbrio.

---

## Exemplo Completo – Do Início ao Fim

Abaixo está um script autônomo que você pode colocar em um arquivo chamado `process_html.py`. Ele inclui tratamento de erros, registro de logs e um pequeno helper que imprime a redução de tamanho que você alcançou.

```python
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

def process_html(
    src_path: str,
    dst_path: str,
    depth: int = 3,
    fmt: str = "HTML"
) -> None:
    """
    Loads an HTML file, applies resource handling, and saves it in the requested format.
    Returns nothing; prints size statistics for quick verification.
    """
    if not os.path.isfile(src_path):
        raise FileNotFoundError(f"Source file not found: {src_path}")

    # Load document
    doc = HTMLDocument(src_path)

    # Set up resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = depth

    # Configure save options (including format)
    save_opts = SaveOptions()
    save_opts.resource_handling_options = res_opts
    save_opts.format = fmt.upper()   # Aspose expects upper‑case format strings

    # Perform save / conversion
    doc.save(dst_path, save_opts)

    # Report size change
    original = os.path.getsize(src_path)
    final = os.path.getsize(dst_path)
    reduction = (original - final) / original * 100
    print(f"Saved {fmt.lower()} to '{dst_path}'. Size reduced by {reduction:.2f}%.")

# -------------------------------------------------------------------------
# Example usage
if __name__ == "__main__":
    input_file = "YOUR_DIRECTORY/big_page.html"
    output_file = "YOUR_DIRECTORY/big_page_processed.html"

    process_html(
        src_path=input_file,
        dst_path=output_file,
        depth=3,          # apply resource handling up to three levels
        fmt="HTML"       # change to "PDF" or "PNG" to convert format
    )
```

**Saída esperada (console):**

```
Saved html to 'YOUR_DIRECTORY/big_page_processed.html'. Size reduced by 42.57%.
```

Abra o arquivo processado; você verá uma página mais leve que ainda se parece com a original. Se você alterou `fmt` para `"PDF"`, o console mostrará o tamanho do arquivo PDF e você poderá abri‑lo em qualquer visualizador de PDF.

---

## Perguntas Frequentes & Casos Limítrofes

- **E se a página referenciar recursos via HTTPS que exigem autenticação?**  
  Aspose.HTML segue redirecionamentos, mas não envia credenciais automaticamente. Você pode pré‑baixar esses ativos ou usar um manipulador `WebRequest` personalizado (fora do escopo deste guia).

- **Posso preservar CSS inline enquanto removo arquivos externos?**  
  Sim — defina `resource_options.max_handling_depth = 0`. Isso ignora arquivos externos, mas mantém quaisquer blocos `<style>` intactos.

- **E quanto a imagens muito grandes que ainda aumentam o tamanho da saída?**  
  Após salvar, você pode executar uma passagem secundária com Pillow para reduzir as imagens, ou deixar que as opções de compressão de imagem integradas do Aspose.HTML façam isso (use `save_options.image_quality`).

- **O limite de profundidade é aplicado por tipo de recurso?**  
  O limite é global para todos os tipos de recurso (imagens, scripts, estilos). Se precisar de controle granular, será necessário filtrar os recursos manualmente após carregar o documento.

---

## Conclusão

Agora você tem uma compreensão sólida de **como usar SaveOptions** no Aspose.HTML

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Converter HTML para PDF em Java – Usando Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Como Converter HTML para MHTML com Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [Como Usar Aspose para Renderizar HTML em PNG – Guia Passo a Passo](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}