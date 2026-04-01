# Založení repozitáře s template a spuštění první aplikace

## GENERAL PRACTICE

**Repozitář** (repository/repo) je kontejner pro tvůj kód. Představ si ho jako složku s historií — ukládá nejen aktuální stav souborů, ale i všechny změny, které jsi kdy udělal.

**Template** je předpřipravená šablona projektu. Místo vytváření prázdného repozitáře dostaneš základní strukturu s potřebnými soubory.

**Console aplikace** je program, který běží v terminálu (konzoli). Píšeš do ní text, ona ti odpovídá — žádné okna s tlačítky.

## CTGM-SPECIFIC

V naší akademii používáme GitHub organizaci **codetogodmode**. Sandbox repozitáře si vytváříš přes Discord bota v kanálu #repos.

### Vytvoření repozitáře

V Discord kanálu #repos napiš:
```
/new-repo název: moje-prvni-aplikace template: console
```

Bot vytvoří `sandbox-{tvoje-jméno}-moje-prvni-aplikace` s předpřipravenou strukturou Console aplikace.

### Stažení do custom složky

Když máš repozitář, musíš ho **klonovat** (stáhnout) na svůj počítač:

```bash
git clone https://github.com/codetogodmode/sandbox-jmeno-moje-prvni-aplikace.git moje-slozka
```

Tenhle příkaz:
- Stáhne repozitář z GitHubu
- Vytvoří složku `moje-slozka` (místo dlouhého názvu repozitáře)
- Nakopíruje tam všechny soubory včetně Git historie

### Struktura Console template

Tvoje aplikace bude obsahovat:
```
moje-slozka/
├── Program.cs          # Hlavní soubor s kódem
├── MojePrvniAplikace.csproj  # Konfigurace projektu
└── .gitignore         # Co Git má ignorovat
```

### Spuštění aplikace

Otevři terminál v složce projektu a spusť:

```bash
dotnet run
```

Tenhle příkaz:
1. **Zkompiluje** tvůj C# kód do spustitelného programu
2. **Spustí** výslednou aplikace
3. Zobrazí výstup v terminálu

### Ukázka kódu z template

Základní Program.cs vypadá takto:

```csharp
Console.WriteLine("Hello, World!");
```

**Console.WriteLine()** je method (metoda), která vypíše text do terminálu. Po spuštění uvidíš:
```
Hello, World!
```

### Technické termíny

**Kompilace**: Překład tvého C# kódu do jazyka, kterému rozumí počítač. C# je "high-level" jazyk (blízký lidské řeči), počítač rozumí jen "machine code" (nuly a jedničky).

**Runtime**: Prostředí, ve kterém tvůj program běží. .NET runtime se stará o správu paměti, bezpečnost, komunikaci se systémem.

**Project file** (.csproj): XML soubor, který říká .NET toolingu, jaký typ aplikace vytváříš, jaké knihovny používáš, pro kterou verzi .NET kompilovat.

### Základní Git workflow

1. **Clone** - stáhneš repozitář: `git clone <url> <složka>`
2. **Změny** - upravíš kód v editoru
3. **Add** - označíš změny k uložení: `git add Program.cs`
4. **Commit** - uložíš změny s popisem: `git commit -m "Změnil jsem uvítací text"`
5. **Push** - pošleš změny na GitHub: `git push`

Více o Git workflow najdeš v <https://github.com/codetogodmode/handbook/blob/main/github-guide.md>

Až budeš experimentovat s kódem, vytvoř si branch pro každou změnu — nikdy nepracuj přímo na main. Template ti dává fungující základ, ze kterého můžeš stavět dál.
