# 1:1 s Michaelem — Onboarding & Setup Test

**Datum:** 1.4.2026
**Přítomni:** Martin, Michael
**Layer:** Pre-Layer 1 (onboarding)
**AI režim:** N/A (setup, ne výuka)

## Co se probíralo

Martin udělal 1:1 onboarding call s Michaelem — ověření přístupů na GitHubu a Discordu, kompletní setup prerekvizit, a test celého flow od vytvoření sandbox repa přes klonování po spuštění aplikace.

## Klíčové koncepty

### GitHub governance
Michael sdílel obrazovku a ověřil, že vidí 6 public repos v organizaci codetogodmode, ale nevidí private repos (ops, discord-bot). Project board "Academy Ops" je viditelný, ale issues (v private ops repu) nejsou otvíratelné. Governance funguje jak bylo zamýšleno.

### Discord permissions
Postupný průchod kanály — Michael nemůže psát do #pravidla, #oznámení, #code-explain (správně read-only). Může psát do #general, #help, #repos. Bot `!ask` funguje, `/new-repo` vytvořil sandbox repo.

### Prerekvizity
- **Git:** Michael neměl nainstalovaný. Prošel codetogodmode.com (přístupový kód IDDQD), stáhl standalone 64-bit installer. Diskuse o ARM vs x64 architektuře.
- **VS Code:** Michael měl nainstalované Visual Studio 2022, ne VS Code. Musel rozlišit — "Code má modrou ikonku, je to textový editor, je to něco trošku jiného." Stáhl a nainstaloval VS Code.
- **C# Dev Kit:** Nainstalován přes VS Code Extensions (Ctrl+Shift+X). Rating 3 hvězdy — "je to nějaký smradlavý, nevadí, funguje to v pohodě."
- **.NET 10 SDK:** Stažen separátně, ověřen přes `dotnet --version`.

### Klonování a spuštění
Michael vytvořil sandbox-michael-test přes `/new-repo` na Discordu. Pak ho zkusil naklonovat — první pokus skončil v System32 (nenavigoval se do správné složky). Martin vysvětlil `cd` navigaci a doporučil vytvořit si dedikovanou složku pro projekty. Po naklonování spuštění přes `dotnet run --project App`.

Zajímavý moment: Martin nechal Michaela zeptat se bota `!ask` jak naklonovat repo — bot odpověděl správně a Michael to zvládl. Ověření, že bot funguje jako reálný asistent.

## Diskuse a otázky

- **Michael** se ptal: "A jako desktop aplikace?" → Martin vysvětlil, že Git není desktop app ale CLI nástroj.
- **Michael** se ptal: "Takže normálně cmdčko?" → Martin potvrdil, že command line / terminál / CMD je totéž.
- **Michael** se ptal: "A kdo je mezi 64 a ARM64?" → Martin vysvětlil rozdíl architektur (ARM = Apple Silicon).
- **Michael** se ptal: "To stáhnout taky v tom nebo separátně?" (o .NET SDK) → Martin vysvětlil, že SDK je separátní instalace.
- **Michael** zmínil zájem o e-shop na hadry — chce to buildovat se svým kamarádem Blazerem. Martin vysvětlil capstone přístup: prototyp v rámci kurikula (frontend + backend + košík), pak full-scale v privátním repu.

## Kód a ukázky

Žádný kód nebyl psán — session byla čistě setup a ověření přístupů. Příkazy použité:
- `git --version` (ověření instalace)
- `dotnet --version` (ověření .NET)
- `git clone <repo-url>` (klonování sandbox repa)
- `cd src` + `dotnet run --project App` (spuštění template projektu)

## Odkazy

- Prerekvizity: https://codetogodmode.com
- GitHub Guide: https://github.com/codetogodmode/handbook/blob/main/github-guide.md
- Setup Guide: https://github.com/codetogodmode/handbook/blob/main/setup-guide.md
- Michaelův sandbox: https://github.com/codetogodmode/sandbox-michael-test

## Další session

Session 0 (intro) — společná session celé skupiny. Představení CTGM, zjištění zájmů, pravidla, live demo (5 AI režimů na message board appce), prereqs check.
