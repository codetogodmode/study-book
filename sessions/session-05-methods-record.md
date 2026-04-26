# Session 5 — Metody: Úklid Calculatoru

**Datum:** Neděle 26. 4. 2026, 20:00–~22:00
**Přítomni:** Martin (tech lead), Hanka (live u Martina), Petra, Petr, Terka, Matěj, Michael (přišel pozdě)
**Layer:** 1 (Console & Git)
**AI režim:** EXPLAIN only

---

## Co se probíralo

Session měla jeden velký cíl: **rozdělit kalkulačku z S4 do metod**. Před refaktoringem ale Martin postavil warm-up demo se 4 izolovanými metodami, aby všichni viděli mechaniku v čistém prostředí, než ji aplikujeme na 100řádkový bordel v Main.

### 1. Rekapitulace S4

**Petr** referoval, že v S4 tiketech udělal **všechny tři varianty** úkolu místo jedné — netušil, že měl vybrat jen jednu. Zasekl se na anti-cyklové obraně: když program dosáhl maxima pokusů, pokračoval místo aby skončil. Sám přišel na to, že potřebuje `return` místo `break`. Martin to využil k vysvětlení rozdílu:

> **return ukončí metodu, break ukončí cyklus, continue přeskočí aktuální iteraci.**

### 2. Warm-up demo metod (~30 min)

Martin postavil čtyři metody postupně, v "demo zóně" Calculatoru:

**1. Bez parametrů, bez návratu:**
```csharp
static void PozdravUzivatele()
{
    Console.WriteLine("Zdravím uživatele z metody.");
}
```
Tři důležité části metody: **návratový typ** (`void`), **self-explanatory jméno**, **parametry**.

**2. S parametrem:**
```csharp
static void PozdravUzivatele(string pozdrav)
{
    Console.WriteLine(pozdrav);
}
// volání: PozdravUzivatele("Zdravím uživatele zvolání metody");
```
Petr se ptal: *"Můžu parametry definovat právě načtením z toho, co mi napíše uživatel? Jaké jsou limitace?"* → Martin: **"Žádné. Můžeš poslat cokoliv typu, který si metoda vydefinuje."**

**3. S návratovou hodnotou:**
```csharp
static int DejMiCisloKrat5(int cislo)
{
    int vysledek = cislo * 5;
    return vysledek;
}
// volání: int nasobek = DejMiCisloKrat5(20);
```
Petr potvrdil pochopení vlastními slovy: *"ten parametr jsem mu tam dal natvrdo, a to je to, co se nakrmí do toho int číslo, ta 20."*

**4. Víc parametrů a scope:**
```csharp
static int Vynasob(int nasobic, int nasobitel)
{
    int vysledek = nasobic * nasobitel;
    return vysledek;
}
```
Klíčový moment — **scope proměnných:** `int vysledek` v jedné metodě je úplně jiná proměnná než v jiné. *"Tento kód a tento kód na sebe vzájemně nevidí."*

**5. Kombinace všeho** — `VytvorPozdravSeJmenem`:
```csharp
static string VytvorPozdravSeJmenem(string jmeno)
{
    string pozdrav = $"Ahoj {jmeno}";
    return pozdrav;
}
```
Volání čte jméno z konzole, pošle do metody, tiskne výsledek.

#### Static keyword odložen
Martin vědomě nevysvětloval `static`: *"To nejlepší, co vám na to řeknu, je teď to neřešte. Všude na začátek píšte static. Vrátíme se k tomu v Layer 2 u OOP, kde bude public, private, internal."*

> **Pro hlubší vysvětlení viz [statické metody — nástroje které fungují bez objektu](../layer-01/staticke-metody-nastroje-ktere-funguji-bez-objektu.md).**

### 3. Refaktoring Calculatoru (~50 min)

Hlavní blok session. Martin extrahoval z Main 9 metod, postupně, po každé extrakci spustil aplikaci a ověřil funkčnost.

**Extrahované metody (v pořadí):**

| # | Metoda | Návratový typ | Parametry |
|---|--------|---------------|-----------|
| 1 | `WelcomeScreen()` | `void` | — |
| 2 | `Menu()` | `Operation` | — |
| 3 | `DisplayMenuOptions()` | `void` | — |
| 4 | `IsOperationInputValid(int n)` | `bool` | int |
| 5 | `GetNumber(string order)` | `float` | string |
| 6 | `Calculate(Operation op, float a, float b)` | `float` | Operation, float, float |
| 7-10 | `Add`, `Subtract`, `Multiply`, `Divide` | `float` | float, float |
| 11 | `ContinueApplication()` | `bool` | — |

#### Klíčové momenty refaktoringu

**Operation enum rozšířen o `Invalid`** — když uživatel zadá neplatné číslo, metoda `Menu` musí vrátit *něco*. Řešení:
```csharp
enum Operation { Add, Subtract, Multiply, Divide, Invalid }
```
Když user napíše blbost, vrátíme `Operation.Invalid`. (Viz [enum — pojmenované konstanty místo magic numbers](../layer-01/enum-pojmenovane-konstanty-misto-magic-numbers.md).)

**První bug po extrakci Menu:** Když Menu vrátila Invalid, program pokračoval do Calculate a počítal s nesmysly. **Petr** navrhl: *"if se to rovná invalid, tak break."* Martin opravil: **break by ukončil celý while → program skončí. My chceme znova na menu → `continue`.**

**DRY moment u GetNumber:** První a druhé číslo se získávalo dvěma stejnými bloky. Extrakce do jedné metody s parametrem `numberOrder`, volání 2× s `"první"` / `"druhé"`. **Terka** navrhla pojmenování parametru: *"Order?"* → použito.

**Single Responsibility pattern** — Martin explicitně pojmenoval princip: *"každý logický celek by měl mít svoji vlastní odpovědnost."* Menu byla moc dlouhá → rozdělil na `DisplayMenuOptions` (jen tiskne) + `IsOperationInputValid` (jen kontroluje). **Klíčové:** metoda může volat další metodu, ne jen z Mainu. (Viz [rozpoznání kdy rozdělit nebo extrahovat metodu](../layer-01/rozpoznani-kdy-rozdelit-nebo-extrahovat-metodu.md).)

**Demokratické hlasování — expression-bodied vs explicit:** Martin ukázal `IsOperationInputValid` ve dvou verzích — dlouhá s `return false` / `return true`, kratší jako `return n >= 1 && n <= 4;`.
- Terka: *"Já bych asi vrátila tu podmínku zpátky"* (dlouhá)
- Petra: *"taky tu podmínku, jenom šoupala do dvou závorek"* (dlouhá s else)
- Petr: kratší
- Matěj: *"chápu oboji, líbí se mi kratší, ale přizpůsobím se"*

**Výsledek:** dlouhá verze v Calculatoru. Kratší verze ukázána Petrovi jako bonus pro jeho personal projekt.

**Mikrométody Add/Subtract/Multiply/Divide** — Petr se ptal: *"Tohle má nějakou výhodu, nebo je to procvičení?"* Martin přiznal: *"Spíš procvičení. Ale benefit je, že když chci upravit logiku sčítání, najdu to v jednořádkové metodě, ne ve velké Calculate."*

**Petr identifikoval skutečný benefit sám:**
> *"Já bych měl pocit, že největší benefit tohohle je, že tam vlastně můžu volat kdykoliv pak v tom kódu. Že je to jako přepoužívání."*

Martin přidal **paralelu s agile:**
> *"Když ti přijde ticket na změnu, místo toho abys měnil 10 míst v aplikaci, tak z 10 míst voláš metodu, v té metodě máš logiku a změníš jenom logiku v té jedné metodě."*

(Hlubší kontext: [proč používat metody — organizace kódu pro lepší přehlednost](../layer-01/proc-pouzivat-metody-organizace-kodu-pro-lepsi-prehlednost.md).)

#### Climax: Main z ~100 řádků na ~30

```csharp
static void Main(string[] args)
{
    bool running = true;
    while (running)
    {
        WelcomeScreen();
        Operation choice = Menu();
        if (choice == Operation.Invalid) continue;

        float first = GetNumber("první");
        float second = GetNumber("druhé");
        float result = Calculate(choice, first, second);
        Console.WriteLine($"Výsledek: {result}");

        running = ContinueApplication();
    }
}
```

Plný refaktorovaný kód: <https://github.com/codetogodmode/demo-calculator>

### 4. Error Lens extension

**Terka** se ptala: *"Jak si tam dáš to, aby ti to psalo ty doporučení? Protože mi to tam nic takovýho nepíše."*

Martin: **VS Code Marketplace → Error Lens.** Doporučení všem — chyby v editoru přímo na řádku.

### 5. Posun rozvrhu

Martin navrhl **skip středy 29. 4.** a posun S6 na **neděli 3. 5. 2026**:
- Důvody: čas na vstřebání metod, prodloužený víkend (1. 5. = svátek), Martinovo daňové přiznání.
- Všichni souhlasili.

### 6. Bonus: Petřin for-cyklus bug

Po session Petra zmínila, že její for cyklus s `===` linkou nefunguje — text se nezobrazí. Martin prošel s ní podmínku:
- Měla `for (int i = 0; i > 50; i++)` — `>` místo `<`.
- Cyklus se vůbec nespustil, protože podmínka byla od začátku false.
- **Lekce:** vždycky zkontrolovat podmínku for cyklu — `<` vs `>` je klasická chyba. (Viz [cykly — jak opakovat činnosti v programu](../layer-01/cykly-jak-opakovat-cinnosti-v-programu.md).)

---

## Klíčové koncepty

- **Metoda** = pojmenovaný kus kódu se 3 částmi: návratový typ, jméno, parametry
- **`void`** = "nic nevracím". Pro metody, které jen něco dělají
- **`return`** = ukončí metodu a vrátí hodnotu (v `void` ukončí bez hodnoty)
- **Scope proměnné** — proměnná v jedné metodě nevidí na proměnnou v jiné. Stejné jméno OK, je to jiná proměnná
- **DRY (Don't Repeat Yourself)** — opakující se kód → extrahuj do metody
- **Single Responsibility** — každá metoda má jeden jasný účel
- **Reuse benefit** — metoda umožňuje měnit logiku na jednom místě, ne v 10 kopiích
- **Operation.Invalid pattern** — když nejde vrátit "nic" (metoda vyžaduje návratový typ), přidej do enumu sentinel hodnotu
- **`continue` vs `break` vs `return`:**
  - `return` → ukončí metodu
  - `break` → ukončí cyklus
  - `continue` → přeskočí aktuální iteraci, pokračuj další

---

## Odkazy

**Předchozí session:**
- [Session 4 — Cykly](./session-04-cycles-record.md)

**Study-book — metody (vygenerováno přes `!explain` po S5):**
- [Proč používat metody — organizace kódu pro lepší přehlednost](../layer-01/proc-pouzivat-metody-organizace-kodu-pro-lepsi-prehlednost.md)
- [Rozpoznání kdy rozdělit nebo extrahovat metodu](../layer-01/rozpoznani-kdy-rozdelit-nebo-extrahovat-metodu.md)
- [Statické metody — nástroje které fungují bez objektu](../layer-01/staticke-metody-nastroje-ktere-funguji-bez-objektu.md)

**Study-book — související koncepty:**
- [Entry point aplikace — kde program začíná](../layer-01/entry-point-aplikace-kde-program-zacina.md) (Main jako metoda)
- [Enum — pojmenované konstanty místo magic numbers](../layer-01/enum-pojmenovane-konstanty-misto-magic-numbers.md) (Operation.Invalid)
- [Cykly — jak opakovat činnosti v programu](../layer-01/cykly-jak-opakovat-cinnosti-v-programu.md) (continue/break)
- [Podmínky a logické operátory](../layer-01/podminky-a-logicke-operatory-rozhodovani-v-programu.md)
- [Jednoduchá kalkulačka pro začátečníky](../layer-01/jednoducha-kalkulacka-pro-zacatecniky.md)

**Externí:**
- Demo Calculator (refaktorovaný): <https://github.com/codetogodmode/demo-calculator>
- Error Lens extension: <https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens>

---

## Další session

**Session 6 — Kolekce + úvod do debuggeru** (neděle 3. 5. 2026, 20:00).
- Středa 29. 4. SKIP — týden na vstřebání + prodloužený víkend
- Téma: `List<T>`, `foreach`, případně debugger + breakpointy
