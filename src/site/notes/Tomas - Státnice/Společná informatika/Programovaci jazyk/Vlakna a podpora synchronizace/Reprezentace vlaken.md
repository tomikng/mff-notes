---
{"dg-publish":true,"permalink":"/tomas-statnice/spolecna-informatika/programovaci-jazyk/vlakna-a-podpora-synchronizace/reprezentace-vlaken/","tags":["tomas","spolecna_informatika","programovaci_jazyky"],"noteIcon":""}
---

### Vlákna a podpora synchronizace v C#

#### Reprezentace vláken v C#

V C# jsou [[Tomas - Státnice/Společná informatika/architektury os a pc/Paralelní programování a synchronizace#^df6511\|vlákna]] (threads) reprezentována třídou `Thread` z jmenného prostoru `System.Threading`. Vlákno představuje nejmenší jednotku zpracování, která může být naplánována operačním systémem.

**Příklad vytvoření a spuštění vlákna:**
```csharp
using System;
using System.Threading;

class Program
{
    static void Main()
    {
        Thread vlakno = new Thread(NovaMetoda);
        vlakno.Start(); // Spustí nové vlákno
    }

    static void NovaMetoda()
    {
        Console.WriteLine("Vlákno běží!");
    }
}
```

V tomto příkladu je vytvořeno nové vlákno pomocí třídy `Thread`, které následně vykoná metodu `NovaMetoda`.

#### Základní operace na vláknech:
- **Spuštění vlákna**: `Thread.Start()` spustí vlákno.
- **Zastavení vlákna**: V C# není podporováno přímé zastavení vlákna z důvodu bezpečnosti, ale lze využít metody jako `Thread.Interrupt()` nebo kontrolní mechanismy pomocí vlajek.
- **Join**: Metoda `Thread.Join()` blokuje volající vlákno, dokud se spuštěné vlákno nedokončí.
- **Sleep**: `Thread.Sleep(int milliseconds)` způsobí, že vlákno přestane na danou dobu vykonávat jakoukoli práci.

#### Synchronizace vláken
Synchronizace je proces zajištění toho, že více vláken může bezpečně přistupovat ke sdíleným prostředkům bez konfliktů.

**Příklad synchronizace pomocí `lock`:**
```csharp
private static readonly object zamek = new object();

static void BezpecnaMetoda()
{
    lock(zamek)
    {
        // Kritická sekce
        Console.WriteLine("Bezpečný přístup");
    }
}
```

#### Pokročilé možnosti
- **Task Parallel Library (TPL)**: Moderní způsob práce s vlákny v C#.
- **Async/Await**: Usnadňuje práci s asynchronními úlohami, přičemž vlákna jsou spravována automaticky.

### Shrnutí
- **Třída `Thread`** v C# slouží k reprezentaci a správě vláken.
- **Synchronizace** pomocí `lock`, `Monitor`, nebo dalších nástrojů zajišťuje bezpečný přístup ke sdíleným prostředkům.
- Moderní metody jako TPL a `async/await` usnadňují práci s paralelním a asynchronním programováním.