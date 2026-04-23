# Session 4 — Cykly: for, while, switch bonus, Calculator v loopu

**Datum:** 22. 4. 2026 (středa)
**Přítomni:** Martin, Terka, Petr, Petra, Michael
**Omluveni/absent:** Hanka, Ondra (passive)
**Layer:** 1 (Console & Git)
**AI režim:** EXPLAIN only
**Trvání:** ~105 min (plán byl 90, přetáhli jsme o ~15 min kvůli zápasu s negacemi)

## Co se probíralo

Session 4 dohnala cykly, které propadly z S3. Začala rekapitulací S3 úkolů — Petra přidala do svého projektu výpis pozdravu podle denní doby přes `DateTime.Now`, což vedlo k zajímavé odbočce o časových zónách a budoucím L3/L4 tématech (UTC, server vs. client side). Jako bonus Martin ukázal `switch` statement jako alternativu k řetězci `else if`, a skupina demokraticky rozhodla, že v Calculatoru zůstane `else if` (častější v reálném použití) a `switch` se uloží do study-book pro referenci. Pak následovaly oba plánované cykly — `for` pro přesný počet opakování a `while` pro Calculator v loopu. Při implementaci loop-exit ("chceš další výpočet?") se rozjela dlouhá diskuze o negacích v logických výrazech, kde se Martin sám zamotal a Terka s Petrem pomohli najít cestu ven. Metody propadly do S5 — Martin to vědomě odložil, protože session už měla přes 90 minut.

## Klíčové koncepty

### switch — alternativa k řetězci `else if`

Když máme několik `else if` pod sebou a všechny porovnávají **jedinou proměnnou přes `==`**, může se to zapsat přehledněji přes `switch`:

```csharp
switch (choice)
{
    case Operation.Add:
        result = firstNumber + secondNumber;
        break;
    case Operation.Subtract:
        result = firstNumber - secondNumber;
        break;
    case Operation.Multiply:
        result = firstNumber * secondNumber;
        break;
    case Operation.Divide:
        if (secondNumber != 0)
            result = firstNumber / secondNumber;
        else
            Console.WriteLine("Nulou se dělit nedá");
        break;
    default:
        Console.WriteLine("Neznámá operace");
        break;
}
```

Klíčové:
- `switch (proměnná)` — co porovnáváme
- `case Hodnota:` — jedna větev (odpovídá `if (proměnná == Hodnota)`)
- **`break;` na konci každého case** — povinné, jinak se pokračuje do dalšího case
- `default:` — co se stane, pokud nic nesedí (odpovídá `else`)
- **Použít když:** pouze přesné porovnávání, jediná proměnná, žádné `&&` / `||`
- **Nepoužívat když:** složené podmínky nebo porovnání s `>`, `<`, atd.

V praxi se `switch` moc nepoužívá — `if / else if` je univerzálnější. V Calculatoru zůstává `else if`.

### for cyklus — pro přesný počet opakování

```csharp
for (int i = 0; i < 30; i++)
{
    Console.Write("=");
}
```

Tři části `for` (oddělené středníky):
1. **Inicializace:** `int i = 0` — deklarace a počáteční hodnota iterační proměnné (konvenčně `i`)
2. **Podmínka:** `i < 30` — dokud platí, cyklus pokračuje
3. **Increment:** `i++` — zvýš `i` o 1 po každé iteraci (zkratka pro `i = i + 1`)

Uvnitř cyklu **čteme** hodnotu `i`, ale neměníme ji.

Použití: dekorativní linka `===`, cokoliv kde víme přesně kolikrát.

### while cyklus — dokud platí podmínka

```csharp
bool running = true;

while (running)
{
    // ... kód, který se opakuje ...
    
    Console.Write("Chceš další výpočet? (y/n): ");
    string textInput = Console.ReadLine().ToLower();
    if (textInput != "y")
    {
        running = false;
    }
}
```

Klíčové:
- `while (podmínka)` — dokud `podmínka == true`, tělo se opakuje
- Podmínka se vyhodnocuje **před každou iterací**
- Pokud podmínka nikdy nepřestane platit → **nekonečný cyklus** (Ctrl+C ho zabije)
- Existuje i `do-while` (podmínka na konci) — v praxi se moc nepoužívá

### Bug s negacemi v loop-exit

Martin se při implementaci "chceš pokračovat?" dostal do vtipné pasti:

**Špatně (vždy true):**
```csharp
if (textInput != "y" || textInput != "Y")
{
    running = false;  // toto se provede VŽDYCKY
}
```
`||` znamená "stačí aby platil jeden". Když napíšu "y", neplatí první část, ale platí druhá (`"y" != "Y"`) → podmínka splněna. Bug.

**Špatně (nikdy ne):**
```csharp
if (textInput != "y" && textInput != "Y")
```
Napíšu "n": `"n" != "y"` (true) AND `"n" != "Y"` (true) → vejdeme. Funguje! Ale čte se těžko.

**Elegantní (Petrův návrh):**
```csharp
string textInput = Console.ReadLine().ToLower();
if (textInput != "y")
{
    running = false;
}
```
`.ToLower()` převede vstup na malá písmena, pak stačí jedno porovnání. Méně mentálního úsilí.

### Debug přes Console.WriteLine

Martin ukázal **primitivní formu logování** — vkládání `Console.WriteLine("popis toho co se stalo")` do kódu, abyste viděli co program dělá. Reálný debugger přijde v S5 (breakpointy, inspekce proměnných). Ale i tenhle primitivní log se používá v produkci — na ministerstvu práce, kam Martin dodávala, aplikace takhle logují a centrální systém to sbírá.

## Diskuse a otázky

- **Petra** se ptala: "Jde, že si webová aplikace vezme čas z prohlížeče, ne ze serveru?" → Martin: Jde, ale potřebuje client-side app (React, add-on do Chromu). Backend v .NETu běží na serveru, takže `DateTime.Now` = čas serveru. Řeší se v L3/L4.
- **Petr** se ptal: "Proč tam chceš nechat `else if` a ne `switch`? Myslel jsem, že `switch` je vhodnější." → Martin: Syntakticky ano, ale `switch` se v reálném kódu používá výjimečně. `if/else` je univerzálnější a důležitější znát syntax.
- **Terka** se ptala (o switch): "Kdy používáš `switch` a kdy `else if`?" → Martin: `switch` když porovnáváš jedinou proměnnou přes `==` proti konkrétním hodnotám. `if/else` jinak — když máš `>`, `<`, `&&`, `||`, nebo víc proměnných.
- **Petr** navrhl `.ToLower()` jako řešení negace-pasti → Martin to přijal jako finální implementaci Calculatoru.
- **Terka** navrhla `&&` při opravě negací → bylo správné řešení, které Martin zpočátku odmítl kvůli vlastnímu zmatku, pak se opravil.
- **Petra** se ptala: "A nemá tam být `&&` místo `||`?" (k první chybné verzi) → Martin: Ano, dobrá intuice — to by fungovalo.

## Kód a ukázky

**Finální Calculator po S4** (v `demo-calculator` repo):
- Enum `Operation` s 4 hodnotami
- `while (running)` obalující celý výpočetní blok
- Menu výpisu + `for` cyklus pro dekorativní linku `===`
- Validace vstupu (`choiceNumber < 1 || choiceNumber > 4`)
- `else if` větve pro 4 operace (`switch` verze v study-book)
- Loop-exit přes `.ToLower()` a porovnání `textInput != "y"`
- Testováno live: násobení 12×12, sčítání 12+15, ukončení přes "n"

## Odkazy

- **Demo Calculator (aktualizovaný kód po S4):** <https://github.com/codetogodmode/demo-calculator>
- **Cykly (for a while) — study-book:** <https://github.com/codetogodmode/study-book/tree/main/layer-01>
- **Switch statement — study-book (bonus):** <https://github.com/codetogodmode/study-book/tree/main/layer-01>
- Session 3 record: <https://github.com/codetogodmode/study-book/blob/main/sessions/session-03-enum-conditions-record.md>
- Handbook AI Policy: <https://github.com/codetogodmode/handbook/blob/main/ai-policy.md>

## Další session

Session 5 — neděle 26. 4. 2026, 20:00. **Metody + začátek kolekcí:**
- **Metody** — rozdělení dlouhého `Main` na logické celky. `static float Add(float a, float b) { ... }`, volání, parametry, návratové hodnoty.
- **Úvod do `List<T>`** (pokud stihneme) — historie výpočtů jako kolekce. `foreach` cyklus pro průchod kolekcí.
- **Debugger teaser** — breakpointy a inspekce proměnných (plně v S6).
