# Session 1 — Terminál, Git clone, Hello World

**Datum:** 12. 4. 2026
**Přítomni:** Martin, Matěj (asistent), Terka, Petr, Petra, Hanka
**Nepřítomni:** Michael, Ondra
**Layer:** 1 (Console & Git)
**AI režim:** EXPLAIN only

## Co se probíralo

Session 1 začala organizačně — Martin oznámil dropout Lenky a Beky, vysvětlil proč Michael a Ondra dnes nejsou (Michael byl na cestě z Brna, Ondra se neozval). Pokračoval vysvětlením struktury Layer 1: dva paralelní projekty per member — Calculator psaný společně na sessions a osobní projekt offline mezi sessions podle kanban ticketu. Martin postupně představil osobní projekty všem přítomným — Terka PandaNursery, Petra Steam library (GameLibrary), Petr GoalTracker, Michael PlaylistManager (nepřítomen), Ondra WorkoutTracker (nepřítomen), Hanka HikingLog.

Následoval praktický setup: vytvoření pracovní složky, orientace v terminálu, klonování member repa z GitHubu. Většina členů řešila autentizaci — na Macu Xcode select, u některých HTTPS password login failed a přešli na VS Code git clone UI. Po naklonování otevření solution ve VS Code (`code .`), prozkoumání Solution Exploreru s oběma projekty, a první Hello World v Calculatoru. Martin vysvětlil entry point (`static void Main`), středník jako ukončení příkazu, `Console.WriteLine` pro výpis a `Console.ReadKey` aby se aplikace nezavřela okamžitě.

Následovalo spuštění aplikace přes `dotnet run --project src/Calculator` — Martin vysvětlil rozdíl mezi spuštěním v terminálu (pre-kompilovaný strojový kód, rychlejší) a v VS Code (debug mode se zachovaným zdrojovým kódem pro pozdější debugging v L1 S5). Petr se zeptal proč je VS Code Run pomalejší a dostal vysvětlení kompilace.

Teorii Gitu Martin vysvětlil až později — co je verzování, commit jako checkpoint, push/pull/clone jako prostředky pro sdílení kódu přes GitHub. Poté přešel na GitHub Projects — ukázal kanban, Calculator project s pre-připravenými S1-S7 tikety, a live přesunul S1 ticket z Backlog přes In Progress do Done během toho co implementoval `Console.WriteLine("2 + 2 = 4")`.

Závěr: pointer na studybook materiály, úkol pro offline práci (upravit uvítací zprávu v personal projektu), bonus challenge (vícebarevný výpis v konzoli). Domluveno že S2 bude ve středu s proměnnými a datovými typy.

## Klíčové koncepty

### Terminál / konzole / command line
Martin vysvětlil že terminal, konzole a command line je v podstatě totéž. Na Macu doporučeno používat iTerm2 místo default Terminal.app. Základní příkazy: `pwd`, `ls`, `cd`, `mkdir`.

### Git clone a verzování
Git jako verzovací nástroj — vytváří checkpointy (commity) aby se dalo vrátit v čase. `git clone` stahuje repo z GitHubu, `git commit` dělá lokální checkpoint, `git push` posílá na GitHub, `git pull` stahuje cizí změny. Autentizace se řeší buď HTTPS + password (někomu nefungoval) nebo přes VS Code Source Control UI (funguje spolehlivěji, Petr to doporučil).

### Entry point C# aplikace
`static void Main(string[] args)` je místo kde .NET začíná spouštět kód. Kód uvnitř se spouští řádek po řádku, každý příkaz končí středníkem. Středník ukončuje každý příkaz, ne nutně každý řádek. Složené závorky `{}` označují blok kódu.

### Console.WriteLine a Console.ReadKey
`Console.WriteLine("text")` napíše text do konzole a odřádkuje. `Console.ReadKey()` počká na stisk klávesy než pokračuje — používáme aby se aplikace nezavřela hned po startu (nebude potřeba až v S2 kdy přidáme smysluplný vstup). Text se vždycky dává do uvozovek.

### dotnet run s projektem
`dotnet run --project src/Calculator` — specifikuje konkrétní projekt který má být spuštěn. Důležité pro member repos kde jsou dva projekty. Alternativa: VS Code Run button, ale ten běží v debug módu a je pomalejší.

### Debug vs production run
Terminal run = pre-kompilovaný strojový kód, rychlý. VS Code run = debug mode se zachovaným zdrojovým kódem pro pozdější debugging (pattern pro L1 S5 když se naučíme breakpoints).

### Case sensitivity
C# je case-sensitive — `Console` a `console` jsou dvě různé věci. Petra se explicitně zeptala a Martin potvrdil že na velká/malá písmena záleží.

### Komentáře
Řádky začínající `//` jsou komentáře — program je ignoruje, jsou pro čtenáře kódu. Studybook materiály o entry pointu obsahují komentáře jako vysvětlení.

## Diskuse a otázky

- **Petr** se ptal: "Vlastně tímhle propojením všechno co napíšu do té složky se mi rovnou ukládá na Git?" → Martin: "Ještě ne, vysvětlím teorii Gitu. Commity vytváříš manuálně, protože nechceš automatický snapshot v půli rozepsané práce."
- **Petr** se ptal: "Když to pustím v terminálu, proč je to rychlejší než když to pustím ve VS?" → Martin: "V terminálu se pouští jen pre-kompilovaný strojový kód. Ve VS Code to běží v debug módu se zachovaným zdrojovým kódem pro debugging, k tomu se dostaneme v S5."
- **Petr** se ptal: "Checkpointy vytvářím manuálně?" → Martin: "Ano, manuálně. Kdyby se dělaly automaticky, mohl bys mít checkpoint uprostřed rozepsané práce kdy aplikace nefunguje."
- **Petra** se ptala: "Je důležitý dávat pozor na velký/malý písmena?" → Martin: "Jo, to je mega důležitý. Case sensitivity. V programování je všechno case-sensitive."
- **Petr** se ptal: "A ten osobní projekt taky normálně píšeme jako do konzole?" → Martin: "V Layer 1 a 2 ano, konzolové aplikace. Layer 3 přechází na webové aplikace. Konzoli používáme protože je tam minimální setup."
- **Terka** se ptala: "Jsou to věci, které se zapamatuju v průběhu?" (o terminálových příkazech) → Martin: "Jo, vžere se to do svalové paměti. Používám dokola jen 12-20 příkazů. Kdykoli si je můžeš najít v studybooku nebo se zeptat AI."

## Kód a ukázky

Finální stav `src/Calculator/Program.cs` po session:

```csharp
namespace Calculator;

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("2 + 2 = 4");
        Console.ReadKey();
    }
}
```

Spuštění:
```bash
cd member-{name}
dotnet run --project src/Calculator
```

Výstup:
```
2 + 2 = 4
```
Program počká na klávesu, po stisku skončí.

## Odkazy

- Study-book Layer 1: https://github.com/codetogodmode/study-book/tree/main/layer-01
- Terminál a příkazový řádek: https://github.com/codetogodmode/study-book/blob/main/layer-01/terminal-prikazovy-radek-okno-do-sveta-vyvojare.md
- Terminál a VS Code jako základní nástroje: https://github.com/codetogodmode/study-book/blob/main/layer-01/terminal-a-vs-code-zakladni-nastroje-vyvojare.md
- Entry point aplikace (kde program začíná): https://github.com/codetogodmode/study-book/blob/main/layer-01/entry-point-aplikace-kde-program-zacina.md
- Git — systém pro sledování změn v kódu: https://github.com/codetogodmode/study-book/blob/main/layer-01/git-system-pro-sledovani-zmen-v-kodu.md
- Založení repozitáře s template a spuštění první aplikace: https://github.com/codetogodmode/study-book/blob/main/layer-01/zalozeni-repozitare-s-template-a-spusteni-prvni-aplikace.md
- Vícebarevný výpis v konzolové aplikaci: https://github.com/codetogodmode/study-book/blob/main/layer-01/vicebarevny-vypis-v-konzolove-aplikaci.md
- Setup Guide: https://github.com/codetogodmode/handbook/blob/main/setup-guide.md
- GitHub Guide: https://github.com/codetogodmode/handbook/blob/main/github-guide.md
- Demo Calculator repo: https://github.com/codetogodmode/demo-calculator

## Další session

Session 2 — středa 15. 4. 2026 ve 20:00. Proměnné a datové typy, čtení uživatelského vstupu (ReadLine + Parse), enum pro menu operací. Cíl: Calculator čte dvě čísla a výběr operace od uživatele. Teaser: jak aplikace pracují s operační pamětí (RAM).
