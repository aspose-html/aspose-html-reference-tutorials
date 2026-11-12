---
category: general
date: 2026-09-07
description: Hur man konverterar en mall till HTML med Java. Lär dig att generera
  HTML från en mall, aktivera foreach-loopar och se ett komplett exempel på en Java-mallmotor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to convert template
- generate html from template
- how to use foreach
- java template engine example
- convert html template
language: sv
lastmod: 2026-09-07
og_description: Hur man konverterar en mall till HTML med Java. Denna handledning
  visar ett komplett exempel på en Java‑mallmotor, hur man genererar HTML från en
  mall och hur man använder foreach.
og_image_alt: Screenshot showing the resulting HTML file after template conversion
og_title: Hur man konverterar mall till HTML med Java – steg‑för‑steg guide
schemas:
- author: Aspose
  dateModified: '2026-09-07'
  description: How to convert template to HTML using Java. Learn to generate HTML
    from a template, enable foreach loops, and see a full java template engine example.
  headline: How to convert template to HTML with a Java template engine
  type: TechArticle
- description: How to convert template to HTML using Java. Learn to generate HTML
    from a template, enable foreach loops, and see a full java template engine example.
  name: How to convert template to HTML with a Java template engine
  steps:
  - name: Reads `template.html` into memory.
    text: Reads `template.html` into memory.
  - name: Substitutes each `{{key}}` with the corresponding value from `data`.
    text: Substitutes each `{{key}}` with the corresponding value from `data`.
  - name: Processes any enabled foreach blocks.
    text: Processes any enabled foreach blocks.
  - name: Writes the transformed content to `resultPath`.
    text: Writes the transformed content to `resultPath`.
  type: HowTo
tags:
- Java
- template engine
- HTML generation
title: Hur man konverterar en mall till HTML med en Java‑mallmotor
url: /sv/java/creating-managing-html-documents/how-to-convert-template-to-html-with-a-java-template-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man konverterar mall till HTML med en Java-mallmotor

Om du behöver **how to convert template** till en färdig‑att‑servas HTML‑sida, ger den här guiden en komplett lösning. Du kommer att se hur du **generate HTML from template** filer, aktiverar loopning med **how to use foreach**, och går igenom ett **java template engine example** som fungerar med XML‑ eller JSON‑datakällor.

Handledningen täcker allt som krävs för att **convert html template** filer i ett enda Java‑program. I slutet kommer du att ha ett körbart projekt som läser en mall, injicerar data och skriver den slutgiltiga HTML‑filen till disk.

## Förutsättningar

* JDK 17 eller senare installerat  
* Ett byggverktyg som Maven eller Gradle (koden använder endast standard‑Java‑klasser)  
* Grundläggande kunskap om Java I/O och XML/JSON‑format  

Inga externa bibliotek krävs för kärnstegen, men du kan ersätta de enkla `Template`‑klasserna med en tredjeparts‑motor om du föredrar.

## Steg 1: Ställ in filsökvägar och mallmarkörer

Det första steget definierar var mallen, datakällan och utdata ska ligga. Mallen innehåller `{{...}}`‑platshållare som motorn kommer att ersätta.

```java
// Step 1: Define paths to the template, data source, and output file
String templatePath = "src/main/resources/template.html";   // contains {{...}} expressions
String dataPath     = "src/main/resources/data.xml";        // can also be a JSON file
String resultPath   = "src/main/resources/result.html";
```

*Varför detta är viktigt*: Att hårdkoda sökvägar låter dig köra programmet från vilken IDE som helst utan extra konfiguration. Du kan också skicka dessa värden som kommandoradsargument för större flexibilitet.

## Steg 2: Ladda datakällan (XML eller JSON)

Motorn behöver ett dataobjekt som mappar platshållarnamn till värden. Klassen `TemplateData` abstraherar XML‑ och JSON‑parsing.

```java
// Step 2: Load the data source (XML or JSON) that will fill the template
TemplateData data = new TemplateData(dataPath);
```

Om `dataPath` pekar på en JSON‑fil, upptäcker `TemplateData` automatiskt formatet och bygger samma nyckel/värde‑karta. Denna flexibilitet är användbar när du **generate html from template** i olika miljöer.

## Steg 3: Aktivera foreach‑direktivet för loopning

Många mallar behöver upprepa ett block för varje objekt i en samling. Att aktivera foreach‑direktivet instruerar motorn att bearbeta `{{#foreach items}} … {{/foreach}}`‑block.

```java
// Step 3: Enable the foreach directive to allow loop constructs in the template
TemplateLoadOptions loadOptions = new TemplateLoadOptions();
loadOptions.setEnableForeachDirective(true);
```

**Hur man använder foreach**: Inuti `template.html` kan du skriva:

```html
<ul>
{{#foreach products}}
  <li>{{name}} – ${{price}}</li>
{{/foreach}}
</ul>
```

När motorn stöter på detta block, upprepar den `<li>`‑elementet för varje post i `products`‑samlingen som levereras av `TemplateData`.

## Steg 4: Konvertera mallen och skriv resultatet

Nu ersätter motorn alla markörer med faktiska värden och skriver den slutgiltiga HTML‑filen.

```java
// Step 4: Convert the template – replace markers with data values and save the result
Template.convertTemplate(templatePath, data, loadOptions, resultPath);
```

`convertTemplate`‑metoden utför tre åtgärder:

1. Läser `template.html` till minnet.  
2. Ersätter varje `{{key}}` med motsvarande värde från `data`.  
3. Bearbetar eventuella aktiverade foreach‑block.  
4. Skriver det transformerade innehållet till `resultPath`.

## Steg 5: Kör programmet och verifiera resultatet

Till sist, informera användaren om att konverteringen lyckades.

```java
// Step 5: Inform that the conversion has finished
System.out.println("Template conversion completed: " + resultPath);
```

När du kör `main`‑metoden bör du se en konsollrad liknande:

```
Template conversion completed: src/main/resources/result.html
```

Öppna `result.html` i en webbläsare. Alla platshållare kommer att ersättas, och eventuella foreach‑loopar kommer ha genererat de lämpliga HTML‑fragmenten.

### Exempel på förväntat resultat

Givet en enkel `template.html`:

```html
<h1>{{title}}</h1>
<p>{{description}}</p>

<ul>
{{#foreach items}}
  <li>{{name}} – {{quantity}}</li>
{{/foreach}}
</ul>
```

Och en XML `data.xml`:

```xml
<root>
  <title>Shopping List</title>
  <description>Items you need to buy</description>
  <items>
    <item><name>Apples</name><quantity>4</quantity></item>
    <item><name>Bread</name><quantity>1</quantity></item>
    <item><name>Milk</name><quantity>2</quantity></item>
  </items>
</root>
```

Den genererade `result.html` kommer att vara:

```html
<h1>Shopping List</h1>
<p>Items you need to buy</p>

<ul>

  <li>Apples – 4</li>

  <li>Bread – 1</li>

  <li>Milk – 2</li>

</ul>
```

## Kantfall och bästa praxis‑tips

* **Saknade platshållare** – Motorn lämnar okända `{{key}}`‑markörer oförändrade. Du kan lägga till ett valideringssteg som skannar mallen efter återstående klamrar och loggar en varning.
* **Stora datamängder** – För tusentals objekt, överväg att strömma mallen istället för att läsa in hela filen i minnet. Den nuvarande implementeringen är tillräcklig för vanliga webbsidor.
* **JSON vs. XML** – Om du byter till JSON, behåll samma struktur:

  ```json
  {
    "title": "Shopping List",
    "description": "Items you need to buy",
    "items": [
      {"name": "Apples", "quantity": 4},
      {"name": "Bread", "quantity": 1},
      {"name": "Milk", "quantity": 2}
    ]
  }
  ```

  `TemplateData` kommer att parsas automatiskt, så resten av koden förblir oförändrad.
* **Kodning** – Säkerställ att både mall‑ och datafiler använder UTF‑8 för att undvika teckenkorruption, särskilt när du genererar flerspråkig HTML.
* **Säkerhet** – Lita inte på användar‑tillhandahållen data för direkt injicering i HTML utan sanering. Escape HTML‑specialtecken om data kan innehålla markup.

## Fullt körbart exempel

Nedan är en fristående Java‑klass som samlar alla steg. Spara den som `TemplateConverter.java` och kör den från din IDE eller kommandorad.

```java
import java.io.*;
import java.nio.file.*;
import java.util.*;
import javax.xml.parsers.*;
import org.w3c.dom.*;
import com.fasterxml.jackson.databind.*;
import com.fasterxml.jackson.core.type.TypeReference;

/**
 * Demonstrates how to convert template to HTML using a simple Java template engine.
 */
public class TemplateConverter {

    public static void main(String[] args) throws Exception {
        // Step 1: Define paths
        String templatePath = "src/main/resources/template.html";
        String dataPath     = "src/main/resources/data.xml";
        String resultPath   = "src/main/resources/result.html";

        // Step 2: Load data (XML or JSON)
        TemplateData data = new TemplateData(dataPath);

        // Step 3: Enable foreach loops
        TemplateLoadOptions loadOptions = new TemplateLoadOptions();
        loadOptions.setEnableForeachDirective(true);

        // Step 4: Perform conversion
        Template.convertTemplate(templatePath, data, loadOptions, resultPath);

        // Step 5: Notify user
        System.out.println("Template conversion completed: " + resultPath);
    }
}

/**
 * Holds key/value pairs loaded from XML or JSON.
 */
class TemplateData {
    private final Map<String, Object> map = new HashMap<>();

    public TemplateData(String path) throws Exception {
        if (path.endsWith(".json")) {
            loadJson(path);
        } else if (path.endsWith(".xml")) {
            loadXml(path);
        } else {
            throw new IllegalArgumentException("Unsupported data format: " + path);
        }
    }

    private void loadJson(String path) throws IOException {
        ObjectMapper mapper = new ObjectMapper();
        Map<String, Object> jsonMap = mapper.readValue(
                Files.readAllBytes(Paths.get(path)),
                new TypeReference<Map<String, Object>>() {});
        map.putAll(jsonMap);
    }

    private void loadXml(String path) throws Exception {
        DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
        DocumentBuilder builder = factory.newDocumentBuilder();
        Document doc = builder.parse(new File(path));
        doc.getDocumentElement().normalize();
        traverseNode(doc.getDocumentElement(), "");
    }

    private void traverseNode(Node node, String prefix) {
        NodeList children = node.getChildNodes();
        for (int i = 0; i < children.getLength(); i++) {
            Node child = children.item(i);
            if (child.getNodeType() == Node.ELEMENT_NODE) {
                String key = prefix.isEmpty() ? child.getNodeName() : prefix + "." + child.getNodeName();
                if (child.hasChildNodes() && child.getFirstChild().getNodeType() == Node.ELEMENT_NODE) {
                    // Nested element – recurse
                    traverseNode(child, key);
                } else {
                    map.put(key, child.getTextContent().trim());
                }
            }
        }
    }

    public Object get(String key) {
        return map.get(key);
    }

    public Map<String, Object> getAll() {
        return map;
    }
}

/**
 * Options that control how the template is loaded.
 */
class TemplateLoadOptions {
    private boolean enableForeachDirective = false;

    public void setEnableForeachDirective(boolean enable) {
        this.enableForeachDirective = enable;
    }

    public boolean isForeachEnabled() {
        return enableForeachDirective;
    }
}

/**
 * Core engine that performs placeholder replacement and foreach processing.
 */
class Template {
    public static void convertTemplate(String templatePath,
                                       TemplateData data,
                                       Template


## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man konverterar HTML till PDF Java – med Aspose.HTML för Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Hur man redigerar HTML med Aspose.HTML för Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Konvertera HTML till String med Aspose.HTML för Java](/html/english/java/editing-html-documents/manage-inner-outer-html-properties/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}