# Statické metody — nástroje, které fungují bez objektů

## OBECNÁ PRAXE

**Statická metoda** je funkce, která patří ke třídě, ale nemusíš vytvářet objekt, abys ji použil. Jde o "nástroj", který je vždy dostupný.

**Parametry** jsou vstupní hodnoty, které metodě předáš — jako ingredience do receptu.

**Návratový typ** definuje, co metoda vrátí zpět — výsledek její práce.

```csharp
public static int Sectilka(int a, int b)
{
    return a + b;
}

// Použití: zavolám přímo přes název třídy
int vysledek = Calculator.Sectilka(5, 3); // vrátí 8
```

### Kdy použít statické metody

- **Utility funkce** — `Math.Max()`, `Console.WriteLine()`
- **Factory metody** — `DateTime.Now`
- **Validace** — `IsValidEmail(string email)`
- **Konverze** — `int.Parse("123")`

Statické metody jsou jako **nářadí v dílně** — máš je vždy po ruce, nemusíš si kupovat celou dílnu.

### Parametry a návratové typy

```csharp
// void = nic nevrací
public static void Pozdrav(string jmeno)
{
    Console.WriteLine($"Ahoj {jmeno}!");
}

// string = vrací text
public static string ZiskejPozdrav(string jmeno)
{
    return $"Ahoj {jmeno}!";
}

// bool = vrací true/false
public static bool JeSude(int cislo)
{
    return cislo % 2 == 0;
}

// více parametrů
public static double Objem(double delka, double sirka, double vyska)
{
    return delka * sirka * vyska;
}
```

## CTGM-SPECIFIC

V naší akademii začínáš se statickými metodami v **Layer 1**, protože jsou jednodušší než objekty. Nemusíš rozumět třídám a instancím — stačí pochopit "funkce, která něco dělá".

**Practical příklady pro tvoje první projekty:**

```csharp
public static class GameUtils
{
    public static bool IsValidMove(int x, int y)
    {
        return x >= 0 && x <= 7 && y >= 0 && y <= 7;
    }

    public static void PrintBoard(char[,] board)
    {
        for (int i = 0; i < 8; i++)
        {
            for (int j = 0; j < 8; j++)
            {
                Console.Write(board[i, j] + " ");
            }
            Console.WriteLine();
        }
    }
}
```

**Pro kalkulačky:**

```csharp
public static class Calculator
{
    public static double Add(double a, double b) => a + b;
    public static double Subtract(double a, double b) => a - b;
    public static double Multiply(double a, double b) => a * b;
    
    public static double Divide(double a, double b)
    {
        if (b == 0)
            throw new ArgumentException("Nelze dělit nulou");
        return a / b;
    }
}
```

V Layer 2 se naučíš **instanční metody** a pochopíš rozdíl — kdy použít static vs. kdy vytvořit objekt.

Více o metodách najdeš v <https://github.com/codetogodmode/study-book/blob/main/layer-01/> (plní se průběžně ze sessions).
