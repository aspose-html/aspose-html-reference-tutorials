---
category: general
date: 2026-04-23
description: Come utilizzare querySelectorAll in Java per filtrare gli elementi per
  classe, leggere i valori degli attributi e iterare la NodeList per l'estrazione
  dei dati del prodotto.
draft: false
keywords:
- how to use queryselectorall
- how to read attribute
- iterate nodelist java
- filter elements by class
- select elements css selector
language: it
og_description: Come utilizzare querySelectorAll in Java per filtrare gli elementi
  per classe, leggere i valori degli attributi e iterare la NodeList per l'estrazione
  dei dati del prodotto.
og_title: Come usare querySelectorAll in Java – Filtrare per classe
tags:
- Java
- HTML parsing
- DOM manipulation
title: Come usare querySelectorAll in Java – Filtrare per classe
url: /it/java/creating-managing-html-documents/how-to-use-queryselectorall-in-java-filter-by-class/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare querySelectorAll in Java – Filtrare per classe

Usare querySelectorAll in Java è fondamentale quando è necessario estrarre elementi specifici da un documento HTML. In questo tutorial filtreremo gli elementi per classe, leggeremo i valori degli attributi e itereremo un NodeList per estrarre i prezzi dei prodotti da una pagina di catalogo.  

Ti è mai capitato di fissare un enorme file HTML, chiedendoti come estrarre solo le schede “in‑offerta” senza scrivere un parser personalizzato? È esattamente il problema che risolveremo qui—senza librerie aggiuntive oltre a Aspose.HTML, e con pochi passaggi semplici.

Uscirai da questo tutorial con un programma completo e eseguibile che:

* **Seleziona gli elementi** usando un selettore CSS (`select elements css selector`),
* **Filtra per classe** (`filter elements by class`),
* **Legge un attributo personalizzato** (`how to read attribute`),
* **Itera il NodeList risultante** (`iterate nodelist java`).

Non è necessaria alcuna esperienza pregressa con Aspose.HTML—basta una configurazione Java di base e un file HTML su cui testare.

![how to use querySelectorAll in Java example](https://example.com/images/queryselectorall-java.png "how to use querySelectorAll in Java")

---

## Cosa ti servirà

| Requisito | Perché è importante |
|-------------|----------------|
| **Java 17+** | Funzionalità moderne del linguaggio e migliore gestione dei moduli. |
| **Aspose.HTML for Java** (latest version) | Fornisce la classe `Document` e il motore di selettori CSS. |
| **catalog.html** (sample HTML) | La sorgente su cui effettueremo le query. |
| **IDE or plain `javac`** | Per compilare ed eseguire la demo. |

Se non hai ancora aggiunto Aspose.HTML al tuo progetto, inserisci il JAR nella cartella `libs` e aggiungilo al classpath:

```bash
javac -cp "libs/*" CssSelectorDemo.java
java -cp ".:libs/*" CssSelectorDemo
```

---

## Step 1 – Load the HTML Document

Prima di poter eseguire qualsiasi query, è necessario un oggetto `Document` che rappresenti il file HTML. Pensalo come caricare un foglio di calcolo prima di poter leggere le celle.

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **Perché è importante:** La classe `Document` analizza il markup in un albero DOM, consentendo al motore di selettori CSS di funzionare. Saltare questo passaggio ti lascerebbe con una semplice stringa e nessun modo di usare `querySelectorAll`.

---

## Step 2 – Select Elements with a CSS Selector

Ora arriva il cuore della questione: **come usare querySelectorAll**. Il metodo accetta qualsiasi selettore CSS valido, quindi puoi essere tanto preciso—o tanto generico—quanto desideri. Per il nostro scenario vogliamo le schede prodotto che:

* hanno la classe `product-card`,
* sono anche contrassegnate con la classe `sale`,
* e possiedono un attributo `data-price`.

```java
        // Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );
```

> **Spiegazione:**  
> * `.product-card.sale` → filtra gli elementi che contengono **entrambe** le classi.  
> * `[data-price]` → garantisce che l'attributo esista, filtrando efficacemente gli elementi per classe **e** attributo in una singola chiamata.  
> * Il risultato è un `NodeList`, una collezione ordinata che puoi iterare.  
> 
> Se mai avrai bisogno di **select elements css selector** per un pattern diverso, basta cambiare la stringa—nessuna riscrittura del codice è necessaria.

---

## Step 3 – Iterate the NodeList in Java

Un `NodeList` si comporta molto come un array, ma non implementa `Iterable`. Per questo usiamo un classico ciclo `for`—perfetto per scenari di **iterate nodelist java**.

```java
        // Iterate over the selected elements
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
```

> **Perché un ciclo `for`?**  
> Ti dà accesso diretto all'indice, utile per logging o ramificazioni condizionali. Se preferisci un ciclo `while`, la logica rimane identica—basta cambiare la costruzione del ciclo.

---

## Step 4 – Read the `data-price` Attribute

Ora rispondiamo finalmente a **how to read attribute** valori da un elemento. Nell'API DOM, `getAttribute` restituisce la stringa grezza, esattamente come appare nel markup.

```java
            // Read the price value from the data-price attribute
            String priceValue = productElement.getAttribute("data-price");
```

> **Suggerimento:** Se l'attributo potrebbe mancare, `getAttribute` restituisce `null`. Puoi proteggerti da questo con un semplice controllo:

```java
            if (priceValue == null) {
                priceValue = "N/A"; // fallback for missing data-price
            }
```

---

## Step 5 – Output the Results

Ultimo ma non meno importante, stampiamo ogni prezzo sulla console. Questo rispecchia uno scenario reale in cui probabilmente invieresti i valori a un database o a un payload API.

```java
            // Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

### Output previsto sulla console

```
Sale item price: 19.99
Sale item price: 34.50
Sale item price: 12.00
```

Se il selettore non trova nodi corrispondenti, il ciclo semplicemente non viene mai eseguito—non viene sollevata alcuna eccezione. È una buona rete di sicurezza per **edge cases** dove il catalogo potrebbe essere vuoto.

---

## Full Working Example

Mettendo tutto insieme, ecco il file completo che puoi copiare‑incollare in `CssSelectorDemo.java`:

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");

        // Step 2: Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );

        // Step 3 & 4: Iterate over the selected elements and read the price attribute
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
            String priceValue = productElement.getAttribute("data-price");
            if (priceValue == null) {
                priceValue = "N/A"; // fallback if attribute is missing
            }

            // Step 5: Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

Salva il file, compila ed esegui—guarda i prezzi scorrere. 🎉

---

## Common Questions & Pro Tips

| Domanda | Risposta |
|----------|--------|
| *E se devo selezionare anche per nome del tag?* | Basta anteporre il tag: `document.querySelectorAll("div.product-card.sale[data-price]")`. |
| *Posso concatenare più filtri di attributi?* | Assolutamente. Esempio: `[data-price][data-stock]` manterrà solo gli elementi che hanno **entrambi** gli attributi. |
| *`querySelectorAll` è sensibile al maiuscolo/minuscolo?* | Sì—i selettori CSS trattano i nomi di classi e attributi come sensibili al maiuscolo/minuscolo in HTML5. |
| *Come gestisco un file HTML di grandi dimensioni?* | Aspose.HTML trasmette lo stream del documento, ma puoi anche limitare il selettore a un sotto‑albero (`someElement.querySelectorAll(...)`). |
| *What

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}