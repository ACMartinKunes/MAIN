---
title: AC - Financial pack - Controling Basic | Microsoft Docs
description: Jednoduchy popis tematu
author: ACMartinKunes

ms.service: dynamics365-business-central
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.search.keywords: Controling basic, finance 
ms.date: 01/31/2021
ms.author: AC MartinKunes
---
# Controling Basic

Add-on modul **Sada rozšíření pro Finance** obsahuje společné funkce pro podporu fungování ostatních add-on modulů balíčku rozšíření financí a současně obsahuje některé doplňující funkce jako:

- **Credit Check** – napojení na externí databázi Credit Check a kontrola kredibility firem
- **Splátkové kalendáře** – rozložení splátek pohledávek a závazků do dílčích plateb
- **Hierarchický návrh cen** – možnost vypnutí standardního návrhu nejnižších cen
- **Vymáhání pohledávek** - podpora pro vymáhání dlouhodobých pohledávek, které dosud nebyly uhrazeny. U takových pohledávek je potřeba mít především informaci o stavu pohledávky a mít možnost připojit dokumenty.
- **PDP** – Režim Přenesené daňové povinnosti – doplnění kontrol limitů při vydávání dokladů.
- **Skonto dobropisy pro CZ**
- **Kumulování plateb na Platebním příkazu**
- **Účtování přeplatků nákupních záloh**
- **Kontrola registrace k DPH**
- **Kontroly směnných kursů**
- **Viditelný poplatek** - Možnost ke zboží přiřadit tzv. "viditelný poplatek", který se automaticky vkládá do nákupních/prodejních dokladů. Využívá se např. pro účtování poplatku za recyklaci el. odpadu, apod.
- **Spotřební daň** - Povinnost přiznat spotřební daň vzniká výdejem z daňového skladu – prodej v rámci ČR, interní transfer v rámci ČR. Jednou měsíčně je třeba vykázat splatnou spotřební daň. Na položkách zboží je informace o spotřební dani a o povinnosti daň přiznat. Je k dispozici report, který uzavírá otevřené položky spotřební daně. Dále je k dispozici report z žurnálu poskytující podklad pro Prohlášení o spotřební dani.
- Další menší úpravy či vylepšení vybraných oblastí (finance, sklady, obecné, atd.)

Modul Sada rozšíření pro Finance je nutný pro ostatní add-on moduly AC Financial Packu.

## Credit Check

Jedná se o integraci BC na komerční službu CreditCheck, která slouží pro kontrolu bonity partnerů. 

Proto, aby v systému bylo co nejvíce informací o vybraném partnerovi, jsou informace importovány přes webovou službu Creditcheck ERP viz. http://www.creditcheck.cz/ProductDetail.aspx?id=02. 

Společnost CreditCheck deklaruje, že každý den ve své databázi českých firem provádí 185 různých typů kontrol. Služba Creditcheck ERP je zdarma stejně tak jako vytvoření výpisu CreditcheckList. V databázi Creditcheck lze tedy prověřovat partnera bez přihlášení. V případech, kdy je u firmy nalezen oranžový nebo červený semafor je potřeba se pro prohlédnutí detailů přihlásit. Toto je placená služba, kterou si zákazník dle své potřeby uzavře s CreditCheck. 

### Stav CreditCheck 

Stažené informace o bonitě zákazníka CreditCheck ERP (do bonity patří i info o nespolehlivém plátci DPH) jsou na kartě dodavatele zobrazeny v Informačním okně Hodnocení dodavatele. 

> [!NOTE]
> Pro zobrazení informačního okna použijte funkci přizpůsobit. 

### Spuštění webových zdrojů 

Spuštění webových zdrojů kontaktu je nyní umožněno také na kartě dodavatele/zákazníka a také na souvisejících dokladech (nabídka, objednávka, faktura, pokladní doklad, příkaz k úhradě). Spuštění se provede kliknutím na ikonu stavu CreditCheck (semafor). Zobrazí se tento formulář: 

![Spuštění webových zdrojů](media/credit_check.png)

### Zrušení stavu CreditCheck 

Jestliže má uživatel v nastavení zaškrtnut  boolean „*Povolit změnu stavu CreditCheck*“ pak na kartě kontaktu může pomocí funkce „Zrušit stav CreditCheck“ provést zrušení naimportovaného stavu. Důvodem může být to, že si uživatel tohoto partnera zkontroloval a problém pro který má uvedený tento stav, nepovažuje za důležité, proto provede jeho zrušení. 


> [!WARNING]
> Uvedená změna je nevratná a změna stavu CreditCheck (nové označení) se provede pouze v případě, že u uvedeného partnera byl zjištěn nový problém. Např. že se nyní dostal navíc i do insolvenčního řízení. 


## Hierarchický návrh cen 

Standardní prodejní cenotvorba je založena na myšlence vyhledání nejnižší možné ceny. Toto není vždy vyhovující, pak je možné zvolit tzv. Hierarchický návrh cen. 

Poznámka: Hierarchický návrh je dostupný pouze prodejní ceny zboží. 

Hierarchický návrh ceny znamená, že je cena (ale i řádková sleva) dohledávána v pevně definovaném pořadí (dle hierarchie). V případě nalezení definice na učité úrovni již nehledá dále. 

**Prodejní ceny** systém dohledává v následujícím pořadí: 
1. Kampaň 
2. Zákazník 
3. Cenová skupna zákazníka 
4. Všichni zákazníci 

**Prodejní řádkové slevy** systém dohledává v následujícím pořadí: 
1. Kampaň a Zboží 
2. Kampaň a Cenová skupina zboží 
3. Zákazník a Zboží 
4. Cenová skupna zákazníka a Zboží 
5. Všichni zákazníci a Zboží 
6. Zákazník a Cenová skupina zboží 
7. Cenová skupina zákazníka a Cenová skupina zboží
8. Všichni zákazníci a Cenová skupina zboží 

## Platení kalendáře 

Funkcionalita Platebních kalendářů je k dispozici v prodeji i v nákupu a její fungování je v obou oblastech obdobné.  Platební kalendář je možné definovat na neúčtovaném dokladu, ale i dodatečně na zaúčtovaném dokladu v měnu dokladu. 

**Účtování prodejní faktury s platebním kalendářem**

1. Vyberte ikonu ![Žárovky, která otevře funkci Řekněte mi](media/ui-search/search_small.png "Řekněte mi, co chcete dělat"), zadejte **Prodejní faktur** a poté vyberte související odkaz. 
2. Vytvořte novou prodejní fakturu dle vašich zvyklostí. V poli **Datum splatnosti** definujte nejzašší datum pro platební kalendář. 
3. Spusťte akci **Platební kalendář**. 
4. Spusťte funkci **Generovat platby**. 
5. Definujte počet dílčích plateb a systém dopočte pole s částkami plateb. Poslední platbu systém dopočte do celkové výše faktury. 
6. Doplňte **Datum splatnosti** první platby a datumový vzorec do pole Perioda plateb. 
7. Tlačítkem **OK** spusťe generování návrhu platebního kalendáře. 
8. Vytvořený platební kalendář můžete ještě ručně upravit. 
9. Tlačítkem **OK** zavřete stránku. 
10. Na prodejní faktuře spusťte funkci **Účtovat**. 

![Splátkový kalendář](media/calendar.png)

Po zaúčtování prodejní faktury (či objednávky) vzniknou navíc položky zákazníka, které vyrovnají saldo původní položky a k nim vznikne několik nových (se stejným typem dokladu, číslem dokladu, atd.) pohledávek s daty splatnosti a částkami dle platebního kalendáře. 

> [!NOTE]
> Na prodejním dokladu je přítomnost platebního kalendáře indikovánan příznakem Platební kalendář v okně s fakty Detaily prodejní hlavičky. Kliknutím na Ano se příslušný kalendář otevře. 

![Detail platebního kalendáře](media/calendar_detail.png)

**Vytvoření platebního kalendáře k zaúčtované faktuře**

1. Vyberte ikonu ![Žárovky, která otevře funkci Řekněte mi](media/ui-search/search_small.png "Řekněte mi, co chcete dělat"), zadejte **Účtované prodejní faktury** a poté vyberte související odkaz. 
2. Spusťte akci **Platební kalendář**.
3. V řádcích definujte vlastní rozpis splátek. 
4. Vyrovnejte zůstatek faktury a zaúčtujte platební kalendář funkcí **Účtovat**. 

## Kumulování plateb na platebním příkazu 

Funkcionalita umožňuje sloučení řádků platebního příkazu, což je vhodné, pokud je potřeba uhradit více nákupních dokladů jednou částkou. Kumuluje se podle Čísla účtu, SWIFT, IBAN, Měny a volitelně dle VS, KS a SS.  

Tato funkcionalita slučuje řádky plateb pro dodavatele, kteří mají povoleno kumulovat platby, dle pravidel nastavených na bankovním účtu. Další informace naleznete v Nastavení kumulování plateb. 

**Vytvoření platebního příkazu s kumulací plateb**

1. Vyberte ikonu ![Žárovky, která otevře funkci Řekněte mi](media/ui-search/search_small.png "Řekněte mi, co chcete dělat"), zadejte **Platební příkazy** a poté vyberte související odkaz. 
2. Vyberte číslo banky s nastavenou kumulací plateb, pro který chcete vytvořit platební příkaz a potvrďte tlačítkem **OK**.
3. Spusťte akci **Navrhni platby…** (alternativou je ruční zadání řádků příkazu, popř. funkce Import…)
4. Doplňte **Poslední datum splatnosti** a **Částku k dispozici**, popř. upravte další parametry. 
5. Tlačítkem **OK** spusťe generování návrhu plateb. 
6. Vytvořený platební příkaz můžete ještě ručně upravit (pro ověření funkcionality kumulace plateb zkontrolujte, že máte v řádcích více plateb na stejný účet dodavatele se zapnutou kumulací plateb) 
7. Na platebním příkazu spusťte funkci **Vydání**. 
8. Tlačítkem **OK** potvrďte volbu Vydat. 
9. Volbou  **Ano** potvrďte otevření karty vydaného platebního příkazu. 
10. Na vydaném platebním příkazu spusťte funkci **Vytvořit řádky exportu**. 
11. Volbou **Řádky exportu** otevřete seznam řádků exportu. Neslučované položky jsou převedeny do řádků exportu platebního příkazu ve stejném detailu. Pokud chcete změnit výsledek, změňte nastavení a funkci pro vytvoření řádků spusťte znovu. 
12. Spusťte akci **Export platebního příkazu…** (alternativou je ruční zadání řádků příkazu, popř. funkce Import…) 

> [!NOTE]
> Pokud se nekumuluje dle symbolů, tak se sloučené řádky založí s variabilním symbolem z číselné řady a SS a KS se vezmou z prvního slučovaného řádku příkazu. Datum splatnosti se vezme ten nejnižší ze slučovaných řádků. 

**Kumulované platby na bankovním výpisu**

Proces zpracování výpisu je z pohledu uživatele beze změn. Rozdíl je pouze v tom, že při Vydání systém hledá dle identifikačních údajů pohybu na řádku výpisu odpovídající záznamy na vydaném platebním příkazu v řádcích exportu. Pokud najde, na pozadí dojde k nahrazení „kumulovaných plateb“ opět rozdělenými řádky (je přenesen i původní kumulovaný řádek, ovšem s nulovou částkou). 

[Controling Basic](ac-controling-basic-setup.md)  
[Financial Pack](ac-finance-pack.md)  
