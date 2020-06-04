---
title: Begränsningar för Surface Hub Windows 10 Team-enheter i Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Använd Intune till att lägga till eller konfigurera inställningar för Surface Hub-enheter som kör Windows 10 Team.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b57bc0b7c76a6b67a26c7b1fdacb7880173a055c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429693"
---
# <a name="windows-10-team-settings-to-allow-or-restrict-features-on-surface-hub-devices-using-intune"></a>Windows 10 Team-inställningar för att tillåta eller begränsa funktioner på Surface Hub-enheter med hjälp av Intune

I den här artikeln går vi igenom de enhetsbegränsningar i Microsoft Intune du kan konfigurera för enheter som kör Windows 10 Team, inklusive Surface Hub-enheter.

## <a name="before-you-begin"></a>Innan du börjar

[Skapa enhetsprofilen](device-restrictions-configure.md#create-the-profile).

## <a name="apps-and-experience"></a>Appar och upplevelse

De här inställningarna använder [CSP:n SurfaceHub](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Aktivera skärmen när någon är i rummet**: **Blockera** förhindrar att skärmen aktiveras automatiskt när sensorn känner av att någon är i rummet. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Mötesinformation som visas på välkomstskärmen**: Välj vilken information som ska visas på panelen Möten på välkomstskärmen. Alternativen är:
  - **Inte konfigurerat** (standard): Intune varken ändrar eller uppdaterar den här inställningen.
  - **Endast kalender och tid**
  - **Kalender, tid och ämne (ämnet är dolt för privata möten)**
- **Webbadress till bakgrundsbild för välkomstskärm**: Ange webbadressen till en .png-bild du vill använda som anpassad bakgrund på **välkomstskärmen** på Windows 10 Team-enheter. Bilden måste vara i PNG-format och webbadressen måste börja med `https://`.
- **Starta appen Anslut automatiskt**: **Blockera** förhindrar att Connect-appen öppnas automatiskt när en projektion startas. Om funktionen blockeras kan användarna starta Connect-appen manuellt från hubbens inställningar. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Inloggningsförslag**: **Blockera** inaktiverar automatisk ifyllning av inloggningsrutan med inbjudna från schemalagda möten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Mina möten och filer**: **Blockera** inaktiverar funktionen **Mina möten och filer** på Start-menyn. Den här funktionen visar den inloggade användarens möten och filer från Office 365. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

## <a name="azure-operational-insights"></a>Azure Operational Insights

- **Azure Operational Insights**: **Aktivera** samlar in, lagrar och analyserar loggdata från Windows 10 Team-enheter med Azure Operational Insights. Azure Operational Insights ingår i programsviten Microsoft Operations Manager. Om du vill ansluta till Azure Operational Insights måste du ange ett **Arbetsyte-ID** och en **Arbetsytenyckel**.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen. Operativsystemet kanske som standard inte samlar in dessa data.

## <a name="maintenance"></a>Underhåll

De här inställningarna använder [CSP:n SurfaceHub](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Underhållsperiod för uppdateringar**: **Aktivera** skapar en underhållsperiod när uppdateringar kan installeras. Ange underhållsperiodens **Starttid** och **Varaktighet i timmar**, mellan 1–5 timmar.

  När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

## <a name="session"></a>Session

De här inställningarna använder [CSP:n SurfaceHub](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **Volym**: Ange standardvolymvärdet för en ny session, mellan 0–100. När värdet är tomt varken ändrar eller uppdaterar Intune den här inställningen. Operativsystemet kan som standard ange volymen som 45.
- **Skärmtidsgräns**: Ange antalet minuter innan hubbskärmen stängs av.
- **Tidsgräns för session**: Ange antalet minuter innan sessionen upphör.
- **Timeout för viloläge**: Ange antalet minuter innan hubben övergår i viloläge.
- **Återuppta session**: **Blockera** förhindrar att användare återupptar en session när tidsgränsen har uppnåtts. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.

## <a name="wireless-projection"></a>Trådlös projektion

De här inställningarna använder [CSP:n SurfaceHub](https://docs.microsoft.com/windows/client-management/mdm/surfacehub-csp).

- **PIN-kod för trådlös projektion**: **Kräv** tvingar användarna att ange en PIN-kod innan de använder funktionerna för trådlös projektion på enheten. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Trådlös Miracast-projektion**: **Blockera** förhindrar att Miracast-aktiverade enheter används för projektion. När detta anges till **Inte konfigurerad** (standard) ändrar eller uppdaterar Intune inte den här inställningen.
- **Kanal för trådlös Miracast-projektion**: Välj Miracast-kanal för att upprätta anslutningen.

## <a name="next-steps"></a>Nästa steg

Mer information finns i [Konfigurera inställningar för enhetsbegränsning](device-restrictions-configure.md).

[Tilldela profilen](device-profile-assign.md) och [övervaka dess status](device-profile-monitor.md).
