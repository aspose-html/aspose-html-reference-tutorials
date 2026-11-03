---
date: 2026-05-04
description: Dowiedz się, jak wykonać konwersję HTML do PNG, przechwytywać żądania
  sieciowe w Javie oraz obsługiwać uszkodzone linki w Javie przy użyciu Aspose.HTML
  dla Javy.
keywords:
- html to png conversion
- intercept network requests java
- html to image conversion
- load html document java
- handle broken links java
linktitle: Użyj obsługi komunikatów w Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Konwersja HTML do PNG przy użyciu obsługi wiadomości Aspose.HTML w Javie
url: /pl/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwersja HTML do PNG przy użyciu obsługi komunikatów Aspose.HTML w Javie

## Wprowadzenie do konwersji HTML do PNG

W tym samouczku odkryjesz **jak konwertować HTML do PNG**, jednocześnie elegancko obsługując brakujące zasoby przy użyciu Aspose.HTML dla Javy. Przejdziemy przez tworzenie małej strony HTML, która odwołuje się do nieistniejącego obrazu, podłączenie **niestandardowego obsługującego komunikaty** do **przechwytywania żądań sieciowych**, konfigurację **usługi sieciowej**, załadowanie dokumentu i ostateczne wykonanie **konwersji HTML do obrazu**. Na końcu będziesz mieć solidny wzorzec zarówno do **obsługi uszkodzonych linków java**, jak i wysokiej jakości wyjścia PNG — idealny do raportów, miniatur lub podglądów e‑mail.

## Szybkie odpowiedzi
- **Co robi obsługa komunikatów?** Przechwytuje operacje sieciowe (np. żądania obrazów) i pozwala reagować na kody statusu, takie jak 404.  
- **Czy Aspose.HTML może konwertować HTML do PNG?** Tak—`Converter.convertHTML` wykonuje konwersję w jednym wywołaniu.  
- **Czy potrzebuję licencji do tego przykładu?** Tymczasowa licencja usuwa ograniczenia wersji ewaluacyjnej; stała licencja jest wymagana do użytku produkcyjnego.  
- **Która wersja Javy działa?** Dowolny JDK 8+ (przykład działa na JDK 11).  
- **Czy mogę skonfigurować usługę sieciową?** Oczywiście—użyj `configuration.getService(INetworkService.class)`, aby dodać swój handler.

## Czym jest konwersja HTML do PNG?
Konwersja HTML do PNG renderuje stronę internetową (lub fragment HTML) do obrazu rastrowego. Jest to przydatne, gdy potrzebujesz statycznych podglądów dynamicznej treści, generujesz miniatury do newsletterów e‑mailowych lub archiwizujesz strony internetowe jako obrazy.

## Dlaczego używać obsługi komunikatów do przechwytywania żądań sieciowych w Javie?
Obsługa komunikatów daje **precyzyjną kontrolę** nad każdym żądaniem sieciowym — niezależnie od tego, czy jest to obraz, CSS, JavaScript czy plik czcionki. Przechwytując te żądania, możesz **rejestrować brakujące zasoby**, dostarczać treść zastępczą lub nawet ponawiać nieudane pobrania, co sprawia, że Twój potok przetwarzania HTML jest **solidny** i **gotowy do produkcji**.

## Wymagania wstępne
Before we dive in, make sure you have the following ready:

1. **Java Development Kit (JDK)** – pobierz ze [strony Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – pobierz bibliotekę ze [strony wydań Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse lub NetBeans działają bez problemu.  
4. **Podstawowa znajomość Javy** – powinieneś być zaznajomiony z klasami, try‑with‑resources i obsługą wyjątków.  
5. **Tymczasowa licencja** – jeśli korzystasz z wersji próbnej, zdobądź [tymczasową licencję](https://purchase.aspose.com/temporary-license/), aby uniknąć znaków wodnych.

## Importowanie pakietów
Najpierw zaimportuj klasę Java I/O, której będziemy potrzebować do obsługi plików. Reszta klas Aspose jest odwoływana później w pełnych nazwach, co utrzymuje listę importów w porządku.

```java
import java.io.IOException;
```

## Krok 1: Przygotuj kod HTML
Tworzymy minimalny fragment HTML, który celowo odwołuje się do brakującego obrazu. Spowoduje to wywołanie naszego handlera, gdy silnik spróbuje pobrać zasób.

```java
String code = "<img src='missing.jpg'>";
```

## Krok 2: Zapisz kod HTML do pliku
Następnie zapisujemy fragment do *document.html*. Użycie bloku try‑with‑resources zapewnia prawidłowe zamknięcie `FileWriter`.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Krok 3: Napisz własny handler komunikatów
Teraz tworzymy **niestandardowy handler komunikatów**, który sprawdza status HTTP każdego żądania sieciowego. Jeśli odpowiedź nie jest `200`, logujemy przyjazne ostrzeżenie. Zwróć uwagę na wywołanie `invoke(context);` na końcu — przekazuje ono żądanie do kolejnego handlera w łańcuchu, zapobiegając rekurencji.

```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```

## Krok 4: Skonfiguruj usługę sieciową
Aby Aspose.HTML rozpoznało nasz handler, pobieramy **usługę sieciową** z instancji `Configuration` i dodajemy handler do jej kolekcji. To jest krok, w którym **konfigurujemy usługę sieciową** pod kątem niestandardowego zachowania.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Krok 5: Załaduj dokument HTML
Po przygotowaniu konfiguracji ładujemy *document.html*. Silnik teraz korzysta z naszej usługi sieciowej, więc żądanie brakującego obrazu jest przechwytywane przez właśnie dodany handler.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```

## Krok 6: Konwertuj HTML do PNG
Oto serce procesu **konwersji HTML do obrazu**. Metoda `Converter.convertHTML` przyjmuje załadowany `HTMLDocument`, opcjonalny `ImageSaveOptions` (gdzie można dostosować DPI lub jakość) oraz nazwę pliku wyjściowego.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Krok 7: Zwolnij zasoby
Dobre praktyki w Javie nakazują zwolnienie wszystkich zasobów natywnych. Blok `finally` zapewnia, że `Configuration` zostanie zwolniona, nawet jeśli wyjątek zostanie wyrzucony.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Typowe problemy i rozwiązania
- **Rekurencja handlera** – Wywołaj `invoke(context);` tylko raz, aby uniknąć nieskończonych pętli.  
- **Brak licencji** – Bez ważnej licencji wyjściowy PNG będzie zawierał znak wodny.  
- **Nieprawidłowe ścieżki plików** – Użyj ścieżek bezwzględnych lub prawidłowo ustaw katalog roboczy przy ładowaniu `document.html`.  
- **Nieobsługiwane typy zasobów** – Upewnij się, że zasób, który chcesz przechwycić (obraz, CSS itp.), jest rzeczywiście żądany przez silnik HTML.

## Najczęściej zadawane pytania

**Q: Czy mogę łączyć wiele handlerów komunikatów?**  
A: Tak, możesz dodać kilka handlerów do kolekcji `network.getMessageHandlers()`; będą wykonywane w kolejności dodania.

**Q: Czy handler działa również dla zasobów CSS lub skryptów?**  
A: Absolutnie — każde żądanie sieciowe wykonywane przez silnik HTML (obrazy, CSS, JS, czcionki) przechodzi przez handler.

**Q: Jak zmienić żądanie HTTP przed jego wysłaniem?**  
A: Zaimplementuj handler, który modyfikuje `context.getRequest()` przed wywołaniem `invoke(context)`.

**Q: Czy istnieje sposób, aby ukryć ostrzeżenie dla konkretnych URL‑i?**  
A: Wewnątrz handlera sprawdź `context.getRequest().getRequestUri()` i warunkowo pomiń logowanie.

**Q: Jakiej wersji Aspose.HTML wymaga ten interfejs API?**  
A: Kod działa z Aspose.HTML for Java 22.10 i nowszymi.

---
**Ostatnia aktualizacja:** 2026-05-04  
**Testowano z:** Aspose.HTML for Java 24.11  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}