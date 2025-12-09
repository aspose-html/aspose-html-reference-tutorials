---
date: 2025-12-05
description: Dowiedz się, jak ustawiać marginesy stron HTML w Javie przy użyciu Aspose.HTML
  oraz dodawać numery stron i tytuły do swoich dokumentów.
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: Jak ustawić marginesy strony HTML w Javie przy użyciu Aspose.HTML
url: /pl/java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ustawić marginesy strony HTML w Javie przy użyciu Aspose.HTML

W tym samouczku odkryjesz **jak ustawić marginesy strony HTML w Javie** przy użyciu Aspose.HTML dla Javy. Przeprowadzimy Cię przez tworzenie własnych marginesów strony, wstawianie numerów stron oraz dodawanie tytułu dokumentu — wszystko z jasnym, krok po kroku kodem, który możesz skopiować do własnego projektu.

## Quick Answers
- **Jakiej biblioteki potrzebujesz?** Aspose.HTML for Java  
- **Czy mogę sterować marginesami programowo?** Tak, za pomocą reguły CSS `@page` w arkuszu stylów użytkownika  
- **Które formaty wyjściowe obsługują marginesy?** XPS, PDF i inne formaty rastrowe  
- **Czy potrzebna jest licencja do produkcji?** Wymagana jest ważna licencja Aspose.HTML do użytku nie‑testowego  
- **Czy jest kompatybilna z Java 11+?** Absolutnie – biblioteka działa z nowoczesnymi wersjami Javy  

## Co oznacza „Ustawianie marginesów strony HTML w Javie”?
Ustawianie marginesów strony HTML w Javie oznacza konfigurowanie silnika renderującego (dostarczanego przez Aspose.HTML), aby zastosował właściwości CSS page‑box przed konwersją dokumentu do formatu drukowalnego, takiego jak XPS lub PDF. Definiując własną regułę `@page`, kontrolujesz obszar drukowalny, numery stron oraz zawartość nagłówka i stopki.

## Dlaczego warto używać Aspose.HTML do kontroli marginesów?
- **Precyzyjny układ** – CSS `@page` zapewnia kontrolę piksel‑po‑pikselu nad marginesami, nagłówkami i stopkami.  
- **Spójność między formatami** – Te same definicje marginesów działają dla XPS, PDF i wyjść graficznych.  
- **Brak zależności od przeglądarki** – Renderowanie odbywa się po stronie serwera, więc nie potrzebujesz przeglądarki w trybie headless.  

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że spełniasz następujące wymagania:

1. **Środowisko programistyczne Java** – zainstalowany JDK 11 lub nowszy.  
2. **Aspose.HTML for Java** – pobierz i zainstaluj bibliotekę z [tutaj](https://releases.aspose.com/html/java/).  

## Importowanie pakietów

Aby rozpocząć, zaimportuj niezbędne klasy Aspose.HTML:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## Jak ustawić marginesy strony HTML w Javie – przewodnik krok po kroku

### Krok 1: Inicjalizacja konfiguracji i definiowanie własnych marginesów strony

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

W tym bloku tworzymy obiekt `Configuration`, uzyskujemy `IUserAgentService` i wstrzykujemy regułę CSS `@page`, która definiuje marginesy, licznik stron w prawym dolnym rogu oraz tytuł dokumentu wyśrodkowany u góry.

### Krok 2: Utworzenie dokumentu HTML

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Tutaj tworzymy `HTMLDocument` z prostym fragmentem „Hello World”. Ta sama konfiguracja z Kroku 1 jest zastosowana, więc własne marginesy są respektowane podczas renderowania dokumentu.

### Krok 3: Renderowanie do pliku XPS (lub dowolnego obsługiwanego formatu)

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Ten krok tworzy `XpsDevice`, który zapisuje wyrenderowane strony do `output.xps`. Marginesy, numery stron i tytuł zdefiniowane wcześniej pojawią się w finalnym pliku.

## Częste problemy i wskazówki
- **Marginesy wydają się niezmienione** – Upewnij się, że reguła `@page` nie jest nadpisywana przez inne arkusze stylów. Wywołanie `setUserStyleSheet` wymusza najwyższy priorytet.  
- **Numery stron wyświetlają „NaN”** – Sprawdź, czy używasz Aspose.HTML w wersji 23.10 lub nowszej; starsze wersje nie posiadają funkcji `currentPageNumber()`.  
- **Plik wyjściowy jest pusty** – Zweryfikuj, czy ścieżka `Resources.output` jest prawidłowo rozpoznawana i masz uprawnienia do zapisu.  

## Najczęściej zadawane pytania

### Q1: Co to jest Aspose.HTML for Java?
**A:** Aspose.HTML for Java to biblioteka Java, która zapewnia potężne narzędzia do pracy z dokumentami HTML w aplikacjach Java, w tym konwersję, renderowanie i manipulację.

### Q2: Czy mogę dalej dostosować marginesy strony?
**A:** Tak, po prostu edytuj CSS wewnątrz `setUserStyleSheet`. Możesz zmienić dowolne wartości `margin-*` lub dodać dodatkowe pola `@top-*` / `@bottom-*`.

### Q3: Jak mogę dodać więcej treści do dokumentu HTML?
**A:** Zastąp ciąg w `new HTMLDocument("<div>Hello World!!!</div>", …)` własnym kodem HTML lub załaduj zewnętrzny plik używając konstruktora `HTMLDocument(String url, …)`.

### Q4: Czy Aspose.HTML for Java jest kompatybilny z innymi formatami dokumentów?
**A:** Absolutnie. Ten sam `HTMLDocument` może być renderowany do PDF, XPS, obrazów lub nawet EPUB, zmieniając urządzenie wyjściowe (np. `PdfDevice`, `PngDevice`).

### Q5: Czy potrzebuję licencji do używania Aspose.HTML for Java?
**A:** Tak, licencja jest wymagana do użytku produkcyjnego. Możesz uzyskać wersję próbną lub zakupić licencję [tutaj](https://purchase.aspose.com/buy) lub [tutaj](https://releases.aspose.com/).

### Q6: Jak ustawić różne marginesy dla stron nieparzystych i parzystych?
**A:** Użyj pseudo‑klas `@page :left` i `@page :right` w arkuszu stylów, aby zdefiniować odrębne marginesy dla stron lewych (parzystych) i prawych (nieparzystych).

### Q7: Czy mogę osadzić własne czcionki w renderowanym dokumencie?
**A:** Tak. Dodaj reguły `@font-face` do arkusza stylów użytkownika i odwołuj się do czcionek w treści HTML.

## Zakończenie

Teraz opanowałeś **sposób ustawiania marginesów strony HTML w Javie** przy użyciu Aspose.HTML i wiesz, jak dodać numery stron oraz tytuł, aby Twoje dokumenty wyglądały profesjonalnie. Śmiało eksperymentuj z dodatkowymi polami `@page`, własnymi czcionkami lub różnymi formatami wyjściowymi, aby dopasować je do potrzeb projektu.

Jeśli napotkasz jakiekolwiek problemy, oficjalna [dokumentacja Aspose.HTML for Java](https://reference.aspose.com/html/java/) oraz [forum wsparcia Aspose](https://forum.aspose.com/) są doskonałymi miejscami, aby uzyskać pomoc.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-05  
**Tested With:** Aspose.HTML for Java 23.12  
**Author:** Aspose  

---