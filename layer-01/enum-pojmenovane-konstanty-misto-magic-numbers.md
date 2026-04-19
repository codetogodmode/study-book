# Enum — pojmenované konstanty místo magic numbers

## Co je enum

**Enum** je způsob, jak v C# definovat sadu pojmenovaných konstant místo používání "magic numbers" (tajemných čísel v kódu). Je to jako vytvoření vlastního datového typu s předem definovanými možnostmi.

```csharp
enum Den
{
    Pondeli,
    Utery,
    Streda,
    Ctvrtek,
    Patek,
    Sobota,
    Nedele
}
```

Místo psaní `1`, `2`, `3` v kódu píšeš `Den.Pondeli`, `Den.Utery`, `Den.Streda` — kód je čitelnější a méně náchylný na chyby.

## Proč používat enum

**1. Čitelnost kódu**
```csharp
// Špatně — co znamená 3?
if (stav == 3)
{
    Console.WriteLine("Objednávka je odeslána");
}

// Dobře — jasné
if (stav == StavObjednavky.Odeslana)
{
    Console.WriteLine("Objednávka je odeslána");
}
```

**2. Prevence chyb**
```csharp
enum Smer { Sever, Jih, Vychod, Zapad }

// Kompiler ti nedovolí napsat nesmysl
Smer mojSmer = Smer.SuperSever; // CHYBA — neexistuje
```

**3. IntelliSense podpora**
Když napíšeš `Den.` ve VS Code, zobrazí se ti všechny možnosti. U čísel tuhle pomoc nemáš.

## Převod uživatelského vstupu na enum

Uživatel píše text, ty ho musíš převést na enum hodnotu:

```csharp
enum Obtiznost
{
    Lehka = 1,
    Stredni = 2,
    Tezka = 3
}

Console.Write("Vyber obtížnost (1-lehká, 2-střední, 3-těžká): ");
string vstup = Console.ReadLine();

if (int.TryParse(vstup, out int cislo) && 
    Enum.IsDefined(typeof(Obtiznost), cislo))
{
    Obtiznost vybrana = (Obtiznost)cislo;
    Console.WriteLine($"Zvolil jsi: {vybrana}");
}
else
{
    Console.WriteLine("Neplatná volba!");
}
```

**Alternativa s názvem:**
```csharp
Console.Write("Vyber den (Pondeli, Utery, ...): ");
string vstup = Console.ReadLine();

if (Enum.TryParse<Den>(vstup, true, out Den vybranyDen))
{
    Console.WriteLine($"Vybral jsi: {vybranyDen}");
}
else
{
    Console.WriteLine("Neplatný den!");
}
```

## Praktické příklady

**Menu v konzolové appce:**
```csharp
enum MenuVolba
{
    PridatUkol = 1,
    ZobrazitUkoly = 2,
    SmazatUkol = 3,
    Konec = 4
}

Console.WriteLine("1. Přidat úkol");
Console.WriteLine("2. Zobrazit úkoly"); 
Console.WriteLine("3. Smazat úkol");
Console.WriteLine("4. Konec");

string volba = Console.ReadLine();
if (int.TryParse(volba, out int cislo) && 
    Enum.IsDefined(typeof(MenuVolba), cislo))
{
    MenuVolba akce = (MenuVolba)cislo;
    switch (akce)
    {
        case MenuVolba.PridatUkol:
            // logika pro přidání
            break;
        case MenuVolba.Konec:
            return;
    }
}
```

**Stav objektu:**
```csharp
enum StavUkolu
{
    Novy,
    Rozpracovany,
    Hotovy,
    Zruseny
}

class Ukol
{
    public string Nazev { get; set; }
    public StavUkolu Stav { get; set; } = StavUkolu.Novy;
    
    public void Dokoncit()
    {
        Stav = StavUkolu.Hotovy;
        Console.WriteLine($"Úkol '{Nazev}' je hotový!");
    }
}
```

## CTGM-SPECIFIC

V naší akademii používáš enum hlavně v Layer 1 projektech — kalkulačka s menu, todo list, jednoduché hry. Enum ti pomůže organizovat volby uživatele a stavy objektů bez magic numbers.

Více o datových typech najdeš v study-booku: <https://github.com/codetogodmode/study-book/blob/main/layer-01/zakladni-datove-typy-stavebni-kameny-pro-ukladani-dat.md>
