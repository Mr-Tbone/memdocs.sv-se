---
title: Platskomponenter
titleSuffix: Configuration Manager
description: Lär dig hur du konfigurerar plats komponenter för att ändra beteendet för plats system roller och rapportering av plats status.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a3447e6ac71e9c5441a9e82034ee41eabda59374
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718331"
---
# <a name="site-components-for-configuration-manager"></a>Plats komponenter för Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

För varje Configuration Manager plats kan du konfigurera plats komponenter för att ändra beteendet för plats system roller och rapportering av plats status. Konfiguration av plats komponenter gäller för en plats och varje instans av en lämplig plats system roll på platsen.  

Gå till arbets ytan **Administration** i Configuration Manager-konsolen, expandera **plats konfiguration**och välj noden **platser** . Välj en plats. I gruppen **Inställningar** i menyfliksområdet väljer du **Konfigurera plats komponenter**. Välj något av följande alternativ:

- [Program varu distribution](#software-distribution)  
- [Program uppdaterings plats](#software-update-point) 
- [Distribution av operativsystem](#operating-system-deployment)
- [Hanterings plats](#management-point)  
- [Status rapportering](#status-reporting)  
- [E-postavisering](#email-notification)
- [Medlemskaps utvärdering för samling](#bkmk_colleval)


## <a name="about-site-components"></a>Om platskomponenter  

 De flesta alternativ för de olika plats komponenterna är själv för klar Ande när de visas i Configuration Manager-konsolen. Följande information kan dock hjälpa dig att förklara några av de mer komplexa konfigurationerna eller dirigera dig till ytterligare innehåll.  

> [!Note]  
> De tillgängliga alternativen för vissa komponenter varierar om du väljer den centrala administrations platsen, en primär plats eller en sekundär plats. Vissa komponenter är inte tillgängliga för vissa typer av webbplatser.  



### <a name="software-distribution"></a>Programvarudistribution  

#### <a name="content-distribution-settings"></a>Inställningar för innehålls distribution
På fliken **Allmänt** anger du inställningar som ändrar hur plats servern överför innehåll till dess distributions platser. Om du ökar värdena som du använder för inställningar för samtidig distribution kan innehållsdistributionen använda mer bandbredd i nätverket.  

#### <a name="pull-distribution-point"></a>Mottagar distributions plats
Mer information finns i [använda en mottagar distributions plats](../../../plan-design/hierarchy/use-a-pull-distribution-point.md).

#### <a name="network-access-account"></a>Nätverksåtkomstkonto
Mer information finns i [konto för nätverks åtkomst](../../../plan-design/hierarchy/accounts.md#network-access-account).  


### <a name="software-update-point"></a>Programuppdateringsplats  

Mer information finns i [installera en program uppdaterings plats](../../../../sum/get-started/install-a-software-update-point.md).  


### <a name="operating-system-deployment"></a>Distribution av operativsystem

Mer information finns i [ange enhet för etablering av OS-avbildningar](../../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive).


### <a name="management-point"></a>Hanteringsplats  

På fliken **Allmänt** konfigurerar du platsen för att publicera information om dess hanterings platser till Active Directory Domain Services.  

Configuration Manager klienter använder hanterings platser för att hitta tjänster, samt för att hitta plats information, till exempel alternativ för gränser grupp medlemskap och val av PKI-certifikat. Klienter använder också hanterings platser för att hitta andra hanterings platser på platsen, samt distributions platser som program varan ska laddas ned från. Hanterings platser hjälper också klienter att slutföra platstilldelning och hämta klient principer och ladda upp klient information.  

Den säkraste metoden för klienter att hitta hanterings platser är att publicera dem i Active Directory Domain Services. Den här tjänst plats metoden kräver att följande är sant:

- Schemat har utökats för Configuration Manager.
- Det finns en **system hanterings** behållare med lämpliga säkerhets behörigheter för plats servern att publicera till den här behållaren.
- Configuration Manager webbplats har kon figurer ATS att publicera till Active Directory Domain Services.
- Klienterna tillhör samma Active Directory skog som plats serverns skog.  

När klienter i intranätet inte kan använda Active Directory Domain Services för att hitta hanterings platser använder du [DNS-publicering](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns).  

Allmän information om tjänst lokalisering finns i [förstå hur klienter hittar plats resurser och tjänster](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  


#### <a name="publish-selected-intranet-management-points-in-dns"></a>Publicera markerade intranät hanterings platser i DNS
Ange det här alternativet när klienter i intranätet inte kan hitta hanterings platser från Active Directory Domain Services. De kan i stället använda en resurs post för DNS-tjänstens plats (SRV RR) för att hitta en hanterings plats på den tilldelade platsen.  

För att Configuration Manager ska kunna publicera intranät hanterings platser till DNS måste alla följande villkor vara uppfyllda:  

-   DNS-servrarna har BIND version 8.1.2 eller senare.  

-   Dina DNS-servrar har kon figurer ATS för automatiska uppdateringar och stöder tjänst platsens resurs poster.  

-   De angivna fullständigt kvalificerade domän namnen (FQDN) för hanterings platserna i Configuration Manager ha värd poster (A eller AAA-poster) i DNS.  

> [!WARNING]  
>  För att klienter ska hitta hanterings platser som publiceras i DNS måste du tilldela klienterna till en speciell plats (i stället för att använda automatisk platstilldelning). Konfigurera dessa klienter så att de använder plats koden med domänsuffix för hanterings platsen. Mer information finns i [hitta hanterings platser](../../../clients/deploy/assign-clients-to-a-site.md#locating-management-points).  

Om Configuration Manager klienter inte kan använda Active Directory Domain Services eller DNS för att hitta hanterings platser på intranätet, använder de [WINS](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins). Den första hanterings platsen som installeras för platsen publiceras automatiskt till WINS när den har kon figurer ATS för att godkänna HTTP-klientanslutningar på intranätet.  


### <a name="status-reporting"></a>Status rapportering  

De här inställningarna konfigurerar direkt detalj nivån som ingår i status rapporter från platser och klienter.  


### <a name="email-notification"></a>E-postavisering  

Ange information om konto och e-postserver om du vill att Configuration Manager ska kunna skicka e-postmeddelanden för aviseringar.  

Mer information finns i [använda aviseringar och status systemet](../../manage/use-alerts-and-the-status-system.md).


### <a name="collection-membership-evaluation"></a><a name="bkmk_colleval"></a>Medlemskaps utvärdering för samling  

Använd den här komponenten för att ange hur ofta samlings medlemskap utvärderas stegvis. Inkrementell utvärdering uppdaterar ett samlingsmedlemskap med bara nya eller ändrade resurser.  

Mer information finns i [metod tips för samlingar](../../../clients/manage/collections/best-practices-for-collections.md).



##  <a name="use-the-configuration-manager-service-manager-to-manage-site-components"></a><a name="BKMK_ServiceMgr"></a> Hantera platskomponenter med tjänsthanteraren för Configuration Manager  

Du kan använda Configuration Manager Service Manager för att kontrol lera Configuration Manager tjänster och för att visa status för alla Configuration Manager-tjänster eller arbets trådar. Dessa tjänster och trådar kallas gemensamt för Configuration Manager-komponenter. Förstå följande instruktioner om Configuration Manager-komponenter:  

-   Komponenter kan köras på alla plats system.  

-   Komponenterna hanteras på samma sätt som du hanterar tjänster i Windows. Du kan starta, stoppa, pausa, återuppta eller fråga Configuration Manager-komponenter.  

En Configuration Manager-tjänst körs när det finns något för den att göra. Den här åtgärden är vanligt vis när en konfigurations fil skrivs till en komponents inkorg. 


### <a name="use-the-configuration-manager-service-manager"></a>Använd Configuration Manager Service Manager  

1.  I Configuration Manager-konsolen går du till arbets ytan **övervakning** , expanderar **system status**och väljer noden **komponent status** .  

2.  Välj **Start**i gruppen **komponent** i menyfliksområdet och välj sedan **Configuration Manager Service Manager**.  

3.  När Configuration Manager Service Manager öppnas ansluter du till den plats du vill hantera.  

     Om du inte ser den plats som du vill hantera går du till menyn **plats** och väljer **Anslut**. Ange sedan namnet på plats servern för rätt plats.  

4.  Expandera platsen och gå till **Komponenter** eller **Servrar**, beroende på var de komponenter finns som du vill hantera.  

5.  Välj en eller flera komponenter i den högra rutan. Sedan väljer du **fråga** på menyn **komponent** för att uppdatera status för ditt val.  

6.  När komponentens status har uppdaterats använder du ett av de fyra åtgärds alternativen på **komponent** -menyn för att ändra komponentens åtgärd. När du har begärt en åtgärd måste du ställa en fråga till komponenten om du vill se komponentens nya status.  

7.  Stäng Configuration Manager Service Manager när du är klar med att ändra drift status för komponenter.  
