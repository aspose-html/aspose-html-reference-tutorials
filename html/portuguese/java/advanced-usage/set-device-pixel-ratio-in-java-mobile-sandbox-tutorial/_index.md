---
category: general
date: 2026-02-10
description: Defina a proporção de pixels do dispositivo em Java usando o sandbox
  Aspose.HTML. Aprenda como definir a largura e a altura da tela e obter o título
  da página em Java com um exemplo completo e executável.
draft: false
keywords:
- set device pixel ratio
- get page title java
- set screen width height
language: pt
og_description: Defina a proporção de pixels do dispositivo em Java com o sandbox
  Aspose.HTML. Este guia mostra como definir a largura e a altura da tela e obter
  o título da página em Java em alguns passos simples.
og_title: Definir a proporção de pixels do dispositivo em Java – Tutorial Mobile Sandbox
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: definir a proporção de pixels do dispositivo em Java – Tutorial Mobile Sandbox
url: /pt/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# definir taxa de pixel do dispositivo em Java – Tutorial de Sandbox Móvel

Já precisou **definir taxa de pixel do dispositivo** ao testar um site responsivo em Java? Você não está sozinho. Muitos desenvolvedores se deparam com um obstáculo quando a página parece perfeita no desktop, mas quebra em telefones de alta DPI. A boa notícia? Com o sandbox do Aspose.HTML você pode emular um iPhone X (ou qualquer dispositivo) diretamente do seu código Java — sem necessidade de navegador.

Neste guia, vamos percorrer **como definir largura e altura da tela**, configurar a **taxa de pixel do dispositivo**, e finalmente **obter título da página java** para verificar se tudo foi renderizado corretamente. Ao final, você terá um programa autônomo que pode inserir em qualquer projeto e começar a testar layouts móveis instantaneamente.

## Pré-requisitos

- Java 8 ou mais recente (o código também compila com JDK 11)  
- Biblioteca Aspose.HTML for Java (versão 23.7 ou posterior) – você pode obtê-la do Maven Central  
- Uma IDE ou uma configuração simples de linha de comando `javac`  
- Acesso à internet para a URL de demonstração (`https://responsive.example.com`)

Sem frameworks extras, sem Selenium, apenas Java puro e Aspose.HTML.

---

## Etapa 1: Definir largura e altura da tela e taxa de pixel do dispositivo

A primeira coisa que precisamos é um objeto `SandboxOptions` que informa ao sandbox qual “dispositivo” estamos simulando. Aqui usaremos as dimensões do iPhone X (375 × 812 pixels CSS) e uma **taxa de pixel do dispositivo** de 3.0, que reproduz a tela retina de alta DPI.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Por que isso importa:**  
> A chamada `setDevicePixelRatio` escala tudo — de imagens ao renderização de fontes — para que a página pense que está em um telefone real. Se você pular isso, o layout pode recair para consultas de mídia CSS no estilo desktop, frustrando o objetivo do teste móvel.

---

## Etapa 2: Criar a instância do sandbox

Agora transformamos essas opções em um sandbox ativo. Pense no sandbox como um pequeno navegador headless que respeita as dimensões e a taxa de pixel que definimos.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Dica profissional:** Você pode reutilizar o mesmo objeto `Sandbox` para múltiplos carregamentos de página; basta mudar a URL e o sandbox manterá as mesmas características do dispositivo.

---

## Etapa 3: Carregar a página dentro do sandbox

Com o sandbox pronto, carregar uma página é tão simples quanto construir um `HTMLDocument` e passar o sandbox como segundo argumento. Isso força o documento a renderizar usando o dispositivo virtual que definimos anteriormente.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Se a URL estiver inacessível ou a página contiver erros, o Aspose.HTML lançará uma exceção. Para código de produção, você provavelmente envolveria isso em um `try‑catch` e registraria a falha, mas para o tutorial mantemos simples.

---

## Etapa 4: Verificar com get page title java

A verificação de sanidade mais rápida é ler o título do documento. Se o sandbox aplicou corretamente a **taxa de pixel do dispositivo**, o título será idêntico ao que você veria em um iPhone X real.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Saída esperada (exemplo):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Se você vir o título impresso, você definiu com sucesso a **taxa de pixel do dispositivo**, **definiu largura e altura da tela**, e **obteve o título da página** usando Java.

---

## Exemplo Completo e Executável

Abaixo está o programa completo que você pode copiar‑colar em um arquivo chamado `SandboxDemo.java`. Certifique‑se de que os JARs do Aspose.HTML estejam no seu classpath (flag `-cp`) antes de compilar.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.net.URL;

/**
 * Demonstrates how to set device pixel ratio, set screen width height,
 * and get page title java using Aspose.HTML sandbox.
 */
public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define device characteristics ----------
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixels width
        sandboxOptions.setScreenHeight(812);         // CSS pixels height
        sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI screen factor (set device pixel ratio)

        // ---------- Step 2: Create the sandbox ----------
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // ---------- Step 3: Load a web page inside the sandbox ----------
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("https://responsive.example.com"), mobileSandbox);

        // ---------- Step 4: Verify the document loaded correctly ----------
        System.out.println("Title under sandbox: " + htmlDoc.getTitle());
    }
}
```

Compile e execute:

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

Você deverá ver o título impresso no console, confirmando que a página foi renderizada com a **taxa de pixel do dispositivo** desejada.

---

## Perguntas Frequentes & Casos Limite

| Pergunta | Resposta |
|----------|----------|
| **Posso mudar a taxa de pixel em tempo de execução?** | Sim — basta criar um novo `SandboxOptions` com um valor diferente em `setDevicePixelRatio` e instanciar um novo `Sandbox`. Reutilizar o mesmo sandbox após alterar suas opções não é suportado. |
| **E se eu precisar testar vários dispositivos?** | Percorra uma lista de `SandboxOptions` (por exemplo, iPhone 8, Pixel 4) e execute a mesma lógica de carregamento e título para cada um. |
| **Isso funciona com sites HTTPS que têm certificados autoassinados?** | O Aspose.HTML respeita o repositório de confiança SSL padrão do Java. Adicione o certificado ao keystore da JVM ou desative a verificação apenas para testes (não recomendado para produção). |
| **Como capturo uma captura de tela em vez de apenas o título?** | A API `HTMLDocument` fornece métodos `save` que podem exportar a página renderizada para PNG ou JPEG. Use `htmlDoc.save("output.png", SaveFormat.PNG);` após o carregamento. |
| **O sandbox é thread‑safe?** | Cada instância `Sandbox` é isolada, mas você deve evitar compartilhar uma única instância entre múltiplas threads sem sincronização. |

---

## Visão Geral Visual

![Diagrama mostrando a definição da taxa de pixel do dispositivo no sandbox móvel](https://example.com/images/sandbox-diagram.png "diagrama da taxa de pixel do dispositivo")

*A ilustração acima mapeia o fluxo desde a configuração de `SandboxOptions` (incluindo **definir largura e altura da tela** e **definir taxa de pixel do dispositivo**) até o carregamento de uma URL e a extração do título.*

---

## Conclusão

Agora você sabe **como definir a taxa de pixel do dispositivo** em Java, como **definir largura e altura da tela** para emulação móvel precisa, e como **obter título da página java** para confirmar que a renderização foi bem‑sucedida. Esse fluxo de trabalho compacto elimina a necessidade de navegadores pesados durante testes automatizados de UI e se encaixa perfeitamente em pipelines de CI.

Pronto para o próximo passo? Tente exportar a página renderizada como uma imagem, ou experimente depurar consultas de mídia CSS alternando o `devicePixelRatio` entre 1.0 e 3.0. Você também pode explorar os recursos de conversão para PDF do Aspose.HTML para capturar uma versão imprimível da visualização móvel.

Feliz codificação, e que seus layouts móveis estejam sempre nítidos — independentemente da densidade de pixels!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}