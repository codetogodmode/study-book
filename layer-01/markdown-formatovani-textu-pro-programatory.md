# Markdown — formátování textu pro programátory

## OBECNÁ PRAXE

**Markdown** je způsob, jak psát formátovaný text pomocí jednoduchých značek. Místo klikání na tlačítka jako v Wordu píšeš speciální znaky přímo do textu. Je to standard v celém programátorském světě.

**K čemu se používá:**
- **README.md** — popis projektu (co dělá, jak ho spustit)
- **Dokumentace** — návody, API reference
- **Issue a pull request popisy** na GitHubu
- **Komentáře** v kódu (některé nástroje)
- **Poznámky** — rychlé formátování bez složitých editorů

**Proč programátoři milují Markdown:**
- Píšeš ho v jakémkoliv textovém editoru
- Verzuje se v Gitu jako běžný kód
- Automaticky se zobrazuje hezky na GitHubu
- Rychlejší než klikání v Wordu

## Základní syntaxe

```markdown
# Hlavní nadpis
## Podnadpis
### Menší nadpis

**Tučný text** a *kurzíva*

- Seznam
- položek
- s odrážkami

1. Číslovaný
2. seznam
3. položek

`inline kód` — třeba názvy proměnných

```csharp
// Blok kódu
Console.WriteLine("Hello World!");
```

[Odkaz na něco](https://github.com)
```

**Jak to vypadá po zobrazení:**
# Hlavní nadpis
## Podnadpis
**Tučný text** a *kurzíva*
- Seznam položek

## Praktické použití v .NET projektech

**README.md v projektu:**
```markdown
# Kalkulačka

Jednoduchá konzolová kalkulačka v C#.

## Jak spustit

```bash
dotnet run
```

## Co umí

- Sčítání, odčítání
- Násobení, dělení
- Validace vstupu

## Autor

Tvoje jméno
```

**Dokumentace třídy:**
```markdown
# Calculator.cs

## Metody

### `Add(int a, int b)`
Sečte dvě čísla.

**Parametry:**
- `a` — první číslo
- `b` — druhé číslo

**Návratová hodnota:** součet jako `int`
```

## CTGM-SPECIFICKÉ

V naší akademii používáme Markdown všude:

**Handbook a Study Book** — celý obsah je v Markdown souborech. Viz náš handbook: <https://github.com/codetogodmode/handbook/blob/main/>

**README.md v repozitářích** — každý member repo má README s popisem projektů:
```markdown
# member-petr

Moje projekty z Code to God Mode akademie.

## Projekty

### src/Calculator/
Konzolová kalkulačka (Layer 1)

### src/TodoManager/
Správa úkolů s třídami (Layer 2)
```

**Pull Request popisy** — když otevřeš PR, GitHub automaticky načte Markdown template pro popis změn.

**Issues** — úkoly a bugy píšeme v Markdown formátu pro lepší čitelnost.

**Discord** — i Discord podporuje základní Markdown (`**tučně**`, `*kurzíva*`, `inline kód`)

**Jak psát Markdown:**
- VS Code má vestavěnou podporu — soubory `.md` se automaticky zvýrazňují
- `Ctrl+Shift+V` otevře preview (jak bude vypadat)
- GitHub automaticky renderuje `.md` soubory hezky

**Tip:** README.md se zobrazuje automaticky, když někdo navštíví tvůj repozitář na GitHubu. Je to první dojem — udělej ho dobrý.
