---
title: Inställningar för delade Windows Holographic for Business-enheter – Microsoft Intune – Azure | Microsoft Docs
description: Lägg till och använd Windows Holographic for Business för att konfigurera enheter som är delade eller som används av flera användare i Microsoft Intune. Se en lista över inställningar för kontohantering och vad de gör på enheterna, inklusive Microsoft HoloLens.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 88b7f41b873697a7ec34bd1fc2f1098384ab1c18
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915729"
---
# <a name="windows-holographic-for-business-settings-to-manage-shared-devices-using-intune"></a>Windows Holographic for Business-inställningar för hantering av delade enheter med Intune

Windows Holographic for Business-enheter, som Microsoft HoloLens, kan användas av flera användare. Enheter som har flera användare kallas delade enheter och är en del av MDM-lösningar (hantering av mobilenheter).

Med Microsoft Intune kan användare logga in på dessa delade enheter med ett gästkonto. När de använder enheten får de bara åtkomst till funktioner du tillåter.

Den här artikeln listar och beskriver de inställningar du använder i en Windows Holographic for Business-enhetskonfigurationsprofil. När profilen har skapats i Intune distribuerar och tilldelar du sedan profilen till enhetsgrupper i organisationen. Du kan även tilldela profilen till en enhetsgrupp med blandade enhetstyper och OS-versioner.

Mer information om den här funktionen i Intune finns i [Styra åtkomst, konton och energifunktioner på delade datorer eller enheter med flera användare](shared-user-device-settings.md). Mer information om Windows CSP finns i [AccountManagement CSP](/windows/client-management/mdm/accountmanagement-csp).

## <a name="before-your-begin"></a>Innan du börjar

[Skapa en enhetskonfigurationsprofil för delad enhet för flera användare i Windows 10](shared-user-device-settings.md).

När du skapar en delad konfigurationsprofil för Windows 10 finns det fler inställningar än vad som anges i den här artikeln. Inställningarna i den här artikeln stöds på Windows Holographic for Business-enheter.

## <a name="shared-multi-user-device-settings"></a>Inställningar för delade enheter med flera användare

> [!NOTE]
> Enheter som kör Windows Holographic for Business, inklusive Microsoft HoloLens, stöder bara inställningarna i **Kontohantering**. Om du konfigurerar några av de andra inställningarna som visas i Intune, till exempel **Läget för delad dator**, har det ingen inverkan på dessa enheter.

- **Kontohantering**: Välj om konton ska tas bort automatiskt. Alternativen är:
  - **Inte konfigurerat** (standard): Tar automatiskt bort lokala konton som skapats av gäster, konton i AD och Azure AD. När en användare loggar ut enheten, eller när systemunderhåll körs, tas dessa konton bort.

    Ange även:

    - **Borttagning av konto**: Välj när konton tas bort:
      - **Vid tröskelvärdet för lagringsutrymme**
      - **Vid tröskelvärdet för lagringsutrymme och tröskelvärdet för inaktivitet**
      - **Omedelbart efter utloggning**

    Ange även:

    - **Starta borttagning (%)** : Ange ett procenttal (0–100) för diskutrymme. När det totala disk-/lagringsutrymmet sjunker under det värde du anger tas cachelagrade konton bort. Konton tas bort kontinuerligt för att frigöra diskutrymme. Konton som har varit inaktiva längst tas bort först.
    - **Avbryt borttagning (%)** : Ange ett procenttal (0–100) för diskutrymme. När det totala disk-/lagringsutrymmet uppfyller det värde du anger avbryts borttagningen.

  - **Inaktivera**: Lokala konton, AD- och Azure AD-konton som skapats av gäster stannar på enheten och tas inte bort.

## <a name="next-steps"></a>Nästa steg

- [Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).
- Se inställningarna för delad användarenhet i [Windows 10 och senare](shared-user-device-settings-windows.md).