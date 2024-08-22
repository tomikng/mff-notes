---
{"dg-publish":true,"permalink":"/tomas-statnice/databaze-a-web/datovy-management/datove-formaty/hierarchicka-data/","tags":["databaze_a_web","datovy_management","tomas"],"noteIcon":""}
---

> [!NOTE] ChatGPT
> Vygenerováno pomocí ChatGPT na zaklade prezentaci od Klimky
### 1. Formáty pro stromová (hierarchická) data: XML a JSON

**XML (eXtensible Markup Language):**
- **Struktura**: XML používá stromovou strukturu s prvky definovanými pomocí tagů, které jsou vnořeny do sebe, čímž vytvářejí hierarchii. Každý prvek může mít atributy, text a další prvky.
- **Použití**: XML se široce používá ve webových službách, pro ukládání dat a v konfiguračních souborech díky své flexibilitě a schopnosti sebe popisu.
- **Syntaxe**:
  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <root-element>
    <element attribute1="value">Obsah prvku</element>
    <element>
      <subelement>Textový obsah</subelement>
    </element>
  </root-element>
  ```

**JSON (JavaScript Object Notation):**
- **Struktura**: JSON také používá hierarchickou strukturu, ale na rozdíl od XML je založen na klíč-hodnota párech. Podporuje objekty (mapy), pole, čísla, řetězce, booleany a `null`.
- **Použití**: JSON je široce používán pro přenos dat mezi klientem a serverem, zejména v aplikacích založených na JavaScriptu díky své jednoduchosti a čitelnosti.
- **Syntaxe**:
  ```json
  {
    "key1": "value1",
    "key2": {
      "subkey": "subvalue"
    },
    "array": [1, 2, 3]
  }
  ```

### 2. Jazyky pro schémata stromových dat: XML Schema a JSON Schema

**XML Schema (XSD):**
- **Představení**: XML Schema definuje strukturu XML dokumentu, včetně datových typů, elementů, atributů a jejich vztahů.
- **Příklad**:
  ```xml
  <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <xs:element name="Address">
      <xs:complexType>
        <xs:sequence>
          <xs:element name="Street" type="xs:string"/>
          <xs:element name="City" type="xs:string"/>
        </xs:sequence>
      </xs:complexType>
    </xs:element>
  </xs:schema>
  ```

**JSON Schema:**
- **Představení**: JSON Schema definuje strukturu JSON dat, včetně povinných polí, typů hodnot a formátů.
- **Příklad**:
  ```json
  {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "properties": {
      "Street": { "type": "string" },
      "City": { "type": "string" }
    },
    "required": ["Street", "City"]
  }
  ```

### 3. JSON a RDF: JSON-LD

**JSON-LD (JSON for Linking Data):**
- **Účel**: JSON-LD umožňuje zobrazit JSON data jako RDF data, která jsou vhodná pro výměnu na webu. Umožňuje připojit JSON data do grafu, což umožňuje snadnější sdílení a propojení dat na webu.
- **Příklad**:
  ```json
  {
    "@context": {
      "name": "http://schema.org/name",
      "homepage": { "@id": "http://schema.org/url", "@type": "@id" }
    },
    "@id": "http://example.com/person/123",
    "name": "Jane Doe",
    "homepage": "http://janedoe.com"
  }
  ```

### 4. Transformace XML dat: XSLT

**XSLT (eXtensible Stylesheet Language Transformations):**
- **Účel**: XSLT je jazyk pro transformaci XML dokumentů do různých formátů, jako je HTML, text, nebo dokonce jiné XML dokumenty. Transformace se provádí na základě šablon, které definují, jak by měly být jednotlivé prvky XML dokumentu zpracovány.
- **Příklad**:
  ```xml
  <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
    <xsl:template match="/">
      <html>
        <body>
          <h2>Seznam produktů</h2>
          <ul>
            <xsl:for-each select="catalog/product">
              <li><xsl:value-of select="name"/></li>
            </xsl:for-each>
          </ul>
        </body>
      </html>
    </xsl:template>
  </xsl:stylesheet>
  ```

