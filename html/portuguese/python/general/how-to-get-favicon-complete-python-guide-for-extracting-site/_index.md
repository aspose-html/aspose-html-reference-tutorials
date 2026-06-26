---
category: general
date: 2026-06-26
description: Aprenda como obter o favicon carregando o HTML a partir de uma URL e
  extraindo o href das tags <link>. Código Python passo a passo para obter ícones
  de sites rapidamente.
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: pt
og_description: 'Como obter o favicon rapidamente: carregue o HTML a partir da URL,
  encontre a tag <link rel=''icon''> e extraia o href das tags <link> usando Python.'
og_title: Como obter favicon – Tutorial de Python
schemas:
- author: Aspose
  dateModified: '2026-06-26'
  description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  headline: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  type: TechArticle
- description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  name: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  steps:
  - name: What if the site uses a `<meta>` tag instead of `<link>`?
    text: Some older pages embed the icon URL in a `<meta name="msapplication‑TileImage">`.
      You can extend `find_icon_links` to also search for those meta tags and treat
      them the same way.
  - name: How do I handle relative URLs that start with `//`?
    text: '`urljoin` automatically resolves protocol‑relative URLs (`//example.com/favicon.ico`)
      based on the scheme of the base URL, so you don’t need extra logic.'
  - name: Can I retrieve multiple sizes (e.g., 32×32, 180×180) automatically?
    text: Yes—just drop the `filter_ico_urls` step. The script will return every icon
      URL it discovers, including PNGs of various dimensions. You can then sort or
      select based on the filename pattern.
  - name: Does this work on sites that block bots?
    text: 'If a site returns a 403 or requires a custom User‑Agent, tweak the `requests.get`
      call:'
  type: HowTo
tags:
- Python
- Web Scraping
- HTML Parsing
title: Como obter o favicon – Guia completo em Python para extrair ícones de sites
url: /pt/python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como obter Favicon – Guia Completo em Python para Extrair Ícones de Sites

Já se perguntou **como obter favicon** de qualquer site sem vasculhar o código-fonte da página manualmente? Você não é o único — desenvolvedores, profissionais de SEO e até designers frequentemente precisam do pequeno ícone que representa um site. Neste tutorial, mostraremos uma forma limpa, centrada em Python, de carregar HTML a partir de uma URL, localizar as tags `<link rel="icon">` e extrair as URLs dos ícones. Ao final, você saberá exatamente **como obter favicon** para qualquer domínio e terá um script reutilizável pronto para seus projetos.

Cobriremos tudo, desde a obtenção do HTML até o tratamento de casos especiais como URLs relativas e múltiplos formatos de ícone. Nenhum serviço externo é necessário — apenas a biblioteca padrão `requests` e um analisador HTML leve. Pronto para começar? Vamos mergulhar.

## Pré‑requisitos

- Python 3.8+ instalado (o código também funciona em 3.10)  
- Familiaridade básica com `requests` e list comprehensions  
- Acesso à internet para o site alvo  

Se você já tem isso, ótimo — pule para o primeiro passo. Caso contrário, instale a única dependência que precisamos:

```bash
pip install requests beautifulsoup4
```

> **Dica profissional:** `beautifulsoup4` é um analisador testado em batalha que torna “load html from url” muito fácil.

## Etapa 1: Carregar HTML a partir da URL com Python  

A primeira coisa que você precisa fazer ao aprender **como obter favicon** é buscar o código-fonte da página. Esta é a parte de “load html from url” do processo.

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

Por que usar `requests`? Ele lida com redirecionamentos, verificação de HTTPS e timeouts automaticamente, o que significa menos surpresas quando você tentar **obter ícones de sites** mais tarde.

## Etapa 2: Analisar o Documento e Encontrar Links de Ícone  

Agora que temos o HTML, precisamos localizar todos os elementos `<link>` cujo atributo `rel` indica um ícone. Este é o coração de **como obter favicon**.

```python
def find_icon_links(html: str) -> list[BeautifulSoup]:
    """Return a list of <link> tags that declare an icon."""
    soup = BeautifulSoup(html, "html.parser")
    # Look for rel="icon" or rel="shortcut icon"
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]
```

Observe que verificamos tanto `icon` quanto `shortcut icon` porque sites mais antigos ainda usam este último. Essa pequena nuance costuma confundir as pessoas quando pesquisam “como extrair favicons”.

## Etapa 3: Extrair href dos Elementos Link  

Com as tags relevantes em mãos, o próximo passo lógico — **extrair href do link** — é simples.

```python
from urllib.parse import urljoin

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    """Convert each <link> tag’s href into a full absolute URL."""
    urls = []
    for tag in link_tags:
        href = tag.get("href")
        if href:
            # Resolve relative URLs against the base page
            full_url = urljoin(base_url, href)
            urls.append(full_url)
    return urls
```

Usar `urljoin` garante que, mesmo que um site forneça um caminho relativo como `/favicon.ico`, você obterá uma URL absoluta correta — essencial para um script confiável de **como obter favicon**.

## Etapa 4: Opcional – Validar e Filtrar URLs de Ícones  

Às vezes, uma página lista muitos ícones (Apple touch icons, PNGs de vários tamanhos, etc.). Se você se importa apenas com o clássico arquivo `.ico`, filtre adequadamente. Esta etapa mostra **como extrair favicons** de um tipo específico.

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

Sinta-se à vontade para ajustar o filtro: substitua `".ico"` por `".png"` ou verifique `rel="apple-touch-icon"` se precisar de ícones de alta resolução.

## Etapa 5: Baixar os Arquivos de Ícone (Se Você Quiser a Imagem Real)  

Extrair as URLs é metade da batalha; baixar fornece um arquivo que você pode exibir ou armazenar. Aqui está um ajudante rápido:

```python
import os

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    """Save each icon to *folder*, creating it if necessary."""
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")
```

Executar isso após as etapas anteriores lhe dará uma cópia local de cada favicon descoberto, perfeito para cache ou análise offline.

## Etapa 6: Juntando Tudo – Exemplo Completo e Funcional  

Abaixo está o script completo, pronto‑para‑executar, que demonstra **como obter favicon** de qualquer site. Copie‑e‑cole, altere o `target_url` e veja o resultado.

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
import os

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def find_icon_links(html: str) -> list[BeautifulSoup]:
    soup = BeautifulSoup(html, "html.parser")
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    return [urljoin(base_url, tag.get("href")) for tag in link_tags if tag.get("href")]

def filter_ico_urls(urls: list[str]) -> list[str]:
    return [u for u in urls if u.lower().endswith(".ico")]

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")

def get_favicons(target_url: str) -> None:
    print(f"Fetching HTML from {target_url} …")
    html = fetch_html(target_url)

    print("Finding <link> tags that declare icons …")
    icon_tags = find_icon_links(html)

    print(f"Extracting href attributes – {len(icon_tags)} candidates found.")
    raw_urls = extract_icon_urls(target_url, icon_tags)

    # Optional filtering – keep only .ico files
    ico_urls = filter_ico_urls(raw_urls)
    print(f"Filtered to {len(ico_urls)} .ico URLs:", ico_urls)

    if ico_urls:
        download_icons(ico_urls)
    else:
        print("No .ico favicons detected; here are all discovered URLs:")
        print(raw_urls)

# Example usage – replace with any site you want to test
if __name__ == "__main__":
    target_url = "https://www.python.org"
    get_favicons(target_url)
```

**Saída esperada (truncada para brevidade):**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

Se o site fornecer apenas PNG ou Apple touch icons, o script listará essas URLs em vez disso, mostrando exatamente **como obter favicon** em todos os cenários.

## Perguntas Frequentes & Casos Especiais  

### E se o site usar uma tag `<meta>` em vez de `<link>`?  
Algumas páginas antigas incorporam a URL do ícone em uma `<meta name="msapplication‑TileImage">`. Você pode estender `find_icon_links` para também buscar essas meta tags e tratá‑las da mesma forma.

### Como lidar com URLs relativas que começam com `//`?  
`urljoin` resolve automaticamente URLs relativas ao protocolo (`//example.com/favicon.ico`) com base no esquema da URL base, portanto você não precisa de lógica extra.

### Posso recuperar múltiplos tamanhos (ex.: 32×32, 180×180) automaticamente?  
Sim — basta remover a etapa `filter_ico_urls`. O script retornará todas as URLs de ícones que encontrar, incluindo PNGs de várias dimensões. Você pode então ordenar ou selecionar com base no padrão do nome do arquivo.

### Isso funciona em sites que bloqueiam bots?  
Se um site retornar 403 ou exigir um User‑Agent customizado, ajuste a chamada `requests.get`:

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

Essa pequena mudança costuma resolver “como obter favicon” em domínios mais restritos.

## Visão Geral Visual  

![Diagrama mostrando o fluxo de como obter favicon de um site – carregar HTML, analisar tags link, extrair href, download opcional](how-to-get-favicon-diagram.png "diagrama do fluxo de como obter favicon")

*O texto alternativo da imagem contém a palavra‑chave principal, atendendo ao SEO para imagens.*

## Conclusão  

Percorremos **como obter favicon** passo a passo: carregando HTML a partir de uma URL,

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Salvar HTML em C# – Guia Completo Usando um Manipulador de Recursos Personalizado](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Como Editar HTML Usando Aspose.HTML para Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Como Converter HTML para PDF em Java – Usando Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}