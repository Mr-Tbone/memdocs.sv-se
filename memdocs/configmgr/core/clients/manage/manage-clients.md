---
title: Hantera klienter
titleSuffix: Configuration Manager
description: Lär dig hur du hanterar klienter i Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b6d1ee82e116a6d4375e37ccca84c8b35707f8e1
ms.sourcegitcommit: e8076576f5c0ea7e72358d233782f8c38c184c8f
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/28/2020
ms.locfileid: "87334597"
---
# <a name="how-to-manage-clients-in-configuration-manager"></a>Hantera klienter i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När Configuration Manager-klienten installeras på en enhet och har tilldelats en plats visas enheten i arbets ytan **till gångar och efterlevnad** i noden **enheter** och i en eller flera samlingar i noden **enhets samlingar** . Välj enheten eller en samling och kör sedan hanterings åtgärder. Det finns dock andra sätt att hantera klienten, som kan omfatta andra arbets ytor i konsolen, eller aktiviteter utanför-konsolen.  

> [!NOTE]  
> Om du installerar Configuration Manager klienten, men ännu inte har tilldelats en plats, kanske den inte visas i-konsolen. När klienten har tilldelats en plats uppdaterar du medlemskapet i samlingen och uppdaterar sedan konsolen.  
>
> En enhet kan också visas i-konsolen om Configuration Manager-klienten inte är installerad. Det här problemet uppstår om platsen identifierar en enhet men klienten inte är installerad och tilldelad.
>
> Mobila enheter som hanteras med [Exchange Server-anslutningen](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) eller [lokal MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) installerar inte Configuration Manager-klienten.  
>
> Om du vill hantera en enhet från-konsolen använder du kolumnen **klient** i noden **enheter** för att avgöra om klienten är installerad.  

## <a name="manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a>Hantera klienter från noden **enheter**  

Beroende på enhetstypen kanske vissa av dessa alternativ kanske inte är tillgängliga.  

1. I Configuration Manager-konsolen går du till arbets ytan **till gångar och efterlevnad** och väljer noden **enheter** .  

2. Välj en eller flera enheter och välj sedan en av dessa klient hanterings aktiviteter från menyfliksområdet. Du kan också högerklicka på enheten.)  

### <a name="import-user-device-affinity"></a>Importera mappning mellan användare och enhet

Konfigurera kopplingarna mellan användare och enheter, så att du effektivt kan distribuera program vara till användare.  

Mer information finns i [Länka användare och enheter med mappning mellan användare och enhet](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="import-computer-information"></a>Importera dator information

Starta **guiden Importera dator information** för att importera ny dator information till Configuration Manager databasen. Du kan importera flera datorer med en fil eller ange information för en enskild dator.

### <a name="add-selected-items"></a>Lägg till markerade objekt

Innehåller följande alternativ:

- **Lägg till markerade objekt i befintlig enhets samling**: öppnar dialog rutan **Välj samling** . Välj den samling som du vill lägga till den här enheten i. Enheten ingår i den här samlingen med hjälp av en regel för **direkt** medlemskap.  

- **Lägg till markerade objekt i ny enhets samling**: öppnar **guiden skapa enhets samling** där du kan skapa en ny samling. Den valda samlingen ingår i den här samlingen med hjälp av en regel för **direkt** medlemskap.  

Mer information finns i [så här skapar du samlingar](collections/create-collections.md).

### <a name="install-client"></a>Installera klient

Öppnar **guiden Installera klient**. Den här guiden använder push-installation av klienter för att installera eller installera om Configuration Manager-klienten på den valda enheten.

> [!TIP]  
> Det finns många olika sätt att installera Configuration Manager-klienten. Även om klient-push-guiden erbjuder en bekväm klient installations metod från-konsolen, har den här metoden många beroenden och är inte lämplig för alla miljöer. Mer information om beroenden finns i [krav för distribution av klienter till Windows-datorer](../deploy/prerequisites-for-deploying-clients-to-windows-computers.md#client-push-installation). Mer information om andra klient installations metoder finns i [klient installations metoder](../deploy/plan/client-installation-methods.md).

Mer information finns i [så här installerar du Configuration Manager-klienter med push-installation](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)av klienter.

### <a name="run-script"></a>Köra skriptet

Öppnar guiden **Kör skript** för att köra ett PowerShell-skript på den valda enheten.

Mer information finns i [skapa och köra PowerShell-skript](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="install-application"></a>Installera program

Installera ett program på en enhet i real tid. Den här funktionen kan hjälpa till att minska behovet av separata samlingar för varje program.

Mer information finns i [installera program för en enhet](../../../apps/deploy-use/install-app-for-device.md).

### <a name="reassign-site"></a>Tilldela om plats

Tilldela om en eller flera klienter, inklusive hanterade mobila enheter, till en annan primär plats i hierarkin. Du kan individuellt tilldela om klienter eller välja mer än en för att tilldela om dem i grupp.  

### <a name="client-settings---resultant-client-settings"></a>Klient inställningar – resultat av klient inställningar

När du distribuerar flera klient inställningar till samma enhet är prioriteringen och kombinationen av inställningar komplex. Använd det här alternativet om du vill visa den resulterande uppsättningen av klient inställningar som distribueras till den här enheten.

Mer information finns i [så här konfigurerar du klient inställningar](../deploy/configure-client-settings.md).

### <a name="start"></a>Start

- Kör **Resursläsaren** för att se information om maskin-och program varu inventering från en Windows-klient. Mer information finns i följande artiklar:

  - [Visa maskinvaruinventering med hjälp av Resursläsaren](inventory/use-resource-explorer-to-view-hardware-inventory.md)

  - [Visa programvaruinventering med hjälp av Resursläsaren](inventory/use-resource-explorer-to-view-software-inventory.md)

- Fjärradministrera enheten med **fjärr styrning**, **Fjärrhjälp**eller **fjärr skrivbords klienten**. Mer information finns i [så här fjärradministrerar du en Windows-klientdator](remote-control/remotely-administer-a-windows-client-computer.md).

### <a name="approve"></a>Godkänn

När klienten kommunicerar med plats system med HTTP och ett självsignerat certifikat måste du godkänna dessa klienter för att identifiera dem som betrodda datorer. Som standard godkänner plats konfigurationen automatiskt klienter från samma Active Directory skog, betrodda skogar och anslutna Azure Active Directory (Azure AD)-klient organisationer<!-- MEMDocs#318 -->. Detta standard beteende innebär att du inte behöver godkänna varje klient manuellt. Godkänn manuellt de arbets grupps datorer som du litar på och andra ej godkända datorer som du litar på.

> [!IMPORTANT]  
> Även om vissa hanterings funktioner kan fungera för klienter som inte är godkända, är detta ett scenario som inte stöds för Configuration Manager.  

Du behöver inte godkänna klienter som alltid kommunicerar med plats system med hjälp av HTTPS, eller klienter som använder ett PKI-certifikat när de kommunicerar med plats system med HTTP. Dessa klienter etablerar förtroende med hjälp av PKI-certifikaten.

### <a name="block-or-unblock"></a>Blockera eller avblockera

Blockera en klient som du inte längre litar på. Blockering förhindrar att klienten tar emot principer och förhindrar att plats system kommunicerar med klienten.  

> [!IMPORTANT]  
> Att blockera en klient förhindrar bara kommunikation från klienten till att Configuration Manager plats system. Den förhindrar inte kommunikation till andra enheter. När klienten kommunicerar med plats system genom att använda HTTP i stället för HTTPS finns det vissa säkerhets begränsningar.  

Du kan också avblockera en klient som är blockerad.

Mer information finns i [avgöra om klienter ska blockeras](../deploy/plan/determine-whether-to-block-clients.md).

<!-- Change Category is a hybrid action -->

### <a name="clear-required-pxe-deployments"></a>Rensa nödvändiga PXE-distributioner

Du kan distribuera om en nödvändig PXE-distribution genom att rensa statusen för den senaste PXE-distributionen som tilldelats till en Configuration Manager samling eller en dator. Med den här åtgärden återställs statusen för distributionen och de senaste nödvändiga distributionerna installeras om.

Mer information finns i [använda PXE för att distribuera Windows via nätverket](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

### <a name="client-notification"></a>Klientmeddelande

Mer information finns i [klient meddelanden](client-notification.md#client-notification).

### <a name="endpoint-protection"></a>Slutpunktsskydd

Mer information finns i [klient meddelanden](client-notification.md#endpoint-protection).

### <a name="edit-primary-users"></a>Redigera primära användare

Visa användare av den här enheten under de senaste 90 dagarna eller ange enhetens primära användare.

Mer information finns i [Länka användare och enheter med mappning mellan användare och enhet](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="wipe-a-mobile-device"></a>Rensa en mobil enhet

Du kan rensa mobila enheter som stöder rensningskommandot. Den här åtgärden tar permanent bort alla data på den mobila enheten, inklusive personliga inställningar och personliga data. Åtgärden återställer normalt den mobila enheten till fabriksinställningarna. Rensa en mobil enhet när den inte längre är betrodd. Om enheten till exempel tappas bort eller blir stulen.  

> [!TIP]  
> Läs tillverkarens dokumentation om du vill ha mer information om hur den mobila enheten bearbetar ett fjär rensnings kommando.  

Det finns ofta en fördröjning tills den mobila enheten tar emot rensnings kommandot:  

- Om den mobila enheten registreras av Configuration Manager, tar klienten emot kommandot när den laddar ned klient principen.

- Om den mobila enheten hanteras av Exchange Server-anslutningen får den kommandot när den synkroniseras med Exchange.  

Använd kolumnen **Rensa status** för att övervaka när enheten tar emot rensnings kommandot. Du kan avbryta rensnings kommandot tills enheten skickar en rensnings bekräftelse till Configuration Manager.  

### <a name="retire-a-mobile-device"></a>Pensionera en mobil enhet

Alternativet för att **dra tillbaka** stöds endast av mobila enheter som har registrerats av lokal MDM.  

Mer information finns i [skydda dina data med fjär rensning, fjärrlåsning eller lösen ords återställning](../../../mdm/deploy-use/wipe-lock-reset-devices.md).

### <a name="change-ownership"></a>Ändra ägarskap

Om en enhet inte är domänansluten och inte har Configuration Manager-klienten installerad använder du det här alternativet för att ändra ägarskapet till **företaget** eller **personliga**.  

Du kan använda det här värdet i program krav för att styra distributioner och för att styra hur mycket inventering som samlas in från användarnas enheter.  

Du kan behöva lägga till kolumnen **enhets ägare** i vyn genom att högerklicka på en kolumn rubrik och välja den.

### <a name="delete"></a>Ta bort

> [!WARNING]  
> Ta inte bort en klient om du vill avinstallera Configuration Manager-klienten eller ta bort den från en samling.  

Åtgärden **ta bort** tar manuellt bort klient posten från den Configuration Manager databasen. Använd endast den här åtgärden för att felsöka ett problem. Om du tar bort objektet, men klienten fortfarande är installerad och kommunicerar med platsen, återskapar pulsslags identifieringen klient posten. Den visas igen i Configuration Manager-konsolen, även om klient historiken och eventuella tidigare associationer går förlorade.  
> [!NOTE]  
> När du tar bort en mobilen hets klient som har registrerats av Configuration Manager, återkallar den här åtgärden även det utfärdade PKI-certifikatet. Certifikatet avvisas sedan av hanterings platsen, även om IIS inte kontrollerar listan över återkallade certifikat (CRL).
>
> Certifikat på äldre klienter på mobila enheter återkallas inte när du tar bort dessa klienter.

Information om hur du avinstallerar-klienten finns i [avinstallera Configuration Manager-klienten](#BKMK_UninstalClient).  

Information om hur du tilldelar klienten en ny primär plats finns i [tilldela klienter till en plats](../deploy/assign-clients-to-a-site.md).

Om du vill ta bort en klient från en samling konfigurerar du om samlingens egenskaper. Mer information finns i [hantera samlingar](collections/manage-collections.md).

### <a name="refresh"></a>Uppdatera

Uppdatera konsol visningen med de senaste data i databasen. Till exempel, om en enhet visas i listan från identifiering, men inte visas som installerad. När du har installerat-klienten och kontrol lera att den är tilldelad till platsen väljer du **Uppdatera**.

### <a name="properties"></a>Egenskaper

Visa identifierings data och distributioner riktade mot klienten.

Du kan också konfigurera variabler som aktivitetssekvenser använder för att distribuera ett operativ system till enheten. Mer information finns i [Skapa variabler för aktivitetssekvens för enheter och samlingar](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-coll-var).


## <a name="manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a>Hantera klienter från noden **enhets samlingar**

Många av de uppgifter som är tillgängliga för enheter i noden **enheter** är också tillgängliga i samlingar. -Konsolen tillämpar automatiskt åtgärden på alla kvalificerade enheter i samlingen. Den här åtgärden för en hel samling genererar ytterligare nätverks paket och ökar processor användningen på plats servern.  

Tänk på följande innan du kör aktiviteter på samlings nivå. När du har startat kan du inte stoppa aktiviteten från-konsolen.

- Hur många enheter ingår i samlingen?
- Är enheterna anslutna till nätverks anslutningar med låg bandbredd?
- Hur mycket tid behöver den här uppgiften slutföras för alla enheter?

Mer information finns i [hantera samlingar](collections/manage-collections.md).


## <a name="restart-clients"></a>Starta om klienter

Använd Configuration Manager-konsolen för att identifiera klienter som kräver en omstart. Använd sedan en klient meddelande åtgärd för att starta om dem.

> [!Tip]
> Aktivera automatisk klient uppgradering för att hålla dina klienter uppdaterade med mindre ansträngning. Mer information finns i [om automatisk klient uppgradering](upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).

För att identifiera enheter som väntar på en omstart går du till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen och väljer noden **enheter** . Visa sedan statusen för varje enhet i informations fönstret i en ny kolumn med namnet **väntar på omstart**. Varje enhet har ett eller flera av följande värden:

- **Nej**: det finns ingen väntande omstart
- **Configuration Manager**: det här värdet kommer från komponenten för omstart av klienten (RebootCoordinator. log)
- **Byt namn på fil**: det här värdet kommer från Windows repor ting a Pending File Rename operation (HKLM\SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations)
- **Windows Update**: det här värdet kommer från Windows Update Agent rapportering om en väntande omstart krävs för en eller flera uppdateringar (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired)
- **Lägg till eller ta bort funktion**: det här värdet kommer från den Windows-komponentbaserade service rapporteringen som lägger till eller tar bort en Windows-funktion kräver en omstart (HKLM\Software\Microsoft\Windows\CurrentVersion\Component-baserad Servicing\Reboot väntar)

### <a name="create-the-client-notification-to-restart-a-device"></a>Skapa klient meddelandet för att starta om en enhet

1. Välj den enhet som du vill starta om i en samling i noden **enhets samlingar** i-konsolen.
2. Välj **klient meddelande**i menyfliksområdet och välj sedan **starta om**. Ett informations fönster öppnas om omstarten. Välj **OK** för att bekräfta restart-begäran.

När meddelandet tas emot av en klient öppnas ett meddelande fönster i **Software Center** som informerar användaren om omstarten. Som standard sker omstarten efter 90 minuter. Du kan ändra omstarts tiden genom att konfigurera [klient inställningar](../deploy/configure-client-settings.md). Inställningarna för omstarts beteendet finns på fliken [dator omstart](../deploy/about-client-settings.md#computer-restart) i standardinställningarna.


## <a name="configure-the-client-cache"></a><a name="BKMK_ClientCache"></a>Konfigurera klientens cacheminne

Klientcachen lagrar temporära filer för när-klienter installerar program och program. Program uppdateringar använder också-klientcachen, men försöker alltid Ladda ned till cachen oavsett storleks inställning. Konfigurera cacheinställningar, till exempel storlek och plats, när du installerar klienten manuellt när du använder push-installation av klienter eller efter installationen.

Du kan ange cache-mappens storlek med hjälp av klient inställningarna i Configuration Manager-konsolen. Mer information finns i [Inställningar för klient-cache](../deploy/about-client-settings.md#client-cache-settings).

Standard platsen för Configuration Manager-klientcachen är `%windir%\ccmcache` och standard disk utrymmet är 5120 MB.  

> [!IMPORTANT]  
> Kryptera inte mappen som används för klientens cacheminne. Configuration Manager kan inte ladda ned innehåll till en krypterad mapp.  

### <a name="about-the-client-cache"></a>Om klientcachen  

Configuration Manager-klienten hämtar innehållet för nödvändig program vara strax efter distributionens tillgängliga tid men väntar på att köra den tills distributionens schemalagda tid. Vid den schemalagda tiden kontrollerar Configuration Manager klienten om innehållet är tillgängligt i cacheminnet. Om innehållet finns i cacheminnet och det är rätt version, använder klienten det cachelagrade innehållet. När den nödvändiga versionen av innehållet ändras, eller om klienten tar bort innehållet för att göra rummet för ett annat paket, laddar klienten ned innehållet till cacheminnet igen.  

Om klienten försöker ladda ned innehåll för ett program eller program som är större än cachens storlek, så Miss lyckas distributionen på grund av otillräcklig cachestorlek. Klienten genererar status meddelandet 10050 för otillräcklig cachestorlek. Om du ökar cachestorleken senare är resultatet:  

- För ett obligatoriskt program: klienten gör inget nytt försök att ladda ned innehållet automatiskt. Distribuera om paketet och programmet till klienten.  
- För ett obligatoriskt program: klienten försöker automatiskt att ladda ned innehållet när dess klient princip laddas ned.  

Om klienten försöker ladda ned innehåll som är mindre än cachens storlek, men cachen är full, fortsätter alla *nödvändiga* distributioner att försöka igen tills:

- Cache-utrymmet är tillgängligt
- Timeout för hämtning
- Antalet återförsök når gränsen

Om du senare ökar storleken på cacheminnet försöker klienten Ladda ned innehållet igen under nästa återförsöksintervall. Klienten försöker ladda ned innehållet var fjärde timme tills det försöker 18 gånger.  

Cachelagrat innehåll tas inte bort automatiskt. Den finns kvar i cacheminnet i minst en dag efter att klienten har använt det innehållet. Om du konfigurerar innehållet med alternativet att Kvarhåll innehåll i klientcachen, tar klienten inte bort den automatiskt. Om cacheminnet används av innehåll som hämtats under de senaste 24 timmarna och klienten måste ladda ned nytt innehåll, ökar du storleken på cacheminnet eller väljer alternativet för att ta bort beständigt cache-innehåll.

För program, om innehållet för en relaterad distribution för närvarande finns i cacheminnet, hämtar klienten bara nya eller ändrade filer. Relaterade distributioner inkluderar för äldre revisioner av samma distributions typ och ersatta program.

Använd följande procedurer för att konfigurera klientcacheutrymmet under manuell klientinstallation eller efter att klienten har installerats.  

### <a name="configure-the-cache-during-manual-client-installation"></a>Konfigurera cachen under manuell klient installation  

Kör kommandot CCMSetup.exe från installationskällan och ange följande egenskaper, avgränsade med blanksteg:  

- DISABLECACHEOPT  

  - SMSCACHEDIR  

  - SMSCACHEFLAGS  

  - SMSCACHESIZE  

    > [!NOTE]
    > Använd de cache-storlekar som är tillgängliga i **klient inställningarna** i Configuration Manager-konsolen i stället för SMSCACHESIZE. Mer information finns i [Inställningar för klient-cache](../deploy/about-client-settings.md#client-cache-settings).

Mer information om hur du använder dessa kommando rads egenskaper för CCMSetup.exe finns i [om klient installations egenskaper](../deploy/about-client-installation-properties.md).

### <a name="configure-the-cache-during-client-push-installation"></a>Konfigurera cachen under push-installationen av klienten  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .  

2. Välj lämplig plats. På fliken **Start** i menyfliksområdet i gruppen **Inställningar** väljer du **Inställningar för klient installation**och sedan push-installation av **klient**. Växla till fliken **installations egenskaper** .  

3. Ange följande egenskaper, avgränsade med blank steg:  

   - DISABLECACHEOPT  

   - SMSCACHEDIR  

   - SMSCACHEFLAGS  

   - SMSCACHESIZE  

     > [!NOTE]
     > Använd de cache-storlekar som är tillgängliga i **klient inställningarna** i Configuration Manager-konsolen i stället för SMSCACHESIZE. Mer information finns i [Inställningar för klient-cache](../deploy/about-client-settings.md#client-cache-settings).

     Mer information om hur du använder dessa kommando rads egenskaper för CCMSetup.exe finns i [om klient installations egenskaper](../deploy/about-client-installation-properties.md).  

### <a name="configure-the-cache-on-the-client-computer"></a>Konfigurera cachen på klient datorn  

1. På klient datorn öppnar du **Configuration Manager** kontroll panelen.  

2. Växla till fliken **cache** . Ange egenskaper för utrymme och plats. Standardplatsen är `%windir%\ccmcache`.  

3. Om du vill ta bort filerna i cache-mappen väljer du **ta bort filer**.  

### <a name="configure-client-cache-size-in-client-settings"></a>Konfigurera storleken på klientens cacheminne i klient inställningar

Justera storleken på klientens cacheminne utan att behöva installera om klienten. Använd de cachestorlek som är tillgängliga i **klient inställningarna** i Configuration Manager-konsolen. Mer information finns i [Inställningar för klient-cache](../deploy/about-client-settings.md#client-cache-settings).


## <a name="uninstall-the-client"></a><a name="BKMK_UninstalClient"></a>Avinstallera klienten

Du kan avinstallera Configuration Manager klient program varan från en dator genom att använda **CCMSetup.exe** med egenskapen **/Uninstall** . Kör CCMSetup.exe på en enskild dator från kommando tolken eller distribuera ett paket för att avinstallera klienten för en samling datorer.  

> [!NOTE]  
> Det går inte att avinstallera Configuration Manager-klienten från en mobil enhet. Om du måste ta bort Configuration Manager-klienten från en mobil enhet måste du rensa enheten, som tar bort alla data på den mobila enheten.  

1. Öppna en Windows-kommandotolk som administratör. Ändra mappen till den plats där CCMSetup.exe finns, till exempel:`cd %windir%\ccmsetup`

2. Kör följande kommando:`CCMSetup.exe /uninstall`

> [!TIP]  
> Avinstallations processen visar inga resultat på skärmen. Information om hur du kontrollerar att klienten har avinstallerat finns i följande loggfil:`%windir%\ccmsetup\logs\CCMSetup.log`  
>
> Om du behöver vänta tills avinstallationen har slutförts innan du gör något annat, kör du `Wait-Process CCMSetup` i PowerShell. Det här kommandot kan pausa ett skript tills CCMSetup-processen har slutförts.


## <a name="manage-conflicting-records"></a><a name="BKMK_ConflictingRecords"></a>Hantera poster i konflikt

Configuration Manager använder maskin varu identifieraren för att försöka identifiera klienter som kan vara dubbletter och varna dig för poster i konflikt. Om du till exempel installerar om en dator, är maskin varu identifieraren samma men det GUID som används av Configuration Manager kan ändras.  

Configuration Manager löser konflikter automatiskt genom att använda Windows-autentisering av dator kontot eller ett PKI-certifikat från en betrodd källa. När Configuration Manager inte kan lösa en konflikt med dubbla maskin varu identifierare, bestämmer en hierarkisk inställning beteendet.

### <a name="change-the-hierarchy-setting-for-managing-conflicting-records"></a>Ändra hierarkins inställning för att hantera poster i konflikt  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .

1. I menyfliksområdet väljer du **Inställningar för hierarki**.

1. Växla till fliken **klient godkännande och poster i konflikt** och välj ett av följande alternativ:

    - **Lös automatiskt poster i konflikt**
    - **Lösa poster i konflikt manuellt**

### <a name="manually-resolve-conflicting-records"></a>Lösa poster i konflikt manuellt  

1. I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **system status**och väljer noden **motstridiga poster** .  

1. Välj en eller flera poster i konflikt och välj sedan **konflikt**poster.  

1. Välj något av följande alternativ:  

    - **Sammanslagning**: kombinera den nyligen identifierade posten med den befintliga klient posten.  

    - **Ny**: skapa en ny post för klient posten som står i konflikt.  

    - **Blockera**: skapa en ny post för klient posten som står i konflikt, men Markera den som blockerad.  


## <a name="manage-duplicate-hardware-identifiers"></a>Hantera dubbletter av maskin varu identifierare

Du kan ange en lista över maskin varu identifierare som Configuration Manager ignorera för PXE-start och klient registrering. Den här listan hjälper till att lösa två vanliga problem:

1. Många nya enheter innehåller ingen inbyggd Ethernet-port. Tekniker använder ett USB-till-Ethernet-kort för att upprätta en tråd bunden anslutning för distribution av operativ system. Korten delas ofta på grund av kostnad och allmän användbarhet. Platsen använder nätverkskortets MAC-adress för att identifiera enheten. Att återanvända kortet blir problematiskt utan ytterligare administratörs åtgärder mellan varje distribution. Om du vill återanvända kortet i det här scenariot utesluter du dess MAC-adress.

2. När SMBIOS-attributet ska vara unikt har vissa särskilda maskin varu enheter dubbla identifierare. Undanta den här dubblett identifieraren och Använd den unika MAC-adressen för varje enhet.

Använd följande process för att lägga till maskin varu identifierare för Configuration Manager att ignorera:

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .

2. På fliken **Start** i menyfliksområdet väljer du **Inställningar för hierarki**i gruppen **platser** .

3. Växla till fliken **klient godkännande och poster i konflikt** . Om du vill lägga till nya maskin varu identifierare väljer du **Lägg till** i avsnittet **dubbletter av maskin varu identifierare** .

> [!TIP]
> Från och med version 1910 använder du följande PowerShell-cmdlets för att automatisera hanteringen av duplicerade maskin varu identifierare:<!-- 4852819 -->
>
> - New-CMDuplicateHardwareIdGuid
> - Remove-CMDuplicateHardwareIdGuid
> - New-CMDuplicateHardwareIdMacAddress
> - Remove-CMDuplicateHardwareIdMacAddress


## <a name="start-policy-retrieval"></a><a name="BKMK_PolicyRetrieval"></a>Starta princip hämtning

En Configuration Manager-klient laddar ned sin klient princip enligt ett schema som du konfigurerar som klient inställning. Du kan också starta hämtning av princip på begäran från klienten. Till exempel för fel sökning eller testnings situationer.  

- [Klientmeddelande](#bkmk_policy-notify)
- [Kontroll panelen för klienten](#bkmk_policy-manual)
- [Support Center](#bkmk_policy-support)
- [Ett skript](#bkmk_policy-script)

### <a name="start-client-policy-retrieval-with-client-notification"></a><a name="bkmk_policy-notify"></a>Starta klient princip hämtning med klient meddelande  

1. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen och välj **enheter**.  

1. Välj den enhet som du vill hämta principen för. På fliken **Start** i menyfliksområdet väljer du **klient meddelande**i gruppen **enhet** och väljer sedan **Ladda ned dator princip**.  

    > [!NOTE]  
    > Du kan också använda klient meddelanden för att starta princip hämtning för alla enheter i en samling.  

### <a name="start-client-policy-retrieval-from-the-configuration-manager-client-control-panel"></a><a name="bkmk_policy-manual"></a>Starta klient princip hämtning från Configuration Manager klient på kontroll panelen

1. Öppna **Configuration Manager** kontroll panelen på datorn.  

2. Växla till fliken **åtgärder** . Välj **princip för hämtning av dator princip & utvärderings cykel** för att starta dator principen och välj sedan **Kör nu**.  

3. Klicka på **OK** för att bekräfta prompten.  

4. Upprepa föregående steg för alla andra åtgärder. Till exempel kan **hämtning av användar principer & utvärderings cykel** för användar klient inställningar.  

### <a name="start-client-policy-retrieval-with-support-center"></a><a name="bkmk_policy-support"></a>Starta klient princip hämtning med Support Center

Använd Support Center för att begära och Visa klient princip. Mer information finns i [Support Center Reference](../../support/support-center-ui-reference.md#bkmk_support-policy).

### <a name="start-client-policy-retrieval-by-script"></a><a name="bkmk_policy-script"></a>Starta klient princip hämtning med skript  

1. Öppna en skript redigerare, till exempel anteckningar eller Windows PowerShell ISE.  

2. Kopiera och infoga följande exempel på PowerShell-kod<!-- SCCMDocs#1591 --> till filen:  

    ```PowerShell
    $trigger = "{00000000-0000-0000-0000-000000000021}"
    Invoke-WmiMethod -Namespace root\ccm -Class sms_client -Name TriggerSchedule $trigger
    ```  

    > [!TIP]
    > Mer information om schema-ID: n finns i [meddelande-ID](../../support/send-schedule-tool.md#bkmk_sendschedule-guids).

3. Spara filen med fil namns tillägget. ps1.  

4. Kör skriptet på klienten.
