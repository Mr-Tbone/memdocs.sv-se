---
title: Scenarier för villkorlig åtkomst
titleSuffix: Microsoft Intune
description: Läs om hur villkorlig åtkomst med Intune ofta används för enhetsbaserad och appbaserad villkorlig åtkomst.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a0b8e55e-c3d8-4599-be25-dc10c1027b62
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9c1d4dacf29aa0c87a8356306d10bf05acbf3afb
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462175"
---
# <a name="what-are-common-ways-to-use-conditional-access-with-intune"></a>Hur används villkorlig åtkomst vanligtvis med Intune?

Det finns två typer av villkorlig åtkomst som används med Intune: enhetsbaserad villkorlig åtkomst och appbaserad villkorlig åtkomst. Du måste konfigurera de relaterade efterlevnadsprinciperna för att få en villkorlig åtkomst som följer standard i din organisation. Villkorlig åtkomst används vanligtvis för att tillåta eller blockera åtkomst till Exchange, styra åtkomsten till nätverket eller integrering med en Mobile Thread Defense-lösning.
 
Informationen i den här artikeln visar hur du ska använda Intunes funktioner för mobil *enhets*efterlevnad och hantering av mobil*program* (MAM). 

> [!NOTE]
> Villkorlig åtkomst är en funktion i Azure Active Directory som ingår i Azure Active Directory Premium-licenser. Intune utökar den här funktionen genom att lägga till efterlevnad för mobila enheter och hantering av mobilappar i lösningen. Den nod för villkorsstyrd åtkomst som nås från *Intune* är samma nod som den som nås från *Azure AD*.  

## <a name="device-based-conditional-access"></a>Enhetsbaserad villkorlig åtkomst

Intune och Azure Active Directory ser tillsammans till att endast hanterade och kompatibla enheter får åtkomst till e-post, Office 365-tjänster, SaaS-appar (Software as a Service) och [lokala appar](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started). Dessutom kan du konfigurera en princip i Azure Active Directory så att endast datorer som är anslutna till en domän, eller mobila enheter som är registrerade i Intune, kan få åtkomst till Office 365-tjänster.

Intune innehåller funktioner för enhetskompatibilitetprinciper som utvärderar enheternas efterlevnadsstatus. Kompatibilitetsstatusen rapporteras till Azure Active Directory som använder den för att verkställa den princip för villkorlig efterlevnad som skapas i Azure Active Directory när användaren försöker få åtkomst till företagets resurser.

Enhetsbaserad villkorlig åtkomst för Exchange Online och andra Office 365-produkter konfigureras via [Azure-portalen](../fundamentals/what-is-intune.md).

- Läs mer om [Kräv hanterade enheter med villkorlig åtkomst i Azure Active Directory](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).

- Läs mer om [Intunes enhetsefterlevnad](device-compliance-get-started.md).

- Läs mer om [Webbläsare med villkorlig åtkomst som stöds i Azure Active Directory](https://docs.microsoft.com/azure/active-directory/conditional-access/technical-reference#supported-browsers).

> [!NOTE]
> När du på Android-enheter aktiverar enhetsbaserad åtkomst för Sharepoint Online eller webbläsarbaserad åtkomst till Exchange Online måste användare aktivera alternativet **Aktivera webbläsaråtkomst** på den registrerade enheten enligt följande:
> 1. Starta **företagsportalappen**.
> 2. Gå till sidan **Inställningar** från de tre punkterna (…) eller knappen för maskinvara.
> 3. Tryck på knappen **Aktivera webbläsaråtkomst**. 
> 4. I webbläsaren Chrome loggar du ut från Office 365 och startar om Chrome.

### <a name="conditional-access-based-on-network-access-control"></a>Villkorlig åtkomst baserad på åtkomstkontroll för nätverk

Intune har integrerats med partner som Cisco ISE, Aruba Clear Pass och Citrix NetScaler för att kunna ge åtkomstkontroll baserad på Intune-registreringen och enhetsefterlevnadstillståndet.

Användare kan tillåtas eller nekas åtkomst till företagets Wi-Fi- eller VPN-resurser baserat på huruvida enheten hanteras eller är kompatibel med Intunes enhetsefterlevnadsprinciper eller inte.

- Läs mer om [NAC-integrering med Intune](network-access-control-integrate.md).

### <a name="conditional-access-based-on-device-risk"></a>Villkorlig åtkomst baserad på enhetsrisk

Intune samarbetar med Mobile Threat Defense-leverantörer om att tillhandahålla en säkerhetslösning som identifierar skadlig kod, trojaner och andra hot på mobila enheter.

#### <a name="how-the-intune-and-mobile-threat-defense-integration-works"></a>Så här fungerar Intune med Mobile Threat Defense-integrering

När mobila enheter har Mobile Threat Defense-agenten installerad, kan denna skicka meddelanden om efterlevnadstillstånd till Intune om ett hot har identifierats i själva den mobila enheten.

Intune och integrerat mobilhotsskydd spelar en viktig roll vid beslut om villkorlig åtkomst baserat på enhetsrisk.

- Läs mer om [Intunes mobilhotsskydd](mobile-threat-defense.md).

### <a name="conditional-access-for-windows-pcs"></a>Villkorlig åtkomst för Windows-datorer

Villkorlig åtkomst för datorer har ungefär samma funktioner som för mobila enheter. Låt oss tala om hur du kan använda villkorlig åtkomst när du hanterar datorer med Intune.

#### <a name="corporate-owned"></a>Företagsägd

- **Hybrid Azure AD-ansluten:** Det här alternativet används ofta av organisationer som är relativt nöjda med sitt sätt att hantera datorer via AD-grupprinciper eller Configuration Manager.

- **Domänansluten Azure AD och Intune-hantering:** Det här scenariot är avsett för organisationer som vill vara delvis molnbaserade (som huvudsakligen använder molntjänster med målet för att minska användningen av en lokal infrastruktur) eller enbart molnbaserade (ingen lokal infrastruktur). Azure AD Join fungerar bra i en hybridmiljö, vilket ger åtkomst till såväl molnet som lokala appar och resurser. Enheten ansluter till Azure AD och registreras i Intune som kan användas som ett villkor för villkorlig åtkomst till företagsresurser.

#### <a name="bring-your-own-device-byod"></a>BYOD (Bring Your Own Device)

- **Arbetsplatsanslutning och Intune-hantering:** Här kan användaren ansluta sina personliga enheter och få åtkomst till företagets resurser och tjänster. Du kan använda arbetsplatsanslutning och registrera enheter i Intune MDM och ta emot principer på enhetsnivå, vilket är ett annat alternativ för att utvärdera kriterier för villkorlig åtkomst.

Läs mer om [enhetshantering i Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/overview).

## <a name="app-based-conditional-access"></a>Appbaserad villkorlig åtkomst

Intune och Azure Active Directory fungerar tillsammans så att endast hanterade appar har åtkomst till företagets e-post eller andra Office 365-tjänster.

- Läs mer om [appbaserad villkorlig åtkomst med Intune](app-based-conditional-access-intune.md).

### <a name="intune-conditional-access-for-exchange-on-premises"></a>Villkorlig åtkomst för Intune till Exchange lokalt

Villkorlig åtkomst kan användas för att tillåta eller blockera åtkomst till **Exchange On-premises** baserat på enhetsefterlevnadsprinciperna och registreringsstatusen. När villkorlig åtkomst använd i kombination med en enhetsefterlevnadsprincip ges endast kompatibla enheter åtkomst till Exchange On-premises.

Du kan konfigurera avancerade inställningar för villkorlig åtkomst om du vill ha mer detaljerad kontroll, som t.ex.:

- Tillåta eller blockera vissa plattformar.

- Blockera enheter omedelbart som inte hanteras av Intune.

Efterlevnaden för alla enheter som används för att få åtkomst till Exchange lokalt kontrolleras när principerna för enhetsefterlevnad och villkorlig åtkomst tillämpas.

När en enhet inte uppfyller de angivna villkoren leds slutanvändaren genom en process för att registrera enheten och åtgärda de problem som gör att enheten inte är kompatibel.

> [!NOTE]
> Från och med juli 2020 är stödet för Exchange-anslutningsprogrammet inaktuellt och ersätts av [modern hybridautentisering](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) (HMA) i Exchange. Om du använder HMA behöver inte Intune installera och använda Exchange-anslutningsprogrammet. Med den här ändringen tas gränssnittet för att konfigurera och hantera Exchange-anslutningsprogram för Intune bort från administrationscentret för Microsoft Endpoint Manager, om du inte redan använder ett Exchange-anslutningsprogram i din prenumeration.
>
> Om du har konfigurerat ett Exchange-anslutningsprogram i din miljö kan Intune-klientorganisationen fortsätta att använda det, och du fortsätter att ha tillgång till gränssnittet som har stöd för konfigurationen. Mer information finns i [Installera Exchange-anslutningsprogram lokalt](../protect/exchange-connector-install.md). Du kan fortsätta att använda anslutningsprogrammet eller konfigurera modern hybridanslutning (HMA) och sedan avinstallera anslutningsprogrammet.
>
> Modern hybridautentisering ger tillgång till funktioner som tidigare fanns i Exchange Connector för Intune: Mappning av en enhets identitet till Exchange-posten.  Den här mappningen sker nu utanför konfigurationer du skapar i Intune eller kravet på att Intune-anslutningsprogrammet ska vara en brygga mellan Intune och Exchange. Med HMA behöver du inte längre använda den Intune-specifika konfigurationen (anslutningsprogrammet).


<!-- Deprecated with change from the connector to Exchange hybrid modern authentication)

#### How conditional access for Exchange on-premises works

Conditional access for Exchange on-premises works differently than Azure Conditional Access based policies. You install the Intune Exchange on-premises connector to directly interact with Exchange server. The Intune Exchange connector pulls in all the Exchange Active Sync (EAS) records that exist at the Exchange server so Intune can take these EAS records and map them to Intune device records. These records are devices enrolled and recognized by Intune. This process allows or blocks e-mail access.

If the EAS record is new and Intune isn't aware of it, Intune issues a cmdlet (pronounced "command-let") that directs the Exchange server to block access to e-mail. Following are more details on how this process works:

![Exchange on-premises with CA flow-chart](./media/conditional-access-intune-common-ways-use/ca-intune-common-ways-1.png)

1. User tries to access corporate email, which is hosted on Exchange on-premises 2010 SP1 or later.

2. If the device is not managed by Intune, access to email will be blocked. Intune sends a block notification to the EAS client.

3. EAS receives the block notification, moves the device to quarantine, and sends the quarantine email with remediation steps that contain links so the users can enroll their devices.

4. The Workplace join process happens, which is the first step to have the device managed by Intune.

5. The device gets enrolled into Intune.

6. Intune maps the EAS record to a device record, and saves the device compliance state.

7. The EAS client ID gets registered by the Azure AD Device Registration process, which creates a relationship between the Intune device record, and the EAS client ID.

8. The Azure AD Device Registration saves the device state information.

9. If the user meets the conditional access policies, Intune issues a cmdlet through the Intune Exchange connector that allows the mailbox to sync.

10. Exchange server sends the notification to EAS client so the user can access e-mail.
-->

#### <a name="whats-the-intune-role"></a>Vad är Intune-rollen?

Intune utvärderar och hanterar enhetens tillstånd.

#### <a name="whats-the-exchange-server-role"></a>Vad är Exchange-serverrollen?

Exchange-servern tillhandahåller det API och den infrastruktur som krävs för att flytta enheter till karantänen.

> [!IMPORTANT]
> Tänk på att en efterlevnadsprofil och en Intune-licens måste tilldelas enhetsanvändaren för att enhetens efterlevnad ska kunna utvärderas. Om ingen efterlevnadsprincip har distribuerats till användaren behandlas enheten som kompatibel och inga åtkomstbegränsningar tillämpas.

## <a name="next-steps"></a>Nästa steg

[Konfigurera villkorlig åtkomst i Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)

[Konfigurera principer för appbaserad villkorlig åtkomst](app-based-conditional-access-intune-create.md)

[Skapa en princip för villkorlig åtkomst för Exchange lokalt](conditional-access-exchange-create.md)
