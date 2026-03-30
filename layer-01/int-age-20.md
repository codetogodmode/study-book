# int age = 20;

```csharp
int age = 20;
if (age >= 18)
{
  Console.WriteLine("Adult");
}
else 
{
  Console.WriteLine("Child");
}
```

Ahoj! Pojďme si společně projít tento kousek kódu - je to vlastně docela chytrý program, který rozhoduje, jestli je někdo dospělý nebo dítě. 

**Řádek 1: `int age = 20;`**
Tady vytváříme něco, čemu říkáme "proměnná". Představ si ji jako krabičku s nálepkou "age" (věk), do které vkládáme číslo 20. Slovo `int` říká počítači "tohle bude celé číslo" a znak `=` znamená "vlož do této krabičky".

**Řádek 2: `if (age >= 18)`**
Tady začíná podmínka - jako když si řekneš "Jestli je mi 18 nebo víc, pak...". Slovo `if` znamená "jestli", `>=` znamená "je větší nebo rovno" a v závorce kontrolujeme, jestli je věk 18 nebo víc.

**Řádky 3-5:**
```csharp
{
  Console.WriteLine("Adult");
}
```
Tyto složené závorky `{}` ohraničují, co se má stať, když je podmínka pravdivá. `Console.WriteLine("Adult")` jednoduše napíše na obrazovku slovo "Adult" (dospělý).

**Řádek 6: `else`**
To znamená "jinak" - takže "pokud podmínka není pravdivá, tak místo toho udělej tohle".

**Řádky 7-9:**
```csharp
{
  Console.WriteLine("Child");
}
```
Když věk není 18 nebo víc, napíše se "Child" (dítě).

**Co se vlastně stane?**
Protože máme věk 20 a 20 je určitě víc než 18, program napíše "Adult" na obrazovku.

Je to jako automatický vrátný, který se podívá na tvůj věk a rozhodne, jestli tě pustí do "dospělácké" části nebo tě pošle k dětem! 😊
