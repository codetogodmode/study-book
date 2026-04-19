# Podmínky a logické operátory — rozhodování v programu

## OBECNÁ PRAXE

Podmínky jsou způsob, jak program **rozhoduje**. Stejně jako v reálném životě se ptáme "Jestli je venku déšť, vezmu si deštník", program se ptá "Jestli je věk větší než 18, ukáž obsah pro dospělé".

### Porovnávání — ptáme se na vztahy

```
int vek = 20;
bool jeDospely = vek >= 18;  // true
bool jeMlady = vek < 25;     // true
bool jePresne20 = vek == 20; // true
bool neni30 = vek != 30;     // true
```

**Operátory porovnání:**
- `==` rovná se
- `!=` nerovná se  
- `>` větší než
- `<` menší než
- `>=` větší nebo rovno
- `<=` menší nebo rovno

### if/else — základní rozhodování

```
int penize = 150;

if (penize >= 100)
{
    Console.WriteLine("Můžu si koupit hru!");
}
else
{
    Console.WriteLine("Musím si ještě našetřit.");
}
```

### AND (&&) — obě podmínky musí platit

```
int vek = 25;
bool maRidicak = true;

if (vek >= 18 && maRidicak)
{
    Console.WriteLine("Můžeš řídit auto");
}
```

Program říká: "JESTLI je věk alespoň 18 **A ZÁROVEŇ** má řidičák, pak může řídit."

### OR (||) — stačí jedna z podmínek

```
string den = "sobota";

if (den == "sobota" || den == "neděle")
{
    Console.WriteLine("Je víkend!");
}
```

Program říká: "JESTLI je sobota **NEBO** neděle, pak je víkend."

### Negace (!) — otočení pravdy

```
bool jeVenku = false;

if (!jeVenku)
{
    Console.WriteLine("Jsi doma");
}
```

Vykřičník `!` znamená "není pravda, že". Takže `!jeVenku` znamená "není pravda, že je venku" = "je doma".

### Složitější příklad — vstup do klubu

```
int vek = 22;
bool maDoklad = true;
bool jeVip = false;

if ((vek >= 21 && maDoklad) || jeVip)
{
    Console.WriteLine("Vstup povolen");
}
else
{
    Console.WriteLine("Vstup zakázán");
}
```

Logika: "Pustíme tě, JESTLI (máš aspoň 21 let A ZÁROVEŇ máš doklad) NEBO jsi VIP host."

### Praktický příklad — validace uživatelského vstupu

```
Console.WriteLine("Zadej své jméno:");
string jmeno = Console.ReadLine();

Console.WriteLine("Zadej svůj věk:");
int vek = int.Parse(Console.ReadLine());

if (string.IsNullOrEmpty(jmeno))
{
    Console.WriteLine("Jméno nesmí být prázdné!");
}
else if (vek < 0 || vek > 150)
{
    Console.WriteLine("Věk musí být mezi 0 a 150 roky!");
}
else
{
    Console.WriteLine($"Zdravím tě, {jmeno}! Je ti {vek} let.");
}
```

## CTGM-SPECIFIC

V našich projektech se podmínky používají hlavně pro:
- **Validaci vstupu** — je email ve správném formátu?
- **Business logiku** — může uživatel provést tuto akci?
- **Flow control** — jakou cestu má program následovat?

Naučíš se je na praktických příkladech jako kalkulačka, guess-the-number hra, nebo jednoduchá inventura. Vždy se snažíme, aby podmínky dávaly smysl v kontextu reálného problému.

Pro pokročilejší materiály viz: <https://github.com/codetogodmode/study-book/blob/main/layer-01/>
