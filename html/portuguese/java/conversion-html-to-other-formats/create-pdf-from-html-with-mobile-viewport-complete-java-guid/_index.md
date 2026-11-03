---
category: general
date: 2026-03-18
description: Crie PDF a partir de HTML em Java rapidamente. Aprenda como converter
  HTML para PDF, simular tela de iPhone e definir o tamanho da tela para PDFs responsivos.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- simulate iphone screen
- how to set screen
- how to convert html
language: pt
og_description: Crie PDF a partir de HTML em Java. Este guia mostra como converter
  HTML em PDF, simular uma tela de iPhone e definir as dimensões da tela para PDFs
  responsivos perfeitos.
og_title: Criar PDF a partir de HTML com viewport móvel – Tutorial Java
tags:
- Java
- Aspose.HTML
- PDF
- Responsive Design
- Mobile Viewport
title: Criar PDF a partir de HTML com Viewport Móvel – Guia Completo de Java
url: /pt/java/conversion-html-to-other-formats/create-pdf-from-html-with-mobile-viewport-complete-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF a partir de HTML com Viewport Mobile – Guia Java Completo

Já precisou **criar PDF a partir de HTML** mas a saída parecia uma página de desktop em uma tela de telefone minúscula? Você não está sozinho. Quando converte um site responsivo para PDF, o viewport padrão costuma ignorar os pontos de interrupção mobile, deixando‑o com uma bagunça apertada.  

A boa notícia? Você pode **converter HTML para PDF** enquanto **simula uma tela de iPhone**, tudo a partir de código Java puro. Neste tutorial vamos percorrer cada passo — como definir o tamanho da tela, como ajustar o fator de escala do dispositivo e por que essas configurações são importantes para um PDF pixel‑perfect.

> **Dica profissional:** Se você já usou Aspose.HTML para conversões simples, descobrirá que os ajustes de viewport estão a apenas algumas linhas extras de distância.

---

## O que você aprenderá

* Como **criar PDF a partir de HTML** usando Aspose.HTML para Java.  
* O código exato para **simular dimensões de tela de iPhone** (375 × 667 px @ 2× densidade).  
* Onde colocar **como definir a tela** nas opções de conversão.  
* Armadilhas comuns ao converter páginas responsivas e como evitá‑las.  
* Um exemplo Java completo, pronto‑para‑executar, que você pode copiar‑colar no seu IDE.

### Pré‑requisitos

* Java 17 ou superior (o código compila em versões anteriores, mas 17 é recomendado).  
* Biblioteca Aspose.HTML para Java – você pode baixar o JAR mais recente no [site da Aspose](https://products.aspose.com/html/java).  
* Um arquivo HTML simples (`input.html`) que você deseja transformar em PDF.  
* Familiaridade básica com Maven ou Gradle (mostraremos um trecho Maven).

---

## Etapa 1 – Adicionar Aspose.HTML ao seu Projeto

Primeiro de tudo, você precisa da biblioteca no seu classpath. Se usar Maven, adicione esta dependência ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **Por que isso importa:** Aspose.HTML cuida do trabalho pesado — analisar HTML, aplicar CSS e rasterizar o layout. Sem ele, você teria que escrever um motor de navegador completo, o que seria *muito* trabalho.

Se preferir Gradle, o equivalente é:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

---

## Etapa 2 – Preparar Load Options e Simular um Viewport de iPhone

Agora vamos configurar os parâmetros de **como definir a tela**. A classe `HtmlLoadOptions` permite dizer ao Aspose qual tamanho e densidade de pixels fingir que o navegador tem.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;

public class ViewportDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create load options for the HTML document
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();

        // 2️⃣ Simulate a mobile viewport (iPhone 6/7/8) – 375 × 667 pixels with retina density
        loadOptions.setScreenSize(new Size(375, 667));
        loadOptions.setDeviceScaleFactor(2.0);

        // 3️⃣ Convert the HTML file to PDF using the configured viewport
        Converter.convertDocument(
                "YOUR_DIRECTORY/input.html",          // source HTML
                "YOUR_DIRECTORY/output.pdf",          // destination PDF
                new PdfSaveOptions(),
                loadOptions);

        // 4️⃣ Notify that the conversion is complete
        System.out.println("Responsive conversion using mobile viewport.");
    }
}
```

### Por que esses números?

* **375 × 667** corresponde às dimensões lógicas de pixels CSS de um iPhone 6/7/8 em modo retrato.  
* **DeviceScaleFactor = 2.0** informa ao renderizador que cada pixel CSS corresponde a dois pixels físicos, imitando a tela Retina.  

Se precisar de outro dispositivo — por exemplo, um iPhone 12 Pro Max — altere o tamanho para `428 × 926` e mantenha o fator de escala em `3.0`.

---

## Etapa 3 – Executar a Conversão e Verificar o Resultado

Compile e execute a classe:

```bash
mvn compile exec:java -Dexec.mainClass=ViewportDemo
```

Depois que o programa terminar, abra `output.pdf`. Você deverá ver:

* Todas as media queries que visam `max-width: 375px` aplicadas corretamente.  
* Imagens renderizadas nítidas graças ao fator de escala 2×.  
* Texto que respeita a hierarquia de tamanhos de fonte mobile que você definiu no CSS.

Se o PDF ainda parecer uma página de desktop, verifique novamente se seu HTML usa meta tags responsivas:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Sem essa tag, mesmo uma configuração de viewport perfeita não acionará a folha de estilos mobile.

---

## Etapa 4 – Manipulando Recursos Externos (Imagens, Fontes, CSS)

Ao **converter HTML para PDF**, o Aspose.HTML tenta buscar cada recurso vinculado. Se você estiver convertendo uma página que reside no sistema de arquivos local, URLs absolutas (`file:///…`) funcionam bem. Para recursos remotos você pode encontrar:

| Problema | Por que acontece | Correção |
|----------|------------------|----------|
| **Erros 404 para imagens** | O HTML aponta para uma URL que requer autenticação. | Use `HtmlLoadOptions.setBaseUrl("file:///C:/myproject/")` para resolver caminhos relativos, ou incorpore imagens como Base64. |
| **Fontes web ausentes** | O motor PDF não consegue baixar o arquivo de fonte. | Baixe os arquivos `.woff`/`.ttf` localmente e referencie‑os com um caminho relativo. |
| **CSS não aplicado** | O arquivo CSS está bloqueado por CORS. | Hospede o CSS em um servidor que permita requisições cross‑origin, ou incorpore o CSS no próprio HTML. |

Uma maneira rápida de testar o carregamento de recursos é envolver a chamada de conversão em um bloco try‑catch e imprimir a mensagem da `Exception`. O Aspose.HTML fornece logs detalhados que apontam a URL exata que falhou.

```java
try {
    Converter.convertDocument(...);
} catch (Exception ex) {
    System.err.println("Conversion failed: " + ex.getMessage());
}
```

---

## Etapa 5 – Ajustes Avançados (Opcional)

### a) Alterar o Tamanho da Página PDF

Por padrão o Aspose.HTML cria uma página PDF que corresponde ao tamanho do viewport. Se preferir A4 ou Letter, adicione uma configuração `PdfSaveOptions`:

```java
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setPageSize(PageSize.A4);
Converter.convertDocument("input.html", "output.pdf", pdfOptions, loadOptions);
```

### b) Adicionar Cabeçalho/Rodapé Programaticamente

Você pode injetar um cabeçalho/rodapé simples após a conversão usando Aspose.PDF (uma biblioteca separada). O fluxo de trabalho é:

1. Converter HTML → PDF (conforme mostrado).  
2. Abrir o PDF resultante com Aspose.PDF.  
3. Adicionar objetos `HeaderFooter` a cada página.

```java
import com.aspose.pdf.*;

Document pdfDoc = new Document("output.pdf");
for (Page page : pdfDoc.getPages()) {
    page.addHeaderFooter(new HeaderFooter("Generated on " + LocalDate.now()));
}
pdfDoc.save("output-with-header.pdf");
```

### c) Conversão em Lote

Se você tem uma pasta de arquivos HTML, itere sobre eles:

```java
Files.list(Paths.get("html_folder"))
     .filter(p -> p.toString().endsWith(".html"))
     .forEach(p -> {
         String pdfPath = p.toString().replace(".html", ".pdf");
         Converter.convertDocument(p.toString(), pdfPath, new PdfSaveOptions(), loadOptions);
     });
```

---

## Perguntas Frequentes (FAQs)

**Q: Isso funciona com páginas pesadas em JavaScript?**  
A: O Aspose.HTML suporta um subconjunto de JavaScript. Manipulação simples do DOM e alterações de CSS geralmente funcionam, mas frameworks complexos (React, Angular) podem precisar de um snapshot HTML estático pré‑renderizado.

**Q: E se eu precisar converter uma página que usa regras `@media print`?**  
A: A biblioteca respeita `@media print` automaticamente. Contudo, se você também definir um viewport mobile, a folha de estilos de impressão pode sobrescrever alguns estilos mobile. Teste ambos os cenários.

**Q: Posso definir um DPI personalizado para o PDF?**  
A: Sim. Use `PdfSaveOptions.setDpi(300)` antes da conversão. DPI mais alto gera arquivos maiores, mas imagens mais nítidas.

---

## Captura de Tela do Resultado Esperado

Abaixo está uma ilustração da página PDF final (viewport mobile simulado).  
![Captura de tela do PDF gerado pelo demo de criar pdf a partir de html mostrando layout no tamanho de iPhone]  

*O texto alternativo da imagem inclui a palavra‑chave principal para SEO.*

---

## Conclusão

Agora você tem um fluxo sólido para **criar pdf a partir de html** que respeita os breakpoints mobile, simula uma tela de iPhone e lhe dá controle total sobre as dimensões da página. Ajustando `HtmlLoadOptions` você pode responder “**como definir a tela**” para qualquer dispositivo, e usando `Converter.convertDocument` você dominou **como converter html** em Java.

Pronto para o próximo desafio? Experimente combinar esta abordagem com Aspose.PDF para adicionar marcas d’água, mesclar vários PDFs ou proteger o documento com senha. E não se esqueça de experimentar outros dispositivos — basta mudar os valores de `Size` e `DeviceScaleFactor` para corresponder à densidade de pixels que você precisa.

Feliz codificação, e que seus PDFs estejam sempre tão nítidos no papel quanto em uma tela de telefone! 

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}