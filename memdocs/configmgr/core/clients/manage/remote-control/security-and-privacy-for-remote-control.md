---
title: Säkerhets sekretess för fjärr styrning
titleSuffix: Configuration Manager
description: Hämta information om säkerhet och sekretess för fjärr styrning i Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 272ee86b-d3d9-4fd9-b5c4-73e490e1a1e4
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 83631b331030f9648c3e88a2e101a013cfa0e98f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715104"
---
# <a name="security-and-privacy-for-remote-control-in-configuration-manager"></a>Säkerhet och sekretess för fjärr styrning i Configuration Manager

*Gäller för: Configuration Manager (aktuell gren)*

Det här avsnittet innehåller information om säkerhet och sekretess för fjärr styrning i Configuration Manager.  

##  <a name="security-best-practices-for-remote-control"></a><a name="BKMK_Security_HardwareInventory"></a> Rekommenderade säkerhetsmetoder för fjärrstyrning  
 Använd följande rekommenderade säkerhetsmetoder när du hanterar klientdatorer via fjärrstyrning.  

|Regelverk för säkerhet|Mer information|  
|----------------------------|----------------------|  
|Fortsätt inte att ansluta till en fjärrdator om NTLM används i stället för Kerberos-autentisering.|När Configuration Manager upptäcker att fjärrstyrningssession autentiseras med hjälp av NTLM i stället för Kerberos visas en varning som varnar dig om att det inte går att verifiera fjärrdatorns identitet. Fortsätt inte med fjärrstyrningssessionen. NTLM-autentisering är ett svagare autentiseringsprotokoll än Kerberos och är sårbart för repetitionsattacker och personifiering.|  
|Aktivera inte delning via Urklipp i visaren för fjärrstyrning.|Urklipp stöder objekt som körbara filer och text och kan användas under fjärrstyrningssessionen av användaren på värddatorn för att köra ett program på den ursprungliga datorn.|  
|Ange inte lösenord för privilegierade konton när du fjärradministrerar en dator.|Programvara som registrerar tangenttryckningar kan få tag på lösenordet. Eller, om programmet som körs på klientdatorn inte är det program som fjärrstyrningsanvändaren förväntade sig, kan programmet försöka avslöja lösenordet. När konton och lösenord krävs bör slutanvändaren ange dem.|  
|Lås tangentbordet och musen under en fjärrstyrningssession.|Om Configuration Manager upptäcker att fjärr styrnings anslutningen avbryts, kan Configuration Manager automatiskt låsa tangent bordet och musen så att en användare inte kan ta kontroll över den öppna fjärrstyrningssession. Den här identifieringen sker dock inte alltid omedelbart och den sker inte om fjärrstyrningstjänsten avslutas.<br /><br /> Välj åtgärden **Lås fjärrtangentbord och mus** i fönstret **Fjärrstyrning för ConfigMgr** .|  
|Låt inte användare konfigurera fjärrstyrningsinställningar i Software Center.|Aktivera inte klientinställningen **Användare kan ändra princip- eller meddelandeinställningar i Software Center** för att förhindra att användare utsätts för spioneri. Om en användare ändrar den, kan den tillåta att en annan användare på samma dator fjärrvisas. <br /><br />**Den här inställningen gäller för datorn, inte för den inloggade användaren**.|  
|Aktivera Windows-brandväggsprofilen **Domän** .|Aktivera klientinställningen **Aktivera Fjärrstyrning på klienter - Undantagsprofiler för brandvägg** och välj sedan Windows-brandväggsprofilen **Domän** för datorer i intranätet.|  
|Om du loggar ut under en fjärrstyrningssession och loggar in som en annan användare loggar du ut innan du kopplar från fjärrstyrningssessionen.|Om du inte loggar ut i det här scenariot förblir sessionen öppen.|  
|Ge inte användare behörighet som lokal administratör.|Om du beviljar användare behörighet som lokal administratör kan de ta över din fjärrstyrningssession eller kompromettera dina autentiseringsuppgifter.|  
|Använd antingen grupprincip eller Configuration Manager för att konfigurera inställningar för Fjärrhjälp, men inte båda.|Du kan använda Configuration Manager och grupprincip för att göra konfigurations ändringar i inställningarna för Fjärrhjälp. När grupprincipen uppdateras på klienten optimerar den som standard processen genom att bara ändra de principer som har ändrats på servern. Configuration Manager ändrar inställningarna i den lokala säkerhets principen, som kanske inte skrivs över om inte grupprincip uppdateringen framtvingas.<br /><br /> Om principen anges på båda platserna kan det leda till inkonsekventa resultat. Välj en av dessa metoder när du ska konfigurera inställningarna för Fjärrhjälp.|  
|Aktivera klientinställningen **Fråga användaren om Fjärrstyrning-behörighet**.|Även om det finns sätt att komma runt den här klientinställningen som uppmanar användaren att bekräfta en fjärrstyrningssession så minskar inställningen risken för att någon spionerar på användarna när de arbetar med konfidentiella uppgifter.<br /><br /> Uppmana även användarna att kontrollera kontonamnet som visas under fjärrstyrningssessionen och att koppla från sessionen om de misstänker att kontot är obehörigt.|  
|Begränsa listan över tillåtna visningsprogram.|Behörighet som lokal administratör krävs inte för att en användare ska kunna använda fjärrstyrning.|  

### <a name="security-issues-for-remote-control"></a>Säkerhetsproblem vid fjärrstyrning  
 Hanteringen av klientdatorer via fjärrstyrning medför följande säkerhetsproblem:  

-   Lita inte på granskningsmeddelanden relaterade till fjärrstyrning.  

     Om du startar en fjärrstyrningssession och sedan loggar in med alternativa autentiseringsuppgifter skickas granskningsmeddelandena från det ursprungliga kontot, inte kontot som använde de alternativa autentiseringsuppgifterna.  

     Gransknings meddelanden skickas inte om du kopierar de binära filerna för fjärr styrning i stället för att installera Configuration Manager-konsolen och sedan kör fjärr styrning i kommando tolken.  

##  <a name="privacy-information-for-remote-control"></a><a name="BKMK_Privacy_HardwareInventory"></a> Sekretessinformation för fjärrstyrning  
 Med fjärr styrning kan du Visa aktiva sessioner på Configuration Manager klient datorer och eventuellt Visa all information som lagras på dessa datorer. Fjärrstyrning är inte aktiverat som standard.  

 Du kan konfigurera fjärrstyrning så att tydliga meddelanden visas och så att användarens tillstånd krävs innan en fjärrstyrningssession börjar, men fjärrstyrningstjänsten kan också övervaka användare utan deras tillstånd eller kännedom. Du kan ange åtkomstnivån Visa endast så att ingenting kan ändras i fjärrstyrning, eller välja Fullständig behörighet. Kontot för administratören som ansluter visas i fjärrstyrningssessionen så att användarna ser vem som ansluter till deras datorer.  

 Som standard beviljar Configuration Manager den lokala administratörs gruppen behörigheten fjärr styrning.  

 Innan du konfigurerar fjärrstyrning måste du ta hänsyn till integritetskraven.  
