---
title: Funktioner i Technical Preview 1606
titleSuffix: Configuration Manager
description: Lär dig mer om funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1606.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 134a2f60-811e-4dc9-a8f5-1ce0018c5c12
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 05e7bbe6373ed91de5a2bb8e99a8425e733274f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721621"
---
# <a name="capabilities-in-technical-preview-1606-for-configuration-manager"></a>Funktioner i Technical Preview 1606 för Configuration Manager

*Gäller för: Configuration Manager (Technical Preview Branch)*

Den här artikeln beskriver de funktioner som är tillgängliga i den tekniska för hands versionen för Configuration Manager version 1606. Du kan installera den här versionen för att uppdatera och lägga till nya funktioner till din Configuration Manager Technical Preview-webbplats.      Innan du installerar den här versionen av Technical Preview kan du läsa introduktions avsnittet, [teknisk för hands version för Configuration Manager](../../core/get-started/technical-preview.md), för att bekanta dig med allmänna krav och begränsningar för att använda en teknisk för hands version, hur du uppdaterar mellan versioner och hur du ger feedback om funktionerna i en teknisk för hands version.    

**Kända problem i den här tekniska för hands versionen:**  
*  När du uppdaterar från Technical Preview 1604 till 1605, och till version 1606, kan uppdateringen Miss Miss kan och ett fel som liknar följande loggas i **cmupdate. log**:

    ``` Log
    ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END
    ```

    Om detta inträffar klickar du på **Sök efter uppdateringar**i noden **uppdateringar och underhåll** och försöker sedan installera uppdateringen **igen** .
    ***

**Följande är nya funktioner som du kan prova med den här versionen.**  

## <a name="automatically-categorize-devices-into-collections"></a><a name="dmp_category"></a>Kategorisera enheter automatiskt i samlingar
Du kan skapa enhets kategorier, som kan användas för att automatiskt placera enheter i enhets samlingar när du använder Configuration Manager med Microsoft Intune. Användarna måste sedan välja en enhets kategori när de registrerar en enhet i Intune. Du kan också ändra kategori för en enhet från Configuration Manager-konsolen.

**Viktigt:** Den här funktionen fungerar med den **2016 juni** -versionen av Microsoft Intune. Se till att du har uppdaterat till den här versionen innan du provar de här procedurerna.

### <a name="try-it-out"></a>prova!

### <a name="create-a-set-of-device-categories"></a>Skapa en uppsättning enhets kategorier
1.  I arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen expanderar du **Översikt**och klickar sedan på **enhets samlingar**.
2.  På fliken **Start** går du till gruppen **Kategorier** och klickar på **Hantera enhets kategorier**.
3.  I dialog rutan **Hantera enhets kategorier** kan du skapa, redigera eller ta bort kategorier. Försök att skapa en ny kategori.

### <a name="associate-a-collection-with-a-device-category"></a>Koppla en samling till en enhets kategori
När du associerar en samling med en enhets kategori kommer alla enheter i den kategori som du anger att läggas till i samlingen.
1.  I dialog rutan **Egenskaper** för en enhets samling klickar du på **Lägg till regel** > **enhet kategori regel**.
2.  I dialog rutan **Skapa regel för medlemskap i enhets kategori** väljer du den kategori som ska tillämpas på alla enheter i samlingen.
3.  Stäng dialog rutan **Skapa regel för medlemskap i enhets kategori** och dialog rutan Egenskaper för samling.

### <a name="change-the-category-of-a-device"></a>Ändra kategori för en enhet
1.  I arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen expanderar du **Översikt**och klickar sedan på **enheter**.
2.  Välj en enhet i listan **enheter** och klicka sedan på **Ändra kategori**i gruppen **enhet** på fliken **Start** .
3.  I dialog rutan **Redigera enhets kategori** väljer du den kategori som ska användas för enheten och klickar sedan på **OK**.

## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a><a name="dmp_grace"></a>Tvingande respitperiod för nödvändiga program-och program uppdaterings distributioner

I vissa fall kanske du vill ge användarna mer tid att installera nödvändiga program distributioner eller program uppdateringar utöver de tids gränser som du har konfigurerat. Detta kan vanligt vis krävas när en dator har inaktiverats under en längre tid och måste installera ett stort antal program-eller uppdaterings distributioner.
Om en slutanvändare till exempel precis har returnerat från semestern kan de vänta en stund medan förfallna program distributioner installeras.
För att hjälpa till att lösa det här problemet kan du nu definiera en tvingande respitperiod genom att distribuera Configuration Manager klient inställningar till en samling.

### <a name="try-it-out"></a>prova!

Utför följande åtgärder för att konfigurera respitperioden:

1.  På sidan **dator agent** i klient inställningar konfigurerar du den nya **periodens respitperiod för tvång efter distributionens tids gräns (timmar)** med ett värde mellan **1** och **120** timmar.
2.  I en ny nödvändig program distribution, eller i egenskaperna för en befintlig distribution, på sidan **Schemaläggning** väljer du kryss rutan **fördröj tvång på distributionen enligt användar inställningar**, upp till den Respitperiod som definierats i klient inställningarna.
Alla distributioner som har den här kryss rutan markerad och som är riktade till enheter som du också distribuerar klient inställningen till använder tvångs perioden för tvång.

Om du konfigurerar en tvångs Grace-period och markerar kryss rutan, kommer den att installeras i det första icke-affärsfönster som användaren har konfigurerat för den aktuella Grace-perioden när tids gränsen för program installationen har uppnåtts. Användaren kan dock fortfarande öppna Software Center och installera programmet när som helst. När Grace-perioden går ut återgår tvång till det normala beteendet för förfallna distributioner.
Liknande alternativ har lagts till i guiden distribution av program uppdateringar, guiden automatiska distributions regler och egenskaps sidor.

##  <a name="using-configuration-manager-as-a-managed-installer-with-device-guard"></a><a name="dmp_devg"></a>Använda Configuration Manager som ett hanterat installations program med Device Guard

Device Guard är en funktion i Windows 10 som använder maskinvaru-och program varu funktioner för att strikt styra vad som får köras på enheten.

Du kan läsa en detaljerad översikt över vad Device Guard gör och hur det fungerar i [den här TechNet-artikeln](https://technet.microsoft.com/itpro/windows/whats-new/device-guard-overview).

I den här versionen kan Configuration Manager samverka med Device Guard och [Windows AppLocker](https://technet.microsoft.com/library/dd723678(v=ws.10).aspx) så att körbara filer och DLL-filer som distribueras med Configuration Manager automatiskt är betrodda när de kommer från ett hanterat installations program, vilket innebär att de kommer att kunna köras på mål enheten och annan program vara kommer inte att kunna köras om det uttryckligen tillåts att köras av andra AppLocker-regler.  

Den här funktionen kan för närvarande inte konfigureras från Configuration Manager-konsolen. Om du vill konfigurera principen måste du konfigurera en register nyckel på varje klient och konfigurera Windows-tjänster på klienten.
När detta är färdigt konfigurerar du AppLocker-principagenten. När du har konfigurerat princip filen kan du distribuera den till valfri kompatibel klient enhet.


Precis som alla AppLocker-principer kan principer med hanterade installations regler köras i två lägen:

- Gransknings läge – program anteckningen hindras från att köras, men alla program som skulle ha blockerats rapporteras i en loggfil (detta stöds i en senare version av Configuration Manager).
- Tvångs aktivering – program blockeras från att köras.

Mer information om hur du använder Device Guard med Configuration Manager finns på [bloggen för Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/2016/06/20/configmgr-as-a-managed-installer-with-win10).

Mer läsning:

- [Introduktion till Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/introduction-to-device-guard-virtualization-based-security-and-code-integrity-policies)
- [Device Guard-certifiering och efterlevnad](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-certification-and-compliance)
- [Distributions guide för Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)

  ##  <a name="multiple-device-management-points-for-on-premises-mobile-device-management"></a><a name="dmp_onprem"></a>Flera enhets hanterings platser för lokal hantering av mobila enheter  
  Med teknisk för hands version 1606\-, lokal hantering av mobila enheter (MDM) har stöd för en ny funktion i Windows 10-uppdaterings perioden som automatiskt konfigurerar en registrerad enhet att ha mer än en enhets hanterings plats tillgänglig för användning. Den här funktionen gör det möjligt för enheten att återgå till en annan enhets hanterings plats när den normala användningen inte är tillgänglig. Den här funktionen fungerar bara för datorer där uppdatering av Windows 10-årsdag är installerat.  

### <a name="try-it-out"></a>prova!  

1.  Installera mer än en enhets hanterings plats i hierarkin.  

2.  Registrera en uppdaterings enhet för Windows 10-\-årsdag för lokal hantering av mobila enheter.  

Information om hur du förbereder din webbplats och registrerar enheter för\-lokal hantering av mobila enheter finns i [Hantera mobila enheter med lokal infrastruktur](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="cloud-proxy-service-for-managing-clients-on-the-internet"></a><a name="cloud_proxy"></a>Molnbaserad proxy-tjänst för att hantera klienter på Internet

Cloud proxy service är ett enkelt sätt att hantera Configuration Manager-klienter på Internet. Tjänsten, som distribueras till Microsoft Azure och kräver en Azure-prenumeration, ansluter till din lokala Configuration Manager-infrastruktur med hjälp av en ny roll som kallas för Cloud proxy Connector Point. När den är fullständigt distribuerad och konfigurerad kommer klienter att kunna komma åt lokala Configuration Manager plats system roller, oavsett om de är anslutna till det interna privata nätverket eller Internet.

Du använder Configuration Manager-konsolen för att distribuera tjänsten till Azure, lägga till rollen Cloud proxy Connector punkt och konfigurera plats system roller så att de tillåter Cloud proxy-trafik. Cloud proxy service stöder för närvarande endast hanterings plats-, distributions plats-och program uppdaterings plats roller.

Klient certifikat och SSL-certifikat (Secure Socket Layer) krävs för att autentisera datorer och kryptera kommunikation mellan olika lager i tjänsten. Klient datorer får vanligt vis ett klient certifikat via grup princip tvång. För att kryptera trafiken mellan klienter och plats system servern som är värd för rollerna måste du skapa ett anpassat SSL-certifikat från certifikat utfärdaren. Förutom dessa två typer av certifikat måste du också konfigurera ett hanterings certifikat på Azure som låter Configuration Manager distribuera Cloud proxy service.  

### <a name="requirements-for-cloud-proxy-service-in-tp-1606"></a>Krav för Cloud proxy service i TP 1606
- Klient datorer och plats system servern som kör Cloud proxy Connector-platsen.
- Anpassade SSL-certifikat från den interna certifikat utfärdaren – används för att kryptera kommunikation från klient datorerna och autentisera identiteten för Cloud proxy service.
- Azure-prenumeration för Cloud Services.
- Hanterings certifikat för Azure – används för att autentisera Configuration Manager med Azure.

### <a name="limitations-of-cloud-proxy-service-in-tp-1606"></a>Begränsningar för Cloud proxy service i TP 1606

- Stöder endast hanterings plats-, distributions plats-och program uppdaterings plats roller.
- Användar principer stöds inte.
- Kan inte användas med [lokal hantering av mobila enheter](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) i Configuration Manager.
- Stöds endast på Azures offentliga moln plattform.


### <a name="try-it-out"></a>prova!

Processen för att distribuera Cloud proxy service innehåller följande steg:

1. Skapa och utfärda ett anpassat SSL-certifikat för Cloud proxy service.
1. Exportera klient certifikatets rot.
2. Ladda upp hanterings certifikatet till Azure.
3. Konfigurera Cloud proxy service i Configuration Manager-konsolen.
4. Konfigurera den primära platsen för att använda autentisering med klient certifikat.
5. Lägg till Cloud proxy Connector-platsen till din webbplats.
6. Konfigurera plats system rollerna så att de accepterar Cloud proxy-trafik.

I följande avsnitt finns mer information om hur du slutför de här stegen.

#### <a name="create-a-custom-ssl-certificate"></a>Skapa ett anpassat SSL-certifikat

Du kan skapa ett anpassat SSL-certifikat för Cloud proxy service på samma sätt som du gör det för en molnbaserad distributions plats. Följ anvisningarna för att [distribuera tjänst certifikatet för molnbaserade distributions platser](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012) , men gör följande saker på olika sätt:

* När du ställer in den nya certifikat mal len ger du **Läs** -och **registrerings** behörigheter till säkerhets gruppen som du konfigurerade för Configuration Manager-servrar.

#### <a name="export-the-client-certificates-root"></a>Exportera klient certifikatets rot

Det enklaste sättet att exportera roten för de klient certifikat som används i nätverket är att öppna ett klient certifikat på en av de domänanslutna datorer som har en och kopiera den.

>[!NOTE]
>Klient certifikat krävs på alla datorer som du vill hantera med Cloud proxy-tjänsten och på den plats system server som är värd för moln proxyns anslutnings punkt. Om du behöver lägga till ett klient certifikat till någon av dessa datorer kan du läsa [distribuera klient certifikatet för Windows-datorer](../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012).

1. I fönstret Kör skriver du **MMC** och trycker på RETUR.
2. På Arkiv-menyn i hanterings konsolen klickar du på **Lägg till/ta bort snapin-modul..**..
3. I dialog rutan Lägg till eller ta bort snapin-moduler klickar du på **certifikat**, klicka på **Lägg till >**, klicka på **dator konto**, klicka på **Nästa**, klicka på **lokal dator**och klicka sedan på **Slutför**. Stäng dialogrutan genom att klicka på **OK**.
4. Gå till **certifikat > personliga > certifikat**.
5. Dubbelklicka på certifikatet för klientautentisering på datorn, klicka på fliken certifierings Sök väg och dubbelklicka på rot utfärdaren (längst upp i sökvägen).
6.  Klicka på fliken information och sedan på **Kopiera till fil.**...
7. Slutför guiden Exportera certifikat med standard certifikat formatet. Anteckna namn och plats för det rot certifikat som du skapar. Du behöver den för att konfigurera tjänsten Cloud proxy i ett senare steg.

#### <a name="upload-the-management-certificate-to-azure"></a>Ladda upp hanterings certifikatet till Azure

Ett hanterings certifikat för Azure krävs för att Configuration Manager ska kunna komma åt Azure API och konfigurera Cloud proxy service. Mer information och anvisningar om hur du laddar upp ett hanterings certifikat finns i följande artiklar i Azure-dokumentationen:
- [Certifikatöversikt för Azure Cloud Services](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)
- [Överför ett Azure-hanterings API Management certifikat](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/).

Se till att kopiera det prenumerations-ID som är associerat med hanterings certifikatet. Du behöver den för att konfigurera tjänsten Cloud proxy i Configuration Manager-konsolen.

#### <a name="set-up-cloud-proxy-service"></a>Konfigurera Cloud proxy service

1. I Configuration Manager-konsolen går du till **Administration > Cloud Services > Cloud proxy service**.
2. Klicka på **skapa molnbaserad proxy-tjänst**.
3. I guiden skapa molnbaserad proxy-tjänst anger du ditt Azure-prenumerations-ID (kopieras från hanterings portalen för Azure), klickar på Bläddra och väljer den certifikat fil som du använde för att ladda upp som ett Azure-hanterings certifikat. Klicka på **Nästa**. Vänta en stund tills konsolen ansluter till Azure.
4. Fyll i ytterligare information i guiden:
    - Ange den privata nyckel (. pfx-fil) som du exporterade från det anpassade SSL-certifikatet.
    - Ange det rot certifikat som exporter ATS från klient certifikatet.
    - Ange samma FQDN för tjänst namnet som du använde när du skapade den nya certifikat mal len.
    - Avmarkera kryss rutan bredvid **kontrol lera återkallning av klient certifikat** (om du inte offentligt publicerar din CRL-information).
    - Klicka på **Nästa** när du är klar.
5. Granska inställningarna och klicka på **Nästa**. Configuration Manager börjar konfigurera tjänsten. När guiden har slutförts kan du klicka på **Stäng**, men det tar mellan 5 och 15 minuter att etablera tjänsten helt i Azure. Kontrol lera kolumnen **status** för den nyligen konfigurera Cloud proxy-tjänsten för att fastställa när tjänsten är klar.

#### <a name="configure-primary-site-for-client-certification-authentication"></a>Konfigurera primär plats för autentisering av klient certifikat

1. I Configuration Manager-konsolen går du till **Administration > plats konfiguration > platser**.
2. Välj den primära platsen för de klienter som du vill hantera via Cloud proxy service och klicka på **Egenskaper**.
3. På fliken kommunikation på klient datorn i egenskaps bladet primär plats markerar du kryss rutan bredvid **Använd PKI-klientcertifikat (klientautentisering) när det är tillgängligt**.
4. Se till att avmarkera kryss rutan bredvid- **klienter kontrol lera listan över återkallade certifikat (CRL) för plats system**. Det här alternativet krävs endast om du har publicerat din CRL offentligt.
5. Klicka på **OK**.

#### <a name="add-the-cloud-proxy-connector-point"></a>Lägg till Cloud proxy Connector-punkten

Cloud proxy Connector Point är en ny plats system roll för kommunikation med Cloud proxy service. Om du vill lägga till Cloud proxy Connector-punkten följer du anvisningarna i [Lägg till plats system roller för Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md).

#### <a name="configure-roles-for-cloud-proxy-traffic"></a>Konfigurera roller för Cloud proxy-trafik

Det sista steget i att ställa in Cloud proxy service är att konfigurera plats system rollerna så att de accepterar Cloud proxy-trafik. För för hands versionen av Tech 1606 stöds endast rollerna hanterings plats, distributions plats och program uppdaterings plats för Cloud proxy service. Du måste konfigurera varje roll separat.

1. I Configuration Manager-konsolen går du till **Administration > plats konfiguration > servrar och plats system roller**.
2. Klicka på plats system servern för den roll som du vill konfigurera för Cloud proxy-trafik.
3. Klicka på rollen och klicka sedan på **Egenskaper**.
4. I sidan roll egenskaper under klient anslutningar väljer du **https**, markerar kryss rutan bredvid **Tillåt Configuration Manager Cloud proxy-trafik**och klickar sedan på **OK**. Upprepa de här stegen för de återstående rollerna.

#### <a name="check-status-on-a-client-on-the-internet"></a>Kontrol lera status på en klient på Internet

När tjänsten och rollerna har kon figurer ATS helt får de interna klienterna platsen för tjänsten Cloud proxy på nästa plats-begäran. Klienter med uppdaterad plats information kan sedan kommunicera med Configuration Manager på Internet. Avsöknings cykeln för plats begär Anden är var 24: e timme. Om du inte vill vänta på den vanliga schemalagda plats förfrågan kan du framtvinga begäran genom att starta om värd tjänsten för SMS-agent (ccmexec. exe) på datorn.

När klienterna har den nya plats informationen för tjänsten Cloud proxy kan du prova att kontrol lera statusen för klienter som inte längre finns i det interna privata nätverket, men som har Internet åtkomst. Du kan också övervaka trafiken i Cloud proxy service genom att gå till **Administration > Cloud Services > Cloud proxy-tjänsten**, välja tjänsten i list rutan och Visa trafik informationen i informations fönstret.   

## <a name="manage-the-office-365-client-agent-in-configuration-manager"></a><a name="manage_o365"></a>Hantera Office 365-klientagenten i Configuration Manager  

Från och med den tekniska för hands versionen 1606 kan du använda en Configuration Manager klient agent inställning, i stället för grup princip, för att låta Office 365-klienter ta emot uppdateringar från Configuration Manager. När du har konfigurerat den här inställningen och distribuerat Office 365-uppdateringar kommunicerar Configuration Manager klient agenten med Office 365-klient agenten att hämta Office 365-uppdateringar från en distributions plats och installera dem. Configuration Manager också ta inventering av klient agent inställningen.

Mer information finns i [Hantera Office 365 ProPlus-uppdateringar](https://technet.microsoft.com/library/mt741983.aspx).

### <a name="set-the-configuration-manager-client-setting-to-manage-the-office-365-client-agent"></a>Ange Configuration Manager klient inställningen för att hantera Office 365-klient agenten
1.  I Configuration Manager-konsolen klickar du på **Administration** > **Översikt** > **klient inställningar**.
2. Öppna lämpliga enhets inställningar för att aktivera klient agenten. Mer information om standard-och anpassade klient inställningar finns i [Konfigurera klient inställningar](../../core/clients/deploy/configure-client-settings.md).
3. Klicka på **program uppdateringar** och välj **Ja** för inställningen **aktivera hantering av klient agenten för Office 365** .  


## <a name="the-osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a><a name="osdpreservedriveletter"></a>Aktivitetssekvensvariabeln OSDPreserveDriveLetter är föråldrad
Variabeln OSDPreserveDriveLetter bestämmer om aktivitetssekvensen använder enhets beteckningen som har registrerats i WIM-filen för operativ Systems avbildningen när avbildningen tillämpas på en måldator.
- Den här aktivitetssekvensen är inaktuell i Technical Preview 1606.

Under en operativ Systems distribution bestämmer Installationsprogrammet för Windows nu den bäst enhets beteckning som ska användas (vanligt vis C:). Om du vill ange en annan enhet som ska användas kan du ändra platsen i steget Använd operativ systemets aktivitetssekvens. Gå till sidan **Välj den plats där du vill använda den här inställningen för operativ systemet** , Välj en **logisk enhets beteckning**och välj den enhet som du vill använda. Det måste finnas en enhet som har tilldelats den bokstav du väljer på mål datorn. 

## <a name="changes-for-the-updates-and-servicing-node"></a><a name="updatesandservicing"></a>Ändringar för noden Uppdateringar och service
Med teknisk för hands version 1606 har du infört flera ändringar som gäller uppdateringar och underhåll i Configuration Manager-konsolen:
- **Ändra nodnamn:**

    På arbets ytan **övervakning** har noden **plats underhålls status** bytt namn till **uppdateringar och underhålls status**.
- **Mer installations status:**

    När du visar uppdateringens installations status för en plats visar konsolen nu en separat information för följande åtgärder:
    - **Hämta** (Detta gäller endast den plats på den översta nivån där tjänst anslutnings punktens plats system roll är installerad)
    - **Replikering**
    - **Kravkontroll**
    - **Installation**

  Dessutom finns det nu mer detaljerad information för varje steg, inklusive i vilken loggfil du kan visa mer information.  
-   **Nytt alternativ för att försöka utföra nödvändiga fel:**

    På arbets ytan **Administration** och **övervakning** innehåller noden **uppdateringar och underhåll** en ny knapp i menyfliksområdet med namnet **Ignorera krav varningar**.

    När du installerar uppdateringar utan att använda alternativet för att ignorera krav kontroll varningar (från uppdaterings guiden) och installationen av uppdateringen stoppas med status **krav**, kan du välja **Ignorera krav varningar** från menyfliksområdet för att utlösa en automatisk fortsättning på den uppdaterings installation som ignorerar de nödvändiga varningarna.  



- **Renare vy över uppdateringar:**

    När du visar noden **uppdateringar och underhåll** visas nu bara den senast installerade uppdateringen och eventuella nya uppdateringar som är tillgängliga för installation. Om du vill visa tidigare installerade uppdateringar klickar du på knappen ny **Historik** som visas i menyfliksområdet.  

-   **Omdöpt alternativ för för produktion:**

    I noden uppdateringar och underhåll ändras nu knappen med namnet **klient alternativ** för att **Flytta upp för produktions klienten**.
