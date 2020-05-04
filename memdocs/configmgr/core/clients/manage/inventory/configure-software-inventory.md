---
title: Konfigurera programvaruinventering
titleSuffix: Configuration Manager
description: Konfigurera program varu inventering och undanta mappar från program varu inventering i Configuration Manager.
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 74436eb95166ae9bc78d7ae22881b709349bf847
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714432"
---
# <a name="how-to-configure-software-inventory-in-configuration-manager"></a>Så här konfigurerar du program varu inventering i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Den här proceduren konfigurerar standard klient inställningarna för program varu inventering och gäller för alla datorer i hierarkin. Om du bara vill tillämpa inställningarna på vissa datorer skapar du en anpassad enhets klient inställning och tilldelar den till en samling. Mer information om hur du skapar anpassade enhets inställningar finns i [Konfigurera klient inställningar](../../../../core/clients/deploy/configure-client-settings.md).   

## <a name="to-configure-software-inventory"></a>Så här konfigurerar du programvaruinventering  

1. I Configuration Manager-konsolen väljer du **Administration** > **klient inställningar**  **standard klient inställningar**.  

2. På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  

3. Välj **program varu inventering**i dialog rutan **standardinställningar** .  

4. Konfigurera följande värden i listan **Enhetsinställningar** :  

   -   **Aktivera program varu inventering på klienter** – Välj **Sant**i den nedrullningsbara listan.  

   -   Schemalägg **program varu inventering och insamling av filer** – konfigurerar intervallet då klienterna samlar in program varu inventering och filer.   

5. Konfigurera klientinställningarna som du behöver. Avsnittet [program varu inventering](../../../../core/clients/deploy/about-client-settings.md#software-inventory) i artikeln [om klient inställningar](../../../../core/clients/deploy/about-client-settings.md) innehåller en lista över klient inställningar.  

   Klientdatorerna konfigureras med de här inställningarna nästa gång de laddar ned klientprinciper. Information om hur du startar princip hämtning för en enskild klient finns i [Hantera klienter](../../../../core/clients/manage/manage-clients.md).  

   > [!TIP]
   >   Felkod 80041006 i inventoryprovider. log innebär att WMI-providern har slut på minne. Det innebär att minnes kvot gränsen för en provider har nåtts och inventerings leverantören inte kan fortsätta.
   > I det här fallet skapar inventerings agenten en rapport med 0 poster så att inga lager artiklar rapporteras. <br/>
   > En möjlig lösning för det här felet är att minska omfånget för program inventerings samlingen. Om felet inträffar efter att inventerings omfånget har begränsats, kan [MemoryPerHost](https://blogs.technet.microsoft.com/askperf/2008/09/16/memory-and-handle-quotas-in-the-wmi-provider-service/) -egenskapen som definieras i klassen [_ProviderHostQuotaConfiguration](https://msdn.microsoft.com/library/aa394671) tillhandahålla en lösning.

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>Undanta mappar från programvaruinventering  

1.  Skapa en tom fil med Notepad.exe och ge den namnet **Skpswi.dat**.  

2.  Högerklicka på filen **Skpswi. dat** och klicka på **Egenskaper**. I filegenskaperna för filen Skpswi.dat väljer du attributet **Dold** .  

3.  Placera filen **Skpswi.dat** i roten på varje klienthårddisk eller mappstruktur som du vill undanta från programvaruinventering.  

> [!NOTE]  
>  Klientenheten kommer inte att inventeras via programvaruinventering igen såvida inte den här filen tas bort från enheten på klientdatorn.
