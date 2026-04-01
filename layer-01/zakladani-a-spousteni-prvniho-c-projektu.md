# Zakládání a spouštění prvního C# projektu

**Repozitář** je jako složka pro tvůj projekt na GitHubu, kde se uchovává kód a jeho historie změn.

**Template Console** je předpřipravená šablona pro console aplikaci (program, který běží v příkazové řádce a vypisuje text).

## Založení repozitáře z template

1. Jdi na GitHub do template repozitáře
2. Klikni **"Use this template"** → **"Create a new repository"**
3. Zadej název repozitáře (např. `moje-prvni-aplikace`)
4. Klikni **"Create repository"**

## Stažení repozitáře (clone)

**Clone** znamená stáhnout kopii repozitáře z GitHubu na tvůj počítač.

Otevři terminal/příkazový řádek a zadej:

```
git clone https://github.com/tvoje-jmeno/moje-prvni-aplikace.git C:\Dev\MojePrvniAplikace
```

**Vysvětlení:**
- `git clone` - příkaz pro stažení repozitáře
- URL repozitáře - odkaz na tvůj GitHub repozitář  
- `C:\Dev\MojePrvniAplikace` - **custom složka** kde chceš projekt uložit

## Spuštění aplikace

Přejdi do složky projektu:
```
cd C:\Dev\MojePrvniAplikace
```

Spusť aplikaci:
```
dotnet run
```

**Co se stane:** .NET najde soubor `Program.cs` a spustí kód, který obsahuje:

```
Console.WriteLine("Hello, World!");
```

V terminálu uvidíš výstup: `Hello, World!`

## Klíčové technické termíny

**Console aplikace** - program bez grafického rozhraní, komunikuje přes text v terminálu

**dotnet** - nástroj pro práci s .NET projekty (kompilace, spouštění)

**Program.cs** - hlavní soubor s metodou `Main()`, kde program začíne

**Terminal/Příkazový řádek** - textové rozhraní pro zadávání příkazů operačnímu systému

Více o práci s Git a GitHub najdeš v našem [GitHub Guide](github-guide.md).
