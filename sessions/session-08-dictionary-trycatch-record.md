# Session 8 — Dictionary + try-catch: Layer 1 dokončen

**Datum:** Středa 13. 5. 2026, 20:00–~21:30
**Přítomni:** Martin (tech lead), Petr, Petra, Terka, Michael
**Layer:** 1 (Console & Git) — **dokončen**
**AI režim:** EXPLAIN only (po Gate 1 challenge přechod na Helper)

---

## Co se probíralo

Session měla tři velké bloky: **breakpoint recap**, **Dictionary intro + velký refaktor Calculatoru jako překládač symbolů**, **try-catch ošetření vstupů**. Plus Layer 1 closure milestone a Gate 1 invitation.

### 1. Breakpoint recap (~5 min)

**Petr** zkoušel breakpointy ve vlastním kódu během bonus tasku (submenu na historii v GoalTrackeru), ale nedostal se k breakpointu:

> *"Brainpointy jsem nastavil, debug jsem taky pustil, ale nevím, co jsem udělal, že jsem nedošel k jistému brainpointu."*

Martin: doporučení dát breakpoint **logicky před** bod, ke kterému se chceš dostat, a prokrokovat se k němu — zjistíš zároveň proč se k němu nedostal.

Petr screen sharoval problém. Martin pomohl s výběrem stack trace v debug navigaci. **Petrův dotaz:** *"Podle čeho jsi určil, že je to pětka?"* → Martin přiznal:

> *"Já jsem doufal, že se na to nebudeš ptát. Faktem mezi náma — když se mi spustí 3 vlákna, tak si je všechno klikávám a hledám."*

**Petra** breakpointy nezkoušela — je u S5/S6 práce (metody + list), nedostala se k debuggeru.

### 2. Dictionary intro přes Alza scénář (~25 min)

**Motivace:** Calculator si pamatuje historii, ale když chci vědět **kolikrát jsem sčítal**, musím procházet historii a počítat. Dictionary = mapa klíč → hodnota.

**Analogie:**
- **List** = kniha s číslovanými stránkami. První stránka má index 0, druhá index 1, ... Indexovaná seřazená kolekce.
- **Dictionary** = encyklopedie nebo kartotéka. Nehledáš podle čísla stránky, ale podle klíče (písmeno, název).

**Alza demo:** kategorie "PlayStation" → kolekce produktů. Klíč = kategorie, hodnota = produkty.

**Live demo (mimo Calculator):**
```csharp
Dictionary<string, int> pocetKrokuByJmeno = new Dictionary<string, int>();
pocetKrokuByJmeno.Add("Terka", 12000);
pocetKrokuByJmeno.Add("Petra", 10000);
pocetKrokuByJmeno.Add("Petr", 15000);
pocetKrokuByJmeno.Add("Martin", 15500);

foreach (KeyValuePair<string, int> zaznam in pocetKrokuByJmeno)
{
    Console.WriteLine($"{zaznam.Key} ušel dneska {zaznam.Value} kroků");
}
```

**Klíčové body:**
- **`<string, int>`** — typ klíče + typ hodnoty. Klíč může být cokoli (string, int, enum), hodnota taky.
- **`.Add(key, value)`** — přidá pár klíč/hodnota
- **`KeyValuePair<K,V>`** — datový typ jednoho záznamu v iteraci. `pair.Key`, `pair.Value`.
- **Implicitní typování přes `var`** — krátká zmínka, "začátečníky to může zmást."
- **Modifikace přes indexer** — `dict["Martin"] = 5000;` (přepíše existující hodnotu)

### 3. Petrův insight — Dictionary jako překládač

Po demo Petr formuloval mental model:

> *"Takže abych si to představil, to znamená, že vlastně můžu vrazit překládáč mezi uživatele a programu."*

Martin: *"Je to přesně takhle. Více méně to odpovídá i tématicky — `dictionary` jako slovník, jako překládáč."*

**Pivot session:** Martin původně plánoval Dictionary pro **statistiky operací** (kolikrát Add/Subtract/...), ale Petrův insight vedl k velkému refaktoru — **Dictionary jako překládač symbolů** (odpověď na Petrův open question z S4: jak rozpoznat `+` jako Add).

### 4. Velký refaktor Calculatoru (~30 min)

**Cíl:** Uživatel napíše příklad `"30 + 58"` v jednom řádku. Program přes `string.Split` rozdělí na 3 části, přes dictionary přeloží symbol na operaci, spočítá.

**Nový enum `UserChoice`:**
```csharp
enum UserChoice { Calculate, DisplayHistory, EndApplication, Invalid }
```

Existující enum `Operation { Add, Subtract, Multiply, Divide, Invalid }` zachován **pro překládač** (mapování symbol → operace).

**Dictionary jako překládač:**
```csharp
static Dictionary<string, Operation> CreateOperationsBySymbol()
{
    Dictionary<string, Operation> operationsBySymbol = new Dictionary<string, Operation>();
    operationsBySymbol.Add("+", Operation.Add);
    operationsBySymbol.Add("-", Operation.Subtract);
    operationsBySymbol.Add("*", Operation.Multiply);
    operationsBySymbol.Add("/", Operation.Divide);
    return operationsBySymbol;
}
```

Separation of concerns — separátní metoda na vytvoření a naplnění.

**`Menu()` vrací `UserChoice`** + nová `IsUserChoiceInputValid` paralelně k existující `IsOperationInputValid`.

**`GetExpression()` metoda:**
```csharp
static string[] GetExpression()
{
    Console.Write("Napiš příklad: ");
    string textInput = Console.ReadLine();
    return textInput.Split(" ");
}
```

**Main loop nově:**
```csharp
while (true)
{
    UserChoice choice = Menu();

    if (choice == UserChoice.Calculate)
    {
        string[] expression = GetExpression();

        if (!operationsBySymbol.ContainsKey(expression[1]))
        {
            Console.WriteLine("Zadal jsi nevalidní symbol.");
            continue;
        }

        float firstNumber = float.Parse(expression[0]);
        Operation selectedOperation = operationsBySymbol[expression[1]];
        float secondNumber = float.Parse(expression[2]);

        float result = Calculate(selectedOperation, firstNumber, secondNumber);
        // ...
    }
    else if (choice == UserChoice.DisplayHistory) { /* ... */ }
    else if (choice == UserChoice.EndApplication) break;
}
```

**Dead code odstraněn:** `ContinueApplication`, `IsOperationInputValid`, `GetNumber` — refaktorem se staly redundantní.

**Pass-by-reference closure (z S6!):** Martin při refaktoru zachoval `Calculate(Operation, float, float)` metodu beze změny:

> *"Já jsem mohl změnit to, jak tyhle data získávám, bez toho, abych musel jakýmkoliv způsobem lozit do těch metod a něco v nich upravovat. Ta metoda calculate, která počítá s těma mýma operacema, tak její chování se jako pořád nemění. A to je, Petře, odpověď na to, proč jsem zachoval enum operation."*

Petr: *"I chápu."*

**Test refaktoru přes debugger:** Martin nastavil breakpoint v Menu, krokoval přes celý nový workflow:
- Menu → choice = Calculate ✓
- GetExpression → input "30 + 58" → expression = ["30", "+", "58"] ✓
- Dictionary lookup → operationsBySymbol["+"] = Operation.Add ✓
- Parse first/second number ✓
- Calculate → výsledek 88 ✓

Martin: *"Já jsem nečekal, že se mi povede na první pokus."* Pak ručně otestoval invalid symbol (`"60 % 3"`) + DisplayHistory + EndApplication.

### 5. try-catch — ošetření vstupů (~15 min)

**Bug demo:** Martin spustil refaktorovaný Calculator a zadal `"26 + prdel"`. Aplikace spadla na `float.Parse("prdel")`.

**Motivace:**
> *"Když něco spadne fatálně, znamená to, že nám to složí celou apku. V produkční aplikaci to může znamenat poškození dat v databázi, ne jen ukončení."*

**try-catch syntax:**
```csharp
try
{
    firstNumber = float.Parse(expression[0]);
    selectedOperation = operationsBySymbol[expression[1]];
    secondNumber = float.Parse(expression[2]);
}
catch (FormatException)
{
    Console.WriteLine("Chyba: to není číslo. Zkus znovu.");
    continue;
}
```

**Klíčové koncepty:**
- **`try { ... }`** — zkus tohle udělat
- **`catch (FormatException) { ... }`** — pokud se konkrétně tahle výjimka stane, neshazuj aplikaci
- **`Exception`** = globální typ, **`FormatException`** = konkrétní typ. Specific catch je dobrá praxe.
- **Defensive vs reactive:**
  - `ContainsKey(...)` před čtením = **defenzivní obrana** (předcházení výjimce)
  - `try-catch` = **reaktivní zachycení** (po faktu)
  - Oba mají svoje místo. Některé situace pokryje pouze try-catch (např. network error).

**Příklad pro pokročilejší úroveň** (Martin):
> *"Budu mít databázi a záložní databázi. V try napíšu zápis do hlavní DB. Catch full database exception → uložím do záložní. Catch network exception → nezapisuju nikam. Různé reakce na různé typy výjimek."*

### 6. Petřin a Petrův dotaz na try-catch

**Petra:**
> *"Jo, myslím, že to chápu, jenom mě trošku děsí, že se to, v kolika případech se to musí používat. Hádám, že potom je třeba i nějaká zjednodušená verze."*

Martin: *"Nemusíš odchytávat při každé příležitosti. Můžeš obalit celý kus kódu jedním try a několika catches pro různé výjimky. Detaily v OOP — můžeš mít jedno místo na servisě, kde odchytáváš všechno."*

**Petr:**
> *"Užitečné, ale teďka zrovna to většinu trošku zaskočil. To takový, že mám v podstatě hned za mainem hodit try a jenom budu do určitých částů dodávat catch?"*

Martin: *"Try a catch musí být sourozenci, na stejné úrovni. Ne, že bys měl try a o 5 řádků níž catch. Hned za try."*

Petr: *"Akorát znamená, že budu ten catch psát na konec — když dám try na začátek programu, catch dám na konec a budu tam dávat jenom pro ty konkrétní případy."* Martin: *"Víceméně to tak je."*

### 7. Layer 1 closure milestone (~5 min)

Martin explicit:

> *"Pro Mitu (Michaela), Petra a Petru, pro vás tři, kromě Terky (s Terkou bude zle ještě v pátek), jsme aktuálně dokončili Layer 1. Znáte podmínky, cykly, kolekce — list, dictionary, pole — parsování a try-catch. To je to, z čeho se skládá základní konstrukce."*

> *"Tyhle základy jsou znovu používané ve všech oblastech C-sharpu syntakticky a mentálním modelem jsou principy používané napříč všemi jazyky — Python, JavaScript, TypeScript, C++, 60 let staré C. Všude uvidíte podmínky, cykly, kolekce, odchytávání výjimek."*

### 8. Gate 1 invitation (~10 min)

> *"Gate Challenge neslouží jako závěr layeru. Slouží k tomu, abyste se mohli posunout v AI policy. Z Explain (kde se ptáte Discord bota) na Helper (kde žádáte umělou inteligenci o refactory, pojmenování boilerplate, dokumentaci)."*

> *"Konkrétně — refaktor, který jsem dnes dělal ručně, v Helper režimu by ho za mě mohla udělat AI. Doporučuji vám registraci na Claude od Anthropic — je to mazec."*

**Gate 1 format:** Konzolová appka Score Tracker s 3 bugy o rostoucí náročnosti. Najít, opravit, popsat postup v `SOLUTION.md`. Bez časového limitu, ale Martin posuzuje kvalitu popisu.

**Přihlášení:**
- **Petr:** *"Já se hlásím."* ✓ — challenge appku dostává.
- **Michael:** *"Já ještě ne, byl jsem časově vytížený. Projdu poslední dvě sessions, splním tikety, pak budu ready."*
- **Petra:** *"Já bych si asi taky dodělala ty své etikety a pak se na to pustila."* Otázka: časový limit? Martin: *"Není, klidně co nejdřív."*

### 9. S9 posun + závěr (~5 min)

Martin navrhl **posun S9 z 17.5. na neděli 24.5.**:
- 11 dní na gate, tikety, polish aplikace
- Pátek 15.5. 1:1 s Terkou + Hankou (catch-up celého layeru)
- Forza Horizon 6 vychází 15.5., Martin chce pařit přes víkend (honest disclosure)

**Reakce:**
- Petra: *"Tak to rovnou nechme na tu neděli další, prosím."* (souhlas)
- Petr: *"Už je strašně dálko."* (nevadí mu, ale preferoval by rychleji)
- Final: **neděle 24. 5., 20:00**

**S9 formát:** Každý 5-10 min představení aplikace, ostatní (a Martin) hledají bugy. Martin: *"Rejpačka."*

---

## Klíčové koncepty

- **`Dictionary<K,V>`** — mapa klíč → hodnota. Klíč může být libovolný typ.
- **`KeyValuePair<K,V>`** — datový typ jednoho záznamu při iteraci přes Dictionary.
- **`ContainsKey(klíč)`** — bool kontrola existence klíče. Defenzivní pattern.
- **`dict[klíč]`** — indexer pro čtení a zápis. Při čtení neexistujícího klíče → `KeyNotFoundException`.
- **`var` keyword** — implicitní typování. Kompilátor odvodí typ z pravé strany.
- **`string.Split(" ")`** — rozdělí string podle separátoru, vrátí pole.
- **try-catch** — `try { ... } catch (KonkrétníException) { ... }`. Catch musí být sourozenec try.
- **`FormatException`** — výjimka při parsování neplatného formátu (např. `"abc"` na int).
- **Defensive vs reactive error handling** — `ContainsKey`/podmínka = předcházení, try-catch = po faktu.
- **Specific catch** — vždy konkrétní typ výjimky, ne generický `Exception`. Umožňuje různé reakce na různé chyby.

---

## Odkazy

**Předchozí session:**
- [Session 7 — Breakpointy](./session-07-breakpointy-record.md)

**Externí:**
- Demo Calculator (s překládačem + try-catch): <https://github.com/codetogodmode/demo-calculator>

---

## Další session

**Session 9 — Layer 1 closure + showcase** (neděle 24. 5. 2026, 20:00).
- Layer 1 oficiálně uzavřen
- Každý člen 5-10 min představení své aplikace
- Peer review — všichni hledají bugy v cizím kódu
- Mezi S8 a S9 (11 dní): polish aplikací, dokončení tiketů, Gate 1 challenge (Petr přihlášený)
- Martin po ruce na DM během intersession období
