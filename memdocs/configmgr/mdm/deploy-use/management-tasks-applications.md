---
title: Hantera appar för lokal MDM
titleSuffix: Configuration Manager
description: Hantera program för lokal hantering av mobila enheter (MDM) i Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9fafcc4b5462afb1b8e528837ea6ba61203e73d
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347158"
---
# <a name="manage-apps-for-on-premises-mdm-in-configuration-manager"></a>Hantera appar för lokal MDM i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

När du hanterar enheter med Configuration Manager lokal hantering av mobila enheter (MDM) kan du hantera följande program typer:

- Windows Phone-appaket (*.xap-fil)
- Windows Phone-appaket (i Windows Phone Store)
- Windows Installer via MDM
- Webbprogram

Mer allmän information om hur du hanterar Configuration Manager program och distributions typer finns i [hanterings aktiviteter för Configuration Manager program](../../apps/deploy-use/management-tasks-applications.md).

## <a name="create-windows-phone-application"></a><a name="bkmk_winphone"></a>Skapa Windows Phone program

Ett Configuration Manager program har en eller flera distributions typer. Distributions typen innehåller de installationsfiler och den information som krävs för att distribuera program vara till en enhet. En distributions typ har också regler som anger när och hur program varan distribueras.

De allmänna stegen för att skapa en app och distributions typer finns i [skapa ett program](../../apps/deploy-use/create-applications.md#bkmk_create).

Configuration Manager stöder följande typer av AppData för Windows Mobile-enheter:

|Enhetstyp|Filtyper som stöds|
|-----------------|---------------------|
|Windows Phone 8|XAP|
|Windows Phone 8.1|XAP, appx, appxbundle|
|Windows 10 Mobil|XAP, appx, appxbundle|

Distribuera Windows Phone appar som **tillgängliga** eller **obligatoriska**. Du kan också använda distributioner för att avinstallera appar.

## <a name="deploy-and-monitor-apps"></a>Distribuera och övervaka appar

Distribuera och övervaka program för mobila enheter i Configuration Manager samma som du gör för andra enheter, till exempel Station ära datorer och servrar. Mer information finns i följande artiklar:

- [Distribuera program](../../apps/deploy-use/deploy-applications.md)
- [Övervakning av program](../../apps/deploy-use/monitor-applications-from-the-console.md)

Granska följande begränsningar som är begränsade till mobila enheter:

- MDM-registrerade enheter stöder inte simulerade distributioner, användar upplevelser eller schemaläggnings inställningar.

- Lägg inte till fler än 100 språk i en enda app. Den här åtgärden förhindrar att appen installeras på enheten.

## <a name="next-step"></a>Nästa steg

Om du vill göra ändringar, avinstallera eller ersätta ett distribuerat program med ett nytt program hanterar du det på samma sätt som en app i Configuration Manager. Mer information finns i [ändra och ersätta program](../../apps/deploy-use/revise-and-supersede-applications.md).
