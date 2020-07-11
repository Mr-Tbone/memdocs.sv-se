---
title: Skapa anpassade konfigurationsobjekt
titleSuffix: Configuration Manager
description: Hantera inställningar för Windows-datorer och-servrar med ett anpassat konfigurations objekt för Windows-datorer och-servrar
ms.date: 04/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 24637862326b029f974843c18ccba835ee5501ba
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240430"
---
# <a name="create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Skapa anpassade konfigurations objekt för Windows-datorer och serverdatorer som hanteras med Configuration Manager-klienten

*Gäller för: Configuration Manager (aktuell gren)*


Använd Configuration Manager anpassade konfigurations objekt för **Windows-skrivbordet och-servrar** för att hantera inställningar för Windows-datorer och-servrar som hanteras av Configuration Manager-klienten.  



## <a name="start-the-wizard"></a>Starta guiden

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** , **expanderar kompatibilitetsinställningar och**väljer noden **konfigurations objekt** .  

2. Välj **skapa konfigurations objekt**i gruppen **skapa** på fliken **Start** i menyfliksområdet.  

3. Ange ett namn och en valfri beskrivning för konfigurationsobjektet på sidan **Allmänt** i guiden **Skapa konfigurationsobjekt**.  

4. Välj **Windows-baserade datorer och servrar (anpassat)** under **Ange typen av konfigurationsobjekt som du vill skapa**.  

    > [!TIP]  
    > Om du vill ange inställningar för identifieringsmetoden som kontrollerar om ett program finns väljer du **Det här konfigurationsobjektet innehåller programinställningar**.  

5. Du kan hjälpa dig att söka efter och filtrera konfigurations objekt i Configuration Manager-konsolen genom att välja **Kategorier** för att skapa och tilldela kategorier.  



## <a name="detection-methods"></a>Identifierings metoder  

Följ stegen nedan om du vill ange information om identifieringsmetoden för konfigurationsobjektet.  

> [!NOTE]  
> Den här informationen gäller endast om du väljer **det här konfigurationsobjektet innehåller program inställningar** på sidan **Allmänt** i guiden.  

En identifierings metod i Configuration Manager innehåller regler som används för att identifiera om ett program har installerats på en dator. Den här identifieringen sker innan klienten bedömer kompatibiliteten för konfigurationsobjektet. Du kan kontrollera om ett program är installerat genom att leta efter en Windows Installer-fil för programmet, genom att använda ett anpassat skript eller genom att välja **Utgå alltid från att programmet är installerat** för att utvärdera konfigurationsobjektets kompatibilitet oavsett om programmet är installerat eller inte.  


### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Identifiera en programinstallation med hjälp av Windows Installer-filen  

1. På sidan **identifierings metoder** i **guiden skapa konfigurations objekt**väljer du alternativet att **använda Windows Installer identifiering**.  

2. Välj **Öppna**, bläddra till den Windows Installer fil (. msi) som du vill identifiera och välj sedan **Öppna**.  

3. Fältet **version** fylls i automatiskt med versions numret för den Windows Installer filen. Om värdet som visas är felaktigt anger du ett nytt versions nummer här.  

4. Om du vill identifiera varje användar profil på datorn väljer du **det här programmet installeras för en eller flera användare**.  


### <a name="to-detect-a-specific-application-and-deployment-type"></a>Så här identifierar du ett specifikt program och distributionstyp  

1. På sidan **identifierings metoder** i **guiden skapa konfigurations objekt**väljer du att **identifiera ett särskilt program och en distributions typ**. Välj **Välj**.   

2. Välj programmet och den associerade distributionstypen som du vill identifiera i dialogrutan **Ange program**.  


### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>Så här identifierar du en programinstallation med hjälp av ett anpassat skript  

1. På sidan **identifierings metoder** i **guiden skapa konfigurations objekt**väljer du alternativet för att **använda ett anpassat skript för att identifiera det här programmet**.  

2. Välj språk för skriptet i listan. Välj bland följande format:  

    - **VBScript**  

    - **JScript**  

    - **PowerShell**  

        > [!Note]  
        > Från och med version 1810, anropar den Configuration Manager klienten PowerShell med-parametern när ett Windows PowerShell-skript körs som en identifierings metod `-NoProfile` . Det här alternativet startar PowerShell utan profiler. En PowerShell-profil är ett skript som körs när PowerShell startar. <!--3607762-->  

3. Välj **Öppna**, bläddra till det skript som du vill använda och välj sedan **Öppna**.  



## <a name="specify-supported-platforms"></a>Ange plattformar som stöds  

På sidan **plattformar som stöds** i **guiden skapa konfigurations objekt**väljer du de Windows-versioner som du vill att konfigurationsobjektet ska utvärderas för efterlevnad, eller Välj **Markera alla**.

Du kan också **Ange Windows-versionen manuellt**. Välj **Lägg till** och ange varje del av Windows build-numret.

> [!NOTE]
> När du anger Windows Server 2016 `All Windows Server 2016 and higher 64-bit)` innehåller valet även Windows server 2019. Om du bara vill ange Windows Server 2016 använder du alternativet för att **Ange Windows Server version manuellt**. <!--5866480-->



##  <a name="configure-settings"></a>Konfigurera inställningar  

Följ stegen nedan om du vill konfigurera inställningarna i konfigurationsobjektet.  

Inställningarna representerar affärsvillkoren eller de tekniska kriterierna som används för att utvärdera kompatibiliteten på klientenheter. Du kan konfigurera en ny inställning eller bläddra till en befintlig inställning på en referensdator.  

1. På sidan **Inställningar** i **guiden skapa konfigurations objekt**väljer du **nytt**.  

2. Ange följande information fliken **Allmänt** i dialogrutan **Skapa inställning**:  

    - **Namn**: Ange ett unikt namn för inställningen. Använd högst 256 tecken.  

    - **Beskrivning**: Ange en beskrivning av inställningen. Använd högst 256 tecken.  

    - **Inställnings typ**: i listan väljer du och konfigurerar en av följande inställnings typer som ska användas för den här inställningen:  
        - [Active Directory-fråga](#bkmk_adquery)
        - [Sammansättning](#bkmk_assembly)
        - [Filsystem](#bkmk_file)
        - [IIS-metabas](#bkmk_iis)
        - [Register nyckel](#bkmk_regkey)
        - [Register värde](#bkmk_regval)
        - [Skript](#bkmk_script)
        - [SQL-fråga](#bkmk_sql)
        - [WQL-fråga](#bkmk_wql)
        - [XPath-fråga](#bkmk_xpath)

    - **Datatyp**: Välj det format som villkoret returnerar data i innan det används för att utvärdera inställningen. **Data typs** listan visas inte för alla inställnings typer.  

        > [!Tip]  
        > Data typen **svävande punkt** stöder endast tre siffror efter decimal tecknet.  

3. Konfigurera ytterligare information om den här inställningen under listan **Inställningstyp**. De objekt som du kan konfigurera varierar beroende på vilken inställnings typ du har valt.  

4. Välj **OK** för att spara inställningen och stänga dialog rutan **Skapa inställning** .  


### <a name="active-directory-query"></a><a name="bkmk_adquery"></a>Active Directory fråga

- **LDAP-prefix**: Ange ett giltigt prefix till Active Directory Domain Services-frågan för att utvärdera kompatibiliteten på klient datorer. Om du vill göra en global katalogs ökning använder du antingen `LDAP://` eller `GC://` .  

- **Unikt namn (DN)**: Ange det unika namnet på Active Directory Domain Services-objektet som utvärderas för kompatibilitet på klient datorer.  

- **Sök filter**: Ange ett valfritt LDAP-filter för att förfina resultatet från Active Directory Domain Services-frågan för att utvärdera kompatibiliteten på klient datorer. Om du vill returnera alla resultat från frågan anger du `(objectclass=*)` .  

- **Sök omfång**: Ange Sök omfånget i Active Directory Domain Services  

    - **Base**: frågar bara det angivna objektet  

    - **En nivå**: det här alternativet används inte i den här versionen av Configuration Manager  

    - Under **träd**: frågar det angivna objektet och dess fullständiga under träd i katalogen  

- **Egenskap**: ange egenskapen för Active Directory Domain Services-objektet som används för att utvärdera kompatibiliteten på klient datorerna.  

    Om du till exempel vill fråga Active Directory-egenskapen som lagrar antalet gånger som en användare felaktigt anger ett lösen ord anger du `badPwdCount` i det här fältet.  

- **Fråga**: visar frågan som skapats från posterna i **LDAP-prefix**, **unikt namn (DN)**, **Sök filter** (om det angetts) och **egenskap**.  


### <a name="assembly"></a><a name="bkmk_assembly"></a>Paket

En sammansättning är ett stycke kod som flera program kan dela på. Sammansättningar kan ha filnamnstillägget .dll eller .exe. Global Assembly Cache är mappen `%SystemRoot%\Assembly` på klient datorer. I det här cacheminnet lagras alla delade sammansättningar i Windows.  

- **Sammansättningsnamn:** Anger namnet på sammansättningsobjektet som du vill söka efter. Namnet får inte vara samma som andra sammansättnings objekt av samma typ. Registrera den först i den globala sammansättningscachen. Sammansättningsnamnet får innehålla högst 256 tecken.  


### <a name="file-system"></a><a name="bkmk_file"></a>Fil system

- **Skriv**: i listan väljer du om du vill söka efter en **fil** eller **mapp**.  

- **Sökväg**: Ange sökvägen till den angivna filen eller mappen på klient datorerna. Du kan ange systemmiljövariabler och `%USERPROFILE%` miljö variabeln i sökvägen.  

    > [!NOTE]  
    > Om du använder `%USERPROFILE%` miljövariabeln i rutorna **sökväg** eller **fil-eller mappnamn** söker Configuration Manager klienten igenom alla användar profiler på klient datorn. Det här beteendet kan leda till att det hittar flera instanser av filen eller mappen.  
    >   
    > Om kompatibilitetsinställningar inte har åtkomst till den angivna sökvägen genereras ett identifierings fel. Om den fil som du söker efter används för närvarande genereras dessutom ett identifieringsfel.  

    > [!Tip]  
    > Välj **Bläddra** för att konfigurera inställningen från värden på en referens dator.   

- **Fil-eller mappnamn**: Ange namnet på filen eller objektet som du vill söka efter. Du kan ange systemmiljövariabler och `%USERPROFILE%` miljövariabeln i fil-eller mappnamnet. Du kan också använda jokertecken `*` och `?` i fil namnet.  

    > [!NOTE]  
    > Om du anger ett fil-eller mappnamn och använder jokertecken kan den här kombinationen resultera i ett stort antal resultat. Det kan också leda till hög resursanvändning på klient datorn och hög nätverks trafik när resultatet rapporteras till Configuration Manager.  

- **Ta med undermappar**: Sök också i alla undermappar under den angivna sökvägen.  

- **Den här filen eller mappen är associerad med ett 64-bitars program**: om alternativet är aktiverat genomsöker du bara 64-bitars fil platser som `%ProgramFiles%` på 64-bitars datorer. Om det här alternativet inte är aktiverat kan du söka i både 64-bitars platser och 32-bitars platser, till exempel `%ProgramFiles(x86)%` .  

    > [!NOTE]  
    > Om samma fil eller mapp finns på platser för både 64- och 32-bitars systemfiler på samma 64-bitarsdator returneras flera filer av det globala villkoret.  

    Inställnings typen **fil system** stöder inte att du anger en UNC-sökväg till en nätverks resurs i rutan **sökväg** .  


### <a name="iis-metabase"></a><a name="bkmk_iis"></a>IIS-metabas

- **Metabassökväg**: Ange en giltig sökväg till den Internet Information Services (IIS) metabasen. Ett exempel är `/LM/W3SVC/`.  

- **Egenskaps-ID**: ange egenskapen numeric för inställningen IIS-metabasen.  


### <a name="registry-key"></a><a name="bkmk_regkey"></a>Register nyckel

- **Hive**: Välj den registrerings data fil som du vill söka i

    > [!Tip]  
    > Välj **Bläddra** för att konfigurera inställningen från värden på en referens dator. Aktivera **Remote Registry** -tjänsten på fjärrdatorn om du vill bläddra till en register nyckel på en fjärrdator.  

- **Nyckel**: Ange det register nyckel namn som du vill söka efter. Använd formatet `key\subkey`.  

- **Den här register nyckeln är associerad med ett 64-bitars program**: sök efter 64-bitars register nycklar utöver de 32-bitars register nycklarna på klienter som kör en 64-bitars version av Windows.  

    > [!NOTE]  
    > Om samma registernyckel finns både i 64- och 32-bitarsregistret på samma 64-bitarsdator hittas båda registernycklarna genom det globala villkoret.  


### <a name="registry-value"></a><a name="bkmk_regval"></a>Register värde

- **Hive**: Välj den registrerings data fil som du vill söka i.  

    > [!Tip]  
    > Välj **Bläddra** för att konfigurera inställningen från värden på en referens dator. Aktivera **Remote Registry** -tjänsten på fjärrdatorn för att bläddra till ett register värde på en fjärrdator. Du måste också ha administratörs behörighet för att få åtkomst till fjärrdatorn.  

- **Nyckel**: Ange det register nyckel namn som du vill söka efter. Använd formatet `key\subkey`.  

- **Värde**: Ange det värde som måste finnas i den angivna register nyckeln.  

- **Den här register nyckeln är associerad med ett 64-bitars program**: sök i 64-bitars register nycklar utöver de 32-bitars register nycklarna på klienter som kör en 64-bitars version av Windows.  

    > [!NOTE]  
    > Om samma registernyckel finns både i 64- och 32-bitarsregistret på samma 64-bitarsdator hittas båda registernycklarna genom det globala villkoret.  


### <a name="script"></a><a name="bkmk_script"></a>Över

Värdet som skriptet returnerar används för att utvärdera kompatibiliteten för det globala villkoret. Om du till exempel använder VBScript kan du använda kommandot **WScript.Echo Result** för att returnera värdet på variabeln *Resultat* värdet till det globala villkoret.  

- **Identifierings skript**: Välj **Lägg till skript**och ange eller bläddra till ett skript. Det här skriptet används för att hitta värdet. Du kan använda Windows PowerShell-, VBScript- eller Microsoft JScript-skript.  

- **Reparations skript (valfritt)**: Välj **Lägg till skript**och ange eller bläddra till ett skript. Det här skriptet används för att reparera icke-kompatibla inställnings värden. Du kan använda Windows PowerShell-, VBScript- eller Microsoft JScript-skript.  

- **Kör skript med hjälp av autentiseringsuppgifterna för den inloggade användaren**: om du aktiverar det här alternativet körs skriptet på klient datorer som använder autentiseringsuppgifterna för den inloggade användaren.  

> [!Note]  
> Från och med version 1810, när du använder Windows PowerShell som ett identifierings-eller reparations skript, anropar Configuration Manager klienten PowerShell med `-NoProfile` parametern. Det här alternativet startar PowerShell utan profiler. En PowerShell-profil är ett skript som körs när PowerShell startar. <!--3607762-->  


### <a name="sql-query"></a><a name="bkmk_sql"></a>SQL-fråga

- **SQL Server instans**: Välj om du vill att SQL-frågan ska köras på standard instansen, alla instanser eller ett angivet databas instans namn.  

    > [!NOTE]  
    > Instansnamnet måste gälla en lokal instans av SQL Server. Du bör använda ett skript om du vill referera till en klustrad instans av SQL Server.  

- **Databas**: Ange namnet på den Microsoft SQL Server databas som du vill köra SQL-frågan mot.  

- **Kolumn**: Ange kolumn namnet som returneras av Transact-SQL-instruktionen som används för att utvärdera kompatibiliteten för det globala villkoret.  

- **Transact-SQL-uttryck**: Ange den fullständiga SQL-fråga som du vill använda för det globala villkoret. Om du vill använda en befintlig SQL-fråga väljer du **Öppna**.  

    > [!IMPORTANT]  
    > SQL-frågeinställningar stöder inte SQL-kommandon som ändrar databasen. Du kan bara använda SQL-kommandon som läser information från databasen.  


### <a name="wql-query"></a><a name="bkmk_wql"></a>WQL-fråga

- **Namnrymd**: Ange det WMI-namnområde som bedömer kompatibiliteten på klient datorerna. Standardvärdet är `root\cimv2`.  

- **Klass**: Ange mål-WMI-klassen i namn området ovan.  

- **Egenskap**: Ange mål-WMI-egenskapen i ovanstående klass.  

- **WQL-fråga WHERE-sats**: Ange en kvalificerings sats för att minska resultatet. Om du till exempel bara vill skicka frågor till DHCP-tjänsten i klassen Win32_Service kan WHERE-satsen vara `Name = 'DHCP' and StartMode = 'Auto'` .   


### <a name="xpath-query"></a><a name="bkmk_xpath"></a>XPath-fråga

- **Sökväg**: Ange sökvägen till XML-filen på klient datorer som används för att utvärdera kompatibiliteten. Configuration Manager stöder användningen av alla variabler i Windows-systemmiljön och `%USERPROFILE%` användar variabeln i Sök vägs namnet.  

- **XML-fil namn**: Ange fil namnet som innehåller XML-frågan i ovanstående sökväg.  

- **Inkludera undermappar**: aktivera det här alternativet om du vill söka i alla undermappar under den angivna sökvägen.  

- **Den här filen är associerad med ett 64-bitars program**: Sök efter platsen för 64-bitars system filen, `%Windir%\System32` förutom den plats för 32-bitars system `%Windir%\Syswow64` som finns på Configuration Manager klienter som kör en 64-bitars version av Windows.  

- **XPath-fråga**: Ange en giltig fullständig XPath-fråga (XML Path Language).  

- **Namn områden**: identifiera namn områden och prefix som ska användas i XPath-frågan.  

Om du försöker identifiera en krypterad XML-fil hittar kompatibilitetsinställningar filen, men XPath-frågan ger inga resultat. Den Configuration Manager klienten genererar inget fel.  

Om XPath-frågan inte är giltig utvärderas inställningen som inkompatibel på klient datorer.  



##  <a name="configure-compliance-rules"></a>Konfigurera kompatibilitetsregler  

Kompatibilitetsregler anger villkoren som definierar ett konfigurationsobjekts kompatibilitet. Innan kompatibiliteten för en inställning kan utvärderas måste den ha minst en kompatibilitetsregel. Med WMI-, register- och skriptinställningar kan du justera värden som inte är kompatibla. Du kan skapa nya regler eller bläddra till en befintlig inställning i ett konfigurationsobjekt och välja regler i det.  


### <a name="to-create-a-compliance-rule"></a>Så här skapar du en kompatibilitetsregel  

1. På sidan **regler för efterlevnad** i **guiden skapa konfigurations objekt**väljer du **nytt**.  

2. Ange följande information i dialogrutan **Skapa regel**:  

    - **Namn**: Ange ett namn för regeln för efterlevnad.  

    - **Beskrivning**: Ange en beskrivning av regeln för efterlevnad.  

    - **Vald inställning**: Välj **Bläddra** för att öppna dialog rutan **Välj inställning** . Välj den inställning som du vill definiera en regel för eller Välj **ny inställning**. När du är klar väljer du **Välj**.  

        > [!Tip]  
        > Om du vill visa information om den markerade inställningen väljer du **Egenskaper**.  

    - **Regeltyp**: Välj den typ av efterlevnadsprincip som du vill använda:  

        - **Värde**: skapa en regel som jämför värdet som returneras av konfigurationsobjektet med ett värde som du anger. Mer information om ytterligare inställningar finns i [värde regler](#bkmk_value).  

        - **Existentiell**: skapa en regel som utvärderar inställningen beroende på om den finns på en klienten het eller på antalet gånger som den hittas. Mer information om ytterligare inställningar finns i existentiell- [regler](#bkmk_exist).  

3. Stäng dialog rutan **Skapa regel** genom att klicka på **OK** .  




### <a name="value-rules"></a><a name="bkmk_value"></a>Värde regler  

- **Egenskap**: egenskapen för det objekt som ska kontrol leras varierar beroende på den valda inställningen. Vilka egenskaper som är tillgängliga beror på vilken typ av inställning som används. 

- **Inställningen måste vara kompatibel med följande...**: tillgängliga regler eller behörigheter varierar beroende på typen av inställning.

- **Reparera inkompatibla regler när stöd stöds**: Välj det här alternativet för Configuration Manager att reparera icke-kompatibla regler automatiskt. Configuration Manager stöder den här åtgärden med följande regel typer:  

    - **Register värde**: om det inte är kompatibelt anger klienten registervärdet. Om den inte finns skapar klienten värdet.  

    - **Skript**: klienten använder det reparations skript som du angav med inställningen.  

    - **WQL-fråga**  

    > [!IMPORTANT]  
    > Du kan bara reparera inkompatibla regler när regeloperatorn har värdet **Lika med**.  

- **Rapportera inkompatibilitet om den här inställnings instansen inte hittas**: om den här inställningen inte hittas på klient datorer aktiverar du det här alternativet för konfigurationsobjektet för att rapportera inkompatibilitet.  

- **Allvarlighets grad för inkompatibilitet för rapporter**: Ange allvarlighets graden som rapporteras i Configuration Manager rapporter om denna efterlevnadsprincip inte fungerar. Följande allvarlighets grader är tillgängliga:  
    - **Ingen**  
    - **Information**  
    - **Varning**  
    - **Kritisk**  
    - **Kritisk med händelse**: datorer som inte uppfyller den här regeln rapporterar allvarlighets graden **kritisk**. Allvarlighetsgraden registreras även som en Windows-händelse i programhändelseloggen.  


### <a name="existential-rules"></a><a name="bkmk_exist"></a>Existentiell-regler 

> [!NOTE]  
> De alternativ som visas kan variera beroende på vilken inställnings typ du konfigurerar en regel för.  

- **Inställningen måste finnas på klientenheter**  

- **Inställningen får inte finnas på klientenheterna**  

- **Inställningen sker följande antal gånger:**  

- **Allvarlighets grad för inkompatibilitet för rapporter**: Ange allvarlighets graden som rapporteras i Configuration Manager rapporter om denna efterlevnadsprincip inte fungerar. Följande allvarlighets grader är tillgängliga:  
    - **Ingen**  
    - **Information**  
    - **Varning**  
    - **Kritisk**  
    - **Kritisk med händelse**: datorer som inte uppfyller den här regeln rapporterar allvarlighets graden **kritisk**. Allvarlighetsgraden registreras även som en Windows-händelse i programhändelseloggen.  


## <a name="track-configuration-item-remediations"></a><a name="bkmk_track"></a>Spåra reparationer av konfigurations objekt
<!--4261411-->
*(Lanseras i version 2002)*

Från och med Configuration Manager version 2002 kan du **spåra reparations historiken när den stöds** i dina efterlevnadsprinciper för konfigurations objekt. När det här alternativet är aktiverat genererar alla åtgärder som sker på klienten för konfigurationsobjektet ett tillstånds meddelande. Historiken lagras i Configuration Manager databasen.

Bygg anpassade rapporter för att Visa reparations historiken med hjälp av den offentliga vyn **v_CIRemediationHistory**. `RemediationDate`Kolumnen är den tid, i UTC, som klienten körde reparationen. `ResourceID`Identifierar enheten. Genom att skapa anpassade rapporter i vyn **v_CIRemediationHistory** kan du:

- Identifiera möjliga problem med dina reparations skript
- Hitta trender i reparationer, till exempel en klient som är konsekvent inkompatibel med varje utvärderings cykel.

### <a name="enable-the-track-remediation-history-when-supported-option"></a>Aktivera spårnings historiken för spår när alternativ stöds

- För nya konfigurations objekt lägger du till **spårnings historiken spåra när stöd** finns på fliken **regler för efterlevnad** när du skapar en ny inställning på guidens **inställnings** sida.
- För befintliga konfigurations objekt lägger du till **spårnings historiken spåra när stöd** finns på fliken **efterlevnadsprinciper** i **egenskaperna**för konfigurations objekt.
[![Spåra reparations historiken när den stöds i version 2002](./media/4261411-remediation-history.png)](./media/4261411-remediation-history.png#lightbox)

## <a name="next-steps"></a>Nästa steg

[Skapa konfigurationsbaslinjer](create-configuration-baselines.md)
