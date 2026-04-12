# Git — systém pro sledování změn v kódu

Git je nástroj, který si pamatuje **každou změnu** ve tvém kódu. Představ si to jako "Save game" ve hře — kdykoliv můžeš vrátit zpět k jakékoliv předchozí verzi.

## Proč Git potřebuješ

**Bez Gitu:** Pracuješ na kalkulačce. Přidáš novou funkci, něco se rozbije. Chceš se vrátit k fungující verzi — ale nevíš přesně co jsi změnil. Musíš všechno mazat a psát znovu.

**S Gitem:** Každou funkční verzi "uložíš" (commit). Když se něco rozbije, jedním příkazem se vrátíš k poslední fungující verzi. Git ti ukáže přesně co se změnilo.

**V týmu:** Bez Gitu by se soubory posílaly emailem nebo přes sdílené složky. Chaos. S Gitem všichni pracují na stejném projektu současně, Git změny automaticky sloučí.

## Základní Git workflow

1. **Změníš kód** — přidáš metodu, opravíš bug
2. **`git add`** — připravíš změny k uložení
3. **`git commit`** — uložíš změny s popisem
4. **`git push`** — pošleš změny na GitHub (backup + sdílení)

## Příklad z praxe

Představ si, že píšeš kalkulačku a postupně přidáváš funkce:

```
Commit 1: "Add basic Calculator class"
public class Calculator
{
    public int Add(int a, int b) => a + b;
}

Commit 2: "Add subtraction method"  
public int Subtract(int a, int b) => a - b;

Commit 3: "Add division with zero check"
public double Divide(int a, int b)
{
    if (b == 0) throw new ArgumentException("Cannot divide by zero");
    return (double)a / b;
}
```

Každý commit = jeden funkční krok. Pokud při commit 3 něco rozbiješ, Git tě vrátí na commit 2, kde vše fungovalo.

## CTGM-SPECIFIC

V naší akademii používáme Git workflow popsaný v <https://github.com/codetogodmode/handbook/blob/main/github-guide.md>:

**Layer 1:** Pushneš rovnou na main branch — učíš se základy
**Layer 2+:** Pracuješ s branches a pull requesty — jako v reálném týmu

Tvůj hlavní learning repozitář je `member-{tvoje-jméno}` v organizaci github.com/codetogodmode. Pro experimenty si můžeš vytvořit sandbox repo přes `/new-repo` v Discord kanálu #repos.

**Nejčastější příkazy:**
```
git status      # co se změnilo
git add .       # připrav všechny změny
git commit -m "Add login validation"  # ulož s popisem
git push        # pošli na GitHub
```

Git se zpočátku může zdát složitý, ale základní workflow zvládneš rychle. Detailní návod včetně branch workflow pro Layer 2+ najdeš v GitHub Guide.
