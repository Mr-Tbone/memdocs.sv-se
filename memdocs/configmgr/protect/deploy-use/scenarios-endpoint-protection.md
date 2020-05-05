---
title: Skydda datorer mot skadlig kod
titleSuffix: Configuration Manager
description: Lär dig hur du implementerar Endpoint Protection i Configuration Manager för att skydda datorer mot angrepp mot skadlig kod.
ms.date: 05/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
author: mestew
ms.author: mstewart
manager: doubeby
ms.openlocfilehash: 6e0e350fe490de50a053e93f2922feba5e0ea8c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722391"
---
# <a name="example-scenario-use-endpoint-protection-to-protect-computers-from-malware"></a>Exempel scenario: Använd Endpoint Protection för att skydda datorer mot skadlig kod

*Gäller för: Configuration Manager (aktuell gren)*

Den här artikeln innehåller ett exempel scenario för hur du kan implementera Endpoint Protection i Configuration Manager för att skydda datorer i organisationen från angrepp mot skadlig kod.  



## <a name="scenario-overview"></a>Scenarioöversikt

 Configuration Manager installeras och används på Sparbanken. Banken använder för närvarande System Center-Endpoint Protection för att skydda datorer mot angrepp mot skadlig kod. Dessutom använder banken Windows grupprincip för att se till att Windows-brandväggen är aktiverad på alla datorer på företaget och att användarna får en avisering när Windows-brandväggen blockerar ett nytt program.  

Configuration Manager-administratörer har blivit ombedd att uppgradera program varan för Sparbanken för program mot skadlig kod till System Center Endpoint Protection så att banken kan dra nytta av de senaste funktionerna för program mot skadlig kod och kunna hantera den program mot skadlig kod från Configuration Manager-konsolen på ett centralt sätt. 


## <a name="business-requirements"></a>Affärs krav

Den här implementeringen har följande krav:  

- Använd Configuration Manager för att hantera inställningarna för Windows-brandväggen som för närvarande hanteras av grupprincip.  

- Använd Configuration Manager program uppdateringar för att hämta definitioner av skadlig kod till datorer. Om program uppdateringar inte är tillgängliga, till exempel om datorn inte är ansluten till företags nätverket, måste datorerna Ladda ned definitions uppdateringar från Microsoft Update.  

- Användarnas datorer måste utföra en snabb genomsökning av skadlig kod varje dag. Servrarna måste dock köra en fullständig genomsökning varje lördag kl. 01.00, utanför kontorstid.  

- Skicka en e-postavisering när något av följande inträffar:  

  -   Skadlig kod har upptäckts på en dator  

  -   Samma skadliga kod har identifierats på mer än fem procent av datorerna  

  -   Samma hot för skadlig kod har identifierats fler än fem gånger under en 24-timmarsperiod  

  -   Fler än tre olika typer av skadlig kod har identifierats under en 24-timmarsperiod  

  Administratörerna utför sedan följande steg för att implementera Endpoint Protection:  



##  <a name="steps-to-implement-endpoint-protection"></a> Steg för att implementera Endpoint Protection  

|Process|Referens|  
|-------------|---------------|  
|Administratörerna granskar den tillgängliga informationen om de grundläggande begreppen för Endpoint Protection i Configuration Manager.|Översikts information om Endpoint Protection finns i [Endpoint Protection](endpoint-protection.md).|  
|Administratörerna granskar och implementerar de nödvändiga förutsättningarna för att använda Endpoint Protection.|Information om förutsättningarna för Endpoint Protection finns i [Planera för Endpoint Protection](../plan-design/planning-for-endpoint-protection.md).|  
|Administratörer installerar Endpoint Protection plats system rollen på en plats system Server, högst upp i den Sparbanken.|Mer information om hur du installerar Endpoint Protection plats system rollen finns i "förutsättningar" i [konfigurera Endpoint Protection](endpoint-protection-configure.md).|  
|Administratörer konfigurerar Configuration Manager att använda en SMTP-server för att skicka e-postaviseringar.<br /><br /> **Obs:** Du måste bara konfigurera en SMTP-server om du vill bli meddelad via e-post när en Endpoint Protection varning genereras.|Mer information finns i [Konfigurera aviseringar i Endpoint Protection](endpoint-configure-alerts.md).|  
|Administratörerna skapar en enhets samling som innehåller alla datorer och servrar som ska installera Endpoint Protection-klienten. De namnger samlingen **alla datorer som skyddas av Endpoint Protection**.<br /><br /> **Tips:** Det går inte att konfigurera aviseringar för användar samlingar.|Mer information om hur du skapar samlingar finns i [skapa samlingar](../../core/clients/manage/collections/create-collections.md)|  
|Administratörerna konfigurerar följande aviseringar för samlingen: <br /><br />1) **skadlig kod har identifierats**: administratörerna konfigurerar allvarlighets graden **kritisk**. <br /><br />2) **samma typ av skadlig kod har identifierats på flera datorer**: administratörerna konfigurerar allvarlighets graden **kritisk** och anger att aviseringen ska genereras när mer än 5 procent av datorerna har identifierat skadlig kod. <br /><br />3) **samma typ av skadlig kod har identifierats upprepade gånger inom det angivna intervallet på en dator**: administratörerna konfigurerar allvarlighets graden kritisk och anger att aviseringen ska genereras när skadlig kod upptäcks över 5 gånger under en 24-timmarsperiod. <br /><br />4) **flera typer av skadlig kod har identifierats på samma dator inom det angivna intervallet**: administratörerna konfigurerar allvarlighets graden kritisk och anger att aviseringen ska genereras när fler än tre typer av skadlig kod genereras under en 24-timmarsperiod.<br /><br /> Värdet för **aviserings allvarlighets grad** anger den varnings nivå som ska visas i Configuration Manager-konsolen och i aviseringar som de får i ett e-postmeddelande.<br /><br /> De väljer också alternativet **Visa den här samlingen i Endpoint Protection-instrumentpanelen** så att de kan övervaka aviseringarna i Configuration Manager-konsolen.|Se "Konfigurera aviseringar för Endpoint Protection" i [konfigurera Endpoint Protection](endpoint-configure-alerts.md).|  
|Administratörer konfigurerar Configuration Manager program uppdateringar för att ladda ned och distribuera definitions uppdateringar tre gånger per dag med hjälp av en automatisk distributions regel.|Mer information finns i avsnittet "använda Configuration Manager program uppdateringar för att leverera definitions uppdateringar" i [använda Configuration Manager program uppdateringar för att leverera definitions uppdateringar](endpoint-definitions-configmgr.md).|  
|Administratörerna granskar inställningarna i standard principen för program mot skadlig kod som innehåller rekommenderade säkerhets inställningar från Microsoft. För att datorer ska kunna utföra en snabb genomsökning varje dag ändrar de följande inställningar:<br /><br /> 1) **kör en daglig snabb sökning på klient datorer**: **Ja**.<br /><br /> 2) **tid för daglig snabb genomsökning**: **9:00 am**.<br /><br /> Administratörerna noterar att **uppdateringar som distribueras från Microsoft Update** väljs som standard som en definitions uppdaterings källa. Detta uppfyller de affärs krav som datorerna hämtar definitioner från Microsoft Update när de inte kan ta emot Configuration Manager program uppdateringar.|Se [hur du skapar och distribuerar principer för program mot skadlig kod för Endpoint Protection](endpoint-antimalware-policies.md).|  
|Administratörerna skapar en samling som endast innehåller Sparbanken för Sparbanken med namnet **Sparbankens Bank servrar**.|Se [skapa samlingar](../../core/clients/manage/collections/create-collections.md)|  
|Administratörerna skapar en anpassad princip för program mot skadlig kod med namnet **Sparbanken bank Server policy**. De lägger bara till inställningarna för **schemalagda genomsökningar** och gör följande ändringar:<br /><br /> **Genomsökningstyp**:  **Fullständig**<br /><br /> **Dag för genomsökning**:  **Lördag**<br /><br /> **Tidpunkt för genomsökningen**: **01:00:00**<br /><br /> **Kör dagligen en snabbgenomsökning på klientdatorer**:  **Nej**.|Se [hur du skapar och distribuerar principer för program mot skadlig kod för Endpoint Protection](endpoint-antimalware-policies.md).|  
|Administratörerna distribuerar principen för **Sparbanken för sparbanks-bank servern** till samlingen för **Sparbanken för Sparbanken** .|Se "distribuera en princip för program mot skadlig kod till klient datorer" [så här skapar och distribuerar du principer för program mot skadlig kod för Endpoint Protection](endpoint-antimalware-policies.md) artikel.|  
|Administratörerna skapar en ny uppsättning med anpassade klient enhets inställningar för Endpoint Protection och namnger dessa **Endpoint Protection inställningar för Sparbanken**.<br /><br /> **Obs:** Om du inte vill installera och Aktivera Endpoint Protection på alla klienter i hierarkin kontrollerar du att alternativen **hantera Endpoint Protection-klienten på klient datorer** och **installerar Endpoint Protection klient på klient datorer** båda är konfigurerade som **Nej** i standard klient inställningarna.|Mer information finns i [Konfigurera anpassade klient inställningar för Endpoint Protection](endpoint-protection-configure-client.md).|  
|De konfigurerar följande inställningar för Endpoint Protection:<br /><br /> **Hantera Endpoint Protection-klient på klientdatorer**:  **Ja**<br /><br /> Den här inställningen och värdet ser till att alla befintliga Endpoint Protection-klienter som är installerade hanteras av Configuration Manager.<br /><br /> **Installera Endpoint Protection-klient på klientdatorer**:  **Ja**.</br></br>**Obs!** Från och med Configuration Manager 1802 behöver inte Windows 10-enheter ha Endpoint Protection-agenten installerad. Om den redan är installerad på Windows 10-enheter kan Configuration Manager inte ta bort den. Administratörer kan ta bort Endpoint Protection-agenten på Windows 10-enheter som kör minst 1802-klient versionen.|Mer information finns i [Konfigurera anpassade klient inställningar för Endpoint Protection](endpoint-protection-configure-client.md).|  
|Administratörerna distribuerar inställningen för **sparbanken Endpoint Protection** klient inställningar till **alla datorer som skyddas av Endpoint Protection** -samlingen.|Se Konfigurera anpassade klient inställningar för Endpoint Protection i [konfigurera Endpoint Protection i Configuration Manager](endpoint-antimalware-policies.md).|  
|Administratörerna använder guiden Skapa princip för Windows-brandväggen för att skapa en princip genom att konfigurera följande inställningar för domän profilen:<br /><br /> 1) **Aktivera Windows-brandväggen**: **Ja**<br /><br /> 11.2<br />                    **Meddela användaren när ett nytt program blockeras av Windows-brandväggen**: **Ja**|Se [hur du skapar och distribuerar principer för Windows-brandväggen för Endpoint Protection](../../protect/deploy-use/create-windows-firewall-policies.md)|  
|Administratörerna distribuerar den nya brand Väggs principen till samlingen **alla datorer som skyddas av Endpoint Protection** som de skapade tidigare.|Se "så här distribuerar du en princip för Windows-brandväggen" i [skapa och distribuera principer för Windows-brandväggen för Endpoint Protection](create-windows-firewall-policies.md)|  
|Administratörer använder de tillgängliga hanterings uppgifterna för Endpoint Protection för att hantera principer för program mot skadlig kod och Windows-brandväggen, utföra genomsökningar av datorer vid behov, tvinga datorer att ladda ned de senaste definitionerna och ange ytterligare åtgärder som ska vidtas när skadlig kod upptäcks.|Se [Hantera principer för program mot skadlig kod och brand Väggs inställningar för Endpoint Protection](endpoint-antimalware-firewall.md)|  
|Administratörerna använder följande metoder för att övervaka status för Endpoint Protection och de åtgärder som vidtas av Endpoint Protection:<br /><br /> 1) genom att använda noden **Endpoint Protection status** under **säkerhet** i arbets ytan **övervakning** .<br /><br /> 2) genom att använda **Endpoint Protection** -noden i arbets ytan **till gångar och efterlevnad** .<br /><br /> 3) med hjälp av de inbyggda Configuration Manager rapporterna.|Se [övervaka Endpoint Protection](monitor-endpoint-protection.md)|  

 Administratörer rapporterar en lyckad implementering av Endpoint Protection till sin chef och bekräftar att datorerna på Sparbanken nu är skyddade från program mot skadlig kod, enligt de verksamhets krav som de har fått. 

## <a name="next-steps"></a>Nästa steg

Mer information finns i [så här konfigurerar du Endpoint Protection](endpoint-protection-configure.md)