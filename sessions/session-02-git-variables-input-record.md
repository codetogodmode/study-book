# Session 2 — Git workflow, proměnné, uživatelský vstup

**Datum:** 15. 4. 2026
**Přítomni:** Martin, Petr, Terka, Petra, Hanka, Michael (příchod ~53. min)
**Nepřítomni:** Ondra, Matěj
**Layer:** 1 (Console & Git)
**AI režim:** EXPLAIN only

## Co se probíralo

Session 2 začala Editee story jako motivačním úvodem — Martin převyprávěl víkendovou aktivitu s Matějem, kdy se účastnili prodejního webináře na appku Editee ("nejpoužívanější česká AI aplikace pro tvorbu marketingového obsahu"). Výstup: reverse-engineering ukázal, že Editee je wrapper nad Google Gemini / ChatGPT / Grok přes API s přibližně 95% marží. Martin zarámoval pointu: "technická hloubka a vhled do toho, jak tyhle věci fungujou, je aktuálně ekvivalent bullshit detektoru." Terka do toho přinesla vlastní zkušenost se Škoda Auto (osekaná interní verze LLM, kvůli bezpečnosti a úniku informací). Diskuze pak přešla na to, jak wrappery fungují přes systémové prompty, jak je to vidět i u Jarvise v CTGM Discordu, a jak i Edu v Sarchitu funguje na stejném principu.

Po motivační části Martin rychle prošel, jak se kdo popasoval s offline bonusem z S1 (vícebarevný výpis). Petra měla problém se syntaktickými chybičkami (chybějící závorka, středníky), Petr hlásil že Hello World task dotáhl ještě před S1, Terka pracovala na barvičkách live ale narazila na nespolehlivé chování `Console.BackgroundColor` (stejný problém co řešil Michael i Petra offline — Martin to označil jako "občas halucinuje, nemám dobré vysvětlení"). Terka tento problém během session zahodila s "nefunguje, můžeme jít dál."

Hlavní blok byl **git commit/push/pull prakticky**. Martin předvedl terminálový flow na svém `member-martin` s barevnou verzí Calculatoru, kterou měl připravenou: `git status` (červené modified), `git add src/Calculator/Program.cs`, `git status` znovu (zelené staged), `git commit -m "Add colorful welcome screen to calculator"`, `git log --oneline`, `git push`. Na GitHubu ukázal, jak commit dorazil a jak se zbarvila ikona contribution grafu. Členové paralelně commitovali a pushovali svoji offline práci ze S1 (barvičky) do svých member repos. **Autor identity unknown** prompt zastavil Hanku, Petra i Petru — **Petr dal přes Discord chat do `#general` kanálu příkazy `git config --global user.email` a `git config --global user.name`**, a Martin pak postupně každého proháněl setupem (Terka se trápila s uvozovkami v terminálu, Martin jí nakonec pomohl restartem terminálu a správným syntaxem).

Po commit/push přešel na **pull demo**: "vezmu Terku jako oběť." Na svém stroji nový terminál, `cd` pryč z demo-calculator, `git clone <URL> member-terka`, otevřel ve VS Code, upravil `src/PandaNursery/Program.cs` (změnil růžovou na zelenou, přidal pár řádků s pandami), `git add`, `git commit -m "refactor barev"`, `git push`. Pak vyzval Terku: "teď ty, `git pull`." Terka měla otevřený špatný folder ve VS Code (root místo member-terka), Martin jí ukázal jak se přepnout přes `code .` v terminálu, a po pullu uviděla Martinovy změny ve svém editoru. Diskuze o rozdílu `git fetch` (jen zkontroluje) vs `git pull` (stáhne) — Martin: "fetch osobně moc nepoužívám, rovnou pullnu."

Po terminálovém git flow Martin ukázal **alternativu přes VS Code Source Control UI** — žlutě zvýrazněné modifikované soubory v Exploreru, Source Control panel (Ctrl+Shift+G), stage přes plusíčko, commit message, commit and push přes šipku u commit tlačítka. Zdůraznil: "přes klikání bude fungovat spolehlivě, ale proto jsem vás prohnal terminálem, že až budete dělat s AI, chcete rozumět, co se děje."

Druhá polovina session šla na **proměnné a datové typy**. Martin začal RAM teaserem — **Petr** korektně vysvětlil operační paměť jako rychlé úložiště, do kterého se ukládá, abychom nemuseli zapisovat na pomalý disk. Martin navázal: "proměnné jsou to, co my jako vývojáři ukládáme do té RAM." Použil analogii **dětské hry na třídění tvarů** ("čtvereček nenarvu do trojuhelníčku") pro datové typy. Prošel:
- `string` — text v uvozovkách
- `int` — celá čísla, 4 byty v RAM
- `bool` — true/false, binární analogie (jednička/nula, rozsvíceno/zhasnuto)
- `float` — desetinná čísla, 8 desetinných míst, `f` suffix
- `double` — 16 desetinných míst, dvojnásobek RAM (zmíněno, nepoužito)

Zmínil high-level vs low-level languages (C# vs C++/Assembler — v C# se nemusíš starat o velikost bajtů).

Code live na Terčině `member-terka/src/Calculator/Program.cs` (Martin používal Terčin repo pro demo, zároveň trénoval push ze svojí strany). Deklarace proměnných, přiřazení hodnot, `Console.WriteLine` s přímým předáním proměnné jako parametru, pak **string interpolace** `$"První číslo: {prvniCislo}"`. Terka se zeptala na velké/malé písmeno v názvu proměnné — Martin vysvětlil **camelCase** konvenci s obrázkem (první písmeno malé, každé další slovo velkým písmenem, bez mezer).

Iterativně rozšiřoval Calculator: změna hodnoty v proměnné (`prvniCislo = 10` bez re-deklarace), pak ukázal **typickou kaskádovitou chybu** (vypíšeš hodnotu před změnou, proto vidíš starou hodnotu — Terka do toho narazila v reálném čase).

**`Console.ReadLine` + parse** byla třetí velká část. Martin začal příkladem se jménem: `string jmenoUzivatele`, prompt "Řekni mi jméno", `Console.ReadLine()` který vrací string, přiřazení do proměnné, pozdrav přes interpolaci. Funguje.

Pak přešel na **číselný parsování** — Petra se dobře zeptala "a co kdyby mohl napsat celé i desetinné číslo?" — Martin proto zvolil `float` místo `int` pro Calculator input. Důležitý didaktický moment: `string "1" + string "1"` → `"11"` vs `int 1 + int 1` → `2`. Členové viděli na ukázce rozdíl mezi konkatenací textu a sčítáním čísel.

Převod zvládnut přes `float.Parse(textoveCislo)`. Martin zmínil, že `Parse` spadne na nevalidním vstupu — "to je očekávaná chyba, ošetříme v S5 try-catchem."

Kolem 2 hodiny session (Terka si začala všímat) se Martin rozhodl **skipnout enum** a posunout ho do S3 společně s podmínkami. Dotáhl finální Calculator stav s dvěma floaty přes ReadLine, součtem, a string interpolací výsledku.

Na závěr Martin zmínil, že do `#code-explain` kanálu nahrál nová vysvětlení (markdown, stringy, proměnné) a že Terka se nemusí bát, že něco zapomene — studybook na GitHubu to má. Petra se zeptala, kolik řádků má průměrný kód — Martin odpověděl, že v enterprise systémech to jde do milionů, ale díky metodám (S4 téma) a AI (post-L5) nikdo nepíše celou aplikaci ručně. Session oficiálně skončila, několik členů ještě pokračovalo v psaní svého Calculatoru offline.

## Klíčové koncepty

### Editee a GPT wrappery
Editee, jako většina komerčních "AI apek", je wrapper nad velkými LLM (Gemini, ChatGPT, Grok) přes jejich API. 8 "AI specialistů" = 8 různých systémových promptů. Reálné API costy vs cena za předplatné dávají 95% marži. CTGM členové budou schopni tyto systémy stavět po Layer 5 (2-6 týdnů práce) a zároveň je rozpoznat jako uživatelé. Technická hloubka = bullshit detektor.

### Git commit, push, pull
Základní git cyklus pro spolupráci v týmu:
- **`git status`** — ukáže modifikované soubory v lokálním working tree
- **`git add <file>`** nebo **`git add .`** — přesune změny do *stage* (krabice na výrobky ve Martinově továrně)
- **`git commit -m "message"`** — vytvoří lokální checkpoint s popisem změn
- **`git log --oneline`** — vypíše historii commitů v aktuálním repozitáři
- **`git push`** — pošle lokální commity na remote (GitHub)
- **`git pull`** — stáhne cizí změny z remote k sobě
- **`git fetch`** — jen zkontroluje, jestli na remote nejsou změny (bez stažení)

Každý commit potřebuje **message** (povinné přes `-m "..."`) a **autora** (nastavit přes `git config --global user.email` a `git config --global user.name` — bez toho commit neprojde).

### VS Code Source Control UI
Alternativa k terminálu: Source Control panel (Ctrl+Shift+G), žluté modifikované soubory v Exploreru, `+` pro stage, commit message pole, commit tlačítko, šipka dropdown → "commit and push". Výhoda: spolehlivější autentizace (GitHub login přes browser flow). Nevýhoda: člověk nerozumí, co se pod kapotou děje.

### Proměnné a datové typy
Proměnná = pojmenované místo v RAM s konkrétním typem. Deklarace rezervuje místo, přiřazení vloží hodnotu. Typ proměnné se po deklaraci nemění — jen hodnota.

Základní typy:
- `string` — text, v uvozovkách
- `int` — celá čísla, 4 byty, např. `5`, `-10`
- `bool` — `true` / `false` (binární)
- `float` — desetinná čísla, 8 desetinných míst, suffix `f`
- `double` — desetinná čísla, 16 desetinných míst (větší rozsah, dvojnásobek RAM)

### camelCase konvence
Jména proměnných píšeme bez mezer, první písmeno malé, každé další slovo velkým: `prvniCislo`, `jmenoUzivatele`, `textoveCislo`. Není to povinné, ale je to standard. Pascal Case (`PrvniCislo`) se používá pro třídy a metody — přijde v L2.

### String interpolace
Zápis `$"text {proměnná} další text"` vloží hodnotu proměnné do textu. `$` před uvozovkami zapíná interpolaci, složené závorky obsahují název proměnné. Alternativa `"text " + proměnná + " další"` funguje, ale je méně čitelná.

### Console.ReadLine + Parse
`Console.ReadLine()` vrací VŽDY `string` — terminál neví nic o typech. Pro číslo musíme převést (parsovat):
- `int.Parse(text)` — string → int
- `float.Parse(text)` — string → float
- `double.Parse(text)` — string → double

**Pozor:** Parse spadne (FormatException), když uživatel napíše nevalidní vstup (`"abc"` místo čísla). Ošetření try-catchem = S5 téma, pro teď členové "hrají podle pravidel."

### Rozdíl `string` a `int` při sčítání
```csharp
string a = "1";
string b = "1";
Console.WriteLine(a + b);  // vypíše "11" — konkatenace textu

int x = 1;
int y = 1;
Console.WriteLine(x + y);  // vypíše 2 — matematický součet
```

Fundamentální koncept: stejný operátor `+` dělá různé věci podle typu operandů.

## Diskuse a otázky

- **Terka** přispěla k Editee diskuzi: "Já jsem se s tím setkala ještě ve Škodovce, protože Škodovka nechce, aby to bylo napojené na jejich velký umělý inteligence, takže si to osekali a používají si prostě jenom jako svojí." → Martin: "Mít interní aplikaci napojenou oproti umělé inteligenci je možná ta lepší cesta."
- **Petra** se ptala: "Jak odliším ten add od tečky, když ta tečka mi tam dá celý program?" → Martin: "`git add .` přidá všechny změny v repu, `git add src/Calculator/Program.cs` přidá jen ten konkrétní soubor. Oboje funguje."
- **Terka** se ptala: "Co je `git commit -a`?" → Martin: "Spojí `git add` a `git commit` dohromady, respektive měl by. Ale je to celkem dobrá otázka na `!explain`, tady si úplně nejsem jistý."
- **Terka** se ptala: "Proč ten git status byl 'your branch is up to date', když se mi změnila [branch]?" → Martin: "`git status` ti říká, jestli nastaly změny od posledního commitu u tebe lokálně. Ty si žádné změny lokálně neudělala, Martinovy změny byly na GitHubu, proto jsi musela dát `git pull`."
- **Terka** se ptala: "Musím pullovat pokaždé, když přijdu do repa?" → Martin: "Jo, když pracuješ s víc lidma, tak vždycky jako první věc uděláš pull."
- **Petra** se ptala: "Mohla bych jenom poprosit ten začátek?" (git config setup) → Martin jí navedl, Petr zveřejnil příkazy v Discord chatu.
- **Petra** se ptala: "Ještě jednou prosím, co dělá ten `git log --oneline`?" → Martin: "Napíše stav commitů v aktuálním repozitáři."
- **Terka** se ptala: "Proč máš první číslo a velké 'číslo' u druhého slova?" → Martin: "To je camelCase. První písmeno malé, každé další slovo velké, bez mezer."
- **Petr** se zeptal na enum, ale ten byl mimo scope: "Já se to tady stažím pochopit sám, ale z toho, co mi za to píše, furt to nemůžu rozumout." → Martin: "Enum vysvětlím, ale potřebujeme nejdřív parsování a uživatelský vstup." (enum nakonec propadl do S3)
- **Hanka** se ptala: "A co teda znamená to parsování?" → Martin: "Parsování je převod mezi datovými typy tam, kde to je možné."
- **Petra** se ptala: "Kolik takovýhle řádku má průměrný kód?" → Martin: "Moje poslední dvě appky cca 50 tisíc řádků. V enterprise jdou do milionů. Ale většina je generovaná a díky metodám (S4) se to člení do zvládnutelných kusů. Po L5 ti to bude dělat AI."
- **Petra** se ptala: "Co kdyby uživatel mohl napsat celé i desetinné číslo?" → Martin: "V tom případě použijeme `float` — do floatu můžeš uložit celé i desetinné." (Tím se Calculator změnil z `int` na `float`-based — odlišně od plánu v S2 cardu.)
- **Terka** se zeptala o code quality: "Můžu to tady takhle nechat, nebo se mi to zasekne tím, že toho tady mám hodně?" → Martin: "Není to o výkonu, ale o bordelu. Záměrně vás ženu do toho, že váš kód bude jako nechutnej bordel. Až se dostaneme k metodám v S4, začneme to čistit."
- **Terka** retrospektivně o problému s proměnnými: "Můj mozek přemýšlí hodně ve zkratkách. Když mi řekneš, že je tam první číslo 5, tak proč vypisovat jméno proměné, proč tam nenapíšu rovnou 5, 50?" → Martin: "Programování je jiný způsob uvažování. V proměné může být cokoliv, nemusí tam být 50. Teď to máš před obličejem, ale brzy ti ty hodnoty bude definovat uživatel."
- **Petra** dala Terce metaforu: "Můžeš si říkat, že jsi v Excelu a v Excelu taky nenapíšeš to číslo, ale zvolíš buňku a dáš tam C1."

## Kód a ukázky

Finální stav `src/Calculator/Program.cs` po S2:

```csharp
namespace Calculator;

class Program
{
    static void Main(string[] args)
    {
        string textoveCislo;
        float prvniCislo = 5;
        float druheCislo = 50;
        float vysledek = 100;

        Console.WriteLine("Řekni mi první číslo a Enter");
        textoveCislo = Console.ReadLine();
        prvniCislo = float.Parse(textoveCislo);
        Console.WriteLine("Řekni mi druhé číslo a Enter");
        textoveCislo = Console.ReadLine();
        druheCislo = float.Parse(textoveCislo);
        vysledek = prvniCislo + druheCislo;
        Console.WriteLine($"První číslo: {prvniCislo} | Druhé číslo: {druheCislo} | Výsledek součtu: {vysledek}");
        Console.WriteLine();
        Console.ReadKey();
    }
}
```

Co Calculator **zatím NEumí** (přijde v S3):
- Vybrat operaci (enum, menu)
- Podmínky `if/else` pro výběr výpočtu
- Menu v cyklu ("další výpočet?")
- Odčítání, násobení, dělení

## Odkazy

- Study-book Layer 1: https://github.com/codetogodmode/study-book/tree/main/layer-01
- Git — systém pro sledování změn v kódu: https://github.com/codetogodmode/study-book/blob/main/layer-01/git-system-pro-sledovani-zmen-v-kodu.md
- Vícebarevný výpis v konzolové aplikaci: https://github.com/codetogodmode/study-book/blob/main/layer-01/vicebarevny-vypis-v-konzolove-aplikaci.md
- Session 1 record: https://github.com/codetogodmode/study-book/blob/main/sessions/session-01-terminal-hello-world-record.md
- Session 1a Michael catch-up record: https://github.com/codetogodmode/study-book/blob/main/sessions/session-01a-catchup-michael-record.md
- GitHub Guide: https://github.com/codetogodmode/handbook/blob/main/github-guide.md
- AI Policy: https://github.com/codetogodmode/handbook/blob/main/ai-policy.md
- Demo Calculator repo: https://github.com/codetogodmode/demo-calculator

## Další session

Session 3 — neděle 19. 4. 2026 ve 20:00. **Enum** (propadl z S2), podmínky `if/else` a `switch`, složené podmínky `&&` / `||` / `!`, cykly `while`. Kalkulačka konečně počítá podle vybrané operace a menu se opakuje. Git status/log/diff jako nadstavba toho, co jsme se dneska naučili. Teaser do S4: co jsou metody a proč nám pomohou uklidit bordel.
