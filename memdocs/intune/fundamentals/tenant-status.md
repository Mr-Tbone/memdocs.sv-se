---
title: Sidan Klientorganisationsstatus i Microsoft Intune
titleSuffix: Microsoft Intune
description: Använd sidan Klientorganisationsstatus i Intune för att visa viktig klientorganisationsinformation utan att lämna Intune-portalen
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 7954a686-25dc-4fce-b395-324816f46d3b
ms.reviewer: crisk
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cd4c64e08177387561323b1e59bef3b976bf0bf3
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911190"
---
# <a name="use-the-intune-tenant-status-page"></a>Använd sidan Klientorganisationsstatus i Intune

Microsoft Intune-sidan Klientorganisationsstatus är en centraliserad hubb där du kan se aktuell och viktig information om din klientorganisation. Informationen omfattar tillgänglighet för och användning av licenser, anslutningsstatus och viktiga meddelanden om Intune-tjänsten.

> [!TIP]
> En klientorganisation är en instans av Azure Active Directory (Azure AD). Det är en Azure AD-klientorganisation som är värd för din prenumeration på Intune. Mer information finns i [Konfigurera en klientorganisation](/azure/active-directory/develop/quickstart-create-new-tenant) i Azure AD-dokumentationen.

Om du vill visa instrumentpanelen loggar du in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), går till **Administration av klientorganisation** och väljer **Klientorganisationsstatus**.

Sidan är uppdelad i tre flikar:

## <a name="tenant-details"></a>Information om klientorganisation
Information om klientorganisation innehåller översiktlig information om klientorganisationen. Visa information som klientorganisationens namn och plats, MDM-utfärdare och klientorganisationens tjänstversionsnummer. Tjänstversionsnumret är en länk som öppnar artikeln *Nyheter i Intune* på Microsoft Docs. I *Nyheter* kan du läsa om de senaste funktionerna och uppdateringarna för Intune-tjänsten.  

På den här fliken finns också grundläggande information om dina tillgängliga licenser och hur många som har tilldelats till användarna. Licenser för enheter visas inte.

## <a name="connector-status"></a>Status för anslutningsprogrammet
Status för anslutningsprogrammet är en plats för att granska statusen för alla tillgängliga anslutningsprogram för Intune.  

Anslutningsprogram är:
- **Anslutningar du konfigurerar till externa tjänster**. Till exempel tjänsten för *Apples volymköpsprogram* eller *Windows Autopilot*-tjänsten.  Status för den här typen av anslutningsprogram baseras på tiden för den senaste genomförda synkroniseringen.
- **Certifikat eller autentiseringsuppgifter som krävs för att ansluta till en extern ohanterad tjänst**, till exempel *Apple Push Notification Service*-certifikat (APNS). Status för den här typen av anslutningsprogram baseras på förfallotidsstämpeln för certifikatet eller autentiseringsuppgiften.  

När du öppnar fliken *Status för anslutningsprogrammet* visas alla felaktiga anslutningsprogram överst i listan. Därefter visas anslutningsprogram med varningar och sedan listan över felfria anslutningsprogram. Anslutningsprogram som du inte har konfigurerat ännu visas som *Inte aktiverad*.

När det finns fler än ett enda anslutningsprogram av någon typ är statusen en sammanfattning för alla de anslutningsprogrammen. Den lägsta statusen för ett enskilt anslutningsprogram används som hälsotillstånd för gruppen.  

**Status för anslutningsprogrammet:**
- **Ej felfri:**
  - Certifikatet eller autentiseringsuppgiften har upphört att gälla
  - Den senaste synkroniseringen genomfördes för minst tre dagar sedan
- **Varning:**
  - Certifikatet eller autentiseringsuppgiften upphör att gälla inom sju dagar
  - Den senaste synkroniseringen genomfördes för mer än en dag sedan
- **Felfri:**
  - Certifikatet eller autentiseringsuppgiften upphör inte att gälla inom sju dagar
  - Den senaste synkroniseringen genomfördes för mindre än en dag sedan  

När du väljer ett anslutningsprogram i listan visas den portalsida som är relevant för anslutningsprogrammet. På sidan med anslutningsprogram kan du se statusen för tidigare konfigurerade anslutningsprogram, eller välja alternativ för att lägga till eller skapa ett nytt anslutningsprogram av samma typ.

Om du väljer anslutningsprogrammet **Förfallodatum för VPP** öppnas till exempel sidan **Volyminköpsprogramtoken för iOS**, där du kan se mer information om det anslutningsprogrammet. Du kan också skapa en ny konfiguration eller redigera och åtgärda problem med ett befintligt program.

## <a name="service-health-dashboard"></a>Service Health-instrumentpanel  
På instrumentpanelen för Service Health kan du se information om *Tjänstehändelser* som påverkar din klientorganisation och *Intune-nyheter* med information om uppdateringar och planerade ändringar.

### <a name="intune-service-health-and-message-center"></a>Hälsotillstånd för Intune-tjänsten och meddelandecentret
Se information om aktiva incidenter och rekommendationer utan att behöva gå till Service Health-instrumentpanelen för Microsoft 365 eller Meddelandecenter, som båda finns i [Administrationscenter för Microsoft 365 ](https://admin.microsoft.com). Det är bara incidenter som påverkar din klientorganisation som visas.  

När du väljer en incident visas incidentinformationen direkt på sidan Klientorganisationsstatus. Om du vill visa tidigare rekommendationer och incidenter väljer du **Se tidigare incidenter/rekommendationer**. Administrationscentret för Microsoft 365 öppnas och du kan visa rekommendationer och incidenter från de senaste 30 dagarna för din klientorganisation.  

Om du vill visa information för *Hälsotillstånd för Intune-tjänsten* måste ditt konto ha rollen **Global administratör** eller **Tjänstsupportadministratör** i administrationscentret för Azure Active Directory eller Microsoft 365. Om du vill tilldela de här behörigheterna loggar du in på [	Administrationscenter för Microsoft 365](https://admin.microsoft.com) med globala administratörsbehörigheter. Välj **Användare > Aktiva användare** och välj sedan det konto som kräver åtkomst. Välj **Redigera** för Roller, välj *Tjänstsupportadministratör* eller *Global administratör* och **Spara** sedan ändringen för att tilldela behörigheterna.  

Du kan bara konfigurera kommunikationsinställningarna för Hälsotillstånd för Intune-tjänsten via administrationscentret för Microsoft 365.

### <a name="intune-message-center"></a>Meddelandecentret i Intune  
Visa informationskommunikation från Intune-tjänstteamet utan att behöva gå till meddelandecentret för Office. Kommunikationen omfattar meddelanden om ändringar som nyligen har gjorts i Intune-tjänsten eller som är på gång för din klientorganisation.  

Som standard visas de 10 senaste och aktiva meddelandena. Om du vill visa äldre meddelanden väljer du **Se tidigare meddelanden** för att öppna *Meddelandecenter* i Microsoft 365-administrationscentret.  

Om du vill visa information om Nyheter i Intune måste ditt konto ha rollen **Global administratör** eller **Tjänstsupportadministratör** i Azure Active Directory eller rollen **Meddelandecenter-läsare** i administrationscentret för Microsoft 365.  Om du vill tilldela den här behörigheten loggar du in på [	Administrationscenter för Microsoft 365](https://admin.microsoft.com) med administratörsbehörigheter. Välj **Användare > Aktiva användare** och välj sedan det konto som kräver åtkomst. Välj **Redigera** för *Roller*, välj *Administratör för Teams-kommunikation* och **Spara** sedan ändringen för att tilldela behörigheterna.  

Du kan bara konfigurera kommunikationsinställningarna för meddelandecentret i Intune via administrationscentret för Microsoft 365.