---
title: Installations program för snabb korrigeringar
titleSuffix: Configuration Manager
description: Ta reda på när och hur du installerar uppdateringar via installations programmet för snabb korrigeringar för Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f3058277-c597-4dac-86d1-41b6f7e62b36
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9389f407f8bdbafd057770ff63ed9b139e6600b5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720711"
---
# <a name="use-the-hotfix-installer-to-install-updates-for-configuration-manager"></a>Använd installations programmet för snabb korrigeringar för att installera uppdateringar för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Vissa uppdateringar för Configuration Manager är inte tillgängliga från Microsofts moln tjänst och hämtas endast out-of-band. Ett exempel är en begränsad version av en snabbkorrigering för att lösa ett specifikt problem.   
När du måste installera en uppdatering (eller snabb korrigering) som du får från Microsoft och uppdateringen har ett fil namn som slutar med fil namns tillägget **. exe** (inte **Update. exe**), använder du installations programmet för snabb korrigeringar som ingår i den här snabb korrigeringen för att installera uppdateringen direkt på Configuration Manager plats Server.  

Om snabb korrigerings filen har fil namns tillägget **. Update. exe** , kan du läsa mer i [använda verktyget uppdatera registrering för att importera snabb korrigeringar till Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

> [!NOTE]  
> Det här avsnittet innehåller allmän vägledning om hur du installerar snabb korrigeringar som uppdaterar Configuration Manager. Detaljerad information om en viss uppdatering finns i motsvarande KB-artikel på Microsoft Support.  

##  <a name="overview-of-hotfixes-for-configuration-manager"></a><a name="bkmk_Overview"></a>Översikt över snabb korrigeringar för Configuration Manager  
Snabb korrigeringar för Configuration Manager liknar dem för andra Microsoft-produkter, till exempel SQL Server, innehåller antingen en enskild korrigering eller ett paket (en samlad korrigering) och beskrivs i en Microsoft Knowledge Base-artikel.  

Enskilda uppdateringar innehåller en enda fokuserad uppdatering för en viss version av Configuration Manager.  
Uppdaterings paket innehåller flera uppdateringar för en angiven version av Configuration Manager.  
När uppdateringen ingår i ett paket kan du inte bara installera enskilda uppdateringar.  

Om du tänker skapa distributioner för att installera uppdateringar på ytterligare datorer, måste du installera uppdateringspaketet på en central administrationsplatsserver eller en primär platsserver.  

Följande händer när du kör uppdateringspaketet:  

- Det extraherar uppdateringsfilerna för varje aktuell komponent från paketet.  

- En guide startar som leder dig genom en process för att konfigurera uppdateringarna och distributionsalternativ för uppdateringarna.  

- När du har kört guiden installeras uppdateringarna i paketet som gäller platsservern på servern.  

Guiden skapar även distributionspaket som du kan använda för att installera uppdateringarna på ytterligare datorer. Du kan distribuera uppdateringar på ytterligare datorer med hjälp av en distributionsmetod som stöds, t.ex. ett programdistributionspaket eller Microsoft System Center Updates Publisher 2011.  

När guiden körs skapar den en **.cab-fil** på platsservern som kan användas med Updates Publisher 2011. Du kan konfigurera guiden så att den även skapar ett eller flera paket för programdistribution. Du kan använda dessa distributioner för att installera uppdateringar av komponenter, t. ex. klienter eller Configuration Manager-konsolen. Du kan även installera uppdateringar manuellt på datorer som inte kör Configuration Manager-klienten.  

Följande tre grupper i Configuration Manager kan uppdateras:  

- Configuration Manager Server roller, bland annat:  

  - Central administrationsplats  

  - Primär plats  

  - Sekundär plats  

  - SMS-fjärrprovider  

- Configuration Manager-konsolen  

- Configuration Manager-klient  

> [!NOTE]  
> **Uppdateringar för plats system roller** (inklusive uppdateringar av plats databasen och molnbaserade distributions platser) installeras som en del av uppdateringen av plats servrar och-tjänster av plats komponent hanteraren.  
>   
> Uppdateringar av mottagar distributions platser hanteras dock av distributions hanteraren i stället för plats komponent hanteraren.  

Varje uppdaterings paket för Configuration Manager är en självextraherande. exe-fil (SFX) som innehåller de filer som krävs för att installera uppdateringen på tillämpliga komponenter i Configuration Manager. SFX-filen brukar innehålla följande filer:  

|Fil|Information|  
|----------|-------------|  
|&lt;Produkt version\>– QFE – KB&lt;KB-artikel\>-&lt;-\>-&lt;Platform\>language. exe|Detta är uppdateringsfiler. Kommandoraden för denna fil hanteras av Updatesetup.exe.<br /><br /> Ett exempel:<br />Cm1511rtm. exe|  
|Updatesetup.exe|Denna .msi-omslutning hanterar installationen av uppdateringspaketet.<br /><br /> När uppdateringen körs, identifierar Updatesetup.exe visningsspråket på datorn. Uppdateringens standardspråk är engelska. Men om andra visningsspråk stöds, visas användargränssnitt på datorns lokala språk.|  
|License_&lt;language\>.rtf|Eventuellt innehåller varje uppdatering en eller flera licensfiler för de språk som stöds.|  
|&lt;Produkt&uppdateringstyp>-&lt;produkt version\>-&lt;KB-artikel\>-&lt;-\>ID Platform. msp|När uppdateringen gäller Configuration Manager-konsolen eller-klienter, innehåller uppdaterings paketet separata Windows Installer-korrigeringsfiler (MSP).<br /><br /> Ett exempel:<br /><br /> **Configuration Manager-konsoluppdatering:** ConfigMgr1511-AdminUI-KB1234567-i386.msp<br /><br /> **Klient uppdatering:** Configmgr1511. msp<br />Configmgr1511. msp|  

Uppdateringspaketet loggar normalt vad det gör i en loggfil på platsservern. Loggfilen har samma namn som uppdateringspaketet och sparas i mappen **%SystemRoot%/Temp** .  

När du kör uppdateringspaketet extraherar det en fil med samma namn som paketet till en temporär mapp på datorn, och därefter körs Updatesetup.exe. Updatesetup. exe startar program uppdateringen för guiden Configuration Manager &lt;produkt version\> &lt;KB-\> nummer.  

När det gäller uppdateringens omfattning skapar guiden en serie mappar under mappen Configuration Manager installation på plats servern. Mappstrukturen liknar följande:   
**&lt;\>\\\>\\Server namn\>\ SMS_&lt;-platskod\>\snabbkorrigering\\KB-nummer&lt;uppdaterings\>typ&lt;plattform. \\ \\ &lt;**  

Följande tabell innehåller information om mapparna i mappstrukturen:  

|Mappnamn|Mer information|  
|-----------------|----------------------|  
|&lt;Servernamn\>|Detta är namnet på platsservern där du kör uppdateringspaketet.|  
|SMS_&lt;platskod\>|Detta är resurs namnet för Configuration Manager-installationsmappen.|  
|&lt;KB-nummer\>|Detta är id-numret för Knowledge Base-artikeln för det här uppdateringspaketet.|  
|&lt;Uppdaterings typ\>|Detta är de olika typerna av uppdateringar för Configuration Manager. Guiden skapar en separat mapp för varje typ av uppdatering som finns med i uppdateringspaketet. Mappnamnen representerar uppdateringstyperna. De omfattar följande:<br /><br /> **Server**: innehåller uppdateringar av plats servrar, plats databas servrar och datorer som kör SMS-providern.<br /><br /> **Klient**: innehåller uppdateringar av Configuration Manager-klienten.<br /><br /> **AdminConsole**: inkluderar uppdateringar av Configuration Manager-konsolen<br /><br /> Förutom de föregående uppdaterings typerna skapar guiden en mapp med namnet **SCUP**. Den här mappen representerar inte en uppdateringstyp utan innehåller CAB-filen för Updates Publisher.|  
|&lt;Plattform\>|Detta är en plattformsspecifik mapp. Den innehåller uppdateringsfiler som är specifika för en viss processortyp.  Dessa mappar innehåller:<br /><br />– x64<br /><br /> -I386|  

##  <a name="how-to-install-updates"></a><a name="bkmk_Install"></a> Hur du installerar uppdateringar  
Innan du kan installera uppdateringar måste du installera uppdateringspaketet på en platsserver. När du installerar ett uppdateringspaket startas installationsguiden för den uppdateringen. Den här guiden gör följande:  

- Extraherar uppdateringsfilerna  

- Hjälper dig att konfigurera distributioner  

- Installerar aktuella uppdateringar på den lokala datorns serverkomponenter.  

När du har installerat uppdaterings paketet på en plats Server kan du uppdatera ytterligare komponenter för Configuration Manager. I följande tabell beskrivs uppdateringsåtgärderna för dessa olika komponenter.  

|Komponent|Instruktioner|  
|---------------|------------------|  
|Platsserver|Distribuera uppdateringar till en fjärrplatsserver om du inte väljer att installera uppdateringspaketet direkt på fjärrplatsservern.|  
|Platsdatabas|Distribuera – för fjärrplatsservrar – serveruppdateringar som innehåller en uppdatering av platsdatabasen om du inte installerar uppdateringspaketet direkt på fjärrplatsservern.|  
|Configuration Manager-konsolen|Efter den första installationen av Configuration Manager-konsolen kan du installera uppdateringar för Configuration Manager-konsolen på varje dator som kör-konsolen. Du kan inte ändra Configuration Manager-konsolens installationsfiler för att tillämpa uppdateringarna under den första installationen av-konsolen.|  
|SMS-fjärrprovider|Installera uppdateringar för varje instans av SMS-providern som körs på en annan dator än platsservern där du installerade uppdateringspaketet.|  
|Configuration Manager klienter|Efter den första installationen av Configuration Manager-klienten kan du installera uppdateringar för Configuration Manager-klienten på varje dator som kör-klienten.|  

> [!NOTE]  
> Du kan bara distribuera uppdateringar till datorer som kör Configuration Manager-klienten.  

Om du installerar om en klient, Configuration Manager-konsol eller SMS-provider måste du även installera om uppdateringarna för dessa komponenter.  

Använd informationen i följande avsnitt för att installera uppdateringar av varje komponent för Configuration Manager.  

###  <a name="update-servers"></a><a name="bkmk_servers"></a>Uppdatera servrar  
Uppdateringar för servrar kan innehålla uppdateringar av **platser**, **site database**och datorer som kör en instans av **SMS-providern**:  

####  <a name="update-a-site"></a><a name="bkmk_site"></a>Uppdatera en plats  
Om du vill uppdatera en Configuration Manager plats kan du installera uppdaterings paketet direkt på plats servern, eller så kan du distribuera uppdateringarna till en plats Server efter att du har installerat uppdaterings paketet på en annan plats.  

När du installerar en uppdatering på en platsserver, hanterar installationsprocessen de övriga åtgärder som krävs för att tillämpa uppdateringen, t.ex. att uppdatera platssystemsroller. Undantaget till detta är platsdatabasen. Det följande avsnittet innehåller information om hur du uppdaterar platsdatabasen.  

####  <a name="update-a-site-database"></a><a name="bkmk_database"></a>Uppdatera en plats databas  
För att kunna uppdatera plats databasen kör installations processen en fil med namnet **Update. SQL** på plats databasen. Du kan konfigurera uppdateringsprocessen så att platsdatabasen uppdateras automatiskt, eller så kan du uppdatera den manuellt senare.  

**Automatisk uppdatering av plats databasen**  

När du installerar uppdaterings paketet på en plats Server kan du välja att uppdatera plats databasen automatiskt när Server uppdateringen installeras. Detta beslut gäller endast för den plats server där du installerar uppdaterings paketet och gäller inte distributioner som skapas för att installera uppdateringarna på fjärrplatsens servrar.  

> [!NOTE]  
> När du väljer att uppdatera plats databasen automatiskt, uppdaterar processen en databas oavsett om databasen finns på plats servern eller på en fjärrdator.  

> [!IMPORTANT]  
> Innan du uppdaterar plats databasen skapar du en säkerhets kopia av plats databasen. Det går inte att avinstallera en uppdatering av platsdatabasen. Information om hur du skapar en säkerhets kopia för Configuration Manager finns i [säkerhets kopiering och återställning av Configuration Manager](backup-and-recovery.md).  

**Manuell uppdatering av plats databasen**  

Om du väljer att inte uppdatera plats databasen automatiskt när du installerar uppdaterings paketet på plats servern, ändrar Server uppdateringen inte databasen på plats servern där uppdaterings paketet körs. Distributioner som använder paketet som skapas för program varu distribution eller som installerar uppdaterar dock alltid plats databasen.  

> [!WARNING]  
> När uppdateringen inkluderar uppdateringar av både plats servern och plats databasen fungerar inte uppdateringen förrän uppdateringen har slutförts för både plats servern och plats databasen. Platsen är i ett tillstånd som inte stöds förrän uppdateringen har tillämpats på plats databasen.  

**Så här uppdaterar du en plats databas manuellt:**  

1.  Stoppa tjänsten SMS_SITE_COMPONENT_MANAGER på plats servern och stoppa sedan tjänsten SMS_EXECUTIVE.  

2.  Stäng Configuration Manager-konsolen.  

3.  Kör uppdaterings skriptet med namnet **Update. SQL** på platsens databas. Information om hur du kör ett skript för att uppdatera en SQL Server databas finns i dokumentationen för den version av SQL Server som du använder för plats databas servern.  

4.  Starta om tjänster som stoppades i föregående steg.  

5.  När uppdaterings paketet installeras extraheras **Update. SQL** till följande plats på plats servern: ** \\ \\ &lt;\>Server namn&lt;\ SMS_ plats kod\>\snabbkorrigering\\&lt;KB-nummer \Update.SQL\>**  

####  <a name="update-a-computer-that-runs-the-sms-provider"></a><a name="bkmk_provider"></a>Uppdatera en dator som kör SMS-providern  
När du har installerat ett uppdaterings paket som innehåller uppdateringar för SMS-providern måste du distribuera uppdateringen till varje dator som kör SMS-providern. Det enda undantaget är instansen av SMS-providern som tidigare har installerats på platsservern där du installerar uppdateringspaketet. Den lokala instansen av SMS-providern på plats servern uppdateras när du installerar uppdaterings paketet.  

Om du tar bort och sedan installerar om SMS-providern på en dator måste du installera om uppdateringen för SMS-providern på den datorn.  

###  <a name="update-clients"></a><a name="BKMK_clients"></a>Uppdatera klienter  
När du installerar en uppdatering som innehåller uppdateringar för Configuration Manager klienten visas alternativet för att automatiskt uppgradera klienter med uppdateringen eller manuellt uppgradera klienter vid ett senare tillfälle. Mer information om hur du uppgraderar klienten automatiskt finns i [Uppgradera klienter för Windows-datorer](https://technet.microsoft.com/library/mt627885.aspx).  

Du kan distribuera uppdateringar med Updates Publisher eller ett programdistributionspaket eller så kan du välja att installera uppdateringen manuellt på varje klient. Mer information om hur du använder distributioner för att installera uppdateringar finns i [Distribuera uppdateringar av Configuration Manager](#BKMK_Deploy) i den här artikeln.  

> [!IMPORTANT]  
> När du installerar uppdateringar för klienter och uppdaterings paketet innehåller uppdateringar för servrar, måste du även installera Server uppdateringarna på den primära platsen som klienterna är tilldelade till.  

Om du vill installera klient uppdateringen manuellt på varje Configuration Manager-klient måste du köra **msiexec. exe** och referera till den plattformsspecifika klient uppdaterings filen. msp.  

Du kan till exempel använda följande kommando rad för en klient uppdatering. Den här kommando raden kör msiexec på klient datorn och refererar till. msp-filen som uppdaterings paketet extraherade på plats servern **: msiexec. exe \\ \\ &lt;/p\>servername \&lt;SMS_\>platskod\\&lt;\snabbkorrigering KB\>Number\\&lt;\Client\>\\&lt;Platform\> MSP\*/l &lt;v\>logfile REINSTALLMODE = MOUS REINSTALL = ALL**  

###  <a name="update-configuration-manager-consoles"></a><a name="BKMK_console"></a>Uppdatera Configuration Manager-konsoler  
Om du vill uppdatera en Configuration Manager-konsol måste du installera uppdateringen på den dator som kör-konsolen efter att konsol installationen har slutförts.  

> [!IMPORTANT]  
> När du installerar uppdateringar för Configuration Manager-konsolen och uppdaterings paketet innehåller uppdateringar för servrar, måste du även installera Server uppdateringarna på den plats som du använder med Configuration Manager-konsolen.  

Om datorn som du uppdaterar kör Configuration Manager-klienten:  

- Du kan använda en distribution för att installera uppdateringen. Mer information om hur du använder distributioner för att installera uppdateringar finns i [Distribuera uppdateringar av Configuration Manager](#BKMK_Deploy) i den här artikeln.  

- Om du är inloggad direkt på klientdatorn, kan du köra installationen interaktivt.  

- Du kan installera uppdateringen manuellt på varje dator. Om du vill installera Configuration Manager-konsolens uppdatering manuellt på varje dator som kör Configuration Manager-konsolen kan du köra Msiexec. exe och referera till Configuration Manager-konsolens uppdatering. msp-fil.  

Du kan till exempel använda följande kommando rad för att uppdatera en Configuration Manager-konsol. Den här kommando raden kör msiexec på datorn och refererar till. msp-filen som uppdaterings paketet extraherade på plats servern **: msiexec. exe \\ \\ &lt;/p\>servername \&lt;SMS_\>platskod\\&lt;\snabbkorrigering KB\>Number\\&lt;\AdminConsole\>\\&lt;Platform\> MSP\*/l &lt;v\>logfile REINSTALLMODE = MOUS REINSTALL = ALL**  

##  <a name="deploy-updates-for-configuration-manager"></a><a name="BKMK_Deploy"></a> Distribuera uppdateringar av Configuration Manager  
När du har installerat uppdaterings paketet på en plats Server kan du använda någon av följande tre metoder för att distribuera uppdateringar till ytterligare datorer.  

###  <a name="use-updates-publisher-2011-to-install-updates"></a><a name="BKMK_DeploySCUP"></a>Använd Updates Publisher 2011 för att installera uppdateringar  
När du installerar uppdaterings paketet på en plats Server skapar installations guiden en katalog fil för Updates Publisher som du kan använda för att distribuera uppdateringarna på tillämpliga datorer. Den här guiden skapar alltid den här katalogen, även när du väljer alternativet **Använd paket och program för att distribuera den här uppdateringen**.  

Katalogen för Updates Publisher heter **SCUPCatalog. cab** och finns på följande plats på den dator där uppdaterings paketet körs: ** \\ \\ &lt;\>servername \ SMS_&lt;SiteCode\>\snabbkorrigering\\&lt;KB Number \SCUP\SCUPCatalog.cab\>**  

> [!IMPORTANT]  
> Eftersom filen SCUPCatalog. cab skapas med sökvägar som är speciella för plats servern där uppdaterings paketet är installerat, kan den inte användas på andra plats servrar.  

När guiden har slutförts kan du importera katalogen till Updates Publisher och sedan använda Configuration Manager program uppdateringar för att distribuera uppdateringarna. Information om Updates Publisher finns i [updates publisher 2011](https://go.microsoft.com/fwlink/p/?LinkID=83449) i TechNet-biblioteket för System Center 2012.  

Använd följande procedur för att importera filen SCUPCatalog. cab till Updates Publisher och publicera uppdateringarna.  

##### <a name="to-import-the-updates-to-updates-publisher-2011"></a>Så här importerar du uppdateringarna till Updates Publisher 2011  

1.  Starta Updates Publisher-konsolen och klicka på **Importera**.  

2.  På sidan **import typ** i guiden Importera program uppdaterings katalog väljer du **Ange sökvägen till katalogen som ska importeras**och anger sedan filen SCUPCatalog. cab.  

3.  Klicka på **Nästa**och sedan på **Nästa** igen.  

4.  I dialog rutan **säkerhets varning – katalog validering** klickar du på **acceptera**. Stäng guiden när den har slutförts.  

5.  I Updates Publisher-konsolen väljer du den uppdatering som du vill distribuera och klickar sedan på **publicera**.  

6.  På sidan **publicerings alternativ** i guiden publicera program uppdateringar väljer du **fullständigt innehåll**och klickar sedan på **Nästa**.  

7.  Publicera uppdateringarna genom att slutföra guiden.  

###  <a name="use-software-deployment-to-install-updates"></a><a name="BKMK_DeploySWDist"></a>Använd program varu distribution för att installera uppdateringar  
När du installerar uppdaterings paketet på plats servern för en primär plats eller en central administrations plats kan du konfigurera installations guiden för att skapa uppdaterings paket för program distribution. Du kan sedan distribuera varje paket till en samling datorer som du vill uppdatera.  

Om du vill skapa ett program distributions paket går du till sidan **Konfigurera distribution av program uppdateringar** i guiden och markerar kryss rutan för varje uppdaterings paket typ som du vill uppdatera. Tillgängliga typer kan vara servrar, Configuration Manager konsoler och klienter. Ett separat paket skapas för varje typ av uppdatering som du väljer.  

> [!NOTE]  
> Paketet för servrar innehåller uppdateringar för följande komponenter:  
>   
> - Platsserver  
> - SMS-provider  
> - Platsdatabas  

Därefter öppnar du sidan **Konfigurera distributionsmetod för programuppdatering** i guiden och väljer alternativet **Jag använder programdistribution**. Det här valet instruerar guiden att skapa program distributions paketen.  

När guiden har slutförts kan du Visa paketen som skapas i Configuration Manager-konsolen i noden **paket** i arbets ytan **program varu bibliotek** . Du kan sedan använda standard processen för att distribuera program varu paket till Configuration Manager-klienter. När ett paket körs på en klient installeras uppdateringarna av tillämpliga komponenter i Configuration Manager på klient datorn.  

Information om hur du distribuerar paket till Configuration Manager-klienter finns i [paket och program](../../../apps/deploy-use/packages-and-programs.md).  

###  <a name="create-collections-for-deploying-updates-to-configuration-manager"></a><a name="BKMK_DeployCollections"></a>Skapa samlingar för att distribuera uppdateringar till Configuration Manager  
Du kan distribuera vissa uppdateringar på tillämpliga klienter. Följande information kan hjälpa dig att skapa enhets samlingar för de olika komponenterna för Configuration Manager.  

|Komponent i Configuration Manager|Instruktioner|  
|----------------------------------------|------------------|  
|Central administrationsplatsserver|Skapa en direkt medlemskapsfråga och lägg till datorn för central administrationsplatsserver.|  
|Alla primära platsservrar|Skapa en direkt medlemskapsfråga och lägg till varje primär platsserverdator.|  
|Alla sekundära platsservrar|Skapa en direkt medlemskapsfråga och lägg till varje sekundär platsserverdator.|  
|Alla x86-klienter|Skapa en samling med följande frågevillkor:<br /><br /> **Välj \* från sms_r_system inre koppling SMS_G_System_SYSTEM på SMS_G_System_SYSTEM. ResourceID = SMS_R_System. ResourceId där SMS_G_System_SYSTEM. SystemType = "x86-based PC"**|  
|Alla x64-klienter|Skapa en samling med följande frågevillkor:<br /><br /> **Välj \* från sms_r_system inre koppling SMS_G_System_SYSTEM på SMS_G_System_SYSTEM. ResourceID = SMS_R_System. ResourceId där SMS_G_System_SYSTEM. SystemType = "x64-based PC"**|  
|Alla datorer som kör Configuration Manager-konsolen|Skapa en direkt medlemskapsfråga och lägg till varje dator.|  
|Fjärrdatorer som kör en instans av SMS-providern|Skapa en direkt medlemskapsfråga och lägg till varje dator.|  

> [!NOTE]  
> Om du vill uppdatera en platsdatabas distribuerar du platsservern för den platsen.  

Information om hur du skapar samlingar finns i [skapa samlingar](../../../core/clients/manage/collections/create-collections.md).  
