# Rozpoznání kdy rozdělit nebo extrahovat metodu

## OBECNÁ PRAXE

V reálném světě programátoři konstantně refaktorují kód — přepisují ho tak, aby byl čitelnější a udržitelnější. Metody jsou základní nástroj pro organizaci kódu. Když je metoda příliš dlouhá nebo dělá příliš mnoho věcí najednou, rozdělíme ji na menší části.

**Signály, že je čas rozdělit metodu:**

**1. Metoda je příliš dlouhá** — více než 15-20 řádků
**2. Metoda dělá více věcí** — má více než jednu zodpovědnost  
**3. Opakující se kód** — píšeš stejnou logiku na více místech
**4. Těžko se čte** — nerozumíš co dělá, když se k ní vrátíš po týdnu
**5. Hluboké zanořování** — mnoho `if` a `for` cyklů v sobě

### Příklad: Před refaktoringem

```
public void ProcessOrder()
{
    // Validace
    if (string.IsNullOrEmpty(customerName))
        throw new Exception("Jméno zákazníka nesmí být prázdné");
    if (items.Count == 0)
        throw new Exception("Objednávka musí obsahovat položky");
    
    // Výpočet ceny
    decimal totalPrice = 0;
    foreach (var item in items)
    {
        totalPrice += item.Price * item.Quantity;
        if (item.Price < 0)
            throw new Exception("Cena nesmí být záporná");
    }
    
    // Aplikace slevy
    if (customer.IsVip)
        totalPrice *= 0.9m; // 10% sleva
    
    // Uložení do databáze
    var order = new Order
    {
        CustomerName = customerName,
        Items = items,
        TotalPrice = totalPrice,
        OrderDate = DateTime.Now
    };
    database.SaveOrder(order);
    
    // Odeslání emailu
    var subject = "Potvrzení objednávky";
    var body = $"Děkujeme za objednávku. Celková cena: {totalPrice:C}";
    emailService.SendEmail(customer.Email, subject, body);
}
```

### Příklad: Po refaktoringu

```
public void ProcessOrder()
{
    ValidateOrder();
    decimal totalPrice = CalculateTotalPrice();
    totalPrice = ApplyDiscount(totalPrice);
    var order = CreateOrder(totalPrice);
    SaveOrder(order);
    SendConfirmationEmail(totalPrice);
}

private void ValidateOrder()
{
    if (string.IsNullOrEmpty(customerName))
        throw new Exception("Jméno zákazníka nesmí být prázdné");
    if (items.Count == 0)
        throw new Exception("Objednávka musí obsahovat položky");
}

private decimal CalculateTotalPrice()
{
    decimal total = 0;
    foreach (var item in items)
    {
        if (item.Price < 0)
            throw new Exception("Cena nesmí být záporná");
        total += item.Price * item.Quantity;
    }
    return total;
}

private decimal ApplyDiscount(decimal price)
{
    return customer.IsVip ? price * 0.9m : price;
}
```

**Výhody po refaktoringu:**
- Každá metoda dělá jednu věc
- Snadné testování jednotlivých částí
- Znovu použitelný kód (např. `CalculateTotalPrice` můžeš použít jinde)
- Jasný tok programu v hlavní metodě

### Kdy extrahovat opakující se kód

```
// Špatně - duplikace
public void SendWelcomeEmail(string email)
{
    if (string.IsNullOrEmpty(email))
        throw new Exception("Email nesmí být prázdný");
    if (!email.Contains("@"))
        throw new Exception("Neplatný email");
    // pošli email...
}

public void SendNewsletterEmail(string email)
{
    if (string.IsNullOrEmpty(email))
        throw new Exception("Email nesmí být prázdný");
    if (!email.Contains("@"))
        throw new Exception("Neplatný email");
    // pošli newsletter...
}

// Dobře - extrahovaná validace
public void SendWelcomeEmail(string email)
{
    ValidateEmail(email);
    // pošli email...
}

public void SendNewsletterEmail(string email)
{
    ValidateEmail(email);
    // pošli newsletter...
}

private void ValidateEmail(string email)
{
    if (string.IsNullOrEmpty(email))
        throw new Exception("Email nesmí být prázdný");
    if (!email.Contains("@"))
        throw new Exception("Neplatný email");
}
```

## CTGM-SPECIFICKÁ SEKCE

V akademii se s refaktoringem setkáš už v Layer 2, kde se učíš identifikovat "code smells" — kód, který "smrdí" a potřebuje opravu. Refaktoring je klíčová dovednost pro přechod z EXPLAIN na HELPER AI režim.

**Praktický postup v CTGM:**
1. Napiš funkční kód (i když je dlouhý)
2. Rozpoznej signály pro refaktoring
3. Extrahuj části do vlastních metod
4. Otestuj že vše stále funguje
5. Commitni změny s popisem "Refactor: extract validation methods"

Více o organiz
