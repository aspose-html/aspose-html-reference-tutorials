---
title: Zastosuj zewnętrzny CSS do dokumentów HTML w Aspose.HTML dla Java
linktitle: Zastosuj zewnętrzny CSS do dokumentów HTML w Aspose.HTML dla Java
second_title: Przetwarzanie HTML w Javie za pomocą Aspose.HTML
description: Dowiedz się, jak stosować zewnętrzny CSS do dokumentów HTML za pomocą Aspose.HTML dla Java! Postępuj zgodnie z tym przewodnikiem krok po kroku, aby uzyskać kompletny samouczek.
type: docs
weight: 12
url: /pl/java/editing-html-documents/apply-external-css-html-documents/
---
## Wstęp
Podczas pracy z dokumentami HTML stosowanie stylów może mieć ogromne znaczenie dla prezentacji i doświadczenia użytkownika. Jeśli zagłębiasz się w Javę i chcesz nauczyć się stosować zewnętrzne style CSS do dokumentów HTML za pomocą biblioteki Aspose.HTML, jesteś we właściwym miejscu! Ten przewodnik ma na celu wyjaśnienie tego procesu krok po kroku, ułatwiając go nawet tym, którzy mogą być nowicjuszami w Javie lub CSS.
## Wymagania wstępne
Zanim zagłębisz się w kod, musisz zadbać o kilka rzeczy:
### 1. Zestaw narzędzi programistycznych Java (JDK)
 Upewnij się, że masz zainstalowany JDK na swoim komputerze. Możesz pobrać najnowszą wersję z[Witryna internetowa Oracle Java](https://www.oracle.com/java/technologies/javase-downloads.html).
### 2. Aspose.HTML dla Javy
Musisz mieć skonfigurowany Aspose.HTML dla Java. Jeśli jeszcze tego nie zrobiłeś, przejdź do[Strona pobierania Aspose](https://releases.aspose.com/html/java/) i chwyć bibliotekę.
### 3. IDE lub edytor tekstu
Wybierz zintegrowane środowisko programistyczne (IDE), takie jak IntelliJ IDEA, Eclipse, a nawet prosty edytor tekstu, aby napisać kod Java.
### 4. Podstawowa wiedza o Javie
Znajomość programowania w Javie i podstaw CSS z pewnością pomoże Ci poruszać się swobodniej.
## Importuj pakiety
Gdy już wszystko skonfigurujesz, następnym krokiem jest zaimportowanie niezbędnych pakietów do projektu Java. Oto, czego potrzebujesz:
```java
import com.aspose.html.HTMLDocument;
```
Tego typu importy umożliwiają manipulowanie dokumentami HTML i renderowanie ich do różnych formatów, np. PDF.

Podzielimy nasz samouczek na łatwe do opanowania kroki. Każdy krok przeprowadzi Cię przez proces stosowania zewnętrznych stylów CSS do dokumentu HTML przy użyciu Aspose.HTML dla Java.
## Krok 1: Utwórz dokument HTML
Najpierw musimy utworzyć nasz dokument HTML. Zaczniemy od zdefiniowania zawartości za pomocą prostej struktury HTML.
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

 Tutaj zdefiniowaliśmy podstawową strukturę HTML, obejmującą:`<div>` z dwoma akapitami.`HTMLDocument` Klasa ta służy do tworzenia reprezentacji dokumentu naszej zawartości HTML.
## Krok 2: Utwórz element stylu
 Następnie utworzymy`style` element do przechowywania naszych reguł CSS.
```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

 Korzystanie z`createElement` metoda`HTMLDocument` , tworzymy nowy`<style>` element i ustaw jego zawartość tak, aby zawierała nasze definicje CSS dla dwóch klas:`frame1` I`frame2`Klasy te definiują marginesy, wypełnienia, wymiary, kolory tła, rodziny czcionek i kolory tekstu.
## Krok 3: Dodaj styl do nagłówka dokumentu
Teraz, gdy mamy już nasz kod CSS, musimy dodać element stylu do nagłówka dokumentu.
```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

 Pobieramy nagłówek dokumentu i dołączamy nowo utworzony`style` element. Ta akcja skutecznie integruje nasz CSS z dokumentem HTML, pozwalając mu na stylizowanie naszej zawartości HTML.
## Krok 4: Zastosuj klasy do elementów HTML
Następnie zastosujemy wcześniej zdefiniowane klasy CSS do elementów akapitu.
```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

Tutaj uzyskujemy dostęp do pierwszego i ostatniego elementu akapitu w dokumencie i przypisujemy im klasy CSS, które utworzyliśmy. To przypisanie zapewnia, że są one zgodne ze stylami zdefiniowanymi w naszym CSS.
## Krok 5: Ustaw dodatkowe właściwości stylu
Aby jeszcze bardziej ulepszyć wygląd, ustawimy dodatkowe właściwości stylu dla naszych akapitów.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

W tym kroku dopracowujemy nasze style. Rozmiar czcionki pierwszego akapitu jest zwiększany i wyśrodkowany, podczas gdy kolor, rozmiar czcionki i rodzina czcionek ostatniego akapitu są definiowane. To udoskonalenie jest kluczowe dla czytelności i atrakcyjności estetycznej.
## Krok 6: Zapisz dokument HTML
Po zastosowaniu stylów możemy zapisać dokument HTML.
```java
document.save("edit-internal-css.html");
```

 Tutaj wykorzystujemy`save` metoda`HTMLDocument` klasa umożliwiająca zapisanie zmodyfikowanej zawartości HTML do pliku, dzięki czemu zachowane zostaną nasze style i zmiany.
## Krok 7: Przekształć dokument w PDF
Na koniec przekonwertujmy dokument do formatu PDF w celu jego wydrukowania.
```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

 Korzystanie z`PdfDevice` klasa, ustawiamy renderowanie naszego dokumentu HTML do PDF. Ten krok jest kluczowy, gdy chcesz udostępnić stylizowany dokument w powszechnie dostępnym formacie.
## Wniosek
I oto masz — stosowanie zewnętrznego CSS do dokumentów HTML przy użyciu Aspose.HTML dla Javy jest zarówno proste, jak i satysfakcjonujące! Za pomocą zaledwie kilku linijek kodu możesz zamienić zwykły tekst w wizualnie atrakcyjne i profesjonalnie wystylizowane dokumenty. Tak więc, niezależnie od tego, czy projektujesz do użytku osobistego, tworzysz raporty, czy rozwijasz treści internetowe, zrozumienie, jak manipulować HTML i CSS w Javie, to potężna umiejętność, którą warto mieć w swoim zestawie narzędzi.
## Najczęściej zadawane pytania
### Czym jest Aspose.HTML dla Java?
Aspose.HTML for Java to rozbudowana biblioteka umożliwiająca programistom pracę z dokumentami HTML w aplikacjach Java, udostępniająca szeroką gamę funkcji — od manipulacji HTML po renderowanie.
### Czy do korzystania z Aspose.HTML potrzebuję połączenia z Internetem?
Nie, po pobraniu niezbędnych plików bibliotecznych możesz używać Aspose.HTML w trybie offline.
### Czy mogę zastosować wiele plików CSS do dokumentu HTML?
 Tak, możesz utworzyć wiele`<link>` elementy i dołączyć je do nagłówka dokumentu w różnych plikach CSS.
### Czy istnieje różnica pomiędzy wewnętrznym i zewnętrznym CSS?
Tak! Wewnętrzny CSS jest zdefiniowany w dokumencie HTML, podczas gdy zewnętrzny CSS jest umieszczony w oddzielnym pliku i połączony z dokumentem.
### Jak mogę uzyskać pomoc techniczną dotyczącą Aspose.HTML dla Java?
 Możesz uzyskać dostęp do wsparcia społeczności poprzez[Forum Aspose](https://forum.aspose.com/c/html/29) w przypadku jakichkolwiek pytań lub problemów, które możesz napotkać.