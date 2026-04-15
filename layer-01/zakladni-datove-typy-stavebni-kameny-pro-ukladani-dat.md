# Základní datové typy — stavební kameny pro ukládání dat

## OBECNÁ PRAXE

Datové typy říkají počítači, jaký druh informace chceš uložit a jak s ní pracovat. Je to jako označení krabic — když napíšeš "křehké", pošťák ví, že má zacházet opatrně.

C# má několik základních typů:

**Čísla celá:**
```
int věk = 25;
int počet = -10;
```

**Čísla s desetinnou čárkou:**
```
double cena = 199.99;
double teplota = -5.2;
```

**Text:**
```
string jméno = "Martin";
string zpráva = "Dobrý den!";
```

**Pravda/nepravda:**
```
bool jeOnline = true;
bool máZkušenosti = false;
```

**Znak (jedno písmeno):**
```
char známka = 'A';
char první = 'M';
```

Proč typy existují? Počítač potřebuje vědět, jestli `"10"` je text nebo číslo — s textem nemůžeš počítat, s číslem ano.

**Běžné chyby:**
- Snaha počítat s textem: `"10" + 5` → chyba nebo neočekávaný výsledek
- Příliš velké číslo pro `int` → použij `long`
- Ztráta přesnosti: `int výsledek = 10 / 3;` → bude 3, ne 3.33

## CTGM-SPECIFIC

V našich projektech začínáme s praktickými příklady. Typické použití v konzolových aplikacích:

```
Console.Write("Zadej své jméno: ");
string jméno = Console.ReadLine(); // vstup od uživatele je vždy string

Console.Write("Zadej svůj věk: ");
int věk = int.Parse(Console.ReadLine()); // převod string → int

bool jeVětší = věk >= 18;
Console.WriteLine($"Jsi plnoletý: {jeVětší}");
```

Později se naučíš používat `var` keyword — kompilátor typ odhadne sám:
```
var zpráva = "Ahoj"; // automaticky string
var číslo = 42;      // automatически int
```

Ale na začátku píšeme typy explicitně — abys rozuměl, co se děje.
