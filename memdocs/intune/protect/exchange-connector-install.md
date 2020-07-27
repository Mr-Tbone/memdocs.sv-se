---
title: Konfigurera Microsoft Intune Exchange Connector
titleSuffix: Microsoft Intune
description: Använd lokala Intune Exchange Connector för att hantera enhetsåtkomst till Exchange-postlådor baserat på Intune-registrering och Exchange ActiveSync (EAS).
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a0376ea1-eb13-4f13-84da-7fd92d8cd63c
ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e646ce40acaa156910f516c475cd6b0885989941
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462207"
---
# <a name="set-up-the-on-premises-intune-exchange-connector"></a>Konfigurera lokala Intune Exchange Connector

> [!IMPORTANT]
> Informationen i den här artikeln gäller för kunder som kan använda ett Exchange-anslutningsprogram.
>
> Från och med juli 2020 är stödet för Exchange-anslutningsprogrammet inaktuellt och ersätts av [modern hybridautentisering](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) (HMA) i Exchange.  Om du har konfigurerat ett Exchange-anslutningsprogram i din miljö kan Intune-klientorganisationen fortsätta att använda det, och du fortsätter att ha tillgång till gränssnittet som har stöd för konfigurationen. Du kan fortsätta att använda anslutningsprogrammet eller konfigurera modern hybridanslutning (HMA) och sedan avinstallera anslutningsprogrammet.
>
>Om du använder HMA behöver inte Intune installera och använda Exchange-anslutningsprogrammet. Med den här ändringen tas gränssnittet för att konfigurera och hantera Exchange-anslutningsprogram för Intune bort från administrationscentret för Microsoft Endpoint Manager, om du inte redan använder ett Exchange-anslutningsprogram i din prenumeration.

För att skydda åtkomsten till Exchange använder Intune en lokal komponent kallad Microsoft Intune Exchange Connector. På vissa ställen i Intune-konsolen kallas det här anslutningsprogrammet även för *Exchange ActiveSync On-Premises Connector*.

> [!IMPORTANT]
> Intune tar bort stödet för funktionen Exchange On-premises Connector från Intune-tjänsten från och med version 2007 (juli). Befintliga kunder med aktiva anslutningsprogram kan fortsätta att använda funktionen. Nya kunder och befintliga kunder som inte har något aktivt anslutningsprogram kan inte längre skapa nya anslutningsprogram eller hantera EAS-enheter (Exchange ActiveSync) från Intune. Microsoft rekommenderar sådana klientorganisationer att skydda åtkomsten till Exchange lokalt med [HMA (modern hybridautentisering)](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview). HMA ger tillgång till både Intune-appskyddspolicyer (kallas även MAM) och villkorsstyrd åtkomst via Outlook Mobile för Exchange lokalt.

Informationen i den här artikeln beskriver hur du installerar och övervakar Intune Exchange Connector. Du kan använda anslutningsprogrammet med [principer för villkorlig åtkomst](conditional-access-exchange-create.md) för att tillåta eller blockera åtkomsten till dina postlådor i Exchange On-Premises.

Anslutningsprogrammet installeras och körs på din lokala maskinvara. Det identifierar enheter som ansluter till Exchange och kommunicerar enhetsinformation till Intune-tjänsten. Anslutningsprogrammet tillåter eller blockerar enheter beroende på om de har registrerats och är kompatibla. HTTPS-protokollet används för den här kommunikationen.

När en enhet försöker komma åt din lokala Exchange-server mappar Exchange Connector AES-poster (Exchange ActiveSync) i Exchange Server till Intune-poster för att kontrollera att enheten har registrerats med Intune och att den uppfyller enhetens principer. Beroende på dina principer för villkorlig åtkomst tillåts eller blockeras enheten. Mer information finns i [Hur används villkorsstyrd åtkomst vanligtvis med Intune?](conditional-access-intune-common-ways-use.md)

Både *identifieringsaktiviteter* och *tillåt/blockera-åtgärder* utförs med vanliga Exchange PowerShell-cmdlets. Dessa åtgärder utförs med det tjänstkonto som upprättas när Exchange Connector installeras.

Intune stöder installation av flera Intune Exchange-anslutningsprogram per prenumeration. Om du har fler än en lokal Exchange-organisation kan du konfigurera en separat anslutningsapp för varje sådan. Dock kan endast ett anslutningsprogram installeras per Exchange-organisation.  

Följ dessa allmänna steg för att konfigurera en anslutning som gör att Intune kan kommunicera med den lokala Exchange-servern:

1. Ladda ned det lokala anslutningsprogrammet från Intune-portalen.
2. Installera och konfigurera Exchange-anslutningsappen på en dator i den lokala Exchange-organisationen.
3. Verifiera Exchange-anslutningen.
4. Upprepa dessa steg för varje ytterligare Exchange-organisation som du vill ansluta till Intune.

## <a name="how-conditional-access-for-exchange-on-premises-works"></a>Hur villkorlig lokal åtkomst för Exchange lokalt fungerar

Villkorlig åtkomst för Exchange lokalt fungerar annorlunda än villkorliga åtkomstprinciper för Azure. Du installerar det lokala Intune Exchange-anslutningsprogrammet för att interagera direkt med Exchange-servern. Intune Exchange Connector tar emot alla Exchange Active Sync-poster (EAS) som finns på Exchange-servern, så att Intune kan ta dessa EAS-poster och mappa den till Intune-enhetsposterna. Dessa poster och enheter har registrerats och identifierats av Intune. Den här processen tillåter eller blockerar åtkomst till e-post.

Om EAS-posten är ny och Intune inte känner till detta, utfärdas en cmdlet som uppmanar Exchange-servern att blockera åtkomsten till e-post. Här följer lite mer information om hur den här processen fungerar:

> [!div class="mx-imgBorder"]
> ![Flödesschema för Exchange lokalt med CA](./media/exchange-connector-install/ca-intune-common-ways-1.png)

1. Användaren försöker få åtkomst till företagets e-post som finns på Exchange lokalt, version 2010 SP1 eller senare.

2. Om enheten inte hanteras av Intune, blockeras åtkomsten till e-post. Intune skickar ett blockeringsmeddelande till EAS-klienten.

3. EAS får blockeringsmeddelandet, försätter enheten i karantän och skickar karantänsmeddelandet med åtgärdsförslag. Meddelandet innehåller länkar som användarna kan använda för att registrera sina enheter.

4. Den arbetsplatsanslutna processen är det första steget mot att låta enheten hanteras av Intune.

5. Enheten registreras i Intune.

6. Intune mappar EAS-posten till en enhetspost, och sparar enhetens efterlevnadstillstånd.

7. EAS-klient-ID:t registreras i Azure AD:s enhetsregistreringsprocess, i vilken det skapas en relation mellan Intune-enhetsposten och EAS-klient-ID:t.

8. Under Azure AD:s enhetsregistrering sparas enhetens statusinformation.

9. Om användaren uppfyller principerna för villkorsstyrd åtkomst, skickar Intune en cmdlet via Intune Exchange Connector som tillåter att postlådan synkroniseras.

10. Exchange-servern skickar meddelandet till EAS-klienten, så att användaren får åtkomst till e-posten.

## <a name="intune-exchange-connector-requirements"></a>Krav för Intune Exchange Connector

För att ansluta till Exchange behöver du ett konto som har en Intune-licens som anslutningsprogrammet kan använda. Du anger kontot när du installerar anslutningsprogrammet.  

Följande tabell innehåller kraven för datorn där du installerar den lokala Intune Exchange Connector.  

|  Krav  |   Mer information     |
|---------------|------------------------|
|  Operativsystem        | Intune har stöd för Intune Exchange Connector på datorer som kör någon utgåva av Windows Server 2008 SP2 64-bitars, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 eller Windows Server 2016.<br /><br />Anslutningsappen stöds inte i Server Core-installationer.  |
| Microsoft Exchange          | För lokala anslutningar krävs Microsoft Exchange 2010 SP3 eller senare, eller äldre Exchange Online Dedicated. Om du vill ta reda på om Exchange Online Dedicated-miljön har den *nya* eller *äldre* konfigurationen kontaktar du din kontoansvariga. |
| Utfärdare för hantering av mobila enheter           | [Ange utfärdare för hantering av mobila enheter till Intune](../fundamentals/mdm-authority-set.md). |
| Maskinvara              | Datorn där du installerar anslutningen måste ha en 1,6 GHz-processor med 2 GB RAM-minne och 10 GB ledigt diskutrymme. |
|  Active Directory-synkronisering             | [Konfigurera Active Directory-synkronisering](../fundamentals/users-add.md) innan du använder anslutningsprogrammet för att ansluta Intune till Exchange-servern. Dina lokala användare och säkerhetsgrupper måste synkroniseras med din instans av Azure Active Directory. |
| Tilläggsprogramvara         | Datorn som är värd för anslutningsprogrammet måste ha en fullständig installation av Microsoft .NET Framework 4.5 och Windows PowerShell 2.0. |
| Nätverk               | Datorn där du installerar anslutningsprogrammet måste finnas i en domän som har en förtroenderelation med domänen som är värd för Exchange-servern.<br /><br />Konfigurera datorn så att den har åtkomst till Intune-tjänsten via brandväggar och proxyservrar på portarna 80 och 443. Intune använder följande domäner: <br> - manage.microsoft.com <br> - \*manage.microsoft.com<br> - \*.manage.microsoft.com <br><br> Intune Exchange Connector kommunicerar med följande tjänster: <br> - Intune-tjänsten: HTTPS-port 443 <br> - Exchange Client Access Server (CAS): WinRM-tjänsten på port 443<br> - Automatisk upptäckt i Exchange på port 443<br> - Webbtjänster i Exchange (EWS) på port 443  |

### <a name="exchange-cmdlet-requirements"></a>Krav för Exchange-cmdlet

Skapa ett Active Directory-användarkonto för Intune Exchange Connector. Kontot måste ha behörighet att köra följande Windows PowerShell-cmdlets för Exchange:  

- `Get-ActiveSyncOrganizationSettings`, `Set-ActiveSyncOrganizationSettings`
- `Get-CasMailbox`, `Set-CasMailbox`
- `Get-ActiveSyncMailboxPolicy`, `Set-ActiveSyncMailboxPolicy`, `New-ActiveSyncMailboxPolicy`, `Remove-ActiveSyncMailboxPolicy`
- `Get-ActiveSyncDeviceAccessRule`, `Set-ActiveSyncDeviceAccessRule`, `New-ActiveSyncDeviceAccessRule`, `Remove-ActiveSyncDeviceAccessRule`
- `Get-ActiveSyncDeviceStatistics`
- `Get-ActiveSyncDevice`
- `Get-ExchangeServer`
- `Get-ActiveSyncDeviceClass`
- `Get-Recipient`
- `Clear-ActiveSyncDevice`, `Remove-ActiveSyncDevice`
- `Set-ADServerSettings`
- `Get-Command`

## <a name="download-the-installation-package"></a>Ladda ned installationspaketet

På en Windows-server som har stöd för Intune Exchange Connector:

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).  Använd ett konto som är administratör på den lokala Exchange-servern och som har en Exchange Server-licens.

2. Välj **Innehavaradministratör** > **Exchange-åtkomst**.

3. Under **Installation** väljer du **Exchange ActiveSync On-Premises Connector** och sedan **Lägg till**.

   > [!div class="mx-imgBorder"]
   > ![Lägga till en lokal Exchange ActiveSync-anslutningsapp](./media/exchange-connector-install/add-connector.png)

4. På sidan **Lägg till anslutningsapp** väljer du **Ladda ned den lokala anslutningsappen**. Intune Exchange Connector finns i en komprimerad mapp (.zip) som kan öppnas eller sparas. I dialogrutan **Filhämtning** klickar du på **Spara** för att spara den komprimerade mappen på en säker plats.

## <a name="install-and-configure-the-intune-exchange-connector"></a>Installera och konfigurera Intune Exchange Connector

Installera Intune Exchange Connector genom att följa stegen nedan. Om du har flera Exchange-organisationer upprepar du stegen för varje Exchange-anslutningsprogram som du vill konfigurera.

1. Använd ett operativsystem med stöd för Intune Exchange Connector och extrahera filerna i **Exchange_Connector_Setup.zip** till en säker plats.
   > [!IMPORTANT]
   > Byt inte namn på eller flytta filerna i mappen *Exchange_Connector_Setup*. Sådana ändringar gör att installationen av anslutningsprogrammet misslyckas.

2. När filerna har extraherats öppnar du den extraherade mappen och dubbelklickar på **Exchange_Connector_Setup.exe** för att installera anslutningsprogrammet.

   > [!IMPORTANT]
   > Om målmappen inte är en säker plats tar du bort certifikatfilen *MicrosoftIntune.accountcert* när du har installerat dina lokala anslutningsprogram.

3. I dialogrutan **Microsoft Intune Exchange Connector** väljer du antingen **On-premises Microsoft Exchange Server** eller **Hosted Microsoft Exchange Server**.

   ![Bild som visar var du väljer Exchange Server-typ](./media/exchange-connector-install/intune-sa-exchange-connector-config.png)

   För en on-premises Exchange-server anger du antingen servernamnet eller det fullständigt kvalificerade domännamnet för Exchange-servern som är värd för **klientåtkomstserverrollen**.

   För en värdbaserad Exchange-server anger du adressen till Exchange-servern. Så här hittar du URL-adressen till den värdbaserade Exchange-servern:

   1. Öppna Outlook för Office 365.

   2. Välj ikonen **?** längst upp till vänster och välj sedan **Om**.

   3. Leta upp värdet för **POP extern server** .

   4. Välj **Proxyserver** om du vill ange proxyserverinställningar för den värdbaserade Exchange-servern.

       1. Välj **Använd en proxyserver vid synkronisering av information om mobila enheter**.

       1. Ange **proxyserverns namn** och **portnummer** som används för att logga in på servern.

       1. Om autentiseringsuppgifter krävs för åtkomst till proxyservern väljer du **Använd autentiseringsuppgifter för att ansluta till proxyservern**. Ange **domän\användare** och **lösenordet**.

       1. Välj **OK**.

4. I fälten **Användare (domän\användare)** och **Lösenord** anger du autentiseringsuppgifterna för att ansluta till Exchange-servern. Det konto som du anger måste ha en licens för att använda Intune.

5. Ange autentiseringsuppgifter för att skicka meddelanden till en användares Exchange Server-postlåda. Den här användaren kan vara dedikerad till enbart meddelanden. Meddelandeanvändaren behöver en Exchange-postlåda för att skicka meddelanden via e-post. Du kan konfigurera dessa meddelanden med hjälp av principer för villkorlig åtkomst i Intune.

   Kontrollera att tjänsten Automatisk upptäckt och Exchange-webbtjänster har konfigurerats på Exchange CAS-servern. Mer information finns i avsnittet om [klientåtkomstservern](https://technet.microsoft.com/library/dd298114.aspx).

6. I fältet **Lösenord** anger du lösenordet för det här kontot så att Intune kan ansluta till Exchange-servern.

   > [!NOTE]
   > Det konto som du använder för att logga in på klienten måste minst vara Intune-tjänstadministratör. Utan den typen av administratörskonto misslyckas anslutningen med felet ”Fjärrservern returnerade ett fel: (400) Felaktig begäran.”

7. Välj **Anslut**.

   > [!NOTE]
   > Det kan ta några minuter att konfigurera anslutningen.

Under konfigurationen lagrar Exchange Connector dina proxyinställningar för åtkomst till Internet. Om proxyinställningarna ändras konfigurerar du om Exchange Connector så att de uppdaterade proxyinställningarna tillämpas i Exchange Connector.

När Exchange Connector har konfigurerat anslutningen synkroniseras automatiskt mobila enheter som är kopplade till Exchange-hanterade användare och läggs till i Exchange Connector. Synkroniseringen kan ta lite tid att slutföra.

> [!NOTE]
> Om du installerar Intune Exchange Connector och senare behöver ta bort Exchange-anslutningen måste du avinstallera anslutningsprogrammet från den dator där det installerades.

## <a name="install-connectors-for-multiple-exchange-organizations"></a>Installera anslutningsappar för flera Exchange-organisationer

Intune stöder flera Intune Exchange-anslutningsprogram per prenumeration. För en klientorganisation som har flera Exchange-organisationer kan du bara installera ett anslutningsprogram per Exchange-organisation.

Om du vill installera anslutningsprogram för att kunna ansluta till flera Exchange-organisationer laddar du ned .zip-mappen en gång. Återanvänd samma nedladdning för varje anslutningsprogram som du installerar. För varje ytterligare anslutningsapp följer du stegen i föregående avsnitt för att extrahera och köra installationsprogrammet på en server i Exchange-organisationen.

Alla Exchange-organisationer som ansluter till Intune stöder hög tillgänglighet, övervakning och manuell synkronisering. Dessa funktioner beskrivs i följande avsnitt.

## <a name="on-premises-intune-exchange-connector-high-availability-support"></a>Stöd för hög tillgänglighet i lokala Intune Exchange Connector  

För det lokala anslutningsprogrammet innebär hög tillgänglighet att om den Exchange CAS-server som anslutningsprogrammet använder blir otillgänglig, så kan anslutningsprogrammet växla till en annan CAS-server för den aktuella Exchange-organisationen. Exchange Connector i sig har inte stöd för hög tillgänglighet. Om anslutningsappen slutar fungera finns det ingen automatisk redundans, och du måste då byta ut den anslutningsappen genom att [installera en ny anslutningsapp](#reinstall-the-intune-exchange-connector).

Vid en redundansväxling använder anslutningsprogrammet den angivna CAS-servern för att upprätta en anslutning till Exchange. Därefter identifieras ytterligare CAS-servrar för den aktuella Exchange-organisationen. Den här identifieringen gör det möjligt för anslutningsprogrammet att redundansväxla till en annan CAS-server om en sådan finns tillgänglig, tills den primära CAS-servern blir tillgänglig.

Som standard är identifiering av ytterligare CAS aktiverad. Om du behöver inaktivera redundans:

1. På den server där Exchange Connector är installerat går du till **%*ProgramData*%\Microsoft\Windows Intune Exchange Connector**.

2. Med en textredigerare öppnar du **OnPremisesExchangeConnectorServiceConfiguration.xml**.

3. Ändra **\<IsCasFailoverEnabled>*true*\</IsCasFailoverEnabled>** till **\<IsCasFailoverEnabled>*false*\</IsCasFailoverEnabled>** .

## <a name="performance-tune-the-exchange-connector-optional"></a>Justera prestanda för Exchange Connector (valfritt)

När Exchange ActiveSync hanterar 5 000 eller fler enheter kan du konfigurera en valfri inställning för att förbättra anslutningsprogrammets prestanda. Du kan förbättra prestanda genom att tillåta Exchange att använda flera instanser av ett körningsutrymme för PowerShell-kommandon.

Innan du gör den här ändringen kontrollerar du att det konto som du använder för att köra Exchange Connector inte används för andra Exchange-hanteringsbehov. Ett Exchange-konto har ett begränsat antal körningsutrymmen och anslutningsprogrammet använder de flesta av dem.

Prestandajustering är inte lämpligt för anslutningsprogram som körs på äldre eller långsammare maskinvara.

Så här förbättrar du prestanda i Exchange Connector:

1. Öppna installationskatalogen för anslutningsprogrammet på den server där anslutningsprogrammet är installerat.  Standardplatsen är *C:\ProgramData\Microsoft\Windows Intune Exchange Connector*.

2. Redigera filen *OnPremisesExchangeConnectorServiceConfiguration.xml*.

3. Leta upp **EnableParallelCommandSupport** och ange värdet till **true**:

   \<EnableParallelCommandSupport>true\</EnableParallelCommandSupport>

4. Spara filen och starta om Microsoft Intune Exchange Connector-tjänsten.

## <a name="reinstall-the-intune-exchange-connector"></a>Installera om Intune Exchange Connector

Du kan behöva installera om ett Intune Exchange-anslutningsprogram. Endast ett anslutningsprogram kan ansluta till respektive Exchange-organisation. Det betyder att om du installerar ett andra anslutningsprogram för en organisation så ersätter det nya anslutningsprogrammet som du installerar det ursprungliga anslutningsprogrammet.

1. Du kan installera det nya anslutningsprogrammet genom att följa stegen i avsnittet [Installera och konfigurera Exchange Connector](#install-and-configure-the-intune-exchange-connector).

2. När du uppmanas väljer du **Ersätt** för att installera den nya anslutningsappen.
   ![Konfigurationsvarning om att ersätta ett anslutningsprogram](./media/exchange-connector-install/prompt-to-replace.png)

3. Fortsätt med stegen i avsnittet [Installera och konfigurera Intune Exchange Connector](#install-and-configure-the-intune-exchange-connector) och logga in i Intune igen.

4. I det sista fönstret väljer du **Stäng** för att slutföra installationen.
   ![Slutföra installationen](./media/exchange-connector-install/successful-reinstall.png)

## <a name="monitor-an-exchange-connector"></a>Övervaka ett Exchange-anslutningsprogram

När du har konfigurerat Exchange-anslutningsprogrammet kan du visa statusen för anslutningarna och det senaste lyckade synkroniseringsförsöket:

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Välj **Innehavaradministratör** > **Exchange-åtkomst**.

3. Välj **lokal Exchange ActiveSync-anslutningsapp** och lägg sedan till den anslutningsapp som du vill visa.

4. Konsolen visar information om den anslutningsapp som du väljer, där du kan visa **Status** och datum och tid för den senaste lyckade synkroniseringen.

Utöver statusen i konsolen kan du använda [System Center Operations Manager-hanteringspaketet för Exchange-anslutningsappen och Intune](https://www.microsoft.com/download/details.aspx?id=55990&751be11f-ede8-5a0c-058c-2ee190a24fa6=True&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True&fa43d42b-25b5-4a42-fe9b-1634f450f5ee=True). Med hanteringspaketet kan du övervaka Exchange Connector på olika sätt om du behöver felsöka problem.

## <a name="manually-force-a-quick-sync-or-full-sync"></a>Tvinga en snabbsynkronisering eller en fullständig synkronisering manuellt

Intune Exchange Connector synkroniserar automatiskt och regelbundet EAS- och Intune-enhetsposterna. Om efterlevnadsstatusen för en enhet ändras uppdaterar den automatiska synkroniseringsprocessen posterna regelbundet så att enhetsåtkomst kan blockeras eller tillåtas.

- En **snabbsynkronisering** görs regelbundet flera gånger om dagen. Vid en snabbsynkronisering hämtas enhetsinformation för Intune-licensierade och lokala Exchange-användare med villkorlig åtkomst som har ändrats sedan den senaste synkroniseringen.

- En **fullständig synkronisering** utförs en gång om dagen som standard. Vid en fullständig synkronisering hämtas enhetsinformation för alla Intune-licensierade och lokala Exchange-användare med villkorlig åtkomst. En fullständig synkronisering hämtar även information om Exchange Server och ser till att konfigurationen som anges av Intune på Azure-portalen är uppdaterad på Exchange-servern.

Du kan tvinga ett anslutningsprogram att synkronisera med alternativen **Snabbsynkronisering** eller **Fullständig synkronisering** på Intune-instrumentpanelen:

   1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

   2. Välj **Klientadministration** > **Exchange-åtkomst** >  **lokal Exchange ActiveSync-anslutningsapp**.

   3. Välj den anslutningsapp du vill synkronisera och välj sedan Snabbsynkronisering eller Fullständig synkronisering.

   > [!div class="mx-imgBorder"]
   > ![Exempel på skärmbild på anslutningsappinformation](./media/exchange-connector-install/connector-details.png)

## <a name="next-steps"></a>Nästa steg

Skapa en [princip för villkorsstyrd åtkomst för lokala Exchange-servrar](conditional-access-exchange-create.md).
