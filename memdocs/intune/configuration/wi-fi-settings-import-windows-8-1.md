---
title: Importera Wi-Fi-inställningar för Windows-enheter i Microsoft Intune – Azure | Microsoft Docs
description: Exportera Wi-Fi-inställningar från en Windows-enhet som en XML-fil med hjälp av netsh wlan. Sedan importerar du den här filen i Intune för att skapa en Wi-Fi-profil för enheter som kör Windows 8.1, Windows 10 och Windows Holographic for Business.
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
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d17614424cdb20d2d88d818fcdd015c229150d66
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556344"
---
# <a name="import-wi-fi-settings-for-windows-devices-in-intune"></a>Importera Wi-Fi-inställningar för Windows-enheter i Intune

För enheter som kör Windows kan du importera en Wi-Fi-konfigurationsprofil som tidigare exporterats till en fil. **För Windows 10 och senare enheter kan du även [skapa en Wi-Fi-profil](wi-fi-settings-windows.md) direkt i Intune**.

Den här funktionen gäller för:

- Windows 8.1 och senare
- Windows 10 och senare
- Windows 10 Desktop eller Mobile
- Windows 10 Holographic for Business

## <a name="before-you-begin"></a>Innan du börjar

[Skapa en enhetsprofil](wi-fi-settings-configure.md). Profilnamnet **måste** vara samma namn som namnattributet i den trådlösa nätverksprofilens xml-fil. Annars misslyckas det.

## <a name="import-the-wi-fi-settings-into-intune"></a>Importera trådlösa inställningar till Intune

- **Anslutningens namn**: Ange ett namn på Wi-Fi-anslutningen. Det här namnet visas för användarna när de bläddrar bland tillgängliga trådlösa nätverk.
- **Profil-XML**: Använd bläddringsknappen och välj XML-filen som innehåller de Wi-Fi-profilinställningar som du vill importera.
- **Filinnehåll**: Visar XML-koden för den konfigurationsprofil du har valt.

## <a name="export-wi-fi-settings-from-a-windows-device"></a>Exportera trådlösa inställningar från en Windows-enhet

I Windows kan du använda `netsh wlan` för att exportera en befintlig Wi-Fi-profil till en XML-fil som kan läsas av Intune. Nyckeln måste exporteras i oformaterad text för att profilen ska kunna användas.

På en Windows-dator som redan har rätt WiFi-profil installerad, gör du följande:

1. Skapa en lokal mapp för de exporterade trådlösa profilerna, till exempel **c:\WiFi**.
2. Öppna en kommandotolk som administratör.
3. Kör kommandot `netsh wlan show profiles`. Anteckna namnet på den profil som du vill exportera. I det här exemplet är profilnamnet **WiFiName**.
4. Kör kommandot `netsh wlan export profile name="ProfileName" folder=c:\Wifi`. Detta kommando skapar en fil för Wi-Fi-profilen med namnet **Wi-Fi-WiFiName.xml** i målmappen.

> [!IMPORTANT]
>
> - Om du exporterar en profil för trådlöst nätverk som innehåller en i förväg delad nyckel, **måste** du lägga till `key=clear` i kommandot. Ange till exempel:
>
>   `netsh wlan export profile name="ProfileName" key=clear folder=c:\Wifi`
>
> - En i förväg delad nyckel med Windows 10 visar ett reparationsfel i Intune. När detta sker tilldelas den trådlösa nätverksprofilen till enheten och profilen fungerar som förväntat.
> - Om du exporterar en trådlös nätverksprofil som innehåller en i förväg delad nyckel, måste filen vara skyddad. Nyckeln är i oformaterad text, så det är ditt ansvar att skydda den.

## <a name="next-steps"></a>Nästa steg

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).

Se [Översikt över Wi-Fi-inställningar](wi-fi-settings-configure.md), inklusive andra tillgängliga plattformar.
