# Session 0 — Intro

**Datum:** 8. 4. 2026
**Přítomni:** Martin, Matěj, Tereza, Rebeka, Michael, Petr, Petra, Ondra, Lenka, Hanka
**Layer:** Pre-Layer 1 (intro)
**AI režim:** Žádný

## Co se probíralo

Session 0 byla úvodní session celé akademie Code to God Mode. Martin představil filosofii projektu, formát dev teamu (ne kurz, ne bootcamp — vývojářský tým), 5 layers kurikula od konzole po deploy, a AI gate systém s 5 režimy (EXPLAIN → GOD MODE). Následovalo seznamovací kolečko, kde každý member představil sebe, své zájmy a případný projekt. Poté Martin provedl skupinu Discordem (kanály, pravidla, pinned messages, bot !ask) a GitHubem (handbook, study-book, setup guide). Proběhla kontrola prerekvizit — terminál, dotnet, git, VS Code s C# Dev Kit a Dark Modern theme. Na závěr Martin a Matěj předvedli své projekty jako ukázku toho, co je možné vytvořit v God Mode.

## Klíčové koncepty

### Formát dev teamu
Martin zdůraznil, že CTGM není kurz ani bootcamp. Memberové jsou součást vývojářského týmu — Martin je tech lead, Matěj je asistent, všichni ostatní jsou členové. Pracuje se s issues, code review, gates. Žádní studenti, žádní kantoři.

### 5 Layers
- **Layer 1:** Console & Git — základy C#, terminál, debugging
- **Layer 2:** OOP & Quality — třídy, testy, refactoring, sdílený projekt
- **Layer 3:** Data & API — databáze, webové API, capstone projekty startují
- **Layer 4:** Frontend — React + Tailwind, full-stack appka
- **Layer 5:** Ship It — Docker, deploy na internet

### AI gate systém
5 režimů: EXPLAIN → HELPER → PAIR → BUILDER → GOD MODE. Každý režim se odemyká individuálně přes gate challenge — ne podle kalendáře, ale podle prokázané kompetence. Gate 1-2 jsou async (PR s problémem), Gate 3-4 jsou live 1:1 drilling. Aktuálně jsou všichni v režimu EXPLAIN — používají Discord bota v #help.

### Terminál
Martin vysvětlil co je terminál / příkazový řádek / konzole — na Windows se otevře přes cmd. V tomhle prostředí poběží první aplikace v Layer 1. Matěj doplnil, že na Macu je potřeba iTerm2 místo defaultního terminálu.

### Capstone projekty
Od Layer 3 si každý bude stavět vlastní projekt podle vlastních preferencí. Některé projekty už jsou vymyšlené (Enneagram, e-shop, fitness app, diplomka), ostatní se vykrystalizují organicky v průběhu.

## Členové týmu a jejich zájmy

### Rebeka
Pracuje s Martinem, Terkou a Matějem ve firmě (provoz, finance, účetnictví). VŠE absolventka. Zero IT zkušenosti. Ráda cestuje, čte, učí se 5 jazyků. Capstone projekt zatím nemá — čeká až pochopí, co je možné.

### Michael
IT helpdesk, vystudoval IT školu. Programování mu nikdy moc nešlo, chce se přiučit. Ve volném čase tvoří hudbu a hraje fotbal. Chce vytvořit e-shop.

### Tereza
PM, project lead, product manager ve firmě s Martinem. Iniciátorka celé akademie — kontaktovala Martina s nápadem. Capstone: Enneagram osobnostní aplikace s Petrem (Petrova maminka je lektorkou Enneagramu v ČR). Miluje pandy, běh, kolo, hory.

### Petr
IT project management 10 let. Vrátil se k programování díky AI — zjistil, že mu AI dokáže opravit syntaktické chyby, přes které se dřív nedostal. Capstone: e-learningová platforma pro osobnostní rozvoj (Enneagram). Výkonný lektor osobnostního rozvoje.

### Petra
Rok po vysoké škole, pracuje na velvyslanectví (konzulární oddělení, víza). Terčina sestřenka, připojila se na poslední chvíli. Zajímá ji programování jako kariérní posun. Ráda hraje hry a cestuje. Capstone zatím nemá.

### Lenka
Projektová manažerka ve výzkumné agentuře. Martinova švagrová, připojila se na poslední chvíli. Pracuje s velkými kvantity dat v Excelu (makra). Zajímá ji, jak AI a aplikace mohou zjednodušit zpracování dat. Malý syn (3.5 roku). Capstone zatím nemá.

### Ondra
Dokončil kurz tvorby webových aplikací před měsícem, aktivně hledá práci v IT. Rád chodí do fitka, běhá, hraje poloprofesionálně fotbal. Chce vytvořit fitness appku — plány tréninků, aby nemusel 10 minut hledat co si zacvičit.

### Hanka
Chce si vytvořit aplikaci do diplomové práce. Baví ji sport, přechody hor, cestování.

### Matěj (asistent)
Martinův kamarád, prošel si intenzivním kurzem s Martinem před ~2 lety (3 měsíce, 4h spánku). Pracuje ve stejné firmě. Aktuálně nepíše kód ručně — vše přes AI, ale rozumí co kód dělá. Ukázal Bazerant (vlastní chatovací platforma bez limitů), Godot AI agent (herní engine ovládaný přes AI) a open code agent.

## Diskuse a otázky

- **Petr** se ptal: "Přes jednotlivý gejty jdeme společně nebo jako jednotlivci?" → Martin: Layery procházíte společně, ale gates jsou individuální — odemykáte je, až se na to cítíte.
- **Tereza** navrhla schedule: pondělí + středa večer. Po diskuzi domluveno **neděle + středa, 20:00**. Petr preferoval neděli, Martin souhlasil. Start: neděle 12. 4., středa 15. 4.
- **Matěj** varoval, že bez porozumění kódu se dají shodit produkční systémy — sám shodil 7 e-shopů půl hodiny po nástupu do firmy.

## Kód a ukázky

Žádný kód nebyl psán. Proběhla verifikace prerekvizit:
- `dotnet --version` → 10.0.xxx
- `git --version` → číslo verze
- VS Code: C# Dev Kit extension, Dark Modern theme (Ctrl+K, Ctrl+T)

Demo projekty (ukázka, ne výuka):
- **Martin:** Icebreaker (React + Tailwind hra, vytvořeno za ~2 týdny s AI), Broadcast (social media posting tool, ~3 dny s AI)
- **Matěj:** Bazerant (chatovací platforma bez limitů), Godot AI agent (herní engine ovládaný přes AI skilly/MCP), open code agent s custom MCP nástroji

## Odkazy

- Handbook: https://github.com/codetogodmode/handbook
- Setup Guide: https://github.com/codetogodmode/handbook/blob/main/setup-guide.md
- Study Book: https://github.com/codetogodmode/study-book
- Roadmap: https://github.com/codetogodmode/handbook/blob/main/roadmap.md
- AI Policy: https://github.com/codetogodmode/handbook/blob/main/ai-policy.md
- AI Tools Guide: https://github.com/codetogodmode/handbook/blob/main/ai-tools-guide.md

## Další session

Session 1 (Layer 1, S1) — neděle 12. 4. 2026 ve 20:00. Terminál, Hello World, první program, git clone member repa.
