# Datové typy v C# - základní stavební kameny programování

Datové typy říkají počítači, jaký druh informace ukládáme do proměnné. Je to jako označení krabičky - víme, co do ní patří a co s tím můžeme dělat.

**Základní datové typy:**

`int` - celá čísla (-2, 0, 42, 1000)
```csharp
int vek = 25;
int pocetLidi = 150;
```

`string` - text (vždy v uvozovkách)
```csharp
string jmeno = "Petr";
string zprava = "Ahoj světe!";
```

`double` - desetinná čísla (3.14, -5.7, 0.1)
```csharp
double cena = 199.90;
double teplota = -5.5;
```

`bool` - pravda/nepravda (true/false)
```csharp
bool jeSlunecno = true;
bool jeVikend = false;
```

`char` - jeden znak (v apostrofech)
```csharp
char pismeno = 'A';
char symbol = '?';
```

**Proč jsou důležité:**
Každý typ má jiné vlastnosti - s čísly můžeme počítat, texty spojovat, boolean hodnoty používat v podmínkách. Pokud použijeme špatný typ, program nefunguje nebo dělá neočekávané věci.

```csharp
int a = 5;
int b = 3;
int vysledek = a + b; // = 8

string prvni = "Hello";
string druhy = " World";
string spojeny = prvni + druhy; // = "Hello World"
```

C# je "strongly typed" jazyk - musíme vždy říct, jaký typ proměnná má, a nemůžeme do ní pak uložit něco jiného.
