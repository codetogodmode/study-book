# Terminál a VS Code — základní nástroje vývojáře

**Terminál** (také **cmd** nebo **command line**) je textové rozhraní pro ovládání počítače. Místo klikání myší píšeš příkazy.

Ve Windows máš několik možností:
- **Command Prompt** (cmd) — klasický Windows terminál
- **PowerShell** — pokročilejší Windows terminál
- **Git Bash** — terminál s Linux příkazy (instaluje se s Gitem)

## Proč terminál potřebuješ

V programování děláš věci, které v grafickém rozhraní nejdou nebo jsou pomalé:
- Vytvoření nového C# projektu
- Instalace balíčků (NuGet packages)
- Spuštění aplikace
- Práce s Git (commit, push, pull)

## Základní příkazy

```
cd Documents              # Přejdi do složky Documents
cd ..                    # Přejdi o složku výš
dir                      # Zobraz obsah složky (Windows)
ls                       # Zobraz obsah složky (Mac/Linux)
mkdir MujProjekt         # Vytvoř novou složku
```

## Práce s .NET projekty

```
dotnet new console       # Vytvoř novou konzolovou aplikaci
dotnet run              # Spusť aplikaci
dotnet build            # Zkompiluj projekt
dotnet add package Newtonsoft.Json  # Přidej NuGet balíček
```

## Visual Studio Code

**VS Code** je editor kódu — místo kde píšeš programy. Je zdarma, rychlý a má spoustu rozšíření.

**Základní workflow:**
1. Otevři složku s projektem (**File → Open Folder**)
2. Napiš kód
3. Spusť přes terminál (`dotnet run`) nebo **Ctrl+F5**

## Propojení s terminálem

VS Code má **zabudovaný terminál** (**View → Terminal** nebo **Ctrl+`**). Můžeš tak psát kód a spouštět příkazy na jednom místě.

**Praktický příklad:**
1. Otevři terminál, vytvoř projekt:
```
mkdir MojeKalkulacka
cd MojeKalkulacka
dotnet new console
```

2. Otevři VS Code ve stejné složce:
```
code .
```

3. V `Program.cs` napiš:
```
Console.WriteLine("Ahoj světe!");
```

4. Ve VS Code terminálu spusť:
```
dotnet run
```

**Výsledek:** Uvidíš "Ahoj světe!" v terminálu.

## Tipy pro začátek

- **Tab completion** — napiš začátek příkazu a zmáčkni Tab
- **Šipky nahoru/dolů** — procházej historii příkazů
- **Ctrl+C** — zastav běžící program
- Terminál "pamatuje" kde jsi — vždy kontroluj aktuální složku

Terminál zpočátku vypadá scary, ale je to jen jiný způsob komunikace s počítačem. Za týden budeš rychlejší než s myší.
