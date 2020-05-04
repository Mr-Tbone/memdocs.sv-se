---
title: Planera för och konfigurera kompatibilitetsinställningar
titleSuffix: Configuration Manager
description: Lär dig mer om kraven och konfigurations uppgifterna för att arbeta med kompatibilitetsinställningar i Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9ea20b01-676a-4cc2-b328-0098a41b202e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 73ccec4ca318b522c0714bc8e5cc89f6c8899edd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712157"
---
# <a name="plan-for-and-configure-compliance-settings-in-configuration-manager"></a>Planera för och konfigurera kompatibilitetsinställningar i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Innan du börjar arbeta med Configuration Manager kompatibilitetsinställningar, finns det några krav som du behöver känna till och vissa konfigurations åtgärder som du behöver utföra.  

## <a name="prerequisites-for-compliance-settings"></a>Krav för kompatibilitetsinställningar  

|Krav|Mer information|  
|------------------|----------------------|  
|Windows Configuration Manager-klienter måste vara aktiverade och konfigurerade för utvärdering av efterlevnad.|Se nedan|  
|Om du vill köra rapporter måste du konfigurera rapportering för platsen.|[Introduktion till rapportering](../../core/servers/manage/introduction-to-reporting.md)|  
|Nödvändiga säkerhets behörigheter.|Säkerhets rollen **kompatibilitets inställnings hanterare** innehåller de behörigheter som krävs för att hantera kompatibilitetsinställningar, konfigurations objekt för användar data och profiler samt fjärr anslutnings profiler.<br /><br /> [Konfigurera rollbaserad administration](../../core/servers/deploy/configure/configure-role-based-administration.md)|  

##  <a name="enable-and-configure-compliance-settings-for-windows-pcs-only"></a>Aktivera och konfigurera kompatibilitetsinställningar (endast för Windows-datorer)  

Den här proceduren konfigurerar standardklientinställningarna för kompatibilitetsinställningar och gäller för alla datorer i hierarkin. Om du vill att inställningarna bara ska gälla för vissa datorer skapar du en anpassad klientinställning för enheter och kopplar den till en samling som innehåller de datorer som du vill använda kompatibilitetsinställningar för. Mer information om hur du skapar anpassade enhets inställningar finns i [Konfigurera klient inställningar](../../core/clients/deploy/configure-client-settings.md).  

> [!TIP]  
>  Andra typer av enheter kräver ingen specifik konfiguration för utvärderingen av kompatibilitetsinställningar.  

1.  I Configuration Manager-konsolen klickar du på **Administration** > **klient inställningar** > **standardinställningar**.  
2.  På fliken **Start** går du till gruppen **Egenskaper** och klickar på **Egenskaper**.  
3.  Klicka på **Kompatibilitetsinställningar** i dialogrutan **Standardinställningar**.  
4.  Konfigurera följande klientinställningar för kompatibilitetsinställningar:
    - **Aktivera utvärdering av efterlevnad på klienter** – ange som **Sant** om du vill utvärdera kompatibiliteten på klient enheter.
    - **Schemalägg utvärdering av kompatibilitet** – Klicka på **schema** om du vill ändra standard för utvärderings schema för kompatibilitet på klient enheter.
    - **Aktivera användar data och profiler** – aktivera det här alternativet om du vill skapa och distribuera konfigurations objekt för användar data och profiler till Windows-datorer. Mer information finns i [skapa konfigurations objekt för användar data och profiler](../deploy-use/create-remote-connection-profiles.md).
5. Stäng dialogrutan **Standardinställningar** genom att klicka på **OK** .  

Klientdatorerna konfigureras med de här inställningarna nästa gång de laddar ned klientprinciper.  
