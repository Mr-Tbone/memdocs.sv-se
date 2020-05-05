---
title: Teknisk för hands version 1801 | Microsoft Docs
titleSuffix: Configuration Manager
description: Lär dig mer om de funktioner som finns i teknisk för hands version 1801 för Configuration Manager.
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5a352ae0-355f-4fcf-b863-fb0654f51c52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e1e83126748596d9d631caa85506f7b236bf4a76
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074222"
---
# <a name="capabilities-in-technical-preview-1801-for-configuration-manager"></a>Funktioner i Technical Preview 1801 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1801. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats. 

Granska [teknisk för hands version för Configuration Manager](technical-preview.md) innan du installerar den här versionen av Technical Preview. Den artikeln är bekant med de allmänna kraven och begränsningarna för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Kända problem i den här tekniska för hands versionen:**
- **Uppdatering till en ny för hands version Miss lyckas när du har en plats server i passivt läge**. Om du har en [primär plats server i passivt läge](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)måste du avinstallera plats servern för passivt läge innan du uppdaterar till den nya för hands versionen. Du kan installera om den passiva läges plats servern efter att platsen har slutfört uppdateringen.

  Så här avinstallerar du plats servern för passivt läge:
  1. I Configuration Manager-konsolen går du till **Administration** > **Översikt** > **plats konfigurations** > **servrar och plats system roller**och väljer sedan plats servern för passivt läge.
  2. I fönstret **plats system roller** högerklickar du på **plats Server** rollen och väljer sedan **ta bort roll**.
  3. Högerklicka på plats servern för passivt läge och välj sedan **ta bort**.
  4. När plats servern har avinstallerats startar du om tjänsten **CONFIGURATION_MANAGER_UPDATE**på den aktiva primära plats servern.
  <!--sms 489412-->


**Följande är nya funktioner som du kan prova med den här versionen.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 -  Task 1
 -  Task 2              
-->



## <a name="create-phased-deployments"></a>Skapa stegvisa distributioner
<!-- 1357405 -->
Stegvisa distributioner automatiserar en samordnad, sekvenserad distribution av program vara utan att skapa flera distributioner. I den här tekniska för hands versionen kan guiden stegvis distribution utföras för aktivitetssekvenser i administratörs konsolen. Distributioner skapas dock inte. 

### <a name="try-it-out"></a>prova!  
  Försök att slutföra uppgifterna. Sedan skickar du **feedback** från fliken **Start** i menyfliksområdet och låter oss se hur det fungerade.
 
**Skapa en stegvis distribution för en aktivitetssekvens** </br>
1. I arbets ytan **program bibliotek** expanderar du **operativ system**och väljer **aktivitetssekvenser**.
2. Högerklicka på en befintlig aktivitetssekvens och välj **skapa stegvis distribution**. 
3. På fliken **Allmänt** anger du den stegvisa distributionen ett namn, en beskrivning (valfritt) och väljer **automatiskt skapa standard pilot och produktions faser**. 
4. Fyll i fälten **pilot samling** och **produktions samling** . Välj **Nästa**.
5. På fliken **Inställningar** väljer du ett alternativ för var och en av schemaläggnings inställningarna och väljer **Nästa** när du är klar. 
6. På fliken **faser** redigerar du någon av stegen om det behövs och klickar sedan på **Nästa**.
7. Bekräfta dina val på fliken **Sammanfattning** och klicka sedan på **Nästa** för att fortsätta.

## <a name="co-management-reporting"></a>Rapportering om samhantering
<!-- 1356648 -->
Om du använder [Co-Management](../../comanage/overview.md) -funktionerna kan du nu visa en instrument panel med information om samhantering i din miljö. Gå till arbets ytan **övervakning** i Configuration Manager-konsolen, expandera **uppgraderingsberedskap**och välj instrument panelen för **samhantering** . Instrument panelen innehåller följande paneler:
- **Samhanterade enheter**: procent andelen enheter i din miljö som du har aktiverat för samhantering
- **OS-distribution**: nedbrytning av operativ system (OS) efter version. I det här diagrammet används följande grupperingar:
  - Windows 7 & 8. x
  - Windows 10, lägre än 1709
  - Windows 10 1709 och senare
    > [!NOTE] 
    > Windows 10, version 1709 och senare, är en förutsättning för samhantering
- **Status för samhantering**: nedbrytning av enheten lyckades eller misslyckades i följande kategorier:
   - Lyckades, hybrid Azure AD är ansluten
   - Lyckades, Azure AD är ansluten
   - Fel: det gick inte att registrera automatiskt
- **Arbets belastnings över gång**: ett stapeldiagram som visar antalet enheter som du övergått till Microsoft Intune för de tre tillgängliga arbets belastningarna: 
   - Efterlevnadsprinciper
   - Resurs åtkomst
   - Windows Update för företag

### <a name="prerequisites"></a>Krav
- Datorn som kör Configuration Manager-konsolen kräver Internet Explorer 9 eller senare.



## <a name="improvements-to-automatic-deployment-rule-evaluation-schedule"></a>Förbättringar av utvärderings schema för automatisk distributions regel
<!-- 1357133 -->
Baserat på feedback från din [användare](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8819518-software-update-patch-tuesday-scheduling)kan du nu schemalägga en utvärdering av automatisk distributions regel (ADR) som ska motbokas från en bas dag. En förskjutning på två dagar efter den andra tisdagen i månaden utvärderar till exempel regeln på torsdag. 

### <a name="try-it-out"></a>prova!  
 Försök att slutföra uppgifterna. Sedan skickar du **feedback** från fliken **Start** i menyfliksområdet och låter oss se hur det fungerade. <br/>

**Skapa ett anpassat schema som utvärderar och ADR-förskjutning från en bas dag** </br>
1.  I arbets ytan **program bibliotek** expanderar du **program uppdateringar**och väljer **regler för automatisk distribution**.
2. Högerklicka på **automatiska distributions regler** och välj **Skapa regel för automatisk distribution**. 
3. Följ anvisningarna för att slutföra flikarna **Allmänt**, **distribution**och **program uppdateringar** . 
4. På fliken **utvärderings schema** väljer du **kör regeln enligt ett schema** och **Anpassa**.
5. För det anpassade schemat väljer du **varje månad** och sätter i en bas dag, till exempel den andra tisdagen. 
6. Kontrol lera **förskjutningen (dagar)** och antalet dagar för förskjutningen och sedan **OK** när du är färdig.  
7. Slutför resten av **guiden Skapa regel för automatisk distribution**. 



## <a name="reassign-distribution-point"></a>Omtilldela distributions plats
<!-- 1306937 -->
Många kunder har stora Configuration Manager infrastrukturer och minskar de primära eller sekundära platserna för att förenkla sin miljö. De måste fortfarande behålla distributions platser på avdelnings kontor för att kunna hantera innehåll till hanterade klienter. Dessa distributions platser innehåller ofta flera terabyte eller mer av innehållet. Det här innehållet är kostsamt i fråga om tid och nätverks bandbredd för att distribuera till dessa fjärrservrar. 

Med den här funktionen kan du omtilldela en distributions plats till en annan primär plats utan att distribuera om innehållet. Den här åtgärden uppdaterar plats system tilldelningen och behåller allt innehåll på servern. Om du behöver tilldela om flera distributions platser måste du först utföra den här åtgärden på en enda distributions plats och sedan fortsätta med ytterligare servrar en i taget.

> [!IMPORTANT]
> Plats system servern kan bara vara värd för distributions plats rollen. Om plats system servern är värd för en annan Configuration Manager Server roll, till exempel platsen för tillståndsmigrering, kan du inte omtilldela distributions platsen. Det går inte att omtilldela en distributions plats för molnet. 

Det här alternativet fungerar inte med den här versionen på grund av den tekniska för hands versionen av en enda primär plats. Överväg scenariot och skicka sedan **feedback** från fliken **Start** i menyfliksområdet, angående funktionerna i den här åtgärden.
1. I Configuration Manager-konsolen går du till arbets ytan **Administration** och väljer noden **distributions platser** .
2. Högerklicka på mål distributions platsen och välj **omtilldela distributions plats**. 
  ![Omtilldela distributions plats](media/1306937-reassign-dp.png)
3. Välj den plats Server och plats kod som du vill tilldela om distributions platsen. 
  ![Välj en plats Server](media/1306937-select-site.png)



## <a name="improvements-to-hardware-inventory"></a>Förbättringar av maskin varu inventering
<!-- 1357389 -->
För nyligen tillagda klasser kan sträng längder som är större än 255 tecken anges för maskin varu inventerings egenskaper som inte är nycklar.

### <a name="try-it-out"></a>prova!  
Försök att slutföra uppgifterna. Sedan skickar du **feedback** från fliken **Start** i menyfliksområdet och låter oss se hur det fungerade.<br/>

1. I arbets ytan **Administration** klickar du på **klient inställningar** Markera en klient enhets inställning som du vill redigera, högerklickar och väljer sedan **Egenskaper**. 
2. Välj **maskin varu inventering**, sedan **Ange klasser**och **Lägg till**.
3. Klicka på knappen **Anslut** .
4. Fyll i **dator namn**, **WMI-namnrymd**, Välj **rekursivt** vid behov. Ange autentiseringsuppgifter om det behövs för att ansluta. Klicka på **Anslut** om du vill visa namn områdets klasser.
5. Välj en ny klass och klicka sedan på **Redigera**.
6. Ändra **längden** på minst en egenskap som är en sträng, förutom nyckeln, som är större än 255. Klicka på **OK**. 
7. Se till att den redigerade egenskapen har marker ATS för **Lägg till maskin varu inventerings klass** och klicka på **OK**. 
8. Samla in maskin varu inventering med den nyligen tillagda klassen som innehåller en egenskap som är större än 255 tecken långt. 



## <a name="improvements-to-client-settings-for-software-center"></a>Förbättringar av klient inställningar för Software Center
<!-- 1351224 & 1355146 -->
I den här versionen av den tekniska för hands versionen har förbättringar gjorts för Software Center-anpassning under klient inställningarna. 

1. Klient inställningarna för Software Center har nu en **Anpassa** -knapp.
2. En för hands version har lagts till för att visa hur Software Center-banderollen ser ut.<!--1351224-->
    - Om en logo typ inte är markerad, visar förhands granskningen företags namnets text och färg.
    - Om du väljer en logo typ visas texten logo typ och företags namn i förhands granskningen.  
3.  **Dölj ej godkända program i Software Center** är en ny inställning för Software Center. När det här alternativet är aktiverat är användar tillgängliga program som kräver godkännande dolda i Software Center.<!--1355146-->

### <a name="try-it-out"></a>prova!  
 Försök att slutföra uppgifterna. Sedan skickar du **feedback** från fliken **Start** i menyfliksområdet och låter oss se hur det fungerade.

1. I arbets ytan **Administration** klickar du på **klient inställningar**. Välj en klient enhets inställning som ska redige ras. Högerklicka på den och välj sedan **Egenskaper** sedan **Software Center**.
2.  Klicka på knappen **Anpassa** . Testa de olika anpassnings inställningarna, inklusive förhands granskningen.
3. Aktivera inställningen **Dölj ej godkända program i Software Center**. Observera ändringarna i Software Center. 



## <a name="new-settings-for-windows-defender-application-guard"></a>Nya inställningar för Windows Defender Application Guard
<!-- 1356256 -->
För enheter med Windows 10 version 1709 och senare finns det två nya interaktions inställningar för värden för [Windows Defender Application Guard](../../protect/deploy-use/create-deploy-application-guard-policy.md). 
1. Webbplatser kan få åtkomst till värdens virtuella grafik processor. 
2. Filer som hämtats inuti behållaren kan sparas på värden. </br>



## <a name="improvements-to-run-scripts"></a>Förbättringar för att köra skript
<!-- 1236459 -->
Med [funktionen **Kör skript** ](../../apps/deploy-use/create-deploy-scripts.md) kan du nu importera och köra signerade PowerShell-skript. 
- Om du vill behålla skript integriteten måste signerade skript importeras i stället för att använda kopiera/klistra in. 
- Importerade signerade skript kan inte redige ras efter import.
    
>[!IMPORTANT]
>I den här tekniska för hands versionen finns det två tillfälliga begränsningar.
>- Skript kan bara importeras i funktionen kör skript och kan inte redige ras direkt från-konsolen.
>- Skript som importeras med en icke-Unicode-kodning kan visas felaktigt i konsolen. Skriptet körs fortfarande som det ursprungligen skrevs.





## <a name="next-steps"></a>Nästa steg
Information om hur du installerar eller uppdaterar den tekniska för hands versionen finns i [teknisk för hands version för Configuration Manager](technical-preview.md).    
