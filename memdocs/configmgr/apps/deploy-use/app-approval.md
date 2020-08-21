---
title: Godkänna program
titleSuffix: Configuration Manager
description: Lär dig mer om inställningar och beteenden för program godkännande i Configuration Manager.
ms.date: 05/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15aba2a32e680ab9499f5295307c82daafbbed71
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695352"
---
# <a name="approve-applications-in-configuration-manager"></a>Godkänn program i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du [distribuerar ett program](deploy-applications.md) i Configuration Manager kan du kräva godkännande före installationen. Användare begär programmet i Software Center och granskar sedan begäran i Configuration Manager-konsolen. Du kan godkänna eller avvisa begäran.

## <a name="approval-settings"></a><a name="bkmk_approval"></a> Inställningar för godkännande

Program godkännande beteendet beror på om du aktiverar den rekommenderade [upplevelsen för godkännande av valfria appar](#bkmk_opt). En av följande godkännande inställningar visas på sidan **distributions inställningar** i program distributionen:  

### <a name="an-administrator-must-approve-a-request-for-this-application-on-the-device"></a><a name="bkmk_opt"></a> En administratör måste godkänna en begäran om det här programmet på enheten

> [!Note]  
> Configuration Manager aktiverar inte den här funktionen som standard. Innan du använder den aktiverar du den valfria funktionen **Godkänn program begär Anden för användare per enhet**. Mer information finns i avsnittet [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).
>
> Om du inte aktiverar den här funktionen visas den [tidigare versionen](#bkmk_prior).  

Administratören godkänner alla användar förfrågningar för programmet innan användaren kan installera den på den begärda enheten. Om administratören godkänner begäran kan användaren bara installera programmet på den enheten. Användaren måste skicka en annan begäran om att installera programmet på en annan enhet. Det här alternativet är nedtonat när distributions syftet **krävs**, eller när du distribuerar programmet till en enhets samling. <!--1357015-->  

> [!Note]  
> Om du vill dra nytta av nya Configuration Manager funktioner måste du först uppdatera klienter till den senaste versionen. När nya funktioner visas i Configuration Manager-konsolen när du uppdaterar platsen och konsolen, fungerar inte det fullständiga scenariot förrän klient versionen också är den senaste.<!--SCCMDocs issue 646-->  

Visa **program begär Anden** under **program hantering** i arbets ytan **program varu bibliotek** i Configuration Manager-konsolen. (I version 1902 och tidigare kallas den här noden **godkännande begär Anden**.) Det finns nu en **enhets** kolumn i listan för varje begäran. När du vidtar åtgärder på begäran innehåller dialog rutan programbegäran även enhets namnet som användaren skickade begäran från.

Om en begäran inte godkänns inom 30 dagar tas den bort. Om klienten installeras om kan alla väntande begär Anden om godkännande annulleras.  

När du kräver godkännande av en distribution till en enhets samling visas inte appen i Software Center. Om du behöver godkänna en distribution till en användar samling visas appen i Software Center. Du kan fortfarande dölja den från användare med klient inställningen **Dölj ej godkända program i Software Center**. Mer information finns i [klient inställningar för Software Center](../../core/clients/deploy/about-client-settings.md#software-center).

När du har godkänt ett program för installation kan du **neka** begäran i Configuration Manager-konsolen. Om användarna inte redan har installerat programmet hindrar den här åtgärden dem från att installera nya kopior av programmet från Software Center. Om ett program tidigare har godkänts och installerats och du **nekar** begäran för programmet, avinstallerar klienten programmet från användarens enhet.<!--1357891-->

Från och med version 1906, om du godkänner en app-begäran i-konsolen och sedan nekar den, kan du nu godkänna den igen. Appen installeras om på klienten när du har godkänt den.  <!-- 4224910 -->

Automatisera godkännande processen med PowerShell-cmdleten [Godkänn-CMApprovalRequest](/powershell/module/configurationmanager/approve-cmapprovalrequest?view=sccm-ps) . Från och med version 1902 inkluderar denna cmdlet parametern **InstallActionBehavior** . Använd den här parametern för att ange om programmet ska installeras direkt eller under icke-kontors tid.<!-- SCCMDocs-pr issue #3418 -->

Från och med 1906 kan du se vilka distributioner som kräver godkännande. Välj en app i noden **program** . I informations fönstret växlar du till fliken **distributioner** . En ny kolumn som visas som standard **kräver godkännande**.

#### <a name="retry-the-install-of-pre-approved-applications"></a><a name="bkmk_retry"></a> Gör om installationen av för hands godkända program

<!--4336307-->
Från och med version 1906 kan du göra ett nytt försök med installationen av en app som du tidigare godkänt för en användare eller enhet. Alternativet för godkännande är endast tillgängligt för distributioner. Om användaren avinstallerar appen, eller om den inledande installationen Miss lyckas, kommer Configuration Manager inte att utvärdera om dess tillstånd och installera om den. Med den här funktionen kan en support tekniker snabbt försöka installera appen igen för en användare som anropar hjälp.

1. Öppna Configuration Manager-konsolen som en användare som har behörigheten **Godkänn** för programobjektet. Till exempel har de inbyggda rollerna **program administratör** eller **program författare** den här behörigheten.

1. Distribuera en app som kräver godkännande och Godkänn den.

    > [!Tip]  
    > Du kan också [Installera ett program för en enhet](install-app-for-device.md). Den skapar en godkänd begäran om appen på enheten.  

Om programmet inte installeras utan problem, eller om användaren avinstallerar appen, använder du följande process för att försöka igen:

1. I Configuration Manager-konsolen går du till arbets ytan **program varu bibliotek** , expanderar **program hantering**och väljer noden **program begär Anden** . (I version 1902 och tidigare kallas den här noden **godkännande begär Anden**.)

1. Välj den tidigare godkända appen. I gruppen godkännande av begäran i menyfliksområdet väljer du **försök installera igen**.

#### <a name="other-app-approval-resources"></a>Övriga program godkännande resurser

- [Förbättringar av program godkännande i ConfigMgr 1810](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Application-approval-improvements-in-ConfigMgr-1810/ba-p/303534)
- [Uppdateringar av program godkännande processen i Configuration Manager](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Updates-to-the-application-approval-process-in-Configuration/ba-p/275048)

### <a name="require-administrator-approval-if-users-request-this-application"></a><a name="bkmk_prior"></a> Kräv administratörs godkännande om användare begär programmet

> [!Note]  
> Den här funktionen gäller om du inte aktiverar den rekommenderade [upplevelsen för godkännande av valfria appar](#bkmk_opt).

Administratören godkänner alla användar förfrågningar för programmet innan användaren kan installera det. Det här alternativet är nedtonat när distributions syftet **krävs**, eller när du distribuerar programmet till en enhets samling.  

Begär Anden om program godkännande visas i noden **program begär Anden** , under **program hantering** i arbets ytan **program varu bibliotek** . (I version 1902 och tidigare kallas den här noden **godkännande begär Anden**.) Om en begäran inte godkänns inom 30 dagar tas den bort. Om klienten installeras om kan alla väntande begär Anden om godkännande annulleras.  

När du har godkänt ett program för installation kan du **neka** begäran i Configuration Manager-konsolen. Den här åtgärden gör inte att klienten avinstallerar programmet från några enheter. Användaren hindrar användare från att installera nya kopior av programmet från Software Center.  

## <a name="email-notifications"></a><a name="bkmk_email-approve"></a> E-postmeddelanden

<!--1321550-->

Du kan konfigurera e-postaviseringar för begäran om program godkännande. När en användare begär ett program får du ett e-postmeddelande. Klicka på länkar i e-postmeddelandet för att godkänna eller neka begäran, utan att behöva Configuration Manager-konsolen.

Du kan definiera e-postadresserna till de användare som kan godkänna eller neka begäran när du skapar en ny distribution för programmet. Om du behöver ändra listan över e-postadresser efteråt går du till arbets ytan **övervakning** , expanderar **aviseringar**och väljer noden **prenumerationer** . Välj **Egenskaper** från ett av **godkännande programmet via e-** postprenumerationer som är relaterade till program distributionen.

Om det finns fler än en avisering kan du bestämma vilken avisering som ska användas med vilken distribution. Öppna aviserings egenskaperna och Visa listan över **valda aviseringar** på fliken Allmänt. Distributionen är aktive rad som avisering för den här prenumerationen.

Användare kan lägga till en kommentar till begäran från Software Center. Den här kommentaren visar på program förfrågan i Configuration Manager-konsolen. Från och med version 1902 visas kommentaren även i e-postmeddelandet. Med den här kommentaren i e-postmeddelandet kan god kännare fatta ett bättre beslut att godkänna eller avvisa begäran.<!--3594063-->

### <a name="prerequisites"></a>Förutsättningar

#### <a name="to-send-email-notifications-and-take-action-on-internal-network"></a>Skicka e-postmeddelanden och vidta åtgärder i interna nätverk

Med de här kraven får mottagarna ett e-postmeddelande med en avisering om begäran. Om de finns i det interna nätverket kan de också godkänna eller neka begäran från e-postmeddelandet.

- Aktivera den [valfria funktionen](../../core/servers/manage/install-in-console-updates.md#bkmk_options) **Godkänn program begär Anden för användare per enhet**.  

- Konfigurera [e-postavisering för aviseringar](../../core/servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts).  

    > [!NOTE]
    > Den administrativa användare som distribuerar programmet måste ha behörighet att skapa en avisering och en prenumeration. Om den här användaren inte har dessa behörigheter visas ett fel i slutet av **guiden distribuera program vara**: "du har inte säkerhets rättigheter för att utföra den här åtgärden."<!-- 2810283 -->

- Aktivera SMS-providern på den primära platsen för att använda ett certifikat.<!--SCCMDocs-pr issue 3135--> Välj ett av följande alternativ:  

  - Rekommenderas Aktivera [utökad http](../../core/plan-design/hierarchy/enhanced-http.md) för den primära platsen.

    > [!Note]  
    > När den primära platsen skapar ett certifikat för SMS-providern är den inte betrodd av webbläsaren på klienten. Baserat på dina säkerhets inställningar kan en säkerhets varning visas när du svarar på en programbegäran.  

  - Bind ett PKI-baserat certifikat manuellt till port 443 i IIS på den server som är värd för SMS-providerns roll på den primära platsen.

> [!NOTE]
> Om du har flera underordnade primära platser i en hierarki konfigurerar du dessa krav för varje primär plats där du vill aktivera den här funktionen. Länkarna i e-postaviseringen är för administrations tjänsten på den primära platsen.<!-- 7108472 -->

#### <a name="to-take-action-from-internet"></a>Vidta åtgärder från Internet

Med dessa ytterligare valfria krav kan mottagarna godkänna eller neka begäran från var de än är Internet-åtkomst.

- Aktivera administrations tjänsten för SMS-providern via Cloud Management Gateway. Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **servrar och plats system roller** . Välj servern med rollen SMS-provider. I informations fönstret väljer du rollen **SMS-provider** och sedan **Egenskaper** i menyfliksområdet på fliken plats roll. Välj alternativet för att **tillåta Configuration Manager Cloud Management Gateway-trafik för administrations tjänsten**.  

- SMS-providern kräver **.NET 4.5.2** eller senare.  

- Konfigurera en [Gateway för moln hantering](../../core/clients/manage/cmg/plan-cloud-management-gateway.md).

- Publicera webbplatsen till [Azure-tjänster](../../core/servers/deploy/configure/azure-services-wizard.md) för **moln hantering**.

- Aktivera [identifiering av Azure AD-användare](../../core/servers/deploy/configure/configure-discovery-methods.md#azureaadisc).

- Konfigurera inställningar i Azure AD manuellt:  

    1. Gå till [Azure Portal](https://portal.azure.com) som en användare med *globala administratörs* behörigheter. Gå till **Azure Active Directory**och välj **Appregistreringar**.  

    1. Välj det program som du skapade för Configuration Manager integrering av **moln hantering** .  

    1. I menyn **Hantera** väljer du **autentisering**.  

        1. I avsnittet **omdirigerings-URI** klistrar du in följande sökväg: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

        1. Ersätt `<CMG FQDN>` med det fullständigt kvalificerade domän namnet (FQDN) för din Cloud Management Gateway-tjänst (CMG). Till exempel GraniteFalls.Contoso.com.  

        1. Välj sedan **Spara**.  

    1. I menyn **Hantera** väljer du **manifest**.  

        1. I fönstret Redigera manifest hittar du egenskapen **oauth2AllowImplicitFlow** .  

        1. Ändra värdet till **Sant**. Till exempel bör hela raden se ut som på följande rad: `"oauth2AllowImplicitFlow": true,`  

        1. Välj **Spara**.  

### <a name="configure-email-approval"></a>Konfigurera e-postgodkännande

1. I Configuration Manager-konsolen [distribuerar du ett program](deploy-applications.md) som är tillgängligt för en användar samling. På sidan **distributions inställningar** aktiverar du det för godkännande. Ange sedan en eller flera e-postadresser som ska få aviseringar. Avgränsa e-postadresser med semikolon ( `;` ).  

     > [!Note]  
     > Alla i din Azure AD-organisation som tar emot e-postmeddelandet kan godkänna begäran. Vidarebefordra inte e-postmeddelandet till andra såvida du inte vill att de ska vidta åtgärder.  

2. Som användare kan du begära programmet i Software Center.  

3. Du får ett e-postmeddelande inom fem minuter. E-postmeddelandets innehåll liknar följande exempel:  

![Exempel på e-postavisering om program godkännande](media/1321550-email.png)

> [!Note]  
> Länken för att godkänna eller neka är för eng ång slö tillfället. Du kan till exempel konfigurera ett grupp-alias för att ta emot meddelanden. MB godkänner begäran. Nu kan Bruce inte neka begäran.  

Granska filen **NotiCtrl. log** på plats servern för fel sökning.

## <a name="maintenance"></a>Underhåll

Configuration Manager lagrar information om begäran om program godkännande i plats databasen. För begär Anden som har avbrutits eller nekats tar platsen bort begär ande historiken efter 30 dagar. Du kan konfigurera det här borttagnings beteendet med aktiviteten **ta bort föråldrade program begär data** [plats underhåll](../../core/servers/manage/maintenance-tasks.md). Platsen tar aldrig bort alla godkända eller väntande program begär Anden.