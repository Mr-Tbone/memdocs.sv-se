---
title: Hantera distributions platser
titleSuffix: Configuration Manager
description: Använd distributions platser som värd för det innehåll som du distribuerar till enheter och användare.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d1d93dd446a65fda0b259bb10e0c944780d41059
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347099"
---
# <a name="install-and-configure-distribution-points-in-configuration-manager"></a>Installera och konfigurera distributions platser i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Installera Configuration Manager distributions platser som värd för de innehållsfiler som du distribuerar till enheter och användare. Skapa distributions plats grupper för att förenkla hanteringen av distributions platser och hur du distribuerar innehåll till distributions platser.  

Du *installerar en ny distributions plats* med hjälp av installations guiden. Mer information finns i [installera en distributions plats](#bkmk_install). Redigera egenskaperna för distributions platsen om du vill *Hantera egenskaperna för en befintlig distributions plats*. Mer information finns i [Konfigurera en distributions plats](#bkmk_configs).

Konfigurera de flesta distributions plats inställningarna med någon av metoderna. Några inställningar är bara tillgängliga när du antingen installerar eller redigerar, men inte båda:  

- Inställningar som endast är tillgängliga när du installerar en distributions plats:  

    - **Tillåt Configuration Manager att installera IIS på distributions plats datorn**

    - **Konfigurera enhets utrymmes inställningar för distributions platsen**  

- Inställningar som endast är tillgängliga när du redigerar egenskaperna för en distributions plats:  

    - **Hantera grupp relationer för distributions platser**  

    - **Visa innehåll som har distribuerats till distributions platsen**  

    - **Konfigurera hastighets begränsningar för data överföringar till distributions platser**  

    - **Konfigurera scheman för data överföringar till distributions platser**  


## <a name="install-a-distribution-point"></a><a name="bkmk_install"></a>Installera en distributions plats  

Välj en plats system server som en distributions plats innan innehåll kan göras tillgängligt för klient datorer. Tilldela en distributions plats till minst en [avgränsnings grupp](boundary-groups.md#distribution-points) innan lokala klient datorer kan använda distributions platsen som en innehålls käll plats. Lägg till distributions plats rollen till en ny plats system Server eller Lägg till den på en befintlig plats system Server.

### <a name="prerequisites"></a><a name="bkmk_install-prereq"></a>Krav

När du installerar en ny distributions plats använder du en installations guide som vägleder dig genom de tillgängliga inställningarna. Innan du börjar bör du tänka på följande:  

- Du måste ha följande säkerhets behörigheter för att skapa och konfigurera en distributions plats:  

    - **Läst** för **distributions plats** objekt  

    - **Kopiera till distributions plats** för **distributions plats** objekt  

    - **Ändra** för objektet **plats**  

    - **Hantera certifikat för distribution av operativ system** för objektet **plats**  

- Installera Internet Information Services (IIS) på Windows-servern som är värd för distributions platsen. Eller, när du installerar plats system rollen, kan Configuration Manager installera och konfigurera IIS åt dig.  

### <a name="procedure-to-install-a-distribution-point"></a><a name="bkmk_install-procedure"></a>Procedur för att installera en distributions plats  

Använd den här proceduren för att lägga till en ny distributions plats. Information om hur du ändrar konfigurationen för en befintlig distributions plats finns i avsnittet [Konfigurera en distributions plats](#bkmk_configs) .  

Börja med den allmänna proceduren för att [Installera plats system roller](install-site-system-roles.md). Välj **distributions plats** rollen på sidan **urval för system roll** i guiden skapa plats system Server. Den här åtgärden lägger till följande sidor i guiden:  

- [Distributionsplats](#bkmk_config-general)
- [Kommunikation](#bkmk_config-comm)
- [Enhets inställningar](#bkmk_config-drive)
- [Mottagar distributions plats](#bkmk_config-pull)
- [PXE-inställningar](#bkmk_config-pxe)
- [Multicast](#bkmk_config-multicast)
- [Innehållsvalidering](#bkmk_config-valid)
- [Gränser grupper](#bkmk_config-boundary)

> [!Important]  
> Följande inställningar är bara tillgängliga när du installerar en distributions plats:  
>
> - **Tillåt Configuration Manager att installera IIS på distributions plats datorn**  
>
> - **Konfigurera enhets utrymmes inställningar för distributions platsen**  

Mer information om de sidor i guiden som är tilldelad distributions plats rollen finns i avsnittet [Konfigurera en distributions plats](#bkmk_configs) . Om du till exempel vill installera distributions platsen som en [mottagar distributions plats](#bkmk_config-pull)väljer du alternativet för att **tillåta att den här distributions platsen hämtar innehåll från andra distributions platser**. Gör sedan de ytterligare konfigurationer som mottagar distributions platser kräver.  

När du har slutfört guiden skapa plats system Server lägger platsen till distributions plats rollen till plats system servern.  


## <a name="manage-distribution-point-groups"></a><a name="bkmk_manage"></a>Hantera distributions plats grupper  

Distributionsplatsgrupper är en logisk gruppering av distributionsplatser för innehållsdistribution. Använd de här grupperna för att hantera och övervaka innehåll från en central plats för distributions platser som sträcker sig över flera platser. Tänk på följande:

- Lägg till en eller flera distributions platser från valfri plats i hierarkin till en distributions plats grupp.  

- Lägg till en distributions plats i fler än en distributions plats grupp.  

- När du distribuerar innehåll till en distributions plats grupp, Configuration Manager distribuerar innehållet till alla distributions platser som är medlemmar i gruppen.  

- Om du lägger till en distributions plats i gruppen efter en första innehålls distribution distribuerar Configuration Manager automatiskt innehållet till den nya distributions plats medlemmen.  

- Koppla en samling till en distributions plats grupp. När du distribuerar innehåll till samlingen bestämmer Configuration Manager vilka grupper som är associerade med samlingen. Sedan distribueras innehållet till alla distributions platser som är medlemmar i dessa grupper.  

    > [!NOTE]  
    > När du har distribuerat innehållet till en samling och sedan associerar samlingen med en ny distributions plats grupp måste du distribuera om innehållet till samlingen innan innehållet distribueras till den nya distributions plats gruppen.  

I nästa avsnitt visas procedurerna för följande åtgärder för att hantera distributions plats grupper:  

- [Skapa och konfigurera en ny distributions plats grupp](#bkmk_dpgroup-create)
- [Ändra en befintlig distributions plats grupp](#bkmk_dpgroup-modify)
- [Lägg till valda distributions platser i befintliga distributions plats grupper](#bkmk_dpgroup-addexist)

### <a name="procedure-to-create-and-configure-a-new-distribution-point-group"></a><a name="bkmk_dpgroup-create"></a>Procedur för att skapa och konfigurera en ny distributions plats grupp  

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** och väljer noden **distributions plats grupper** .  

2. I menyfliksområdet väljer du **Skapa grupp**.  

3. I fönstret Skapa ny distributions plats grupp anger du **namnet**och eventuellt en **Beskrivning** av gruppen.  

4. På fliken **medlemmar** väljer du **Lägg till**.  

5. I fönstret Lägg till distributions platser väljer du en eller flera distributions platser som ska läggas till som medlemmar i gruppen. Välj sedan **OK**.  

6. Vid behov växlar du till fliken **samlingar** i fönstret Skapa ny distributions plats grupp och väljer **Lägg till**.  

7. I fönstret Välj samlingar väljer du de samlingar som ska associeras med distributions plats gruppen och väljer sedan **OK**.  

8. I fönstret Skapa ny distributions plats grupp väljer du **OK** för att skapa gruppen.  

#### <a name="create-a-new-group-from-an-existing-distribution-point"></a>Skapa en ny grupp från en befintlig distributions plats

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** och väljer noden **distributions platser** . Välj en eller flera distributions platser som ska läggas till i en ny distributions plats grupp.  

2. I menyfliksområdet väljer du **Lägg till markerade objekt**och väljer sedan **Lägg till markerade objekt i ny distributions plats grupp**.  

Den här processen fyller automatiskt i fliken **medlemmar** i fönstret Skapa ny distributions plats grupp med de valda servrarna.

### <a name="procedure-to-modify-an-existing-distribution-point-group"></a><a name="bkmk_dpgroup-modify"></a>Procedur för att ändra en befintlig distributions plats grupp  

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** och väljer noden **distributions plats grupper** .  

2. Välj en befintlig distributions plats grupp som ska ändras. I menyfliksområdet väljer du **Egenskaper**.  

3. Om du vill associera nya samlingar med den här gruppen växlar du till fliken **samlingar** och väljer **Lägg till**. Välj samlingarna och välj sedan **OK**.  

4. Om du vill lägga till nya distributions platser i den här gruppen växlar du till fliken **medlemmar** och väljer **Lägg till**. Välj distributions platser och välj sedan **OK**.  

5. Välj **OK** för att spara ändringarna i distributions plats gruppen.  

### <a name="procedure-to-add-selected-distribution-points-to-existing-distribution-point-groups"></a><a name="bkmk_dpgroup-addexist"></a>Procedur för att lägga till valda distributions platser i befintliga distributions plats grupper  

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** och väljer noden **distributions platser** . Välj en eller flera distributions platser som ska läggas till i en befintlig grupp.  

2. I menyfliksområdet väljer du **Lägg till markerade objekt**och väljer sedan **Lägg till markerade objekt i befintliga distributions plats grupper**.  

3. I **tillgängliga distributions plats grupper**väljer du de grupper som de valda distributions platserna läggs till som medlemmar i. Välj sedan **OK**.  


## <a name="reassign-a-distribution-point"></a><a name="bkmk_reassign"></a>Omtilldela en distributions plats

<!-- 1306937 -->

Många kunder har stora Configuration Manager infrastrukturer och minskar de primära eller sekundära platserna för att förenkla sin miljö. De måste fortfarande behålla distributions platser på avdelnings kontor för att kunna hantera innehåll till hanterade klienter. Dessa distributions platser innehåller ofta flera terabyte eller mer av innehållet. Det här innehållet är kostsamt i fråga om tid och nätverks bandbredd för att distribuera till dessa fjärrservrar.

Med den här funktionen kan du omtilldela en distributions plats till en annan primär plats utan att distribuera om innehållet. Den här åtgärden uppdaterar plats system tilldelningen och behåller allt innehåll på servern. Om du behöver tilldela om flera distributions platser bör du först utföra den här åtgärden på en enda distributions plats. Fortsätt sedan med ytterligare servrar en i taget.

> [!IMPORTANT]  
> Mål servern kan bara vara värd för distributions plats rollen. Om plats system servern är värd för en annan Configuration Manager Server roll, till exempel platsen för tillståndsmigrering, kan du inte omtilldela distributions platsen. Det går inte att omtilldela en distributions plats för molnet.

Innan du omtilldelar en distributions plats lägger du till dator kontot för mål plats servern i den lokala administratörs gruppen på mål distributions plats servern.

Följ dessa steg för att omtilldela en distributions plats:

1. I Configuration Manager-konsolen ansluter du till den centrala administrations platsen.  

2. Gå till arbets ytan **Administration** och välj noden **distributions platser** .  

3. Högerklicka på mål distributions platsen och välj **omtilldela distributions plats**.  

4. Välj den mål plats Server och plats kod som du vill tilldela om distributions platsen.  

Övervaka omtilldelningen på samma sätt som när du lägger till en ny roll. Den enklaste metoden är att uppdatera konsolens vy efter några minuter. Lägg till kolumnen plats kod i vyn. Det här värdet ändras när Configuration Manager tilldelar om servern. Om du försöker utföra en annan åtgärd på mål servern innan du uppdaterar konsolen visas felet "objektet hittades inte". Se till att processen är slutförd och uppdatera konsolen innan du påbörjar andra åtgärder på servern.

Uppdatera Server certifikatet när du har omtilldelat en distributions plats. Den nya plats servern måste kryptera det här certifikatet igen med dess offentliga nyckel och lagra det i plats databasen. Mer information finns i avsnittet **skapa ett självsignerat certifikat eller importera ett PKI-klientcertifikat (Public Key Infrastructure) för distributions plats** inställningen på fliken [Allmänt](#bkmk_config-general) i egenskaperna för distributions platsen.

- För PKI-certifikat behöver du inte skapa ett nytt certifikat. Importera samma. PFX och ange lösen ordet.  

- För självsignerade certifikat, justera förfallo datum och-tid för att uppdatera det.  

- Om du inte uppdaterar certifikatet, bevarar distributions platsen fortfarande innehåll, men följande funktioner fungerar inte:  

    - Meddelanden om innehålls verifiering (Distmgr. log visar att det inte kan dekryptera certifikatet)  

    - PXE-stöd för klienter  

### <a name="tips"></a>Tips

- Utför den här åtgärden från den centrala administrations platsen. Den här metoden hjälper till med replikering till de primära platserna.  

- Distribuera inte innehåll till mål servern och försök sedan att tilldela det igen. Distribution av innehålls aktiviteter som pågår kan Miss lyckas under omtilldelnings processen, men återförsök görs per normal.  

- Om servern också är en Configuration Manager-klient, se till att även tilldela om klienten till den nya primära platsen. Det här steget är särskilt viktigt för mottagar distributions platser, som använder klient komponenter för att ladda ned innehåll.  

- Den här processen tar bort distributions platsen från den gamla platsens standard gränser grupp. Om det behövs måste du manuellt lägga till den i den nya platsens standard gränser grupp. Alla andra gränser grupp tilldelningar förblir desamma.  


## <a name="maintenance-mode"></a><a name="bkmk_maint"></a>Underhålls läge

<!--3555754-->

Från och med version 1902 kan du ange en distributions plats i underhålls läge. Aktivera underhålls läge när du installerar program uppdateringar eller gör ändringar av maskin varan på servern.

Även om distributions platsen är i underhålls läge, har den följande beteenden:

- Webbplatsen distribuerar inget innehåll till den.  

- Hanterings platser returnerar inte platsen för den här distributions platsen till klienter.

- När du uppdaterar platsen uppdateras även en distributions plats i underhålls läge.

- Distributions plats egenskaperna är skrivskyddade. Du kan till exempel inte ändra certifikatet eller lägga till gränser grupper.  

- Alla schemalagda aktiviteter, t. ex. innehålls validering, körs fortfarande i samma schema.

Var försiktig med att aktivera underhålls läge på fler än en distributions plats. Den här åtgärden kan orsaka att prestanda påverkas av andra distributions platser. Beroende på dina gränser för konfiguration av gränser kan klienterna ha ökat nedladdnings tiderna eller kan inte hämta innehåll.

Underhålls läget bör inte vara ett långsiktigt tillstånd för en distributions plats. För åtgärder med lång varaktighet bör du först ta bort distributions plats rollen.

> [!NOTE]
> När en distributions plats är i underhålls läge utför du inte följande åtgärder:<!-- SCCMDocs-pr #4699 -->
>
> - Ta bort roll
> - Omtilldela distributions plats

### <a name="enable-maintenance-mode"></a>Aktivera underhållsläge

För att kunna använda en distributions plats i underhålls läge kräver ditt användar konto behörigheten **ändra** för **plats** klassen. Till exempel har den här behörigheten **infrastruktur administratör** och **Fullständig administratör** inbyggda roller.<!-- SCCMDocs-pr issue #3407 -->

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen.  

2. Välj noden **distributions platser** .  

3. Välj mål distributions plats och välj **Aktivera underhålls läge** från menyfliksområdet.  

Om du vill visa distributions platsernas aktuella status lägger du till kolumnen "underhålls läge" i noden **distributions platser** i-konsolen.

Mer information om hur du automatiserar den här processen med Configuration Manager SDK finns [i SetDPMaintenanceMode-metoden i klassen SMS_DistributionPointInfo](../../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md).


## <a name="configure-a-distribution-point"></a><a name="bkmk_configs"></a>Konfigurera en distributions plats  

Enskilda distributions platser har stöd för en mängd olika konfigurationer. Alla typer av distributions platser stöder dock inte alla konfigurationer. Moln distributions platser stöder till exempel inte PXE-eller multicast-aktiverade distributioner. Mer information om vissa begränsningar finns i följande artiklar:  

- [Använd en moln distributions plats](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

- [Använda en mottagardistributionsplats](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)  

I följande avsnitt beskrivs distributions plats konfigurationerna när du [installerar en ny](#bkmk_install-procedure) eller [redigerar en befintlig](#bkmk_change-procedure):  

- [Allmänna inställningar](#bkmk_config-general)
- [Kommunikation](#bkmk_config-comm)
- [Enhets inställningar](#bkmk_config-drive)
- [Brand Väggs inställningar](#bkmk_firewall)
- [Mottagar distributions plats](#bkmk_config-pull)
- [PXE-inställningar](#bkmk_config-pxe)
- [Multicast](#bkmk_config-multicast)
- [Innehållsvalidering](#bkmk_config-valid)
- [Gränser grupper](#bkmk_config-boundary)

#### <a name="procedure-to-change-a-distribution-point"></a><a name="bkmk_change-procedure"></a>Procedur för att ändra en distributions plats

1. I Configuration Manager-konsolen går du till arbets ytan **Administration** och väljer noden **distributions platser** .  

2. Välj den distributions plats som ska konfigureras. I menyfliksområdet väljer du **Egenskaper**.  

3. Använd informationen i följande avsnitt när du redigerar egenskaperna för distributions platsen.  

4. När du har gjort önskade ändringar väljer du **OK** för att spara inställningarna och stänga egenskaperna för distributions platsen.  

### <a name="general"></a><a name="bkmk_config-general"></a>Redovisningsjournalmallar  

> [!Note]  
> I version 1902 och tidigare har den här sidan ytterligare inställningar för HTTP/HTTPS och certifikat. Från och med version 1906 finns de här inställningarna nu på sidan [kommunikation](#bkmk_config-comm) .

Följande inställningar finns på sidan **distributions plats** i guiden skapa plats system Server och fliken **Allmänt** i fönstret Egenskaper för distributions plats:  

- **Beskrivning**: en valfri beskrivning av den här distributions plats rollen.  

- **Installera och konfigurera IIS om det krävs av Configuration Manager**: om IIS inte redan är installerat på servern kan Configuration Manager installera och konfigurera den. Configuration Manager kräver IIS på alla distributions platser. Om du inte väljer den här inställningen och IIS inte är installerat på servern måste du först installera IIS innan Configuration Manager kan installera distributions platsen.  

    > [!NOTE]  
    > Det här alternativet finns bara på sidan **distributions plats** i guiden skapa plats system Server. Den är bara tillgänglig när du [installerar en ny distributions plats](#bkmk_install-procedure).  

- **Aktivera och konfigurera BranchCache för den här distributions platsen**: Välj den här inställningen om du vill låta Configuration Manager Konfigurera Windows BranchCache på distributions plats servern. Mer information finns i [BranchCache](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

- **Justera nedladdnings hastigheten så att den outnyttjade nätverks bandbredden används (Windows LEDBAT)**<!--1358112-->: Startar i version 1806 och aktiverar distributions platser för att använda nätverks överbelastnings kontroll. Mer information finns i [Windows-LEDBAT](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat). Minimi krav för LEDBAT-support:<!-- SCCMDocs issue 883 -->  

    - Configuration Manager version 1806 (allmän utgåva)  

        - Windows Server, version 1709 eller senare  

    - Configuration Manager version 1806 med Samlad uppdatering (4462978) eller senare  

        - Windows Server, version 1709 eller senare
        - Windows Server 2016 med följande uppdateringar:
           - Kumulativ uppdatering KB4132216, lanserad 21 juni 2018 eller en senare kumulativ uppdatering.
           - Underhålls stack uppdatering KB4284833, publicerad 18 maj 2018 eller en senare underhålls stack uppdatering.

    - Configuration Manager version 1810 eller senare:

        - Windows Server, version 1709 eller senare
        - Windows Server 2016 med följande uppdateringar:
           - Kumulativ uppdatering KB4132216, lanserad 21 juni 2018 eller en senare kumulativ uppdatering.
           - Underhålls stack uppdatering KB4284833, publicerad 18 maj 2018 eller en senare underhålls stack uppdatering.
        - Windows Server 2019  

- **Aktivera den här distributions platsen för förinstallerat innehåll**: med den här inställningen kan du lägga till innehåll på servern innan du distribuerar program vara. Eftersom innehållsfilerna redan finns i innehålls biblioteket överförs de inte över nätverket när du distribuerar program varan. Mer information finns i [förinstallerat innehåll](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent).  

- **Tillåt att den här distributions platsen används som Microsoft-ansluten cache-server**: från och med version 1906 kan du installera en Microsoft-ansluten cache-server på dina distributions platser. Genom att cachelagra det här innehållet lokalt kan dina klienter dra nytta av leverans optimerings funktionen, men du kan skydda WAN-länkar. Mer information, inklusive beskrivning av ytterligare inställningar, finns [i Microsoft Connected cache i Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).


### <a name="communication"></a><a name="bkmk_config-comm"></a>Uppgifter

> [!Note]  
> Från och med version 1906 finns följande inställningar på fliken **kommunikation** . I version 1902 och tidigare finns de här inställningarna på fliken [Allmänt](#bkmk_config-general) .

Följande inställningar finns på sidan **kommunikation** i guiden skapa plats system Server och i fönstret Egenskaper för distributions plats:  

- **Konfigurera hur klient enheter ska kommunicera med distributions platsen**: det finns fördelar och nack delar med att använda **http** eller **https**. Mer information finns i [rekommenderade säkerhets metoder för innehålls hantering](../../../plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

- **Tillåt att klienter ansluter anonymt**: den här inställningen anger om distributions platsen tillåter anonyma anslutningar från Configuration Manager klienter till innehålls biblioteket.  

<!-- I don't think this applies any more, but commenting instead of removing just in case.
    > [!Important]  
    > If you don't use this setting, apply the changes described in Microsoft Knowledge Base article [2619572](https://support.microsoft.com/help/2619572/) on Windows 7 clients. Otherwise repair of Windows Installer applications can fail.  
    >
    > When you deploy a Windows Installer application, the Configuration Manager client downloads the file to its local cache. The client eventually removes the files after the installation finishes. The Configuration Manager client updates the Windows Installer source list for the application. It sets the content path to the content library on associated distribution points. Later, if you try to repair the application on the device, MSIExec attempts to access the content path by using an anonymous user.  
    >
    > After you install the update on clients and modify the documented registry key, MSIExec accesses the content path by using the signed-in user account.  
 -->

- **Skapa ett självsignerat certifikat eller importera ett PKI-klientcertifikat**: Configuration Manager använder det här certifikatet i följande syfte:  

    - Den autentiserar distributions platsen för en hanterings plats innan distributions platsen skickar status meddelanden.  

    - När du **aktiverar PXE-stöd för klienter** på sidan **PXE-inställningar** skickar distributions platsen den till datorer som PXE-start. Dessa datorer använder sedan den för att ansluta till en hanterings plats under distributions processen för operativ systemet.  

    När du konfigurerar alla hanterings platser på platsen för HTTP väljer du alternativet för att **skapa ett självsignerat certifikat**. När du konfigurerar hanterings platserna för HTTPS använder du alternativet för att **Importera certifikat** från PKI.  

    Om du vill importera certifikatet bläddrar du till en giltig PKCS #12-fil (Public Key Cryptography Standard). Den här PFX-eller CER-filen har PKI-certifikatet med följande krav för Configuration Manager:  

    - Den avsedda användningen inkluderar klientautentisering  

    - Aktivera den privata nyckeln som ska exporteras  

    > [!TIP]  
    > Det finns inga särskilda krav på certifikatets ämne eller alternativt namn för certifikat mottagare (SAN). Om det behövs använder du samma certifikat för flera distributions platser.  

    Mer information om certifikat kraven finns i krav för [PKI-certifikat](../../../plan-design/network/pki-certificate-requirements.md).  

    Ett exempel på distribution av det här certifikatet finns i [distribuera klient certifikatet för distributions platser](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

### <a name="drive-settings"></a><a name="bkmk_config-drive"></a>Enhets inställningar  

> [!NOTE]  
> De här alternativen är bara tillgängliga när du installerar en ny distributions plats.  

Ange enhets inställningarna för distributions platsen. Konfigurera upp till två disk enheter för innehålls biblioteket och två disk enheter för paket resursen. Configuration Manager kan använda ytterligare enheter när de första två når den konfigurerade enhets utrymmes reserven. På sidan **enhets inställningar** konfigureras prioriteten för disk enheterna och mängden ledigt disk utrymme som finns kvar på varje disk enhet.  

- **Reserverat enhets utrymme (MB)**: det här värdet avgör mängden ledigt utrymme på en enhet innan Configuration Manager väljer en annan enhet och fortsätter med kopierings processen till den enheten. Innehållsfiler kan omfatta flera enheter.  

- **Innehålls platser**: ange platser för innehålls biblioteket och paket resursen på den här distributions platsen. Som standard är alla innehålls platser inställda på **Automatisk**. Configuration Manager kopierar innehåll till den primära innehålls platsen tills mängden ledigt utrymme når det angivna värdet för **reserverat enhets utrymme (MB)**. När du väljer **Automatisk**, Configuration Manager anger den primära innehålls platsen till disk enheten med mest disk utrymme vid installationen. Den anger de sekundära platserna till disk enheten med det näst mest lediga disk utrymmet. När den primära och den sekundära platsen når enhets utrymmes reserven, Configuration Manager väljer en annan tillgänglig enhet med mest ledigt disk utrymme för att fortsätta kopierings processen.  

> [!Tip]  
> Om du vill förhindra Configuration Manager att installera på en viss enhet skapar du en tom fil med namnet **No_sms_on_drive. SMS** och kopierar den till enhetens rotmapp innan du installerar distributions platsen.  

Mer information finns i [innehålls biblioteket](../../../plan-design/hierarchy/the-content-library.md).

### <a name="firewall-settings"></a><a name="bkmk_firewall"></a>Brand Väggs inställningar

Distributions platsen måste ha följande regler för inkommande trafik som kon figurer ATS i Windows-brand väggen:

- Windows Management Instrumentation (DCOM-in)
- Windows Management Instrumentation (WMI-in)

Utan de här reglerna får klienterna fel 0x801901F4 i DataTransferService. log vid försök att ladda ned innehåll.

### <a name="pull-distribution-point"></a><a name="bkmk_config-pull"></a>Mottagar distributions plats  

När du **aktiverar den här distributions platsen för att hämta innehåll från andra distributions platser**blir den en mottagar distributions plats. Du ändrar beteendet för hur distributions platsen hämtar det innehåll som du distribuerar till den. Mer information finns i [använda en mottagar distributions plats](../../../plan-design/hierarchy/use-a-pull-distribution-point.md).

För varje mottagar distributions plats som du konfigurerar anger du en eller flera käll distributions platser som innehållet ska hämtas från:  

- Välj **Lägg till**och välj sedan en eller flera av de tillgängliga distributions platserna som källor.  

- Använd pilknapparna för att justera prioriteten. När mottagar distributions platsen försöker överföra innehåll är prioriteten den ordning i vilken den kontaktar käll distributions platserna. Den kontaktar först distributions platser med det lägsta värdet.  

### <a name="pxe"></a><a name="bkmk_config-pxe"></a>PXE  

Ange om PXE ska aktive ras på distributions platsen. Använd PXE för att starta operativ Systems distribution på klienter. Mer information om hur du använder PXE i Configuration Manager finns i [använda PXE för att distribuera Windows över nätverket](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

När du aktiverar PXE, Configuration Manager installerar Windows Deployment Services (WDS) på-servern, om det behövs. WDS är den tjänst som utför PXE-starten för att installera operativ system. När du har slutfört guiden för att skapa distributions platsen, Configuration Manager installerar en provider i WDS som använder PXE-startfunktionerna.

Från och med version 1806 kan du aktivera PXE på en distributions plats utan WDS.

Välj alternativet för att **Aktivera PXE-stöd för klienter**och konfigurera sedan följande inställningar:  

> [!Note]  
> Välj **Ja** i dialog rutan **Granska nödvändiga portar för PXE** för att bekräfta att du vill aktivera PXE. Configuration Manager konfigurerar automatiskt standard portarna i Windows-brandväggen. Konfigurera portarna manuellt om du använder en annan brand vägg.  
>
> Om du installerar WDS och DHCP på samma server konfigurerar du WDS så att den lyssnar på en annan port. Som standard lyssnar DHCP på samma port. Mer information finns i [Att tänka på när du har WDS och DHCP på samma server](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP).  

- **Tillåt att den här distributions platsen svarar på inkommande PXE-begäranden**: Ange om WDS ska aktive ras för att svara på PXE-begäranden. Använd den här inställningen för att aktivera och inaktivera tjänsten utan att ta bort PXE-funktionen från distributions platsen.  

- **Aktivera**stöd för okända datorer: Ange om du vill aktivera stöd för datorer som Configuration Manager inte hanterar. Mer information finns i [förbereda för okända dator distributioner](../../../../osd/get-started/prepare-for-unknown-computer-deployments.md).  

- **Aktivera en PXE-svarare utan Windows Deployment-tjänst**: från och med version 1806 aktiverar det här alternativet en PXE-svarare på distributions platsen, vilket inte kräver WDS. Denna PXE-svarare stöder IPv6-nätverk. Om du aktiverar det här alternativet på en distributions plats som redan är PXE-aktiverad, pausar Configuration Manager WDS-tjänsten. Om du inaktiverar det här alternativet, men fortfarande **aktiverar PXE-stöd för klienter**, aktiverar distributions platsen WDS igen.<!--1357580-->  

    > [!Note]  
    > I version 1810 och tidigare stöds inte PXE-svarare utan WDS på servrar som också kör en DHCP-server.
    >
    > Från och med version 1902 kan den nu finnas på samma server som DHCP-tjänsten när du aktiverar en PXE-svarare på en distributions plats utan Windows Deployment-tjänst. <!--3734270-->  

- **Kräv lösen ord när datorer använder PXE**: om du vill ge ytterligare säkerhet för PXE-distributioner anger du ett starkt lösen ord.  

- **Mappning mellan användare och enhet**: Ange hur du vill att distributions platsen ska koppla användare till mål datorn för PXE-distributioner. Välj ett av följande alternativ:  

  - **Tillåt mappning mellan användare och enhet med automatiskt godkännande**: Välj den här inställningen om du vill koppla användare till mål datorn automatiskt utan att vänta på godkännande.  

  - **Tillåt mappning mellan användare och enhet väntar på administratörs godkännande**: Välj den här inställningen om du vill vänta på godkännande från en administrativ användare innan användarna kopplas till mål datorn.  

  - **Tillåt inte mappning mellan användare och enhet**: Välj den här inställningen för att ange att användare inte är kopplade till mål datorn. Den här inställningen är standardinställningen.  

    Mer information om mappning mellan användare och enhet finns i [Länka användare och enheter med mappning mellan användare och enhet](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

- **Nätverks gränssnitt**: ange att distributions platsen svarar på PXE-begäranden från alla nätverks gränssnitt eller från vissa nätverks gränssnitt. Om distributions platsen svarar på vissa nätverks gränssnitt anger du MAC-adressen för varje nätverks gränssnitt.  

    > [!Note]  
    > När du ändrar nätverks gränssnittet måste du starta om WDS-tjänsten för att kontrol lera att den sparar konfigurationen korrekt. Från och med version 1806, när du använder PXE responder-tjänsten, startar du om **CONFIGMGR PXE responder-tjänsten** (SccmPxe).<!--SCCMDocs issue 642-->  

- **Ange svars fördröjning för PXE-server (sekunder)**: när du använder flera PXE-servrar anger du hur länge den här PXE-aktiverade distributions platsen ska vänta innan den svarar på dator begär Anden. Som standard svarar den Configuration Manager PXE-aktiverade distributions platsen direkt.  

### <a name="multicast"></a><a name="bkmk_config-multicast"></a>Multicast  

Ange om multicast ska aktive ras på distributions platsen. Multicast-distributioner sparar nätverks bandbredd genom att samtidigt skicka data till flera Configuration Manager-klienter. Utan multicast skickar servern en kopia av data till varje klient via en separat anslutning. Mer information om hur du använder multicast för OS-distribution finns i [använda multicast för att distribuera Windows via nätverket](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).

När du aktiverar multicast Configuration Manager installeras Windows Deployment Services (WDS) på-servern om det behövs.  

Välj alternativet för att **göra det möjligt för multicast att samtidigt skicka data till flera klienter**och konfigurera sedan följande inställningar:  

- **Konto för multicast-anslutning**: Ange det konto som ska användas när du konfigurerar Configuration Manager databas anslutningar för multicast. Mer information finns i kontot för [multicast-anslutning](../../../plan-design/hierarchy/accounts.md#multicast-connection-account).  

- **Inställningar för multicast-adress**: Ange IP-adresserna för att skicka data till mål datorerna. Som standard hämtar den IP-adressen från en DHCP-server som är aktive rad för att distribuera multicast-adresser. Beroende på nätverks miljö kan du ange ett intervall med IP-adresser från 239.0.0.0 via 239.255.255.255.  

    > [!IMPORTANT]  
    > De IP-adresser som du konfigurerar måste vara tillgängliga för de mål datorer som begär operativ system avbildningen. Kontrol lera att routrar och brand väggar tillåter multicast-trafik mellan mål datorn och distributions platsen.  

- **UDP-port intervall för multicast**: Ange det intervall av UDP-portar som används för att skicka data till mål datorerna.  

    > [!IMPORTANT]  
    > UDP-portarna måste vara tillgängliga för de mål datorer som begär operativ system avbildningen. Kontrol lera att routrar och brand väggar tillåter multicast-trafik mellan mål datorn och plats servern.  

- **Högsta antal klienter**: Ange det högsta antalet mål datorer som kan hämta operativ system avbildningen från den här distributions platsen.  

- **Aktivera schemalagd multicast**: ange hur Configuration Manager styr när operativ system ska börja distribueras till mål datorerna. Konfigurera följande alternativ:  

    - **Start fördröjning för session (minuter)**: Ange antalet minuter som Configuration Manager väntar innan den svarar på den första distributions förfrågan.  

    - **Minsta sessionsgräns (klienter)**: Ange hur många förfrågningar som ska tas emot innan Configuration Manager börjar distribuera operativ systemet.  

> [!IMPORTANT]  
> Från och med version 1806, för att aktivera och konfigurera multicast på fliken **multicast** i egenskaperna för distributions platsen, måste distributions platsen använda Windows Deployment service.  
>
> - Om du **aktiverar PXE-stöd för klienter** och **gör det möjligt för multicast att samtidigt skicka data till flera klienter**kan du inte **Aktivera en PXE-svarare utan Windows Deployment-tjänst**.  
>
> - Om du **aktiverar PXE-stöd för klienter** och **aktiverar en PXE-svarare utan Windows Deployment service**, kan du inte **Aktivera multicast för att samtidigt skicka data till flera klienter**  

### <a name="group-relationships"></a><a name="bkmk_config-group"></a>Grupp relationer  

> [!NOTE]  
> De här alternativen är bara tillgängliga när du redigerar egenskaperna för en tidigare installerad distributions plats.  

Hantera distributions plats grupper som distributions platsen är medlem i.  

Om du vill lägga till den här distributions platsen som en medlem i en befintlig distributions plats grupp väljer du **Lägg till**. I fönstret Lägg till distributions plats grupper väljer du en befintlig grupp och väljer sedan **OK**.  

Om du vill ta bort den här distributions platsen från en distributions plats grupp markerar du gruppen i listan och väljer sedan **ta bort**. Om du tar bort distributions platsen från en distributions plats grupp tas inget innehåll bort från distributions platsen.

### <a name="content"></a><a name="bkmk_config-content"></a>Innehåll  

> [!NOTE]  
> De här alternativen är bara tillgängliga när du redigerar egenskaperna för en tidigare installerad distributions plats.  

Hantera det innehåll som du har distribuerat till distributions platsen. Välj i listan över distributions paket och utför följande åtgärder:  

- **Verifiera**: starta processen för att verifiera integriteten hos innehållsfilerna för program varan. Om du vill visa resultatet av innehålls validerings processen expanderar du **distributions status**på arbets ytan **övervakning** och väljer sedan noden **innehålls status** . Mer information finns i avsnittet [validera innehåll](deploy-and-manage-content.md#validate-content).  

- **Distribuera**om: kopierar alla innehållsfiler för den valda program varan till distributions platsen och skriver över de befintliga filerna. Du använder vanligt vis den här åtgärden för att reparera innehållsfiler. Mer information finns i [distribuera om innehåll](deploy-and-manage-content.md#redistribute-content).  

- **Ta bort**: tar bort innehållsfilerna för program varan från distributions platsen. Mer information finns i [ta bort innehåll](deploy-and-manage-content.md#remove-content).  

### <a name="content-validation"></a><a name="bkmk_config-valid"></a>Innehålls validering  

Ange ett schema för att verifiera integriteten för innehållsfiler på distributions platsen. När du aktiverar innehålls validering enligt ett schema startar Configuration Manager processen vid den schemalagda tiden. Den verifierar allt innehåll på distributions platsen baserat på den lokala SMS_PackagesInContLib SCCMDP-klassen. Du kan också konfigurera prioritet för innehålls validering. Prioriteten anges som standard till **lägsta**. Att öka prioriteten kan öka processor-och disk användningen på servern under validerings processen, men den bör bli snabbare.

Om du vill visa resultatet av innehålls validerings processen expanderar du **distributions status**på arbets ytan **övervakning** och väljer sedan noden **innehålls status** . Den visar innehållet för varje program varu typ, till exempel program, program uppdaterings paket och start avbildning.  

> [!WARNING]  
> Även om du anger schemat för innehålls validering genom att använda den lokala tiden för datorn, visar Configuration Manager-konsolen schemat i UTC.  

Mer information finns i avsnittet [validera innehåll](deploy-and-manage-content.md#validate-content).

### <a name="boundary-groups"></a><a name="bkmk_config-boundary"></a>Gränser grupper  

Hantera de gränser grupper som du tilldelar den här distributions platsen. Lägg till distributions platsen till minst en avgränsnings grupp. Vid innehålls distribution måste klienterna finnas i en kant linje som är kopplad till en distributions plats för att använda distributions platsen som en käll plats för innehåll.

Konfigurera gränser grupp *relationer* som definierar när och till vilka gränser grupper en klient kan gå tillbaka för att hitta innehåll. Mer information finns i [gränser grupper](boundary-groups.md).

Välj **Lägg till** och välj en befintlig avgränsnings grupp i listan.

Om du vill skapa en ny avgränsnings grupp för den här distributions platsen väljer du **skapa**. Mer information om hur du skapar och konfigurerar en avgränsnings grupp finns i [procedurer för gränser grupper](boundary-group-procedures.md).

När du redigerar egenskaperna för en tidigare installerad distributions plats hanterar du alternativet för att **Aktivera för distribution på begäran**. Med det här alternativet kan Configuration Manager automatiskt distribuera innehåll till den här servern när en klient begär det. Mer information finns i [innehålls distribution på begäran](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).

### <a name="schedule"></a><a name="bkmk_config-sched"></a>Ange  

> [!NOTE]  
> De här alternativen är bara tillgängliga när du redigerar egenskaperna för en tidigare installerad distributions plats.
>
> Den här fliken är endast tillgänglig när du redigerar egenskaperna för en distributions plats som är fjärran sluten till plats servern.  

Konfigurera ett schema som begränsar när Configuration Manager kan överföra data till distributions platsen. Begränsa data med prioritet eller Stäng anslutningen för valda tids perioder.

Om du vill begränsa data väljer du tids perioden i rutnätet och väljer sedan någon av följande inställningar för **tillgänglighet**:  

- **Öppen för alla prioriteter**: Configuration Manager skickar data till distributions platsen utan begränsningar. Den här inställningen är standard för alla tids perioder.  

- **Tillåt medelhög och hög prioritet**: Configuration Manager skickar endast data med medelhög prioritet och hög prioritet till distributions platsen.  

- **Tillåt endast hög prioritet**: Configuration Manager skickar endast data med hög prioritet till distributions platsen.  

- **Stängd**: Configuration Manager skickar inga data till distributions platsen.  

Konfigurera **distributions prioriteten** för program vara på fliken **distributions inställningar** i program varu egenskaperna.

> [!IMPORTANT]  
> Schemat baseras på tids zonen från den sändande platsen, inte på distributions platsen.  

### <a name="rate-limits"></a><a name="bkmk_config-rate"></a>Hastighets begränsningar  

> [!NOTE]  
> De här alternativen är bara tillgängliga när du redigerar egenskaperna för en tidigare installerad distributions plats.  
>
> Den här fliken är endast tillgänglig när du redigerar egenskaperna för en distributions plats som är fjärran sluten till plats servern.  

Konfigurera hastighets begränsningar för att kontrol lera den nätverks bandbredd som Configuration Manager använder för att överföra innehåll till distributions platsen. Välj bland följande alternativ:  

- **Obegränsat vid överföring till den här destinationen**: Configuration Manager skickar innehåll till distributions platsen utan hastighets begränsnings begränsningar. Den här inställningen är standardinställningen.  

- **Puls läge**: det här alternativet anger storleken på de data block som plats servern skickar till distributions platsen. Du kan också ange en tidsfördröjning mellan varje datablock som skickas. Använd det här alternativet om du måste skicka data över en nätverks anslutning med låg bandbredd till distributions platsen. Du har till exempel begränsningar för att skicka 1 KB data var femte sekund, oavsett länkens hastighet eller användning vid en specifik tidpunkt.  

- **Begränsad till angivna högsta överföringshastighet per timme**: Ange den här inställningen om du vill att en plats ska skicka data till en distributions plats genom att bara använda den procent andel av tiden som du konfigurerar. När du använder det här alternativet identifierar Configuration Manager inte nätverkets tillgängliga bandbredd. I stället delar den tid det kan skicka data. Servern skickar data under en kort tids period, som följs av tids perioder då data inte skickas. Om du till exempel ställer in **begränsad bandbredd** på **50%** skickar Configuration Manager data under en tids period följt av en lika lång tids period då inga data skickas. Data blockets faktiska storlek eller storlek hanteras inte. Den hanterar bara den tid under vilken data skickas.  
