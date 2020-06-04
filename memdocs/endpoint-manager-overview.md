---
title: Översikt över Microsoft Endpoint Manager – Azure | Microsoft Docs
description: Slutpunktshanteraren innehåller Intune, Configuration Manager, samhantering, skrivbordsanalys, Windows Autopilot och administrationscentret för att hantera alla enheter, inklusive lokalt.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/21/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: ''
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: d9e3d03211907f31008b31d68c4ed5cd11ae1a6e
ms.sourcegitcommit: fb77170957f50aa386ff825fb4183b4fd9e3e488
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/22/2020
ms.locfileid: "83791732"
---
# <a name="microsoft-endpoint-manager-overview"></a>Översikt av Microsoft Endpoint Manager

Microsoft Endpoint Manager hjälper till att leverera den moderna arbetsplats och den moderna hantering du behöver för att skydda dina data, i molnet och lokalt. Slutpunktshanteraren innehåller de tjänster och verktyg som du använder för att hantera och övervaka mobila enheter, stationära datorer, virtuella datorer, inbäddade enheter och servrar.

Slutpunktshanteraren kombinerar tjänster som du kanske känner till och redan använder, inklusive Microsoft Intune, Configuration Manager, Desktop Analytics, samhantering och Windows Autopilot. Dessa tjänster ingår i Microsoft 365-stacken för att skydda åtkomst, skydda data och svara på och hantera risker.

Börja med att titta på följande två minuter långa video från Brad Anderson, Microsofts vice ordförande för Microsoft 365:

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="what-you-get"></a>Det här får du

Slutpunktshanteraren innehåller följande tjänster:

- **Microsoft Intune**: Intune är en helt molnbaserad leverantör för hantering av mobilenheter (MDM) och hantering av mobilprogram (MAM) för dina appar och enheter. Du kan styra funktioner och inställningar på Android, Android Enterprise, iOS/iPad, macOS och Windows 10-enheter. Den kan integreras med andra tjänster, inklusive Azure Active Directory (AD), Mobile Threat-försvarare, ADMX-mallar, Win32-och anpassade LOB-appar med mera.

  Om du har en lokal infrastruktur, till exempel Exchange eller en Active Directory, är anslutningsprogram för Intune också tillgängliga:

  - **Intune Connector för Active Directory** lägger till poster i din lokala Active Directory-domän för datorer som registrerar sig med Windows Autopilot. Mer information finns i [Distribuera Azure AD-anslutna hybridenheter](/mem/intune/enrollment/windows-autopilot-hybrid).
  - **Intune Exchange Connector** tillåter (eller blockerar) enhetsåtkomst till Exchange-servrarna om enheterna är registrerade i Intune och uppfyller dina principer. Mer information finns i [Konfigurera lokala Intune Exchange Connector](/mem/intune/protect/exchange-connector-install).
  - **Intune Certificate Connector** bearbetar certifikatförfrågningar från enheter som använder certifikat för autentisering och S/MIME-e-postkryptering. Mer information finns i [Använd certifikat för autentisering](/mem/intune/protect/certificates-configure).

  Som en del av slutpunktshanteraren kan du använda Intune för att skapa och kontrollera efterlevnad och distribuera appar, funktioner och inställningar till dina enheter med hjälp av molnet.

  Mer information finns i [Vad är Microsoft Intune](https://docs.microsoft.com/intune/fundamentals/what-is-intune).

- **Configuration Manager**: Configuration Manager är en lokal hanteringslösning för hantering av stationära datorer, servrar och bärbara datorer som finns i ditt nätverk eller är Internet-baserade. Du kan molnaktivera lösningen för att integrera den med Intune, Azure Active Directory (AD), Microsoft Defender ATP och andra molntjänster. Använd Configuration Manager för att distribuera appar, programuppdateringar och operativsystem. Du kan också övervaka efterlevnad, fråga och agera för klienter i realtid och mycket mer.

  Som en del av slutpunktshanteraren kan du fortsätta att använda Configuration Manager som du alltid har gjort. Om du är redo att flytta några uppgifter till molnet kan du överväga [samhantering](https://docs.microsoft.com/configmgr/comanage/).

  Mer information finns i [Vad är Configuration Manager](https://docs.microsoft.com/configmgr/core/understand/introduction).

- **Samhantering**: Samhantering kombinerar din befintliga lokala Configuration Manager-investering med molnet med hjälp av Intune och andra Microsoft 365-molntjänster. Du väljer om Configuration Manager eller Intune är hanteringsutfärdaren för sju olika arbetsbelastningsgrupper.

  Som en del av slutpunktshanteraren använder samhantering molnfunktioner, inklusive villkorlig åtkomst. Du behåller vissa uppgifter lokalt samtidigt som du kör andra uppgifter i molnet med Intune.

  Mer information finns i [Vad är samhantering?](https://docs.microsoft.com/configmgr/comanage/overview).

- **Desktop Analytics**: Desktop Analytics är en molnbaserad tjänst som integrerar med Configuration Manager. Den ger kunskap och information för att kunna fatta välgrundade beslut om uppdateringsberedskapen för Windows-klienter. Tjänsten kombinerar data från din organisation med data som sammanställs från miljontals enheter som är anslutna till Microsoft-molnet. Den innehåller information om säkerhetsuppdateringar, appar och enheter i din organisation och identifierar kompatibilitetsproblem med appar och drivrutiner. Skapa en pilot för enheter som troligen ger bästa möjliga insikter för tillgångar i organisationen.

  Som en del av slutpunktshanteraren använder du molnbaserade insikter om Desktop Analytics för att hålla Windows 10-enheterna aktuella.

  Mer information finns i [Vad är Desktop Analytics?](https://docs.microsoft.com/configmgr/desktop-analytics/overview).

- **Windows Autopilot**: Windows Autopilot konfigurerar och förkonfigurerar nya enheter, så att de är redo att användas. Den är utformad för att förenkla livscykeln för Windows-enheter, både för IT och slutanvändare, från den första distributionen till slutet av livscykeln.

  Som en del av slutpunktshanteraren använder du Autopilot för att förkonfigurera enheter och automatiskt registrera enheter i Intune. Du kan också integrera Autopilot med Configuration Manager och samhantering för mer komplexa enhetskonfigurationer (i förhandsversion).

  Du hittar mer information i [Översikt av Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) och [Registrera Windows-enheter i Intune](/mem/intune/enrollment/enrollment-autopilot).

- **Azure Active Directory (AD)** : Endpoint Manager använder Azure AD till att identifiera enheter, användare, grupper och multifaktorautentisering (MFA). **Azure AD Premium**, som kan medföra ytterligare kostnader, har [fler funktioner](https://azure.microsoft.com/pricing/details/active-directory/) som hjälper dig att skydda appar och data som dynamiska grupper, automatisk registrering och villkorsstyrd åtkomst.

  Mer information finns i [Lägg till användare](/mem/intune/fundamentals/users-add), [Konfigurera automatisk registrering](/mem/intune/enrollment/windows-enroll) och [om villkorsstyrd åtkomst](/mem/intune/protect/conditional-access).

- **Administrationscentret för Endpoint Manager**: [Administrationscentret](https://go.microsoft.com/fwlink/?linkid=2109431) är en webbplats för att skapa principer och hantera dina enheter. Den ansluter till andra viktiga enhetshanteringstjänster, inklusive grupper, säkerhet, villkorlig åtkomst och rapportering. I det här administrationscentret visas även enheter som hanteras av Configuration Manager och Intune (i förhandsversion).

## <a name="choose-whats-right-for-you"></a>Välj vad som passar dig bäst

Det finns några olika sätt att avgöra vad som passar din organisation bäst. Dina nästa steg beror på vad din organisation gör. Överväg vad du försöker uppnå.

Exempel:

- Om du ständigt etablerar nya enheter börjar du med Windows Autopilot.
- Om du lägger till regler och kontrollinställningar för dina användare, appar och enheter börjar du med Intune.
- Om du förnärvarande använder Configuration Manager för att distribuera appar och vill använda villkorlig åtkomst baserat på säkerhetskrav, börjar du med samhantering.
- Om du förnärvarande använder Configuration Manager och är ansvarig för att hålla Windows 10-enheterna uppdaterade börjar du med Desktop Analytics.
- Om du kommer igång med MDM och MAM, eller om du använder ADMX-mallar för att kontrollera Office, Microsoft Edge och Windows-inställningar, börjar du med Intune.

Du kan också tänka på slutpunktshanteraren som tre delar: moln, lokalt och moln + lokalt:

- **Moln**: Alla data lagras i Azure. Och inga fler datacenter. Med den här metoden får du mobilitetsfördelarna med molnet och säkerhetsfördelarna med Azure.

- **Lokalt**: Om du har en lokal infrastruktur som innehåller Configuration Manager eller som inte är redo att använda molnet kan du behålla dina befintliga system.

- **Moln + lokalt**: Många miljöer är blandade och använder en metod för molnanslutning. Det innebär att de använder en kombination av molnet och lokalt. För nya enheter kan du använda fördelarna med Intune för att komma åt och skydda data. Om du använder Configuration Manager ansluter du till molnet för ytterligare funktioner och analyser. Om du vill flytta vissa arbetsbelastningar till molnet är samhantering ett bra alternativ.

## <a name="what-you-need-to-get-started"></a>Vad du behöver för att komma igång

Microsoft Endpoint Manager är en lösningsplattform som kombinerar flera tekniker. Det är inte en ny licens. Tjänsterna licensieras enligt de enskilda licensvillkoren. Mer information finns i avsnittet om [villkor för produktlicensiering](https://www.microsoft.com/licensing/product-licensing/products).

Om du för närvarande använder Configuration Manager får du även Microsoft Intune för att hantera dina Windows-enheter. För andra plattformar, som iOS/iPad och Android, behöver du en separat Intune-licens.

I de flesta fall kan Microsoft 365 vara det bästa alternativet, eftersom du får slutpunktshanteraren och Office 365. Mer information finns i [Microsoft 365](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise).

## <a name="next-steps"></a>Nästa steg

[Använd kraften i Cloud Intelligence för att förenkla och påskynda IT och gå mot en modern arbetsplats](https://www.microsoft.com/microsoft-365/blog/2019/11/04/use-the-power-of-cloud-intelligence-to-simplify-and-accelerate-it-and-the-move-to-a-modern-workplace/)

[Microsoft Endpoint Manager](https://www.microsoft.com/microsoft-365/microsoft-endpoint-manager)

[Självstudie: Genomgång av Intune i Microsoft Endpoint Manager](/intune/fundamentals/tutorial-walkthrough-endpoint-manager)

[Vad är Microsoft 365? Utbildningsmodul](https://docs.microsoft.com/learn/modules/what-is-m365/index)
