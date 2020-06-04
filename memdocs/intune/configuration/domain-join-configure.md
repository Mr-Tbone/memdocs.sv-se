---
title: Domänanslutningsinställningar för Windows 10 i Microsoft Intune – Azure | Microsoft Docs
description: Skapa en konfigurationsprofil för domänanslutningsenhet för Azure AD-anslutna hybridenheter. Använd profilen för att distribuera lokal Active Directory-domäninformation till enheter som tillhandahålls med Windows Autopilot och Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 211722a02183d3b86525468f907d4093331d9de6
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988428"
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

    - **Plattform**: Välj **Windows 10 och senare**.
    - **Profil**: Välj **Domänanslutning (förhandsversion)** .

4. Välj **Skapa**.
5. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange ett beskrivande namn på principen. Namnge dina principer så att du enkelt kan identifiera dem senare. Exempel på ett bra principnamn: **Windows 10: Domänanslutningsprofil som innehåller information om lokal domän för registrering av anslutna AD-hybridenheter med Windows Autopilot**.
    - **Beskrivning**: Ange en beskrivning av principen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.
7. Välj **Konfigurationsinställningar** och ange följande egenskaper:

    - **Datornamnsprefix**: Ange ett prefix för enhetsnamnet. Datornamn är 15 tecken långa. Efter prefixet genereras de återstående 15 tecknen slumpmässigt.
    - **Domännamn**: Ange det fullständiga domännamn (FQDN) som enheterna ska anslutas till. Ange till exempel `americas.corp.contoso.com.`
    - **Organisationsenhet** (valfritt): Ange den fullständiga sökvägen ([unikt namn](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name)) till den organisationsenhet (OU) där datorkontona ska skapas. Ange till exempel `"CN=Users,DC=Contoso,DC=com"`. Om du inte anger något värde används en välkänd datorobjektcontainer.

      Mer information och råd om den här inställningen finns i [Distribuera Azure AD-anslutna hybridenheter](../enrollment/windows-autopilot-hybrid.md).

8. Välj **Nästa**.

9. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

    Välj **Nästa**.

10. Under **Tilldelningar** väljer du de användare eller den användargrupp som ska få din profil. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](device-profile-assign.md).

    Välj **Nästa**.

11. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

Den är nu redo så att du kan [distribuera Azure AD-anslutna hybridenheter med hjälp av Intune och Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).

## <a name="next-steps"></a>Nästa steg

När profilen har [tilldelats](device-profile-assign.md) [övervakar du dess status](device-profile-monitor.md).

[Distribuera Azure AD-anslutna hybridenheter med hjälp av Intune och Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).
