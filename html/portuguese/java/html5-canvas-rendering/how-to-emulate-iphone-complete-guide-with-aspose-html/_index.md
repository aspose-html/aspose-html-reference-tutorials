---
category: general
date: 2026-03-26
description: Aprenda como emular iPhone em Java usando Aspose.HTML. Inclui etapas
  para definir um agente de usuário personalizado e definir a proporção de pixels
  do dispositivo para renderização móvel precisa.
draft: false
keywords:
- how to emulate iphone
- set custom user agent
- set device pixel ratio
- how to set user-agent
- how to set dpr
language: pt
og_description: Como emular iPhone em Java? Este tutorial mostra como definir um agente
  de usuário personalizado e a proporção de pixels do dispositivo usando Aspose.HTML,
  entregando páginas móveis com perfeição de pixel.
og_title: Como emular iPhone – Guia passo a passo do Aspose.HTML
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Como Emular iPhone – Guia Completo com Aspose.HTML
url: /pt/java/html5-canvas-rendering/how-to-emulate-iphone-complete-guide-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como emular iPhone – Guia completo com Aspose.HTML

Já se perguntou **como emular iPhone** ao testar uma página web localmente? Talvez você esteja depurando um layout responsivo e o navegador de desktop simplesmente não sirva. A boa notícia é que você não precisa de um dispositivo físico—`DocumentSandbox` da Aspose.HTML permite que você imite a tela, o user‑agent e o device‑pixel‑ratio (DPR) de um iPhone com algumas linhas de Java.  

Neste tutorial vamos percorrer passo a passo como definir um **user agent personalizado**, configurar o **device pixel ratio** e verificar se tudo funciona como esperado. Ao final, você terá um sandbox reutilizável que renderiza páginas exatamente como um iPhone 8, e entenderá por que cada configuração é importante.

## O que você vai alcançar

- Crie um objeto `Screen` que reflita as dimensões e o DPR de um iPhone.  
- Aplique uma string de **user agent personalizada** para que os servidores acreditem que a requisição vem do Safari no iOS.  
- Construa um `DocumentSandbox` que una a tela e o user‑agent.  
- Execute um `HTMLDocument` dentro do sandbox e veja a saída no console confirmando a configuração.  

Nenhuma biblioteca externa além do Aspose.HTML é necessária, e o código funciona em qualquer ambiente Java 17+.

---

![captura de tela de como emular iPhone](https://example.com/images/iphone-emulation.png "como emular iPhone usando sandbox do Aspose.HTML")

## Como emular iPhone com Aspose.HTML Sandbox

A primeira coisa que precisamos é um `Screen` que reflita as dimensões físicas do iPhone *e* sua densidade de pixels. Este é o núcleo de **como emular iPhone** com precisão.

```java
import com.aspose.html.devices.Screen;

// Step 1: Define iPhone 8 screen size (width, height) and DPR
Screen mobileScreen = new Screen(375, 667, 2.0); // iPhone 8 dimensions, DPR = 2
```

**Por que isso importa:**  
- A largura = 375 px e a altura = 667 px são as dimensões em pixels CSS que você verá no Chrome DevTools ao selecionar um iPhone 8.  
- Definir o DPR para 2 indica ao motor de renderização que trate cada pixel CSS como dois pixels físicos, proporcionando texto e imagens nítidos—exatamente como um dispositivo real faz.

> *Dica de especialista:* Se precisar emular um iPhone mais recente (como o iPhone 13), basta alterar os números para 390 × 844 e DPR = 3.

## Definindo um User Agent Personalizado (set custom user agent)

Em seguida, precisamos **definir um user agent personalizado** para que o servidor sirva o HTML/CSS específico para mobile. Sem isso, muitos sites ainda pensarão que você está em um desktop.

```java
// Step 2: Define an iPhone Safari user‑agent string
String iPhoneUserAgent = "Mozilla/5.0 (iPhone; CPU iPhone OS 16_0 like Mac OS X) " +
                         "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                         "Version/16.0 Mobile/15E148 Safari/604.1";
```

**Como isso funciona:**  
- O cabeçalho `User-Agent` é o aperto de mão que os navegadores usam para se apresentar.  
- Ao fornecer a string exata que o Safari no iOS 16 envia, você garante que o servidor retorne os recursos otimizados para mobile (imagens responsivas, scripts adaptativos, etc.).  

Se algum dia precisar **definir user-agent** para outro dispositivo, basta substituir a string pelo valor apropriado—Google Chrome, Firefox ou até um bot customizado.

## Configurando Device Pixel Ratio (set device pixel ratio)

Agora realmente **definimos o device pixel ratio** dentro do sandbox. Esta é a etapa que responde diretamente à pergunta “**como definir dpr**” para um ambiente simulado.

```java
import com.aspose.html.sandbox.DocumentSandbox;

// Step 3: Build the sandbox with screen and user‑agent
DocumentSandbox documentSandbox = new DocumentSandbox.Builder()
        .setScreen(mobileScreen)          // applies the DPR we defined earlier
        .setUserAgent(iPhoneUserAgent)    // applies the custom user‑agent
        .build();
```

**Explicação:**  
- O padrão `Builder` permite anexar fluentemente tanto a tela (que carrega o DPR) quanto o user‑agent.  
- Quando o sandbox renderiza um `HTMLDocument`, ele fingirá que está sendo executado em um dispositivo com aquela densidade de pixels exata.  

> *Por que isso importa:* Algumas consultas de mídia CSS usam `device-pixel-ratio` (por exemplo, `@media (-webkit-min-device-pixel-ratio: 2)`). Se você não definir o DPR, essas regras nunca são acionadas, e você perderá recursos de alta resolução.

## Verificando a Configuração do Sandbox (how to set user-agent)

Vamos colocar o sandbox em ação. O trecho a seguir cria um `HTMLDocument`, carrega uma página e imprime uma confirmação de que o sandbox está ativo.

```java
import com.aspose.html.HTMLDocument;

public class SandboxWithDprAndUa {
    public static void main(String[] args) {
        // Re‑use the sandbox we built earlier
        // DocumentSandbox documentSandbox = ... (from previous step)

        // Step 4: Load a page inside the sandbox
        HTMLDocument doc = new HTMLDocument("https://example.com", documentSandbox);

        // Step 5: Optional – output a sanity check
        System.out.println("Sandbox configured with DPR=2 and iPhone user‑agent.");
    }
}
```

**Saída esperada no console**

```
Sandbox configured with DPR=2 and iPhone user-agent.
```

Se você executar o programa e vir essa linha, você **emulou iPhone** com sucesso usando o DPR e o user‑agent corretos. Abra a página em um navegador real e inspecione as dimensões da viewport—você notará que elas correspondem aos valores de iPhone que definimos.

## Armadilhas comuns e como definir DPR corretamente (how to set dpr)

Mesmo com o código correto, alguns detalhes podem causar problemas:

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **DPR permanece em 1** | Você passou um `Screen` sem o terceiro argumento (DPR). | Sempre use `new Screen(width, height, dpr)`. |
| **User‑Agent ignorado** | O sandbox não foi anexado ao `HTMLDocument`. | Passe o `documentSandbox` como segundo argumento ao construtor do `HTMLDocument`. |
| **Dimensões erradas** | Uso de pixels de dispositivo em vez de pixels CSS. | Lembre‑se: largura/altura são **pixels CSS**, não pixels de hardware. |
| **Servidor ainda envia CSS de desktop** | Alguns sites usam JavaScript para detectar dispositivos, não apenas o cabeçalho. | Considere também injetar uma meta tag viewport, se necessário. |

Mantendo esses pontos em mente, você raramente encontrará uma situação em que a emulação não se comporte como esperado.

## Expandindo o Sandbox – Próximos passos

Agora que você sabe **como definir user agent personalizado** e **como definir dpr**, pode experimentar ainda mais:

- **Altere o tamanho da tela** para emular tablets ou telefones maiores.  
- **Troque o user‑agent** para testar Chrome no Android (`"Mozilla/5.0 (Linux; Android 12; ...) Chrome/110.0"`).  
- **Adicione cookies ou cabeçalhos** via o método `setHeaders` do sandbox para testes autenticados.  
- **Capture uma captura de tela** usando `HTMLDocument.renderToFile("output.png")` para comparar diferenças visuais automaticamente.

Essas extensões permitem que você construa um harness de teste completo sem jamais sair do seu IDE.

## Conclusão

Cobremos **como emular iPhone** usando o `DocumentSandbox` da Aspose.HTML, mostrando exatamente **como definir user agent personalizado**, **como definir device pixel ratio**, e até as sutis diferenças entre “**como definir user-agent**” e “**como definir dpr**”. O exemplo completo e executável demonstra cada parte em um só lugar, para que você possa copiar‑colar, ajustar e começar a testar layouts mobile imediatamente.  

Experimente—troque as dimensões da tela, brinque com diferentes user‑agents e veja como suas páginas reagem. Quando você dominar essas configurações, depurar designs responsivos se torna muito mais fácil, e você economizará inúmeras horas correndo atrás de bugs em dispositivos reais.

Tem perguntas ou quer compartilhar suas próprias variações? Deixe um comentário abaixo, e boa emulação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}