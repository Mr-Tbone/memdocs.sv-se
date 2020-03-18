---
title: Operativsystem och webbläsare som stöds av Microsoft Intune
titleSuffix: ''
description: Visar en lista över enhetsplattformar och webbläsare som stöds för Intunes enhetshantering
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/19/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5d1ac59c-a885-4276-8576-f3cf81c2d268
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7f2fd16e0d4130fcc13b69a34d17777f1fd3d0f4
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79355913"
---
# <a name="supported-operating-systems-and-browsers-in-intune"></a>Operativsystem och webbläsare som stöds i Intune

Granska de operativsystem och webbläsare som stöds innan du installerar Microsoft Intune.

Hjälp med att installera Intune på din enhet finns i [Användning av hanterade enheter för att få jobbet gjort](https://docs.microsoft.com/user-help/company-portal-frequently-asked-questions) och [Bandbreddsanvändning i Intune-nätverk](network-bandwidth-use.md).

Mer information om stöd för tjänstens konfigurationsprovider finns i [Referens för CSP (Configuration Service Provider)](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference).

> [!NOTE]
> Intune kräver nu Android 5.x (Lollipop) eller högre för att program och enheter ska få åtkomst till företagsresurser via företagsportalappen för Android och Intune App SDK för Android. Detta krav gäller INTE för Polycom Android-baserade Teams-enheter som kör version 4.4. Dessa enheter kommer att fortsätta stödjas. 

## <a name="intune-supported-operating-systems"></a>Operativsystem som stöds i Intune

Du kan hantera enheter som kör följande operativsystem:

[!INCLUDE [mdm-supported-devices](../includes/mdm-supported-devices.md)]

### <a name="supported-samsung-knox-standard-devices"></a>Samsung Knox Standard-enheter som stöds

För att undvika fel med Knox-aktivering förhindrar MDM-registrering försöker appen Företagsportal bara att utföra Samsung Knox-aktivering vid MDM-registrering om enheten visas i [listan över Knox-enheter som stöds](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Enheter som inte har stöd för Samsung Knox-aktivering registreras som Android-standardenheter. En Samsung-enhet kan ha vissa modellnummer som har stöd för Knox medan andra inte stöds. Kontrollera att Knox är kompatibelt med enhetsåterförsäljaren innan du köper och distribuerar Samsung-enheter.

> [!NOTE]
> Registrering av Samsung Knox-enheter kan kräva att du [ger åtkomst till Samsung-servrar](https://support.samsungknox.com/hc/articles/115013833108-Our-corporate-devices-are-behind-a-firewall-How-do-I-enable-Knox-Workspace-devices-to-contact-Samsung-servers).

Följande är en lista över Samsung-enhetsmodeller som inte har stöd för Knox. De registreras som inbyggda Android-enheter av appen Företagsportal för Android:

| **Enhetsnamn** | **Enhetsmodellnummer** |
| --- | --- |
| Galaxy Avant | SM-G386T |
| Galaxy Core 2/Core 2 Duos | SM-G355H<br>SM-G355M |
| Galaxy Core Lite | SM-G3588V |
| Galaxy Core Prime | SM-G360H |
| Galaxy Core LTE | SM-G386F<br>SM-G386W |
| Galaxy Grand | GT-I9082L<br>GT-I9082<br>GT-I9080L |
| Galaxy Grand 3 | SM-G7200 |
| Galaxy Grand Neo | GT-I9060I |
| Galaxy Grand Prime Value Edition | SM-G531H |
| Galaxy J Max | SM-T285YD |
| Galaxy J1 | SM-J100H<br>SM-J100M<br>SM-J100ML |
| Galaxy J1 Ace | SM-J110F<br>SM-J110H |
| Galaxy J1 Mini | SM-J105M |
| Galaxy J2/J2 Pro | SM-J200H<br>SM-J210F |
| Galaxy J3 | SM-J320F<br>SM-J320FN<br>SM-J320H<br>SM-J320M |
| Galaxy K Zoom | SM-C115 |
| Galaxy Light | SGH-T399N |
| Galaxy Note 3 | SM-N9002<br>SM-N9009 |
| Galaxy Note 7/Note 7 Duos | SM-N930S<br>SM-N9300<br>SM-N930F<br>SM-N930T<br>SM-N9300<br>SM-N930F<br>SM-N930S<br>SM-N930T |
| Galaxy Note 10.1 3G | SM-P602 |
| Galaxy S2 Plus | GT-I9105P |
| Galaxy S3 Mini | SM-G730A<br>SM-G730V |
| Galaxy S3 Neo | GT-I9300<br>GT-I9300I |
| Galaxy S4 | SM-S975L |
| Galaxy S4 Neo | SM-G318ML |
| Galaxy S5 | SM-G9006W |
| Galaxy S6 Edge | 404SC |
| Galaxy Tab A 7.0&quot; | SM-T280<br>SM-T285 |
| Galaxy Tab 3 7&quot;/Tab 3 Lite 7&quot; | SM-T116<br>SM-T210<br>SM-T211 |
| Galaxy Tab 3 8.0&quot; | SM-T311 |
| Galaxy Tab 3 10.1&quot; | GT-P5200<br>GT-P5210<br>GT-P5220 |
| Galaxy Trend 2 Lite | SM-G318H |
| Galaxy V Plus | SM-G318HZ |
| Galaxy Young 2 Duos | SM-G130BU |

### <a name="windows-pc-software-client"></a>Windows PC-programvaruklient

En [Intune-programvaruklient](manage-windows-pcs-with-microsoft-intune.md) kan distribueras och installeras på Windows-datorer som en alternativ metod för registrering. Den här funktionen är bara tillgänglig i den klassiska Intune-portalen. Du kan använda Intune-programvaruklienten till att hantera datorer med Windows 10 och senare, förutom Windows 10 Home Edition.

> [!Note]
> Microsoft tillkännagav att stöd för Windows 7 upphör den 14 januari 2020. På samma datum upphör även Intunes stöd för enheter med Windows 7.
>
> Mer information finns i [Intune-plan för förändring: Supporten för Windows 7 upphör](whats-new.md#windows-7-ends-extended-support).
>
> Microsoft Intune kommer att dra tillbaka supporten för den Silverlight-baserade Intune-konsolen den 15 oktober 2020. Den här indragningen omfattar slut support för Silverlight-konsolens konfigurerade PC-programklient (kallas även för PC-agent).
>
> Mer information finns i [Microsoft Intune avslutar supporten för den Silverlight-baserade administratörskonsolen](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Take-Action-Microsoft-Intune-ending-support-for-the-Silverlight/ba-p/916249).

<!--  ### Exchange ActiveSync management

You can manage [Exchange ActiveSync devices](../enrollment/device-enrollment.md#mobile-device-management-with-exchange-activesync-and-intune) from the Intune console. This option provides a limited set of management capabilities when compared to the other methods. See [Capabilities of built-in Mobile Device Management in Office 365](https://support.office.com/article/Capabilities-of-built-in-Mobile-Device-Management-for-Office-365-a1da44e5-7475-4992-be91-9ccec25905b0) for a list of supported devices.  -->

## <a name="intune-supported-web-browsers"></a>Webbläsare som stöds av Intune

Olika administrativa uppgifter som kräver att du använder en av följande administrativa webbplatser.

- [Administrationscenter för Microsoft 365](https://go.microsoft.com/fwlink/p/?LinkId=698854)
- [Azure Portal](https://portal.azure.com/)

Följande webbläsare stöds för dessa portaler:

- Microsoft Edge (senaste versionen)
- Microsoft Internet Explorer 11
- Safari (senaste versionen, endast Mac)
- Chrome (senaste versionen)
- Firefox (senaste versionen)

### <a name="intune-classic-portal"></a>Intunes klassiska portal

Den klassiska Intune-portalen används bara för att hantera enheter som registrerats med Intune PC-klienten (https://manage.microsoft.com) ). Den klassiska Intune-portalen kräver stöd för Silverlight-webbläsaren.

Följande Silverlight-webbläsare har stöd för Intune-konsolen:

- Internet Explorer 10 eller senare
- Google Chrome (versioner före version 42)
- Mozilla Firefox med Silverlight aktiverat (tidigare versioner än version 56)

> [!Note]
> Den klassiska Intune-portalen stöder inte Microsoft Edge och mobila webbläsare eftersom de inte stöder [Microsoft Silverlight](https://msdn.microsoft.com/library/cc838158(v=vs.95).aspx).

Endast användare med behörighet som tjänsteadministratör eller innehavaradministratören med den globala administratörsrollen kan logga in på den här portalen. Om du vill få åtkomst till administrationskonsolen måste kontot ha en licens för att använda Intune och inloggningsstatusen **Tillåten**.
