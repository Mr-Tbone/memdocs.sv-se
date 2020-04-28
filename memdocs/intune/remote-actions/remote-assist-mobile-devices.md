---
title: Fjärrassistera mobila enheter som hanteras med Intune
description: Du kan välja bland fyra olika alternativ när det gäller att fjärrassistera användarna med sina mobila enheter.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
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
ms.openlocfilehash: 548f63dcbd1635c106573fda40f8cc7bf312866e
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086656"
---
# <a name="remotely-assist-mobile-devices-managed-by-microsoft-endpoint-manager"></a>Fjärrassistera mobila enheter som hanteras av Microsoft Endpoint Manager

Det finns fyra tillgängliga alternativ för att fjärradministrera enheter som hanteras av Microsoft Endpoint Manager:

- [Microsoft Teams](https://products.office.com/microsoft-teams/) är navet där du kan chatta, mötas och samarbeta oavsett var du befinner dig.
- [Snabbhjälp](https://support.microsoft.com/help/4027243/windows-10-solve-pc-problems-with-quick-assist) är ett Windows 10-program som låter två personer dela en enhet via en fjärranslutning.
- [TeamViewer](https://www.teamviewer.com/) är ett tredjepartsprogram som du köper separat. Det ger en omfattande uppsättning funktioner för fjärråtkomst och support. Intune-och [TeamViewer-integrering](teamviewer-support.md) möjliggör fjärrsupport med TeamViewer, och anslutningsappen hanteras direkt i Intune.
- [Fjärrkontroll](https://docs.microsoft.com/configmgr/core/clients/manage/remote-control/introduction-to-remote-control) ingår i Microsoft Endpoint Configuration Manager. Den används för att fjärradministrera, ge hjälp eller visa vilka arbetsgruppsdatorer eller domänanslutna datorer som helst.

| Funktioner, plattformar, licensiering | **Teams** | Snabbhjälp | TeamViewer (Intune) | Fjärrstyrning (ConfigMgr) |
|:---:|:---:|:---:|:---:|:---:|
| Fjärrvy och kontroll |![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Chatt |![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)||![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Filöverföring |![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Förhöjd administratörsåtkomst |||![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Oövervakad åtkomst |||![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Samtidig fjärrstyrning |![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Stöd för flera användare |||![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Fjärråtgärder ||![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Support via Internet |![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Granskningsrapportering |![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)||![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Stöd för alla plattformar (Windows, iOS, Android, macOS) |![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)||![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Integrerad med Windows 10 – ingen ytterligare app krävs ||![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Kräver att enheten samhanteras av Configuration Manager och Intune ||||![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Kräver ytterligare licensiering\* |![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)||![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|![Markering](../enrollment/media/enrollment-method-capab/checkmark.png)|

\* Teams kräver O365- eller M365-licensiering. Användning av TeamViewer och Intune kräver licensiering från både TeamViewer och Intune. Fjärrstyrning är en funktion i Configuration Manager och kräver Configuration Manager-licensiering.