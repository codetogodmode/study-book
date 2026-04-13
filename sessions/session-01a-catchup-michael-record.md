# 1:1 s Michaelem — Session 1 catch-up

**Datum:** 13. 4. 2026
**Přítomni:** Martin, Michael
**Layer:** 1 (Console & Git)
**AI režim:** EXPLAIN only

## Co se probíralo

Michael nestíhal Session 1 (12. 4.), proto proběhl 1:1 catch-up den poté. Martin provedl Michaela přesně tím samým obsahem co skupina na S1 — struktura member repa s dvěma projekty, git clone, otevření ve VS Code, první Hello World v Calculatoru, spuštění programu, přečtení README personal projektu, a kanban workflow.

Michael je IT helpdesk s programátorským vzděláním ze školy, takže konceptuálně věci chytal rychle. Ptal se na konkrétní detaily (F5 shortcut, commit/push graph na GitHub profilu), ale celou setup fázi prošel bez technických problémů. Na konci measurable úspěch: PlaylistManager lokálně spuštěný, kanban ticket připraven v To-Do sloupci pro offline práci.

## Klíčové koncepty

### Struktura member repa
Martin vysvětlil že Michaelovo `member-michael` repo obsahuje dva projekty: `Calculator` (sdílený, píšeme na sessions) a `PlaylistManager` (osobní projekt Michaela, offline práce). Oba v `src/` složce, otevíratelné přes jeden solution ve VS Code.

### Git clone workflow
- Otevřít GitHub → svůj repo → zelené tlačítko **Code** → kopírovat HTTPS URL
- V terminálu ve zvolené složce: `git clone <url> member-michael` (explicitní cíl = vlastní složka)
- `cd member-michael` → přesun do nově klonované složky
- `code .` → otevře aktuální složku ve VS Code

### Calculator live demo
Otevřít `src/Calculator/Program.cs` a přepsat template Hello World na `Console.WriteLine("2 + 2 = 4")`. Spuštění dvěma způsoby:
1. **Run tlačítko** (▶ vpravo nahoře v editoru)
2. **Terminal:** `dotnet run --project src/Calculator` — specifikuje konkrétní projekt kvůli tomu, že repo má dva

### Personal projekt
`src/PlaylistManager/` je Michaelův osobní projekt. README.md v té složce popisuje co bude aplikace dělat (správa playlistu, přehrávání skladeb, historie). Michael ho má otevírat přes `Ctrl+Shift+V` ve VS Code pro formátovaný preview.

### Kanban workflow (GitHub Projects)
- Projects tab → jeho PlaylistManager board
- View → Board (místo Table)
- Sloupce: **Backlog** → **Todo** → **In Progress** → **Done**
- Drag & drop ticketu mezi sloupci
- Focus na tickety v **Todo** (nikoli Backlog) mezi sessions

### GitHub contribution graph
Michael se ptal na activity indicator na GitHub profilu. Martin ukázal svůj profil jako příklad — barevné čtverečky reprezentují aktivitu (commity, PRs, issues, reviews) za den. Čím aktivnější, tím sytější barva. Motivační prvek pro sledování vlastního pokroku.

## Diskuse a otázky

- **Michael** se ptal: "Složku v GitHubu, nebo na ploše?" → Martin: "Na ploše. Pracovní složka pro všechny tvoje projekty lokálně."
- **Michael** se ptal: "F5 nefunguje, jo?" (o klasické debug zkratce ve VS Code) → Martin: "Funguje i F5, i Run tlačítko, i `dotnet run` v terminálu. Výběr je na tobě."
- **Michael** se ptal: "Commit a push — to bylo možná v nějakém pozdějším session?" → Martin: "Ano, commit a push budeme probírat ve středu na S2."
- **Michael** se ptal: "Co znamenají ty barevné čtverečky aktivity na profilu?" → Martin: "Contribution graph — ukazuje kolik jsi toho na GitHub udělal každý den. Commit, PR, issue, code review — všechno se počítá."

## Kód a ukázky

Finální stav `src/Calculator/Program.cs` po 1:1:

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
cd member-michael
dotnet run --project src/Calculator
```

PlaylistManager projekt byl otevřen a README.md přečten — implementace uvítací zprávy zůstává jako offline task.

## Odkazy

- Study-book Layer 1: https://github.com/codetogodmode/study-book/tree/main/layer-01
- Terminál a příkazový řádek: https://github.com/codetogodmode/study-book/blob/main/layer-01/terminal-prikazovy-radek-okno-do-sveta-vyvojare.md
- Entry point aplikace: https://github.com/codetogodmode/study-book/blob/main/layer-01/entry-point-aplikace-kde-program-zacina.md
- Git — systém pro sledování změn v kódu: https://github.com/codetogodmode/study-book/blob/main/layer-01/git-system-pro-sledovani-zmen-v-kodu.md
- Založení repozitáře s template a spuštění první aplikace: https://github.com/codetogodmode/study-book/blob/main/layer-01/zalozeni-repozitare-s-template-a-spusteni-prvni-aplikace.md
- Session 1 group record: https://github.com/codetogodmode/study-book/blob/main/sessions/session-01-terminal-hello-world-record.md
- Demo Calculator repo: https://github.com/codetogodmode/demo-calculator

## Další session

Session 2 — středa 15. 4. 2026 ve 20:00. Proměnné a datové typy, čtení uživatelského vstupu (ReadLine + Parse), enum pro menu operací. První commit a push na GitHub. Teaser: jak aplikace pracují s operační pamětí (RAM).
