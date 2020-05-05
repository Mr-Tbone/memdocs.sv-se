---
title: Konfigurera fjärr styrning
titleSuffix: Configuration Manager
description: Konfigurera fjärr styrning i Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78f74a9659a011defd50e6ab0e9e1cfe85eec16b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076738"
---
# <a name="configuring-remote-control-in-configuration-manager"></a>Konfigurera fjärr styrning i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

 Den här proceduren beskriver hur du konfigurerar standard klient inställningarna för fjärr styrning. De här inställningarna gäller för alla datorer i hierarkin. Om du vill att inställningarna bara ska gälla för vissa datorer tilldelar du en anpassad enhets klient inställning till en samling som innehåller dessa datorer. Mer information finns i [så här konfigurerar du klient inställningar](../../../../core/clients/deploy/configure-client-settings.md). 

Om du vill använda Fjärrhjälp eller fjärr skrivbord måste det installeras och konfigureras på datorn som kör Configuration Manager-konsolen. Mer information om hur du installerar och konfigurerar Fjärrhjälp eller Fjärrskrivbord finns i dokumentationen för Windows.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Så här aktiverar du fjärrstyrning och konfigurerar klientinställningar  

1. I Configuration Manager-konsolen väljer du **Administration** > **klient inställningar** > **standard klient inställningar**.  

2. På fliken **Start** går du till gruppen **Egenskaper** och väljer **Egenskaper**.  

3. I dialog rutan **standard** väljer du **fjärrverktyg**.  

4. Konfigurera klient inställningar för fjärr styrning, Fjärrhjälp och fjärr skrivbord. En lista över klient inställningar för fjärrverktyg som du kan konfigurera finns i [fjärrverktyg](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

   Du kan ändra namnet på företaget som visas i dialogrutan **Fjärrstyrning för ConfigMgr** genom att konfigurera ett värde för **Organisationsnamn som visas i Software Center** i klientinställningarna för **Datoragent** .  

   Klientdatorerna konfigureras med de här inställningarna nästa gång de laddar ned klientprinciper. Information om hur du startar princip hämtning för en enskild klient finns i [Hantera klienter](../../../../core/clients/manage/manage-clients.md).  

#### <a name="enable-keyboard-translation"></a>Aktivera tangent bords Översättning

Som standard skickar Configuration Manager nyckel positionen från visnings platsen till delnings platsen. Detta kan ge ett problem för tangent bords konfigurationer som skiljer sig från visnings program till delare. Ett visnings program med ett engelskt tangent bord skulle t. ex. skriva "A", men delarnas franska tangent bord skulle ge en "Q". Nu har du möjlighet att konfigurera fjärr styrning så att själva själva figuren skickas från Viewers tangent bord till delnings sidan, och vad visnings programmet avser att skriva kommer till delningen.

Om du vill aktivera tangent bords översättning väljer du **åtgärd**i **Configuration Manager fjärr styrning**och väljer **Aktivera tangent bords översättning** för att överföra nyckel position.

> [!NOTE]
>
> Särskilda nycklar, till exempel ~! # @ $%, kommer inte att översättas korrekt.


## <a name="keyboard-shortcuts-for-the-remote-control-viewer"></a>Kortkommandon för fjärr styrnings visaren

|Kortkommando|Beskrivning|  
|-----------------------|-----------------|  
|Alt+Page Up|Växlar mellan att köra program från vänster till höger.|  
|Alt+Page Down|Växlar mellan att köra program från höger till vänster.|  
|Alt+Insert|Växlar mellan att köra program i den ordning som de öppnades.|  
|Alt+Home|Visar **Start** -menyn.|  
|Ctrl+Alt+End|Visar dialogrutan Windows-säkerhet (Ctrl+Alt+Del).|  
|Alt+Delete|Visar Windows-menyn.|  
|Ctrl+Alt+minustecken (på det numeriska tangentbordet)|Kopierar det aktiva fönstret på den lokala datorn till Urklipp på fjärrdatorn.|  
|Ctrl+Alt+plustecken (på det numeriska tangentbordet)|Kopierar hela fönsterområdet på den lokala datorn till Urklipp på fjärrdatorn.|  
