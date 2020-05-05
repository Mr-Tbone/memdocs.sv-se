---
title: Skicka schema-verktyget
titleSuffix: Configuration Manager
description: Använd verktyget Skicka schema för att utlösa ett schema på en Configuration Manager-klient.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d5ce547d-3b3b-47d3-bcd7-6ff94692c046
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78e154c5361063224d9e8c99bc87ba117958edf4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723126"
---
# <a name="send-schedule-tool"></a>Skicka schema-verktyget

*Gäller för: Configuration Manager (aktuell gren)*

Verktyget Skicka schema är ett av de [Configuration Manager verktygen](tools.md). Använd den för att utlösa ett schema på en klient eller utlösa utvärderingen av en angiven konfigurations bas linje. Den fungerar för den lokala datorn eller riktar sig till en fjärran sluten klient.  

Använd till exempel verktyget för att utlösa ett inventerings schema eller en utvärdering av efterlevnad. Om ett antal Configuration Manager-klienter inte nyligen har rapporterat inventerings-eller kompatibilitetsstatus kör du verktyget för att starta det schema som krävs på varje klient.



## <a name="usage"></a>Användning

Kör **SendSchedule. exe** som administratör. 

`SendSchedule /L [Computer Name]`
`SendSchedule "<Message GUID | DCM UID>" [Computer Name]` 

När du har utlöser ett meddelande (GUID), se **SMSClientMethodProvider. log**. Mer information om tillgängliga meddelande-GUID finns i [meddelande-ID](#bkmk_sendschedule-guids).

När du har utlöst utvärderingen av en konfigurations bas linje (DCM-UID), se **DCMAgent. log**.



## <a name="command-line-options"></a>Kommandoradsalternativ


### <a name="option-l"></a>Alternativet`/L` 
Lista alla meddelande-GUID eller DCM-UID som är tillgängliga för sändning. Visa det meningsfulla namnet på meddelanden i data tabellen för var och en. Om dator namnet saknas används den lokala datorn. Om du anger ett meddelande utan ett dator namn skickar det meddelandet till den lokala datorn. 



## <a name="examples"></a>Exempel

#### <a name="list-the-available-messages-on-the-local-machine"></a>Visa en lista över tillgängliga meddelanden på den lokala datorn 
`SendSchedule /L` 

#### <a name="list-the-available-messages-on-the-client-mypc"></a>Visa en lista över tillgängliga meddelanden på klient dator gruppen: 
`SendSchedule /L MyPC`

#### <a name="trigger-hardware-inventory-on-the-local-machine"></a>Utlös maskin varu inventering på den lokala datorn
`SendSchedule {00000000-0000-0000-0000-000000000001}`

#### <a name="trigger-hardware-inventory-on-mypc"></a>Utlös maskin varu inventering på min dator: 
`SendSchedule {00000000-0000-0000-0000-000000000001} MyPC` 

#### <a name="trigger-the-evaluation-of-a-specific-configuration-baseline-on-mypc"></a>Utlös utvärdering av en speciell konfigurations bas linje på min dator: 
`SendSchedule ScopeId_611E8382-C064-4B62-B0DE-EFFB52AE8994/Baseline_36722778-69dd-4423-9632-b61148b2b67e MyPC` 



## <a name="message-ids"></a><a name="bkmk_sendschedule-guids"></a>Meddelande-ID

|Meddelande-ID  |Visningsnamn  |
|---------|---------|
|{00000000-0000-0000-0000-000000000001}|Maskinvaruinventering|
|{00000000-0000-0000-0000-000000000002}|Programvaruinventering|
|{00000000-0000-0000-0000-000000000003}|Identifierings inventering|
|{00000000-0000-0000-0000-000000000010}|Fil insamling|
|{00000000-0000-0000-0000-000000000011}|IDMIF-samling|
|{00000000-0000-0000-0000-000000000021}|Begär dator tilldelningar|
|{00000000-0000-0000-0000-000000000022}|Utvärdera dator principer|
|{00000000-0000-0000-0000-000000000023}|Uppdatera standard MP-aktivitet|
|{00000000-0000-0000-0000-000000000024}|LS (plats tjänst) uppgift för att uppdatera platser|
|{00000000-0000-0000-0000-000000000025}|Uppdaterings aktivitet för LS timeout|
|{00000000-0000-0000-0000-000000000026}|Tilldelning av Policy Agent förfrågan (användare)|
|{00000000-0000-0000-0000-000000000027}|Utvärdera tilldelning för princip agent (användare)|
|{00000000-0000-0000-0000-000000000031}|Användnings rapport för avläsning av program vara|
|{00000000-0000-0000-0000-000000000032}|Käll uppdaterings meddelande|
|{00000000-0000-0000-0000-000000000037}|Rensar cache för proxy-inställningar|
|{00000000-0000-0000-0000-000000000040}|Rensning av dator princip agent|
|{00000000-0000-0000-0000-000000000041}|Rensning av användar princip agent|
|{00000000-0000-0000-0000-000000000042}|Princip agent verifiera dator princip/tilldelning|
|{00000000-0000-0000-0000-000000000043}|Princip agent verifiera användar princip/tilldelning|
|{00000000-0000-0000-0000-000000000051}|Försöker igen/uppdatera certifikat i AD på MP|
|{00000000-0000-0000-0000-000000000061}|Status rapportering för peer-DP|
|{00000000-0000-0000-0000-000000000062}|Schema för väntande peer-DP-paket|
|{00000000-0000-0000-0000-000000000063}|Installations schema för SUM-uppdateringar|
|{00000000-0000-0000-0000-000000000101}|Samlings cykel för maskin varu inventering|
|{00000000-0000-0000-0000-000000000102}|Samlings cykel för program varu inventering|
|{00000000-0000-0000-0000-000000000103}|Cykel för insamling av identifierings data|
|{00000000-0000-0000-0000-000000000104}|Fil insamlings cykel|
|{00000000-0000-0000-0000-000000000105}|Samlings cykel för IDMIF|
|{00000000-0000-0000-0000-000000000106}|Rapport cykel för avläsning av program vara|
|{00000000-0000-0000-0000-000000000107}|Uppdaterings cykel för Windows Installers källista|
|{00000000-0000-0000-0000-000000000108}|Program uppdatering princip åtgärd utvärderings cykel för tilldelning av program uppdateringar|
|{00000000-0000-0000-0000-000000000109}|PDP underhålls princip gren distributions plats underhålls uppgift|
|{00000000-0000-0000-0000-000000000110}|DCM-princip|
|{00000000-0000-0000-0000-000000000111}|Skicka tillstånds meddelande som inte har skickats|
|{00000000-0000-0000-0000-000000000112}|Rensar cache för tillstånds system princip|
|{00000000-0000-0000-0000-000000000113}|Uppdatera käll princip|
|{00000000-0000-0000-0000-000000000114}|Uppdatera Store-princip|
|{00000000-0000-0000-0000-000000000115}|Tillstånds system princip Mass sändning hög|
|{00000000-0000-0000-0000-000000000116}|Sändning av tillstånds system princip Mass sändning|
|{00000000-0000-0000-0000-000000000121}|Princip åtgärd i Application Manager|
|{00000000-0000-0000-0000-000000000122}|Användar princip åtgärd i Application Manager|
|{00000000-0000-0000-0000-000000000123}|Global utvärderings åtgärd i Application Manager|
|{00000000-0000-0000-0000-000000000131}|Start Sammanfattning för energispar funktioner|
|{00000000-0000-0000-0000-000000000221}|Återutvärdera slut punkts distribution|
|{00000000-0000-0000-0000-000000000222}|Utvärderingen av slut punkten för principen|
|{00000000-0000-0000-0000-000000000223}|Identifiering av externa händelser|



