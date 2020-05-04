---
title: Dela program i Software Center
titleSuffix: Configuration Manager
description: Dela en länk till ett program i Software Center i Configuration Manager.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be2e930e3f59bc5a4d7db9e27ce2f875814fd358
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710078"
---
# <a name="share-an-application-from-software-center"></a>Dela ett program från Software Center

*Gäller för: Configuration Manager (aktuell gren)* <!-- 1706 -->

Du kan kopiera en hyperlänk till ett program i Software Center med hjälp ![av](media/share15.png)knappen dela**delning** i vyn programinformation.   Du kan bara dela hyperlänkar för program. Om programmet blir otillgängligt öppnar hyperlänken ett fönster med ett meddelande om att programmet inte är tillgängligt.

1. Välj **program**och välj sedan programmet.
2. Klicka på ![knappen](media/share15.png) dela **resurs** .
3. Klicka på **Kopiera** i fönstret.
4. Klistra in webb adressen i ett e-postmeddelande för att dela programmet.  

> [!TIP]  
>  Om du vill skapa en länk i ett Outlook-e-postmeddelande trycker du på **CTRL** + **K** och klistrar in URL: en.  
>  
> Som standard visar Outlook en säkerhets varning för Software Center-protokollet när mottagaren klickar på länken. Förhindra detta i din miljö genom att lägga till en betrodd protokoll nyckel i registret. Till exempel, `HKCU\Software\Policies\Microsoft\Office\16.0\Common\Security\Trusted Protocols\All Applications\softwarecenter:`  
