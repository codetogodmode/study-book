# Cykly — jak opakovat činnosti v programu

## OBECNÁ PRAXE

Cyklus (loop) je konstrukce, která ti umožní **opakovat kus kódu vícekrát**, aniž bys ho musel psát znovu a znovu. Jako když v kuchyni nakrájíš 10 rajčat — nenapíšeš si 10× "nakroj rajče", ale řekneš "10× opakuj: nakroj rajče".

V programování máme dva hlavní typy cyklů:

**For cyklus** — používáš když **víš předem kolikrát** chceš něco opakovat:
```
for (start; podmínka; krok) {
    // kód co se má opakovat
}
```

**While cyklus** — používáš když **nevíš předem kolikrát** se to bude opakovat, ale víš kdy přestat:
```
while (podmínka je splněná) {
    // kód co se má opakovat
}
```

### For cyklus s iterační proměnnou

**Iterační proměnná** (často `i`, `j`, `k`) je čítač, který sleduje "kolikátá jsme v pořadí":

```
for (int i = 0; i < 5; i++) {
    Console.WriteLine($"Iterace číslo: {i}");
}
```

Výstup:
```
Iterace číslo: 0
Iterace číslo: 1
Iterace číslo: 2
Iterace číslo: 3
Iterace číslo: 4
```

**Co se děje:**
- `int i = 0` — začni s čítačem na 0
- `i < 5` — opakuj dokud je i menší než 5
- `i++` — po každém opakování zvyš i o 1

### While cyklus

```
int pokus = 1;
while (pokus <= 3) {
    Console.WriteLine($"Pokus číslo {pokus}");
    pokus++;
}
```

Výstup:
```
Pokus číslo 1
Pokus číslo 2
Pokus číslo 3
```

### Praktické příklady

**Výpis čísel od 1 do 10:**
```
for (int cislo = 1; cislo <= 10; cislo++) {
    Console.WriteLine(cislo);
}
```

**Násobková tabulka:**
```
int cislo = 7;
for (int i = 1; i <= 10; i++) {
    Console.WriteLine($"{cislo} × {i} = {cislo * i}");
}
```

**Hádání čísla (while):**
```
Random random = new Random();
int tajneCislo = random.Next(1, 11);
int tip = 0;

while (tip != tajneCislo) {
    Console.Write("Hádej číslo od 1 do 10: ");
    tip = int.Parse(Console.ReadLine());
    
    if (tip != tajneCislo) {
        Console.WriteLine("Špatně, zkus to znovu!");
    }
}

Console.WriteLine("Správně! Číslo bylo " + tajneCislo);
```

**Sčítání čísel dokud uživatel nezadá 0:**
```
int soucet = 0;
int cislo = -1; // cokoliv kromě 0

while (cislo != 0) {
    Console.Write("Zadej číslo (0 = konec): ");
    cislo = int.Parse(Console.ReadLine());
    soucet += cislo;
}

Console.WriteLine($"Součet všech čísel: {soucet}");
```

## CTGM-SPECIFICKÉ

V našich prvních projektech v Layer 1 budeš cykly používat hlavně pro:
- **Opakování menu** aplikace (while cyklus dokud uživatel nezvolí "ukončit")
- **Procházení seznamů** úkolů nebo položek (for cyklus)
- **Validace vstupu** (while dokud uživatel nezadá správnou hodnotu)

Kompletní průvodce prací s kódem a Git workflow najdeš v <https://github.com/codetogodmode/handbook/blob/main/github-guide.md>.
