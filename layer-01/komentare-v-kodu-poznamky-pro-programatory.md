# Komentáře v kódu — poznámky pro programátory

## Co jsou komentáře

Komentáře jsou **poznámky v kódu**, které čte pouze člověk — počítač je ignoruje. Jsou to vysvětlení, proč něco děláš nebo jak to funguje. Představ si je jako poznámky na okraj učebnice.

V C# máme tři typy komentářů:

```
// Jednořádkový komentář - celý řádek za // se ignoruje

/* Víceřádkový komentář
   může pokračovat přes více řádků
   až do uzavírací */

/// XML dokumentační komentář pro metody a třídy
```

## Kdy komentáře používat

### 1. Vysvětlení složitého kódu

```
// Převod Celsia na Fahrenheit podle vzorce F = C × 9/5 + 32
double fahrenheit = celsius * 9.0 / 5.0 + 32;
```

### 2. Popis účelu metody nebo části kódu

```
// Kontrola, jestli je číslo sudé
if (number % 2 == 0)
{
    Console.WriteLine("Číslo je sudé");
}
```

### 3. Vysvětlení proč, ne jen co

```
// Přidáváme 1, protože pole začíná od indexu 0, ale uživatel počítá od 1
int userPosition = arrayIndex + 1;
```

### 4. Upozornění na důležité věci

```
// POZOR: Tato metoda mění původní pole!
public void SortArray(int[] numbers)
{
    Array.Sort(numbers);
}
```

## Kdy komentáře NEPOUŽÍVAT

### Nekomentuj očividné věci

```
// Špatně - komentář nic nepřidává
int age = 25; // Nastavení věku na 25

// Dobře - bez komentáře, kód mluví za sebe
int age = 25;
```

### Nekomentuj špatný kód, oprav ho

```
// Špatně
// Tato metoda dělá hodně věcí najednou
public void DoEverything() { ... }

// Dobře - rozděl metodu na menší části
public void ValidateInput() { ... }
public void SaveToDatabase() { ... }
```

## Praktický příklad

```
public class Calculator
{
    /// <summary>
    /// Vypočítá DPH z ceny bez daně
    /// </summary>
    /// <param name="priceWithoutTax">Cena bez DPH</param>
    /// <returns>Výše DPH</returns>
    public double CalculateVAT(double priceWithoutTax)
    {
        // V ČR je standardní DPH 21%
        const double VAT_RATE = 0.21;
        
        // Výpočet: cena × sazba DPH
        return priceWithoutTax * VAT_RATE;
    }
    
    /* TODO: Přidat podporu pro sníženou sazbu DPH (12%)
       pro knihy, léky a základní potraviny */
}
```

## CTGM-SPECIFIC — naše pravidla

V akademii preferujeme **kód, který se sám vysvětluje**:

- Používej popisné názvy proměnných místo komentářů
- Rozděl složité metody na menší s jasnými názvy
- Komentuj jen to, co není z kódu patrné

**Zlaté pravidlo:** Dobrý kód potřebuje minimum komentářů. Pokud musíš komentovat co kód dělá, pravděpodobně by měl být přepsán jasněji.

Více o čistém kódu najdeš později v <https://github.com/codetogodmode/handbook/blob/main/definition-of-done.md>
