# Sčítání dvou čísel a výpis výsledku

```csharp
int a = 5;
  int b = 10;
  int result = a + b;
  Console.WriteLine($"Součet: {result}");
```

Tento kód ukazuje základní matematickou operaci a výpis výsledku:

**Řádek 1:** `int a = 5;`
- Vytváříme proměnnou jménem "a"
- `int` znamená, že bude obsahovat celé číslo
- Přiřazujeme jí hodnotu 5
- Středník ukončuje příkaz

**Řádek 2:** `int b = 10;`
- Stejně jako předtím, vytváříme druhou proměnnou "b"
- Obsahuje číslo 10

**Řádek 3:** `int result = a + b;`
- Vytváříme třetí proměnnou "result"
- Počítáme součet a + b (5 + 10 = 15)
- Výsledek 15 se uloží do proměnné result

**Řádek 4:** `Console.WriteLine($"Součet: {result}");`
- Vypíše text na obrazovku
- `$` před uvozovkami umožňuje vložit proměnnou do textu
- `{result}` se nahradí hodnotou proměnné (15)
- Na obrazovce se objeví: "Součet: 15"

Proměnné si můžete představit jako krabičky s nálepkami, do kterých ukládáme hodnoty. Později můžeme tyto hodnoty použít nebo změnit.
