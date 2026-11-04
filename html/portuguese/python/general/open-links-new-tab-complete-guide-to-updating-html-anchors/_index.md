---
category: general
date: 2026-07-05
description: Abrir links em nova aba usando Python – aprenda como adicionar target="_blank",
  mudar o alvo do link, usar seletor de atributo contém e salvar o HTML modificado
  sem esforço.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: pt
og_description: Abra links em nova aba rapidamente. Este tutorial mostra como adicionar
  target="_blank", alterar o destino do link e salvar o HTML modificado com Python.
og_title: Abrir links em nova aba – Guia passo a passo de atualização de HTML
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: Abrir links em nova aba – Guia completo para atualizar âncoras HTML
url: /pt/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Abrir Links em Nova Aba – Guia Completo para Atualizar Âncoras HTML

Já precisou **abrir links em nova aba** em uma página HTML estática, mas não sabia por onde começar? Você não está sozinho. Muitos desenvolvedores encontram esse obstáculo ao limpar sites legados ou adicionar ajustes de acessibilidade. Neste tutorial, vamos percorrer uma solução prática que **adiciona target blank**, **altera o alvo do link** e salva **html modificado** com segurança — tudo com algumas linhas de Python.

Também abordaremos como usar um **seletor de atributo contém** para que você toque apenas nas âncoras que realmente importam (por exemplo, todo link que aponta para *example.com*). Ao final, você terá um script reutilizável que pode ser inserido em qualquer projeto, independentemente do tamanho.

## O Que Você Vai Aprender

- Carregar um arquivo HTML em um objeto de documento manipulável.  
- Selecionar elementos `<a>` cujo atributo `href` contém uma substring específica.  
- **Adicionar target blank** e definir o atributo `rel="noopener"` para melhorar a segurança.  
- **Salvar html modificado** de volta ao disco sem perder a formatação.  

Sem dependências externas além da biblioteca padrão e **beautifulsoup4** (uma instalação mínima). Se você já usa outro parser, os conceitos se aplicam diretamente.

---

## Pré‑requisitos

- Python 3.8+ instalado na sua máquina.  
- Familiaridade básica com HTML e Python.  
- Pacote `beautifulsoup4` (`pip install beautifulsoup4`).  

É só isso — nenhum framework pesado necessário.

---

## Etapa 1: Carregar o Documento HTML

Primeiro de tudo: precisamos ler o arquivo fonte e entregá‑lo ao BeautifulSoup. Pense nisso como abrir uma tela em branco onde você pode desenhar novos atributos.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Por que isso importa:** Usar `Path` mantém o código independente do SO, e `html.parser` já vem incluído, então você não precisa de parsers extras para tarefas simples.

---

## Etapa 2: Usar um Seletor de Atributo Contém para Encontrar os Links Certos

Queremos tocar apenas nas âncoras que apontam para *example.com*. O seletor CSS `a[href*='example.com']` faz exatamente isso — `*=` significa “contém”. O método `select` do BeautifulSoup entende essa sintaxe.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Dica profissional:** Se precisar de uma correspondência sem distinção entre maiúsculas e minúsculas, troque por um pequeno loop que verifica `if 'example.com' in a.get('href', '').lower()`.

Agora `anchor_elements` contém todos os links que nos interessam, prontos para a próxima transformação.

---

## Etapa 3: Alterar o Alvo do Link – Adicionar Target Blank e Proteger o Link

Abrir um link em nova aba é tão simples quanto definir `target="_blank"`. Contudo, navegadores modernos recomendam também adicionar `rel="noopener"` (ou `noreferrer`) para impedir que a página recém‑aberta acesse a janela original via `window.opener`. Esse pequeno ajuste de segurança pode impedir ataques de phishing.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Por que usamos atribuição direta de dicionário:** Ela cria automaticamente o atributo caso esteja ausente e o sobrescreve se já existir — perfeito para uma operação de **alterar alvo do link**.

---

## Etapa 4: Salvar o HTML Modificado de Volta ao Disco

A etapa final é escrever a marcação atualizada em um novo arquivo. Manter o original intacto permite reverter caso algo dê errado.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **O que `prettify()` faz:** Formata o HTML com identação agradável, tornando o arquivo salvo mais fácil de ler e comparar depois. Se preferir o espaçamento original, substitua `prettify()` por `str(soup)`.

---

## Script Completo – Solução de Um Clique

Abaixo está o script completo, pronto para ser executado. Salve‑o como `update_links.py` e execute `python update_links.py` no seu terminal.

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### Resultado Esperado

Suponha que `links.html` originalmente contenha:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Após executar o script, `links-updated.html` ficará assim:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Somente o link para *example.com* recebeu os atributos **add target blank**, demonstrando que nosso **attribute contains selector** funcionou exatamente como esperado.

---

## Perguntas Frequentes & Casos de Borda

### E se um link já possuir um atributo `rel`?

Nosso loop o sobrescreve com `"noopener"`. Se precisar preservar valores existentes (por exemplo, `"nofollow"`), concatene em vez de substituir:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### Como lidar com múltiplos domínios?

Basta expandir a lista de seletores:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### `prettify()` altera a estrutura original do HTML?

Ele re‑indenta, mas não altera a ordem das tags nem os valores dos atributos. Se precisar manter exatamente o espaçamento original, substitua `prettify()` por `str(soup)` como mencionado anteriormente.

---

## Dicas Profissionais para Scripts Prontos para Produção

- **Backup antes de sobrescrever:** Adicione um passo de cópia (`shutil.copy`) para manter o arquivo original seguro.  
- **Logging em vez de print:** Use o módulo `logging` para projetos escaláveis.  
- **Processamento em lote:** Percorra um diretório com `Path.rglob("*.html")` para atualizar muitos arquivos de uma vez.  

Esses ajustes transformam um simples script de **open links new tab** em uma ferramenta robusta para qualquer fluxo de manutenção web.

---

## Conclusão

Agora você tem um método sólido e reutilizável para **open links new tab** em qualquer coleção de HTML estático. Ao aproveitar um **attribute contains selector**, você pode **change link target** exatamente onde precisar, **add target blank**, e **save modified html** sem perder a formatação.

Teste em uma página de exemplo, depois escale para todo o seu site. Precisa ajustar o seletor para PDFs, imagens ou outros domínios? Basta mudar a string CSS — o resto permanece igual.

Sinta‑se à vontade para deixar um comentário se encontrar algum detalhe inesperado, ou compartilhar como você estendeu o script para seus próprios projetos. Boa codificação, e que todas as suas âncoras abram exatamente onde você deseja!

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui código completo e exemplos passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}