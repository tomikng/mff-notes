---
{"dg-publish":true,"permalink":"/tomas-statnice/databaze-a-web/datovy-management/datove-formaty/modely-a-formaty-pro-grafova-data-rdf-a-labeled-property-graph/","tags":["databaze_a_web","databaze","tomas"],"noteIcon":""}
---

## RDF

**1. RDF (Resource Description Framework)**
**Popis a použití:**
- RDF je model pro reprezentaci informací o zdrojích na webu, který používá **grafy**, kde každý **uzel** představuje entitu (subjekt nebo objekt) a hrana představuje vztah mezi těmito entitami (predikát).
- RDF se používá pro modelování komplexních datových struktur a propojení dat napříč různými zdroji, zejména na sémantickém webu.
  
**Serializace RDF:**
- RDF data mohou být serializována v různých formátech, včetně:
  - **Turtle**: Čitelný formát pro lidi, vhodný pro zápis RDF dat.
  - **RDF/XML**: XML-based serializace RDF, vhodná pro aplikace vyžadující strukturovaný XML formát.
  - **JSON-LD**: JSON serializace RDF, často používaná v moderních webových aplikacích.

**Příklad:**
```turtle
@prefix foaf: <http://xmlns.com/foaf/0.1/> .

<http://example.org/person/JohnDoe> 
  a foaf:Person ;
  foaf:name "John Doe" ;
  foaf:age 28 .
```

**2. Labeled Property Graph (LPG)**

**Popis a použití:**
- Labeled Property Graph je model grafových dat, kde uzly a hrany mohou mít štítky (labels) a vlastnosti (properties). Tento model se často používá v databázích jako Neo4j.
- LPG je vhodný pro aplikace, které vyžadují rychlý přístup k datům a kde je důležité provádět složité dotazy nad propojenými daty.

**Příklad:**
- Uzly mohou reprezentovat osoby a hrany vztahy mezi nimi. Např. uzel s vlastnostmi jako `jméno: "Jan"` a hrana s vlastností `od: "2020-01-01"`.

**Porovnání RDF a LPG:**
- **RDF** je více standardizovaný a podporovaný na webu, vhodný pro sémantická data a propojení různých datových zdrojů.
- **LPG** je flexibilnější a efektivnější pro dotazování a manipulaci s daty v rámci jedné aplikace nebo databáze.

### Slovník pro definici slovníků v RDF - RDF Schema (RDFS)

**Popis a použití:**
- RDF Schema (RDFS) je rozšíření RDF, které umožňuje definovat třídy a vlastnosti pro RDF data, což umožňuje organizaci a kategorizaci dat.
- RDFS se používá k definování ontologií, které poskytují kontext a význam pro data na sémantickém webu.

**Příklad:**
```turtle
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

ex:Person a rdfs:Class ;
  rdfs:label "Person" .

ex:knows a rdf:Property ;
  rdfs:domain ex:Person ;
  rdfs:range ex:Person .
```
V tomto příkladu je `ex:Person` definována jako třída a `ex:knows` jako vlastnost, která spojuje dvě osoby.

### Jazyky pro dotazování a transformaci grafových dat - SPARQL a Cypher

**1. SPARQL**

**Popis a použití:**
- SPARQL je dotazovací jazyk pro RDF data, který umožňuje extrakci a manipulaci s informacemi uloženými v RDF formátu.
- SPARQL se často používá na sémantickém webu pro dotazování nad RDF daty.

**Příklad dotazu:**
```sparql
SELECT ?name WHERE {
  ?person a ex:Person ;
          ex:name ?name .
}
```
Tento dotaz vrátí všechna jména osob v datasetu.

**2. Cypher**

**Popis a použití:**
- Cypher je dotazovací jazyk pro Labeled Property Graph model, zejména používaný v databázi Neo4j.
- Cypher umožňuje jednoduché a efektivní dotazování a manipulaci s grafovými daty.

**Příklad dotazu:**
```cypher
MATCH (p:Person)-[:KNOWS]->(friend)
RETURN p.name, friend.name
```
Tento dotaz vrátí všechny dvojice osob, kde jedna zná druhou.

Tyto informace jsou podrobně diskutovány v dokumentu na stránkách **24-28** pro RDF a LPG, **29-30** pro RDF Schema a **28-30** pro SPARQL a Cypher .