---
title: Ändra namn på en enhet med Microsoft Intune – Azure | Microsoft Docs
description: Byt namn på en enhet med hjälp av Microsoft Intune.
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
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4ff0e650a3eccf057158d3faf28875e42ed90a4d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80325031"
---
# <a name="rename-a-device-in-intune"></a>Ändra namn på en enhet i Intune

Med åtgärden **Byt namn på enhet** kan du byta namn på en enhet som har registrerats i Intune. Enhetens namn ändras i Intune och på enheten.

Du kan byta namn på följande enhetstyper:
- företagsägda Windows-enheter 
- Övervakat iOS/iPadOS
- företagsägda MacOS 10-enheter

Den här funktionen stöder för närvarande inte namnbyte av Windows-hybridenheter för Azure AD.

## <a name="rename-a-device"></a>Byta namn på en enhet

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Välj **Enheter** > **Alla enheter** > välj en enhet > **...**  > **Byt namn på enhet**.
4. På bladet **Byt namn på enhet** skriver du det nya namnet i textrutan. Du kan använda bokstäver, siffror och bindestreck. Namnet måste innehålla minst en bokstav eller bindestreck.
5. Om du vill starta om enheten efter namnbytet väljer du **Ja** bredvid **Starta om efter namnbyte**.
6. Välj **Byt namn**.

## <a name="windows-device-rename-rules"></a>Regler för byte av Windows-enhetsnamn
När du byter namn på en Windows-enhet måste det nya namnet följa dessa regler:
- 15 tecken eller mindre (måste vara mindre än eller lika med 63 byte exklusive avslutande NULL)
- Inte null eller en tom sträng
- Tillåten ASCII: bokstäver (a-z, A-Z), siffror (0-9) och bindestreck
- Tillåten Unicode: tecken > = 0x80, måste vara en giltig UTF8, måste vara IDN-mappningsbara (det vill säga att RtlIdnToNameprepUnicode lyckas; se RFC 3492)
- Namn får inte enbart innehålla siffror
- Inga blanksteg i namnet
- Förbjudna tecken: { | } ~ [ \ ] ^ ' : ; < = > ? & @ ! " # $ % ` ( ) + / , . _ *)


## <a name="next-steps"></a>Nästa steg

För att se status för enhetsåtgärden **Byt namn** kontrollerar du sidan **Översikt** för enheten.
