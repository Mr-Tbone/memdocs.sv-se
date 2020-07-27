---
title: Lägg till företagsportalen för macOS-appar
titleSuffix: Microsoft Intune
description: Lägg till företagsportalsappen för macOS.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/16/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a58e22af70a3cf119cb044a15b40ba581fe6452c
ms.sourcegitcommit: 5c15b59cde085787b85f032f88add70a11d8e9a2
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452858"
---
# <a name="add-the-macos-company-portal-app"></a>Lägg till företagsportalsappen för macOS

Om du vill hantera enheter, installera valfria appar och få åtkomst till resurser som skyddas av villkorsstyrd åtkomst på macOS-enheter med användartillhörighet, måste användarna installera företagsportalsappen och logga in på den. Du kan ge instruktioner till användarna om att installera företagsportalen för macOS, eller installera den på enheter som redan har registrerats direkt från Intune.

Du kan använda något av följande alternativ när du installerar företagsportalen för macOS-appen:
- [Be användarna ladda ned och installera företagsportalen](#instruct-users-to-download-and-install-company-portal)
- [Installera företagsportalen för macOS som en verksamhetsspecifik macOS-app](#install-company-portal-for-macos-as-a-macos-lob-app)
- [Installera företagsportalen för macOS med hjälp av ett macOS-kommandoskript](#install-company-portal-for-macos-by-using-a-macos-shell-script)

För att apparna ska vara skyddade och uppdaterade när de har installerats, levereras företagsportalsappen med Microsoft AutoUpdate (MAU).

> [!NOTE]
> Företagsportalsappen kan bara installeras automatiskt på enheter som använder Intune och som redan har registrerats med hjälp av direktregistrering eller automatisk enhetsregistrering. För personliga enheter eller vid manuell registrering måste företagsportalsappen laddas ned och installeras för att initiera registreringen. Se [Be användarna ladda ned och installera företagsportalen](#instruct-users-to-download-and-install-company-portal).
## <a name="instruct-users-to-download-and-install-company-portal"></a>Be användarna ladda ned och installera företagsportalen

Du kan be användarna ladda ned, installera och logga in på företagsportalen för macOS. Anvisningar om att ladda ned, installera och logga in på företagsportalen finns i [Registrera din macOS-enhet med företagsportalappen](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp).

##  <a name="install-company-portal-for-macos-as-a-macos-lob-app"></a>Installera företagsportalen för macOS som en verksamhetsspecifik macOS-app

Företagsportalen för macOS kan laddas ned och installeras med hjälp av funktionen [Verksamhetsspecifika macOS-appar](lob-apps-macos.md). Den version som laddas ned är den version som alltid kommer att installeras. Den kan behöva uppdateras regelbundet för att säkerställa att användarna får bästa möjliga upplevelse under den första registreringen.

1. Lägg till företagsportalappen för macOS från https://go.microsoft.com/fwlink/?linkid=853070. 

2. Följ instruktionerna för att skapa en verksamhetsspecifik macOS-app i [Verksamhetsspecifika macOS-appar](lob-apps-macos.md).

> [!NOTE]
> När du har installerat företagsportalen för macOS, kommer appen att uppdateras automatiskt med Microsoft AutoUpdate (MAU).
## <a name="install-company-portal-for-macos-by-using-a-macos-shell-script"></a>Installera företagsportalen för macOS med ett macOS-kommandoskript

Företagsportalen för macOS kan laddas ned och installeras med hjälp av funktionen [macOS-kommandoskript](macos-shell-scripts.md). Med det här alternativet installeras alltid den aktuella företagsportalsversionen för macOS. Du får dock inte den programinstallationsrapportering som du kanske är van vid när du distribuerar program med [verksamhetsspecifika macOS-appar](lob-apps-macos.md).

1. Ladda ned ett skriptexempel med installation av företagsportalen för macOS från [Exempel på Intune-kommandoskript – Företagsportal](https://github.com/microsoft/shell-intune-samples/tree/master/Apps/Company%20Portal).

2. Följ anvisningarna för att distribuera macOS-kommandoskriptet med hjälp av [macOS-kommandoskript](macos-shell-scripts.md). 
    - Ange **Köra skript som inloggad användare** till **Nej** (för att köra i systemkontexten).
    - Ange **Maximalt antal nya försök om skriptet misslyckas** till **3**.

> [!NOTE]
> Skriptet kräver Internetåtkomst när det körs, för kunna ladda ned den aktuella versionen av företagsportalen för macOS. 
## <a name="next-steps"></a>Nästa steg
- Mer information om hur du tilldelar appar finns i [Tilldela appar till grupper](apps-deploy.md).
- Mer information om att konfigurera automatisk enhetsregistrering finns i [Programmet för enhetsregistrering – Registrera macOS](https://docs.microsoft.com/mem/intune/enrollment/device-enrollment-program-enroll-macos).
- Mer information om att konfigurera inställningar för Microsoft AutoUpdate på macOS finns i [Mac-uppdateringar](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/mac-updates).