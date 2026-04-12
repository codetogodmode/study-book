# Entry point aplikace — kde program začíná

## OBECNĚ

Každý C# program musí mít **entry point** — místo, kde začne běžet. To je metoda `Main` uvnitř třídy (většinou se jmenuje `Program`). Když spustíš `dotnet run`, .NET najde tuto metodu a začne ji vykonávat řádek po řádku.

```
class Program
{
    static void Main(string[] args)  ← TADY PROGRAM ZAČÍNÁ
    {
        Console.WriteLine("Hello!");
        Console.WriteLine("Druhý řádek");
        // Program skončí na konci Main metody
    }
}
```

**Slovníček:**
- **class Program** — třída (kontejner pro kód), jméno může být jakékoliv
- **static** — metoda patří k třídě, ne k objektu (zatím neřeš proč)
- **void** — metoda nic nevrací
- **string[] args** — argumenty z příkazového řádku (např. `dotnet run --verbose`)
- **Console.WriteLine** — vypíše text do konzole

## CTGM-SPECIFICKÉ

V našich template repozitářích (`template-console`, `template-webapi`) používáme **top-level programs** — moderní syntax bez `class Program`:

```
// Takto vypadají naše templaty (C# 10+)
Console.WriteLine("Hello from Calculator!");
Console.WriteLine("Program běží...");
```

Je to stejné jako klasický zápis, jen kratší. .NET si `class Program` a `Main` metodu vytvoří automaticky. Pro začátečníky je to jednodušší — méně syntaxe, víc focus na logiku.

**Kdy použít klasický zápis:**
- Když potřebuješ více tříd v jednom souboru
- V enterprise projektech (zvyk)
- Když pracuješ se starším .NET Framework

**Kdy použít top-level:**
- Console aplikace (naše projekty)
- Prototypy a experimenty
- Moderní .NET projekty

**Komentáře:** `//` na začátku řádku = poznámka pro tebe, program ji ignoruje.

Více o struktuře projektů: <https://github.com/codetogodmode/handbook/blob/main/github-guide.md>
