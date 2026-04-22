# Switch statement - rozhodování podle hodnoty

```csharp
switch (choice)
        {
            case Operation.Add:
                {
                    result = firstNumber + secondNumber;
                    break;
                }
            case Operation.Substract:
                {
                    result = firstNumber - secondNumber;
                    break;
                }
            case Operation.Multiply:
                {
                    result = firstNumber * secondNumber;
                    break;
                }
            case Operation.Divide:
                {
                    if (secondNumber != 0)
                    {
                        result = firstNumber / secondNumber;
                    }
                    else
                    {
                        Console.WriteLine("Nulou se nedá dělit");
                    }
                    break;
                }
            default:
                {
                    result = 0F;
                    Console.WriteLine("Zadal jsi špatnou operaci");
                    break;
                }
        }
```

## Co je switch statement

Switch je způsob, jak programu říct: "podle toho, jakou hodnotu má proměnná `choice`, udělej jednu z několika různých věcí". Je to jako **rozdělovač na železnici** - vlak (program) jede podle toho, kterou proměnná má hodnotu.

Switch je alternativa k dlouhé řadě `if-else` podmínek, která je čitelnější když máš hodně možností.

## Jak funguje tvůj kód

```csharp
switch (choice)  // Podívej se na hodnotu proměnné choice
{
    case Operation.Add:    // Pokud choice = Operation.Add
        {
            result = firstNumber + secondNumber;  // Sečti čísla
            break;  // Skoč ven ze switch
        }
    
    case Operation.Substract:  // Pokud choice = Operation.Substract
        {
            result = firstNumber - secondNumber;  // Odečti čísla
            break;
        }
    
    case Operation.Multiply:  // Pokud choice = Operation.Multiply
        {
            result = firstNumber * secondNumber;  // Vynásob čísla
            break;
        }
    
    case Operation.Divide:  // Pokud choice = Operation.Divide
        {
            if (secondNumber != 0)  // Kontrola - nulou se nedělí
            {
                result = firstNumber / secondNumber;
            }
            else
            {
                Console.WriteLine("Nulou se nedá dělit");
            }
            break;
        }
    
    default:  // Pokud choice není žádná z výše uvedených hodnot
        {
            result = 0F;
            Console.WriteLine("Zadal jsi špatnou operaci");
            break;
        }
}
```

## Klíčová slova

**`case`** - definuje jednu možnost. "Pokud je hodnota tohle, udělej..."

**`break`** - ukončí switch a skočí za jeho konec. **Bez break by program pokračoval dalšími case!**

**`default`** - "záchranná síť". Spustí se, pokud žádný case neodpovídá hodnotě.

## Operation.Add - co to je?

`Operation` je pravděpodobně **enum** - seznam pojmenovaných konstant. Místo používání čísel (1, 2, 3, 4) máš smysluplné názvy:

```csharp
enum Operation
{
    Add,        // místo 1
    Substract,  // místo 2
    Multiply,   // místo 3
    Divide      // místo 4
}
```

## Proč je tam `if (secondNumber != 0)`?

Dělení nulou způsobí **crash** programu. Proto se kontroluje: pokud druhé číslo není nula (`!= 0`), teprve pak se dělí. Jinak se vypíše chybová hláška.

## CTGM-SPECIFIC

V naší akademii používáme enum místo "magic numbers" od Layer 1. Enum najdeš vysvětlený v <https://github.com/codetogodmode/study-book/blob/main/layer-01/enum-pojmenovane-konstanty-misto-magic-numbers.md>

Tohle je typická struktura kalkulačky - máš operaci (sčítání, odčítání...) uloženou v enum a switch rozhodne, kterou matematickou operaci provést.
