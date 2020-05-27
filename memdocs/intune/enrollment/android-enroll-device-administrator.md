---
title: Administratörsregistrering för Android-enhet i Microsoft Intune
titleSuffix: ''
description: Registrera Android-enheter i Intune med hjälp av enhetsadministratörsregistrering.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/23/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5200f0476e3f692b02cbac9b0934c35e522ee906
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983626"
---
# <a name="android-device-administrator-enrollment"></a>Administratörsregistrering för Android-enhet

Android-enhetsadministratören (kallas ibland för ”äldre” Android-hantering och lanserades med Android 2.2) är ett sätt att hantera Android-enheter. Det finns dock en bättre hanteringsfunktion med [Android Enterprise](https://www.android.com/enterprise/management/) (lanseras med Android 5.0). För att kunna flytta till en modern, mer omfattande och säkrare enhetshantering,minskar Google stödet för enhetsadministration i nya versioner av Android.

För att undvika försämrad funktion avråder vi därför från att registrera nya enheter med enhetsadministratörsprocessen som beskrivs nedan.

Av samma skäl rekommenderar vi också att du migrerar enheter från enhetsadministratörshantering om enheterna ska uppdateras till Android 10. 

Fortsätt till nästa avsnitt om du fortfarande vill att användarna ska registrera sina Android-enheter med enhetsadministratörshantering.  

Mer information om Googles Android Enterprise-funktioner finns i följande artiklar:
- [Googles vägledning för migrering från enhetsadministratören till Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Googles dokumentation om tillbakadragningen av API:et för enhetsadministratören](https://developers.google.com/android/work/device-admin-deprecation)

## <a name="set-up-device-administrator-enrollment"></a>Ställ in administratörsregistrering

1. Förbered hantering av mobila enheter genom att ange MDM-utfärdare som **Microsoft Intune**. Fler anvisningar finns i [Ange MDM-utfärdare](../fundamentals/mdm-authority-set.md). Du anger det här objektet bara när du konfigurerar Intune för hantering av mobila enheter.
2. Logga in på [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) och välj > **Enheter** > **Android** > **Android-registrering** > **Personliga och företagsägda enheter med enhetsadministratörsbehörigheter** > **Använd enhetsadministratör för att hantera enheter**.
3. [Berätta för dina användare hur de registrerar sina enheter](../user-help/enroll-device-android-company-portal.md).  

När en användare har registrerat sig kan du börja hantera användarens enheter i Intune, inklusive [tilldela efterlevnadsprinciper](../protect/compliance-policy-create-android.md), [hantera appar](../apps/app-management.md) med mera.

Information om andra användaraktiviteter finns i de här artiklarna:
- [Resurser om slutanvändarens upplevelse med Microsoft Intune](../fundamentals/end-user-educate.md)
- [Använda en Android-enhet med Intune](https://docs.microsoft.com/mem/intune/user-help/why-enroll-android-device)


## <a name="block-device-administrator-enrollment"></a>Blockera administratörsregistrering
Se [Ange begränsningar för enhetstyp](enrollment-restrictions-set.md) för att blockera Android-enheter eller endast blockera personligt ägda Android-enheter från registrering.


## <a name="next-steps"></a>Nästa steg
- [Efterlevnadsprinciper för enheter](../protect/compliance-policy-create-android.md)
- [Hantera appar](../apps/app-management.md)
