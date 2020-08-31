---
title: Partner för enhetsefterlevnad i Microsoft Intune – Azure | Microsoft Docs
description: Använd en partner för enhetsefterlevnad från tredje part som källa för efterlevnadsdata för enheter som du hanterar med Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/17/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe6a46c10f55378292e57548494852c4014c062a
ms.sourcegitcommit: 21b6c0c054e5371f32d611a2411ccd166b0e03bc
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88643711"
---
# <a name="support-third-party-device-compliance-partners-in-intune"></a>Stöd för partner från tredje part för enhetsefterlevnad i Intune

Microsoft Intune kan lägga till information om efterlevnadsstatus i Azure Active Directory (Azure AD) för de enheter som du hanterar med en eller flera tredjepartspartner för enhetsefterlevnad. Med den här konfigurationen kan efterlevnadsdata från dessa enheter användas med dina principer för villkorsstyrd åtkomst.

Som standard är Intune konfigurerat för att vara MDM-utfärdare (Mobile Device Management) för dina enheter. När du lägger till en efterlevnadspartner i Azure AD och Intune konfigurerar du partnern som källa för MDM-utfärdare (Mobile Device Management) för de enheter som du tilldelar den partnern via en Azure AD-användargrupp.

Slutför följande uppgifter för att möjliggöra användning av data från partner för enhetsefterlevnad:

1. **Konfigurera Intune så att det fungerar med partnern för enhetsefterlevnad** och konfigurera sedan grupper av användare vars enheter hanteras av den aktuella partnern.

2. **Konfigurera att din efterlevnadspartner ska skicka data till Intune**.

3. **Registrera dina iOS- eller Android-enheter hos den aktuella partnern för enhetsefterlevnad**.

När dessa uppgifter har slutförts skickar partnern för enhetsefterlevnad information om enhetstillstånd till Intune. Intune lägger sedan till den här informationen i Azure AD. Enheter med tillståndet icke-kompatibel får till exempel den statusen tillagd i enhetsposten i Azure AD.

Efterlevnadstillstånd utvärderas sedan av principer för villkorsstyrd åtkomst, samma som informationen om efterlevnadstillstånd för enheter som hanteras av Intune.  Som standard är Intune en registrerad efterlevnadspartner för iOS och Android. När du lägger till ytterligare partner kan du ange prioritetsordningen för att se till att rätt partner hanterar enheten så att det passar dina affärsbehov.

## <a name="supported-device-compliance-partners"></a>Partner för enhetsefterlevnad som stöds

Som förhandsversion:

- VMWare Workspace ONE UEM (tidigare AirWatch)

## <a name="prerequisites"></a>Förutsättningar

- En prenumeration på Microsoft Intune och åtkomst till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

- En prenumeration hos partnern för enhetsefterlevnad.

- Läs i dokumentationen för din efterlevnadspartner om vilka plattformar som stöds och ytterligare krav.

## <a name="configure-intune-to-work-with-a-device-compliance-partner"></a>Konfigurera Intune så att det fungerar med en partner för enhetsefterlevnad

Aktivera stöd för partner för enhetsefterlevnad om du vill använda information om efterlevnadsstatus från den partnern med dina principer för villkorsstyrd åtkomst.

### <a name="add-a-compliance-partner-to-intune"></a>Lägga till en efterlevnadspartner i Intune

1. Logga in på [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Gå till **Innehavaradministration** > **Anslutningsprogram och token** > **Hantering av partnerefterlevnad** > **Lägg till efterlevnadspartner**.

   > [!div class="mx-imgBorder"]
   > ![Lägga till en partner för enhetsefterlevnad](./media/device-compliance-partners/add-compliance-partner.png)

3. På sidan **Grundläggande inställningar** expanderar du listrutan **Efterlevnadspartner** och väljer den partner som du ska lägga till.

   - Om du vill använda VMware Workspace ONE som efterlevnadspartner för iOS- eller Android-plattformar väljer du **VMware Workspace ONE mobilefterlevnad**.

   Välj sedan listrutan för **Plattform** och välj plattformen. macOS stöds inte i den här förhandsversionen.

   Du är begränsad till en partner per plattform, även om du har lagt till flera efterlevnadspartner i Azure AD.

4. Välj de användargrupper vars enheter ska hanteras av den här partnern vid **Tilldelningar**. Med den här tilldelningen ändrar du MDM-utfärdare för tillämpliga enheter till den här partnern. Användare som har enheter som hanteras av partnern måste också tilldelas en licens för Intune.

5. På sidan **Granska och skapa** granskar du dina val och väljer sedan **Skapa** för att slutföra den här konfigurationen.

Konfigurationen visas nu på sidan Hantering av partnerefterlevnad.

### <a name="modify-the-configuration-for-a-compliance-partner"></a>Ändra konfigurationen för en efterlevnadspartner

1. Logga in på [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Gå till **Innehavaradministration** > **Anslutningsprogram och token** > **Hantering av partnerefterlevnad** och välj den partnerkonfiguration som du vill ändra. Konfigurationer ordnas efter plattformstyp.

3. På sidan **Översikt** över partnerkonfiguration väljer du **Egenskaper** för att öppna sidan Egenskaper där du kan redigera tilldelningarna.

4. På sidan **Egenskaper** väljer du **Redigera** för att öppna vyn Tilldelningar där du kan ändra de grupper som ska använda den här konfigurationen.

5. Välj **Granska och spara** och **Spara** för att spara dina ändringar.

6. *Det här steget gäller bara när du använder en VMware Workspace ONE*:

   Från Workspace ONE UEM-konsolen måste du manuellt synkronisera ändringarna som du sparade i administrationscentret för Microsoft Endpoint Manager. Tills du har synkroniserat ändringarna manuellt är Workspace ONE UEM inte medveten om konfigurationsändringarna och tar inte emot efterlevnadsrapporter från användare i nya grupper som du har tilldelat.

   Synkronisera manuellt från Azure-tjänster:
   1. Logga in på din VMware Workspace One UEM-konsol.
   2. Gå till **Inställningar** > **System** > **Enterprise-integration** > **Katalogtjänster**.
   3. För *Synkronisera Azure-tjänster* klickar du på **SYNKRONISERA**.

      Alla ändringar du har gjort sedan den inledande konfigurationen eller den senaste manuella synkroniseringen synkroniseras från Azure-tjänster till UEM.  

## <a name="configure-your-compliance-partner-to-work-with-intune"></a>Konfigurera din efterlevnadspartner så att den fungerar med Intune

Om du vill att en partner för enhetsefterlevnad ska fungera med Intune måste du slutföra konfigurationer som är specifika för den partnern. Information om den här uppgiften finns i dokumentationen för den aktuella partnern:

- [VMware Workspace ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)  

## <a name="enroll-your-ios-or-android-devices-to-that-device-compliance-partner"></a>Registrera dina iOS- eller Android-enheter hos den aktuella partnern för enhetsefterlevnad

Information om hur du registrerar enheter med den partnern hittar du i dokumentationen om partner för enhetsefterlevnad. När enheterna har registrerats och skickat efterlevnadsdata till partnern vidarebefordras dessa data till Intune och läggs till i Azure AD.

## <a name="monitor-devices-managed-by-third-party-device-compliance-partners"></a>Övervaka enheter som hanteras av tredjepartspartner för enhetsefterlevnad

När du har konfigurerat tredjepartspartner för enhetsefterlevnad och registrerat enheterna hos dem kommer partnern att vidarebefordra efterlevnadsinformation till Intune. När Intune har mottagit informationen kan du visa data om enheterna i Azure Portal.

Logga in på Azure Portal och gå till **Microsoft Intune** > **Enheter** > [**Alla enheter**](https://portal.azure.com/#blade/Microsoft_AAD_Devices/DevicesMenuBlade/Devices/menuId/).

## <a name="next-steps"></a>Nästa steg

Använd dokumentationen från din tredje partspartner för att skapa efterlevnadsprinciper för enheter.

- [VMware Workspace ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)
