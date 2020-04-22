---
title: Domänanslutningsinställningar för Windows 10 i Microsoft Intune – Azure | Microsoft Docs
description: Skapa en konfigurationsprofil för domänanslutningsenhet för Azure AD-anslutna hybridenheter. Använd profilen för att distribuera lokal Active Directory-domäninformation till enheter som tillhandahålls med Windows Autopilot och Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 207b3983c214ad4e166ae58ea0ccd18ea23bf418
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79364402"
---
# <a name="configuration-domain-join-settings-for-hybrid-azure-ad-joined-devices-in-microsoft-intune"></a>Inställningar för domänanslutningskonfiguration för Azure AD-anslutna hybridenheter i Microsoft Intune

I många miljöer används lokal Active Directory (AD). När AD-domänanslutna enheter även är anslutna till Azure AD kallas de för Azure AD-anslutna hybridenheter. Använd Windows Autopilot till att [registrera Azure AD-anslutna hybridenheter](../enrollment/windows-autopilot-hybrid.md) i Microsoft Intune. För att kunna registrera dig behöver du också en konfigurationsprofil för **Domänanslutning**.

En konfigurationsprofil för **Domänanslutning** innehåller domäninformation för det lokala Active Directory. När enheterna etableras (och vanligtvis är offline) distribuerar profilen AD-domäninformationen så att enheterna vet vilken lokal domän de ska ansluta till. Om du inte skapar någon domänanslutningsprofil kanske enheterna inte kan distribueras.

Den här funktionen gäller för:

- Windows 10 och senare
- Azure AD-anslutna hybridenheter
- Hybriddistribution med Autopilot + Intune

Den här artikeln visar hur du skapar en domänanslutningsprofil för en Autopilot-hybriddistribution. Du kan också se tillgängliga inställningar.

## <a name="create-the-profile"></a>Skapa profilen

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande egenskaper:

    - **Namn**: Ange ett beskrivande namn på principen. Namnge dina principer så att du enkelt kan identifiera dem senare. Exempel på ett bra principnamn: **Windows 10: Domänanslutningsprofil som innehåller information om lokal domän för registrering av anslutna AD-hybridenheter med Windows Autopilot**.
    - **Beskrivning**: Ange en beskrivning av principen. Denna inställning är valfri, men rekommenderas.
    - **Plattform**: Välj **Windows 10 och senare**.
    - **Profiltyp**: Välj **Domänanslutning (förhandsversion)** .

4. Välj **Inställningar**. Ange följande egenskaper:

    - **Datornamnsprefix**: Ange ett prefix för enhetsnamnet. Datornamn är 15 tecken långa. Efter prefixet genereras de återstående 15 tecknen slumpmässigt.
    - **Domännamn**: Ange det fullständiga domännamn (FQDN) som enheterna ska anslutas till. Ange till exempel `americas.corp.contoso.com.`
    - **Organisationsenhet** (valfritt): Ange den fullständiga sökvägen ([unikt namn](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name)) till den organisationsenhet (OU) där datorkontona ska skapas. Ange till exempel `"CN=Users,DC=Contoso,DC=com"`. Om du inte anger något värde används en välkänd datorobjektcontainer.

      Mer information och råd om den här inställningen finns i [Distribuera Azure AD-anslutna hybridenheter](../enrollment/windows-autopilot-hybrid.md).

5. När du är klar väljer du **OK** > **Skapa** för att spara dina ändringar.

Profilen skapas och visas i profillistan. Den är nu redo så att du kan [distribuera Azure AD-anslutna hybridenheter med hjälp av Intune och Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).

## <a name="next-steps"></a>Nästa steg

När profilen har skapats är den klar att tilldelas. [Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

[Distribuera Azure AD-anslutna hybridenheter med hjälp av Intune och Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).
