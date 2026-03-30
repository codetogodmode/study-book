# int a = 5;

```csharp
int a = 5;
  int b = 10;
  int result = a + b;
  Console.WriteLine($"Součet: {result}");
```

Ahoj! Podívejme se na tento jednoduchý kód krok za krokem:

**Řádek 1: `int a = 5;`**
Vytváříme "krabičku" s názvem `a` a vložíme do ní číslo 5. Slovo `int` říká počítači, že v této krabičce budou celá čísla (integer = celé číslo). Středník na konci je jako tečka ve větě - říká počítači, že příkaz skončil.

**Řádek 2: `int b = 10;`**
Totéž jako předtím, jen vytváříme druhou krabičku `b` s číslem 10.

**Řádek 3: `int result = a + b;`**
Vytváříme třetí krabičku `result`. Do ní vložíme výsledek sčítání obsahu krabiček `a` a `b`. Počítač si vezme 5 + 10 = 15 a uloží to do `result`.

**Řádek 4: `Console.WriteLine($"Součet: {result}");`**
Tady říkáme počítači: "Napiš na obrazovku text." `Console.WriteLine` je příkaz pro výpis. Dolar `$` před uvozovkami znamená, že můžeme do textu vložit proměnné pomocí složených závorek `{}`. Takže se vypíše: "Součet: 15"

Celý program tedy sečte dvě čísla a výsledek ukáže na obrazovce. Je to jako kalkulačka, kterou jsme si naprogramovali!
