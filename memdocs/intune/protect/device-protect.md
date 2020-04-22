---
title: Skydda enheter med Microsoft Intune
titleSuffix: Microsoft Intune
description: Läs olika exempel på hur Intune kan hjälpa dig att skydda dina enheter mot obehörig åtkomst och andra hot.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/19/2018
ms.topic: conceptual
ms.subservice: protect
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: c9ee00d13b32e1f52937489b86d29f075e5f580a
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79352312"
---
# <a name="protect-devices-with-microsoft-intune"></a>Skydda enheter med Microsoft Intune

Microsoft Intune hjälper dig att skydda de enheter som du hanterar och lagrade data på dessa enheter.

## <a name="device-configuration"></a>Enhetskonfiguration
Med Microsoft Intunes [konfigurationsprinciper](../configuration/device-profiles.md) kan du skydda och konfigurera enheter med hjälp av flera inställningar och funktioner. Till exempel:

- Du kan begränsa användningen av maskinvarufunktioner på enheten, till exempel kameran eller Bluetooth.
- Du kan konfigurera kompatibla och icke-kompatibla appar. Du får en avisering om en icke-kompatibel app installeras (och på vissa plattformar kan installationen blockeras).

## <a name="reset-passcodes-when-users-are-locked-out-of-their-devices"></a>Återställa lösenord när användare har låsts ute från sina enheter
Det första steget för att skydda företagets data på mobila enheter är att kräva ett lösenord för att använda enheten. Det betyder att du ibland kan behöva [återställa ett lösenord](../remote-actions/device-passcode-reset.md) eller hjälpa en anställd att göra det, antingen genom att ta bort lösenordet eller genom att ställa in ett tillfälligt lösenord på distans. Du kan också [fjärrlåsa en enhet](../remote-actions/device-remote-lock.md) om den blir stulen eller borttappad.

## <a name="retire-devices-and-remove-data"></a>Dra tillbaka enheter och ta bort data
När en enhet behöver [tas bort från Intune-hanteringen](../remote-actions/devices-wipe.md) (till exempel om en användare lämnar företaget eller om enheten blir stulen) vill du förmodligen ta bort data från enheten. Intune tillhandahåller flera metoder med vilka du kan skydda företagets data.

## <a name="require-devices-to-be-compliant"></a>Kräv att enheter är kompatibla
I Intune finns [efterlevnadsprinciper för enheter](device-compliance-get-started.md) som gör att du kan utvärdera (och i vissa fall reparera) enheter som inte uppfyller de regler som du anger. Du kan t.ex. få rapporter om:
- jailbrokade iOS/iPadOS-enheter
- krypterade eller inte krypterade enheter
- hälsotillståndet för Windows 10-enheter (som bestäms av tjänsten Hälsoattestering).

## <a name="protect-apps-and-the-data-they-use"></a>Skydda appar och de data som de använder
I Intune finns flera funktioner som hjälper dig att skydda appar och deras data. Principer för hantering av mobilprogram (MAM) kan:
- förhindra att data säkerhetskopieras från en skyddad app
- begränsa åtgärder för att kopiera och klistra in andra appar
- kräva en PIN-kod för att få åtkomst till en app. Mer information finns i [Skydda data och appar med Microsoft Intune](../apps/app-protection-policy.md)

## <a name="add-an-additional-layer-of-protection-to-devices"></a>Lägga till ett extra skyddslager för enheter
[Multi-Factor Authentication (MFA)](../enrollment/multi-factor-authentication.md) är ett säkrare sätt att autentisera enhetsanvändare i nätverket.  Med MFA måste användarna bekräfta sin identitet utöver användarnamn och lösenord, via ett telefonsamtal eller SMS.

## <a name="control-windows-hello-for-business-settings-on-windows-devices"></a>Kontrollera Windows Hello för företag-inställningar på Windows-enheter
Med Intune kan du integrera [Windows Hello för företag](windows-hello.md), som är en alternativ inloggningsmetod för Windows 10 och senare som använder Active Directory eller ett Azure Active Directory-konto i stället för ett lösenord, smartkort eller virtuellt smartkort.

## <a name="disable-activation-lock-on-ios-devices"></a>Inaktivera aktiveringslåset på iOS-enheter
Aktiveringslåset är en funktion som skyddar användarnas enheter. Funktionen kräver att användarna anger sina Apple-ID:n och lösenord innan de kan radera eller återaktivera enheter. Den här funktionen kan dock leda till problem om användaren t.ex. lämnar företaget utan att ta bort låset. [Inaktivera aktiveringslås för iOS/iPadOS](../remote-actions/device-activation-lock-disable.md) kan hjälpa genom att ta bort låset från de övervakade iOS/iPadOS-enheterna så att du kan allokera eller radera dem.

## <a name="next-steps"></a>Nästa steg

Läs mer om [skydd mot mobilhot](mobile-threat-defense.md)
