---
{"dg-publish":true,"permalink":"/tomas-statnice/spolecna-informatika/programovaci-jazyk/primitivni-objektove-typy/hodnotove-a-referencni-typy/","tags":["tomas","spolecna_informatika","programovaci_jazyky"],"noteIcon":""}
---

#### Hodnotové typy
Hodnotové typy v C# ukládají přímo data a jsou uloženy na zásobníku (stack). Mezi nejčastější hodnotové typy patří **čísla** (`int`, `double`, `float`, `decimal`) a **výčtové typy** (`enum`), které reprezentují pevně danou sadu konstant. Hodnotové typy jsou rychlé, protože práce se zásobníkem je obecně velmi efektivní.

**Příklad:**
```csharp
int cislo = 42;
enum Barva { Cervena, Zelena, Modra };
```

#### Referenční typy
Referenční typy ukládají odkaz (referenci) na skutečná data, která jsou uložena na haldě (heap). Typickými referenčními typy jsou **třídy** (`class`), **rozhraní** (`interface`), **delegáti** a **pole**. Práce s referenčními typy může být náročnější na výkon kvůli alokaci na haldě a nutnosti garbage collectoru pro správu paměti.

**Příklad:**
```csharp
string text = "Ahoj";
class Osoba { public string Jmeno; }
```

#### Klíčové rozdíly mezi hodnotovými a referenčními typy:
- **Hodnotové typy**: Data jsou uložena přímo, změny se provádějí na lokální kopii.
- **Referenční typy**: Data jsou uložena na haldě, změny prováděné na kopii ovlivňují původní objekt.