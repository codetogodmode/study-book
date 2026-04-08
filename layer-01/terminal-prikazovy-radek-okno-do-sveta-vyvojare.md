# Terminál/příkazový řádek — okno do světa vývojáře

## OBECNÁ PRAXE

**Terminál** (nebo **příkazová řádka**) je textové rozhraní, kde komunikuješ s počítačem příkazy místo klikání. Píšeš textový příkaz, stiskneš Enter, počítač ho vykoná. Pro vývojáře je to každodenní nástroj — rychlejší než klikání v průzkumníkovi souborů.

**Proč terminál?** Protože .NET nástroje jsou postavené na příkazech. `dotnet run` spustí program, `git commit` uloží změny. Programátoři celého světa používají tytéž příkazy — na Windows, Mac i Linux.

### Spuštění na Windows

**Nejrychlejší cesty:**
1. **Windows + R** → napiš `cmd` → Enter
2. **Stiskni Windows** → napiš "cmd" → Enter
3. **V průzkumníku:** klikni do adresního řádku → napiš `cmd` → Enter (otevře terminál v té složce)

### Základní příkazy

```
dir                 # zobraz soubory a složky
cd nazev-slozky     # vstup do složky
cd ..               # o složku výš
mkdir nova-slozka   # vytvoř složku
cls                 # vymaž obrazovku
```

**Tip:** Používej **Tab** pro automatické doplňování názvů souborů a složek.

### Praktický příklad

```
C:\Users\Jmeno> mkdir moje-projekty
C:\Users\Jmeno> cd moje-projekty
C:\Users\Jmeno\moje-projekty> dotnet new console -n Kalkulacka
C:\Users\Jmeno\moje-projekty> cd Kalkulacka
C:\Users\Jmeno\moje-projekty\Kalkulacka> dotnet run
Hello, World!
```

## CTGM-SPECIFIC

**Ve VS Code terminál spustíš:**
- **Ctrl+středník** (česká klávesnice)
- **Ctrl+backtick** (anglická klávesnice)
- **Terminal menu → New Terminal**

**Naše workflow:** Terminál používáme hlavně pro Git příkazy a spouštění .NET aplikací:

```
git clone https://github.com/codetogodmode/member-jmeno.git
cd member-jmeno
dotnet run --project src/Calculator
```

**Důležité:** Vždy se ujisti, že jsi ve správné složce před spouštěním příkazů. `dir` (nebo `ls` na Mac/Linux) ti ukáže, kde jsi.

Terminál se zpočátku může zdát složitý, ale během prvních sessions si zvykneš. Je to jako řídit auto — zpočátku myslíš na každý pohyb, později to děláš automaticky.
