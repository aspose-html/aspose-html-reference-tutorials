---
category: general
date: 2026-03-05
description: Jak zapytać HTML w Javie, aby odczytać plik HTML i wyodrębnić obrazy.
  Dowiedz się, jak odczytać plik HTML w Javie, pobrać adresy URL obrazów w Javie oraz
  iterować po NodeList w Javie.
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: pl
og_description: Jak zapytać HTML w Javie i pobrać adresy URL obrazów. Ten przewodnik
  pokazuje, jak odczytać plik HTML w Javie, zlokalizować obrazy i iterować po NodeList
  w Javie.
og_title: Jak przeszukiwać HTML w Javie – wyodrębniać adresy URL obrazów
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: Jak przeszukiwać HTML w Javie – wyodrębnić adresy URL obrazów
url: /pl/java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zapytać HTML w Javie – wyodrębnić adresy URL obrazów

Zastanawiałeś się kiedyś **jak zapytać HTML** w Javie, aby wyciągnąć każde zdjęcie na stronie? Nie jesteś jedyny — programiści stale muszą czytać pliki HTML, pobierać obrazy i potem coś z nimi zrobić. W tym samouczku przeprowadzimy praktyczny przykład, który dokładnie pokazuje **jak zapytać HTML**, jak odczytać plik HTML w stylu Java oraz jak uzyskać adresy URL obrazów w Javie.

Użyjemy Aspose.HTML for Java, ale koncepcje — XPath, selektory CSS i iterowanie po `NodeList` — mają zastosowanie do każdej biblioteki DOM. Po zakończeniu tego przewodnika będziesz pewny **jak wyodrębnić obrazy**, będziesz wiedział, jak **iterować po NodeList w Javie**, i będziesz mieć gotowy do uruchomienia fragment kodu, który możesz wkleić do swojego projektu.

![How to query HTML in Java example](https://example.com/placeholder.png "How to query HTML in Java")

---

## Co się nauczysz

- Wczytaj dokument HTML z dysku (read HTML file Java)
- Zlokalizuj tagi `<img>` używając zarówno XPath, jak i selektorów CSS (how to extract images)
- Iteruj przez otrzymany `NodeList` (iterate over NodeList Java)
- Wypisz atrybut `src` każdego obrazu (get image URLs Java)

Brak zewnętrznych usług, brak skomplikowanych narzędzi budujących — tylko czysta Java i pojedyncza zależność Maven.

---

## Wymagania wstępne

- Java 8 lub nowsza zainstalowana
- Maven lub Gradle do zarządzania zależnościami
- Podstawowa znajomość struktury HTML
- Opcjonalnie, ale przydatne: prosty plik HTML (`sample.html`) zawierający kilka elementów `<figure><img …></figure>`

Jeśli masz to wszystko, możemy od razu przejść do działania.

---

## Krok 1: Odczyt pliku HTML w Javie – wczytanie dokumentu

Na początek musimy wczytać HTML do pamięci. Klasa `HTMLDocument` z Aspose.HTML wykonuje ciężką pracę. Pomyśl o niej jak o otwarciu książki, aby móc przewracać do dowolnej strony.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.NodeList;
import com.aspose.html.dom.Element;

/**
 * Demonstrates how to query HTML in Java and extract image URLs.
 */
public class QueryExample {
    public static void main(String[] args) throws Exception {

        // ① Load the HTML document from a local file.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

**Dlaczego to ważne:** Wczytanie pliku daje Ci drzewo DOM, które możesz przeszukiwać. Jeśli ścieżka jest nieprawidłowa, otrzymasz `FileNotFoundException`, więc sprawdź lokalizację przed uruchomieniem.

---

## Krok 2: Zlokalizuj obrazy przy pomocy XPath – jak wyodrębnić obrazy

XPath to potężny język zapytań, który pozwala precyzyjnie wskazać węzły. Tutaj żądamy każdego `<img>` wewnątrz `<figure>`, który posiada również atrybut `alt`.

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**Dlaczego XPath?** Jest zwięzły i działa nawet przy nieporządnym HTML. Wyrażenie `//figure/img[@alt]` oznacza: „dowolny `<img>` pod `<figure>`, który posiada atrybut `alt`”. Jeśli potrzebujesz filtrować po innych atrybutach, po prostu zmodyfikuj nawiasy.

---

## Krok 3: Zlokalizuj obrazy przy pomocy selektora CSS – alternatywny sposób wyodrębniania obrazów

Czasami wolisz składnię CSS, ponieważ odzwierciedla to to, co piszesz w arkuszach stylów. `querySelectorAll` przyjmuje ten sam selektor, którego użyłbyś w przeglądarce.

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**Dlaczego oba?** Pokazanie obu metod pozwala wybrać narzędzie, z którym czujesz się najpewniej. W praktyce używa się jednego, ale posiadanie obu przykładów czyni samouczek bardziej kompletnym.

---

## Krok 4: Iteruj po NodeList w Javie – pobierz adresy URL obrazów w Javie

Teraz, gdy mamy kolekcję, musimy przejść przez nią. To właśnie tutaj wchodzi w grę **iterate over NodeList Java**. Wyciągniemy atrybut `src` każdego obrazu i go wypiszemy.

```java
        // ④ Loop through the NodeList returned by the CSS query.
        for (int i = 0; i < cssImages.getLength(); i++) {
            Element imageElement = (Element) cssImages.item(i);
            // Extract the "src" attribute – that’s the image URL.
            System.out.println("Image src: " + imageElement.getAttribute("src"));
        }
    }
}
```

**Dlaczego klasyczna pętla `for`?** `NodeList` z Aspose nie implementuje `Iterable`, więc rozszerzona składnia `for‑each` nie skompiluje się. Użycie pętli indeksowanej jest niezawodnym sposobem na **iterate over NodeList Java**.

---

## Oczekiwany wynik

Uruchomienie programu na przykładowym HTML takim jak:

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

Wygeneruje coś podobnego do:

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

Jeśli Twój plik zawiera więcej tagów `<img>` spełniających kryteria, liczby odpowiednio się zwiększą.

---

## Typowe pułapki i wskazówki profesjonalne

- **Problemy ze ścieżką pliku:** Użyj ścieżki bezwzględnej lub umieść `sample.html` względem katalogu roboczego projektu.  
- **Brak atrybutu `alt`:** Nasze zapytania XPath/CSS filtrują po `[@alt]`. Jeśli potrzebujesz *wszystkich* obrazów, usuń filtr atrybutu (`//figure/img` lub `figure img`).  
- **Wydajność:** Dla bardzo dużych dokumentów rozważ parsery strumieniowe, ale dla większości zadań web‑scrapingu podejście DOM jest wystarczające.  
- **Problemy z kodowaniem:** Aspose.HTML respektuje zestaw znaków zadeklarowany w HTML. Jeśli widzisz nieczytelne znaki, upewnij się, że plik jest zapisany jako UTF‑8.  

---

## Rozszerzanie przykładu

Teraz, gdy możesz **get image URLs Java**, możesz chcieć:

1. **Pobierz obrazy** używając `java.net.URL` i `Files.copy`.  
2. **Zapisz adresy URL w bazie danych** do późniejszego przetwarzania.  
3. **Filtruj po rozszerzeniu pliku** (`src.endsWith(".png")`).  

Wszystkie te operacje są prostymi rozszerzeniami pętli pokazanej w Kroku 4.

---

## Podsumowanie

W tym przewodniku omówiliśmy **jak zapytać HTML** w Javie od początku do końca: wczytywanie pliku, lokalizowanie obrazów zarówno przy pomocy XPath, jak i selektorów CSS oraz **iterowanie po NodeList w Javie**, aby wypisać `src` każdego obrazu. Masz teraz solidne podstawy do **how to extract images**, i wiesz dokładnie **how to read HTML file Java** przy użyciu Aspose.HTML.

Śmiało dostosuj kod do własnych potrzeb scrapowania — niezależnie od tego, czy chcesz pobierać inne atrybuty, obsługiwać tagi `<a>`, czy przekazywać adresy URL do pobieracza. Wzorzec pozostaje ten sam: wczytaj, zapytaj, iteruj i działaj.

Masz pytania lub chcesz podzielić się ciekawym przypadkiem użycia? zostaw komentarz poniżej i szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}