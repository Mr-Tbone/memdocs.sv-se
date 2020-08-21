---
title: Skapa frågor
titleSuffix: Configuration Manager
description: Upptäck hur du skapar och importerar frågor i Configuration Manager. Innehåller exempel frågor och tips.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d15252c3b3c93c7e90e517c502c4c3dd2dfcf20
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700052"
---
# <a name="create-queries-in-configuration-manager"></a>Skapa frågor i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

I den här artikeln beskrivs hur du skapar och importerar frågor i Configuration Manager.  

##  <a name="create-a-query"></a><a name="BKMK_Create"></a> Skapa en fråga  
 Använd den här proceduren för att skapa en fråga i Configuration Manager.  

1.  I Configuration Manager-konsolen väljer du **övervakning**.  

2.  I arbets ytan **övervakning** väljer du **frågor**. På fliken **Start** går du till gruppen **skapa** och väljer **Skapa fråga**.  

3.  På fliken **Allmänt** i **guiden Skapa fråga**anger du ett unikt namn och eventuellt en kommentar för frågan.  

4.  Om du vill importera en befintlig fråga och använda den som grund för den nya frågan väljer du **Importera frågeuttryck**. I dialog rutan **Bläddra efter fråga** väljer du en fråga som du vill importera och väljer sedan **OK**.  

5.  I listan **objekt typ** väljer du den typ av objekt som du vill att frågan ska returnera. I den här tabellen beskrivs några exempel på de typer av objekt som du kan söka efter:  

    |Objekttyp|Beskrivning|  
    |-----------------|-----------------|  
    |**Systemresurs**|Använd om du vill söka efter vanliga systemattribut, t. ex. NetBIOS-namnet på en enhet, klient versionen, klientens IP-adress och Active Directory Domain Services information.|  
    |**Användarresurs**|Använd för att söka efter typisk användar information, t. ex. användar namn, användar grupp namn och namn på säkerhets grupper.|  
    |**Distribution**|Använd om du vill söka efter vanliga attribut för en distribution, t. ex. distributions namn, schema och den samling som den distribuerades till.|  

6.  Välj **Redigera frågeuttryck** för att öppna &lt; dialog rutan Egenskaper för frågans namns \> **instruktion** .  

7.  På fliken **Allmänt** i &lt; dialog rutan Egenskaper för frågans namn \> **instruktion** anger du de attribut som frågan returnerar och hur de ska visas. Välj ikonen **ny** om du vill lägga till ett nytt attribut. Du kan också välja **Visa frågespråk** för att ange eller redigera frågan direkt i WMI Query Language (WQL). Exempel på WMI-frågor finns i avsnittet [exempel på WQL-frågor](#BKMK_Example) i den här artikeln.  

    > [!TIP]  
    > Du kan använda följande referens dokumentation som hjälp för att skapa egna WQL-frågor:  
    >   
    > -   [WQL (SQL för WMI)](/windows/win32/wmisdk/wql-sql-for-wmi)  
    > -   [WHERE-sats](/windows/win32/wmisdk/where-clause)  
    > -   [WQL-operatorer](/windows/win32/wmisdk/wql-operators)  

8.  På fliken **villkor** i &lt; \> dialog rutan **Egenskaper** för frågeuttryck anger du villkor som används för att förfina frågeresultatet. Du kan till exempel bara returnera resurser som har plats koden **XYZ**. Du kan konfigurera flera villkor för en fråga.  

    > [!IMPORTANT]  
    > Om du skapar en fråga som inte innehåller några villkor returnerar frågan alla enheter i samlingen **Alla system** .  

9. På fliken **kopplingar** i &lt; dialog rutan Egenskaper för frågans namn \> **instruktion** kan du kombinera data från två olika attribut i frågeresultatet. Även om Configuration Manager automatiskt skapar frågor till kopplingar när du väljer olika attribut för frågeresultatet, innehåller fliken **kopplingar** fler avancerade alternativ. Configuration Manager stöder dessa attribut klasser:  

    |Kopplingstyp|Beskrivning|  
    |---------------|-----------------|  
    |Inre|Visar endast matchande resultat. Används alltid av kopplingar som skapas automatiskt.|  
    |Vänster|Visar alla resultat för basattributet och endast matchande resultat för kopplingsattributet.|  
    |Höger|Visar alla resultat för attributet Join och endast matchande resultat för basattributet.|  
    |Fullständig|Visar alla resultat för både attributet base och attributet Join.|  

     Mer information om hur du använder kopplings åtgärder finns i SQL Server-dokumentationen.  

10. Välj **OK** för att stänga &lt; dialog rutan Egenskaper för frågans namn \> **uttryck** .  

11. På fliken **Allmänt** i **guiden Skapa fråga**anger du att frågeresultatet inte är begränsat till medlemmarna i en samling, att de är begränsade till medlemmarna i en angiven samling, eller att en fråga för en samling visas varje gången frågan körs.  

12. Skapa frågan genom att slutföra guiden. Den nya frågan visas på noden **frågor** på arbets ytan **övervakning** .  

##  <a name="import-a-query"></a><a name="BKMK_Import"></a> Importera en fråga  
 Använd den här proceduren för att importera en fråga till Configuration Manager. Information om hur du exporterar frågor finns i [hantera frågor](../../../core/servers/manage/manage-queries.md).  

1.  I Configuration Manager-konsolen väljer du **övervakning**.  

2.  I arbets ytan **övervakning** väljer du **frågor**. På fliken **Start** går du till gruppen **skapa** och väljer **Importera objekt**.  

3.  På sidan **namn på MOF-fil** i **guiden Importera objekt**väljer du **bläddra** för att välja den Managed Object Format (MOF) som innehåller den fråga som du vill importera.  

4.  Granska informationen om frågan som ska importeras och slutför sedan guiden. Den nya frågan visas på noden **frågor** på arbets ytan **övervakning** .  

##  <a name="example-wql-queries"></a><a name="BKMK_Example"></a> Example WQL queries

Det här avsnittet innehåller exempel på WQL-frågor som du kan använda i din-hierarki eller ändra för andra orsaker. Om du vill använda dessa frågor väljer du **Visa frågespråk** i dialog rutan **Egenskaper för frågeuttryck** . Kopiera och klistra sedan in frågan i fältet **frågeuttryck** .  

> [!TIP]  
> Använd jokertecknet `%` för en obestämd teckensträng. Returnerar till exempel `%Visio%` Microsoft Office Visio 2010.  

### <a name="computers-that-run-windows-10"></a>Datorer som kör Windows 10

Använd följande fråga om du vill returnera NetBIOS-namnet och operativsystemversionen för alla datorer som kör Windows 7.  

``` WQL
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from
SMS_R_System where
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 10%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Datorer som har ett särskilt programvarupaketet installerat  

Använd följande fråga om du vill returnera NetBIOS-namnet och programvarupaketet för alla datorer som har en specifikt programvarupaket installerat. Det här exemplet returnerar alla datorer med en version av Microsoft Visio installerad. Ersätt `Microsoft%Visio%` med det program varu paket som du vill fråga efter.  

> [!TIP]  
> Den här frågan söker efter programpaketet med hjälp av namnen som visas i programlistan på Kontrollpanelen i Windows.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =
SMS_R_System.ResourceId where
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Microsoft%Visio%"  
```  

### <a name="computers-in-a-specific-active-directory-domain-services-organizational-unit"></a>Datorer i en angiven organisations enhet för Active Directory Domain Services

Använd följande fråga om du vill returnera NetBIOS-namnet och organisationsenhets namnet för alla datorer i en angiven ORGANISATIONSENHET. Ersätt texten `OU Name` med namnet på den organisationsenhet som du vill fråga efter.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_R_System.SystemOUName from
SMS_R_System where
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Datorer med ett visst NetBIOS-namn

Använd följande fråga om du vill returnera NetBIOS-namnet på alla datorer som börjar med en specifik sträng med tecken. I det här exemplet returnerar frågan alla datorer med ett NetBIOS-namn som börjar med `ABC` .  

``` WQL
select SMS_R_System.NetbiosName from
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="devices-of-a-specific-type"></a><a name="BKMK_DeviceType"></a> Enheter av en viss typ.

Enhets typer lagras i Configuration Manager-databasen under resurs klassen **SMS_R_System** och attributnamnet **AgentEdition**. Använd den här frågan om du bara vill hämta de enheter som matchar agent versionen av den enhets typ som du anger:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Använd något av följande värden för &lt; enhets-ID \> :  

|Enhetstyp|Värde för AgentEdition|  
|-----------------|---------------------------|  
|Stationär eller bärbar dator i Windows|0|  
|Windows ARM-baserad enhet (som kör Windows RT)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Mac-dator|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|Intel-system på ett chip|12|  
|UNIX- och Linux-servrar|13|  
|Microsoft HoloLens (MDM)|15|
|Microsoft Surface Hub (MDM)|16|

> [!NOTE]
> Värden som inte finns med i den här tabellen är kopplade till enheter som inte längre stöds.

<!-- removed with hybrid EOL
|iOS|8|  
|iPad|9|  
|iPod touch|10|  
|Android|11|  
|Apple macOS (MDM)|14|
|Android for Work|17|
 -->

Om du till exempel bara vill returnera Mac-datorer använder du den här frågan:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="next-steps"></a>Nästa steg

[Hantera frågor](manage-queries.md)