---
title: Aktivera borttappat läge för iOS/iPadOS med Microsoft Intune – Azure | Microsoft Docs
description: Aktivera eller starta borttappat läge för att anpassa ett meddelande som visas på låsskärmen på en borttappad eller stulen iOS/iPadOS-enhet med hjälp av Microsoft Intune. Få även information om säkerhet och sekretess när du använder åtgärden för borttappat läge.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 126a7489-fe3e-43fd-a681-defb2fe0bb66
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: acb8a7d4c5ab73cde7f50365e91ef985fdaf341f
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79349088"
---
# <a name="enable-lost-mode-on-iosipados-devices-with-intune"></a>Aktivera borttappat läge på iOS/iPadOS-enheter med Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Med enhetsåtgärden **Borttappat läge** kan du aktivera borttappat läge på förlorade eller stulna iOS/iPadOS-enheter. Med det här läget kan du ange ett meddelande och ett telefonnummer som visas på enhetens låsskärm. Enheten måste vara en företagsägd iOS/iPadOS-enhet som är i övervakat läge för att kunna använda borttappat läge.

## <a name="supported-platforms"></a>Plattformar som stöds

- iOS 9.3 och senare
- iPad 13.0 eller senare

Den här funktionen stöds inte för: 
- Windows
- Windows Phone
- macOS
- Android

## <a name="enable-lost-mode"></a>Aktivera borttappat läge

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Välj **Enheter** och sedan **Alla enheter**.
4. I listan med enheter som du hanterar väljer du en iOS/iPadOS-enhet och sedan **Borttappat läge (endast övervakat)** .
5. Under **Borttappat läge**, väljer du **Aktivera**.
6. I **Meddelande som ska visas på låsskärmen**, skriver du ett meddelande som ska visas på enhetens låsskärm.
7. Alternativt kan du ange ett telefonnummer i rutan **Telefonnummer att visa**.
6. Klicka på **OK** för att spara ändringarna.

När du aktiverar borttappat läge blockeras all användning av enheten. Slutanvändaren kan inte öppna enheten förrän du inaktiverar borttappat läge. När borttappat läge är aktiverat kan du hitta enheten med hjälp av åtgärden [Hitta enhet](device-locate.md).

## <a name="security-and-privacy-information-for-the-lost-mode-and-locate-device-actions"></a>Information om säkerhet och sekretess för åtgärderna för borttappat läge och hitta enhet
- Ingen platsinformation för enheten skickas till Intune förrän du har aktiverat den här åtgärden.
- När du använder åtgärden Hitta enhet skickas enhetens latitud- och longitudkoordinater till Intune och visas i Azure-portalen.
- Data lagras i 24 timmar och tas sedan bort. Du kan inte ta bort platsdata manuellt.
- Platsinformationen krypteras både under lagring och vid överföring.
- Se till att ta med information för att återlämna den borttappade enheten i det meddelande som ska visas på låsskärmen.

## <a name="next-steps"></a>Nästa steg

Om du vill se status för aktivering av borttappat läge öppnar du **Enheter** och väljer **Enhetsåtgärder**.
