
# Programovací jazyk Python - znalostní požadavky
V jazyce Python budeme pracovat i v druhém ročníku, kde s jeho pomocí budeme programovat počítače micro:bit, a budeme navazovat na základy z prvního ročníku, zveřejňuji vám tu požadavky na znalosti na konci prvního ročníku. Snažím se tím předejít situaci, kdy studenti neznají odpovědi na základní otázky, které pokládám stále dokola.

Počítejte s tím, že většinu hodin budeme začínat čtením kódu a rozborem, co kód dělá, zpočátku společným rozborem, později na známky (berte to jako rychlé zkoušení na začátku hodiny). Cílem tohoto čtení je vybudovat si sebejistotu při čtení kódu a nejsnáze se to dělá jako u každého jiného čtení: Procvičováním.

Znalosti, které nejsou povinné, ale považuji jejich znalost za užitečnou a můžete si tím zlepšit známku jsou označeny jako **[ ROZŠIŘUJÍCÍ ]**

## Doporučené studijní opory:
* [https://www.w3schools.com/python/default.asp](https://www.w3schools.com/python/default.asp)
* [https://microbit-micropython.readthedocs.io/en/latest/index.html](https://microbit-micropython.readthedocs.io/en/latest/index.html)
* **ZA ELEMENTÁRNÍ ZNALOST POVAŽUJI**, že když něco končí **`()`** (s případnými argumenty uvnitř), jedná se o *callable* tedy *volatelný objekt*. Pro vaše potřeby můžete všechny volatelné objekty považovat za **funkce** - existují ještě *metody*, ale jsou strukturně natolik podobné, že pokud se nebudete věnovat programování hlouběji, můžete tato slova považovat téměř za synonyma.

## Moduly:
* [https://www.w3schools.com/python/python_modules.asp](https://www.w3schools.com/python/python_modules.asp)
* Modul je v podstatě knihovna s různými strukturami, které chceme použít v programování. Můžeme si tak nahrát rozšiřující funkce, které chceme používat v kódu.
Zároveň, pokud nějakou strukturu používáme v různých projektech, nemusíme jí psát pokaždé znovu, můžeme si ji dát do samostatné knihovny. Nemusíme ani využívat celou knihovnu, ale můžeme si z ní načíst jen to, co potřebujeme.
U rozsáhlejších projektů se může hodit udržovat rozdílné části kódu v samostatných knihovnách, abychom se rychleji orientovali - to se může hodit v okamžiku, kdy budeme ve druhém ročníku programovat pomocí Pythonu micro:bit.
* **jak vytvořit modul?** ... jakýkoli soubor končící příponou *.py 
*(pozor na `-` ve jménu souboru, protože jde o nepovolený znak proměnné, nelze takový soubor načíst standardní cestou a nejjednodušší je tento znak ve jménech knihoven nepoužívat)*
* musíte znát klíčové slovo **import** a znát rozdíl mezi následujícími zápisy:
  * varianta (A)
    ```
    import random
    ```
    Modul **random** je importován jako samostatný objekt. Pokud budete chtít volat funkce či proměnné v něm definované musíte tak učinit přes tečkovou konvenci:
    ```
    roll = random.randint(1, 6)
    ```
        
  * varianta (B)
    ```
    from random import *
    ```
    Vše z modulu **random** je importováno přímo do hlavního modulu. Výhodou je, že můžeme funkce definované v importovaném modulu volat přímo:
    ```
    roll = randint(1, 6)
    ```
    Nicméně **toto řešení je obecně považováno za špatný návyk** (tzv. *namespace pollution* čili *znečištění jmenného prostoru*), mimo jiné protože hrozí kolize definovaných funkcí, pokud různé zdroje definují funkce stejných jmen.
    **Ve specifických případech se této formy však užívá**, pokud se předpokládá, že píšeme program pro specifické prostředí či hardware a jeho funkce, které budeme používat ve velké míře si tak importujeme hned na začátku. Ve druhém ročníku se budeme potkávat s tím, že programy pro micro:bit v prostředí python.microbit.org obvykle začínají těmito řádky:
    ```
    # Imports go at the top
    from microbit import *
    ```

  * modifikovaná varianta (B*)
    ```
    from random import randint

    roll = randint(1, 6)
    ```
    Pokud chceme z celé knihovny využívat jen jednu či několik konkrétních funkcí či proměnných, můžeme si je do hlavního modulu importovat výše uvedeným způsobem jmenovitě. Tím máme přehled o tom, co jsme si do hlavního programu importovali nemělo by dojít ke konfliktům ve jmenném prostoru.
    Pokud chceme importovat více prvků z modulu, oddělujeme je ve výčtu čárkou (viz příklad u modulu **random**)

  * **[ ROZŠIŘUJÍCÍ ]** varianta (C)
    ```
    import random as r
    ```
    Modul **random** je importován jako samostatný objekt stejně jako u varianty (A), ovšem klíčové slovo `as` umožňuje definovat jméno, kterým modul budeme volat a můžeme si tak výrazně zkrátit volání jeho funkcí
    ```
    roll = r.randint(1, 6)
    ```

* ze všech rozšiřujících knihoven byste měli znát alespoň modul **random**:
    [https://www.w3schools.com/python/module_random.asp](https://www.w3schools.com/python/module_random.asp)
  * **`random()`** ... vrací náhodný **float** mezi `0` a `1`
  * **`randint()`** ... vrací náhodný **integer** ze zadaného rozsahu
  * měli byste umět vysvětlit, co dělá následující kód:
    ```
    from random import random, randint
    
    evaluation_1 = 1 + (random() * 4)
    evaluation_2 = randint(1, 5)
    print("evaluation 1:", evaluation_1, "\nevaluation 2:", evaluation_2)
    ```
  * **[ ROZŠIŘUJÍCÍ ]**
    * **`uniform()`** ... vrací náhodný **float** ze zadaného rozsahu
    *Není třeba znát tuto metodu, ale je třeba vědět, že základní metoda **random()** generuje jen v rozsahu čísel 0 a 1. Případně zkuste zvážit, proč je základní metoda **random()** definována právě takto.*

* další knihovna, se kterou se pravděpodobně často setkáte je modul **math**:
    [://www.w3schools.com/python/module_math.asp](https://www.w3schools.com/python/module_math.asp)
    * **`sqrt()`** ... vrací odmocninu z čísla zadaného jako argument
        ```
        from math import sqrt

        # zadejme délky odvěsen pravoúhlého trojúhelníku
        a = 3
        b = 4

        # výpočet přepony
        c = sqrt(a**2 + b**2)
        ```
    **[ ROZŠIŘUJÍCÍ ]**
    * **`pi`** ... Ludolfovo číslo vyjadřující poměr obvodu kružnice k jejímu průměru
    * **`e`** ... Eulerovo číslo, základ přirozeného logaritmu
    **[ POZNÁMKA ]** všiměte si, že **`pi`** a **`e`** jsou konstanty, nikoli funkce
    * **`log()`** ... lze použít jako přirozený logaritmus s jedním argumentem:
        ```
        import math

        print(math.log(math.e**2))
        ```
        do terminálu se potom vypíše:
        ```
        2.0
        ```
        funkci `log()` však můžeme použít i s dvěma parametry - první číslo pak udává logaritmovanou hodnotu a druhé základ logaritmu:
        ```
        import math

        print(math.log(1024,2))
        ```
        do terminálu se potom vypíše:
        ```
        10.0
        ```
        
    * **`sin()`** ... funkce sinus
    * **`cos()`** ... funkce cosinus
    * **`tan()`** ... funkce tangens
    * **[ POZNÁMKA ]** funkce cotangens není považována za základní funkci, využívá se vztahu *cotg(x) = 1 / tan(x)*
    

## Datové typy, které je třeba znát:
Jedná se o naprosto základní datové typy, které jsou v nějaké podobě přítomné ve všech běžně používaných jazycích. Jejich jména se mohou napříč jazyky mírně měnit, stejně jako určité detaily (například místo seznamů můžete narazit na obecnější strukturu pole), jde mi tedy především o znalost principů.
[https://www.w3schools.com/python/python_datatypes.asp](https://www.w3schools.com/python/python_datatypes.asp)
* **integer** ... celá čísla (mohou být i záporná). Lze s nimi provádět matematické operace (viz *aritmetické operátory*), výsledek ale může být float
* **float** ... čísla s desetinnou čárkou - umožňují vyjadřovat desetinná čísla.
* **string** ... řetězec znaků - lze je skládat (pomocí operátoru `+`) a opakovat (pomocí operátoru `*` následovaného nezáporným celým číslem)
* **boolean** ... má jen dvě hodnoty: `True` nebo `False`. zabírá jen velmi malé množství paměti; proměnná tohoto typu může být použita jako podmínková klauzule
* **list** ... seznamy slouží k uchovávání vícero položek v jedné proměnné, můžeme se odvolávat na konkrétní položku
* **[ ROZŠIŘUJÍCÍ ]** Potenciálně užitečné pro hlubší pochopení jazyka Python, je datový typ **NoneType** a hodnota `None`:
    [https://www.w3schools.com/python/python_none.asp](https://www.w3schools.com/python/python_none.asp)

### Stringy neboli řetězce
* [https://www.w3schools.com/python/python_strings.asp](https://www.w3schools.com/python/python_strings.asp)
* Řetězec znaků zapíšeme tak, že ho obklopíme jednoduchými či dvojitými rovnými uvozovkami:
    ```
    day = 'friday'
    day = "friday"
    ```
    Díky existenci dvojího zápisu je snadné psát tyto uvozovky uvnitř stringu - pokud se liší od počátečního znaku, jsou interpretovány jako znak, nikoli jako funkční symbol:
    ```
    day = "Today is 'friday'"
    day = 'Today is "friday"'
    ```
* Pokud z nějakého důvodu potřebujeme zapsat znak, který buď nemá svou klávesu, nebo je standardně interpretován jako funkční symbol, používáme takzvané **řídící znaky** (můžete se setkat i s výrazem **únikové znaky**, což vychází z doslovného překladu anglického označení **escape characters**, někdy se můžete setkat i s pojmem **escape sekvence**, protože jsou obvykle zapisovány pomocí sekvence po sobě jdoucích znaků).
  [https://www.w3schools.com/python/python_strings_escape.asp](https://www.w3schools.com/python/python_strings_escape.asp)
  Řídící znaky se zapisují tak, že začnete zpětným lomítkem `\` následovaným sekvencí znaků určujících, o jaký znak má jít:
  *   **`\'`** ... jednoduché rovné uvozovky, někdy používány jako apostrof
  Příklad: `text = 'It\'s alright.'`
  *   **`\"`** ... dvojité rovné uvozovky
  *   **`\\`** ... zpětné lomítko
  *   **`\n`** ... nový řádek
  Příklad: `text = "First line.\nSecond line."`
  *   **`\t`** ... tabulátor
* Pokud chceme napsat **víceřádkový string** použijeme jako obklopující znaky tři po sobě jdou jednoduché či dvojíté rovné uvozovky:
    ```
    text = """Lorem ipsum dolor sit amet,
    consectetur adipiscing elit,
    sed do eiusmod tempor incididunt
    ut labore et dolore magna aliqua."""
    ```
* **[ ROZŠIŘUJÍCÍ ]** Pokud chceme vygenerovat nějaký souvislý text z hodnot proměnných, může se nám hodit znalost takzvaných **f-stringů**. Jedná se možnost jak trochu zpřehlednit integraci proměnných do řetězce.
    představte si, že chcete z proměnných `nickname`, která obsahuje jméno uživatele, a `followage`, která obsahuje délku odběru kanálu ve dnech, vypsat, jak dlouho vás uživatel sleduje.
    Pokud ještě potřebujete zápis nějak formátovat - třeba followage by obsahoval float a chtěli bychom to nějak zaokrouhlit na dvě desetinná místa, začalo by to být klasický zápis poněkud nepřehledný.
    ```
    print(nickname + " follows you " + str(round(followage, 2)) + " days.")
    ```
    Proto se od Pythonu 3.6 zavedly f-stringy a staly se preferovaným způsobem formátování: zapíšeme ho tak, že před uvozovky jedno- či víceřádkového stringu zapíšeme `f` a na místa, kam chceme umístit hodnoty proměnných zadáme takzvaný *placeholder* označený pomocí složených závorek `{}`. Do těchto závorek potom vepíšeme jméno proměnné, která se automaticky převede na datový typ string.
    Uvnitř placeholderu můžou být i jednoduché operace s proměnnými a konstantami a i formátování proměnné, které se provádí pomocí modifikátoru `:` následovaného označením formátovacího typu, například `.2f` pro výpis na dvě desetinná místa. Výsledný **f-string**, který by měl být přehlednější pak vypadá takto:
    ```
    print(f"{nickname} follows you {followage:.2f} days.")
    ```    
    Více informací o formátovacích typech se můžete dozvědět zde: [https://www.w3schools.com/python/ref_string_format.asp](https://www.w3schools.com/python/ref_string_format.asp)

## Komentáře
* [https://www.w3schools.com/python/python_comments.asp](https://www.w3schools.com/python/python_comments.asp)
* Začátečníky podceňovaný, přesto velmi důležitý nástroj při psaní kódu. Nepodceňujte komentáře - zkuste o kódu uvažovat tak, že si do nich zapíšete všechno, co byste potřebovali říct, abyste za půl roku, poté, co jste kód vůbec neviděli, hned věděli, co se v něm kde děje
* komentáře mohou sloužit k vysvětlení části kódu
    ```
    # declare a variable
    name = "John"

    # print name
    print(name)    # John
    ```
* komentáře můžeme použít k větší čitelnosti kódu
    ```
    # This will print Hello, World!
    print("Hello, World!")
    ```
* komentáře mohou být použity, aby zabránili spuštění nějaké části kódu, čehož se často využívá během testování
    ```
    number1 = 10
    number2 = 15

    sum = number1 + number2

    print("The sum is:", sum)
    # print('The product is:', product)
    ```

### Víceřádkové komentáře
V jazyce Python není definován žádný zápis určený přímo pro víceřádkový komentář. Běžně se ale využívá toho, že string, který není uložený do žádné proměnné, nebo není parametrem funkce, pak ho interpret ignoruje. To znamená, že tyto stringy lze využívat jako komentáře.
Využívá se toho právě v případě víceřádkových stringů - někdy se můžete setkat s tím, že na začátku kódu budete mít takto shrnuto, co daná knihovna řeší.
```
"""
This is an example 
of multiline comment
"""
print("Hello, World!")
```

## Proměnné:
* [https://www.w3schools.com/python/python_variables_names.asp](https://www.w3schools.com/python/python_variables_names.asp)
* jak se zapisují hodnoty různých datových typů:
    ```
    name = 'Me'
    my_id = 13
    duck = False
    my_list = []
    ```
* jak se mohou, respektive nesmí jmenovat proměnné (jak používat čislice ve jménu proměnné, užití mezer a speciálních znaků, klíčová slova ve jménu proměnné )
* jaký je vliv velikosti písmen na identifikaci proměnných? 
Porovnejte například zápis `age`, `AGE` a `Age`
* **[ ROZŠIŘUJÍCÍ ]** co znamená, když proměnná začíná znakem `_`?

## Operátory
### Aritmetické operátory
* [https://www.w3schools.com/python/python_operators_arithmetic.asp](https://www.w3schools.com/python/python_operators_arithmetic.asp)
* jak se zapisují základní aritmetické operace sčítání, odčítání, násobení dělení (operátory `+`, `-`, `*` `/`)
* jak fungují operátory `+` a `*`, když je aplikujeme na **string**?
* **[ ROZŠIŘUJÍCÍ ]** užitečné operace jako mocnina, celočíselné dělení a modulo (operátory `**`, `//` a `%`)
  
### Přiřazovací operátory
* [https://www.w3schools.com/python/python_operators_assign.asp](https://www.w3schools.com/python/python_operators_assign.asp)
* základní přiřazení `=`
* modifikace hodnoty: `+=`, `-=`, `*=` a `/=`
* **[ ROZŠIŘUJÍCÍ ]** operátory `//=`, `%=` nebo `**=`

### Porovnávací operátory
* [https://www.w3schools.com/python/python_operators_comparison.asp](https://www.w3schools.com/python/python_operators_comparison.asp)
* rovnost `==`
(**JE TŘEBA ZNÁT ROZDÍL MEZI OPERÁTORY `=` A `==`**, je to jedna z nejčastějších chyb v zápisu kódu)
* různé typy nerovností
  * `!=` není rovno, 
  * `>` větší než, 
  * `<` menší než, 
  * `>=` větší nebo rovno než, 
  * `<=` menší nebo rovno než
* uveďte běžný případ použití (viz *Podmíněné příkazy* a *Cykly*)

### Logické operátory
* [https://www.w3schools.com/python/python_operators_logical.asp](https://www.w3schools.com/python/python_operators_logical.asp)
* logické operátory určují jaká **logická funkce** má být provedena se zadaným výrazem.
  * **logická funkce** je funkce, která má za vstupní výrazy parametry, kterým lze přiřadit logickou hodnotu (v Pythonu hodnoty mohou být `True` nebo `False`), a vrací opět logickou hodnotu.
* operátory 
  * `and` ... **konjunkce**: binární funkce, která ověřuje zda jsou oba parametry `True`
  * `or`  ... (inkluzivní) **disjunkce**: binární funkce, která ověřuje, zda alespoň jeden parametr je `True`
  * `not` ... **negace**: unární funkce, která vrací opačnou hodnotu než má vstupní parametr
* konstanty - v některých případech jde konstanty použít jako nulární funkce (tedy bez parametru)
  * `True` ... vrací vždy hodnotu `True`
  * `False` ... vrací vždy hodnotu `False`
* **[ ROZŠIŘUJÍCÍ ]** pravdivostní hodnoty proměnných: Python umí přiřadit každé proměnné pravdivostní hodnotu, obdobně jako bychom zavolali funkci `bool()` s danou proměnnou jako parametrem.
  * **string** - Prázdný řetězec (`""` nebo `''`) je `False`, jinak (tedy například i `" "`) je `True`
  * **integer** - Nula (`0`) je `False`, jinak (tedy například i `-5`) je `True`
  * **float** - Nula (`0.0`) je `False`, jinak (tedy například i `-5.0`) je `True`
  * **list** - Prázdný list (`[]`) je `False`, jinak (tedy list s alespoň jedním prvkem) je `True`
  * **NoneType** (hodnota `None`) - vždy `False`

## Podmíněné příkazy:
* [https://www.w3schools.com/python/python_conditions.asp](https://www.w3schools.com/python/python_conditions.asp)
* Podmíněné příkazy jsou nejdůležitější nástroj větvení kódu. 
* **[ TERMINOLOGICKÁ POZNÁMKA ]** Podmínkou rozumíme jakýkoliv výraz, kterému lze přiřadit pravdivostní hodnotu.

* Základní klíčové slovo je **`if`** po něm následuje **podmínka** a **`:`**,
    další řádek odsadíme a zapíšeme, co se má stát při splnění podmínky. Toto je jediná povinná část podmínky
    ```
    if day == "friday":
        print("Congratulations! Weekend is near! Keep working!")
    ```
* Pokud chcete situaci rozčlenit do více stavů, můžeme využít kličové slovo **`elif`**, kterým za které napíšeme další kontrolovanou **podmínku**.
    Pamatujte, že podmínky se vyhodnocují v pořadí v jakém jsou zapsané a do další podmínky se dostaneme jen neúspěchem všech předchozích.
    ```
    # Chceme zjistit, zda je x uvnitř rozmezí 5 a 10
    if x < 5:
        print("x není v rozmezí")
    elif x <= 10:
        print("x je v rozmezí")
    elif x > 10:
        print("x není v rozmezí")
    ```
* Na konec můžete případně zařadit klíčové slovo **`else`** které znamená *ve všech ostatních případech*
    Příklad stejného vyhodnocení trochu efektivnějším způsobem:
    ```
    if (x < 5) or (x > 10):
        print("x není v rozmezí")
    else:
        print("x je v rozmezí")
    ```
* Příklad plně rozvinutého podmíněného příkazu:
    ```
    import math
    
    D = b**2 - 4 * a * c
        
    if D > 0:
        x1 = (-b + math.sqrt(D)) / (2 * a)
        x2 = (-b - math.sqrt(D)) / (2 * a)
        print(f"Two real roots: x1 = {x1}, x2 = {x2}")
    elif D == 0:
        x = -b / (2 * a)
        print(f"Real double root: x = {x}.")    
    else:
        print("No real root.")
    ```
### Vnořené podmíněné příkazy
Je dobré připomenout, že dovnitř podmíněných příkazů lze vkládat jiné podmíněné příkazy. Všiměte si, že úroveň vnoření je dána odsazením zleva, takzvanou indentací, kterých lze řadit více za sebe a podle toho poznáme, jak hluboko jsme ve struktuře kódu.
```
if year % 400 == 0:
    leap_year = True
else:
    if year % 100 == 0:
        leap_year = False
    else:
        if year % 4 == 0:
            leap_year = True
        else:
            leap_year = False
```
Všiměte si, že výše popsaný algoritmus lze pomocí `elif` zapsat bez potřeby vnořovat další podmíněný příkaz. Kód je potom čitelnější:
```
if year % 400 == 0:
    leap_year = True
elif year % 100 == 0:
    leap_year = False
elif year % 4 == 0:
    leap_year = True
else:
    leap_year = False
```

## Cykly:
Cyklus je kód, který se provádí opakovaně. Místo abychom vypisovali stále dokola ty samé kroky, tak sepišeme jednu sadu (jeden průchod cyklu) a určíme, kolikrát se má vnitřek cyklu opakovat.

### FOR-cyklus čili cyklus s konkrétním počtem opakování
* [https://www.w3schools.com/python/python_for_loops.asp](https://www.w3schools.com/python/python_for_loops.asp)
* Pokud známe konkrétní počet opakování předem, nejsnazší způsob, je použít cyklus `for`.
  Například pokud bychom chtěli napsat instrukce pro nakreslení čtverce, mohlo by to vypadat nějak takto:
  ```
  import turtle as t
  
  for i in range(4):
      t.forward(100)
      t.left(90)
  ```
* Nejčastějším způsobem použití cyklu `for` však je, že ho chceme použít pro procházení nějaké skupiny položku po položce. Například bychom chtěli vypsat všechny Sněhurčiny trpaslíky ze seznamu `dwarfs` - pak nejprve určíme jméno proměnné do které se načte hodnota konkrétní položky a pak určíme, kde se má položka hledat:
  ```
  dwarfs = ["Prófa","Rejpal","Kejchal", "Stydlín", "Dřímal", "Štístko","Šmudla"]
  for name in dwarfs:
      print(f"{name} jde z práce a zpívá: Ajho, ajho!")
  ```
* **[ ROZŠIŘUJÍCÍ ]** Možná jste si všimli, že v našem příkladu s kreslením čtverce jsme vůbec nepoužili hodnotu proměnné `i`. V případech, kdy hodnotu proměnné přes kterou iterujeme vůbec nechceme použít, můžeme uvést její jméno `_` a pythonu tím řekneme, že její hodnotu nebudeme vůbec potřebovat. Náš příklad by pak vypadal takto: 
  ```
  import turtle as t
  
  for _ in range(4):
      t.forward(100)
      t.left(90)
  ```

### WHILE-cyklus čili cyklus s podmínkou
* [https://www.w3schools.com/python/python_while_loops.asp](https://www.w3schools.com/python/python_while_loops.asp)
* Někdy se může stát, že neznáme konkrétní počet opakování, jen známe okolnosti, za kterých máme stále pokračovat, případně kdy skončit. Pro takové situace použijeme cyklus `while` za který doplníme podmínku, kterou zkontroluje při každém průchodu a pokud je pravdivá provede další průchod cyklem.
 Hezkým příkladem pro použití byl hod kostkou ve hře *Člověče nezlob se!* kde se hází znovu, když padně 6. Všimněte si, že když podmínka nebude splněna hned na začátku, vnitřek cyklu se vůbec neprovede.
  ```
  from random import randint
  # budeme potřebovat generátor náhodných čísel
  
  roll = randint(1, 6) # samotný hod
  bonus = 0            # čítač bonusových hodů
  
  while roll == 6:     # když padne 6 házej znovu
      bonus += 1
      roll = randint(1, 6)
  
  roll += 6 * bonus    # konečný výsledek hodu
  ```

## Definice funkcí
* [https://www.w3schools.com/python/python_functions.asp](https://www.w3schools.com/python/python_functions.asp)
* Některé části procedury chceme vykonávat častěji a místo abychom pořád dokola opakovali ten samý kód, můžeme si je uložit jako funkce. Tím zajistíme, že kód bude jen na jednom místě a pokud bychom potřebovali upravit jeho mechanismus, nemusíme se bát, že ho někde zapomeneme opravit.
* Pro definici funkce se používá klíčové slovo **`def`** následované jménem funkce a závorkami. Takto si vytvoříme funkci, která nám vypíše aktuální datum a čas:
* **[ UPOZORNĚNÍ ]** modul **datetime** využívaný v následujících příkladech není implementován v Pythonu pro micro:bit, který využívá zjednodušený modul **utime**. 
 * Specifikace modulu **utime** pro micro:bit : [https://microbit-micropython.readthedocs.io/en/latest/utime.html](https://microbit-micropython.readthedocs.io/en/latest/utime.html)
   ```
   # Chceme mít příkaz, který nám vypíše aktuální čas a nechceme přemýšlet nad moduly v pythonu
   def now():
    from datetime import datetime # modul datetime je knihovna sloužící k práci s datem a časem
     
     actual_time = datetime.now()
     print(actual_time)
    ```
* Funkce můžeme také modifikovat pomocí parametrů, které uvedeme do závorek - v našem případě bychom například chtěli mít možnost vypsat jenom čas, bez data, ale zachovat i možnost napsat datum. Případně vypsat jen datum.
* **[ TERMINOLOGICKÁ POZNÁMKA ]** parametr je proměnná, kterou zadáváme do funkce, argument je pak označení pro její hodnotu. Parametry se tedy objevují při definici funkce, argumenty při jejím volání
 * `def now(mode)` ... *mode* je v následujícím příkladu parametr
 * `now("date")` ... *"date"* by byl argument při volání funkce
  ```
    def now(mode):
        from datetime import datetime               # modul datetime je knihovna sloužící k práci s datem a časem

        if mode == "time":
            actual_time = datetime.now().time()     # vypíše pouze čas
        elif mode == "date":
            actual_time = datetime.now().date()     # vypíše pouze datum
        elif mode == "full":
            actual_time = datetime.now()
        else:
            actual_time = f"Unknown mode. Actual datetime is {datetime.now()}"
        print(actual_time)
  ```
* Ne vždy ale chceme, aby se nám výsledek vypsal, ale chceme s ním pracovat dál. Pak využijeme klíčové slovo **`return`**, které definuje, co funkce vrací na výstupu:
    ```
    def now(mode):
        from datetime import datetime               # modul datetime je knihovna sloužící k práci s datem a časem

        if mode == "time":
            actual_time = datetime.now().time()     # vypíše pouze čas
        elif mode == "date":
            actual_time = datetime.now().date()     # vypíše pouze datum
        elif mode == "full":
            actual_time = datetime.now()
        else:
            actual_time = None                      # na neznámý vstup nevíme jak reagovat

        return actual_time                          # funkce vrátí hodnotu proměnné actual_time
    ```
* Parametr samozřejmě můžeme použít jako vstupní argument pro nějaký výpočet, dokonce to bývá nejčastější využití:
    ```
    # Chceme napříkald funkci, která nám bude převádět stupně Fahrenheita na stupně Celsia:

    def f2c(fahrenheit):                            # jméno funkce doporučuji zvolit takové,
                                                    # aby bylo srozumitelné a pokud ji plánujeme
                                                    # psát často, může být výhodnější zvolit krátké jméno
        celsius = (fahrenheit - 32) * 5 / 9
        return celsius
    ```
* Když už jsme si vysvětlili co dělá klíčové slovo **`return`**, můžeme si definovat hod kostkou z našeho příkladu u WHILE-cyklu jako funkci:
    ```
    def d6plus():
        """ 
        Ze stolních RPG jako je Dungeons&Dragons jsme si vypůjčili označení
        pro hod šestistěnnou kostkou. Jako d6+ se někdy značí hod, kdy se po hození
        šestky hází znovu a hodnota se přičítá k výsledku.
        """
        from random import randint
    
        roll = randint(1, 6) # samotný hod
        bonus = 0            # čítač bonusových hodů
        while roll == 6:     # když padne 6 házej znovu
            bonus += 1
            roll = randint(1, 6)
        roll += 6 * bonus    # konečný výsledek hodu

        return roll
    ```
* **[ ROZŠIŘUJÍCÍ ]** Všimněte si že první string zapsaný ihned pod hlavičkou funkce se v Pythonu nazývá docstring (dokumentační řetězec). Slouží k oficiální dokumentaci funkce a lze vyvolat pomocí funkce **`help()`**, které jako argument zadáte název této funkce. Při zadání příkazu `help(d6plus)` se vám potom do terminálu vypíše následující:
    ```
    Help on function d6plus in module __main__:

    d6plus()
        Ze stolních RPG jako je Dungeons&Dragons jsme si vypůjčili označení
        pro hod šestistěnnou kostkou. Jako d6+ se někdy značí hod, kdy se po hození
        šestky hází znovu a hodnota se přičítá k výsledku.
    ```

* **[ ROZŠIŘUJÍCÍ ]** Někdy se může stát, že ve většině případů chceme funkci volat s konkrétním nastavením a je občas to změnit. K tomu můžeme použít takzvané **defaultní hodnoty parametrů**. Ty se uvádí na konci výčtu parametrů a pokud chceme všem parametrům, které je mají nastavené, ponechat defaultní hodnotu, můžeme ji vynechat.
    Například u funkce **`now()`**, kterou jsme si definovali výše můžeme předpokládat, že nás bude nejčasteji zajímat aktuální čas, protože obvykle víme, který je den. Můžeme ji tedy definovat následující způsobem a když ji zavoláme `now()` vypíše se nám automaticky jen aktuální čas.
 * Podrobnější popis můžete nastudovat zde: [https://www.w3schools.com/python/python_arguments.asp](https://www.w3schools.com/python/python_arguments.asp)
    ```
    def now(mode="time"):                           # defaultní hodnota parametru mode je "time"
        from datetime import datetime               # modul datetime je knihovna sloužící k práci s datem a časem

        if mode == "time":
            actual_time = datetime.now().time()     # vypíše pouze čas
        elif mode == "date":
            actual_time = datetime.now().date()     # vypíše pouze datum
        elif mode == "full":
            actual_time = datetime.now()
        else:
            actual_time = None                      # na neznámý vstup nevíme jak reagovat

        return actual_time                          # funkce vrátí hodnotu proměnné actual_time
    ```
* **[ JEŠTĚ VÍCE ROZŠIŘUJÍCÍ ]** Můžete si všimnout, že stále máme problém s tím, že pokud uživatel zadá nějaký neznámý parametr, vrátí nám funkce hodnotu `None`. Jedním ze způsobů, jak to můžeme ošetřit je, že v takovém případě zavoláme funkci s defaultním parametrem. To můžeme provést pomocí takzvané rekurze, tedy že funkce zavolá samu sebe, obvykle s jiným argumentem, než mělo původní volání. Tuto možnost využívejte opatrně a pokud si nejste jisti, jak funguje, raději se jí vyhněte - při špatně napsaném algoritmu riskujete zacyklení programu a při neefektivní implementaci rekurze může dojít k zahlcení paměti (tzv. stack overflow) i u matematicky korektního algoritmu.
  * Základní informace jsou zde: [https://www.w3schools.com/python/gloss_python_function_recursion.asp](https://www.w3schools.com/python/gloss_python_function_recursion.asp)
  ```
    def now(mode="time"):                           # defaultní hodnota parametru mode je "time"
        from datetime import datetime               # modul datetime je knihovna sloužící k práci s datem a časem

        if mode == "time":
            actual_time = datetime.now().time()     # vypíše pouze čas
        elif mode == "date":
            actual_time = datetime.now().date()     # vypíše pouze datum
        elif mode == "full":
            actual_time = datetime.now()
        else:
            actual_time = now()                     # na neznámý vstup reagujeme
                                                    # voláním defaultního parametru pomocí rekurze

        return actual_time                          # funkce vrátí hodnotu proměnné actual_time
    ```
    **[ UPOZORNĚNÍ ]** Reálná praxe vývoje programů by situaci s neznámým argumentem s největší pravděpodobností řešila vyvoláním výjimky a chybového hlášení `ValueError`. Problematika chybových hlášení je však dalece za hranicemi rozsahu našeho kurzu. 
    * Pokud by vás tato problematika zajímala, můžete začít například zde: [https://www.w3schools.com/python/python_try_except.asp](https://www.w3schools.com/python/python_try_except.asp)
    * Pro potřeby výuky **stačí, když budete mít na zřeteli, že je třeba nějak ošetřit situace, kdy funkci zavoláme s nezamýšleným či nečekaným parametrem**. Pokud neomezíme chod funkce jen na požadované hodnoty, tak se nám v lepším případě program zhroutí, v horším se začne chovat neočekávaně.
    * Hledáním podivného chování programu se zabývají **softwaroví testeři**, kteří se obvykle snaží program přimět k podivnému chování či pádu. Poměrně dobře ilustruje náplň jejich práce následující vtip:

        > **Softwarový tester vejde do baru.**
        > 
        > Vběhne do baru.  
        > Přikrade se do baru.  
        > Vtančí do baru.  
        > Vletí do baru.  
        > Skočí do baru.  
        > - Tester si objedná 1 pivo.
        Barman odpoví: „Zde je vaše objednávka na pivo.“ a tester dostane 1 pivo.
        > - Tester si objedná 2 piva. 
        Barman odpoví: „Zde je vaše objednávka na pivo v požadovaném počtu 2 ks.“ a tester dostane 2 piva.
        > - Tester si objedná 0 piv. 
        Barman odpoví: „Vaše přání bylo automaticky splněno.“
        > - Tester si objedná -1 pivo. 
        Barman odpoví: „Bohužel nevím jak donést záporné množství objednané položky pivo“
        > - Tester si objedná 9999999999 piv. 
        Barman odpoví: „Položku pivo máme už jen v počtu 67 ks.“
        > - Tester si objedná ještěrku. 
        Barman odpoví: „Bohužel položku ještěrka nemáme v nabídce.“
        > - Tester si objedná "qwertzuuio". 
        Barman odpoví: „Pardon, nerozuměl jsem vaší objednávce.“
        >
        > Tester ukončí testování baru.
        > 
        > **Do baru vstoupí skutečný zákazník**
        > 
        > Zákazník se zeptá barmana: „Mohl bych si u vás zajít na toaletu?“
        > Barman odejde do skladu. Po chvili se vrátí s toaletní mísou,
        > postaví ji na bar a odpoví: „Zde je vaše objednávka na pivo.“
        > V baru rychle stoupá hladina unikající vody
        > 
        > *Po nahlášení incidentu tester reportuje bug s popisem:*  
        > *Bar byl vytopen, protože barman při snaze vyplnit objednávku
        > procházel kompletní inventář skladu, nikoli jen skladové zásoby zboží.*

        Funkce, která způsobila vytopení baru v uvedeném vtipu mohla vypadat nějak takto:


        ```
        def order(request):
            """
            Funkce hledá jakékoliv známé klíčové slovo v textu od zákazníka.
            Rozpoznanou věc rovnou doručí na bar.
            """
            from storage import inventory
            # z vymyšleného modulu storage si importujeme seznam věcí inventory
            # inventory je datová struktura slovník (dictionary) ve formátu "položka":množství
        
            from parser import items
            # vymyšlený modul, který nám ze zadané otázky vytáhne klíčová slova
            # smyšlená funkce items() vrací list, kde každá položka 
            # bude dvojice s názvem věci jako první položka a kvantitou
            # jako druhou položkou. 
            # Pokud funkce items() rozpozná věc, ale neidentifikuje množství, 
            # uvede defaultní množství, tedy 1

            order = items(request)  # do proměnné order si pomocí funkce items uložíme seznam objednaných položek
            response = []

            if len(order) == 0:     # toto nastane, pokud items() nerozpozná žádná klíčová slova
                response = ["Pardon, nerozuměl jsem vaší objednávce."]
            else:
                for item in order:  # každá položka v proměnné je dvojice (komodita, množství)
                    if item[0] not in inventory:
                        partial_response = f"Bohužel položku {item[0]} nemáme v nabídce."
                    elif item[1] == 0:
                        partial_response = f"Vaše přání bylo automaticky splněno."
                    elif item[1] < 0:
                        partial_response = f"Bohužel nevím jak donést záporné množství objednané položky {item[0]}"
                    elif inventory[item[0]] == 0:       # pokud je skladové množství dané položky 0
                        partial_response = f"Bohužel {item[0]} už nemáme na skladě."
                    elif item[1] > inventory[item[0]]:  # pokud je objednávka větší než skladové zásoby
                        partial_response = f"Položku {item[0]} máme už jen v počtu {inventory[item[0]]} ks."
                    elif item[1] > 5:
                        partial_response = (
                            f"Nemáme dost nádobí, abychom mohli hostům donést tak velkou "
                            f"objednávku položky {item[0]} najednou. Ale mohu vám donést "
                            f"pro začátek 5 ks a pak si můžete objednat další."
                        )        # Využití implicitního řetězení stringů v závorce pro zapssání dlohouhého stringu
                    else:
                        partial_response = f"Zde je vaše objednávka na {item[0]}"
                        if item[1] > 1: 
                            partial_response += f" v požadovaném počtu {item[1]} ks"
                        partial_response += "."
                    response.append(partial_response)

            return response            
        ```
