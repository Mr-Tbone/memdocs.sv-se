---
title: Hanterings uppgifter för program
titleSuffix: Configuration Manager
description: Hantera Configuration Manager program och distributions typer.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0896204fa994643064676b55b20d63d349c4098b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710120"
---
# <a name="management-tasks-for-configuration-manager-applications"></a>Hanterings uppgifter för Configuration Manager program

*Gäller för: Configuration Manager (aktuell gren)*

Använd informationen i den här artikeln som hjälp för att hantera Configuration Manager program och distributions typer.  

Information om hur du skapar program och distributions typer finns i [skapa program](../../apps/deploy-use/create-applications.md).  

> [!IMPORTANT]  
>  Beroende på typen av program eller distributions typ kan vissa hanterings alternativ inte vara tillgängliga.  

##  <a name="manage-applications"></a>Hantera program  
 I arbets ytan **program bibliotek** expanderar du **program hanterings** > **program**, väljer det program som ska hanteras och väljer sedan en hanterings aktivitet.  

|Uppgift|Information|  
|----------|-------------|  
|**Hantera åtkomstkonton**|Öppnar dialogrutan **Hantera åtkomstkonton** där du kan specificera den behörighetsnivå som tillåts för det innehåll som förknippas med det valda programmet.|  
|**Skapa förinstallerad innehålls fil**|Öppnar **Guiden Skapa förinstallerad innehållsfil** som hjälper dig att hantera distributionen av innehåll till fjärrdistributionsplatser. När schemaläggningen och begränsning inte ger en giltig lösning för fjärrdistributionsplatsen kan du förinstallera innehållet på distributionsplatsen<br /><br /> Se [Hantera innehåll och innehålls infrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Revisionshistorik**|Öppnar dialog rutan **program revisions historik** där du kan visa egenskaperna för revisioner som har gjorts i programmet, ta bort gamla program revisioner och återställa gamla versioner av det här programmet.<br /><br /> Se [ändra och ersätta program](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Skapa distributionstyp**|Öppnar **guiden skapa distributions typ** där du kan lägga till en ny distributions typ i det valda programmet.<br /><br /> Se [skapa program](../../apps/deploy-use/create-applications.md).|  
|**Uppdatera statistik**|Uppdaterar informationen som visas i noden **Distributioner** i arbetsytan **Övervakning** om distributionerna av det här programmet.<br /><br /> Se [övervaka program från Configuration Manager-konsolen](../../apps/deploy-use/monitor-applications-from-the-console.md).|  
|**Återinför**|Återställer ett program som har dragits tillbaka med hjälp av åtgärden för att **dra tillbaka** hantering.|  
|**Pensionera**|När du drar tillbaka ett program är det inte längre tillgängligt för distribution, men program och distributioner av programmet tas inte bort. Befintliga kopior av programmet som är installerade på klientdatorerna tas inte bort. Alla ändringar i programmet tas bort från Configuration Manager efter 60 dagar. Men installerade kopior av programmet tas inte bort.<br /><br /> Om du vill ta bort ett program måste du först återkalla programmet, ta bort alla distributioner, ta bort referenser till programmet från andra distributioner och sedan ta bort alla programmets revisioner.<br /><br /> Se [omarbeta och ersätt program](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Exportera**|Öppnar **guiden Exportera program** som låter dig exportera de valda programmen till en. zip-fil som du sedan kan arkivera eller installera på en annan plats. Om du väljer att exportera program innehåll skapas en mapp som innehåller innehållet.<br /><br /> Du kan också exportera program beroenden, ersättnings förhållanden och-villkor och innehåll för programmet och dess beroenden.<br /><br /> Windows PowerShell-cmdleten **export-CMApplication**, utför samma funktion. Mer information finns i [export-CMApplication](https://go.microsoft.com/fwlink/p/?LinkID=258880) i referens dokumentationen för Microsoft System Center 2012 Configuration Manager SP1-cmdlet.|  
|**Ta bort**|Raderar det program som valts för tillfället.<br /><br /> Du kan inte radera ett program om andra program är beroende av det, om det har en aktiv distribution eller om det har beroende aktivitetssekvenser.|  
|**Simulera distribution**|Öppnar **Guiden simulera programdistribution** där du kan testa resultaten av programvarudistribution för datorer utan att installera eller avinstallera programmet.<br /><br /> Se [simulera program distributioner](../../apps/deploy-use/simulate-application-deployments.md).|  
|**Distribuera**|Öppnar **Guiden Distribuera programvara** där du kan distribuera det valda programmet till datorsamlingar i din hierarki.<br /><br /> Se [distribuera program](../../apps/deploy-use/deploy-applications.md).|  
|**Distribuera innehåll**|Öppnar **Guiden Distribuera innehåll** där du kan kopiera innehållet för det valda programmet till distributionsplatser i hierarkin.<br /><br /> Se [Hantera innehåll och innehålls infrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Visa relationer**|Visar ett grafiskt diagram över relationerna mellan de valda programmen och andra program. Välj något av följande:<br><br><ul><li>**Beroende** – visar program som är beroende av det valda programmet och de program som det valda programmet är beroende av.</li><li>**Ersättnings** – visar program som det valda programmet ersätter och program som det valda programmet har ersatts av.</li><li>**Globala villkor** – visar de globala villkor som det här programmet refererar till.</li></ol><br /> Se [omarbeta och ersätt program](../../apps/deploy-use/revise-and-supersede-applications.md) och [skapa globala villkor](../../apps/deploy-use/create-global-conditions.md).|  
|**Kopiera program**|Kopiera eller duplicera Configuration Manager program för att skapa en ny. Den här åtgärden är användbar för att testa något eller när du behöver skapa ett liknande program. Webbplatsen skapar ett nytt program med **-copy** som lagts till i namnet. Även om platsen kopierar de flesta metadata till det nya programmet, kopieras inga distributioner.|

##  <a name="manage-deployment-types"></a>Hantera distributions typer  
 I arbets ytan **program bibliotek** expanderar du **program hantering**, väljer **program**och väljer sedan det program som har den distributions typ som du vill hantera. I informations fönstret väljer du fliken **distributions typer** , väljer den distributions typ som du vill hantera och väljer sedan en hanterings aktivitet.  

|Uppgift|Information|  
|----------|-------------|  
|**Öka prioritet**|Ökar prioriteten hos den valda distributionstypen. Distributionstyper utvärderas i ordning. När en distributions typ uppfyller de angivna kraven körs den och inga ytterligare distributions typer på prioritets listan kommer att utvärderas.|  
|**Minska prioritet**|Minskar prioriteten hos den valda distributionstypen.|  
|**Ta bort**|Raderar den valda distributionstypen.<br><br>Du kan inte radera en distributionstyp om en distributionstyp i ett annat program refererar till den.<br>Om du vill ta bort en distributions typ måste du ta bort alla beroenden till distributions typen som finns i andra distributions typer.<br>Dessutom måste du också ta bort tidigare revisioner av alla program som har en distributions typ som refererar till den distributions typ som du vill ta bort.|  
|**Uppdatera innehåll**|Uppdaterar innehållet för den valda distributionstypen.<br /><br /> När du startar den här guiden för en distributions typ som har ett virtuellt program startas **guiden Uppdatera innehåll** . Med den här guiden kan du ändra publicerings alternativ och krav regler för det valda virtuella programmet. Mer information finns i [skapa program](../../apps/deploy-use/create-applications.md).<br /><br /> När du uppdaterar innehållet för en distributionstyp skapas en ny revision av programmet. Det kan leda till att klientenheterna uppdateras med det nya programmet.|  
