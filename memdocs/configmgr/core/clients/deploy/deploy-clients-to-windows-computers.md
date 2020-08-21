---
title: Distribuera klienter till Windows
titleSuffix: Configuration Manager
description: Lär dig hur du distribuerar Configuration Manager-klienten till Windows-datorer.
ms.date: 09/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2eea75f39430f1cc38ff994280425ca918eaa432
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694567"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-configuration-manager"></a>Distribuera klienter till Windows-datorer i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln innehåller information om hur du distribuerar Configuration Manager-klienten till Windows-datorer. Mer information om hur du planerar och förbereder klient distribution finns i följande artiklar:

- [Installationsmetoder för klient](plan/client-installation-methods.md)  
- [Krav för distribution av klienter till Windows-datorer](prerequisites-for-deploying-clients-to-windows-computers.md)
- [Säkerhet och sekretess för Configuration Manager-klienter](plan/security-and-privacy-for-clients.md)  
- [Metodtips för klientdistribution](plan/best-practices-for-client-deployment.md)  


## <a name="client-push-installation"></a><a name="BKMK_ClientPush"></a> Push-installation av klient

Det finns tre huvudsakliga sätt att använda klient-push:  

- När du konfigurerar push-installation av klienter för en plats körs klient installationen automatiskt på datorer som platsen identifierar. Den här metoden är begränsad till platsens konfigurerade gränser när gränserna är konfigurerade som en gräns grupp.  

- Starta push-installation av klienten genom att köra guiden push-installation av klient för en bestämd samling eller resurs i en samling.  

- Använd guiden för push-installation av klienter för att installera Configuration Manager-klienten, som du kan använda för att [fråga](../../servers/manage/introduction-to-queries.md) resultatet. Installationen kommer endast att lyckas om ett av objekten som returneras av frågan är **ResourceID** -attributet i **system resurs** klassen.

Om plats servern inte kan kontakta klient datorn eller starta installations processen, försöker den automatiskt att installera igen varje timme. Servern fortsätter att försöka igen i upp till sju dagar.  

Du kan spåra klient installations processen genom att installera en återställnings status punkt innan du installerar klienterna. När du installerar en återställnings status punkt tilldelas den automatiskt till klienter när de installeras med push-installation av klienten. Du kan spåra klient installations förloppet genom att visa rapporter om klient distribution och tilldelning.

Klient logg filen innehåller mer detaljerad information om fel sökning. Loggfilerna kräver ingen återställnings status plats. CCM. log-filen på plats servern registrerar till exempel eventuella problem som inträffar när plats servern ansluter till datorn. Filen CCMSetup. log på klienten registrerar installations processen.  

> [!IMPORTANT]  
> Push-installation av klienter lyckas bara om alla krav är uppfyllda. Mer information finns i [installations metodens beroenden](prerequisites-for-deploying-clients-to-windows-computers.md#installation-method-dependencies).

### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Konfigurera platsen för att automatiskt använda klient-push för identifierade datorer

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .  

2. Välj den plats som du vill konfigurera automatisk push-installation av klient för hela platsen.  

3. På fliken **Start** i menyfliksområdet väljer du **klient installations inställningar**i gruppen **Inställningar** och väljer sedan push-installation av **klient**.  

4. På fliken **Allmänt** i fönstret Egenskaper push-installation av klient väljer du **Aktivera automatisk push-installation av klient för hela platsen**.

5. Från och med version 1806 aktive ras en Kerberos-kontroll för klient-push när du uppdaterar platsen. Alternativet att **tillåta anslutnings återställning till NTLM** är aktiverat som standard, vilket är konsekvent med föregående beteende. Om platsen inte kan autentisera klienten med hjälp av Kerberos, försöker den ansluta igen med hjälp av NTLM. Den rekommenderade konfigurationen för förbättrad säkerhet är att inaktivera den här inställningen, vilket kräver Kerberos utan NTLM-återställning.<!--1358204-->  

    > [!NOTE]  
    > När klient-push används för att installera Configuration Manager-klienten, skapar plats servern en fjärr anslutning till klienten. Från och med version 1806 kan platsen kräva ömsesidig Kerberos-autentisering genom att inte tillåta återställning till NTLM innan anslutningen upprättas. Den här förbättringen hjälper till att skydda kommunikationen mellan servern och klienten.  
    >
    > Beroende på dina säkerhets principer kanske din miljö redan föredrar eller kräver Kerberos över den äldre NTLM-autentiseringen. Mer information om säkerhets överväganden för dessa autentiseringsprotokoll finns i [säkerhets princip inställningen i Windows för att begränsa NTLM](/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).  
    >
    > Om du vill använda den här funktionen måste klienterna vara i en betrodd Active Directory skog. Kerberos i Windows förlitar sig på Active Directory för ömsesidig autentisering.  

6. Välj de system typer som Configuration Manager ska pusha klient program varan till. Välj om du vill installera-klienten på domänkontrollanter.  

7. På fliken **konton** anger du ett eller flera konton för Configuration Manager som ska användas när den ansluter till mål datorn. Välj ikonen **skapa** , ange **användar namn** och **lösen ord** (högst 38 tecken), bekräfta lösen ordet och välj sedan **OK**. Ange minst ett konto för push-installation av klienter. Kontot måste ha lokal administratörs behörighet på mål datorn för att klienten ska kunna installeras. Om du inte anger ett konto för push-installation av klienter Configuration Manager försöker använda plats systemets dator konto. Klient-push mellan domäner Miss lyckas när du använder plats systemets dator konto.  

    > [!NOTE]  
    > Om du vill använda klient-push från en sekundär plats anger du det konto på den sekundära platsen som initierar klient-push.  
    >
    > Mer information om kontot för push-installation av klienter finns i nästa procedur, [med guiden push-installation av klient](#use-the-client-push-installation-wizard).  

8. Ange eventuella installations egenskaper som krävs på fliken **installations egenskaper** .

    Om du har utökat Active Directory-schemat för Configuration Manager publicerar platsen de angivna [klient installations egenskaperna](about-client-installation-properties.md) till Active Directory Domain Services. När CCMSetup körs utan installations egenskaper läses dessa egenskaper från Active Directory.  

    > [!NOTE]  
    > Om du aktiverar push-installation av klienter på en sekundär plats ställer du in egenskapen **SMSSITECODE** på den överordnade primära platsens Configuration Manager plats kod. Om du har utökat Active Directory-schemat för Configuration Manager för att automatiskt hitta rätt platstilldelning, ställer du in den här egenskapen på **Auto**.

### <a name="use-the-client-push-installation-wizard"></a>Använd guiden push-installation av klient

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .  

2. Välj den plats som du vill konfigurera automatisk push-installation av klient för hela platsen.  

3. På fliken **Start** i menyfliksområdet väljer du **klient installations inställningar**i gruppen **Inställningar** och väljer sedan push-installation av **klient**.  

4. Ange eventuella installations egenskaper som krävs på fliken **installations egenskaper** .  

    Om du har utökat Active Directory-schemat för Configuration Manager publicerar platsen de angivna [klient installations egenskaperna](about-client-installation-properties.md) till Active Directory Domain Services. När CCMSetup körs utan installations egenskaper läses dessa egenskaper från Active Directory.

5. Gå till arbets ytan **till gångar och efterlevnad** i Configuration Manager-konsolen.  

6. Välj en eller flera datorer i noden **enheter** . Eller Välj en samling datorer i noden **enhets samlingar** .  

7. På fliken **Start** i menyfliksområdet väljer du något av följande alternativ:  

    - För att push-överföra klienten till en eller flera enheter väljer du **Installera klient**i gruppen **enhet** .  

    - För att push-överföra klienten till en samling enheter väljer du **Installera klient**i gruppen **samling** .  

8. Granska informationen på sidan **innan du börjar** i guiden installera Configuration Manager klienten och välj sedan **Nästa**.  

9. Välj lämpliga alternativ på sidan **installations alternativ** .  

10. Granska installations inställningarna och slutför sedan guiden.  

> [!NOTE]  
> Använd den här guiden för att installera klienter även om platsen inte är konfigurerad för push-installation av klienter.  

## <a name="software-update-based-installation"></a><a name="BKMK_ClientSUP"></a> Installation baserad på program uppdatering  

Klient installation baserad på program uppdatering publicerar klienten till en program uppdaterings plats som en program uppdatering. Använd den här metoden för att installera eller uppgradera vid första tiden.  

Om Configuration Manager-klienten är installerad på en dator tar datorn emot klient principer från-platsen. Den här principen inkluderar program uppdaterings platsens Server namn och den port som program uppdateringarna ska hämtas från.

> [!IMPORTANT]  
> För installation baserad på program uppdatering använder du samma Windows Server Update Services (WSUS)-Server för klient installation och program uppdateringar. Den här servern måste vara den aktiva programuppdateringsplatsen på en primär plats. Mer information finns i [installera en program uppdaterings plats](../../../sum/get-started/install-a-software-update-point.md).

Om Configuration Manager-klienten inte är installerad på en dator kan du konfigurera och tilldela ett grupprincip-objekt. Grupprincip anger Server namnet på program uppdaterings platsen.  

Du kan inte lägga till kommando rads egenskaper i en klient installation baserad på program uppdatering. Om du har utökat Active Directory-schemat för Configuration Manager, frågar klient installationen automatiskt Active Directory Domain Services efter installations egenskaperna.  

Om du inte har utökat Active Directory schema använder du grupprincip för att etablera klient installations inställningar. De här inställningarna tillämpas automatiskt på klient installation baserad på program uppdatering. Mer information finns i avsnittet om [hur du etablerar klient installations egenskaper](#BKMK_Provision) och artikeln om [hur du tilldelar klienter till en plats](assign-clients-to-a-site.md).  

Använd följande procedurer för att konfigurera datorer utan en Configuration Manager-klient för att använda program uppdaterings platsen. Det finns också en procedur för att publicera-klient program varan på program uppdaterings platsen.  

> [!TIP]  
> Om datorerna är i ett vänte läge som väntar på omstart efter en tidigare programinstallation kan en klient installation baserad på program uppdatering medföra att datorn startas om.  

### <a name="configure-a-group-policy-object-to-specify-the-software-update-point"></a>Konfigurera ett grupprincip-objekt för att ange program uppdaterings platsen  

1. Använd **konsolen Grupprinciphantering** för att öppna ett nytt eller befintligt Grupprincip-objekt.  

2. Expandera **dator konfiguration**, **administrativa mallar**och **Windows-komponenter**och välj sedan **Windows Update**.  

3. Öppna egenskaperna för inställningen **Ange sökväg till tjänsten Microsoft Update på intranätet**och välj sedan **aktive rad**.  

4. **Ange intranät uppdaterings tjänsten för att identifiera uppdateringar**: Ange namn och port för program uppdaterings plats servern.  

    - Om du har konfigurerat Configuration Manager plats systemet så att det använder ett fullständigt kvalificerat domän namn (FQDN) använder du det formatet.  

    - Om det Configuration Manager plats systemet inte har kon figurer ATS för att använda ett fullständigt domän namn, använder du ett kort namn format.

    > [!TIP]  
    > Information om hur du fastställer port numret finns i [så här avgör du vilka port inställningar som används av WSUS](../../../sum/plan-design/plan-for-software-updates.md).

    Exempel i FQDN-format: `http://server1.contoso.com:8530`  

5. **Ange intranäts statistik Server**: den här inställningen konfigureras vanligt vis med samma server namn.

6. Tilldela grupprincip-objektet till de datorer där du vill installera klienten och ta emot program uppdateringar.  

### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>Publicera Configuration Manager-klienten till program uppdaterings platsen  

1. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** .  

2. Välj den plats där du vill konfigurera klient installation baserad på program uppdatering.  

3. På fliken **Start** i menyfliksområdet väljer du **Inställningar för klient installation**i gruppen **Inställningar** och väljer sedan **klient installation baserad på program uppdatering**.  

4. Välj **Aktivera klient installation baserad på program uppdatering**.  

5. Om platsens klient version är nyare än versionen på program uppdaterings platsen öppnas dialog rutan **senare version av klient paket upptäckt** . Välj **Ja** om du vill publicera den senaste versionen.  

    > [!NOTE]  
    > Den här dialog rutan är tom om du inte redan har publicerat klient program varan på program uppdaterings platsen.

Program uppdateringen för den Configuration Manager klienten uppdateras inte automatiskt när det finns en ny version. När du uppdaterar platsen upprepar du proceduren för att uppdatera klienten.  

## <a name="group-policy-installation"></a><a name="BKMK_ClientGP"></a> grupprincip installation

Använd grupprincip i Active Directory Domain Services för att publicera eller tilldela Configuration Manager-klienten. Klienten installeras när datorn startas. När du använder grupprincip visas klienten i **Lägg till eller ta bort program** på kontroll panelen. Användaren kan installera den därifrån.  

Använd Windows Installer paket CCMSetup.msi för grupprincip-baserade installationer. Den här filen finns i `<ConfigMgr installation directory>\bin\i386` mappen på plats servern. Du kan inte lägga till egenskaper i den här filen för att ändra installations beteendet.  

> [!IMPORTANT]  
> Du måste ha administratörs behörighet för att få åtkomst till installationsfilerna för-klienten.  

- Om du har utökat Active Directory-schemat för Configuration Manager och du har valt domänen på fliken **publicering** i dialog rutan **plats egenskaper** söker klient datorer automatiskt Active Directory Domain Services efter installations egenskaper. Mer information finns i [om klient installations egenskaper som publicerats till Active Directory Domain Services](about-client-installation-properties-published-to-active-directory-domain-services.md).  

- Om du inte har utökat Active Directory-schemat läser du avsnittet om hur du [konfigurerar klient installations egenskaper](#BKMK_Provision) för information om hur du lagrar installations egenskaper i Windows-registret på datorer. Klienten använder dessa installations egenskaper när den installeras.  

Mer information finns i [så här använder Grupprincip för att installera program vara på distans](https://support.microsoft.com/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server).  

## <a name="manual-installation"></a><a name="BKMK_Manual"></a> Manuell installation

Installera klient program varan på datorer manuellt med hjälp av CCMSetup.exe. Du kan hitta det här programmet och dess stödfiler i mappen klient i mappen Configuration Manager-installation på plats servern. Platsen delar den här mappen i nätverket som:  

`\\<site server name>\SMS_<site code>\Client\`  

`<site server name>` är namnet på den primära plats servern. `<site code>` är den primära plats koden som klienten är tilldelad till. Om du vill köra CCMSetup.exe från kommando raden på klienten ansluter du till den här nätverks platsen och kör sedan kommandot.  

> [!IMPORTANT]  
> Du måste ha administratörs behörighet för att få åtkomst till installationsfilerna för-klienten.  

CCMSetup.exe kopierar alla nödvändiga komponenter till klient datorn och anropar Windows Installer-paketet (Client.msi) för att installera-klienten. Du kan inte köra Client.msi direkt.  

Ändra klient installationens beteende genom att ange kommando rads alternativ för både CCMSetup.exe och Client.msi. Se till att du anger CCMSetup-parametrar som börjar med `/` innan du anger Client.msi egenskaper. Exempel:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`

I det här exemplet installeras klienten med följande alternativ:  

|Alternativ|Beskrivning|  
|--------------|-----------------|  
|`/mp:SMSMP01`|Den här CCMSetup-parametern anger hanterings platsens SMSMP01 för hämtning av de nödvändiga installationsfilerna för klienter.|  
|`/logon`|Den här CCMSetup-parametern anger att installationen ska avbrytas om en befintlig Configuration Manager-klient hittas på datorn.|  
|`SMSSITECODE=AUTO`|Den här Client.msi egenskapen anger att klienten försöker hitta Configuration Manager platskod som ska användas, genom att använda Active Directory Domain Services, till exempel.|  
|`FSP=SMSFP01`|Den här Client.msi egenskapen anger att återställnings status punkten med namnet SMSFP01 används för att ta emot tillstånds meddelanden som skickas från klient datorn.|  

Mer information finns i [om klient installations parametrar och egenskaper](about-client-installation-properties.md).  

> [!TIP]  
> Information om hur du installerar Configuration Manager-klienten på en modern Windows 10-enhet med Azure Active Directory (Azure AD)-identitet finns i [Installera och tilldela Configuration Manager Windows 10-klienter med Azure AD för autentisering](deploy-clients-cmg-azure.md). Den här proceduren gäller för klienter på ett intranät eller på Internet.  

### <a name="manual-installation-examples"></a>Exempel på manuella installationer

De här exemplen gäller för Active Directory anslutna klienter på ett intranät. De använder följande värden:  

- **MPSERVER**: server som är värd för hanterings platsen
- **FSPSERVER**: server som är värd för återställnings status punkten  
- **ABC**: platskod  
- **contoso.com**: domän namn  

Anta att du har konfigurerat alla plats system servrar med ett intranät-FQDN och publicerat plats informationen till Active Directory.  

Börja med följande steg på klient datorn:  

1. Logga in som lokal administratör.  
2. Mappa enhet Z till `\\MPSERVER\SMS_ABC\Client` .  
3. Växla kommando tolken till enhet Z.  

Kör sedan ett av följande kommandon:  

#### <a name="manual-example-1"></a>Manuellt exempel 1  

`CCMSetup.exe`  

Det här kommandot installerar klienten utan ytterligare parametrar eller egenskaper. Klienten konfigureras automatiskt med de klient installations egenskaper som publiceras till Active Directory Domain Services, inklusive de här inställningarna:  

- Platskod: den här inställningen kräver att klientens nätverks plats inkluderas i en avgränsnings grupp som du har konfigurerat för klient tilldelning.  
- Hanterings plats.
- Återställnings status punkt.
- Kommunicera enbart med HTTPS.  

Mer information finns i [om klient installations egenskaper som publicerats till Active Directory Domain Services](about-client-installation-properties-published-to-active-directory-domain-services.md).  

#### <a name="manual-example-2"></a>Manuellt exempel 2  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
Det här kommandot åsidosätter den automatiska konfiguration som Active Directory Domain Services tillhandahåller. Det kräver inte att du inkluderar klientens nätverks plats i en gränser grupp som är konfigurerad för klient tilldelning. I stället anger installationen dessa inställningar:

- Platskod
- Hanterings plats för intranät
- Internetbaserad hanterings plats
- Återställnings status plats som tar emot anslutningar från Internet
- Använd ett PKI-certifikat (Public Key Infrastructure) för klienter (om tillgängligt) som har den längsta giltighets perioden

## <a name="logon-script-installation"></a><a name="BKMK_ClientLogonScript"></a> Installation av inloggnings skript

Configuration Manager stöder inloggnings skript för att installera Configuration Manager-klient program varan. Använd program filen CCMSetup.exe i ett inloggnings skript för att utlösa klient installationen.  

Vid installation med inloggningsskript går samma metoder att använda som vid manuell installation av klienter. Ange `/logon` installations parametern för CCMSsetup.exe. Om någon version av klienten redan finns på datorn förhindrar den här parametern klienten från att installeras. Det här beteendet förhindrar ominstallation av klienten varje gången inloggnings skriptet körs.  

Om du inte anger en installations källa med hjälp av `/Source` parametern och ingen hanterings plats från vilken du vill hämta installationen anges av `/MP` parametern, CCMSetup.exe letar upp hanterings platsen genom att söka Active Directory Domain Services. Detta inträffar endast om du har utökat schemat för Configuration Manager och publicerat platsen till Active Directory Domain Services. Alternativt kan klienten lokalisera en hanteringsplats via DNS eller WINS.  

## <a name="package-and-program-installation"></a><a name="BKMK_ClientApp"></a> Paket-och program installation

Använd Configuration Manager för att skapa och distribuera ett paket och program som uppgraderar klient programmet för valda enheter. Configuration Manager tillhandahåller en paket definitions fil som fyller i paket egenskaperna med vanliga värden. Anpassa klient installationens beteende genom att ange ytterligare kommando rads parametrar och egenskaper.  

> [!NOTE]  
> Du kan inte uppgradera Configuration Manager 2007-klienter med den här metoden. Uppgradera klienterna automatiskt i stället. Då skapas och distribueras ett paket med den senaste versionen av klienten automatiskt. Mer information finns i [Uppgradera klienter](../manage/upgrade/upgrade-clients.md).  
>
> Mer information om hur du migrerar från äldre versioner av Configuration Manager-klienten finns i [Planera en strategi för klient migrering](../../migration/planning-a-client-migration-strategy.md).  

### <a name="create-a-package-and-program-for-the-client-software"></a>Skapa ett paket och program för klient programmet  

Använd följande procedur för att skapa ett Configuration Manager-paket och-program som du kan distribuera till Configuration Manager klient datorer för att uppgradera klient program varan.  

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **program hantering**och väljer noden **paket** .  

2. På fliken **Start** i menyfliksområdet väljer du **skapa paket från definition**i gruppen **skapa** .  

3. På sidan **paket definition** i guiden väljer du **Microsoft** i listan **utgivare** och väljer **Configuration Manager klient uppgradering** från listan **paket definition** .  

4. På sidan **källfiler** väljer du **Hämta alltid filer från en källmapp**.  

5. På sidan **källmapp** väljer du **nätverks Sök väg (UNC-namn)**. Ange Nätverks Sök vägen för den server och resurs som innehåller klientens installationsfiler.  

    > [!NOTE]  
    > Den dator där Configuration Manager distributionen körs måste ha åtkomst till den angivna nätverksmappen. Annars Miss lyckas klient installationen.  

    Om du vill ändra någon av klient installations egenskaperna ändrar du kommando raden CCMSetup.exe på fliken **Allmänt** i dialog rutan **Egenskaper för tyst uppgradering av Configuration Manager agent** . Standard egenskaperna för installationen är `/noservice SMSSITECODE=AUTO` .  

6. Distribuera paketet till alla distributionsplatser där du vill ha klientuppgraderingspaketet. Distribuera sedan paketet till enhets samlingar som innehåller klienter som du vill uppgradera.  

## <a name="intune-mdm-managed-windows-devices"></a><a name="bkmk_mdm"></a> Intune MDM-hanterade Windows-enheter

Distribuera Configuration Manager-klienten till enheter som har registrerats med Microsoft Intune.

Den här proceduren gäller för en traditionell klient som är ansluten till ett intranät. Den använder traditionella autentiseringsmetoder för klienter. För att se till att enheten behålls i ett hanterat tillstånd efter att klienten har installerats måste den finnas i intranätet och inom en Configuration Manager platsens gränser.  

Anvisningar om hur du installerar Configuration Manager-klienten på en modern Windows 10-enhet med hjälp av Azure AD-identitet finns i [Installera och tilldela Configuration Manager Windows 10-klienter med Azure AD för autentisering](deploy-clients-cmg-azure.md).

När du har installerat Configuration Manager-klienten avregistreras inte enheterna från Intune. De kan använda Configuration Manager klienten och MDM-registrering på samma gång. Mer information finns i [Översikt över samhantering](../../../comanage/overview.md).  

> [!Note]
> Du kan använda andra klient installations metoder för att installera Configuration Manager-klienten på en Intune-hanterad enhet. Om en Intune-hanterad enhet exempelvis finns på intranätet och är ansluten till Active Directory-domänen, kan du använda grup princip för att installera Configuration Manager-klienten.<!-- SCCMDocs#757 -->

### <a name="install-the-configuration-manager-client-by-using-intune"></a>Installera Configuration Manager-klienten med hjälp av Intune

1. I Intune [lägger du till en branschspecifika Windows-app](https://docs.microsoft.com/mem/intune/apps/lob-apps-windows) som innehåller Configuration Manager-klientens installations fil **CCMSetup.msi**. Du hittar den här filen i `\bin\i386` mappen i installations katalogen för Configuration Manager på plats servern.  

2. I Intune Software Publisher anger du kommando rads parametrar. Använd till exempel det här kommandot med en traditionell klient på ett intranät:  

    `CCMSETUPCMD="/MP:<FQDN of management point> SMSMP=<FQDN of management point> SMSSITECODE=<your site code> DNSSUFFIX=<DNS suffix of management point>"`  

    > [!NOTE]  
    > Ett exempel på ett kommando som kan användas med en modern Windows 10-klient med Azure AD-autentisering finns i [så här förbereder du Internetbaserade enheter för samhantering](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).  

3. [Tilldela appen](../../../../intune/apps/apps-deploy.md) till en grupp med de registrerade Windows-datorerna.  

## <a name="os-image-installation"></a><a name="BKMK_ClientImage"></a> Installation av operativ system avbildning

Förinstallera Configuration Manager-klienten på en referens dator som du använder för att skapa en operativ system avbildning.

> [!IMPORTANT]  
> När du använder Configuration Manager aktivitetssekvens för att distribuera en operativ system avbildning, tar steget [förbereda ConfigMgr-klienten](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture) bort Configuration Manager klienten helt.  

### <a name="prepare-the-client-computer-for-imaging"></a>Förbereda klient datorn för avbildning  

1. Installera klient programmet för Configuration Manager manuellt på referens datorn. Mer information finns i [så här installerar du Configuration Manager klienter manuellt](#BKMK_Manual).  

    > [!IMPORTANT]  
    > Ange inte en Configuration Manager Platskod för klienten i CCMSetup.exe kommando rads egenskaper.  

2. I en kommando tolk skriver `net stop ccmexec` du för att stoppa tjänsten för SMS-agenttjänsten (CcmExec.exe) på referens datorn.  

3. Ta bort SMSCFG.INI-filen från Windows-mappen på referens datorn.  

4. Ta bort alla certifikat som lagras i det lokala dator arkivet på referens datorn. Om du t. ex. använder PKI-certifikat måste du ta bort certifikaten i det **personliga** arkivet för **dator** och **användare**innan du avbildar datorn.  

5. Om klienterna är installerade i en annan Configuration Manager-hierarki än referens datorns hierarki tar du bort den betrodda rot nyckeln från referens datorn.  

    > [!NOTE]  
    > Om klienterna inte kan fråga Active Directory Domain Services för att hitta en hanterings plats använder de den betrodda rot nyckeln för att fastställa betrodda hanterings platser. Om du distribuerar alla avbildade klienter i samma hierarki som huvud datorn lämnar du den betrodda rot nyckeln på plats.
    >
    > Om du distribuerar klienterna i olika hierarkier tar du bort den betrodda rot nyckeln. Etablera även dessa klienter med den nya betrodda rot nyckeln. Mer information finns i [Planera för den betrodda rot nyckeln](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

6. Använd din avbildnings program vara för att avbilda en avbildning av referens datorn.  

7. Distribuera avbildningen till mål datorerna.  

## <a name="workgroup-computers"></a><a name="BKMK_ClientWorkgroup"></a> Arbets grupps datorer

Configuration Manager stöder klient installation för datorer i arbets grupper. Installera klienten på arbets grupps datorer med hjälp av metoden som anges i [så här installerar du Configuration Manager klienter manuellt](#BKMK_Manual).  

### <a name="prerequisites"></a>Förutsättningar  

- Installera klienten manuellt på varje arbets grupps dator. Under installationen måste den interaktiva användaren ha lokal administratörs behörighet.  

- Konfigurera nätverks åtkomst kontot för platsen för att få åtkomst till resurser i Configuration Manager plats Server domän. Ange det här kontot i plats komponenten för program varu distribution. Mer information finns i [plats komponenter](../../servers/deploy/configure/site-components.md).  

### <a name="limitations"></a>Begränsningar  

- Arbets grupps klienter kan inte hitta hanterings platser från Active Directory Domain Services. I stället använder de DNS, WINS eller någon annan hanterings plats.  

- Global nätverks växling stöds inte. Arbets grupps klienter kan inte fråga Active Directory Domain Services för plats information.  

- Active Directory identifierings metoder kan inte identifiera datorer i arbets grupper.  

- Du kan inte distribuera program vara till användare av arbets grupps datorer.  

- Du kan inte använda push-installation av klienter för att installera-klienten på arbets grupps datorer.  

- Arbets grupps klienter kan inte använda Kerberos för autentisering, och de kan kräva manuellt godkännande.  

- Du kan inte konfigurera en arbets grupps klient som en distributions plats. Configuration Manager kräver att distributions plats datorerna är medlemmar i en domän.  

### <a name="install-the-client-on-workgroup-computers"></a>Installera klienten på arbets grupps datorer  

Kontrol lera kraven och följ anvisningarna i avsnittet [så här installerar du Configuration Manager-klienter manuellt](#BKMK_Manual).  

#### <a name="workgroup-example-1"></a>Arbets grupps exempel 1

I det här exemplet utförs följande åtgärder:

- Installerar klienten för klient hantering för intranät
- Anger plats koden
- Anger DNS-suffixet för att hitta en hanterings plats  

`CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

#### <a name="workgroup-example-2"></a>Arbets grupps exempel 2

Det här exemplet kräver att klienten finns på en nätverks plats som har kon figurer ATS i en avgränsnings grupp. Om detta krav inte uppfylls fungerar inte automatiskt platstilldelning. Kommandot innehåller en återställnings status plats på servern FSPSERVER. Med den här egenskapen kan du spåra klient distribution och identifiera eventuella klient kommunikations problem.

`CCMSetup.exe FSP=fspserver.constoso.com`  

## <a name="internet-based-client-management"></a><a name="BKMK_ClientInternet"></a> Internetbaserad klient hantering  

> [!NOTE]  
> Det här avsnittet gäller inte för klienter som använder en [Gateway för moln hantering](../manage/cmg/plan-cloud-management-gateway.md). Om du vill installera Internetbaserade klienter med hjälp av en Cloud Management Gateway, se [Installera och tilldela Configuration Manager Windows 10-klienter med Azure AD för autentisering](deploy-clients-cmg-azure.md).  

Om Configuration Manager-platsen stöder [Internetbaserad klient hantering](../manage/plan-internet-based-client-management.md) för klienter som ibland finns på ett intranät och ibland på Internet, har du två alternativ när du installerar klienter på intranätet:  

- Ta med egenskapen Client.msi `CCMHOSTNAME=<internet FQDN of the internet-based management point>` när du installerar-klienten genom att använda manuell installation eller klient-push, till exempel. När du använder den här metoden tilldelar du klienten en plats direkt. Du kan inte använda automatisk platstilldelning. Se avsnittet [så här installerar du Configuration Manager klienter manuellt](#BKMK_Manual) , som innehåller ett exempel på den här konfigurations metoden.  

- Installera klienten för intranäts klient hantering och tilldela klienten en Internetbaserad klient hanterings plats. Ändra hanterings platsen genom att använda klient egenskaperna på sidan **Configuration Manager** på kontroll panelen eller genom att använda ett skript. När du använder den här metoden kan du använda automatisk klienttilldelning. Mer information finns i avsnittet [så här konfigurerar du klienter för internetbaserad klient hantering efter klient installation](#BKMK_ConfigureIBCM_MP) .  

Om du vill installera klienter som finns på Internet väljer du någon av följande metoder som stöds:  

- Tillhandahålla en mekanism för dessa klienter att tillfälligt ansluta till intranätet med ett VPN. Installera sedan klienten genom att använda valfri lämplig klient installations metod.  

- Använd en installations metod som är oberoende av Configuration Manager. Paketera till exempel källfilerna för klient installationen till ett flyttbart medium och skicka mediet till användarna. Källfilerna för klient installation finns i `<installation path>\Client` mappen på Configuration Manager plats Server. På mediet lägger du till ett skript som kan kopieras manuellt över mappen client. I den här mappen installerar du klienten med hjälp av CCMSetup.exe och alla lämpliga kommando rads egenskaper för CCMSetup.  

> [!NOTE]  
> Configuration Manager stöder inte installation av en klient direkt från den Internetbaserade hanterings platsen eller från den Internetbaserade program uppdaterings platsen.

Klienter som hanteras via Internet måste kommunicera med Internetbaserade plats system. Se till att dessa klienter också har PKI-certifikat (Public Key Infrastructure) innan du installerar-klienten. Installera dessa certifikat oberoende av Configuration Manager. Mer information finns i [krav för PKI-certifikat](../../plan-design/network/pki-certificate-requirements.md).  

### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Installera klienter på Internet genom att ange kommando rads egenskaper för CCMSetup  

1. Följ anvisningarna i avsnittet [så här installerar du Configuration Manager-klienter manuellt](#BKMK_Manual). Inkludera alltid följande alternativ:  

    - Kommando rads parameter för CCMSetup `/source:<local path of the copied Client folder>`  

    - Kommando rads parameter för CCMSetup `/UsePKICert`  

    - Client.msi egenskap `CCMHOSTNAME=<FQDN of internet-based management point>`  

    - Client.msi egenskap `SMSSIGNCERT=<local path of exported site server signing certificate>`  

    - Client.msi egenskap `SMSSITECODE=<site code of internet-based management point>`  

    > [!NOTE]  
    > Om platsen har fler än en Internetbaserad hanterings plats spelar det ingen roll vilken som du anger för `CCMHOSTNAME` egenskapen. När en Configuration Manager-klient ansluter till den angivna Internetbaserade hanterings platsen skickar den en lista över tillgängliga Internetbaserade hanterings platser på platsen. Klienten väljer slumpmässigt en i listan.

2. Om du inte vill att klienten ska kontrol lera listan över återkallade certifikat (CRL) anger du kommando rads parametern CCMSetup `/NoCRLCheck` .  

3. Om du använder en Internetbaserad återställnings status plats anger du egenskapen Client.msi `FSP=<internet FQDN of the internet-based fallback status point>` .  

4. Om du installerar klienten för klient hantering enbart för Internet anger du egenskapen Client.msi `CCMALWAYSINF=1` .  

5. Avgör om du måste ange ytterligare kommando rads parametrar för CCMSetup. Om klienten till exempel har mer än ett giltigt PKI-certifikat kan du behöva ange ett kriterium för val av certifikat. En lista över tillgängliga egenskaper finns i [om klient installations parametrar och egenskaper](about-client-installation-properties.md).  

#### <a name="internet-based-example"></a>Internet-baserat exempel

`CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`

I det här exemplet installeras klienten med följande beteenden:

- Använd källfiler från en mapp på enhet D.
- Använd ett PKI-klientcertifikat.
- Välj det certifikat som har den längsta giltighets perioden.
- Klient hantering enbart för Internet.
- Tilldela klienten att använda den Internetbaserade hanterings platsen med namnet SERVER1.
- Tilldela den Internetbaserade återställnings status punkten i contoso.com-domänen.
- Tilldela klienten till ABC-webbplatsen.  

### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation"></a><a name="BKMK_ConfigureIBCM_MP"></a> Konfigurera klienter för internetbaserad klient hantering efter klient installation  

Använd någon av dessa procedurer för att tilldela den Internetbaserade hanterings platsen när du har installerat-klienten. Den första konfigurationen kräver manuell konfiguration och är lämplig för ett fåtal klienter. Den andra är lämpligare för att konfigurera många klienter.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-from-the-configuration-manager-control-panel"></a>Konfigurera klienter för internetbaserad klient hantering efter klient installation från Configuration Manager kontroll panelen  

1. Öppna **Configuration Manager** kontroll panelen på klienten.  

2. På fliken **Internet** anger du det fullständigt kvalificerade domän namnet (FQDN) för den Internetbaserade hanterings platsen som Internet- **FQDN**.  

    > [!NOTE]  
    > Fliken **Internet** är endast tillgänglig om klienten har ett PKI-klientcertifikat.  

3. Om klienten ansluter till Internet med hjälp av en proxyserver anger du inställningarna för proxyservern.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Konfigurera klienter för internetbaserad klient hantering efter klient installation genom att använda ett skript  

##### <a name="powershell"></a>PowerShell

1. Öppna en PowerShell-redigerare i rad, t. ex. PowerShell ISE eller Visual Studio Code. Du kan också använda en text redigerare, t. ex. anteckningar.

2. Kopiera och infoga följande rader kod i redigeraren. Ersätt `'mp.contoso.com'` med Internet-FQDN för din Internetbaserade hanterings plats.

    ``` PowerShell
    $newInternetBasedManagementPointFQDN = 'mp.contoso.com'
    $client = New-Object -ComObject Microsoft.SMS.Client
    $client.SetInternetManagementPointFQDN($newInternetBasedManagementPointFQDN)
    Restart-Service CcmExec
    $client.GetInternetManagementPointFQDN()
    ```

    > [!NOTE]  
    > Den sista raden är bara att verifiera det nya värdet för Internet hanterings platsen.
    >
    > Om du vill ta bort en specifik Internetbaserad hanterings plats tar du bort serverns FQDN-värde inom citat tecken. Raden blir `$newInternetBasedManagementPointFQDN = ''` .

3. Spara filen med fil namns tillägget. ps1.  

4. Kör skriptet med förhöjd behörighet på klient datorer. Använd någon av följande metoder:  

    - Distribuera filen till befintliga Configuration Manager-klienter med ett paket och ett program.  

    - Kör filen lokalt på befintliga Configuration Manager-klienter genom att dubbelklicka på skript filen i Utforskaren.  

Du kanske måste starta om klienten för att ändringarna ska börja gälla.  

## <a name="provision-client-installation-properties"></a><a name="BKMK_Provision"></a> Etablera klient installations egenskaper

Etablera klient installations egenskaper för grup princip och klient installationer som baseras på program uppdatering. Använd Windows grupprincip för att etablera datorer med Configuration Manager klient installations egenskaper. Egenskaperna lagras i datorns register. Klienten läser dem när den installeras. Den här proceduren krävs normalt inte, men kan krävas för vissa klient installations scenarier, till exempel:  

- Du använder de grup princip inställningar eller klient installations metoder som är baserade på program uppdatering. Du har inte utökat Active Directorys schema för Configuration Manager.  

- Du vill åsidosätta klientinstallationsegenskaper på vissa specifika datorer.  

> [!NOTE]  
> Om några installations egenskaper anges på CCMSetup.exe kommando rad används inte installations egenskaper som är etablerade på datorer.

En administrativ mall för grup princip `ConfigMgrInstallation.adm` som heter anges på installations mediet för Configuration Manager. Använd den här mallen för att etablera klient datorer med installations egenskaper.

> [!TIP]
> Som standard `ConfigMgrInstallation.adm` stöder inte strängar som är större än 255 tecken. Den här konfigurationen kan påverka hur du lägger till flera parametrar eller parametrar med långa värden, till exempel CCMCERTISSUERS.<!-- SCCMDocs#1648 -->
>
> Så här löser du det här problemet:
>
> 1. Redigera `ConfigMgrInstallation.adm` i anteckningar.
> 2. `VALUENAME SetupParameters`Ändra `MAXLEN` värdet till ett större heltal för egenskapen. Till exempel `MAXLEN 511`.

### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Konfigurera och tilldela klient installations egenskaper med hjälp av ett grup princip objekt  

1. Importera den administrativa mallen ConfigMgrInstallation. adm till ett nytt eller befintligt grup princip objekt (GPO) med hjälp av ett redigerings program som Windows Redigeraren för grupprincipobjekt. Du hittar den här filen i `TOOLS\ConfigMgrADMTemplates` mappen på installations mediet för Configuration Manager.  

2. Öppna egenskaperna för den importerade inställningen **Konfigurera klientdistributionsinställningar**.  

3. Välj **Aktiverad**.  

4. I rutan **CCMSetup** anger du de CCMSetup-kommandoradsegenskaper som krävs. En lista över alla kommando rads egenskaper för CCMSetup och exempel på hur de används finns i [om klient installations parametrar och egenskaper](about-client-installation-properties.md).  

5. Tilldela GRUPPRINCIPOBJEKTet till de datorer som du vill etablera med Configuration Manager klient installations egenskaper.