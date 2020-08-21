---
title: Vanliga frågor och svar om Desktop Analytics
titleSuffix: Configuration Manager
description: Vanliga frågor och svar om Desktop Analytics.
ms.date: 02/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: b24369f2c2f21208f188cf5c0c2ef3a28db83c04
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700828"
---
# <a name="desktop-analytics-faq"></a>Vanliga frågor och svar om Desktop Analytics

## <a name="prerequisites"></a>Förutsättningar

### <a name="can-i-use-cloud-enabled-analytics-with-intune-managed-devices"></a><a name="bkmk_intune"></a> Kan jag använda molnbaserad analys med Intune-hanterade enheter?

Inte idag, men se meddelandet från Microsoft antändning 2019 on [Insights-driven enhets hantering](https://myignite.techcommunity.microsoft.com/sessions/81690?source=sessions). Den här planerade lösningen är efterföljande till Enhetens hälsotillstånd och Uppgraderingsberedskap.

De flesta kunder som kan dra nytta av arbets flödet för Skriv bords analys använder Configuration Manager för att distribuera Windows. Vi vet att Intune-kunder älskar ytterligare insikter från analys data och vi arbetar på sätt att dela insikter med dem också.

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>Det har varit över 72 timmar och portalen bearbetar fortfarande data, vad härnäst?

När du först konfigurerar Desktop Analytics kan rapporterna i Configuration Manager och skriv bords analys portalen inte Visa fullständiga data direkt. Det kan ta 2-3 dagar för tjänsten att bearbeta data. Om den har varit över 72 timmar och portalen fortfarande bearbetar data, följer du dessa steg:

- Bekräfta att aktiva enheter är korrekt konfigurerade genom att använda [instrument panelen för anslutnings hälsa](monitor-connection-health.md). Den här instrument panelen uppdateras inte i real tid.
- Kontrol lera att enheterna skickar diagnostikdata till Skriv bords analys tjänsten. Mer information finns i [Aktivera data delning](enable-data-sharing.md).
- Etablera [Azure AD-program](troubleshooting.md#bkmk_AzureADApps) i Azure AD.
- Kontrol lera enheter som du har kopplat till din organisation under de senaste sju dagarna. Gå till fönstret **anslutna tjänster** i [Skriv bords analys portalen](https://aka.ms/desktopanalytics). Välj **registrera enheter**och **Visa senaste data**

  > [!IMPORTANT]
  > Alternativet Skriv bords analys för att **Visa senaste data** är föråldrat. Den här åtgärden kommer att tas bort i en framtida version av Desktop Analytics-tjänsten. Mer information finns i [föråldrade funktioner](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!--7080949-->  

[Kontakta Microsoft-supporten](https://support.microsoft.com/hub/4343728/support-for-business)om enheterna är korrekt konfigurerade och du fortfarande inte ser några data i din arbets yta.

## <a name="connect-configuration-manager"></a>Ansluta Configuration Manager

### <a name="can-i-change-the-target-or-additional-collections"></a>Kan jag ändra mål eller ytterligare samlingar?

Ja, Använd följande process:

- I Configuration Manager-konsolen går du till arbets ytan **Administration** , expanderar **Cloud Services**och väljer noden **Azure-tjänster** . Öppna egenskaperna för posten som är kopplad till din station ära Analytics-tjänst.

- På fliken **stationär Analytics-anslutning** ändrar du **mål samlingen** eller hanterar de ytterligare samlingarna.

<!-- 7130169 -->
> [!Note]
> Ta inte med fler än 20 samlingar i listan över ytterligare samlingar. Var försiktig med det totala antalet enheter i varje samling. Inkludera alltid din [globala pilot samling med och exkludera samlingar](deploy-pilot.md#bkmk_GlobalPilot).  

> [!IMPORTANT]  
> Configuration Manager använder en inställnings princip för att konfigurera enheter i mål samlingen. Den här principen inkluderar inställningar för diagnostikdata för att göra det möjligt för enheter att skicka data till Microsoft. Om du ändrar mål samlingen återställs inte inställnings principen på enheterna längre i mål samlingen. Om du inte vill att enheterna ska kunna skicka diagnostikdata konfigurerar du om [enheterna](account-close.md#reconfigure-clients).

## <a name="windows-upgrade"></a>Windows-uppgradering

### <a name="can-i-upgrade-windows-and-change-architecture"></a>Kan jag uppgradera Windows och ändra arkitektur?

Desktop Analytics har utformats för bästa möjliga uppgraderingar på plats. Uppgraderingar på plats stöder inte migreringar från 32 till 64-bitars arkitektur. Om du behöver migrera datorer i det här scenariot använder du uppdaterings scenariot. Desktop Analytics Insights är fortfarande värdefulla i det här scenariot, men du kan bortse från den detaljerade vägledningen.

Mer information finns i [Uppdatera en befintlig dator med en ny version av Windows](../osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md).

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>Kan jag ändra från BIOS till UEFI vid uppgradering av Windows?

Ja. Mer information finns i [konvertera från BIOS till UEFI under en uppgradering på plats](../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>Kan jag använda Desktop Analytics med Windows 10-LTSC?

Desktop Analytics stöder inte LTSC-enheter (Long-term Servicing Channel) för Windows 10. Mer information finns i [Översikt över Windows som en tjänst](/windows/deployment/update/waas-overview#long-term-servicing-channel).

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>Kan jag minska hur lång tid det tar att uppdatera data i min Skriv bords analys Portal?

Det finns två typer av data i Skriv bords analys portalen: administratörs data och diagnostikdata. Om du vill uppdatera administratörs data på begäran öppnar du utfällda data och väljer **tillämpa ändringar**. Den här åtgärden utlöser omedelbart en eng ång slö uppdatering av alla väntande administratörs ändringar i dina arbets ytor. Ändringarna sprids och är allmänt tillgängliga inom 15-60 minuter. Tids inställningen beror på arbets ytans storlek och omfattningen av väntande ändringar. Du kan begära en data uppdatering på begäran upp till sex gånger under en 24-timmarsperiod.

Alla data uppdateras automatiskt en gång per dag, även om du inte begär en data uppdatering på begäran. Det finns inget sätt att utlösa en uppdatering på begäran av diagnostikdata. Mer information om de olika typerna av data i Desktop Analytics finns i [data svars tid](troubleshooting.md#data-latency).

## <a name="privacy"></a>Sekretess

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>Kan Desktop Analytics användas utan en direkt klient anslutning till Microsoft Datahantering-tjänsten?

Nej, hela tjänsten drivs av Windows-diagnostikdata som kräver att enheterna har denna direkta anslutning.

### <a name="can-i-choose-the-data-center-location"></a>Kan jag välja Data Center plats?

För Azure Log Analytics: Ja, när du konfigurerar Desktop Analytics och skapar arbets ytan Log Analytics.

För tjänsten Microsoft Datahantering service och Analytics Azure Storage: Nej, finns dessa två tjänster i USA.

### <a name="where-is-my-organizations-data-stored"></a>Var lagras min organisations data?

Windows-diagnostikdata från dina datorer krypteras, skickas till och bearbetas i Microsoft-hanterade säkra data Center som finns i USA. Microsoft tillhandahåller analyser av Skriv bords analys-relaterade data till dig via Desktop Analytics-lösningen i Azure Portal. Desktop Analytics stöds i de flesta regioner där [Log Analytics är tillgängligt](https://azure.microsoft.com/global-infrastructure/services/?products=monitor&regions=all). Om du väljer en internationell Azure-region skickas dina diagnostikdata fortfarande till och bearbetas i Microsofts säkra data Center i USA.

## <a name="existing-windows-analytics-customers"></a>Befintliga Windows Analytics-kunder

> [!Important]  
> Windows Analytics-tjänsten dras tillbaka den 31 januari 2020.
>
> Mer information finns i [KB 4521815: pensionering i Windows Analytics den 31 januari 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

### <a name="can-i-use-update-compliance-together-with-desktop-analytics"></a>Kan jag använda Uppdateringsefterlevnad tillsammans med Desktop Analytics?

Ja. Om du använder [uppdateringsefterlevnad](/windows/deployment/update/update-compliance-get-started) i Azure Portal idag kan du fortsätta att göra det nu och utöver 2020 januari.

Mer information finns i [KB 4521815: pensionering i Windows Analytics den 31 januari 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

### <a name="are-there-any-windows-analytics-features-that-arent-available-in-desktop-analytics"></a>Finns det några Windows Analytics-funktioner som inte är tillgängliga i Desktop Analytics?

<!-- 3616924 -->
Ja, följande Windows Analytics-funktioner har antingen tagits bort eller är ännu inte tillgängliga i Desktop Analytics:

#### <a name="general"></a>Allmänt

- Stöd för scenarier som inte kräver Configuration Manager. Till exempel [Intune-support](#bkmk_intune).
- Licens krav för en giltig Windows-licens jämfört med E3, E5
- Stöd för flera arbets ytor per Azure AD-klient
- Möjlighet att köra anpassade frågor och exportera rå data för lösningen
- Data modell dokumentation för anpassade rapporter

#### <a name="upgrade-readiness"></a>Uppgraderingsberedskap

- Webbplats identifierings data för Internet Explorer
- Insikter för Microsoft 365 App-tillägg ( [finns nu i Configuration Manager](#bkmk_office))
- Feedback Hub Insights

#### <a name="update-compliance"></a>Uppdateringsefterlevnad

- Stöd för Windows Update för företag
- Insikter om leverans optimering
- Stöd för långsiktig service kanal för Windows 10 (LTSC)
- Windows Insider-rapporter
- Windows Defender-status

> [!Note]
> Alla befintliga Uppdateringsefterlevnad funktioner, inklusive sådana som inte är tillgängliga i Desktop Analytics, är fortfarande tillgängliga i [uppdateringsefterlevnad](/windows/deployment/update/update-compliance-get-started) -lösningen i Azure Portal.

#### <a name="device-health"></a>Enhetens hälsotillstånd

- Driv rutins hälsa
- App Health (utanför en distributions plan)
- Vanliga krascher för enheter eller driv rutiner som induceras av driv rutiner
- Windows inloggnings hälsa
- Windows informationsskydd
- Stöd för Windows Server

## <a name="other"></a>Annat

### <a name="can-i-use-desktop-analytics-for-my-microsoft-365-apps-upgrades"></a><a name="bkmk_office"></a> Kan jag använda Desktop Analytics för att uppgradera mina Microsoft 365-appar?

Nej, Desktop Analytics fokuserar på Windows. Microsoft utvecklade Desktop Analytics i nära samarbete med många kunder. Kundfeedback är om hur Desktop Analytics förbättrar sin förmåga att hantera Windows-distributioner på ett säkert sätt. De berättar också för oss att de vill att [Microsoft 365 Apps](../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness) är mer nära integrerad med hanterings verktygen för Microsoft 365-appar i Configuration Manager och Intune. Microsoft fortsätter att investera i dessa områden, samtidigt som vi fokuserar på Windows-scenarier i Desktop Analytics.

### <a name="how-can-i-provide-feedback-about-desktop-analytics"></a>Hur kan jag ge feedback om Desktop Analytics?

Om du vill dela din feedback om Desktop Analytics väljer du ikonen **Skicka ett leende** överst i portalen. Ta med en skärm bild med ditt bidrag för att hjälpa Microsoft att bättre förstå din feedback. Du kan också skicka in produkt förslag och rösta på andra idéer på [UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805).

> [!Note]
> Dela aldrig privat information via skicka ett leende eller UserVoice. Sådan privat information innehåller ditt klient-ID eller ditt kommersiella ID. Microsoft tillhandahåller inte support via skicka ett leende-eller UserVoice-kanaler. Om du vill få hjälp med din arbets yta för Desktop Analytics väljer du länken **Hjälp och support** på navigerings menyn för att öppna ett support ärende.