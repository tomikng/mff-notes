---
{"dg-publish":true,"permalink":"/tomas-statnice/databaze-a-web/databaze/poznamky/moderni-databazove-systemy/","tags":["databaze","databaze_a_web","tomas"],"noteIcon":""}
---

## Základní třídy moderních databázových systémů
### Databázové modely
-   První generace – navigační: Hierarchický model (stromy), Síťový
    model (grafy)
-   Druhá generace – relační
-   Třetí generace – post-relační
    -   Rozšíření relačního modelu – objektově-relační – objekty, třídy,
        dědičnost
    -   Nové modely navazující na populární technologie – objekty, XML,
        NoSql (key/value, column, document, graph, …) – Big Data
    -   Multi-model systém, NewSQL – zpátky k relacím
### Relační model
-   Ukládání objektů a jejich vzájemných asociací do <mark style="background: #FFF3A3A6;">tabulek</mark> (relací)
-   Řádek v tabulce (člen relace) = objekt/asociace, sloupec (atribut) =
    atribut objektu/asociace
-   Schéma tabulky (relace) = název schématu + seznam atributů a jejich
    typů
-   Základní omezení integrity – unikátní identifikace řádku, simple
    type atributy, hodnoty NULL (žádné "díry")
-   Optimální pro některé aplikace, ale: nepodporuje <mark style="background: #FFF3A3A6;">složité datové typy</mark>
    -   Normalizace dat do tabulkové podoby ovlivňuje výkon při
        vyhledávání rozsáhlých, <mark style="background: #FFF3A3A6;">složitých a hierarchicky strukturovaných  dat</mark>
    -   objevily se objektově orientované programovací jazyky – koncept uživatelsky definovaných tříd
### Hierarchický model
-   Data jsou uspořádána do záznamů, které se rekurzivně skládají z
    jiných záznamů
-   IBM’s IMS (Information Management System) - Jeden z prvních komerčně
    dostupných DBMS.
-   Les stromů – vztahy typu 1:n
    -   První nezávislý = redundance – záznam nemůže být uložen ve 2
        různých stromech, aniž by se duplikoval
-   Zpracování dat: hierarchické, počínaje kořenem, hloubkové,
    procházení zleva doprava
    -   První ukládání na pásky – lineární přístup
    -   Později (příchod disků) přímý přístup díky technikám hashování a
        B-stromů
### Síťový model
-   Datové záznamy propojené binárními vztahy, blízko ER modelu
    -   Zpracování dat: navigační primitiva, podle kterých se k záznamům
        přistupuje, aktualizují se jeden po druhém; Relační
        dotazovací jazyky: množinová orientace
-   Uzly = typy záznamů – reprezentují entity reálného světa, mají
    atomická nebo složená pole, záznam = datová jednotka (má
    identifikátor)
-   Hrany = typy množin – typ vztahu 1:n, seznam záznamů = hlavní
    záznam + členové množiny

### Big Data

1. **Popis a vlastnosti:**
   - **Big Data** se týká masivních datových souborů, které jsou příliš velké a komplexní, než aby je bylo možné zpracovat tradičními databázovými systémy. Big Data se vyznačují následujícími charakteristikami:
     - **Objem (Volume):** Obrovské množství dat produkovaných každý den, například z IoT zařízení, sociálních sítí, nebo finančních transakcí.
     - **Rychlost (Velocity):** Rychlost, jakou jsou data generována a potřebná k analýze. Příkladem může být analýza dat v reálném čase z Twitteru nebo datových toků z finančních transakcí.
     - **Různorodost (Variety):** Různé formáty dat, jako jsou strukturovaná, nestrukturovaná a semi-strukturovaná data, například textové dokumenty, videa, zvukové soubory a senzory.
     - **Proměnlivost (Variability):** Změna ve struktuře a kvalitě dat v průběhu času. Příkladem je sezónní změna v datech z e-commerce nebo náhlé změny ve vzorcích chování uživatelů.

2. **Výzvy Big Data:**
   - **Ukládání:** Tradiční systémy často nedokáží efektivně ukládat a spravovat tak velké objemy dat.
   - **Zpracování:** Potřeba paralelního zpracování velkých objemů dat vyžaduje distribuované systémy, jako jsou Hadoop a Spark.
   - **Integrace:** Kombinace různorodých datových zdrojů do jednoho konzistentního formátu.
   - **Bezpečnost a soukromí:** Ochrana citlivých dat je klíčová, zvláště při práci s tak obrovskými a různorodými datovými sadami.

3. **Big Data Ekosystém:**
   - **Apache Hadoop:** Open-source rámec pro distribuované ukládání a zpracování velkých datových sad. Hadoop používá HDFS (Hadoop Distributed File System) pro ukládání dat a MapReduce pro paralelní zpracování.
   - **Apache Spark:** Rámec pro zpracování dat, který nabízí rozšířené možnosti nad Hadoopem, jako je in-memory zpracování, což umožňuje rychlejší analýzu dat.
   - **Data Lakes:** Úložiště pro velké množství nestrukturovaných a strukturovaných dat, která mohou být zpracována podle potřeby. Umožňuje ukládat data ve své původní podobě bez potřeby předběžného zpracování (schema-on-read).

### Princip MapReduce

1. **Princip a aplikace:**
   - **MapReduce** je programovací model a související implementace pro zpracování velkých datových sad paralelně na velkém počtu strojů (clusterů). Skládá se ze dvou hlavních fází:
     - **Map fáze:** Rozděluje úlohu na menší podúlohy a zpracovává každý záznam jednotlivě. Vstup je převeden na dvojice klíč-hodnota.
     - **Reduce fáze:** Shrnuje výsledky z *Map* fáze tak, že kombinuje všechny hodnoty přiřazené ke stejnému klíči.
   - **Pseudokódu:**
```python
# Map Function
def map(key, value):
    # Perform some operation on the value to generate intermediate key-value pairs
    for element in process(value):
        emit(intermediate_key, intermediate_value)

# The framework automatically handles shuffling and sorting of intermediate key-value pairs

# Reduce Function
def reduce(intermediate_key, values):
    # Aggregate or process the list of values for each intermediate key
    result = aggregate(values)
    emit(intermediate_key, result)
```
- Příklad (Četnost slov)
```python
def map(key, value):
	for each word in value:
		emit(word, 1)

def reduce(key, values):
	sum = 0
	for each value in values:
		sum += value
	emit(key, sum)
```
   - **Výhody:** Škálovatelnost, odolnost vůči chybám díky distribuci dat a úkolů.
   - **Nevýhody:** Omezená flexibilita, komplexnost implementace pro některé typy analýz.

### NoSQL databáze

1. **Typy a vlastnosti:**
   - **Dokumentové databáze:** Ukládají data ve formě dokumentů (např. JSON, BSON). Každý dokument může obsahovat různé typy a množství dat.
   - **Klíč-hodnota databáze:** Data jsou organizována do párů klíč-hodnota, kde klíč je unikátní identifikátor a hodnota může být libovolná data.
   - **Sloupcové databáze:** Umožňují ukládání dat po sloupcích, což zlepšuje výkon při analytických dotazech na velkých datových sadách.
   - **Grafové databáze:** Zaměřené na modelování a dotazování se na složité vztahy mezi daty, například vztahy v sociálních sítích.

2. **Příklad rozdílů:**
   - **Relace vs. Dokument:** V relačních databázích jsou data uložena v tabulkách s pevně danou strukturou, zatímco v dokumentových databázích mohou mít dokumenty různou strukturu a obsahovat složitější hierarchie.

### Grafové databáze

1. **Datový model:**
   - **Popis:** Grafová databáze ukládá data jako uzly (entity) a hrany (vztahy). Tento model je výkonný pro aplikace, kde jsou data silně propojena a kde je třeba provádět složité dotazy na vztahy mezi entitami.
   - **Příklad:** Sociální síť, kde uzly reprezentují uživatele a hrany představují přátelství mezi nimi.

### Multi-model databáze a Polystore

1. **Rozdíly, výhody a nevýhody:**
   - **Multi-model databáze:** Tyto systémy podporují více datových modelů (např. dokumentový, grafový, relační) v rámci jednoho databázového systému. Umožňují ukládání a dotazování dat různými způsoby podle specifických potřeb aplikace.
   - **Polystore:** Integruje více různých databázových systémů a umožňuje provádění dotazů napříč těmito systémy, aniž by bylo nutné data migrovat do jednoho systému.

2. **Příklad multi-model dotazu:**
   - **Dotaz:** Umožňuje vyhledávat data z různých modelů v jednom dotazu, například kombinace relačních dat a dokumentových dat v jednom dotazu v rámci multi-model databáze.
   - **Možné problémy:** Složitost a snížení výkonu kvůli nutnosti kombinovat různé dotazovací mechanizmy, složitější optimalizace a ladění.