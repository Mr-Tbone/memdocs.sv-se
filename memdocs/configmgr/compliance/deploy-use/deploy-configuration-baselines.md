---
title: Distribuera konfigurationsbaslinjer
titleSuffix: Configuration Manager
description: Distribuera konfigurations bas linjer för att definiera distributioner av konfigurations bas linjer och lägga till eller ta bort konfigurations bas linjer från distributioner.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9be8aaf3-075e-4acd-abd2-7459254e16e2
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 55b559f9b16eabfe2c2096497e6f63816b400803
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712339"
---
# <a name="how-to-deploy-configuration-baselines-in-configuration-manager"></a>Så här distribuerar du konfigurations bas linjer i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Konfigurations bas linjer i Configuration Manager måste distribueras till en eller flera samlingar av användare eller enheter innan klient enheter i dessa samlingar kan bedöma kompatibiliteten med konfigurations bas linjen.  

Använd dialogrutan **Distribuera konfigurationsbaslinjer** för att definiera distributioner av konfigurationsbaslinjer, det vill säga lägga till och ta bort konfigurationsbaslinjer i distributioner samt göra upp ett utvärderingsschema.  

## <a name="deploy-a-configuration-baseline"></a>Distribuera en konfigurationsbaslinje  

1.  I Configuration Manager-konsolen klickar du på **till gångar och efterlevnad** > **Compliance Settings** > kompatibilitetsinställningar**konfigurations bas linjer**.  

3.  I listan **Konfigurationsbaslinjer** väljer du den konfigurationsbaslinje du vill distribuera. Gå sedan till fliken **Start** . I gruppen **Distribution** klickar du på **Distribuera**.  

4.  I dialogrutan **Distribuera konfigurationsbaslinjer** väljer du den konfigurationsbaslinje du vill distribuera i listan **Tillgängliga konfigurationsbaslinjer** . Klicka på **Lägg till** för att lägga till dem i listan **Markerade konfigurationsbaslinjer** .  

    > [!IMPORTANT]  
    >  Om du ändrar ett konfigurationsobjekt som har lagts till i en distribuerad konfigurationsbaslinje, utvärderas inte kompatibiliteten för det ändrade konfigurationsobjektet förrän under nästa schemalagda utvärdering.  

5.  Ange följande information:  

    -   **Reparera inkompatibla regler när stöd** finns – reparerar automatiskt regler som inte är kompatibla för Windows Management INSTRUMENTATION (WMI), registret, skript och alla inställningar för mobila enheter som har registrerats av Configuration Manager.  

    -   **Tillåt reparation utanför underhållsfönstret** – Om en underhållsperiod har angetts för den samling som du distribuerar konfigurationsbaslinjen till, aktiverar du det här alternativet för att låta kompatibilitetsinställningar ändra värdet utanför underhållsperioden. Mer information om underhålls perioder finns i [använda underhålls](../../core/clients/manage/collections/use-maintenance-windows.md)perioder.  

6.  **Generera en avisering** – konfigurerar en avisering som genereras om konfigurations bas linjens kompatibilitet är mindre än en angiven procent andel vid en angiven tidpunkt. Du kan även ange om du vill att en avisering ska skickas till System Center Operations Manager.  

7.  **Samling** – Klicka på **Bläddra** och välj den samling där du vill distribuera konfigurationsbaslinjen.  

8.  **Ange schema för utvärdering av kompatibilitet för denna konfigurations bas linje** Anger det schema enligt vilket den distribuerade konfigurations bas linjen utvärderas på klient datorer. Det kan vara ett enkelt eller ett anpassat schema.  

    > [!NOTE]  
    >  Om konfigurationsbaslinjen distribueras till en dator utvärderas kompatibiliteten inom två timmar från den starttid som du har schemalagt. Om den distribueras till en användare utvärderas kompatibiliteten när användaren loggar in.  

9. Klicka på **OK** . Dialogrutan **Distribuera konfigurationsbaslinjer** stängs, och distributionen skapas. Mer information om hur du övervakar distributionen finns i [övervaka kompatibilitetsinställningar](monitor-compliance-settings.md).  
