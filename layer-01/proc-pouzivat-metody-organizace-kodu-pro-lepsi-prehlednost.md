# Proč používat metody — organizace kódu pro lepší přehlednost

## Mentální model — program jako recept

Představ si program jako kuchařský recept. Můžeš napsat vše do jednoho dlouhého odstavce, nebo rozdělit do kroků. Stejně tak kód — místo jedné obří metody vytvoříš několik malých, každou pro jeden úkol.

**Špatně — vše v jednom:**
```csharp
static void Main()
{
    Console.WriteLine("=== KALKULAČKA ===");
    Console.Write("Zadej první číslo: ");
    string input1 = Console.ReadLine();
    int cislo1 = Convert.ToInt32(input1);
    Console.Write("Zadej druhé číslo: ");
    string input2 = Console.ReadLine();
    int cislo2 = Convert.ToInt32(input2);
    int vysledek = cislo1 + cislo2;
    Console.WriteLine($"Výsledek: {cislo1} + {cislo2} = {vysledek}");
    Console.WriteLine("Děkuji za použití kalkulačky!");
}
```

**Lépe — rozděleno do metod:**
```csharp
static void Main()
{
    ZobrazUvod();
    int prvni = ZiskejCisloOdUzivatele("první");
    int druhe = ZiskejCisloOdUzivatele("druhé");
    int vysledek = Secti(prvni, druhe);
    ZobrazVysledek(prvni, druhe, vysledek);
    ZobrazZaver();
}

static void ZobrazUvod()
{
    Console.WriteLine("=== KALKULAČKA ===");
}

static int ZiskejCisloOdUzivatele(string poradi)
{
    Console.Write($"Zadej {poradi} číslo: ");
    return Convert.ToInt32(Console.ReadLine());
}

static int Secti(int a, int b)
{
    return a + b;
}

static void ZobrazVysledek(int a, int b, int vysledek)
{
    Console.WriteLine($"Výsledek: {a} + {b} = {vysledek}");
}

static void ZobrazZaver()
{
    Console.WriteLine("Děkuji za použití kalkulačky!");
}
```

## Single Responsibility Principle (SRP)

Každá metoda by měla mít **jeden jasný účel**. Pokud název metody obsahuje "a" nebo "také", pravděpodobně dělá příliš mnoho věcí.

**Špatně — metoda dělá více věcí:**
```csharp
static void ZpracujUzivatele()
{
    // Načte data
    Console.Write("Zadej jméno: ");
    string jmeno = Console.ReadLine();
    
    // Validuje data
    if (string.IsNullOrEmpty(jmeno))
    {
        Console.WriteLine("Chyba: prázdné jméno");
        return;
    }
    
    // Ukládá data
    // ... kód pro uložení ...
    
    // Zobrazuje potvrzení
    Console.WriteLine($"Uživatel {jmeno} byl uložen");
}
```

**Lépe — každá metoda má jeden účel:**
```csharp
static void SpravujUzivatele()
{
    string jmeno = NactiJmenoOdUzivatele();
    
    if (!JeJmenoValidni(jmeno))
    {
        ZobrazChybu("Prázdné jméno není povoleno");
        return;
    }
    
    UlozUzivatele(jmeno);
    ZobrazPotvrzeni(jmeno);
}

static string NactiJmenoOdUzivatele()
{
    Console.Write("Zadej jméno: ");
    return Console.ReadLine();
}

static bool JeJmenoValidni(string jmeno)
{
    return !string.IsNullOrEmpty(jmeno);
}
```

## Separation of Concerns

Rozděluj kód podle **oblastí odpovědnosti**. UI logika (zobrazování) patří jinam než business logika (výpočty).

**Příklad — správa úkolů:**
```csharp
// UI vrstva - komunikace s uživatelem
static void Main()
{
    while (true)
    {
        ZobrazMenu();
        int volba = ZiskejVolbuOdUzivatele();
        
        switch (volba)
        {
            case 1:
                PridejUkol();
                break;
            case 2:
                ZobrazVsechnyUkoly();
                break;
            case 0:
                return;
        }
    }
}

static void PridejUkol()
{
    Console.Write("Název úkolu: ");
    string nazev = Console.ReadLine();
    
    // Volá business logiku
    if (UlozNovyUkol(nazev))
    {
        Console.WriteLine("Úkol byl přidán!");
    }
    else
    {
        Console.WriteLine("Chyba při ukládání úkolu");
    }
}

// Business logika - pravidla aplikace
static bool UlozNovyUkol(string nazev)
{
    if (string.IsNullOrWhiteSpace(nazev))
        return false;
        
    if (nazev.Length > 100)
        return false;
    
    // Zde by bylo uložení do souboru/databáze
    return true;
}
```

## Jak rozpoznat, kdy rozdělit metodu
