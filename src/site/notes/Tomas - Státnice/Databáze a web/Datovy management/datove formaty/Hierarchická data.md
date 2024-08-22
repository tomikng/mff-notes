---
{"dg-publish":true,"permalink":"/tomas-statnice/databaze-a-web/datovy-management/datove-formaty/hierarchicka-data/","tags":["databaze_a_web","datovy_management","tomas"],"noteIcon":""}
---

# XML (eXtensible Markup Language):
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
## XML z Konceptualniho modelu
- 👀: konceptulani model je neorientovany graf -> musime hrany orientovat abychim vytvorili nejakou hierarchii -> muzeme modelovat pomoci XML
- Data centric vs data oriented
![Pasted image 20240822102202.png](/img/user/assets/img/Pasted%20image%2020240822102202.png)
## XML Namespace
![Pasted image 20240822102304.png](/img/user/assets/img/Pasted%20image%2020240822102304.png)
## XML Schema (XSD)
$$\text{XML je validni} \Leftrightarrow \text{je validovan na XML Schema} $$
```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           xmlns:vc="http://www.w3.org/2007/XMLSchema-versioning"
           elementFormDefault="qualified" attributeFormDefault="unqualified"
           vc:minVersion="1.1">
    <xs:complexType name="TypeAddress">
        <!-- specification of content -->
        <xs:sequence>
            <xs:element name="Street" type="xs:string"/>
            <xs:element name="Number" type="xs:integer"/>
            <xs:element name="City" type="xs:string"/>
        </xs:sequence>
        <!-- specification of attributes -->
        <xs:attribute name="Country" type="xs:string" default="CZ"/>
    </xs:complexType>
    <xs:element name="Address" type="TypeAddress"/>
</xs:schema>
```
Ekvivalentne
```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           xmlns:vc="http://www.w3.org/2007/XMLSchema-versioning"
           elementFormDefault="qualified" attributeFormDefault="unqualified"
           vc:minVersion="1.1">
    <xs:element name="Address">
	    <xs:complexType>
	        <!-- specification of content -->
	        <xs:sequence>
	            <xs:element name="Street" type="xs:string"/>
	            <xs:element name="Number" type="xs:integer"/>
	            <xs:element name="City" type="xs:string"/>
	        </xs:sequence>
	        <!-- specification of attributes -->
	        <xs:attribute name="Country" type="xs:string" default="CZ"/>
	    </xs:complexType>
    </xs:element>
</xs:schema>
```

- V prvnim pripade se jedna o reusability - Piseme modularne

![Pasted image 20240822102736.png](/img/user/assets/img/Pasted%20image%2020240822102736.png)
- Complex content je sequence v pripadech nahore
## XLST  (eXtensible Stylesheet Language Transformations)
### XPath
Nejdrive pokud, chceme zformulovat XLST musime umet XPATH.
- Funguje jako normalni nagvigace ve strome
### Filtrovani
![Pasted image 20240822105856.png](/img/user/assets/img/Pasted%20image%2020240822105856.png)
### XLST
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
  ![Pasted image 20240822110339.png](/img/user/assets/img/Pasted%20image%2020240822110339.png)
# JSON (JavaScript Object Notation)
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

## JSON Schema
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

### JSON a RDF: JSON-LD

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

```json
{
  "@context": {
    "name": "http://schema.org/name",
    "homepage": { "@id": "http://schema.org/url", "@type": "@id" }
  },
  "@graph": [
    {
      "@id": "http://example.com/person/123",
      "name": "Jane Doe",
      "homepage": "http://janedoe.com"
    },
    {
      "@id": "http://example.com/person/456",
      "name": "John Smith",
      "homepage": "http://johnsmith.com"
    },
    {
      "@id": "http://example.com/person/789",
      "name": "Alice Johnson",
      "homepage": "http://alicejohnson.com"
    }
  ]
}

```