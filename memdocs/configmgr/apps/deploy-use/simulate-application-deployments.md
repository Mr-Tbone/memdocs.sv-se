---
title: Simulera programdistributioner
titleSuffix: Configuration Manager
description: Utvärdera identifierings metoden, kraven och beroenden för en distributions typ utan att installera programmet.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bed491b4800dd6ae8b53a837618abf3d8a5a597d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710596"
---
# <a name="simulate-application-deployments-with-configuration-manager"></a>Simulera program distributioner med Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Du kan använda simulerade distributioner för att testa en program distribution utan att installera eller avinstallera programmet. En simulerad distribution utvärderar identifierings metoden, kraven och beroenden för en distributions typ. Den rapporterar resultatet i noden **distributioner** på arbets ytan **övervakning** . Använd proceduren i det här avsnittet för att simulera en program distribution i Configuration Manager.  

> [!NOTE]  
> Det går inte att simulera distributioner för samlingar av mobila enheter.  
>   
> Det går inte att distribuera ett program med distributionssyftet **Avinstallera** om det finns en aktiv simulerad distribution för samma program.  

## <a name="configure-a-simulated-application-deployment"></a>Konfigurera en simulerad program distribution

1.  I Configuration Manager-konsolen väljer du något av följande:  
    -   En samling av användare.  
    -   En samling av enheter.  
    -   Ett Configuration Manager-program.  

2.  På fliken **Start** går du till gruppen **distribution** och väljer **simulera distribution**.  

3.  Ange följande information för den simulerade distributionen i guiden simulera program distribution:  

    -   **Programmet**. Välj **Bläddra**och välj sedan det program som du vill skapa en simulerad distribution för.  

    -   **Samling**. Välj **Bläddra**och välj sedan den samling som du vill använda för den simulerade distributionen.  

    -   **Åtgärd**. I list rutan väljer du om du vill simulera installationen eller avinstallationen av det valda programmet.  

    -   **Distribuera automatiskt med eller utan användar inloggning**. Om det här alternativet är markerat utvärderar klienterna den simulerade distributionen oavsett om klienterna är inloggade eller inte.  

4.  Klicka på **Nästa**, granska informationen på sidan **Sammanfattning** och slutför sedan guiden för att skapa den simulerade program distributionen.  

5.  Simulerade program visas i noden **distributioner** på arbets ytan **övervakning** med syftet **simulera**. Mer information om hur du övervakar program distributioner finns i [övervaka program från Configuration Manager-konsolen](../../apps/deploy-use/monitor-applications-from-the-console.md).  
