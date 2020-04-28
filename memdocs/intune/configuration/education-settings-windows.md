---
title: Utbildningsinställningar för Windows 10 i Microsoft Intune – Azure | Microsoft Docs
description: Se en lista över alla utbildningsinställningar för Windows 10-enheter. Använd de här inställningarna i en konfigurationsprofil för enheter med appen Gör ett prov, välj hur användare eller elever loggar in, övervaka skärmen under provet och mer i Intune.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/03/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 551f0a442f81712cff29a9ff6f55c62aeaba547a
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078200"
---
# <a name="configure-the-take-a-test-app-on-windows-10-devices-using-intune"></a>Konfigurera appen Gör ett prov på Windows 10-enheter med Intune

Med appen Gör ett prov kan du på ett säkert sätt administrera onlinetester på klassrummets Windows 10-enheter. Om du ska konfigurera appen Gör ett prov, måste du skapa en profil för enhetskonfigurationer i Intune och konfigurera inställningarna för en begränsad provmiljö. I den här artikeln beskrivs inställningarna för appen Gör ett prov. 

När du har konfigurerat profilen tilldelar och distribuerar du den till dina elever. 

[Appen Gör ett prov i Intune](education-settings-configure.md) har mer information om den här funktionen.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en enhetskonfigurationsprofil](education-settings-configure.md#create-a-device-profile).

## <a name="take-a-test-settings"></a>Inställningar för Gör ett prov
När du har skapat en enhetskonfigurationsprofil går du till **Profiltyp** och väljer **Begränsad provmiljö (utbildning)** . Där finns följande appinställningar för Gör ett prov. 


- **Kontotyp**: Välj hur användare loggar in på provet. Alternativen är:
  - Azure AD-konto
  - Domänkonto
  - Lokalt konto
  - Lokalt gästkonto: Endast tillgängligt på enheter som kör Windows 10, version 1903 och senare.    
- **Användarnamn för kontot**: Ange användarnamnet för det konto som används till appen Gör ett prov. Du kan ange konton i följande format:
  - `user@contoso.com`
  - `domain\username`
  - `user@contoso.com`
  - `computerName\username`
- **Kontonamn**: Om du ska konfigurera ett lokalt gästkonto anger du namnet på kontot som används med appen Gör ett prov. Kontonamnet visas som en ikon på inloggningsskärmen. Eleverna klickar på ikonen för att starta testet.  
- **Webbadress till begränsad provmiljö**: Ange webbadressen till det prov som du vill att användarna ska göra. Mer information om hur du hämtar webbadressen finns i [dokumentationen för Gör ett prov](https://docs.microsoft.com/education/windows/take-tests-in-windows-10).
- **Skrivaranslutning**: Välj **Krävs** för att enbart tillåta åtkomst till appen Gör ett prov från enheter som är anslutna till en skrivare. Den här inställningen innebär att appens utskriftsknapp blir tillgänglig för de som ska göra provet. **Inte konfigurerad** innebär att eleverna kommer åt appen från enheter som inte är anslutna till någon skrivare.  
- **Skärmövervakning**: Välj **Tillåt** för att övervaka skärmaktiviteten medan användarna gör provet. **Inte konfigurerad** förhindrar dig från att övervaka skärmen under provet.
- **Textförslag**: Välj **Tillåt** så kan provdeltagarna se textförslag. **Inte konfigurerat** blockerar textförslag medan användarna gör ett prov.

## <a name="next-steps"></a>Nästa steg

Kom ihåg att [tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).
