# Jednoduchá kalkulačka pro začátečníky

```csharp
static void Main(string[] args)
    {
        string textoveCislo;
        float prvniCislo = 5;
        float druheCislo = 50;
        float vysledek = 100;

        Console.WriteLine("Řekni mi první číslo a Enter");
        textoveCislo = Console.ReadLine();
        prvniCislo = float.Parse(textoveCislo);
        Console.WriteLine("Řekni mi druhé číslo a Enter");
        textoveCislo = Console.ReadLine();
        druheCislo = float.Parse(textoveCislo);
        vysledek = prvniCislo + druheCislo;
        Console.WriteLine($"První číslo: {prvniCislo} | Druhé číslo: {druheCislo} | Výsledek součtu: {vysledek}");
        Console.WriteLine();
        Console.ReadKey();
    }
```

## OBECNĚ — Jak funguje konzolová aplikace

Konzolová aplikace je program, který komunikuje s uživatelem pomocí textu. Uživatel píše text na klávesnici (vstup) a program mu odpovídá textem na obrazovce (výstup). Tohle je nejzákladnější způsob, jak se učit programování.

Každá C# konzolová aplikace má **entry point** — místo, kde program začíná. To je metoda `Main`. Když spustíš program, .NET najde tuto metodu a začne vykonávat příkazy jeden po druhém shora dolů.

## Rozebírání kódu řádek po řádku

**Hlavička metody:**
```csharp
static void Main(string[] args)
```
- `Main` — jméno metody, kde program začíná
- `string[] args` — parametr pro argumenty z příkazového řádku (zatím nepoužíváme)
- `static void` — technické klíčové slova (vysvětlíme později)

**Deklarace proměnných:**
```csharp
string textoveCislo;
float prvniCislo = 5;
float druheCislo = 50;
float vysledek = 100;
```
- `string` — datový typ pro text (řetězec znaků)
- `float` — datový typ pro desetinná čísla
- `textoveCislo` — proměnná bez počáteční hodnoty
- `prvniCislo = 5` — proměnná s počáteční hodnotou (později se přepíše)

**Komunikace s uživatelem:**
```csharp
Console.WriteLine("Řekni mi první číslo a Enter");
textoveCislo = Console.ReadLine();
prvniCislo = float.Parse(textoveCislo);
```
- `Console.WriteLine()` — vypíše text na obrazovku
- `Console.ReadLine()` — čeká, až uživatel něco napíše a stiskne Enter
- `float.Parse()` — převede text na číslo (string "5" → float 5.0)

**Výpočet a výstup:**
```csharp
vysledek = prvniCislo + druheCislo;
Console.WriteLine($"První číslo: {prvniCislo} | Druhé číslo: {druheCislo} | Výsledek součtu: {vysledek}");
```
- `prvniCislo + druheCislo` — sečte dvě čísla
- `$"..."` — **string interpolation** — do textu vložíš hodnoty proměnných pomocí `{nazevPromenne}`

**Konec programu:**
```csharp
Console.ReadKey();
```
- Čeká na stisk jakékoliv klávesy před zavřením programu

## Co se děje při spuštění

1. Program se spustí a začne v metodě `Main`
2. Vytvoří čtyři proměnné v paměti
3. Napíše "Řekni mi první číslo a Enter"
4. Čeká, až uživatel něco napíše (například "12.5")
5. Převede text "12.5" na číslo 12.5
6. Totéž udělá pro druhé číslo
7. Sečte obě čísla a uloží výsledek
8. Vypíše formátovaný výsledek
9. Čeká na stisk klávesy a pak skončí

## CTGM-SPECIFIC — Naše praxe

V Layer 1 se učíš základy konzolových aplikací přesně tímhle způsobem. Používáme **template-console** z naší organizace, který obsahuje hotovou strukturu projektu.

Všechny svoje konzolové programy budeš vytvářet ve svém **member repozitáři** ve složkách `src/NazevProjektu/`. Každý projekt commitneš a pushneš na GitHub — to je součást učení práce s Gitem.

Detailní návod na práci s repozitáři najdeš v <https://github.com/codetogodmode/handbook/blob/main/github-guide.md>.

Pro vysvětlení konceptů jako jsou proměnné, datové typy nebo string interpolation používej Discord bota v #help — stačí napsat `!ask Co je string interpolation?`
