---
title: Konfigurera registrering för macOS-enheter
titleSuffix: Microsoft Intune
description: Läs om hur du konfigurerar registreringen av macOS-enheter i Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/12/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 46429114-2e26-4ba7-aa21-b2b1a5643e01
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1de1b015daad50837142ce9628543f0b2d7587d7
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093757"
---
# <a name="set-up-enrollment-for-macos-devices-in-intune"></a>Konfigurera registrering för macOS-enheter i Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

I Intune kan du hantera macOS-enheter för att ge användarna åtkomst till företagets e-post och appar.

Som Intune-administratör kan du ställa in registrering av företagsägda och egna macOS-enheter (”bring your own device” eller BYOD). 

## <a name="prerequisites"></a>Krav

Uppfyll följande krav innan du konfigurerar registreringen av macOS-enheter:

- [Kontrollera att enheten är kvalificerad för registrering av Apple-enheter](https://support.apple.com/en-us/HT204142#eligibility).
- [Konfigurera domäner](../fundamentals/custom-domain-name-configure.md)
- [Ange MDM-utfärdare](../fundamentals/mdm-authority-set.md)
- [Skapa grupper](../fundamentals/groups-add.md)
- [Konfigurera företagsportalen](../apps/company-portal-app.md)
- Tilldela användarlicenser i [Administrationscenter för Microsoft 365](https://go.microsoft.com/fwlink/p/?LinkId=698854)
- [Hämta ett Apple MDM-pushcertifikat](../enrollment/apple-mdm-push-certificate-get.md)

## <a name="user-owned-macos-devices-byod"></a>Användarägda macOS-enheter (BYOD)

Du kan låta användarna registrera sina egna personliga enheter i Intune-hanteringen. Detta kallas ”Bring Your Own Device” eller BYOD. När du har uppfyllt förutsättningarna och tilldelat användarlicenser kan användarna registrera sina enheter genom att göra följande:
- gå till [webbplatsen för företagsportalen](https://portal.manage.microsoft.com) eller
- ladda ned företagsportalappen för Mac från [aka.ms/EnrollMyMac](https://aka.ms/EnrollMyMac).

Du kan även skicka dem en länk med anvisningar för registrering online: [Registrera din macOS-enhet i Intune](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp).

Information om andra slutanvändaraktiviteter finns i de här artiklarna:

- [Resurser om slutanvändarupplevelsen med Microsoft Intune](../fundamentals/end-user-educate.md)
- [Använd din macOS-enhet med Intune](../user-help/enroll-your-device-in-intune-macos-cp.md)

## <a name="company-owned-macos-devices"></a>Företagsägda macOS-enheter
Intune har stöd för följande registreringsmetoder för macOS-enheter som ägs av företaget, i organisationer som köper enheter till sina användare:
- [Automatisk enhetsregistrering för Apple (ADE)](device-enrollment-program-enroll-macos.md): Organisationer kan köpa macOS-enheter via ADE. Med ADE kan du distribuera en registreringsprofil ”over-the-air” för att hantera enheter.
- [Enhetsregistreringshanteraren (DEM)](device-enrollment-manager-enroll.md): Du kan använda ett DEM-konto till att registrera upp till 1 000 enheter.

## <a name="block-macos-enrollment"></a>Blockera macOS-registrering
Som standard kan macOS-enheter registreras i Intune. Se [Ange begränsningar för enhetstyp](enrollment-restrictions-set.md) för att blockera macOS-enheter från registrering.

## <a name="enroll-virtual-macos-machines-for-testing"></a>Registrera virtuella macOS-datorer för testning

> [!NOTE]
> Virtuella macOS-datorer stöds endast för testning. Du bör inte använda virtuella macOS-datorer som produktionsenheter för dina slutanvändare. 

Du kan registrera virtuella macOS-datorer för testning med antingen Parallels Desktop eller VMware Fusion. 

För Parallels Desktop måste du ange maskinvarutyp och serienummer för de virtuella datorerna så att Intune kan identifiera dem. Följ Parallels anvisningar för inställning av maskinvarutyp och [serienummer](http://kb.parallels.com/123455) och ange de nödvändiga inställningarna för testning. Vi rekommenderar att du matchar maskinvarutypen på enheten som kör de virtuella datorerna med maskinvarutypen för de virtuella datorer som du skapar. Du hittar den här maskinvarutypen i **Apple-menyn** > **Om denna Mac** > **Systemrapport** > **Modellidentifierare**. 

För VMware Fusion behöver du [redigera .vmx-filen](https://kb.vmware.com/s/article/1014782) och ange maskinvarumodell samt serienummer för den virtuella datorn. Vi rekommenderar att du matchar maskinvarutypen på enheten som kör de virtuella datorerna med maskinvarutypen för de virtuella datorer som du skapar. Du hittar den här maskinvarutypen i **Apple-menyn** > **Om denna Mac** > **Systemrapport** > **Modellidentifierare**. 

## <a name="user-approved-enrollment"></a>Registrering av användargodkänd

MDM-registrering av användargodkänd är en typ av macOS-registrering som du kan använda för att hantera vissa känsliga inställningar. Mer information finns i [Apples supportdokumentation](https://support.apple.com/HT208019).  
 
Från och med juni 2020 betraktas alla nya macOS MDM-registreringar i Intune, inklusive de som inte görs via automatisk enhetsregistrering (ADE), som godkända av användaren. Slutanvändaren måste installera hanteringsprofilen manuellt i **Systeminställningar** > **Profiler** och därmed godkänna hanteringsprofilen. Systeminställningar startas automatiskt från Företagsportal-appen för användare med egna macOS-enheter. [Instruktioner för att installera hanteringsprofilen](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp) finns i företagsportalappen.     

MDM-registreringar för egna macOS-enheter innan juni 2020 kanske inte betraktas som godkända av användaren om inte slutanvändaren har godkänt hanteringsprofilen manuellt i **Systeminställningar** > **Profiler**. För registreringar av egna enheter efter juni 2020 startar företagsportalappen **Systeminställningar** åt användaren och användaren måste välja Installera. Om användaren inte godkänner hanteringsprofilen under registreringen kan användaren gå till **Systeminställningar** > **Profiler**, välja hanteringsprofilen och välja **Godkänn** för att godkänna profilen senare.

### <a name="find-out-if-a-device-is-user-approved"></a>Ta reda på om en enhet är användargodkänd
1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Alla enheter** > välj enheten > **Maskinvara**.
3. Markera fältet för **användargodkänd registrering**.


## <a name="next-steps"></a>Nästa steg

När macOS-enheter registreras kan du [skapa anpassade inställningar för enheterna](../configuration/custom-settings-macos.md).
