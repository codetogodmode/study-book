# Vytvoření a spuštění první C# konzolové aplikace

**Co je repozitář?**
Repozitář je složka s kódem tvého programu. Obsahuje všechny soubory potřebné k běhu aplikace. Je to jako šanon na dokumenty, ale pro programátory.

**Template Console**
Template je předpřipravená šablona aplikace. Console template vytvoří základ pro program, který běží v příkazové řádce (černé okno s textem).

**Postup vytvoření:**

1. **Otevři příkazovou řádku** (Windows: cmd nebo PowerShell)

2. **Přejdi do složky, kde chceš projekt vytvořit:**
```
cd C:\MojeProjekty
```

3. **Vytvoř nový projekt:**
```
dotnet new console -n MojeApp
```
Tím vytvoříš složku "MojeApp" s připraveným kódem.

4. **Přejdi do složky projektu:**
```
cd MojeApp
```

5. **Spusť aplikaci:**
```
dotnet run
```

**Co se stalo?**
Vznikl soubor `Program.cs` s tímto kódem:
```csharp
Console.WriteLine("Hello, World!");
```

**Technické termíny:**
- **dotnet** = nástroj pro práci s .NET projekty
- **Console** = okno pro zobrazování textu
- **WriteLine** = příkaz pro vypsání textu na nový řádek
- **.cs** = přípona pro C# soubory
- **run** = spustit program

**Výsledek:**
Program vypíše "Hello, World!" a skončí. To je tvoje první fungující C# aplikace!

Teď můžeš upravit text v `Console.WriteLine()` a znovu spustit `dotnet run` pro zobrazení změn.
