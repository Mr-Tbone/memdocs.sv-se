---
title: Inställningar i Microsoft Intune för delade enheter eller enheter med flera användare – Azure | Microsoft Docs
description: Lägg till och använd Windows 10 och Windows Holographic for Business-enheter som är delade eller som används av flera användare i Microsoft Intune. Se en lista över alla inställningar och vad de gör på enheterna, inklusive Microsoft HoloLens. Kontrollera gästkonton, hantera konton och ta bort inaktiva konton, tillåt eller förhindra att spara i lokal lagring, ange energi- och strömsparalternativ, välj när uppdateringar installeras och använd enheter i utbildningsmiljöer i en enhetskonfigurationsprofil.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f85c30c9472849d26802c8cdccd7a95006a3e4a
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83984006"
---
# <a name="control-access-accounts-and-power-features-on-shared-pc-or-multi-user-devices-using-intune"></a>Kontrollera åtkomst, konton och energifunktioner på delade datorer eller enheter med flera användare med Intune

Enheter som har flera användare kallas delade enheter och är en vanlig del av MDM-lösningar (hantering av mobilenheter). Med Microsoft Intune kan du anpassa delade enheter som kör följande plattformar:

- Windows 10 Professional och senare
- Windows 10 Enterprise och senare
- Windows Holographic for Business, till exempel HoloLens

Till exempel har skolor enheter som normalt används av många elever. Med den här inställningen kan skolans Intune-administratör aktivera delad dator-funktionen för att tillåta en användare åt gången. Elever kan inte växla mellan olika inloggade konton på enheten. När eleven loggar ut väljer du även att ta bort alla användarspecifika inställningar.

Slutanvändare kan logga in på dessa delade enheter med ett gästkonto. När användare loggar in cachelagras autentiseringsuppgifterna. När slutanvändarna använder enheten får de bara åtkomst till funktioner du tillåter. Till exempel väljer du när enheten försätts i strömsparläge, om användarna kan se och spara filer lokalt, att aktivera eller inaktivera energisparfunktioner med mera. Du styr även om gästkontot tas bort när användaren loggar ut eller inaktiva konton tas bort när ett tröskelvärde nås.

Den här artikeln visar hur du skapar en konfigurationsprofil och innehåller länkar till tillgängliga inställningar med deras beskrivningar.

När profilen har skapats i Intune distribuerar och tilldelar du profilen till enhetsgrupper i organisationen. Du kan också tilldela den här profilen till enhetsgrupper med blandade enhetstyper och versioner av operativsystemet (OS).

## <a name="create-the-profile"></a>Skapa profilen

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande egenskaper:

   - **Plattform**: Välj **Windows 10 och senare**.
   - **Profil**: Välj **Delad enhet för flera användare**.

4. Välj **Skapa**.
5. Ange följande egenskaper i **Grundinställningar**:

   - **Namn**: Ange ett beskrivande namn på den nya profilen.
   - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.
7. Under **Konfigurationsinställningar**  visas olika inställningar som du kan konfigurera beroende på vilken plattform du väljer. Välj din plattform för detaljerade inställningar:

    - [Windows 10 och senare](shared-user-device-settings-windows.md)
    - [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md)

8. Välj **Nästa**.

9. Under **Omfångstaggar** (valfritt), tilldelar du en tagg för att filtrera profilen till specifika IT-grupper, till exempel `US-NC IT Team` eller `JohnGlenn_ITDepartment`. Mer information om omfångstaggar finns i [Använda RBAC och omfångstaggar för distribuerad IT](../fundamentals/scope-tags.md).

    Välj **Nästa**.

10. Under **Tilldelningar** väljer du de enhetsgrupper som ska få din profil. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](device-profile-assign.md).

    Välj **Nästa**.

    > [!NOTE]
    > Se till att tilldela profilen till enhetsgrupper i din organisation.

11. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

Nästa gång varje enhet checkar in tillämpas principen.

## <a name="next-steps"></a>Nästa steg

- Se alla inställningar för [Windows 10 och senare](shared-user-device-settings-windows.md) och [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md).
- När [profilen har tilldelats](device-profile-assign.md) [övervakar du dess status](device-profile-monitor.md).
