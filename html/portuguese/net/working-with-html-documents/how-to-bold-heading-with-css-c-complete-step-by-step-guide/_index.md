---
category: general
date: 2026-01-01
description: Como deixar o título em negrito e aplicar estilo itálico usando C# e
  CSS. Aprenda a definir o peso da fonte do título, aplicar negrito e itálico e estilizar
  títulos rapidamente.
draft: false
keywords:
- how to bold heading
- how to apply italic
- apply bold and italic
- how to apply bold
- set heading font weight
language: pt
og_description: Como colocar negrito no título na primeira frase, depois aprender
  a aplicar itálico, combinar negrito e itálico e definir o peso da fonte do título
  com exemplos claros.
og_title: Como deixar o título em negrito – Guia completo para CSS e C#
tags:
- CSS
- C#
- Web Development
title: Como deixar o título em negrito com CSS e C# – Guia completo passo a passo
url: /pt/net/working-with-html-documents/how-to-bold-heading-with-css-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como deixar o título em negrito – Guia completo para CSS & C#

Já se perguntou **como deixar o título em negrito** em uma página web sem ter que vasculhar documentos intermináveis? Você não está sozinho. A maioria dos desenvolvedores se depara com esse problema quando precisam de um ajuste visual rápido, especialmente quando estão combinando HTML, CSS e um pouco de C# para controlar a interface.

Neste tutorial vamos percorrer um exemplo completo e executável que mostra exatamente como aplicar negrito, itálico e estilos combinados a um elemento `<h1>`. Ao longo do caminho também abordaremos **como aplicar itálico**, como **aplicar negrito e itálico** juntos, e a sutil diferença entre usar CSS `font-weight` versus a API de baixo nível `WebFontStyle`. Ao final, você será capaz de **definir o peso da fonte do título** com confiança, independentemente da stack que estiver usando.

## Pré-requisitos

- .NET 6+ (ou .NET Framework 4.8 se preferir)
- Visual Studio 2022 ou qualquer IDE compatível com C#
- Conhecimento básico de HTML e CSS
- Um projeto simples WinForms ou WPF que hospeda um controle WebView2 (o exemplo usa WinForms)

Se algum desses itens lhe for desconhecido, não entre em pânico – vamos apontar o código mínimo que você precisa, e você pode copiar‑colar direto em um novo projeto.

---

## Etapa 1: Criar uma página HTML mínima

Primeiro, precisamos de um arquivo HTML que o controle WebView2 possa carregar. Salve o seguinte como `index.html` na pasta de saída do seu projeto (por exemplo, `bin\Debug\net6.0-windows`).

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Heading Styling Demo</title>
    <style>
        /* Default styling – we’ll override this from C# */
        h1 {
            font-family: 'Arial', sans-serif;
            font-weight: normal;
            font-style: normal;
        }
    </style>
</head>
<body>
    <h1 id="title">Dynamic Heading</h1>
    <p>Open the C# console or UI to see the heading change.</p>
</body>
</html>
```

> **Por que isso importa:** Manter o CSS minimalista nos dá uma base limpa para que possamos ver exatamente o que o código C# faz. O atributo `id="title"` facilita a seleção do título a partir do script.

---

## Etapa 2: Configurar o projeto WinForms com WebView2

Crie um novo **Windows Forms App** (`.NET 6`) e adicione o pacote NuGet **Microsoft.Web.WebView2**. Arraste um controle `WebView2` para o formulário, nomeie-o `webView` e defina sua propriedade `Dock` como `Fill`.

```csharp
using System;
using System.Windows.Forms;
using Microsoft.Web.WebView2.Core;

namespace HeadingStyler
{
    public partial class MainForm : Form
    {
        public MainForm()
        {
            InitializeComponent();
            InitializeAsync();
        }

        private async void InitializeAsync()
        {
            // Ensure the WebView2 runtime is available
            await webView.EnsureCoreWebView2Async();

            // Load the local HTML file
            var htmlPath = System.IO.Path.Combine(
                AppDomain.CurrentDomain.BaseDirectory, "index.html");
            webView.CoreWebView2.Navigate($"file:///{htmlPath}");
        }
    }
}
```

> **Dica de especialista:** Se a navegação falhar, verifique se `index.html` foi copiado para a pasta de saída (defina *Copy to Output Directory* → *Copy always*).

---

## Etapa 3: Localizar o elemento de título em C#

Depois que a página terminar de carregar, podemos capturar o elemento `<h1>`. A API `CoreWebView2` fornece um método `ExecuteScriptAsync` que executa JavaScript e retorna o resultado. Contudo, para o propósito deste tutorial usaremos o **wrapper DOM de baixo nível** que vem com o WebView2 (disponível via `webView.CoreWebView2`).

```csharp
private async void WebView_NavigationCompleted(
    object sender, CoreWebView2NavigationCompletedEventArgs e)
{
    // Step 1: Locate the heading element you want to style
    var heading = await webView.CoreWebView2
        .ExecuteScriptAsync("document.querySelector('h1');");

    // The script returns a JS object reference we can manipulate.
    // In practice we’ll call methods on it via ExecuteScriptAsync.
}
```

> **Por que fazemos isso:** O acesso direto ao DOM nos permite evitar a injeção de grandes blocos de JavaScript. É mais limpo e demonstra **como aplicar negrito** usando a API WebView2.

---

## Etapa 4: Aplicar estilos de negrito, itálico e combinados

Agora usaremos três abordagens diferentes para estilizar o título:

1. **CSS `font-weight`** – a maneira mais comum, atendendo ao requisito de **definir o peso da fonte do título**.
2. **CSS `font-style`** – como **aplicar itálico**.
3. **`WebFontStyle` flags** – uma alternativa de baixo nível que nos permite **aplicar negrito e itálico** simultaneamente.

```csharp
private async void StyleHeading()
{
    // 1️⃣ Apply a bold weight (700) – classic CSS method
    await webView.CoreWebView2.ExecuteScriptAsync(@"
        var h = document.querySelector('h1');
        h.style.fontWeight = '700';
    ");

    // 2️⃣ Apply italic style – fulfills “how to apply italic”
    await webView.CoreWebView2.ExecuteScriptAsync(@"
        var h = document.querySelector('h1');
        h.style.fontStyle = 'italic';
    ");

    // 3️⃣ Use the low‑level API to combine bold + italic flags
    // This requires the WebFontStyle enumeration from the WebView2 SDK.
    await webView.CoreWebView2.ExecuteScriptAsync(@"
        var h = document.querySelector('h1');
        // The following line mimics WebFontStyle usage in C#
        // Note: This is illustrative; actual flag usage happens in C#
        // h.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
    ");
}
```

> **Explicação:**  
> • `fontWeight = '700'` indica ao navegador que renderize o texto com um peso **negrito**.  
> • `fontStyle = 'italic'` inclina os glifos, atendendo à consulta **como aplicar itálico**.  
> • A linha comentada mostra como você *poderia* definir `WebFontStyle` a partir de C# se possuir um wrapper que exponha o enum. Em um cenário real, você chamaria um método C# no objeto `heading`, por exemplo, `heading.Font.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;`.

Para realmente invocar a API de baixo nível a partir de C#, você precisaria de um wrapper COM interop. Aqui está um exemplo mínimo assumindo que você tem uma referência ao namespace `Microsoft.Web.WebView2.Wpf`:

```csharp
using Microsoft.Web.WebView2.WinForms;
using Microsoft.Web.WebView2.Core;
using System.Runtime.InteropServices;

private async void ApplyWebFontStyle()
{
    var script = @"
        (function() {
            var h = document.querySelector('h1');
            // Expose the element to C#
            return h;
        })();";

    var result = await webView.CoreWebView2.ExecuteScriptAsync(script);
    // The result is a JSON representation; you’d need a proper COM object to set flags.
    // For brevity, the example focuses on the CSS path which works everywhere.
}
```

> **Conclusão:** Se você está confortável com o modelo COM do WebView2, a abordagem de flags oferece controle granular. Caso contrário, a rota CSS é perfeitamente adequada e funciona em todos os navegadores.

---

## Etapa 5: Juntar tudo – Exemplo completo funcional

Abaixo está um único arquivo `MainForm.cs` que compila e executa. Ele carrega o HTML e, em seguida, estiliza o título assim que a navegação é concluída.

```csharp
using System;
using System.Windows.Forms;
using Microsoft.Web.WebView2.Core;

namespace HeadingStyler
{
    public partial class MainForm : Form
    {
        public MainForm()
        {
            InitializeComponent();
            webView.NavigationCompleted += WebView_NavigationCompleted;
            InitializeAsync();
        }

        private async void InitializeAsync()
        {
            await webView.EnsureCoreWebView2Async();
            var htmlPath = System.IO.Path.Combine(
                AppDomain.CurrentDomain.BaseDirectory, "index.html");
            webView.CoreWebView2.Navigate($"file:///{htmlPath}");
        }

        private async void WebView_NavigationCompleted(
            object sender, CoreWebView2NavigationCompletedEventArgs e)
        {
            // Apply the three styling techniques
            await webView.CoreWebView2.ExecuteScriptAsync(@"
                var h = document.querySelector('h1');
                h.style.fontWeight = '700';   // bold
                h.style.fontStyle = 'italic'; // italic
                // For low‑level API, you’d use:
                // h.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
            ");
        }
    }
}
```

### Saída esperada

Quando você executar o aplicativo, a janela exibirá:

- **“Dynamic Heading”** renderizado em **negrito** (peso 700) e **itálico**.
- O parágrafo ao redor permanece inalterado.
- Se você inspecionar o elemento (Ctrl + Shift + I), verá os estilos inline aplicados.

---

## Perguntas comuns e casos de borda

### 1️⃣ *E se o título já tiver uma classe?*  
Você pode adicionar uma classe via `classList.add('my‑bold‑italic')` e definir os estilos em uma folha de estilos, ou continuar usando estilos inline como mostrado. Estilos inline são vantajosos quando você precisa de uma mudança rápida e pontual.

### 2️⃣ *Todos os navegadores respeitam `font-weight: 700`?*  
Sim, 700 corresponde ao peso **Bold** na especificação CSS. Se a família de fontes não fornecer uma variante em negrito, o navegador a sintetizará, o que pode parecer ligeiramente borrado. Por isso, recomenda‑se usar uma família de fontes com uma variante verdadeira em negrito (por exemplo, Arial).

### 3️⃣ *Posso animar a transição de normal para negrito?*  
Com certeza. Adicione uma transição CSS:

```css
h1 {
    transition: font-weight 0.3s ease, font-style 0.3s ease;
}
```

Então alterne os estilos a partir de C# e observe a animação suave.

### 4️⃣ *E quanto à acessibilidade?*  
Negrito e itálico são pistas visuais, não semânticas. Para leitores de tela, considere adicionar `aria-label` ou usar uma hierarquia de títulos adequada (`<h1>` → `<h2>`) para transmitir importância.

---

## Dicas profissionais e armadilhas

- **Dica de especialista:** Mantenha seu CSS em um arquivo separado e use C# apenas para alternar classes. Isso torna a lógica da UI mais limpa e fácil de manter.
- **Cuidado com:** Sobrescrever estilos do agente de usuário. Alguns navegadores aplicam `font-weight: bold` padrão a tags `<strong>`; evite misturá‑los com estilos manuais a menos que deseje.
- **Nota de desempenho:** Alterações de estilo inline são baratas, mas se você planeja estilizar dezenas de elementos, agrupe‑as em uma única chamada de script para reduzir idas‑e‑voltas.

---

## Conclusão

Cobrimos tudo o que você precisa saber sobre **como deixar o título em negrito** e **como aplicar itálico**, além do truque para **aplicar negrito e itálico** juntos e **definir o peso da fonte do título** programaticamente a partir de C#. Usando uma pequena página HTML, um host WinForms WebView2 e algumas chamadas `ExecuteScriptAsync`,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}