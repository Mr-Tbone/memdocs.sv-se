---
title: Så här återställer du ditt konto
titleSuffix: Configuration Manager
description: Lär dig hur du återställer ditt Skriv bords analys konto.
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 884d4864-950b-4139-b778-d5368e1f6ef2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ece2d2725b8485f55fdce7761098577485bc2d1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722496"
---
# <a name="how-to-reset-your-account"></a>Så här återställer du ditt konto

<!-- 3733897 -->

Om du konfigurerar Desktop Analytics i din miljö, men vill börja om med onboarding och registrering, använder du den här processen för att återställa ditt konto.

## <a name="prerequisites"></a>Krav

Endast en **Global administratör** kan återställa kontot i Azure Portal.

## <a name="behaviors"></a>Funktions

- Den här processen ändrar inte några befintliga Azure AD-användare, appar eller behörigheter

- Om du väljer att lägga till en ny arbets yta behålls ingen av följande användar indata på till gångar:
    - Betydelse
    - Ägare
    - Uppgraderings beslut
    - Reparations anteckningar

## <a name="process"></a>Process

1. Öppna [Skriv bords analys portalen](https://aka.ms/desktopanalytics) i Microsoft 365 enhets hantering som en användare med rollen **Global administratör** .

1. I menyn **globala inställningar** väljer du **anslutna tjänster**. I avsnittet registrera enheter väljer du alternativet för att **återställa**.

1. Om du väljer att fortsätta återställs ditt konto. Du måste konfigurera Desktop Analytics igen.

## <a name="next-steps"></a>Nästa steg

När du har återställt uppdaterar du sidan och kör onboarding-processen igen. Mer information finns i [så här konfigurerar du Skriv bords analys](set-up.md).

Om du har problem under den här processen kan du kontakta Microsoft Support för ytterligare hjälp.
