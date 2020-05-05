---
title: Så här felsöker du en distribution av Intune-appskyddsprincip
description: Beskriver hur du felsöker problem som kan uppstå när du distribuerar Intune-appskyddsprinciper.
author: simonxjx
manager: dcscontentpm
localization_priority: Normal
search.appverid:
- MET150
audience: ITPro
ms.date: 4/17/2020
ms.service: microsoft-intune
ms.topic: conceptual
ms.author: v-six
ms.custom: CSSTroubleshoot
appliesto:
- Intune
ms.openlocfilehash: 3b4c02e366f4778e65b4fe4c853ed147fcdb1df3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82072760"
---
# <a name="troubleshooting-app-protection-policy-deployment-in-intune"></a>Felsöka en distribution av appskyddsprincip i Intune

## <a name="introduction"></a>Introduktion

Den här artikeln hjälper dig att förstå och felsöka problem när du använder appskyddsprinciper i Microsoft Intune. Följ de avsnitt som gäller för din situation.

## <a name="basic-steps"></a>Grundläggande steg

### <a name="collect-initial-data"></a>Samla in inledande data

Innan du påbörjar felsökningen bör du samla in viss grundläggande information som klargör problemet och minskar tiden för att hitta en lösning.

Samla in följande information:

- Vilken principinställning tillämpas inte? Tillämpas någon princip?
- Vad är användarupplevelsen? Har användare installerat och startat målappen?
- När började problemet? Har appskyddet någonsin fungerat?
- Vilken plattform (Android eller iOS) gäller problemet för?
- Hur många användare påverkas? Påverkas alla eller bara vissa enheter?
- Hur många enheter påverkas? Påverkas alla eller bara vissa enheter?
- Intune-appskyddsprinciper kräver inte någon MDM-tjänst (hantering av mobilenheter), men påverkas användare som använder Intune eller en EMM från tredje part?
- Påverkas alla hanterade appar eller bara vissa appar? Påverkas exempelvis LOB-appar som har [Intune App SDK](../developer/app-sdk-get-started.md) men inte butiksappar?

Nu kan du starta felsökningen baserat på svaren på dessa frågor.

### <a name="verify-prerequisites"></a>Verifiera kraven

Nästa steg i fel sökningen är att kontrollera om alla krav är uppfyllda.

Även om du kan använda Intune-appskyddsprinciper oberoende av en MDM-lösning måste följande krav vara uppfyllda:

- Användaren måste ha en tilldelad Intune-licens.
- Användaren måste tillhöra en säkerhetsgrupp som är målet för en appskyddsprincip. Samma appskyddsprincip måste rikta sig till den specifika app som används.
- För Android-enheter krävs Företagsportal-appen för att appskyddsprinciper ska tas emot.
- Om du använder appar för [Word, Excel eller PowerPoint](https://products.office.com/business/office) måste följande ytterligare krav uppfyllas:
    - Användaren måste ha en licens för [Microsoft 365 Apps for business eller enterprise](https://products.office.com/business/compare-more-office-365-for-business-plans) som är kopplat till användarens Azure Active Directory-konto (Azure AD). Prenumerationen måste inkludera Office-apparna på mobila enheter och kan inkludera ett molnlagringskonto med [OneDrive för företag](https://onedrive.live.com/about/business/). Office 365-licenser kan tilldelas i [administrationscentret för Microsoft 365](https://admin.microsoft.com) med hjälp av [dessa instruktioner](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc).
    - Användaren måste ha en hanterad plats som konfigurerats med hjälp av den detaljerade **Spara som**-funktionen. Det här kommandot finns under inställningen **Spara kopior av organisationsdata** för appskyddsprincip. Om den hanterade platsen till exempel är OneDrive ska [OneDrive](https://onedrive.live.com/about/)-appen vara konfigurerad i användarens Word-, Excel- eller PowerPoint-app.
    - Om den hanterade platsen är OneDrive måste appen vara mål för den appskyddsprincip som distribuerats till användaren.

  > [!NOTE]
  > Office-mobilappar har för närvarande endast stöd för SharePoint Online och inte lokal SharePoint.

- Om du använder Intune-appskyddsprinciper tillsammans med lokala resurser (Microsoft Skype för företag och Microsoft Exchange Server) måste du aktivera [Hybrid Modern Authentication (HMA) för Skype för företag och Exchange](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview).

Intune-appskyddsprinciper kräver att användarens identitet är konsekvent mellan appen och [Intune App SDK](../developer/app-sdk-get-started.md). Det enda sättet att garantera denna konsekvens är via modern autentisering. Det finns scenarier där appar kan fungera i en lokal konfiguration utan modern autentisering. Resultatet är dock inte konsekvent eller garanterat.

Mer information om hur du aktiverar HMA för hybridkonfigurationer och lokala konfigurationer för Skype för företag finns i följande artiklar:

- **Hybrid**<br>
[Hybrid Modern autentisering för SfB och Exchange blir allmänt tillgängliga](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Hybrid-Modern-Auth-for-SfB-and-Exchange-goes-GA/ba-p/134756)

- **Lokalt**<br>
[Modern autentisering för SfB OnPrem med AAD](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Modern-Auth-for-SfB-OnPrem-with-AAD/ba-p/180910)

### <a name="check-app-protection-policy-status"></a>Kontrollera status för appskyddsprincip

Följ dessa steg för att kontrollera status för appskydd:

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Appar** > **Övervakare** > **Appskyddsstatus**, och välj sedan panelen **Tilldelade användare**.
3. Ta fram en lista över användare och grupper genom att välja **Välj användare** på sidan **Apprapportering**.
4. Sök efter och välj en av de berörda användarna i listan, och välj sedan **Välj användare**. Längst upp i fönstret Apprapportering kan du se om användaren är licensierad för appskydd och har en licens för O365. Du kan även se appens status för alla användarens enheter.
5. Anteckna viktig information såsom riktade appar, enhetstyper, principer, status för enhetsincheckning och tid för senaste synkronisering.

> [!NOTE]
> Appskyddsprinciper tillämpas bara när appar används i en arbetskontext. Det kan till exempel vara när användaren kommer åt appar med hjälp av ett arbetskonto.

Mer finns i [Så här verifierar du konfigurationen av din appskyddsprincip i Microsoft Intune](../apps/app-protection-policies-validate.md).

### <a name="verify-that-user-identity-is-consistent-between-app-and-intune-app-sdk"></a>Kontrollera att användaridentiteten är konsekvent mellan appen och Intune App SDK

I de flesta scenarier loggar användarna in på sina konton med hjälp av användarhuvudnamn (UPN). I vissa miljöer (till exempel lokala scenarier) använder användarna dock kanske någon annan form av inloggningsuppgifter. I dessa fall kan det hända att det UPN som används i appen inte matchar UPN-objektet i Azure AD. När det här problemet uppstår tillämpas inte appskyddsprinciper som förväntat.

Microsofts rekommenderade bästa praxis är att matcha UPN mot den primära SMTP-adressen. Den här metoden gör det möjligt för användarna att logga in på hanterade appar, Intune-appskydd och andra Azure AD-resurser genom att ha en konsekvent identitet. Mer information finns i [ifyllning av Azure AD UserPrincipalName](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-userprincipalname).

Om din miljö kräver alternativa inloggningsmetoder kan du läsa mer i [Konfigurera alternativt inloggnings-ID](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id), särskilt [Modern hybridautentisering med alternativt ID](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id#hybrid-modern-authentication-with-alternate-id).

### <a name="verify-that-the-user-is-targeted"></a>Verifiera att användaren är målet

Intune-appskyddsprinciper måste vara riktade till användare. Om du inte tilldelar en appskyddsprincip till en användare eller användargrupp tillämpas inte principen.

Kontrollera att principen tillämpas på målanvändaren genom att följa dessa steg:

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Appar** > **Övervaka** > **Appskyddsstatus** och välj sedan panelen **Användarstatus** (baserat på enhetens OS-plattform).
I fönstret **Apprapportering** som öppnas väljer du **Välj användare** för att söka efter en användare.
3. Välj användaren i listan. Du kan se information om den användaren.

När du tilldelar principen till en användargrupp kontrollerar du att användaren finns i användargruppen. Det gör du genom att följa dessa steg:

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Grupper > Alla grupper** och sök sedan efter och välj den grupp som används för din tilldelning av appskyddsprincip.
3. Under avsnittet **Hantera** väljer du **Medlemmar**.
4. Om den berörda användaren inte visas granskar du [Hantera app- och resursåtkomst med hjälp av Azure Active Directory-grupper](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups) och dina regler för gruppmedlemskap. Se till att den berörda användaren ingår i gruppen.
5. Kontrollera att den berörda användaren inte finns i någon av de undantagna grupperna för principen.

> [!IMPORTANT]
> - Intune-appskyddsprincipen måste tilldelas till användargrupper och inte till enhetsgrupper.
> - Om den berörda enheten använder Programmet för enhetsregistrering (DEP) för Apple ser du till att **Användartillhörighet** är aktiverat. Användartillhörighet krävs för alla appar som kräver användarautentisering under DEP.
> - Om den berörda enheten använder Android Enterprise kommer endast arbetsprofiler att ha stöd för appskyddsprinciper.


### <a name="verify-that-the-managed-app-is-targeted"></a>Verifiera att den hanterade appen är riktad

När du konfigurerar Intune-appskyddsprinciper måste målapparna använda [Intune App SDK](../developer/app-sdk-get-started.md). Annars fungerar kanske inte appskyddsprinciperna korrekt.

Se till att den riktade appen visas i [Microsoft Intune-skyddade appar](../apps/apps-supported-intune-apps.md). För LOB-appar eller anpassade appar kontrollerar du att apparna använder den senaste versionen av [Intune App SDK](../developer/app-sdk-get-started.md). . Tänk på följande:

För iOS är den här metoden viktig eftersom varje version innehåller korrigeringar som påverkar hur dessa principer tillämpas samt hur de fungerar. Mer information finns i [Intune App SDK iOS-versioner](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/releases).
För Android är den här metoden inte lika viktig. Användare måste dock ha den senaste versionen av Företagsportal-appen installerad eftersom Företagsportal-appen fungerar som principhanteringsagent.

> [!NOTE]
> Från och med september 2019 börjar Intune stödja iOS-appar som har Intune App SDK 8.1.1 och senare versioner. Appar som skapats med hjälp av SDK-versioner före 8.1.1 kommer inte längre att stödjas. 

## <a name="more-information"></a>Mer information

### <a name="special-requirements-for-intune-mdm-managed-devices"></a>Särskilda krav för Intune MDM-hanterade enheter

När du skapar en appskyddsprincip kan du rikta den till alla apptyper eller till följande apptyper:

- Appar på ohanterade enheter
- Appar på Intune-hanterade enheter
- Appar i Android-arbetsprofilen

> [!NOTE] 
> Ange apptyper genom att ange **Rikta till alla typer av appar** till **Nej**, och välj sedan i listan **Apptyper**.

För iOS krävs följande ytterligare [appkonfigurationsinställningar](../apps/app-configuration-policies-use-ios.md) för att rikta in appinställningar (APP) till appar på Intune-registrerade enheter:

- **IntuneMAMUPN** måste konfigureras för alla MDM-hanterade program (Intune eller en EMM från tredje part). Mer information finns i Konfigurera inställningen för användar-UPN för Microsoft Intune eller en EMM-lösning från tredje part.
- **IntuneMAMDeviceID** måste konfigureras för alla tredjepartsprogram och LOB MDM-hanterade program.
- **IntuneMAMDeviceID** måste konfigureras som enhetens ID-token. Det kan till exempel vara nyckel=IntuneMAMDeviceID, värde={{deviceID}}. Mer information finns i [Lägg till appkonfigurationsprinciper för hanterade iOS-enheter](../apps/app-configuration-policies-use-ios.md).
- Om bara **IntuneMAMDeviceID**-värdet konfigureras betraktar Intune APP enheten som ohanterad.

### <a name="scenario-policy-changes-are-not-working"></a>Scenario: Principändringar fungerar inte
[Intune App SDK](../developer/app-sdk-get-started.md) söker regelbundet efter principändringar. Den här processen kan dock fördröjas av någon av följande orsaker:

- Appen har inte checkat in med tjänsten.
- Företagsportal-appen har tagits bort från enheten.

Intune-appskyddsprincipen förlitar sig på användaridentitet. Därför krävs en giltig inloggning som använder ett arbets- eller skolkonto till appen och en konsekvent anslutning till tjänsten. Om användaren inte har loggat in på appen, eller om Företagsportal-appen har tagits bort från enheten, tillämpas inte principuppdateringar.

Dessutom kan ändringar och uppdateringar av appskyddsprinciper ta upp till åtta timmar innan de börjar gälla. Om tillämpligt tvingas principuppdateringen vanligtvis att tillämpas tidigare om alla appar stängs och enheten startas om.

Kontrollera appskyddsstatus med hjälp av följande steg:

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Appar** > **Övervakare** > **Appskyddsstatus**, och välj sedan panelen **Tilldelade användare**.
3. På sidan Apprapportering väljer du **Välj användare** för att öppna en lista över användare och grupper.
4. Sök efter och välj en av de berörda användarna i listan, och välj sedan **Välj användare**.
5. Granska de principer som tillämpas för närvarande, inklusive status och tid för senaste synkronisering.
6. Om statusen är **Inte incheckad**, eller om visningen anger att det inte har gjorts en synkronisering nyligen, kontrollerar du om användaren har en konsekvent nätverksanslutning. För Android-användare kontrollerar du att de har den senaste versionen av Företagsportal-appen installerad.

> [!IMPORTANT]
> [Intune App SDK](../developer/app-sdk-get-started.md) söker efter en selektiv rensning var 30:e minut. Ändringar av befintlig princip för användare som redan är inloggade visas dock kanske inte förrän upp till åtta timmar senare. Du kan påskynda den här processen genom att instruera användaren att logga ut från appen och sedan logga in igen eller starta om enheten.

Intune-appskyddsprincipen innehåller stöd för flera identiteter. Intune kan tillämpa appskyddsprinciper på endast det arbets- eller skolkonto som är inloggat i appen. Det finns dock endast stöd för ett arbets- eller skolkonto per enhet.

### <a name="scenario-the-policy-is-applied-but-ios-users-can-still-transfer-work-files-to-unmanaged-apps"></a>Scenario: Principen tillämpas, men iOS-användare kan fortfarande överföra arbetsfiler till ohanterade appar
Med funktionen **Öppna i hantering** ( ![knappen Öppna i](media/troubleshoot-app-protection/troubleshoot-app-protection.jpg) ) för iOS-enheter kan du begränsa överförandet av filer mellan appar som är distribuerade via ![MDM-kanalen](media/troubleshoot-app-protection/troubleshoot-app-protection.jpg). Användaren kan kanske överföra arbetsfiler från hanterade platser såsom OneDrive och Exchange till ohanterade appar eller platser, beroende på konfigurationen. Funktionen **Öppna i hantering** i iOS fungerar utanför andra dataöverföringsmetoder. Därför påverkas den inte av inställningarna för **Spara som** och **Kopiera/klistra in**.

Du kan använda Intune-appskyddsprinciper tillsammans med iOS-funktionen **Öppna i hantering** för att skydda företagets data på följande sätt:

- **Medarbetarägda enheter som inte hanteras av en MDM-lösning**: Du kan konfigurera inställningarna för appskyddsprincipen med **Tillåt endast att appen överför data till principhanterade appar**. Med den här konfigurationen ger beteendet **Öppna i** för en principhanterad app visar endast andra principhanterade appar som alternativ för delning. Om en användare till exempel försöker skicka en skyddad fil som en bilaga från OneDrive i den inbyggda e-postappen går det inte att läsa filen.

- **Enheter som hanteras av MDM-lösningar**: För enheter som registrerats i Intune eller MDM-lösningar från tredje part styrs datadelning mellan appar med hjälp av appskyddsprinciper och andra hanterade iOS-appar som distribuerats via MDM av Intune APP och av iOS-funktionen **Öppna i hantering**.<br/><br/>
För att säkerställa att appar som du distribuerar med hjälp av en MDM-lösning också är associerade med dina Intune-appskyddsprinciper konfigurerar du inställningen för användar-UPN enligt beskrivningen i [Konfigurera inställningen för användar-UPN](../apps/data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm).<br/><br/>Om du vill ange hur dataöverföring till andra appar ska tillåtas aktiverar du inställningen **Skicka organisationsdata till andra appar** och väljer önskad delningsnivå.<br/><br/>Om du vill ange hur en app ska ta emot data från andra appar aktiverar du inställningen **Ta emot data från andra appar** och väljer önskad nivå för datamottagning.

Mer information om hur du tar emot och delar appdata finns i [Inställningar för dataflytt](../apps/app-protection-policy-settings-ios.md#data-protection).

Mer information finns i [Hantera dataöverföring mellan iOS-appar med Microsoft Intune](../apps/data-transfer-between-apps-manage-ios.md).

## <a name="references"></a>Referenser

Om du fortfarande letar efter en lösning på ett relaterat problem, eller om du vill ha mer information om Intune, kan du skicka en fråga till vårt [Microsoft Intune-forum](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc). Många supporttekniker, MVP:er och medlemmar i vårt utvecklingsteam besöker forumen. Du har därför goda möjligheter till att hitta någon som har den information du behöver.

Information om hur du öppnar en supportbegäran för Microsoft Intune-teamet för produktsupport finns i [Så kan du få support för Microsoft Intune](../fundamentals/get-support.md).

Mer information om Intune-appskyddsprinciper finns i följande artiklar:

- [Felsöka hantering av mobilprogram](../apps/troubleshoot-mam.md)
- [Vanliga frågor och svar om MAM och appskydd](../apps/mam-faq.md)
- [Tips för support: Felsöka Intune-appskyddsprincip med hjälp av loggfiler på lokala enheter](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372)

Alla de senaste nyheterna, information och tekniska tips finns på våra officiella bloggar:

- [Microsoft Intune-supportteamets blogg](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Bloggen om Enterprise Mobility and Security](https://cloudblogs.microsoft.com/enterprisemobility)

## <a name="next-steps"></a>Nästa steg

- Ytterligare information om felsökning av Intune information finns i [Använd felsökningsportalen för att hjälpa företagets användare](../fundamentals/help-desk-operators.md). 
- Lär dig om kända problem i Microsoft Intune. Mer information finns i [Kundframgång för Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess).
- Behöver du mer hjälp? Se [Ta reda på hur du kan få support för Microsoft Intune](../fundamentals/get-support.md).
