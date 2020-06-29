---
title: Hitta den primära användaren av en Microsoft Intune-enhet.
titleSuffix: ''
description: Hitta den primära användaren (eller mappning mellan användare och enhet) för en Intune-enhet.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4319435b170203f6dfd3763f1d05d2752fc76f8e
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107521"
---
# <a name="find-the-primary-user-of-an-intune-device"></a>Hitta den primära användaren av en Intune-enhet

Primär användare, även kallat mappning mellan användare och enhet, är en egenskap för varje enhet i Intune. En Intune-enhet kan ha noll eller en primär användare tilldelad. När det inte finns någon primär användare tilldelad, kallas enheten en ”delad enhet”.

## <a name="find-a-devices-primary-user"></a>Hitta en enhets primära användare

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > välj en enhet.
3. På sidan **Översikt** visas den primära användaren.

## <a name="change-a-devices-primary-user"></a>Ändra en enhets primära användare

Den primära användaren av en enhet kan uppdateras för Windows 10-enheter som är Azure AD-anslutna eller Hybrid Azure AD-anslutna.

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Alla enheter** > välj en enhet > **Egenskaper** > **Ändra primär användare**.
3. Välj en ny användare och välj **Välj**.

När den primära användaren har uppdaterats så uppdateras den även på Intune- och Azure AD-enhetsblad.
>[!NOTE]
>1. Det kan ta upp till 10 minuter innan uppdateringar av den primära användaren visas i Endpoint Manager och Azure AD.
>2. Ändring av enhetens primära användare medför inte att medlemskapet i lokala grupper ändras, som tillägg eller borttagning av användare från den lokala gruppen ”Administratörer”.
>3. Om du ändrar den primära användaren ändras inte ”Registrerat av”-användaren. 


## <a name="what-is-the-primary-user"></a>Vad är en primär användare?
Egenskapen Primär användare används för att mappa en licensierad Intune-användare till sina enheter i
- Företagsportalsappen
- webbplatsen för slutanvändare
- IT-processer som felsökningsidorna i Microsoft Azure-portalen. Dessa sidor mappar användarkonton till enheter med hjälp av den primära användaren. 

### <a name="company-portal-app"></a>Företagsportalappen
Företagsportalappen förväntar sig att det användarkonto som har loggat in på företagsportalen är den primära användaren på den aktuella enheten. Om en annan användare har tilldelats som primär användare, visas en varning i företagsportalen:

”Enheten är redan tilldelad till någon annan i organisationen. Kontakta företagets support om att bli den primära användaren. Du kan fortsätta att använda företagsportalen men funktionerna kommer att vara begränsade”.

Om en Intune-enhet inte har någon primär användare tilldelad, identifierar företagsportalappen den som en delad enhet. Delade enheter kan identifieras visuellt tack vare den ”delad”-etikett som visas på enhetspanelen. I det här läget kan företagsportalen fortfarande användas för att begära och installera tillgängliga appar. Självbetjäningsåtgärder (återställ/byt namn/dra tillbaka) är dock inte tillgängliga.  

För att tillgängliga appar ska kunna visas i företagsportalen på delade enheter, måste de tilldelas till en användargrupp. De kommer att installeras i systemets kontext eller användarkontext, beroende på hur appen konfigurerades av IT-administratören. Mer information om appkontext finns i [Installera appar på Windows 10-enheter](../apps/apps-windows-10-app-deploy.md). Företagsportalen version 10.3.4651.0 eller senare krävs för att använda den här funktionen.


## <a name="who-is-assigned-as-the-primary-user"></a>Vem är tilldelad som primär användare?
Intune lägger automatiskt till en primär användare till enheter under eller strax efter registrering. Registreringsmetoden bestämmer när den primära användaren läggs till för en enhet.

| Plattform | Registreringsmetod | Primär användare tilldelad | Primär användare har tilldelats |
| ---- | ---- | ---- | ---- |
| Windows | Lägg till arbete eller skola (användarstyrd) | Användaren som registrerar sig | Under registrering |   
| Windows | Modern appinloggning (användarstyrd) | Användaren som registrerar sig | Under registrering | 
| Windows | Registrera endast i MDM (användarstyrd) | Användaren som registrerar sig | Under registrering | 
| Windows | Microsoft Azure AD-anslutning (utan konfiguration) | Användaren som registrerar sig | Under registrering | 
| Windows | Microsoft Azure AD-anslutning (Autopilot utan konfiguration) | Användaren som registrerar sig | Under registrering | 
| Windows | Registrera endast i MDM | Användaren som registrerar sig | Under registrering | 
| Windows | Hybrid AADJ + automatisk registrering, grupprincip | Första användaren som loggar in på Windows | När den första användaren loggar in på Windows| 
| Windows | Samhantering | Första användaren som loggar in på Windows | När den första användaren loggar in på Windows | 
| Windows | Microsoft Azure AD-anslutning (token för massregistrering) | Inga | Inte tillämpligt | 
| Windows | Microsoft Azure AD-anslutning (Autopilot, självdistributionsläge) | Inga | Inte tillämpligt | 
| Plattformsoberoende | Användarstyrd registrering med företagsportalappen | Användaren som registrerar sig | Under registrering |
| Plattformsoberoende | Enhetsregistreringshanterare (DEM) | Registrera DEM-användare | Under registrering |
| iOS/iPadOS, macOS | Apples automatiska enhetsregistrering (DEP med användartillhörighet) | Användaren som registrerar sig | Under registrering |
| iOS/iPadOS, macOS | Apples automatiska enhetsregistrering (DEP utan användartillhörighet) | Inga | Inte tillämpligt |
| Android | Företagsägda, dedikerade Android-enheter | Inga | Inte tillämpligt |

## <a name="primary-user-and-azure-ad-device-owner"></a>Primär användare och Microsoft Azure AD-enhetsägare
I vissa fall kan den primära Intune-användaren skilja sig åt från egenskapen för Microsoft Azure AD-enhetens **Ägare** (kan visas under **Enheter** > **Azure AD-enheter**). Microsoft Azure AD-enhetsägaren läggs till under en enhets registrering i Azure Active Directory.

Den här kommande funktionen ställer automatiskt in egenskapen **Ägare** på nyregistrerade Hybrid Azure AD-anslutna enheter samtidigt som den primära Intune-användaren anges.

## <a name="next-steps"></a>Nästa steg
[Hantera dina Intune-enheter](device-management.md)
