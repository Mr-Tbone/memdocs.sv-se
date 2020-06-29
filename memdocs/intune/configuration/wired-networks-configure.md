---
title: Konfigurera inställningar för kabelanslutna 802.1x-nätverk för macOS-enheter i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Skapa eller lägg till en konfigurationsprofil för en kabelansluten nätverksenhet för stationära macOS-datorer. Se de olika inställningarna, lägg till certifikat, välj en EAP-typ och välj en autentiseringsmetod i Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f237daa5e95cb5428e707828f0104c697e338718
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85095802"
---
# <a name="add-and-use-wired-networks-settings-on-your-macos-devices-in-microsoft-intune"></a>Lägga till och använda inställningar för kabelanslutna nätverk på macOS-enheter i Microsoft Intune

Många organisationer använder kabelanslutna nätverk till att ge nätverksåtkomst åt stationära datorer. Microsoft Intune har inbyggda inställningar som kan distribueras till användare och macOS-enheter i din organisation. Den här gruppen med inställningar kallas för en ”profil”. Du kan ta med vanliga inställningar i din profil, som nätverksgränssnitt, godkända EAP-typer och inställningar för betrodda servrar.

När profilen är klar kan du tilldela den till olika användare och grupper. När profilen har tilldelats får användare tillgång till organisationens kabelanslutna nätverk utan att de behöver konfigurera något själva.

Använd den här funktionen till att skapa 802.1 x-profiler för hantering av kabelanslutna nätverk inom ramen för din MDM-lösning. Distribuera sedan de kabelanslutna nätverken till dina macOS-enheter.

Den här funktionen gäller för:

- macOS

Du kan till exempel ha ett kabelanslutet nätverk med namnet **Contoso kabelanslutet nätverk**. Du vill att alla stationära macOS-enheter ska ansluta till det här nätverket. Så här ser processen ut:

1. Skapa en profil för ett kabelanslutet nätverk med inställningar som ansluter till **Contoso kabelanslutet nätverk**.
2. Tilldela profilen till en grupp som innehåller alla användare av stationära macOS-datorer. Du kan läsa mer om att använda grupptyper i [Användargrupper kontra enhetsgrupper](device-profile-assign.md#user-groups-vs-device-groups).
3. Användarna ser **Contoso kabelanslutet nätverk** i listan med nätverk i datorn. De kan sedan ansluta till nätverket med hjälp av den autentiseringsmetod som du har valt.

I den här artikeln går vi igenom stegen för att skapa en profil för ett kabelanslutet nätverk. Den innehåller också en länk som beskriver de olika inställningarna.

## <a name="create-the-profile"></a>Skapa profilen

1. Logga in till [administrationscentret för Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Välj **Enheter** > **Konfigurationsprofiler** > **Skapa profil**.
3. Ange följande egenskaper:

    - **Plattform**: Välj **macOS**.
    - **Profil**: Välj **Kabelanslutet nätverk**.

4. Välj **Skapa**.
5. Ange följande egenskaper i **Grundinställningar**:

    - **Namn**: Ange ett beskrivande namn på profilen. Namnge dina profiler så att du enkelt kan identifiera dem senare. Ett bra profilnamn är exempelvis **Profil för kabelanslutet nätverk för alla macOS-enheter på hela företaget**.
    - **Beskrivning**: Ange en beskrivning av profilen. Denna inställning är valfri, men rekommenderas.

6. Välj **Nästa**.
7. I **Konfigurationsinställningar** väljer du nätverkets nätverksgränssnitt och EAP-typ (Extensible Authentication Protocol). En lista med alla inställningar och vad de gör finns i:

    - [macOS](wired-network-settings-macos.md)

8. Välj **Nästa**.
9. Under **Tilldelningar** väljer du de användargrupper eller enhetsgrupper som ska få profilen. Mer information om hur du tilldelar profiler finns i [Tilldela användar- och enhetsprofiler](device-profile-assign.md).

    Välj **Nästa**.

10. Granska inställningarna under **Granska + skapa**. När du väljer **Skapa** sparas dina ändringar och profilen tilldelas. Principen visas också i profillistan.

> [!TIP]
> Om du använder certifikatbaserad autentisering i profilen för kabelanslutna nätverk ska du distribuera nätverksprofilen, certifikatprofilen och profilen för betrodd rot till samma grupper. Den här distributionen gör att alla enheter kan identifiera certifikatutfärdarens legitimitet. Mer information finns i [Konfigurera certifikat med Microsoft Intune](../protect/certificates-configure.md).

## <a name="next-steps"></a>Nästa steg

Profilen skapas, men den kanske inte gör någonting. Se till att du [tilldelar profilen](device-profile-assign.md) och [övervakar](device-profile-monitor.md) dess status.
