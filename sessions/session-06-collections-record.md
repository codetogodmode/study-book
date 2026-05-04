# Session 6 — Kolekce: Calculator si pamatuje historii

**Datum:** Neděle 3. 5. 2026, 20:00–~21:35
**Přítomni:** Martin (tech lead), Petr, Petra, Terka
**Layer:** 1 (Console & Git)
**AI režim:** EXPLAIN only

---

## Co se probíralo

Session měla dvě hlavní části: **kolekce** (pole, `string.Split`, `List<T>`, `foreach`) a **rozšíření Calculatoru** o historii výpočtů. Plus krátký teaser debuggeru na konec.

### 1. Rekapitulace S5 — metody

**Petr** referoval, že hlavní task (#9) má hotový — refactoring + `ClassifyProgress` + `MotivationalMessage`. **Bonus task Operation.Invalid (#10)** ho ale "strašně zasekl, nevěděl jsem co podobně chceš". Když Martin sdílel obrazovku s Petrovým kódem, ukázalo se, že **Petr to udělal po svém** — kontrolu invalid vstupu řeší **uvnitř `Menu()` metody přes `break`**, nikoli přes `continue` v Mainu. Martin to ocenil:

> *"Tady tohle ti funguje tak, jak bys potřeboval. Akorát máš tu ochranu znova v Mainu a ta už je redundantní, protože ta nikdy nebude hitnutá."*

Petr smázl redundantní kontrolu z Mainu. **Bonus splněn alternativním přístupem** — místo "vrať Invalid + continue v Mainu" zvolil "ošetři uvnitř Menu, nikdy nevrať Invalid ven".

**Petra** přiznala, že se k S5 tiketům dostala **2 hodiny před session** a má v projektu základní extrakce (menu, úvod, volby), ale vnitřek (různé podmínky pro akce) ještě ne. Také zjistila, že **S5 tikety nemá v project boardu**.

**Martin přiznal vlastní chybu:** issues vytvoření `gh issue create` se nepropsaly do project boardu — nevšiml si toho. Slíbil **zpětnou nahrávku S5 tiketů + S6 tikety** přidat do boardu po session.

**Terka** nemluvila o S5 explicitně, ale řekla:
> *"Já bych potřebovala se na to v úterý podívat... jsem trošku ztracená a ještě jestli bychom nemohli dojet ty moje úkoly."*

Martin nabídl **úterý 1:1**, Terka přijala. Petra na společné úterý nemůže (ale o ničem to nesignalizovalo).

### 2. Kolekce — pole, Split, List

Martin postavil koncept ve třech krocích: **pole → Split → List**.

#### Pole (`string[]`)

**Motivace:** "Co když uživatel chce zadávat více jmen a já dopředu nevím kolik?"

**Live demo:**
```csharp
Console.Write("Kolik jmen chceš zadávat? ");
int count = int.Parse(Console.ReadLine());

string[] jmena = new string[count];

for (int i = 0; i < count; i++)
{
    Console.Write("Zadej jméno: ");
    jmena[i] = Console.ReadLine();
}

foreach (string jmeno in jmena)
{
    Console.WriteLine($"Ahoj, {jmeno}!");
}
```

**Klíčové body:**
- **Inicializace** `new string[count]` — pole musí mít fixní velikost při vytvoření
- **Indexy od 0** — `jmena[0]` je první, `jmena[count-1]` je poslední
- **Přístup přes index** — `jmena[2]` = "třetí" prvek (protože indexy začínají od 0)
- **`foreach`** — projde celou kolekci bez nutnosti znát index

**Real world:** Alza košík — pro každý jeden produkt v košíku se vyrenderuje jeden řádek, dopředu se neví kolik produktů uživatel přidá.

#### `string.Split` — pole jako návratový typ

**Petrův open question z minulé session:** *"Jak parsujem '20 plus 50' jako jeden vstup?"*

Demo:
```csharp
Console.Write("Napiš příklad (např. 20 plus 50): ");
string textInput = Console.ReadLine();

string[] rozdeleny = textInput.Split(" ");

Console.WriteLine($"Část 0: {rozdeleny[0]}");
Console.WriteLine($"Část 1: {rozdeleny[1]}");
Console.WriteLine($"Část 2: {rozdeleny[2]}");
```

**Když uživatel napíše víc** (`"80 plus 70 minus 20 plus 30"`), pole má víc prvků. Místo natvrdo zapsaných indexů použít `foreach` — projde **všechny prvky bez ohledu na velikost**.

**Petr:** "Ale `foreach` se používá jenom u kolekcí, nebo pak ještě někde?" → **Ano, `foreach` projíždí kolekce vždycky.**

#### Multi-rozměrná pole — krátká zmínka

Martin zmínil že existují 2D, 3D pole (`string[,]`, `string[,,]`), ale **80% času pole jednorozměrné**. "Detaily ve směrových vektorech, do toho nepůjdeme."

#### `List<T>` — dynamická kolekce

**Motivace:** "Pole musí dopředu vědět velikost. Ale my nechceme říct uživateli 'zadej 5 čísel', chceme říct 'zadávej dokud chceš'."

```csharp
List<int> cisla = new List<int>();
string textInput = "";
bool running = true;

while (running)
{
    Console.Write("Zadej číslo (k = konec): ");
    textInput = Console.ReadLine();

    if (textInput == "k")
    {
        running = false;
    }
    else
    {
        int cislo = int.Parse(textInput);
        cisla.Add(cislo);
    }
}

int suma = 0;
foreach (int zapsane in cisla)
{
    Console.WriteLine($"Aktuální suma je {suma}, připočítávám {zapsane}");
    suma = suma + zapsane;
}

Console.WriteLine($"Celková suma zadaných čísel je {suma}");
```

**Klíčové body:**
- **Generic syntax** `List<int>` = "List čeho?" → typ v zobácích.
- **Inicializace přes `new`** — `List<int>` je komplexní datový typ, vyžaduje **konstruktor** (Martin to nazval, "vrátíme se k tomu v OOP").
- **`Add`** — přidá prvek na konec, nemusíš znát index.
- **`foreach`** s iterační proměnou typu obsahu (`int zapsane`).

**Mental model:** Excel SUMA — "vy nadtaháte do buněk čísla, neví se kolik, pak vyberete a Excel sečte."

### 3. Calculator dostane historii

**Cíl:** Po každém výpočtu si Calculator uloží záznam (čísla + operace + výsledek). Uživatel si přes novou volbu menu může historii zobrazit.

**Postup:**

1. **`List<string> history` před while smyčkou** — aby přežila iterace.

2. **Metoda `SaveToHistory`** — Martin ji nejdřív napsal jako `static void` s parametry, ale **Petr si všiml problému:**

   > *"Jak to z toho pak dostaneš, abych si to vypsal?"*

   Skvělý insight — Petr objevil **pass-by-value vs pass-by-reference** problém ještě před tím, než ho někdo pojmenoval. Martin krátce vysvětlil:

   > *"Existují dva typy předávání hodnot. Jedna je pass by reference, druhá je pass by value. U komplexních typů (jako List) se předává reference, ne kopie, ale je to komplikovanější věc — vrátíme se v Layer 2."*

   **Pragmatický fix:** udělat metodu která vrací updated list:

   ```csharp
   static List<string> SaveToHistory(List<string> history, float first, float second, Operation op, float result)
   {
       string record = $"{first} {op} {second} = {result}";
       history.Add(record);
       return history;
   }
   ```

3. **Metoda `DisplayHistory`** — void, foreach výpis:
   ```csharp
   static void DisplayHistory(List<string> history)
   {
       Console.WriteLine($"V historii je aktuálně {history.Count} záznamů:");
       foreach (string record in history)
       {
           Console.WriteLine(record);
       }
   }
   ```

4. **Nová operace v enumu** — `DisplayHistory` jako index 4, `Invalid` posunut na index 5:
   ```csharp
   enum Operation { Add, Subtract, Multiply, Divide, DisplayHistory, Invalid }
   ```
   Plus update `IsOperationInputValid` (validní 1-5) a `DisplayMenuOptions`.

   **Martin přiznal frikci:** *"Přidal jsem novou operaci a najednou musím být na třech různých místech, kde to musím změnit. Naštěstí jsem to měl rozdělené do metod, takže vím kam šáhnout. Tohle nám později vyřeší OOP — Open/Closed Principle."* (Předzvěst Layer 2.)

5. **V Mainu — větvení podle volby:**
   ```csharp
   if (choice == Operation.DisplayHistory)
   {
       DisplayHistory(history);
       continue;
   }
   ```

   **Petrův dotaz:** *"Proč máš `if` a ne `else if`?"*

   Martin: *"V tomto případě se to chová stejně, protože iterace končí přes `continue`. Kdybych neměl `continue`, podmínka by se vyhodnocovala individuálně každá."*

6. **Spustit, otestovat** — udělat 5 různých výpočtů, pak volba 5 (Display History) → vypíše všechny záznamy.

### 4. Real world scénáře (pro Terku)

Martin dal Terce explicit goal-first vysvětlení (Petra ho to vyžádala v polovině session), pak rozšířil scénáři:

- **Alza košík** — kolekce produktů, foreach iteruje, počet u ikony aktualizuje
- **Paginace ledniček** — Alza nenačítá 1000 ledniček do paměti, ale 24 na stránku → praktiky **pagination** a **virtualization**
- **Databáze** — tabulka je kolekce, jedna tabulka může mít 10 záznamů, jiná miliardu
- **Burndown charty** — Petr to chápe ze své PM praxe: kolekce tiketů → foreach → propočet → graf

**Petrův dotaz na velikost:** *"Jak velké kolekce se v praxi používají?"* → vedlo k diskusi o paměťové optimalizaci (`int` = 4 byty, milion intů = 4 MB), pagination, virtualization. Nad rámec L1 ale Petr unikátně schopen ten kontext absorbovat.

### 5. Pokročilé typy kolekcí (krátká zmínka)

- **Dictionary** — key-value pairs, přijde příští session
- **Linked list** — spojový seznam, prvky odkazují na sebe
- **Queue** (FIFO) — fronta na letišti
- **Stack** (FILO/LIFO) — zásobník nábojů, talířů

Martin: *"Ale to jsou kolekce v 20% věcí, které 80% času používat nebudete. Vy nejvíc budete používat List."*

### 6. Debugger — krátký teaser

Martin ukázal:
- **Breakpoint** — klik na číslo řádku, červená tečka
- **F5** spustí v Debug režimu, program zastaví na breakpointu
- **Locals panel** — vidíme aktuální hodnoty proměnných
- Pokračování → zastaví na dalším breakpointu

> *"Tohle byl jenom krátký teaser. Znova se na to podíváme příště pořádně."*

### 7. Plán a rozvrh

- **S7 — neděle 10. 5. 2026, 20:00**
- Středu 6. 5. **skip** (svátek 8.5., prodloužený víkend)
- S7 obsah: **debugger pořádně** + **Dictionary** + **Gate 1 readiness check**
- **Gate 1 formát:** asynchronní — Martin pošle appku s úmyslnými chybami, member je najde, opraví, pošle zpět s vysvětlením postupu. Po Gate 1 → Helper AI mode.

---

## Klíčové koncepty

- **Pole (`T[]`)** — fixní velikost, primitivní datový typ, indexované od 0
- **`string.Split(separator)`** — vrátí pole, rozdělí string podle separátoru
- **`List<T>`** — dynamická kolekce, používá se přes `Add`, `Count`, indexer `[i]`
- **Generic syntax `<T>`** — type parametr, "kolekce čeho?". Detaily Layer 3.
- **`new` pro komplexní typy** — volá konstruktor (vrátíme se v Layer 2 OOP)
- **`foreach`** — iteruje přes kolekci, pro každý prvek provede tělo. Bez indexů.
- **Pass-by-value vs pass-by-reference** — primitivní typy se předávají kopií, kolekce přes referenci. Detaily Layer 2.
- **Open/Closed Principle (předzvěst)** — přidání operace = update na 3 místech. OOP to vyřeší.

---

## Odkazy

**Předchozí session:**
- [Session 5 — Metody](./session-05-methods-record.md)

**Externí:**
- Demo Calculator (s historií): <https://github.com/codetogodmode/demo-calculator>

---

## Další session

**Session 7 — Debugger + Dictionary + Gate 1 prep** (neděle 10. 5. 2026, 20:00).
- Středa 6. 5. SKIP (prodloužený víkend, svátek 8.5.)
- Téma: F5/breakpointy/Locals panel pořádně, `Dictionary<K,V>` pro statistiky operací, příprava na Gate 1
- Po S7: Petr na Gate 1 challenge (asynchronní, Helper AI unlock)
