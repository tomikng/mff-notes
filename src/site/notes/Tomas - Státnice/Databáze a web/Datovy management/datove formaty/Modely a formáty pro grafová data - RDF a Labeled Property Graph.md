---
{"dg-publish":true,"permalink":"/tomas-statnice/databaze-a-web/datovy-management/datove-formaty/modely-a-formaty-pro-grafova-data-rdf-a-labeled-property-graph/","tags":["databaze_a_web","databaze","tomas"],"noteIcon":""}
---

> [!NOTE] ChatGPT
> Vygenerováno pomocí ChatGPT na zaklade prezentaci od Klimky
## RDF (Resource Description Framework)
**Popis a použití:**
- RDF je model grafových dat, který reprezentuje informace jako sadu trojic (subjekt, predikát, objekt). Tento model se široce používá pro sémantické modelování dat a propojení dat z různých zdrojů na webu.
![Pasted image 20240821133001.png](/img/user/assets/img/Pasted%20image%2020240821133001.png)
![Pasted image 20240821140537.png](/img/user/assets/img/Pasted%20image%2020240821140537.png)
### Formáty serializace dat
RDF model lze serializovat v několika formátech, z nichž každý slouží různým účelům a použitím.

#### 1. Turtle (Terse RDF Triple Language)
Turtle je lidsky čitelný formát serializace RDF, který je kompaktní a snadno pochopitelný, zejména pro ty, kteří se orientují v syntaxi RDF.
![Pasted image 20240821134429.png](/img/user/assets/img/Pasted%20image%2020240821134429.png)
![Pasted image 20240821134515.png](/img/user/assets/img/Pasted%20image%2020240821134515.png)
![Pasted image 20240821134555.png](/img/user/assets/img/Pasted%20image%2020240821134555.png)
![Pasted image 20240821134839.png](/img/user/assets/img/Pasted%20image%2020240821134839.png)
![Pasted image 20240821134951.png](/img/user/assets/img/Pasted%20image%2020240821134951.png)
**Příklad:**
```turtle
@prefix foaf: <http://xmlns.com/foaf/0.1/> .

<http://example.org/person/JohnDoe> 
  a foaf:Person ;
  foaf:name "John Doe" ;
  foaf:age 28 ;
  foaf:knows <http://example.org/person/JaneDoe> .
```

#### 2. N-Triples
N-Triples je textový formát pro kódování RDF grafů, navržený tak, aby byl jednoduchý a snadno parsovatelný.

**Příklad:**
```ntriples
<http://example.org/person/JohnDoe> <http://xmlns.com/foaf/0.1/name> "John Doe" .
<http://example.org/person/JohnDoe> <http://xmlns.com/foaf/0.1/age> "28"^^<http://www.w3.org/2001/XMLSchema#integer> .
```
![Pasted image 20240821134216.png](/img/user/assets/img/Pasted%20image%2020240821134216.png)
#### 3. TriG
TriG rozšiřuje Turtle o podporu pojmenovaných grafů, což umožňuje seskupování trojic do různých grafů v rámci jednoho dokumentu.

**Příklad:**
```trig
@prefix foaf: <http://xmlns.com/foaf/0.1/> .

{
  <http://example.org/person/JohnDoe> 
    a foaf:Person ;
    foaf:name "John Doe" ;
    foaf:age 28 ;
    foaf:knows <http://example.org/person/JaneDoe> .
}

GRAPH <http://example.org/graph1> {
  <http://example.org/person/JaneDoe>
    a foaf:Person ;
    foaf:name "Jane Doe" ;
    foaf:age 26 .
}
```

#### 4. N-Quads
N-Quads je rozšíření N-Triples, které přidává podporu pojmenovaných grafů, což umožňuje přidání názvu grafu vedle subjektu, predikátu a objektu.

**Příklad:**
```nquads
<http://example.org/person/JohnDoe> <http://xmlns.com/foaf/0.1/name> "John Doe" <http://example.org/graph1> .
<http://example.org/person/JohnDoe> <http://xmlns.com/foaf/0.1/age> "28"^^<http://www.w3.org/2001/XMLSchema#integer> <http://example.org/graph1> .
```

### Srovnání s Labeled Property Graph (LPG)
**Popis a použití:**
- RDF používá standardizovaný model, který je široce podporován na webu, a je zvláště užitečný pro propojení dat napříč různými doménami.
- LPG (Labeled Property Graph) je flexibilnější model, často používaný v grafových databázích jako Neo4j, kde uzly a hrany mohou mít vlastnosti a štítky.
![Pasted image 20240822090511.png](/img/user/assets/img/Pasted%20image%2020240822090511.png)![Pasted image 20240822090608.png](/img/user/assets/img/Pasted%20image%2020240822090608.png)
**Klíčové rozdíly:**
- **RDF** je více vhodné pro aplikace, které vyžadují interoperabilitu dat a sémantickou bohatost.
- **LPG** je lepší pro scénáře, kde je důležitý výkon a složité dotazování v rámci jedné aplikace.

### RDF Schema (RDFS)
**Popis a použití:**
- RDF Schema je rozšíření RDF, které umožňuje definovat třídy, vlastnosti a jejich vztahy, což usnadňuje vytvoření strukturovaných a organizovaných RDF dat.
![Pasted image 20240821135523.png](/img/user/assets/img/Pasted%20image%2020240821135523.png)
![Pasted image 20240821140012.png](/img/user/assets/img/Pasted%20image%2020240821140012.png)
**Příklad:**
```turtle
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

ex:Person a rdfs:Class ;
  rdfs:label "Osoba" .

ex:knows a rdf:Property ;
  rdfs:domain ex:Person ;
  rdfs:range ex:Person .
```

![Pasted image 20240821140227.png](/img/user/assets/img/Pasted%20image%2020240821140227.png)
### Dotazovací jazyky
#### 1. SPARQL
- SPARQL je dotazovací jazyk pro RDF, který umožňuje dotazování nad RDF datovými sadami a manipulaci s těmito daty.

**Příklad:**
```sparql
SELECT ?name WHERE {
  ?person a ex:Person ;
          ex:name ?name .
}
```

#### 2. Cypher
- Cypher je dotazovací jazyk pro Labeled Property Graphs, používaný především v databázi Neo4j.

**Příklad:**
```cypher
MATCH (p:Person)-[:KNOWS]->(friend)
RETURN p.name, friend.name
```