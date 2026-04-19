# Session 3 — Enum, podmínky, funkční Calculator

**Datum:** 19. 4. 2026 (neděle)
**Přítomni:** Martin, Matěj, Terka, Petr, Petra, Michael
**Omluveni/absent:** Hanka (off), Ondra (sleduje pasivně přes záznamy — časové vytížení, potvrzeno DM 15. 4.)
**Layer:** 1 (Console & Git)
**AI režim:** EXPLAIN only
**Trvání:** ~90 min (striktní limit dodržen)

## Co se probíralo

Session 3 navázala na S2, kde propadl enum. Začala rekapitulací S2 úkolů (Petr i Petra dokončili dnes odpoledne). Hlavní obsah: enum jako vlastní datový typ, if/else/else if pro rozhodování, složené podmínky s `&&` a `||`, a kompletní implementace funkční kalkulačky. Cykly (while, for) propadly do S4 kvůli dodrženému 90min limitu. Na konci feedback round od členů — všichni v pohodě s tempem a formátem.

## Klíčové koncepty

### Enum — vlastní datový typ

Motivace přes "magic numbers": `if (choice == 2)` — kdo ví, co to 2 znamená? Proto si vytvoříme vlastní datový typ, který má pojmenované konstantní hodnoty.

```csharp
namespace Calculator;

enum Operation
{
    Add,        // 0
    Subtract,   // 1
    Multiply,   // 2
    Divide      // 3
}

class Program
{
    static void Main(string[] args)
    {
        // ...
    }
}
```

Klíčové body:
- Enum se definuje **mimo `class Program`** (uvnitř `namespace`)
- Indexace od **0** (všechno v programování začíná od 0)
- `enum` = zkratka pro `enumeration` = výčet konstantních hodnot
- Cast int → enum: `Operation op = (Operation)(choice - 1);` (konverze, ne parsování)
- Rozdíl: **parsování** je text → číslo, **casting** je mezi jinými datovými typy

### if / else / else if — rozhodování

Demo scénář "má Terka žízeň?" — program se zeptá, podle odpovědi reaguje různě.

```csharp
if (zizen == "ano")
{
    Console.WriteLine("Terka si dala drinka");
}
else if (zizen == "trochu")
{
    Console.WriteLine("Terka neví, co chce");
}
else
{
    Console.WriteLine("Terka si nedala nic");
}
```

Klíčové:
- `==` je **porovnání** (dvě rovnítka), `=` je **přiřazení** (jedno rovnítko)
- Větve jsou **vyhodnocovány shora dolů** — první splněná se provede, zbytek přeskočí
- `else` chytne **cokoli jiného** (napíšu "jo" / "prdel" / "" — spadne do else)
- C# je **case sensitive**: `"ano"` ≠ `"Ano"` ≠ `"ANO"`. Řeší se `.ToLower()` na vstupu

### Složené podmínky — && a ||

- `&&` = **AND** (a zároveň) — oba výroky musí platit
- `||` = **OR** (nebo) — stačí, aby jeden platil
- `!=` = **není rovno** (negace porovnání)

Aplikace v kalkulačce:

```csharp
// Validace vstupu — mimo rozsah 1-4
if (choiceNumber < 1 || choiceNumber > 4)
{
    Console.WriteLine("Napsal jsi špatné číslo");
    return;
}
```

**Princip DRY** (Don't Repeat Yourself) — místo dvou podmínek s duplikovaným kódem jedna složená.

### Komentáře v kódu

Terka si všimla zelených textů v Petrově kódu (Petr si kopíroval Martinovy komentáře ze S2 dema) a zeptala se, co to je. Martin vysvětlil:

```csharp
// Dvě lomítka začínají komentář
Console.WriteLine("Hello"); // komentář může být i za řádkem kódu
// Počítač tenhle řádek ignoruje, slouží jen pro programátora
```

Klíčové:
- Komentář začíná **dvěma lomítky** `//`
- Všechno za `//` do konce řádku počítač **ignoruje**
- Slouží **pro programátora**, aby se líp vyznal v kódu
- Pozor: pokud zakomentuješ kus kódu (`// Console.WriteLine(...)`), přestane se provádět — využívá se pro dočasné vypínání kódu

### return — ukončení programu

`return` v `static void Main` okamžitě ukončí program. Užitečné při validaci vstupu — když uživatel zadá špatnou hodnotu, vypíšeme chybu a skončíme.

### Defaultní hodnota při deklaraci

Kompilátor hlásí chybu "nepřiřazená proměnná", když přiřazení je uvnitř if/else větví a on neví, že vždy některá spadne. Řešení: `float result = 0f;` — defaultní hodnota při deklaraci. `0f` = float zero (suffix `f` říká kompilátoru, že je to float, ne int).

## Diskuse a otázky

- **Petr** navrhl alternativu: "Nahradit 0,1,2,3 za znaky +,-,*,/" → Martin: Jde to, ale potřeboval by sis udělat mapu (symbol → operace). Dictionary se naučíme na konci Layer 1.
- **Petra** se ptala: "Musí být hodnoty enumu anglicky?" → Ne, i české fungují. Ale tlačíme na angličtinu kvůli konvenci.
- **Petr** se ptal: "Dalo by se místo `choice - 1` napsat `choice--`?" → Ano, ale pozor: `choice--` uloží výsledek zpět do `choice`, `choice - 1` ne. Různá sémantika.
- **Petra** se ptala: "Může být enumů víc?" → Ano, kolik chceš. Každý musí mít jiný název.
- **Terka** se ptala: "Jak odlišit velké a malé ano?" → Case sensitive jazyk. Řešení: `zizen.ToLower()` před porovnáním.
- **Terka** se ptala: "A kdyby napsala jo nebo má místo ano?" → Potřebovala bys mapu. Enum typu souhlasu (souhlas / částečný souhlas / nesouhlas) + překlad frází. Zatím neděláme.
- **Petra** implementovala větev pro násobení — napsala kompletní `else if (choice == Operation.Multiply) { result = firstNumber * secondNumber; }` správně.
- **Petr** implementoval větev pro dělení **včetně kontroly dělení nulou** — vnořená podmínka `if (secondNumber != 0) { result = ... } else { Console.WriteLine("Dělit se nedá nulou"); }`. Martin ukázal alternativu přes `&&`: `else if (choice == Operation.Divide && secondNumber == 0)`.

## Kód a ukázky

**Finální stav Calculator.cs po S3** — kalkulačka plně funguje s:
- Menu pro výběr operace (1-4)
- Enum Operation (Add, Subtract, Multiply, Divide)
- Validace vstupu (`choiceNumber < 1 || choiceNumber > 4` → chyba + return)
- Parsování dvou čísel typu float
- if/else/else if pro 4 operace
- Divide-by-zero kontrola (vnořená podmínka)
- Defaultní hodnota `float result = 0f;`
- Vypsání výsledku se string interpolací

**Testováno live:**
- 40 + 50 = 90 ✓
- 70 − 120 = -50 ✓
- 12 × 11 = 132 ✓
- 20 / 0 → "nulou se nedá dělit" ✓
- 10 / 4 = 2.5 ✓

## Odkazy

- **Demo Calculator — aktualizovaný kód po S3:** <https://github.com/codetogodmode/demo-calculator>
- **Enum — pojmenované konstanty místo magic numbers:** <https://github.com/codetogodmode/study-book/blob/main/layer-01/enum-pojmenovane-konstanty-misto-magic-numbers.md>
- **Podmínky a logické operátory — rozhodování v programu:** <https://github.com/codetogodmode/study-book/blob/main/layer-01/podminky-a-logicke-operatory-rozhodovani-v-programu.md>
- **Komentáře v kódu — poznámky pro programátory:** <https://github.com/codetogodmode/study-book/blob/main/layer-01/komentare-v-kodu-poznamky-pro-programatory.md>
- Session 2 record: <https://github.com/codetogodmode/study-book/blob/main/sessions/session-02-git-variables-input-record.md>
- Handbook AI Policy: <https://github.com/codetogodmode/handbook/blob/main/ai-policy.md>

## Další session

Session 4 — středa 22. 4. 2026, 20:00. **Cykly:**
- `while` cyklus — aby kalkulačka běžela dokola, dokud uživatel neřekne stop
- `for` cyklus — pro přesný počet opakování (dekorativní `====KALKULAČKA====`)
- Úvod do **metod** — začátek úklidu bordelu v Main
