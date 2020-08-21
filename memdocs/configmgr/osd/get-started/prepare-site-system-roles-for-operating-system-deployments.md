---
title: Förbereda plats system roller för OSD
titleSuffix: Configuration Manager
description: Konfigurera plats system rollerna innan du distribuerar operativ system i Configuration Manager
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d9331ce452e40944e4a9b363773d254a32f2c58
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697491"
---
# <a name="prepare-site-system-roles-for-os-deployments-with-configuration-manager"></a>Förbereda plats system roller för operativ Systems distributioner med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Om du vill distribuera operativ system i Configuration Manager måste du först förbereda följande plats system roller som kräver vissa konfigurationer och överväganden.



##  <a name="distribution-points"></a><a name="BKMK_DistributionPoints"></a> Distributions platser  

Distributions platsens plats system roll innehåller källfiler som kan hämtas av klienter. Det här innehållet gäller för program, program uppdateringar, OS-avbildningar, start avbildningar och driv rutins paket. Styra innehålls distribution med hjälp av alternativ för bandbredd, begränsning och schemaläggning.  

Det är viktigt att du har tillräckligt med distributions platser för att stödja distribution av operativ system till datorer. Det är också viktigt att du planerar för placeringen av dessa distributions platser i hierarkin. Mer information finns i [Hantera innehåll och innehålls infrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md). Den här artikeln innehåller några ytterligare planerings överväganden för distributions platser som är speciella för distribution av operativ system.  


###  <a name="additional-planning-considerations-for-distribution-points"></a><a name="BKMK_AdditionalPlanning"></a> Ytterligare planerings överväganden för distributions platser  

Följande objekt är ytterligare planerings saker att överväga för distributions platser:  

#### <a name="how-can-i-prevent-unwanted-os-deployments"></a>Hur kan jag förhindra oönskade operativ Systems distributioner?  
Configuration Manager skiljer inte plats servrar från andra mål datorer i en samling. Om du distribuerar en obligatorisk aktivitetssekvens till en samling som innehåller en plats Server körs aktivitetssekvensen på samma sätt som andra datorer i samlingen. Se till att operativ Systems distributionen använder en samling som innehåller de avsedda klienterna.  

Hantera beteendet för aktivitetssekvensdistributioner med hög risk. En distribution med hög risk installeras automatiskt på en klient och kan orsaka oönskade resultat. Till exempel en aktivitetssekvens med syftet obligatorisk som distribuerar ett operativ system. Konfigurera verifierings inställningar för distributionen för att minska risken för en oönskad högrisk distribution. Mer information finns i [Inställningar för att hantera distributioner med hög risk](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

#### <a name="how-many-computers-can-receive-an-os-image-at-one-time-from-a-single-distribution-point"></a>Hur många datorer kan ta emot en operativ system avbildning på en gång från en enda distributions plats?  
Om du vill beräkna hur många distributions platser du behöver bör du tänka på följande variabler:  
- Distributions platsens bearbetnings hastighet
- Distributions platsens disk hastighet
- Tillgänglig bandbredd i nätverket
- Avbildnings paketets storlek   
  
Om du till exempel inte anser några andra server resurs faktorer, är det maximala antalet datorer som kan bearbeta ett bild paket på 4 GB på en timme på ett 100-megabit/SEK Ethernet-nätverk 11 datorer.  

`100 megabits/sec = 12.5 megabytes/sec = 750 megabytes/min = 45 gigabytes/hour = 11 images @ 4 GB per image`  

Om du måste distribuera ett operativ system till ett angivet antal datorer inom en angiven tidsram distribuerar du avbildningen till ett lämpligt antal distributions platser.  

#### <a name="can-i-deploy-an-os-to-a-distribution-point"></a>Kan jag distribuera ett operativ system till en distributions plats?  
Du kan distribuera ett operativ system till en distributions plats, men operativ system avbildningen måste tas emot från en annan distributions plats.  


###  <a name="configuring-distribution-points-to-accept-pxe-requests"></a><a name="BKMK_PXEDistributionPoint"></a> Konfigurera distributions platser för att godkänna PXE-begäranden  

Om du vill distribuera operativ system till Configuration Manager klienter som gör PXE-startbegäranden konfigurerar du en eller flera distributions platser så att PXE-begäranden accepteras. När du har konfigurerat distributions platsen svarar den på PXE-startbegäranden och avgör vilken distributions åtgärd som ska vidtas. Mer information finns i [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).  


###  <a name="customize-the-ramdisk-tftp-block-and-window-sizes-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a> Anpassa RamDisk TFTP-block och fönster storlekar på PXE-aktiverade distributions platser  

Du kan anpassa RamDisk TFTP-block och fönster storlekar för PXE-aktiverade distributions platser. Om du har anpassat nätverket kan en stor block-eller fönster storlek medföra att hämtningen av start avbildningen inte kan slutföras med ett timeout-fel. Med anpassningarna av RamDisk TFTP-block och fönster storlek kan du optimera TFTP-trafik när du använder PXE för att uppfylla dina särskilda nätverks krav. Testa de anpassade inställningarna i din miljö för att avgöra vilken konfiguration som är mest effektiv.  

-   **TFTP-block storlek**: block storleken är storleken på de data paket som servern skickar till klienten som laddar ned filen. En större blockstorlek gör att servern kan skicka färre paket, så det finns färre fram-och-åter-förseningar mellan servern och klienten. En stor block storlek leder dock till fragmenterade paket, som de flesta PXE-klient implementeringar inte stöder.  

-   **TFTP-fönsterstorlek**: TFTP kräver ett bekräftelsepaket (ACK) för varje datablock som skickas. Servern skickar inte nästa block i ordningsföljden förrän den tagit emot ACK-paketet för föregående block. Med TFTP-fönster kan du definiera hur många data block det tar för att fylla ett fönster. Servern skickar datablock tills fönstret fylls och sedan skickar klienten ett ACK-paket. Om du ökar den här fönster storleken minskar antalet fördröjningar mellan klienten och servern och den totala nödvändiga tiden för att hämta en start avbildning minskar.  
  

#### <a name="modify-the-ramdisk-tftp-window-size"></a>Ändra storlek på RamDisk TFTP-fönstret  
Om du vill anpassa storleken på RamDisk TFTP-fönstret lägger du till följande register nyckel på PXE-aktiverade distributions platser:  

- **Plats**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Namn**: RamDiskTFTPWindowSize  
- **Typ**: REG_DWORD  
- **Värde**: (anpassad fönster storlek)  
    - Standardvärdet är **1** (ett data block fyller fönstret).  

#### <a name="modify-the-ramdisk-tftp-block-size"></a>Ändra storlek på RamDisk TFTP-blocket  
Om du vill anpassa storleken på RamDisk TFTP-fönstret lägger du till följande register nyckel på PXE-aktiverade distributions platser:  

- **Plats**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Namn**: RamDiskTFTPBlockSize  
- **Typ**: REG_DWORD  
- **Värde**: (anpassad block storlek)  
    - Standardvärdet är **4096**.  

> [!Note]  
> Både Windows Deployment Services och Configuration Manager PXE responder-tjänsten har stöd för dessa TFTP-konfigurationer.  


###  <a name="configure-distribution-points-to-support-multicast"></a><a name="BKMK_DPMulticast"></a> Konfigurera distributions platser som stöder multicast  

Multicast är en nätverks optimerings metod. Använd den på distributions platser när flera klienter sannolikt kommer att ladda ned samma OS-avbildning på samma gång. När du använder multicast kan flera datorer samtidigt hämta operativ system avbildningen som den är multicast av distributions platsen. Utan multicast skickar distributions platsen en kopia av data till varje klient via en separat anslutning. Mer information finns i [använda multicast för att distribuera Windows via nätverket](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

Innan du distribuerar operativ systemet måste du konfigurera en distributions plats så att den stöder multicast. Mer information finns i [Installera och konfigurera distributions platser](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).



##  <a name="state-migration-point"></a><a name="BKMK_StateMigrationPoints"></a> Plats för tillståndsmigrering  

Platsen för tillståndsmigrering lagrar användar tillstånds data som USMT samlar in på en dator och sedan återställs på en annan dator. Men när du fångar in användar inställningar för en OS-distribution på samma dator, till exempel en distribution där du uppdaterar Windows på mål datorn, kan du välja om du vill lagra data på samma dator med hjälp av hårda länkar eller använda en plats för tillståndsmigrering. För vissa dator distributioner skapar Configuration Manager automatiskt en association mellan tillstånds lagret och mål datorn när du skapar tillstånds lagret. Tänk på följande faktorer när du planerar för platsen för tillståndsmigrering:    


### <a name="user-state-size"></a>Användartillståndets storlek  

Storleken på användartillståndet har en direkt inverkan på diskutrymmet på tillståndsmigreringsplatsen och nätverkets prestanda under migreringen. Överväg storleken på användartillståndet och antalet datorer som ska migreras. Tänk också på vilka inställningar som ska migreras från datorn. Om mappen **Mina dokument** exempelvis redan har säkerhetskopierats till en server behöver du kanske inte migrera den som en del av avbildnings distributionen. Undvik onödiga migreringar försätter den övergripande storleken på användar tillstånden mindre och minskar den effekt som den annars skulle ha på nätverks prestanda och disk lagring på plats för tillståndsmigrering.  


### <a name="user-state-migration-tool"></a>Migreringsverktyg för användartillstånd  

Om du vill avbilda och återställa användar tillstånd under distributionen av operativ systemen använder du ett User State Migration Tool-paket (USMT) som pekar på USMT-källfilerna. Configuration Manager skapar automatiskt det här paketet i Configuration Manager-konsolen i program **biblioteks**  >  **program hanterings**  >  **paket**. Configuration Manager använder USMT 10 för att avbilda användar tillstånd från ett operativ system och sedan återställa det till ett annat. Windows Assessment and Deployment Kit (Windows ADK) för Windows 10 innehåller USMT 10.

En beskrivning av olika migrerings scenarier för USMT 10 finns i [vanliga scenarier för migrering](/windows/deployment/usmt/usmt-common-migration-scenarios) i Windows-dokumentationen.  


### <a name="retention-policy"></a>Retention-principen  

När du konfigurerar platsen för tillståndsmigrering anger du hur lång tid det tar att lagra de användar tillstånds data som lagras. Hur länge data lagras på tillståndsmigreringsplatsen beror på två parametrar:  

-   Den effekt da lagrade uppgifterna har på diskutrymmet.  

-   Det eventuella kravet att lagra uppgifterna under en tid om du skulle behöva migrera dem igen.  
  
  
Tillståndsmigrering sker i två faser: data insamlas och data återställs. När du avbildar data samlas användartillståndsdata in och sparas på tillståndsmigreringsplatsen. När du återställer data hämtas användartillståndsdata från tillståndsmigreringsplatsen, skrivs till måldatorn och därefter släpper aktivitetssekvenssteget **Frisläpp tillståndslager** de lagrade uppgifterna. När data släpps, startar lagringstimern. Om du väljer alternativet för att ta bort migrerade data omedelbart raderas användar tillstånds data så fort de släpps. Om du väljer att lagra data under en viss tidsperiod raderas data när den angivna tiden har gått efter att tillståndsdata har släppts. Den längre tid du ställer in kvarhållningsperioden, desto mer disk utrymme kommer du förmodligen att behöva.  


### <a name="select-drive-to-store-user-state-migration-data"></a>Välj enhet för lagring av användartillstånd  

När du konfigurerar platsen för tillståndsmigrering anger du den enhet på servern som ska lagra data för migrering av användar tillstånd. Välj enhet i en fast lista med enheter. Vissa av enheterna kan vara skrivskyddade enheter som CD-enheten eller en enhet utanför nätverket. Vissa enhets beteckningar kan inte mappas till några enheter på datorn. Ange en skrivbar, delad enhet när du konfigurerar platsen för tillståndsmigrering.  


### <a name="configure-a-state-migration-point"></a>Konfigurera en tillståndsmigreringsplats  

Använd följande metoder för att konfigurera en plats för tillståndsmigrering för att lagra användar tillstånds data:  

-   Använd **Guiden skapa platssystemserver** för att skapa en ny platssystemserver för tillståndsmigreringsplatsen.  

-   Använd **Guiden lägg till platssystemroller** för att lägga till en tillståndsmigreringsplats i en befintlig server.  

När du använder dessa guider uppmanas du att ange följande information för platsen för tillståndsmigrering:  

-   Mapparna där användartillståndsdata ska lagras.  

-   Högsta antal klienter som kan lagra data på tillståndsmigreringsplatsen.  

-   Minsta lediga utrymme på tillståndsmigreringsplatsen för lagring av användartillståndsdata.  

-   Borttagningsprincip för rollen. Ange antingen att användar tillstånds data tas bort omedelbart efter att den återställts på en dator eller efter ett angivet antal dagar efter det att användar data har återställts på en dator.  

-   Huruvida tillståndsmigreringsplatsen bara svarar på förfrågningar om att återställa användartillståndsdata. När du aktiverar det här alternativet kan du inte använda platsen för tillståndsmigrering för att lagra användar tillstånds data.  

Anvisningar för hur du installerar en plats system roll finns i [lägga till plats system roller](../../core/servers/deploy/configure/add-site-system-roles.md).