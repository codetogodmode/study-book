# Proměnné — základní stavební kameny programu

## Co je to proměnná

Proměnná je **pojmenované úložiště** pro hodnotu v paměti počítače. Představ si to jako **krabičku s popiskem**, do které si můžeš uložit hodnotu a později ji použít.

```csharp
string jmeno = "Petr";
int vek = 25;
```

## Deklarace proměnných

**Deklarace** znamená vytvoření nové proměnné. Říkáš programu: "Vytvořte mi krabičku tohoto typu s tímhle názvem."

```csharp
string jmeno;        // Deklarace — vytvořil jsem prázdnou krabičku pro text
int vek;             // Deklarace — vytvořil jsem prázdnou krabičku pro číslo
bool jeStudent;      // Deklarace — vytvořil jsem prázdnou krabičku pro ano/ne
```

Zatím jsou krabičky prázdné — obsahují **výchozí hodnoty** (prázdný string, nula, false).

## Přiřazování hodnot

**Přiřazení** znamená vložení konkrétní hodnoty do proměnné. Používáš k tomu operátor `=`.

```csharp
jmeno = "Anna";      // Do krabičky "jmeno" vložím text "Anna"
vek = 30;            // Do krabičky "vek" vložím číslo 30
jeStudent = true;    // Do krabičky "jeStudent" vložím hodnotu "ano"

Console.WriteLine($"Ahoj {jmeno}, je ti {vek} let.");
// Výstup: Ahoj Anna, je ti 30 let.
```

Můžeš deklarovat a přiřadit najednou:
```csharp
string mesto = "Praha";  // Deklarace + přiřazení v jednom kroku
```

## Uživatelský vstup — ReadLine()

Program může číst text, který uživatel napíše. Používá se method `Console.ReadLine()`.

```csharp
Console.Write("Jak se jmenuješ? ");
string uzivatelJmeno = Console.ReadLine();
Console.WriteLine($"Ahoj {uzivatelJmeno}!");
```

**Pozor:** `ReadLine()` **vždy** vrací `string` — i když uživatel napíše číslo.

## Parsování — převod textu na čísla

Když chceš číselný vstup, musíš text **parsovat** (převést) na číslo.

```csharp
Console.Write("Kolik je ti let? ");
string vstup = Console.ReadLine();
int vek = int.Parse(vstup);

Console.WriteLine($"Za 10 let ti bude {vek + 10} let.");
```

**Bezpečnější parsování:**
```csharp
Console.Write("Zadej číslo: ");
string vstup = Console.ReadLine();

if (int.TryParse(vstup, out int cislo))
{
    Console.WriteLine($"Zadal jsi číslo: {cislo}");
}
else
{
    Console.WriteLine("To není platné číslo!");
}
```

## Praktický příklad

```csharp
// Kalkulačka pro výpočet obdélníka
Console.WriteLine("=== Výpočet plochy obdélníka ===");

Console.Write("Zadej šířku: ");
string vstupSirka = Console.ReadLine();
double sirka = double.Parse(vstupSirka);

Console.Write("Zadej výšku: ");
string vstupVyska = Console.ReadLine();
double vyska = double.Parse(vstupVyska);

double plocha = sirka * vyska;

Console.WriteLine($"Plocha obdélníka je {plocha} cm²");
```

## Klíčové body

- **Deklarace:** Vytváříš novou proměnnou s typem a názvem
- **Přiřazení:** Vkládáš hodnotu do proměnné operátorem `=`
- **ReadLine():** Číst vstup od uživatele — vždy je to string
- **Parsování:** Převést string na jiný typ (`int.Parse()`, `double.Parse()`)
- **TryParse():** Bezpečný převod — nekončí chybou při neplatném vstupu
