# Session 7 — Recap kolekcí + breakpointy

**Datum:** Neděle 10. 5. 2026, 20:00–~21:30
**Přítomni:** Martin (tech lead), Petr, Petra. Terka chyběla live (vezme záznam).
**Layer:** 1 (Console & Git)
**AI režim:** EXPLAIN only

---

## Co se probíralo

Session se na začátku zásadně přeplánovala. Původní plán byl debugger + Dictionary + try-catch. Petr ale otevřel slovy *"chtěl bych projet kolekce znova — vím co kolekce jsou, ale nevím v který části kódu ji mám vyvolat a do kterých ji mám vůbec zapsat"*, Petra přiznala *"přirozeně nestíhám, jsem zatím na pátém úkolu"* a zmínila že její DateTime greeting "funguje, ale nechápe proč". Vzhledem k tomu, že byli ve třech a oba měli konkrétní problém, Martin přeřadil:

> *"Vzhledem k tomu, že jsme jenom ve třech a vy oba dva přišli s tím, že máte nějaký problém, dnes primární fokus bude na to, co řešíte vy dva. Potom případně bych vám ukázal breakpointy a zbytek (Dictionary, try-catch) bychom defernuli do další session. Tím pádem layer 1 nebude končit na session 7, ale na session 9."*

### 1. Filozofický odbočení — programátorské myšlení a tempo

Než Martin začal s recap, sdílel vlastní zkušenost:

> *"Programátoři obecně uvažují jinak než normální lidi. Syntaxi pamatovat je nejméně důležité, principy nejvíc. Ale ty principy si nejlépe zapamatuješ tím, že pořád něco píšeš. Ve chvíli kdy přestaneš, do tvého uvažování začne zase zasahovat selský rozum — a ten je obrovský nepřítel programátorů. Když jsem psal velké enterprise systémy a měsíc je nedělal, měl jsem obrovský problém se do toho dostat zpátky. Je to podobný jako s kytarou — když týden nehraješ, nedáš dohromady akord. Svalová paměť."*

Skupina souhlasila vrátit se k **2× týdně tempu**.

### 2. Recap kolekcí — sumu Excelovou (~25 min)

Martin postavil čisté mini-demo:

```csharp
List<int> cisla = new List<int>();
bool running = true;

while (running)
{
    string textInput = Console.ReadLine();
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
foreach (int cislo_zaznam in cisla)
{
    suma = suma + cislo_zaznam;
}

Console.WriteLine($"Výsledek sumy: {suma}");
```

**Klíčové body:**
- **Konstruktor:** `new List<int>()` volá konstruktor — krátká zmínka, "vrátíme se v OOP".
- **`Add` na kolekci**, ne sčítání čísla na číslo. Petr to potvrdil — pochopil rozdíl.
- **Iterační proměná `cislo_zaznam`** — Petra se ptala "vadí, že to int předem nezmiňujeme?" → Martin: stejně jako u `int i = 0` ve `for` cyklu, iterační proměnná se deklaruje při použití. Lze pojmenovat libovolně, nemusí být `cislo` (kolize).

### 3. Bonus: `string.Split` + vnořený foreach (~15 min)

Petr otázka: *"Můžu uložit víc hodnot v jednom záznamu?"* — vedlo k Petrově původnímu tématu z S6 (jak parsovat víc čísel z jednoho readline) přes `string.Split`.

```csharp
while (true)
{
    string textInput = Console.ReadLine();
    if (textInput == "k") break;

    string[] textoveCislaVRadku = textInput.Split(" ");

    foreach (string textoveCislo in textoveCislaVRadku)
    {
        cisla.Add(int.Parse(textoveCislo));
    }
}
```

**Klíčové body:**
- **`while (true) + break`** alternativa pro `bool running` — Martin: *"Petře, dokážeš vysvětlit co se stane?"* → Petr: *"když narazí na podmínku text rovná k, vyvolá break, ukončí cyklus."*
- **Vnořený cyklus** — vnější iterace přes řádky, vnitřní přes čísla v řádku
- **Optimalizace:** lze `cisla.Add(int.Parse(textoveCislo))` napřímo, bez mezilehlé proměné `cislo`

### 4. List metody bokem — `Clear`, `Remove`, filtr přes 2 kolekce (~10 min)

- **`Clear()`** — vyčistí všechny záznamy. **Není to samé jako nová kolekce** — pořád operuje na stejném bloku v paměti (foreshadow reference vs value).
- **`Remove(0)`** — odebere první výskyt hodnoty 0.
- **Filtr přes 2 kolekce:** Petr otázka jak vyfiltrovat věty obsahující slovo. Martin ukázal pattern `staré_věty + nové_věty`, foreach + `if (!věta.Contains("prdel"))` → `nové_věty.Add(věta)`.

### 5. Bonus: Lambda / LINQ teaser (~5 min)

Martin pak ukázal jak by se to napsalo jedním řádkem:

```csharp
staré_věty = staré_věty.Except(staré_věty.Where(x => x.Contains("prdel"))).ToList();
```

> *"To je anonymní funkce / lambda. Dostanete se k tomu v L3 u databází. Když jdeš na Alzu a chceš jen ledničky, voláš podobný výraz proti databázi. Pro teď stačí vědět, že to existuje."*

Petra: *"Dává to smysl, ale že bychom to sami vymysleli někdy."* — zdravá reakce na intentional overshoot.

### 6. Petřin DateTime greeting fix (~10 min)

Petra sdílela obrazovku. Problém: `static string GetTimeBasedGreeting()` má `return $"Dobré ranko..."`, ale v `Main` ji volá jen jako `GetTimeBasedGreeting();` (bez přiřazení do proměné). Workaround: dala dovnitř metody `Console.WriteLine` + `return`, "fungovalo to" ale je to antipattern.

Martin **sokratický walkthrough**:

> *"Kdybys do proměné `cislo` chtěla přiřadit nula, jak to uděláš?"* → Petra: `int cislo = 0`.
> *"Kdybys do proměné `greeting` chtěla přiřadit výsledek metody `GetTimeBasedGreeting`, jak to uděláš?"* → Petra: `string greeting = GetTimeBasedGreeting();`

Pak `Console.WriteLine(greeting);`. Pak zjednodušení na jeden řádek `Console.WriteLine(GetTimeBasedGreeting());`.

Petra: *"Tak to dává smysl. Jo, jo, chápu. Děkuju."*

Martin: *"Tohle je vrstvení metod — voláš metodu z metody z metody."*

### 7. Breakpointy (~25 min)

Martin udělal **úmyslný bug** v `Multiply` (vrací `a + b` místo `a * b`). Demo: `20 * 6 = 26`.

**Krok za krokem:**
1. **Klik vedle čísla řádku** → červená tečka = breakpoint
2. **Spustit v Debug režimu** — drop-down vedle Run → "Debug Project"
3. **Call stack** — vybrat správné vlákno (`C# Calculator`), aplikace běží v několika vláknech
4. Aplikace běží do breakpointu, zastaví
5. **Hover na proměnnou** ukáže aktuální hodnotu
6. **Step over (klávesa nahoře)** — další řádek v aktuální metodě
7. **Step into (šipka dolů)** — vstoupit do volané metody (debugger jde dovnitř `Calculate`, pak dovnitř `Multiply`, najde tam `+` místo `*`)
8. **Continue** — pokračovat do dalšího breakpointu nebo konce
9. **Stop (červené tlačítko)** — ukončit debug

Po opravě bug + rebuild (kompilace) → `50 * 90 = 4500`, OK.

**Druhý scénář — breakpoint v cyklu:**
- Breakpoint dovnitř `foreach` v `DisplayHistory`
- Při zobrazení historie se zastaví **pro každou jednu iteraci** — vidět aktuální `record` proměnnou
- Continue (F5 nebo play tlačítko) přeskočí k další iteraci

**Třetí scénář — dělení nulou jako user bug report:**
- Calculator umožní dělení 0 → `Infinity`
- "Uživatel pošle screenshot, vy nevíte odkud" → breakpoint před `Calculate`, krokovat dovnitř `Divide`, vidět `b == 0`, implementovat ochranu

**Locals panel** — kromě hover je tu levý postranní panel se všemi lokálními proměnnými automaticky vypsanými.

**Petr otázka:** *"Můžu se vrátit zpátky v čase v debuggeru?"* → Martin: *"Ne. Ono už se to stalo."*

**Martinova teoretická poznámka — proč rebuild:**
> *"C# je kompilovaný jazyk. Když opravím kód za běhu, ta aktuálně běžící verze je z předchozí kompilace. Musím stopnout, rebuild (rekompilovat) a pustit znova. Javascript a Python jsou interpretované, tam by to zafungovalo i bez rebuild."*

Pas Martin link na Petřin problém: *"Kdyby si Petro znala breakpointy, mohla bys breakpointem zjistit kde tvoje hodnota nikam nedoletí."*

### 8. Plán S8 a S9

- **Středa 13. 5., 20:00** — **Session 8: Dictionary + try-catch**
- **Neděle 17. 5., 20:00** — **Session 9: Layer 1 closure + showcase**
  - Každý představí svou aplikaci ostatním
  - Peer review — ostatní hledají bugy v jejich kódu
  - Cíl: dotáhnout své aplikace mezi S8 a S9
- **Petr během session** našel vlastní bug v `termination` logice (při startu aplikace ihned ukončit nešlo, museli projít cíl) — *"Hele, mezi časem jsem to upravil."*

---

## Klíčové koncepty

- **`List<T>`** — dynamická kolekce, `Add`, `Count`, `Clear`, `Remove(hodnota)`
- **`foreach`** — iterace přes kolekci, iterační proměná typu obsahu, nesmí kolidovat s existujícími proměnými
- **`string.Split(" ")`** — rozdělí string podle separátoru, vrátí pole stringů
- **Vnořený cyklus** — pro 2D data (řádky × čísla v řádku)
- **`while (true) + break`** — nekonečný cyklus s explicitním ukončením přes break
- **Filtr přes 2 kolekce** — staré + nové, foreach + if + Add do nové
- **Lambda / LINQ** — `.Where(x => x.Contains(...))` jako anonymní funkce, kratší alternativa k cyklu+if. Detaily Layer 3.
- **Vrstvení metod** — `Console.WriteLine(GetTimeBasedGreeting())` — výsledek metody jako parametr jiné metody
- **Breakpoint** — pauza aplikace na konkrétním řádku v debug režimu
- **Step over / Step into** — krokování po řádku nebo dovnitř volané metody
- **Locals panel** — automatický výpis všech lokálních proměných v aktuálním scope
- **Kompilace vs interpretace** — C# je kompilovaný (rebuild po změně), JavaScript/Python interpretované

---

## Odkazy

**Předchozí session:**
- [Session 6 — Kolekce](./session-06-collections-record.md)

**Externí:**
- Demo Calculator (s historií, debugovaný): <https://github.com/codetogodmode/demo-calculator>

---

## Další session

**Session 8 — Dictionary + try-catch** (středa 13. 5. 2026, 20:00).
- `Dictionary<K,V>` pro statistiky operací (kolikrát Add, Subtract, ...)
- `try-catch` jako safety net proti pádu aplikace (např. `int.Parse("abc")`)

**Session 9 — Layer 1 closure + showcase** (neděle 17. 5. 2026, 20:00).
- Každý představí svou aplikaci
- Peer review — hledání bugů v cizím kódu
- Mezi S8 a S9: vypimpovat své aplikace
