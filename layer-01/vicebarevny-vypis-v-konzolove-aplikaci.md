# Vícebarevný výpis v konzolové aplikaci

**OBECNÁ PRAXE:**
Konzolové aplikace standardně píšou text v jedné barvě (většinou bílá na černé). Ale můžeš barvu textu i pozadí změnit, aby byl výstup čitelnější a uživatelsky přívětivější. V C# to děláš pomocí `Console.ForegroundColor` (barva písma) a `Console.BackgroundColor` (barva pozadí).

**Proč to používat:**
- **Rozlišení typů zpráv** — chyby červeně, úspěchy zeleně
- **Lepší orientace** — důležité informace zvýrazněné
- **Profesionální vzhled** — aplikace nevypadá jako "škola"

**Základní použití:**
```
Console.ForegroundColor = ConsoleColor.Red;
Console.WriteLine("Chyba: Soubor nenalezen!");
Console.ResetColor(); // vrátí původní barvy
```

**Praktické příklady:**

```
// Chybové hlášky červeně
Console.ForegroundColor = ConsoleColor.Red;
Console.WriteLine("❌ Neplatný vstup!");
Console.ResetColor();

// Úspěšné operace zeleně
Console.ForegroundColor = ConsoleColor.Green;
Console.WriteLine("✅ Soubor úspěšně uložen");
Console.ResetColor();

// Upozornění žlutě
Console.ForegroundColor = ConsoleColor.Yellow;
Console.WriteLine("⚠️  Disk je skoro plný");
Console.ResetColor();

// Informace modře
Console.ForegroundColor = ConsoleColor.Blue;
Console.WriteLine("ℹ️  Načítám data...");
Console.ResetColor();
```

**Smysluplné použití v kalkulačce:**
```
Console.Write("Zadej první číslo: ");
double a = double.Parse(Console.ReadLine());

Console.Write("Zadej operaci (+, -, *, /): ");
string operace = Console.ReadLine();

if (operace == "/")
{
    Console.ForegroundColor = ConsoleColor.Yellow;
    Console.WriteLine("⚠️  Pozor na dělení nulou!");
    Console.ResetColor();
}

// Výsledek zvýrazněný
Console.ForegroundColor = ConsoleColor.Cyan;
Console.WriteLine($"Výsledek: {vysledek}");
Console.ResetColor();
```

**Tip:** Vždy používej `Console.ResetColor()` po barevném výpisu, jinak všechny další texty zůstanou v té barvě.

**CTGM-SPECIFICKÉ:**
V našich template projektech (`template-console`) najdeš ukázku barevného výpisu. Používej barvy smysluplně — ne každý řádek jinou barvou, ale konzistentně podle typu zprávy. Více o organizaci kódu a best practices v <https://github.com/codetogodmode/handbook/blob/main/definition-of-done.md>
