---
title: Inställningar för delade Windows 10-enheter – Microsoft Intune – Azure | Microsoft Docs
description: Lägg till och använd Windows 10 för att konfigurera enheter som är delade eller som används av flera användare i Microsoft Intune. Se en lista över alla inställningar och vad de gör på enheterna, inklusive Microsoft Surface. Kontrollera gästkonton, hantera konton och ta bort inaktiva konton, tillåt eller förhindra att spara i lokal lagring, ange energi- och strömsparalternativ, välj när uppdateringar installeras och använd enheter i utbildningsmiljöer i en enhetskonfigurationsprofil.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
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
ms.openlocfilehash: f013074ac67b7622b509d8b9781de3ab5f4041e0
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429496"
---
# <a name="windows-10-and-later-settings-to-manage-shared-devices-using-intune"></a>Inställningar för Windows 10 och senare för att hantera delade enheter med Intune

Enheter med Windows 10 och senare, till exempel Microsoft Surface, kan användas av många användare. Enheter som har flera användare kallas delade enheter och är en del av MDM-lösningar (hantering av mobilenheter).

Med Microsoft Intune kan slutanvändare logga in på dessa delade enheter med ett gästkonto. När de använder enheten får de bara åtkomst till funktioner du tillåter. Som Intune-administratör konfigurerar du åtkomst, väljer när konton tas bort, styr energisparfunktionernas inställningar med mera för dina delade Windows 10-enheter.

Den här artikeln listar och beskriver de inställningar du använder i en enhetskonfigurationsprofil för Windows 10 (och senare). När profilen har skapats i Intune distribuerar och tilldelar du profilen till enhetsgrupper i organisationen. Du kan även tilldela profilen till en enhetsgrupp med blandade enhetstyper och OS-versioner.

Mer information om den här funktionen i Intune finns i [Styra åtkomst, konton och energifunktioner på delade datorer eller enheter med flera användare](shared-user-device-settings.md). Mer information om Windows CSP finns i [SharedPC CSP](https://docs.microsoft.com/windows/client-management/mdm/sharedpc-csp).

## <a name="before-your-begin"></a>Innan du börjar

[Skapa profilen](shared-user-device-settings.md).

## <a name="shared-multi-user-device-settings"></a>Inställningar för delade enheter med flera användare

Dessa inställningar använder [SharedPC CSP](https://docs.microsoft.com/windows/client-management/mdm/sharedpc-csp).

- **Läget för delad dator**: **Aktivera** aktiverar läget för datordelning. I det här läget loggar bara en användare i taget in på enheten. En annan användare kan inte logga in förrän den första loggar ut. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Gästkonto**: Välj alternativet om du vill skapa ett gästalternativ på inloggningssidan. Gästkonton kräver inte några användarautentiseringsuppgifter eller någon autentisering. Den här inställningen skapar ett nytt lokalt konto varje gång den används. Alternativen är:
  - **Gäst**: Skapar ett gästkonto lokalt på enheten.
  - **Domän**: Skapar ett gästkonto i Azure Active Directory (AD).
  - **Gäst och domän**: Skapar ett gästkonto lokalt på enheten och i Azure Active Directory (AD).
- **Kontohantering**: Välj om konton ska tas bort automatiskt. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Aktiverad**: Konton som skapas av gäster, konton i AD och Azure AD tas bort automatiskt. När en användare loggar ut enheten, eller när systemunderhåll körs, tas dessa konton bort.

    Ange även:

    - **Borttagning av konto**: Välj när konton tas bort:
      - **Vid tröskelvärdet för lagringsutrymme**
      - **Vid tröskelvärdet för lagringsutrymme och tröskelvärdet för inaktivitet**
      - **Omedelbart efter utloggning**

    Ange även:

    - **Starta borttagning (%)** : Ange ett procenttal (0–100) för diskutrymme. När det totala disk-/lagringsutrymmet sjunker under det värde du anger tas cachelagrade konton bort. Konton tas bort kontinuerligt för att frigöra diskutrymme. Konton som har varit inaktiva längst tas bort först.
    - **Avbryt borttagning (%)** : Ange ett procenttal (0–100) för diskutrymme. När det totala disk-/lagringsutrymmet uppfyller det värde du anger avbryts borttagningen.
    - **Tröskelvärde för inaktivt konto**: Ange antalet dagar i rad innan borttagning av kontot som inte har loggat in, mellan 0–60 dagar.

  - **Inaktiverad**: Lokala konton, AD- och Azure AD-konton som skapats av gäster stannar på enheten och tas inte bort.

- **Lokal lagring**: Med lokal lagring kan användarna spara och visa filer på enhetens hårddisk. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Aktiverad**: Förhindrar att användarna sparar och visar filer på enhetens hårddisk.
  - **Inaktiverad**: Tillåter att användarna visar och sparar filer lokalt med Utforskaren.

- **Energisparprinciper**: Tillåt eller förhindra att användare ändra energisparinställningar. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Aktiverad**: Användarna kan inte inaktivera viloläge, åsidosätta alla vilolägesåtgärder (som att fälla ned locket) eller ändra energisparinställningarna.
  - **Inaktiverad**: Användarna kan försätta enheten i viloläge, fälla ned locket för att aktivera viloläge och ändra energisparinställningarna.

- **Vilogräns (sekunder)** : Ange antalet inaktiva sekunder (0–18 000) innan enheten försätts i strömsparläge. `0` innebär att enheten aldrig är i viloläge. Om du inte anger en tid försätts enheten i strömsparläge efter 3 600 sekunder (60 minuter).

- **Logga in när datorn väcks**: Välj om användarna måste logga in när enheten varit i viloläge. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Aktiverad**: Användarna måste logga in med ett lösenord när enheten lämnar viloläge.
  - **Inaktiverad**: Användarna måste inte ange användarnamn och lösenord.

- **Starttid för underhåll (minuter från midnatt)** : Ange tiden i minuter (0–1 440) när automatiska underhållsuppgifter, som Windows Update, körs. Standardstarttiden är midnatt, eller noll (`0`) minuter. Ändra starttiden genom att ange en starttid i minuter från midnatt. Om du till exempel vill att underhållet ska börja kl. 02:00 anger du `120`. Om du vill att underhållet ska börja kl. 20:00 anger du `1200`.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

- **Utbildningsprinciper**: Välj om policyer för utbildningsmiljön är aktiverade. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Aktiverad**: De rekommenderade inställningarna för enheter som används i skoloranvänds, som är mer restriktiva.
  - **Inaktiverad**: Standardinställningar och rekommenderade utbildningspolicyer används inte.

  Mer information om vad utbildningsprinciper gör finns i [Rekommendationer för Windows 10-konfiguration för utbildningskunder](https://docs.microsoft.com/education/windows/configure-windows-for-education).

> [!TIP]
> [Konfigurera en delad dator eller en gästdator](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc) (en annan dokumentwebbplats öppnas) är en bra resurs om den här Windows 10-funktionen, som beskriver begrepp och grupprinciper som kan ställas in i delat läge.

## <a name="next-steps"></a>Nästa steg

- [Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).
- Se inställningarna för [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md).
