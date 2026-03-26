---
category: general
date: 2026-03-26
description: Exemplo de top‑level await mostrando await delay JavaScript, classe de
  incremento de contador e campos de classe públicos JavaScript em uma demonstração
  ao vivo.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: pt
og_description: Exemplo de top-level await que demonstra await delay JavaScript, classe
  de incremento de contador e campos de classe públicos JavaScript em um tutorial
  conciso.
og_title: exemplo de await de nível superior – Usando await delay em JavaScript
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: Exemplo de await de nível superior – Usando await delay em JavaScript
url: /pt/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# exemplo de top level await – Usando await delay em JavaScript

Já se perguntou como pausar a execução de um módulo sem envolver tudo em um IIFE async? É exatamente isso que um **top level await example** permite fazer. Neste tutorial vamos percorrer uma pequena página web que usa `await delay javascript` para adiar trabalho, e então cria uma `increment counter class` que aproveita **public class fields javascript**. Ao final você terá um trecho completo, pronto‑para‑copiar‑e‑colar, que roda em qualquer navegador moderno.

Vamos cobrir tudo, desde definir uma classe com um campo público até conectar um simples helper de atraso baseado em promises. Sem bibliotecas externas, sem etapa de build — apenas HTML puro, um `<script type="module">` e os recursos mais recentes do ECMAScript. Se você já está confortável com funções async, verá por que top‑level await parece uma extensão natural. Se você é novo na sintaxe de **javascript class public field**, não se preocupe — explicamos o porquê de cada linha.

## O que você vai aprender

- Como um **top level await example** funciona dentro de um script de módulo.
- O padrão para um helper `await delay javascript` que imita `setTimeout` com promises.
- Como escrever uma **increment counter class** que usa um campo público (`count`) e um bloco de inicialização estático.
- Saída esperada no console e como verificar que o bloco estático dispara antes do restante do script.
- Dicas para solucionar armadilhas comuns, como navegadores antigos que não suportam top‑level await.

> **Dica profissional:** Navegadores modernos (Chrome 106+, Firefox 102+, Edge 106+) já suportam top‑level await. Se precisar dar suporte a ambientes mais antigos, considere empacotar com uma ferramenta como Vite ou Babel.

## Etapa 1 – Definir uma classe com um campo público e um bloco estático

A primeira parte da nossa demonstração é uma classe que armazena um contador numérico. Observe a linha `count = 0;` — esta é a sintaxe de **public class fields javascript** introduzida no ES2022. Ela cria uma propriedade de instância sem precisar de um construtor.

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**Por que um bloco estático?** Ele nos permite executar lógica de inicialização única (como logs) no momento em que o módulo é analisado, *antes* de qualquer top‑level await ser executado. Isso garante que a mensagem apareça primeiro no console, provando que a classe foi avaliada cedo.

## Etapa 2 – Criar um helper `await delay javascript`

Em seguida precisamos de uma pequena função de atraso baseada em promise. É essencialmente um wrapper em torno de `setTimeout`, mas retornando uma promise que pode ser aguardada.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**Caso extremo:** Se `ms` for negativo ou não for um número, `setTimeout` o trata como `0`. Você poderia adicionar validação, mas para uma demo o one‑liner mantém as coisas legíveis.

## Etapa 3 – Usar Top‑Level Await para pausar a execução

Agora vem a estrela do show: top‑level await. Como nosso script é um módulo (`type="module"`), podemos colocar `await` diretamente no escopo superior. Isso pausa o módulo até que a promise seja resolvida, permitindo controlar a ordem dos efeitos colaterais.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**Pergunta comum:** “Posso usar top‑level await em uma tag `<script>` normal?” Não — apenas scripts de módulo o suportam. Se você esquecer `type="module"`, receberá um erro de sintaxe.

## Etapa 4 – Instanciar a classe, incrementar e registrar o resultado

Finalmente juntamos tudo: criamos uma instância, chamamos `increment()`, e exibimos o contador final. Isso demonstra a **increment counter class** em ação.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### Saída esperada no console

```
Counter class initialized
Final count: 1
```

Se você abrir a página nas DevTools, deverá ver a mensagem do bloco estático aparecer **antes** que o atraso termine, confirmando que a classe foi avaliada primeiro.

## Etapa 5 – Por que usar campos de classe públicos em vez de um construtor?

Você pode se perguntar por que não escrevemos:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

Ambas as abordagens funcionam, mas **public class fields javascript** fornecem uma sintaxe mais limpa e declarativa. O campo é definido uma única vez, não dentro de cada chamada ao construtor, o que pode ser mais fácil de ler quando a classe cresce. Além disso, blocos estáticos não podem ser colocados dentro de um construtor, então separar a lógica de inicialização torna‑se mais natural.

## Etapa 6 – Adaptando o exemplo para aplicativos do mundo real

Em produção você frequentemente precisará de mais que um único contador. Aqui vão algumas ideias rápidas:

- **Múltiplos contadores:** Armazene‑os em um `Map` indexado por identificador.
- **Estado persistente:** Substitua `console.log` por gravações em `localStorage`.
- **Inicialização async:** Use o bloco estático para buscar configuração de um servidor antes que quaisquer instâncias sejam criadas.

Todos esses padrões ainda se beneficiam do top‑level await, porque você pode buscar dados uma única vez no carregamento do módulo e garantir que estejam prontos para cada consumidor.

## Perguntas Frequentes

**P: O top‑level await bloqueia outros módulos?**  
R: Não. Cada módulo roda de forma independente. Apenas o módulo que contém o await é pausado; os demais continuam carregando em paralelo.

**P: E se a promise de atraso for rejeitada?**  
R: Uma rejeição não tratada abortará a avaliação do módulo e aparecerá como erro no console. Envolva o await em um `try…catch` se precisar de fallback elegante.

**P: A palavra‑chave `static` é obrigatória?**  
R: Não para o contador em si, mas o bloco estático é uma maneira prática de demonstrar que o código roda *uma única vez* no carregamento — ótimo para logs ou detecção de recursos.

## Conclusão

Você acabou de construir um **top level await example** que demonstra `await delay javascript`, uma **increment counter class**, e o poder de **public class fields javascript**. O trecho completo e executável está acima, e a saída no console prova que o bloco estático dispara antes do código atrasado.

A partir daqui você pode experimentar fluxos async mais complexos, trocar o atraso por uma chamada real a uma API, ou expandir a classe com métodos adicionais. Lembre‑se, o JavaScript moderno permite tratar módulos como entidades async de primeira classe — sem wrappers extras.

Feliz codificação, e sinta‑se à vontade para compartilhar suas variações nos comentários. Se este guia foi útil, compartilhe com um colega que ainda está lutando com padrões async!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}